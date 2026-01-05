This file provides guidance to LLM agents like Claude Code and Gemini when working with code in this repository.

## Project Overview

Loomium is a full-stack Next.js application serving as a multi-tenant portal integrating with Flex Rental Solutions. It
provides a "mission control" dashboard with marketplace, educational content (Loomi-U), operational tools, and reporting
features.

**Active Feature Development:**

- [Filmwerks SketchUp Import Feature](./docs/pm/sketchup-import-feature-knowledge-base.md)

**Tech Stack:**

- **Frontend:** Next.js 12, React 18, Chakra UI, Emotion, Framer Motion, SASS
- **State Management:** Zustand, React Hook Form
- **Backend:** Next.js API Routes, Node.js 18.x
- **Database:** MySQL with Sequelize ORM
- **Authentication:** NextAuth.js (custom Flex Rental Solutions provider + Google OAuth)
- **CMS:** Sanity.io
- **Payments:** Stripe
- **Error Monitoring:** Sentry
- **Testing:** Jest (unit), Playwright (E2E)

## Development Commands

### Setup and Development

```sh
# Install dependencies
pnpm install

# Run development server
pnpm dev

# Application available at http://localhost:3000
```

### Build and Production

```sh
# Create production build
pnpm build

# Start production server
pnpm start
```

### Code Quality

```sh
# Lint codebase
pnpm lint
```

### Testing

**Jest (Unit Tests):**

```sh
# Run all Jest tests with coverage
pnpm test
```

- Config: `jest.config.js`
- Uses Next.js Jest configuration
- Setup file: `setupTests.js`
- Coverage collected from all `.js` and `.jsx` files

**Playwright (E2E Tests):**

```sh
# Run E2E tests
npx playwright test

# Run specific test file
npx playwright test tests/e2e/import.spec.ts

# Run with UI mode
npx playwright test --ui

# View test report
npx playwright show-report
```

- Config: `playwright.config.ts`
- Test directory: `tests/`
- Base URL: `http://localhost:3000`
- Runs on chromium, firefox, webkit

## Architecture

### Application Structure

**Pages and Routing:**

- `pages/` - Next.js pages and routing
- `pages/api/` - API routes organized by domain:
    - `auth/` - NextAuth.js authentication
    - `main/` - Main application APIs
    - `mission-control/` - MC-specific endpoints
    - `marketplace/` - Marketplace functionality
    - `loomiu/` - Educational content
    - `reports/` - Reporting functionality
    - `sanity/` - Sanity CMS integration
    - `netsuite/` - NetSuite integration
    - `billing-portal/` - Stripe billing

**Source Organization (`src/`):**

- `components/` - React components organized by domain:
    - `Global/` - Application-wide components and observers
    - `Layout/` - Reusable layout components
    - `Main/` - Main application features
- `context/` - React Context providers:
    - `main/` - Main application context
    - `missionControl/` - MC-specific context
    - `casl/` - Permissions context
- `store/` - Zustand stores organized by feature
- `models/` - Sequelize database models (~38 models)
- `db/connection/` - Database connection configuration
- `hooks/` - Custom React hooks
- `utils/` - Utility functions
- `sanity-queries/` - Sanity CMS queries
- `chakraTheme/` - Chakra UI theme configuration
- `assets/` - Static assets

### Key Architectural Patterns

**Application Initialization (`pages/_app.tsx`):**
The app uses a provider hierarchy:

1. `ChakraProvider` - UI theming
2. `SessionProvider` - NextAuth.js session
3. `AbilityContextProvider` - CASL permissions
4. `MCProvider` - Mission Control context
5. `MainProvider` - Main application context

**Observer Pattern:**
Global observer components in `_app.tsx` listen for state changes:

- `NewCustomerProcessObserver` - New customer signup flow
- `SubscriptionPurchaseObserver` - Subscription purchases
- `SignUpProcessObserver` - User signup flow
- `EnableProductProcessObserver` - Product enablement
- `MarketplaceConfig` - Marketplace configuration

