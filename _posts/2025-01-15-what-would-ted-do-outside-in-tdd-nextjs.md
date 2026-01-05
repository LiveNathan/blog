---
layout: post
title: "What Would Ted Do? Outside-In TDD for Next.js Feature Development"
date: 2025-01-15 00:00:00 -0000
categories: [ tdd, nextjs, typescript, workflow, ted-young ]
---

## The Challenge

You know Test-Driven Development in Java. You know Spring Boot, Vaadin, and hexagonal architecture. You've studied Ted
M. Young's (JitterTed's) outside-in workflow extensively. Now you're staring at a Next.js codebase thinking: *Can I even
do TDD here? Does this workflow translate?*

**Short answer:** Yes. The principles translate. The tools differ.

This guide maps Ted's outside-in TDD workflow to Next.js development. It's not a TypeScript tutorial—it's a step-by-step
plan for building features the "Ted way" in an unfamiliar ecosystem.

**What makes this guide different:** I wrote the initial version *before* building any features (pure prediction), then
updated it with real code after completing a production feature (136 tests, ~2000 lines of code). The blog post shows
both my predictions and what actually happened—including what I got wrong. See
the [Retrospective section](#retrospective-predictions-vs-reality) for the full comparison.

**Note on Next.js Version:** This guide was originally written speculatively before building any features. The actual
implementation described here uses **Next.js 16 with the Pages Router** (`pages/` directory). The core TDD workflow
translated perfectly. If you're using the App Router (`app/` directory), the core TDD workflow remains the same, but
file organization and some APIs differ. The principles translate—the file paths change.

## Table of Contents

1. [The Quick Reference](#quick-reference)
2. [Can You Do TDD in Next.js?](#can-you-do-tdd-in-nextjs)
3. [The Outside-In Workflow for Next.js](#the-outside-in-workflow)
4. [Running Example: SketchUp Import Feature](#running-example)
5. [Step-by-Step: Building the Feature](#step-by-step)
6. [Java → Next.js Translation Guide](#translation-guide)
7. [Safety Nets & Confidence Builders](#safety-nets)
8. [**Retrospective: Predictions vs. Reality**](#retrospective-predictions-vs-reality) ⭐
9. [Resources](#resources)

---

## Quick Reference

When you're stuck and need to know "what's next?", use this:

**Starting a new feature:**

1. Write IO-Based test (Playwright) for endpoint accessibility → Should FAIL
2. Create Next.js page file → IO test PASSES. Refactor step omitted for brevity.
3. Write IO-Based test for UI interaction → Should FAIL
4. Add minimal UI component → IO test PASSES
5. Write IO-Based test for form submission → Should FAIL (no API endpoint)
6. **Drop down:** Write API route test (Jest, IO-Based) → Should FAIL
7. Create API route handler → API test PASSES
8. **Drop down:** Write service/util test (Jest, IO-Free) → Should FAIL
9. Implement service logic → Service test PASSES
10. **Back up:** IO-Based form submission test → Should PASS now
11. Refactor, commit, repeat for next increment

**When tests are green at current layer:** Move up one layer.
**When tests fail and you can't make them pass:** Drop down one layer.

---

## Can You Do TDD in Next.js?

Your fears are valid. The JavaScript/TypeScript ecosystem doesn't have the same testing culture as Java. But here's what
you need to know:

### Yes, You Can Do TDD in Next.js

**Testing Tools Available:**

- **Playwright** - IO-Based tests. Spins up the entire Next.js application and tests via real browser automation. This
  is your `@SpringBootTest` equivalent (full application context).
- **Jest** - Both IO-Free and IO-Based tests. This is your JUnit equivalent.
- **React Testing Library** - Component testing (optional, we'll mostly use Playwright for UI)

**Test Categorization (Ted's IO-Free vs IO-Based):**

> Note that I have not used the term unit and integration test. Those terms are terrible. Every time somebody says
> unit, I say, "What do you mean? What is a unit?" And you can get into a debate, but that gets you nowhere. Not
> important. What's important is if it uses IO or not. To me, that's all that matters." - Ted M. Young

- **IO-Free tests (Jest):** Pure business logic, transformations, calculations. No framework, no database, no HTTP, no
  file system. These run in microseconds and have no mocks or test doubles.
- **IO-Based tests (Jest & Playwright):** Tests that touch IO - HTTP requests, database calls, file uploads, the Next.js
  framework itself. These are slower but necessary for adapter layers.

### Setting Up Your Test Environment

In a Java project you might separate your tests using `@Tag` annotations. The in Intellij create two run configurations.
In Next.js, you can do this with different run scripts.

```json
{
  "scripts": {
    "test": "jest",
    "test:watch": "jest --watch",
    "test:e2e": "playwright test",
    "test:e2e:ui": "playwright test --ui",
    "test:all": "pnpm test && pnpm test:e2e"
  }
}
```

**Script explanations:**

- `test` - Run all Jest tests (IO-Free + IO-Based Jest tests)
- `test:watch` - Run Jest in watch mode (auto-reruns tests on file changes for continuous TDD feedback)
- `test:e2e` - Run Playwright tests headlessly
- `test:e2e:ui` - Run Playwright in UI mode (launches graphical test explorer interface)
- `test:all` - Run everything (Jest + Playwright)

**Test running philosophy** (following Ted's approach):

- Run IO-Free tests (Jest unit tests) **constantly** - they're microseconds fast
- Run IO-Based tests (Jest API tests + Playwright) **periodically** - they're slower but necessary
- The separation lets you get rapid feedback on business logic while still having confidence in integration points

### Key Differences from Java/Spring

| Java/Spring Pattern         | Next.js Equivalent                   | Test Type | Notes                                          |
|-----------------------------|--------------------------------------|-----------|------------------------------------------------|
| `@SpringBootTest`           | Playwright test                      | IO-Based  | Tests full app via real HTTP + browser         |
| `@WebMvcTest` with MockMvc  | Jest test of API route handler       | IO-Based  | Import and call handler directly (no HTTP)     |
| Direct controller test      | Jest test of API route handler       | IO-Based  | Same as above - directly invoke the function   |
| Domain service test         | Jest test of utility function        | IO-Free   | Pure functions in `utils/` or `services/`      |
| `@Tag("io")` for slow tests | Separate test commands               | -         | `npx playwright test` vs `pnpm test`           |
| TestContainers              | TestContainers (works with Next.js!) | IO-Based  | See [varianter/testcontainers-nextjs-template] |
| WireMock                    | msw (Mock Service Worker) or nock    | IO-Based  | msw preferred for modern JS HTTP mocking       |

### Questions Answered

**Q: Do Next.js apps have endpoints?**
A: Yes. Files in `pages/api/` become HTTP endpoints. `pages/api/import/process.ts` → `POST /api/import/process`

**Q: Is there a domain layer?**
A: Not by default, but you should create one. Put pure business logic in `src/domain/` for true hexagonal architecture.
Keep it framework-free and IO-free. The typical Next.js pattern of mixing everything in `utils/` or `services/` defeats
the purpose of separation. Consider:

- `src/domain/` - Pure business logic (IO-Free, no framework dependencies)
- `src/application/` - Use case coordination (knows about domain, references IO via interfaces)
- `src/adapters/` - Framework adapters (API routes, database access, external services)

**Q: Do we use DTOs or domain objects?**
A: Both. TypeScript interfaces for API contracts (DTOs), separate objects for business logic.

**Q: How do we handle authentication in tests?**
A: Playwright can log in once and reuse session. Jest tests can mock `getSession()`.

**Q: Can we do outside-in TDD?**
A: Absolutely. Start with Playwright (edge), drop to Jest (internals), work your way back up.

---

## The Outside-In Workflow

Ted's workflow adapted for Next.js:

```
┌─────────────────────────────────────────────┐
│  Layer 1: Playwright (IO-Based)             │
│  • Page accessibility                       │
│  • UI rendering                             │
│  • Form submission                          │
│  • Full happy path                          │
│                                             │
│  Test: tests/e2e/csv-import.spec.ts        │
│  Tool: Playwright                           │
│  Speed: Slow (seconds)                      │
│  IO: HTTP, server, framework, database      │
│  When: Start here, return here             │
└─────────────────────────────────────────────┘
                    ↓ (test fails, need API)
┌─────────────────────────────────────────────┐
│  Layer 2: API Routes (Jest, IO-Based)       │
│  • Request parsing                          │
│  • Validation                               │
│  • Response formatting                      │
│  • Status codes                             │
│                                             │
│  Test: pages/api/import/__tests__/         │
│  Tool: Jest                                 │
│  Speed: Fast (milliseconds)                 │
│  IO: Next.js framework, possibly database   │
│  When: Playwright test needs backend        │
└─────────────────────────────────────────────┘
                    ↓ (test fails, need logic)
┌─────────────────────────────────────────────┐
│  Layer 3: Services/Utils (Jest, IO-Free)    │
│  • Business logic                           │
│  • Transformations                          │
│  • Pure functions                           │
│  • Domain rules                             │
│                                             │
│  Test: src/utils/csvImport/__tests__/      │
│  Tool: Jest                                 │
│  Speed: Very fast (microseconds)            │
│  IO: NONE - no mocks, no test doubles      │
│  When: API test needs logic                 │
└─────────────────────────────────────────────┘
```

**Test Organization:** This guide uses **co-located tests** with `__tests__` folders next to the code being tested. This
keeps tests close to implementation and makes them easier to find. For IO-Based Playwright tests, use a dedicated
`tests/` directory since they test across multiple files and layers.

**The Flow:**

1. Start at the edge (Playwright IO-Based test)
2. Test fails because feature doesn't exist
3. Add minimal code to make it pass
4. When you need logic that doesn't exist, drop down a layer
5. Write test at that layer, implement, get it green. Refactor.
6. Come back up, original test should pass now. Refactor.

> "What I'm doing is sort of this outside in development. I'm trying to figure out what the web UI needs from the
> service and then I can start test driving." - Ted M. Young

**Important Distinction: Automated vs Manual Testing**

Ted's approach uses automated tests for slices of the application (IO-Free domain logic, IO-Based adapters) but
often relies on manual testing for full end-to-end flows. He says, "I don't find end-to-end tests being
all that useful to automate. Manually running stuff. That's a test. It's just not an automated test."

In this guide, we're using Playwright to automate tests at the application boundary. Playwright **does** spin up the
entire Next.js application (development server) and test through a real browser - this is a true end-to-end test.
However, we're using it strategically for specific user flows rather than trying to test every possible path through
the UI. You'll still want to manually test the complete application in a production-like environment periodically, as
Playwright tests run against the dev server, not your actual production stack.

---

## Running Example

**Feature:** Import SketchUp CSV exports into Flex Rental Solutions Pull Sheets

**User Story:**
As a user, I want to upload a SketchUp CSV export so that I can bulk-create Pull Sheets with inventory and custom notes
in Flex Rental Solutions without manual entry.

**Acceptance Criteria:**

- User can access the import page (authenticated only)
- User can select a CSV file
- User can specify a target element number (Quote, Event Folder, or existing Pull Sheet)
- System validates CSV format and element number
- System matches CSV barcodes to Flex inventory
- System creates or replaces Pull Sheets with line items
- System handles both inventory items and custom note lines
- User sees detailed results page with success/error summary

**CSV Format:**

```csv
Status,Definition Name,Quantity,Tag
100001,LED Panel,5,
100002,Audio Cable,10,
CUSTOM,Special rigging note,1,Production Notes
```

**Note:** This is a real feature built for production, not a tutorial example. All code samples are from the actual
implementation.

---

## Step-by-Step

### Phase 1: Page Accessibility (IO-Based Layer)

**Goal:** Confirm authenticated users can reach the page.

**What Ted Would Do (Java/Spring):**

```java

@WebMvcTest(ImportController.class)
@Tag("io")
class ImportMvcTest {
    @Test
    void getToImportPageReturns200() {
        mockMvc.perform(get("/import"))
                .andExpect(status().is2xxSuccessful());
    }
}
```

**Next.js Equivalent (Real Production Code):**

```typescript
// tests/e2e/sketchup-import/sketchup-import-access.spec.ts
import {expect, test} from '../../fixtures/mockFlexApi';

test.describe('Authentication', () => {
  test.describe('Unauthenticated Access', () => {
    // Reset the storage state for this test to avoid being authenticated
    test.use({storageState: {cookies: [], origins: []}});

    test('unauthenticated user is shown a login prompt on a protected page', async ({page}) => {
      await page.goto('/operations/sketchup-import');
      await expect(page.getByRole('heading', {
        name: "You need to login to see this page"
      })).toBeVisible();
    });
    });

  test.describe('Authenticated Access', () => {
    test('authenticated user sees SketchUp Import title', async ({page}) => {
      await page.goto('/operations/sketchup-import');
      await expect(page.getByRole('heading', {name: 'SketchUp Import'})).toBeVisible();
    });
    });
});
```

**Key Differences from Prediction:**

- Uses `mockFlexApi` fixture to avoid hitting real API (critical for preventing rate limits)
- Uses `storageState` pattern for auth instead of filling login form each time
- Simpler assertion - just checks heading visibility
- Authentication handled by Playwright global setup (more efficient)

**Run the test:**

```bash
npx playwright test tests/e2e/csv-import/accessibility.spec.ts
```

**Expected result:** ❌ FAIL (page doesn't exist)

**Make it pass (Real Implementation):**

```typescript
// pages/operations/sketchup-import/index.tsx
import {Heading, VStack} from "@chakra-ui/react";
import PageSEOWrapper from "components/Layout/PageSEOWrapper";
import NeedToLoginMessage from "components/Main/NeedToLoginMessage";
import {userStatus} from "constants/userStatus";
import {pagesNames} from "constants/pagesNames";
import useTypeOfUser from "hooks/useTypeOfUser";

function SketchUpImport() {
  const typeOfUser = useTypeOfUser();

  return (
          <PageSEOWrapper
                  title = {pagesNames.SKETCHUP_IMPORT}
  description = {pagesNames.SKETCHUP_IMPORT}
          >
          {typeOfUser !== userStatus.NOUSER && (
                  <VStack align = "stretch"
  gap = {6}
  maxW = "600px"
  w = "100%"
  px = {
  {
    base: "4", md
  :
    "6", xl
  :
    "8"
  }
}
  py = "6" >
  <Heading as = "h1" > SketchUp
  Import < /Heading>
  {/* Form components will go here */
  }
  </VStack>
)
}

  {
    typeOfUser === userStatus.NOUSER && <NeedToLoginMessage / >
  }
  </PageSEOWrapper>
)
  ;
}

export default SketchUpImport;
```

**Key Differences from Prediction:**

- Uses client-side auth check (`useTypeOfUser` hook) instead of `getServerSideProps`
- This is the Loomium pattern - simpler and works well with NextAuth
- Uses Chakra UI components (`VStack`, `Heading`) for consistent styling
- Shows `NeedToLoginMessage` component instead of redirecting to login
- No TypeScript `NextPage` type (not needed in this pattern)

**Run the test again:**

```bash
npx playwright test tests/e2e/csv-import/accessibility.spec.ts
```

**Expected result:** ✅ PASS

Commit to git.

There is an important refactor step that happens here as part of the TDD loop. I have omitted it for brevity.

---

### Phase 2: File Upload UI (IO-Based Layer)

**Goal:** User can select a CSV file and see it in the UI.

**What Ted Would Do:**
Continue at IO-Based layer testing the UI interaction. In Java/Spring with Thymeleaf, he'd use MockMvc to check that the
form backing object is present in the model.

```java
@WebMvcTest(ImportController.class)
@Tag("io")
class ImportMvcTest {
    @Autowired MockMvc mockMvc;

    @Test
    void importPageShowsFileUploadForm() throws Exception {
        mockMvc.perform(get("/import"))
               .andExpect(status().isOk())
               .andExpect(view().name("import"))
               .andExpect(model().attributeExists("importForm"));
    }
}
```

**Next.js Equivalent (Playwright):**

In React/Next.js, we test the rendered DOM with Playwright.

```typescript
// tests/e2e/csv-import/file-upload.spec.ts
import {test, expect} from '@playwright/test';
import path from 'path';

test.describe('CSV Import - File Upload', () => {
    test.beforeEach(async ({page}) => {
        // Assume authenticated (use Playwright's storage state)
        await page.goto('/operations/csv-import');
    });

    test('displays file upload dropzone', async ({page}) => {
        await expect(page.locator('[data-testid="csv-dropzone"]')).toBeVisible();
        await expect(page.getByText('Drop CSV file here')).toBeVisible();
    });

    test('accepts CSV file and displays filename', async ({page}) => {
        // Create test CSV file path
        const filePath = path.join(__dirname, 'fixtures', 'valid-import.csv');

        // Upload file
        const fileInput = page.locator('input[type="file"]');
        await fileInput.setInputFiles(filePath);

        // Verify file name is displayed
        await expect(page.getByText('valid-import.csv')).toBeVisible();
    });

    test('rejects non-CSV files', async ({page}) => {
        const filePath = path.join(__dirname, 'fixtures', 'invalid.txt');

        const fileInput = page.locator('input[type="file"]');
        await fileInput.setInputFiles(filePath);

        await expect(page.getByText('Only CSV files are accepted')).toBeVisible();
    });
});
```

**Create test fixture:**

```bash
mkdir -p tests/e2e/csv-import/fixtures
```

```csv
# tests/e2e/csv-import/fixtures/valid-import.csv
Barcode,Quantity,Notes
ABC123,5,Handle with care
XYZ789,2,
```

**Run the test:**

```bash
npx playwright test tests/e2e/csv-import/file-upload.spec.ts
```

**Expected result:** ❌ FAIL (no dropzone component)

**Make it pass:**

```typescript
// pages/operations/csv-import/index.tsx
import type {NextPage, GetServerSideProps} from 'next';
import {getSession} from 'next-auth/react';
import PageSEOWrapper from 'components/Layout/PageSEOWrapper';
import CSVUpload from 'components/Main/Operations/CSVImport/FileUpload';

const CSVImportPage: NextPage = () => {
    return (
        <PageSEOWrapper title = "CSV Import"
    description = "Import line items from CSV" >
        <h1>Import
    CSV < /h1>
    < CSVUpload / >
    </PageSEOWrapper>
)
    ;
};

export const getServerSideProps: GetServerSideProps = async (context) => {
    const session = await getSession(context);

    if (!session) {
        return {
            redirect: {
                destination: '/login',
                permanent: false,
            },
        };
    }

    return {
        props: {session},
    };
};

export default CSVImportPage;
```

```typescript
// src/components/Main/Operations/CSVImport/FileUpload/index.tsx
import {useDropzone} from 'react-dropzone';
import {useState} from 'react';
import {Box, Text} from '@chakra-ui/react';

const CSVUpload = () => {
    const [fileName, setFileName] = useState<string | null>(null);
    const [error, setError] = useState<string | null>(null);

    const {getRootProps, getInputProps} = useDropzone({
        accept: {'text/csv': ['.csv']},
        maxFiles: 1,
        onDrop: (acceptedFiles, rejectedFiles) => {
            setError(null);
            if (rejectedFiles.length > 0) {
                setError('Only CSV files are accepted');
                return;
            }
            if (acceptedFiles.length > 0) {
                setFileName(acceptedFiles[0].name);
            }
        },
    });

    return (
        <Box>
            <Box
                {...getRootProps()}
    data - testid = "csv-dropzone"
    border = "2px dashed"
    borderColor = "gray.300"
    p = {8}
    textAlign = "center"
    cursor = "pointer"
        >
        <input {...getInputProps()}
    />
    < Text > Drop
    CSV
    file
    here, or
    click
    to
    select < /Text>
    < /Box>
    {
        fileName && <Text mt = {2} > File
    :
        {
            fileName
        }
        </Text>}
        {
            error && <Text mt = {2}
            color = "red.500" > {error} < /Text>}
                < /Box>
        )
            ;
        }
        ;

        export default CSVUpload;
```

**Run the test:**

```bash
npx playwright test tests/e2e/csv-import/file-upload.spec.ts
```

**Expected result:** ✅ PASS

Commit. Refactor. Commit.

---

### Phase 3: Form Submission (IO-Based Layer → API Layer)

**Goal:** User can submit the form with CSV file and order number, then see results.

**What Ted Would Do:**
Write IO-Based test for POST submission. Test will fail because the API endpoint doesn't exist. This is the signal to
drop down to the API layer.

```java
@WebMvcTest(ImportController.class)
@Tag("io")
class ImportMvcTest {
    @Test
    void submittingCsvImportsItemsAndRedirects() throws Exception {
        MockMultipartFile csvFile = new MockMultipartFile(
            "file", "test.csv", "text/csv", "Barcode,Qty\n123,1".getBytes());

        mockMvc.perform(multipart("/import")
                .file(csvFile)
                .param("orderNumber", "ORD-123"))
                .andExpect(status().is3xxRedirection())
                .andExpect(redirectedUrl("/import/result"));
    }
}
```

**Note on POST-Redirect-GET Pattern:**
In production applications, form submissions typically follow the Post-Redirect-Get (PRG) pattern to prevent duplicate
submissions on browser refresh. The flow would be: POST form data → API processes → redirect to results page → GET
displays results. For this example, we're using a simpler client-side state update pattern to focus on the TDD
workflow, but you should consider PRG for real applications.

**IO-Based Test (Playwright):**

```typescript
// tests/e2e/csv-import/form-submission.spec.ts
import {test, expect} from '@playwright/test';
import path from 'path';

test.describe('CSV Import - Form Submission', () => {
    test.beforeEach(async ({page}) => {
        await page.goto('/operations/csv-import');
    });

    test('submits CSV and order number successfully', async ({page}) => {
        // Upload CSV
        const filePath = path.join(__dirname, 'fixtures', 'valid-import.csv');
        const fileInput = page.locator('input[type="file"]');
        await fileInput.setInputFiles(filePath);

        // Enter order number
        await page.fill('[name="orderNumber"]', 'ORD-12345');

        // Submit form
        await page.getByRole('button', {name: 'Import'}).click();

        // Expect success message
        await expect(page.getByText('Import completed successfully')).toBeVisible();
        await expect(page.getByText('2 items imported')).toBeVisible();
    });

    test('shows error for invalid order number', async ({page}) => {
        const filePath = path.join(__dirname, 'fixtures', 'valid-import.csv');
        const fileInput = page.locator('input[type="file"]');
        await fileInput.setInputFiles(filePath);

        await page.fill('[name="orderNumber"]', 'INVALID');
        await page.getByRole('button', {name: 'Import'}).click();

        await expect(page.getByText('Order not found')).toBeVisible();
    });
});
```

**Run the test:**

```bash
npx playwright test tests/e2e/csv-import/form-submission.spec.ts
```

**Expected result:** ❌ FAIL (no API endpoint, no form submit handler)

This is the signal to drop down to the API layer.

---

### Phase 4: API Route (IO-Based, Jest)

**Goal:** API endpoint accepts CSV file and order number, returns success/error.

**What Ted Would Do (Direct Controller Test, IO-Based):**

```java
class ImportControllerTest {
    @Test
    void processImportReturnsSuccessForValidInput() {
        ImportService service = new ImportService();
        ImportController controller = new ImportController(service);

        ImportResult result = controller.processImport("ORD-123", csvData);

        assertThat(result.success()).isTrue();
        assertThat(result.itemsImported()).isEqualTo(2);
    }
}
```

**Next.js Equivalent (Jest test of API route):**

```typescript
// pages/api/import/__tests__/process.test.ts
import {createMocks} from 'node-mocks-http';
import handler from '../process';
import formidable from 'formidable';

// Mock formidable for this IO-Based test
// Note: This is an IO-Based test at the API route layer (adapter layer in hexagonal terms)
// We're testing the request/response handling logic, not file system IO
// Using jest.mock() here is acceptable per Ted's guidance - we're simulating the file upload
// without actually writing to disk. The CSV parsing logic will be tested separately as IO-Free.
jest.mock('formidable');

describe('POST /api/import/process', () => {
    it('returns success for valid CSV file and order number', async () => {
        const mockParse = jest.fn((req, callback) => {
            callback(null,
                {orderNumber: 'ORD-12345'}, // fields
                {
                    file: [{
                        filepath: '/tmp/test.csv',
                        originalFilename: 'test.csv',
                        mimetype: 'text/csv'
                    }]
                } // files
            );
        });

        (formidable.IncomingForm as jest.Mock).mockImplementation(() => ({
            parse: mockParse
        }));

        const {req, res} = createMocks({
            method: 'POST',
            headers: {'content-type': 'multipart/form-data'},
        });

        await handler(req, res);

        expect(res._getStatusCode()).toBe(200);
        const data = JSON.parse(res._getData());
        expect(data.success).toBe(true);
    });

    it('returns 400 for invalid order number', async () => {
        const mockParse = jest.fn((req, callback) => {
            callback(null,
                {orderNumber: 'INVALID'},
                {file: [{filepath: '/tmp/test.csv'}]}
            );
        });

        (formidable.IncomingForm as jest.Mock).mockImplementation(() => ({
            parse: mockParse
        }));

        const {req, res} = createMocks({
            method: 'POST',
            headers: {'content-type': 'multipart/form-data'},
        });

        await handler(req, res);

        expect(res._getStatusCode()).toBe(400);
        const data = JSON.parse(res._getData());
        expect(data.error).toBe('Order not found');
    });
});
```

**Run the test:**

```bash
pnpm test pages/api/import/__tests__/process.test.ts
```

**Expected result:** ❌ FAIL (handler doesn't exist)

**Make it pass (minimal implementation):**

```typescript
// pages/api/import/process.ts
import type {NextApiRequest, NextApiResponse} from 'next';
import formidable from 'formidable';
import fs from 'fs/promises';

// Disable Next.js body parser - required for formidable
export const config = {
    api: {
        bodyParser: false,
    },
};

export default async function handler(
    req: NextApiRequest,
    res: NextApiResponse
) {
    if (req.method !== 'POST') {
        return res.status(405).json({error: 'Method not allowed'});
    }

    const form = formidable();

    form.parse(req, async (err, fields, files) => {
        if (err) {
            return res.status(500).json({error: 'File upload failed'});
        }

        const orderNumber = Array.isArray(fields.orderNumber)
            ? fields.orderNumber[0]
            : fields.orderNumber;

        // Hardcode for now to make test pass
        if (orderNumber === 'INVALID') {
            return res.status(400).json({error: 'Order not found'});
        }

        const uploadedFile = Array.isArray(files.file) ? files.file[0] : files.file;

        if (!uploadedFile) {
            return res.status(400).json({error: 'No file uploaded'});
        }

        // Read CSV content
        const csvData = await fs.readFile(uploadedFile.filepath, 'utf-8');

        if (!csvData.includes('Barcode')) {
            return res.status(400).json({error: 'Invalid CSV format'});
        }

        // Hardcoded success response
        return res.status(200).json({
            success: true,
            itemsImported: 1,
        });
    });
}
```

This uses [`formidable`](https://github.com/node-formidable/formidable) for multipart/form-data handling.

**What is formidable?** It's a Node.js library for parsing form data, especially file uploads. Next.js doesn't handle
multipart form data by default, so you need a library like formidable. It reads uploaded files from the HTTP request
and gives you access to both form fields and file metadata (path, mimetype, etc.).

**Run the test:**

```bash
pnpm test pages/api/import/__tests__/process.test.ts
```

**Expected result:** ✅ PASS

**Note:** This is hardcoded. Next step: drop down to service layer for real logic.

---

### Phase 5: Service/Util Layer (IO-Free, Jest)

**Goal:** Parse CSV, validate data, match barcodes to inventory.

**What Ted Would Do (IO-Free Domain/Service Tests):**

```java
class ImportServiceTest {
    @Test
    void parseCSVExtractsLineItems() {
        String csv = "Barcode,Quantity\nABC123,5\nXYZ789,2";

        List<LineItem> items = ImportService.parseCSV(csv);

        assertThat(items).hasSize(2);
        assertThat(items.get(0).barcode()).isEqualTo("ABC123");
        assertThat(items.get(0).quantity()).isEqualTo(5);
    }
}
```

**Next.js Equivalent (Real Production Code):**

```typescript
// src/utils/sketchupImport/__tests__/csvParser.test.ts
import {describe, expect, it} from "@jest/globals";
import {parseAndCleanCsv} from "../csvParser";

describe('parseAndCleanCsv', () => {
  describe('Domain Object Creation', () => {
    it('creates InventoryItem for rows with numeric Status', () => {
      const csvContent = `Status,Definition Name,Quantity
100001,Test Inventory Item,10`;

      const result = parseAndCleanCsv(csvContent);

      expect(result).toHaveLength(1);
      expect(result[0]).toEqual({
        type: 'inventory',
        barcode: '100001',
        quantity: 10,
        definitionName: 'Test Inventory Item'
      });
    });

    it('creates NoteLineItem for rows with non-numeric Status', () => {
      const csvContent = `Status,Definition Name,Quantity
CUSTOM,Custom Item Description,5`;

      const result = parseAndCleanCsv(csvContent);

      expect(result).toHaveLength(1);
      expect(result[0]).toEqual({
        type: 'note',
        description: 'Custom Item Description',
        quantity: 5,
        definitionName: 'Custom Item Description',
        tag: undefined
      });
    });
  });

  describe('Whitespace Handling', () => {
    it('givenCsvWithWhitespace_whenParsed_thenValuesAreTrimmed', () => {
      const csvContent = `  Status  ,  Definition Name  ,  Quantity
  100001  ,  Test Item With Spaces  ,  5
100002,Test Item Without Spaces,3`;

      const result = parseAndCleanCsv(csvContent);

      expect(result).toHaveLength(2);
      expect(result[0]).toEqual({
        type: 'inventory',
        barcode: '100001',
        quantity: 5,
        definitionName: 'Test Item With Spaces'
      });
    });
    });
});
```

**Key Differences from Prediction:**

- Uses discriminated union types (`type: 'inventory' | 'note'`) for type-safe parsing
- More sophisticated - handles two different domain types (inventory vs. notes)
- Test names use Given-When-Then pattern (influenced by TDD learning)
- No success/error result object - throws `ValidationError` for failures
- Uses Zod internally for validation (not shown but used in the implementation)

**Run the test:**

```bash
pnpm test src/utils/csvImport/__tests__/parseCSV.test.ts
```

**Expected result:** ❌ FAIL (function doesn't exist)

**Make it pass (Real Implementation):**

```typescript
// src/utils/sketchupImport/csvParser.ts
import {parse} from 'csv-parse/sync';
import {ParsedRow, ValidationError} from './types';
import {parseLineItem, RawCsvRow, validateCsvHeaders} from './validation';

/**
 * Parses and cleans CSV content, returning domain objects (InventoryItem or NoteLineItem)
 *
 * Uses Zod discriminated unions for type-safe validation and parsing.
 */
export function parseAndCleanCsv(csvContent: string): ParsedRow[] {
  let records: RawCsvRow[];

    try {
      records = parse(csvContent, {
        columns: true,
            skip_empty_lines: true,
            trim: true,
        });
    } catch (error: any) {
      const errorMessage = error?.message || '';

      // Provide user-friendly error messages for common CSV issues
      if (errorMessage.includes('Invalid Record Length')) {
        throw new ValidationError('CSV file is malformed. Please check that all rows have the same number of columns.');
      }
      if (errorMessage.includes('Quote Not Closed')) {
        throw new ValidationError('CSV file is malformed. Please check that all quotes are properly closed.');
      }
      throw error;
    }

  // Validate headers
  if (records.length > 0) {
    const headers = Object.keys(records[0]);
    const {valid, missing} = validateCsvHeaders(headers);
    if (!valid && missing && missing.length > 0) {
      throw new ValidationError('CSV must have required columns: Definition Name, Status, Quantity');
        }
  }

  const parsedRows: ParsedRow[] = [];

  for (const row of records) {
    // Use Zod-based parser to validate and convert row
    const lineItem = parseLineItem(row);

    if (lineItem) {
      parsedRows.push(lineItem);
    }
    // Invalid rows are silently skipped (tolerance for mixed valid/invalid data)
  }

  return parsedRows;
}
```

**Key Differences from Prediction:**

- Throws exceptions instead of returning success/error objects (simpler)
- Uses Zod schemas (in `validation.ts`) for row parsing - more type-safe
- More sophisticated error messages for common CSV issues
- Delegates validation logic to separate `validation.ts` module (better separation)
- Tolerates mixed valid/invalid rows (skips invalid instead of failing entirely)

This uses the [`csv-parse`](https://csv.js.org/parse/) library (part of the actively-maintained `csv` package).

**Run the test:**

```bash
pnpm test src/utils/csvImport/__tests__/parseCSV.test.ts
```

**Expected result:** ✅ PASS

Commit. Refactor. Commit.

---

### Phase 6: Wire It Together (Back Up to API Layer)

**Goal:** API route uses the CSV parser.

**What Ted Would Do:**
Update the controller to use the newly created service/parser.

```java
@PostMapping("/import")
public String processImport(@RequestParam("file") MultipartFile file) throws IOException {
    importService.parse(file.getInputStream());
    return "redirect:/import/result";
}
```

**Update the API handler:**

```typescript
// pages/api/import/process.ts
import type {NextApiRequest, NextApiResponse} from 'next';
import formidable from 'formidable';
import fs from 'fs/promises';
import {parseCSV} from 'utils/csvImport/parseCSV';

export const config = {
    api: {
        bodyParser: false,
    },
};

export default async function handler(
    req: NextApiRequest,
    res: NextApiResponse
) {
    if (req.method !== 'POST') {
        return res.status(405).json({error: 'Method not allowed'});
    }

    const form = formidable();

    form.parse(req, async (err, fields, files) => {
        if (err) {
            return res.status(500).json({error: 'File upload failed'});
        }

        const orderNumber = Array.isArray(fields.orderNumber)
            ? fields.orderNumber[0]
            : fields.orderNumber;

        // Validate order number (stubbed for now)
        if (orderNumber === 'INVALID') {
            return res.status(400).json({error: 'Order not found'});
        }

        const uploadedFile = Array.isArray(files.file) ? files.file[0] : files.file;

        if (!uploadedFile) {
            return res.status(400).json({error: 'No file uploaded'});
        }

        // Read and parse CSV
        const csvData = await fs.readFile(uploadedFile.filepath, 'utf-8');
        const parseResult = parseCSV(csvData);

        if (!parseResult.success) {
            return res.status(400).json({error: parseResult.error});
        }

        // TODO: Match barcodes, create line items
        // For now, just return success
        return res.status(200).json({
            success: true,
            itemsImported: parseResult.items?.length || 0,
        });
    });
}
```

**Run API tests:**

```bash
pnpm test pages/api/import/__tests__/process.test.ts
```

**Expected result:** ✅ PASS (should still pass, now with real parsing)

**TDD Check:** The tests should still pass because we're replacing the hardcoded logic with real parsing that produces
the same behavior. The test mocks were simulating valid CSV data, so the real parser should handle it the same way. If
the tests FAIL here, it means our parser has a bug - go back and fix the parser until the API tests pass again. This is
"coming back up" from the lower layer after implementing the logic there.

---

### Phase 7: Complete the Flow (Back Up to IO-Based Layer)

**Goal:** Wire up the frontend to call the API.

**Where we are in the TDD cycle:**
We've been working our way down and back up:

1. Phase 3: Wrote Playwright test for form submission - FAILED (no API)
2. Phase 4: Dropped to API layer, wrote tests - FAILED (no handler)
3. Phase 4: Created API handler with hardcoded response - API tests PASSED
4. Phase 5: Dropped to service layer, wrote CSV parser tests - FAILED (no parser)
5. Phase 5: Implemented CSV parser - Parser tests PASSED
6. Phase 6: Wired parser into API handler - API tests still PASS
7. **Phase 7 (current):** Back to Playwright - should now PASS because API exists and works

**What Ted Would Do:**
Implement the HTML form in the Thymeleaf template to submit data to the backend.

```html
<!-- src/main/resources/templates/import.html -->
<form method="post" enctype="multipart/form-data" th:action="@{/import}">
    <div class="dropzone">
        <input type="file" name="file" accept=".csv" />
    </div>
    <input type="text" name="orderNumber" placeholder="Order Number" />
    <button type="submit">Import</button>
</form>
```

**Update the upload component:**

```typescript
// src/components/Main/Operations/CSVImport/FileUpload/index.tsx
import {useDropzone} from 'react-dropzone';
import {useState} from 'react';
import {Box, Text, Input, Button, VStack} from '@chakra-ui/react';

const CSVUpload = () => {
    const [file, setFile] = useState<File | null>(null);
    const [fileName, setFileName] = useState<string | null>(null);
    const [orderNumber, setOrderNumber] = useState('');
    const [result, setResult] = useState<any>(null);
    const [error, setError] = useState<string | null>(null);
    const [isSubmitting, setIsSubmitting] = useState(false);

    const {getRootProps, getInputProps} = useDropzone({
        accept: {'text/csv': ['.csv']},
        maxFiles: 1,
        maxSize: 25 * 1024 * 1024, // 25MB limit
        onDrop: (acceptedFiles, rejectedFiles) => {
            setError(null);
            if (rejectedFiles.length > 0) {
                setError('Only CSV files are accepted');
                return;
            }
            if (acceptedFiles.length > 0) {
                const uploadedFile = acceptedFiles[0];
                setFile(uploadedFile);
                setFileName(uploadedFile.name);
            }
        },
    });

    const handleSubmit = async () => {
        if (!file || !orderNumber) return;

        setError(null);
        setResult(null);
        setIsSubmitting(true);

        try {
            // Use FormData for file upload
            const formData = new FormData();
            formData.append('file', file);
            formData.append('orderNumber', orderNumber);

            const response = await fetch('/api/import/process', {
                method: 'POST',
                body: formData, // No Content-Type header - browser sets it with boundary
            });

            const data = await response.json();

            if (!response.ok) {
                setError(data.error || 'Upload failed');
                return;
            }

            setResult(data);
        } catch (err) {
            setError(err instanceof Error ? err.message : 'Network error occurred');
        } finally {
            setIsSubmitting(false);
        }
    };

    return (
        <VStack spacing = {4}
    align = "stretch" >
        <Box
            {...getRootProps()}
    data - testid = "csv-dropzone"
    border = "2px dashed"
    borderColor = "gray.300"
    p = {8}
    textAlign = "center"
    cursor = "pointer"
        >
        <input {...getInputProps()}
    />
    < Text > Drop
    CSV
    file
    here, or
    click
    to
    select < /Text>
    < /Box>
    {
        fileName && <Text>File
    :
        {
            fileName
        }
        </Text>}

        < Input
        name = "orderNumber"
        placeholder = "Order Number (e.g., ORD-12345)"
        value = {orderNumber}
        onChange = {(e)
    =>
        setOrderNumber(e.target.value)
    }
        />

        < Button
        onClick = {handleSubmit}
        isDisabled = {!
        file || !orderNumber
    }
        isLoading = {isSubmitting}
            >
            Import
            < /Button>

        {
            result && (
                <Box p = {4}
            bg = "green.100"
            borderRadius = "md" >
                <Text>Import
            completed
            successfully < /Text>
            < Text > {result.itemsImported}
            items
            imported < /Text>
            < /Box>
        )
        }

        {
            error && (
                <Box p = {4}
            bg = "red.100"
            borderRadius = "md" >
            <Text color = "red.700" > {error} < /Text>
                < /Box>
        )
        }
        </VStack>
    )
        ;
    }
    ;

    export default CSVUpload;
```

**Run IO-Based tests:**

```bash
npx playwright test tests/e2e/csv-import/form-submission.spec.ts
```

**Expected result:** ✅ PASS

**Run all tests:**

```bash
npx playwright test tests/e2e/csv-import/  # All IO-Based Playwright tests
pnpm test                                    # All Jest tests (IO-Free + IO-Based)
```

**Expected result:** All green ✅

Commit. Refactor. Commit.

---

### Phase 8: Next Increment (Barcode Matching)

**Now repeat the cycle for the next feature increment:**

1. **IO-Based test (Playwright):** "Matched barcodes create line items in order"
2. **Fails** → Need barcode matching logic
3. **Drop to IO-Free layer (Jest):** Write test for barcode lookup
4. **Implement** barcode lookup util (IO-Free)
5. **Back to API layer (Jest, IO-Based):** Wire it up
6. **Back to Playwright (IO-Based):** Test passes

This is the rhythm. Red → Green → Refactor. Outside-in. Let the tests pull the design into existence.

---

## Translation Guide

### Java/Spring → Next.js/TypeScript

| Java/Spring                               | Next.js                                 | Notes                                            |
|-------------------------------------------|-----------------------------------------|--------------------------------------------------|
| `@RestController`                         | `pages/api/[route].ts`                  | File-based routing                               |
| `@GetMapping("/items")`                   | `if (req.method === 'GET')`             | Manual method checking (consider NestJS instead) |
| `@PostMapping`                            | `if (req.method === 'POST')`            | Manual method checking (consider NestJS instead) |
| `@Service`                                | `src/utils/` or `src/services/`         | No annotation, just export functions             |
| Domain objects in `domain/` package       | TypeScript interfaces + pure functions  | Keep business logic framework-free               |
| `@WebMvcTest`                             | Playwright (IO-Based test)              | Tests full HTTP request                          |
| Direct controller test (new Controller()) | Jest test (`node-mocks-http`)           | Import and call handler directly                 |
| Service test (new Service())              | Jest test of util function              | Just call the function                           |
| `@Tag("io")` for slow tests               | Separate test commands                  | `playwright test` vs `pnpm test`                 |
| `application.properties`                  | `.env.local` + `.env`                   | Config and secrets (git-ignored)                 |
| Spring Dependency Injection               | Manual imports or DI library (optional) | Most Next.js code uses manual imports            |
| JPA/Hibernate                             | Sequelize, Prisma, or raw SQL           | Different ORM, same concept                      |

**Note on environment configuration:** Next.js uses `.env` files similar to direnv in Java projects:

- `.env.local` - Local overrides, secrets, API keys (git-ignored, like your direnv `.envrc`)
- `.env` - Default values, non-sensitive config (can be committed)
- `.env.production` - Production-specific values
  In production, you'd use actual environment variables (Vercel, Docker, etc.), not `.env` files. This combines the
  function of both `application.properties` (config) and `.env` (secrets) from Java world.

**Note on Spring Boot equivalent:** If you're coming from Spring Boot and find Next.js API routes too low-level,
consider [**NestJS**](https://nestjs.com/) instead. NestJS is heavily inspired by Spring Boot with decorators
(`@Controller`, `@Get`, `@Post`), dependency injection, modules, and similar architecture patterns. It's
TypeScript-first
and designed for enterprise applications. The trade-off: you lose Next.js's React integration and file-based routing.

### Testing Tool Mapping

| Test Type              | Java Tool                        | Next.js Tool                     | IO Type  | When to Use                     |
|------------------------|----------------------------------|----------------------------------|----------|---------------------------------|
| MVC Test               | MockMvc with `@WebMvcTest`       | Playwright                       | IO-Based | Test full HTTP request/response |
| Direct Controller Test | JUnit, instantiate controller    | Jest with `node-mocks-http`      | IO-Based | Test handler logic without HTTP |
| Service Test           | JUnit, instantiate service       | Jest                             | IO-Free  | Test pure business logic        |
| Domain Test            | JUnit                            | Jest                             | IO-Free  | Test domain rules/calculations  |
| Repository Test        | `@DataJpaTest` or TestContainers | Jest with test database or mocks | IO-Based | Test actual database queries    |


### Test Data Builders in TypeScript

**Java:**

```java
Member member = new MemberBuilder()
        .withEmail("john@example.com")
        .build();
```

**TypeScript equivalent:**

```typescript
// src/utils/testHelpers/builders.ts
interface Member {
    id: string;
    email: string;
    name: string;
}

export class MemberBuilder {
    private member: Partial<Member> = {
        id: 'test-id',
        name: 'Test User',
        email: 'test@example.com',
    };

    withEmail(email: string): this {
        this.member.email = email;
        return this;
    }

    withName(name: string): this {
        this.member.name = name;
        return this;
    }

    build(): Member {
        return this.member as Member;
    }
}

// Usage in tests:
const member = new MemberBuilder()
    .withEmail('john@example.com')
    .build();
```

### About Mocking and Test Doubles

**IO-Free tests:** No mocks. No test doubles. No stubbing. Just pure functions.

> When you're testing out the application layer, you still don't want to use IO yet. So, you plug in a mock or a test
> double. Tests are running fast but now you need to...simulate [what's] not really there.

**The distinction:**

- **Domain/Service layer (IO-Free):** Just instantiate objects.
- **Application layer (IO-Based):** This is where you might use test doubles to simulate external dependencies (
  databases, APIs).

In Next.js terms:

- **IO-Free (utils/services):** `parseCSV(csvString)` - just pass in a string, check the output
- **IO-Based (API routes):** May need to simulate database calls or external APIs

> 98% of my tests don't use any kind of mocking framework because I don't need to.

The architecture itself - separating IO from logic - eliminates the need for most mocking.

---

## Safety Nets

### How to Know You're On Track

**Green lights:**

- ✅ Tests fail for the reason you predicted
- ✅ You can explain what each test is verifying
- ✅ You're adding code in response to a failing test
- ✅ Refactorings don't break tests
- ✅ Each commit is small and makes sense on its own

**Red flags:**

- 🚩 Tests pass immediately (might not be testing the right thing)
- 🚩 You're writing code without a failing test first
- 🚩 You don't understand why the test passed/failed
- 🚩 Tests are tightly coupled to implementation details
- 🚩 You've been stuck for more than 1 hour

---

## Retrospective: Predictions vs. Reality

This guide was written *before* building any production features. After completing the **SketchUp Import feature** (34
Playwright tests, 13 API tests, 89 service tests, ~2000 lines of production code), here's what actually happened:

### ✅ What Worked Exactly As Predicted

**1. Outside-In TDD Workflow**
The three-layer approach translated perfectly:

- Started with Playwright tests for page accessibility
- Dropped to Jest API tests when Playwright needed backend
- Dropped to Jest IO-Free tests for business logic
- Came back up as tests passed

**2. IO-Free vs IO-Based Distinction**
This was the most valuable insight from Ted's approach:

- IO-Free tests (CSV parsing, validation logic) run in microseconds and have **zero mocks**
- IO-Based tests (API routes, Flex API calls) are slower but necessary
- The separation made TDD fast and enjoyable

**3. Test Organization**

- Co-located `__tests__/` folders work great
- Playwright tests in `tests/e2e/` for cross-cutting concerns
- Test file naming conventions matched exactly

**4. Tools and Libraries**

- `formidable` for file uploads ✅
- `csv-parse` for CSV parsing ✅
- `node-mocks-http` for API route testing ✅
- Playwright for E2E tests ✅

### 🎯 What Evolved Beyond Predictions

**1. React Hook Form + Zod (Not Predicted)**
The real implementation uses sophisticated form handling:

```typescript
const {register, handleSubmit, setValue, formState: {errors}} = useForm<ImportFormData>({
  resolver: zodResolver(ImportFormSchema),
  mode: "onChange",
});
```

This wasn't in the original guide but became essential for:

- Real-time validation
- Type-safe form data
- Client-side error messages

**2. Playwright Fixtures (Game Changer)**
The blog mentioned mocking but didn't predict how critical fixtures would be:

```typescript
// tests/fixtures/mockFlexApi.ts - 200+ lines of mock Flex API endpoints
import {expect, test} from '../../fixtures/mockFlexApi';  // Critical import!
```

**Lesson:** Without this fixture, we hit rate limits on the real Flex API during test runs. This was discovered the hard
way.

**3. Hexagonal Architecture Pattern**
The real code has stronger separation than predicted:

- **`FlexClient` class** - Adapter for all Flex API calls (hexagonal "driven" adapter)
- **`importService.ts`** - Orchestration layer (use case)
- **`csvParser.ts`, `validation.ts`** - Pure domain logic
- **API route** - Thin adapter calling the service

This made testing easier because:

- Service tests mock only `FlexClient` (one boundary)
- API tests mock the entire service
- Parser tests mock nothing

**4. Observability (Not Mentioned)**
Production code needs visibility:

```typescript
import {logger} from "utils/logger";

logger
        .withMetadata({elementNumber, userId, flexInstance})
        .info('SketchUp import started');
```

Plus Sentry integration, database logging, and breadcrumbs. The blog focused on testing but production requires
debugging tools.

**5. Manual Integration Tests**
Discovered a new pattern:

```typescript
// src/utils/sketchupImport/__tests__/barcodeService.manual.test.ts
describe.skip('Barcode Service - Manual Integration Tests', () => {
  // Tests against real Flex API, skipped by default
});
```

These run: `pnpm test:manual:barcode`

Why? Because mocking can hide bugs. We had a mock structure that didn't match production data, causing a bug that only
appeared in staging. Manual integration tests catch these.

### ❌ What Didn't Match Predictions

**1. Authentication Pattern**
**Predicted:** Server-side redirect with `getServerSideProps`

```typescript
export const getServerSideProps: GetServerSideProps = async (context) => {
  const session = await getSession(context);
  if (!session) return {redirect: {destination: '/login'}};
  return {props: {session}};
};
```

**Reality:** Client-side check with custom hook

```typescript
const typeOfUser = useTypeOfUser();
{
  typeOfUser === userStatus.NOUSER && <NeedToLoginMessage / >
}
```

**Why the difference?** The Loomium codebase already had established patterns. Following existing conventions was more
important than the "theoretically correct" approach.

**2. Post-Redirect-Get Pattern**
**Predicted:** "For this example, we're using a simpler client-side state update"

**Reality:** Fully implemented PRG pattern with database persistence

```typescript
const importId = uuidv4();
await SketchUpImportLog.create({id: importId, ...result});
await router.push(`/operations/sketchup-import/results/${importId}`);
```

Turned out this was critical for:

- Users refreshing results page
- Sharing import results URLs
- Historical analysis

**3. Test Doubles Usage**
**Predicted:** "98% of my tests don't use any kind of mocking framework"

**Reality:** More like 70% IO-Free (no mocks), 30% IO-Based (strategic mocking)

The IO-Based tests mock:

- `FlexClient` (adapter boundary)
- `getSession` (NextAuth)
- `getCustomer` (database)

**Key insight:** The hexagonal architecture made mocking boundaries clear. We mock at adapter boundaries, never in
domain logic.

### 📚 Biggest Lessons Learned

**1. The Workflow Actually Works**
Outside-In TDD in Next.js is not just possible—it's enjoyable. The rapid feedback from IO-Free tests (microseconds)
combined with the safety net of Playwright tests (full integration) gave confidence to refactor aggressively.

**2. Test Speed Matters More Than Expected**
Running 89 Jest tests in ~2 seconds vs. 34 Playwright tests in ~30 seconds makes a huge difference in workflow. You
run IO-Free tests constantly, IO-Based tests periodically.

**3. Type Safety Reduces Test Burden**
TypeScript + Zod caught entire classes of bugs that would have required tests in JavaScript:

- Column name typos
- Missing required fields
- Type coercion issues

This let us focus tests on business logic, not syntax validation.

**4. Production Code Needs More Than The Blog Shows**
Real features need:

- Logging and observability
- Error tracking (Sentry)
- Database persistence
- Admin configuration UIs
- Results pages
- CSV templates
- Rate limit handling

The blog shows the TDD workflow but not the full production context.

**5. Fixture Maintenance Is Real Work**
The `mockFlexApi.ts` fixture is 200+ lines and needs updates when:

- New Flex API endpoints are called
- Response formats change
- New admin settings are added

This is maintenance overhead but absolutely worth it to avoid rate limits and flaky tests.

### 🎓 Advice for Your Next Feature

**Do This:**

- ✅ Start with Playwright test for page accessibility
- ✅ Use Outside-In workflow (edge → internals)
- ✅ Keep IO-Free tests truly IO-Free (no mocks!)
- ✅ Use Zod for all validation
- ✅ Create Playwright fixtures for external APIs
- ✅ Write manual integration tests for critical adapters
- ✅ Follow the codebase's existing patterns (even if blog says otherwise)

**Don't Do This:**

- ❌ Don't mock inside domain logic
- ❌ Don't skip IO-Free tests and only write E2E tests
- ❌ Don't import from `@playwright/test` - use your fixtures!
- ❌ Don't test implementation details - test behavior
- ❌ Don't write tests after code (defeats the purpose)

**When Stuck:**

1. Check if similar code exists elsewhere in the codebase
2. Look at test files for patterns (we have 136 tests now)
3. Ask: "Am I testing behavior or implementation?"
4. Drop down a layer if the current test is too hard to make pass

---

## Resources

### Ted M. Young's Work

**Core Workflow Articles:**

- [Predicting the Failing Test](https://ted.dev/articles/2021/11/05/predicting-the-failing-test/) - The foundation of
  PTDD
- [Implementing the Feature](https://ted.dev/articles/2022/05/09/implementing-the-feature/) - Green phase and tightening
  assertions
- [I'm Done with Unit and Integration Tests](https://ted.dev/articles/2023/04/02/i-m-done-with-unit-and-integration-tests/) -
  IO-Free vs IO-Based taxonomy

**Videos:**

- [TDD & Hexagonal Architecture Exercise - Part 1](https://www.youtube.com/watch?v=BYHlxsyD288) - Pure domain TDD with
  ZOMBIES
- [Song Themes Episode 2](https://www.youtube.com/watch?v=S100FP9piGs) - Outside-in web development, test categorization

**Code Examples:**

- [yacht-tdd repository](https://github.com/jitterted/yacht-tdd) - Nullables pattern (testing without mocks)
- [ensembler repository](https://github.com/jitterted/ensembler) - Full hexagonal architecture example

### Next.js/TypeScript Testing

**Official Docs:**

- [Next.js Testing Documentation](https://nextjs.org/docs/app/guides/testing)
- [Playwright Documentation](https://playwright.dev/docs/intro)
- [Jest Documentation](https://jestjs.io/docs/getting-started)

**Patterns:**

- [Testing API Routes with Jest](https://nextjs.org/docs/testing#jest-and-react-testing-library)
- [Playwright Best Practices](https://playwright.dev/docs/best-practices)

**CSV Parsing:**

- [csv-parse Documentation](https://csv.js.org/parse/) - Production-ready CSV parser
- [Top JavaScript CSV Parsers](https://www.oneschema.co/blog/top-5-javascript-csv-parsers) - Comparison of libraries

**File Uploads:**

- [Handling multipart/form-data in Next.js](https://dev.to/mazinashfaq/handling-multipartform-data-in-nextjs-26ea)
- [formidable on GitHub](https://github.com/node-formidable/formidable)


---

## Final Thoughts

When I started this project, I knew Java and Spring Boot but was new to Next.js and React. The question was: "Can I
do TDD the way Ted Young teaches in this unfamiliar ecosystem?"

After building a production feature with 136 automated tests, the answer is **yes**—but with adjustments. The
Outside-In workflow, IO-Free vs IO-Based distinction, and test-first discipline all translated. The tools and patterns
differ, but the principles hold.

The retrospective section shows what I got right in my predictions and what I learned the hard way. If you're in a
similar position—experienced in one stack, learning another—I hope this guide gives you confidence that TDD works
across ecosystems. The mechanics change. The discipline doesn't.

---

*This guide synthesizes research from Ted M. Young's YouTube transcripts, blog posts, and public codebases, then
validates those ideas through building a real production feature. All credit for the core methodology goes to Ted. The
translation to Next.js—including the mistakes and corrections—is mine. - Nathan*
