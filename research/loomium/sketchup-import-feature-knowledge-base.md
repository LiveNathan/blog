# Filmwerks SketchUp Import Feature Knowledge Base

**Status:** In Development
**Context:** MVP for Filmwerks to import SketchUp CSV reports into Flex Rental Solutions via Loomium.

## Overview

This feature allows Filmwerks users to export a report from SketchUp (as a CSV) and import it into Flex Rental
Solutions. The tool acts as a "bridge" within the Loomium portal, accepting the CSV and user input (Quote/Pull Sheet
number), and then interacting with the Flex API to create and populate a Pull Sheet.

## Core Workflow

1. **Input (Upload UI):**
    * User uploads a CSV file generated from SketchUp.
    * User provides a **Target Element Number** (either a Quote Number or an existing Pull Sheet Number).
    * User optionally provides a name for the new Pull Sheet.
2. **Transform:**
    * System parses the CSV.
    * **Barcode Lookup:** Translates SketchUp "Status" (or Barcode column) to Flex Managed Resource IDs.
        * *Note:* Use the bulk barcode lookup endpoint in Flex API to optimize this.
    * **Filtering:** Identifies valid inventory items vs. non-inventory/custom items.
3. **Load (Flex Interaction):**
    * **Scenario A: Target is a Quote Number**
        * Create a new child Pull Sheet under this Quote.
        * Set initial status (e.g., "Import In Progress").
    * **Scenario B: Target is a Pull Sheet Number**
        * Check if the Pull Sheet is empty.
        * **If Empty:** Proceed to load lines.
        * **If Not Empty:**
            * Archive the existing Pull Sheet (via Flex Workflow Action).
            * Create a *new* Pull Sheet (effectively "Cancel and Replace").
            * *Note:* Should check if scanning has already started (scan progress). If items are already scanned, the
              process might need to fail or warn (MVP decision: likely fail/stop to avoid data loss).
    * **Populate:**
        * Add matched inventory items as line items.
        * Add non-inventory items as "Note" lines (or skip, based on final MVP decision).
    * **Finalize:**
        * Execute Workflow Action to move Pull Sheet to "Import Complete" status.
4. **Output (Feedback UI):**
    * Display import results.
    * Summary of success/failed lines.
    * Error details for unmatched items.

## Technical Implementation Details

### Platform Architecture

* **Framework:** Loomium (Next.js 12, React 18, TypeScript)
* **API:** Flex Rental Solutions API
* **File Handling:** `react-dropzone` (frontend), `formidable` (backend)
* **CSV Parsing:** TBD (likely `papaparse` or `csv-parse`)
* **UI Library:** Chakra UI

### Key Loomium Patterns

**Creating a New Page:**

- Pages are code-based in `pages/` directory (NOT Sanity)
- File: `pages/operations/sketchup-import/index.tsx`
- Add route to `src/constants/routes.ts`: `SKETCHUP_IMPORT: "/operations/sketchup-import"`
- Use `PageSEOWrapper`, `Can` component for permissions
- Check auth with `getOAuthKeys(session)?.access_token`

**File Upload Pattern:**

- Frontend: `react-dropzone` with `useDropzone` hook
- Accept CSV: `accept: { 'text/csv': ['.csv'] }`
- Upload via FormData to API endpoint
- Backend: `formidable.IncomingForm()` with `bodyParser: false`
- See: `pages/api/support/upload-file/index.tsx` for reference

**Flex API Integration:**

- Use `flexOAuth2Request` from `utils/flex/flexOAuth2Request`
- Handles auth tokens, error logging, Sentry integration
- Pattern: `flexOAuth2Request(session, "element/123", "GET")`
- Base URL: `https://{flex_instance}/f5/api/{endpoint}`

### Key Flex API Endpoints

**Element Operations:**

- **Get Element:** `GET /element/{id}` - Fetch Quote or Pull Sheet details
- **Create Element:** `POST /element` - Create new Pull Sheet
    - Requires: `definitionId` (Pull Sheet definition), `parentId` (Quote ID)
- **Update Element:** `PUT /element/{id}` - Update Pull Sheet status/name
- **Add Line Items:** POST to element lines endpoint (TBD - need to explore)

**Barcode Lookup:**