**Route-Based Layout:**

- Routes WITH main menu: Application pages
- Routes WITHOUT main menu: Login, signup, checkout, widget config
- Mission Control routes use a separate menu system

**Authentication:**

- NextAuth.js with custom credential provider for Flex Rental Solutions
- Google OAuth for admin users (restricted to `@flexrentalsolutions` domain)
- Customer authentication via encrypted API keys stored in MySQL
- API key encryption/decryption using `FA_SECRET` passphrase

**Database Models:**

- Sequelize ORM with MySQL
- Models organized by domain (e.g., `mission-control/`, `workload/`, `toolbox/`)
- Connection configured via environment variables
- Uses `mysql2` dialect

**State Management:**

- Zustand stores in `src/store/` organized by feature
- Context API for auth, permissions, and application-wide state
- Observer components trigger updates based on store changes

**Permissions:**

- CASL library for ability-based access control
- `CanWrapper` component for conditional rendering
- Permissions checked client-side based on user role and session

**Content Management:**

- Sanity.io for structured content
- Queries in `src/sanity-queries/`
- Image optimization via Sanity CDN

**Styling:**

- Chakra UI component library with custom theme
- SCSS for global styles (`styles/globals.scss`)
- Emotion for CSS-in-JS
- Montserrat font (weights: 400, 500, 600, 700, 800)

**TypeScript Configuration:**

- Strict mode enabled
- Base URL: `./src` for absolute imports
- Path alias: `@/assets/*` maps to `/assets/*`

## Development Conventions

### Routing and Pages

**Pages are code-based, NOT created in Sanity:**

- Sanity.io is used ONLY for CMS content (articles, courses, marketing pages)
- Application features are built as **code** in `pages/` directory
- Each file in `pages/` becomes a route automatically (Next.js file-based routing)

**Pattern for creating a new page:**

1. Create file: `pages/[path]/index.tsx` (e.g., `pages/operations/sketchup-import/index.tsx`)
2. Export a NextPage component
3. Add route constant to `src/constants/routes.ts`
4. Wrap content with `PageSEOWrapper` from `components/Layout/PageSEOWrapper`
5. Use `Can` component from `components/Layout/CanWrapper` for permission checks
6. Check authentication with `getOAuthKeys(session)?.access_token`

**Example page structure:**

```typescript
import type { NextPage } from "next";
import { useSession } from "next-auth/react";
import PageSEOWrapper from "components/Layout/PageSEOWrapper";
import Can from "components/Layout/CanWrapper";
import getOAuthKeys from "utils/flex/getOAuthKeys";

const MyFeaturePage: NextPage = () => {
  const session = useSession();
  const hasAccessToken = getOAuthKeys(session)?.access_token;

  return (
    <PageSEOWrapper title="Feature Name" description="Description">
      {hasAccessToken ? (
        <Can I="read" a="feature_module">
          {/* Your feature component */}
        </Can>
      ) : (
        <NeedToLoginMessage />
      )}
    </PageSEOWrapper>
  );
};

export default MyFeaturePage;
```

### File Upload Pattern

The codebase uses `react-dropzone` and `formidable` for file uploads:

**Frontend pattern** (see `src/components/Main/Support/CreateTicket/ModalNewTicket/UploadFile/index.tsx`):

```typescript
import { useDropzone } from "react-dropzone";

const { getRootProps, getInputProps, acceptedFiles } = useDropzone({
  accept: { 'text/csv': ['.csv'] },
  maxSize: 25 * 1024 * 1024, // 25MB
  onDrop: (acceptedFiles, rejections) => {
    // Handle files
  }
});

// Upload to API
const uploadFile = async (file: File) => {
  const formData = new FormData();
  formData.append("file", file);

  await fetch("/api/your-endpoint/upload", {
    method: "POST",
    body: formData,
  });
};
```

**Backend API pattern** (see `pages/api/support/upload-file/index.tsx`):

```typescript
import formidable from "formidable";
import { getSession } from "next-auth/react";

export const config = {
  api: {
    bodyParser: false, // REQUIRED for formidable
  },
};

export default async function handler(req: NextApiRequest, res: NextApiResponse) {
  const session: any = await getSession({ req });
  const oAuthKeys = getOAuthKeys(session, req.headers.cookie);

  if (!oAuthKeys?.user_id) {
    return res.status(401).end();
  }

  const form = new formidable.IncomingForm();
  form.parse(req, async (err, fields, files) => {
    // Process files.file
  });

  res.status(200).json({ response: true });
  res.end();
}
```

### Flex API Integration Pattern

All Flex API calls use `flexOAuth2Request` utility (see `src/utils/flex/flexOAuth2Request/index.ts`):

```typescript
import { flexOAuth2Request } from "utils/flex/flexOAuth2Request";

// GET request
const data = await flexOAuth2Request(
  session,
  "element/123", // Relative URL (base is https://{flex_instance}/f5/api/)
  "GET"
);

// POST request
const result = await flexOAuth2Request(
  session,
  "element",
  "POST",
  { name: "New Element", definitionId: 42 }
);

// PUT request
const updated = await flexOAuth2Request(
  session,
  "element/123",
  "PUT",
  { status: "In Progress" }
);
```

**How it works:**

- Automatically adds `X-Auth-Token` header from session
- Automatically adds `X-Api-Client: squarewave` header
- Base URL: `https://{flex_instance}/f5/api/{url}`
- Returns parsed JSON or text based on content-type
- Logs to Google Analytics
- Sends errors to Sentry
- Session contains: `access_token`, `user_id`, `flex_instance`

### Import Paths

Use absolute imports from `src/` directory:

```typescript
import { MCAdminUser } from "models/mission-control/MCAdminUser";
import useGlobalErrorsListener from "hooks/pageWrapper/useGlobalErrorsListener";
```

### Component Organization

- Components use index.tsx pattern
- Custom hooks often in separate files (e.g., `useComponentName.tsx`)
- Helper functions in dedicated files within component directories

### API Routes

- Follow Next.js API route conventions
- Organize by domain in `pages/api/`
- Use Sequelize models for database access
- Handle authentication via NextAuth session

### Database Models

- Define in `src/models/` organized by domain
- Use Sequelize DataTypes
- Include timestamps: false if not using created_at/updated_at
- Specify tableName explicitly

### Testing Patterns

- E2E tests check authentication requirements
- Tests organized in `tests/` directory
- Use descriptive test names
- Verify visible UI elements with accessibility queries

### Error Monitoring

- Sentry integrated for both client and server
- Error boundaries should be in place
- Use `useGlobalErrorsListener` hook for global error handling

## Common Tasks

### Adding a New API Route

1. Create file in appropriate `pages/api/` subdirectory
2. Import required models from `src/models/`
3. Use NextAuth session for authentication
4. Return appropriate status codes and JSON responses

### Adding a New Database Model

1. Create model file in `src/models/[domain]/[ModelName]/index.ts`
2. Import `db` from `db/connection`
3. Define schema with Sequelize DataTypes
4. Export model for use in API routes

### Adding a New Page

1. Create page in `pages/` directory
2. Add route constant to `constants/routes`
3. Update `_app.tsx` route arrays if layout differs
4. Wrap with appropriate SEO wrapper

### Working with Permissions

1. Use `CanWrapper` component for conditional rendering
2. Check abilities via CASL context
3. Permissions defined in security groups and user overrides

### Sanity Content Integration

1. Create query in `src/sanity-queries/`
2. Use `@sanity/client` for fetching
3. Render with `@portabletext/react` for rich text
4. Use `SanityImage` component for images