- **Bulk Barcode Scan:** Endpoint TBD (likely `/inquiry/scan` or similar)
- Translates barcodes to Managed Resource IDs
- Use bulk endpoint to minimize API calls

**Workflow Actions:**

- **Execute Workflow:** Endpoint TBD
- Actions: `Import In Progress`, `Import Complete`, `Archive`
- Check if scanning started before archiving

### Implementation Checklist

**Routing & Page Structure:**

- File path: `pages/operations/sketchup-import/index.tsx`
- Route constant: `SKETCHUP_IMPORT` in `src/constants/routes.ts`
- Permission module: Define in permissions system (TBD - likely "operations" or new "sketchup_import")

**Component Structure:**

- Main page component: `pages/operations/sketchup-import/index.tsx`
- Feature component: `src/components/Main/Operations/SketchUpImport/index.tsx`
- Upload component: `src/components/Main/Operations/SketchUpImport/FileUpload/index.tsx`
- Results component: `src/components/Main/Operations/SketchUpImport/ImportResults/index.tsx`

**API Routes:**

- Upload CSV: `pages/api/operations/sketchup-import/upload-csv/index.ts`
- Process Import: `pages/api/operations/sketchup-import/process-import/index.ts`
- Get Import Status: `pages/api/operations/sketchup-import/status/[importId].ts`

**Utils/Services:**

- CSV Parser: `src/utils/sketchUpImport/parseCSV/index.ts`
- Barcode Lookup: `src/utils/sketchUpImport/lookupBarcodes/index.ts`
- Pull Sheet Creator: `src/utils/sketchUpImport/createPullSheet/index.ts`
- Line Item Adder: `src/utils/sketchUpImport/addLineItems/index.ts`

**Testing Strategy:**

- E2E tests in `tests/sketchup-import/`
- Test auth requirements first
- Test CSV upload
- Test barcode lookup
- Test Pull Sheet creation (Quote parent)
- Test Pull Sheet replacement (existing Pull Sheet parent)
- Characterization tests for Flex API interactions

## Feature Development Checklist

### Phase 1: Setup & Upload UI

- [ ] **Local Development Setup**
    - [ ] Create feature branch.
    - [ ] Ensure local environment is running (`pnpm dev`).
- [ ] **Upload UI Implementation**
    - [ ] Create a new page/view for SketchUp Import.
    - [ ] Add File Upload component (CSV).
    - [ ] Add Text Input for "Target Element Number" (Quote or Pull Sheet).
    - [ ] Add Text Input for "New Pull Sheet Name" (Optional).
    - [ ] Add "Start Import" button.

### Phase 2: Transform Logic

- [ ] **CSV Parsing**
    - [ ] Implement CSV reader.
    - [ ] Implement column mapping (match SketchUp columns to internal model).
- [ ] **Data Transformation**
    - [ ] Implement Flex API service method to fetch Managed Resource IDs from Barcodes.
    - [ ] Handle "No Match" scenarios (flag as error or note).

### Phase 3: Load Logic (The "Heavy Lifting")

- [ ] **Element Lookup**
    - [ ] Implement service to fetch details of the provided "Target Element Number".
    - [ ] Determine if target is Quote or Pull Sheet.
- [ ] **Pull Sheet Creation Strategy**
    - [ ] **From Quote:** Implement logic to create new child Pull Sheet.
    - [ ] **From Pull Sheet:** Implement logic to check content/status.
        - [ ] If exists & not empty: Trigger "Archive" workflow action on old sheet, then create new.
- [ ] **Line Item Loading**
    - [ ] Iterate through transformed items and POST to Flex to add lines.
    - [ ] Handle rate limiting or batching if necessary (Flex API is often 1 call per line).
- [ ] **Status Updates**
    - [ ] Set initial status upon creation.
    - [ ] Set final status upon completion.

### Phase 4: Output & Feedback

- [ ] **Results UI**
    - [ ] Display summary report after process finishes.
    - [ ] List any items that failed to import.

### Phase 5: QA & Handover

- [ ] **Manual Testing**
    - [ ] Test with valid Quote Number.
    - [ ] Test with valid Pull Sheet Number (Empty).
    - [ ] Test with valid Pull Sheet Number (Existing items).
    - [ ] Test with Invalid Barcodes.
- [ ] **Code Review & Merge**.

## Notes & Learnings

* *Add notes here as development progresses...*
