# TDD Workflow Checklist for Feature Development

This checklist provides a repeatable, step-by-step process for implementing user stories using Test-Driven Development
in the Loomium codebase.

## Pre-Work (Before Starting Any User Story)

- [ ] Review the user story and acceptance criteria
- [ ] Identify which parts of the system you need to understand
- [ ] Use an LLM to explore relevant code patterns
- [ ] Ask clarifying questions if requirements are ambiguous
- [ ] Break down the story into the smallest testable increments

## For Each User Story / Asana Task

### 1. Setup (5-10 minutes)

- [ ] Create a feature branch: `git switch -c [story-number]-[brief-description]`
    - Modern Git (2.23+) - clearer syntax
    - Old way still works: `git checkout -b [story-number]-[brief-description]`
- [ ] Ensure dev environment is running: `pnpm dev`
- [ ] Open the relevant files in your editor
- [ ] Review acceptance criteria one more time

### 2. Exploration & Planning (15-30 minutes)

- [ ] **Identify unknowns:** What parts of the system are unclear?
- [ ] **Chat with an LLM about:**
    - Which files need to be modified
    - What existing patterns to follow
    - Any potential gotchas or edge cases
- [ ] **Document findings:** Add notes to the knowledge base if you learn something new
- [ ] **List the files you'll create/modify:**
    - Pages: `pages/.../index.tsx`
    - Components: `src/components/.../index.tsx`
    - API routes: `pages/api/.../index.ts`
    - Utils: `src/utils/.../index.ts`
    - Tests: `tests/.../[feature].spec.ts`

### 3. Write the First Test (RED) (10-15 minutes)

**Playwright (E2E) Test Pattern:**

- [ ] Create test file: `tests/[feature]/[scenario].spec.ts`
- [ ] Write the absolute simplest test first
    - Example: "Authenticated users can access the page"
    - Example: "Page displays the upload form"
- [ ] Run the test: `npx playwright test tests/[feature]`
- [ ] **Verify it fails** (RED state)
- [ ] **Ask an LLM:** "Does this test make sense given the existing architecture?"

**Jest (Unit) Test Pattern (if applicable):**

- [ ] Create test file: `src/[component]/__tests__/[component].test.tsx`
- [ ] Write a simple unit test
- [ ] Run: `pnpm test`
- [ ] **Verify it fails**

### 4. Write Minimal Code to Pass (GREEN) (20-40 minutes)

- [ ] Implement the absolute minimum to make the test pass
- [ ] **Don't add extra features** - only what the test requires
- [ ] Run the test again: `npx playwright test tests/[feature]`
- [ ] **Verify it passes** (GREEN state)
- [ ] **Pair with an LLM:**
    - You: Describe what you want to do
    - LLM: Suggests code following Loomium patterns
    - LLM: Explains the React/Next.js/TypeScript patterns
    - You: Ask questions about anything unclear

### 5. Refactor (if needed) (10-20 minutes)

- [ ] Is the code clear and simple?
- [ ] Does it follow existing Loomium patterns?
- [ ] Are there any obvious improvements?
- [ ] **Only refactor if it improves clarity** - don't over-engineer
- [ ] Re-run tests to ensure they still pass

### 6. Commit (5 minutes)

### 7. Repeat (TDD Cycle)

- [ ] Write the next test for the next smallest increment
- [ ] **Examples of incremental tests:**
    - Can upload a CSV file
    - Displays uploaded file name
    - Shows validation error for invalid file
    - Submits file to API endpoint
    - API endpoint receives and processes file
    - etc.

### 8. Characterization Tests (Optional but Recommended)

As you learn how existing systems work:

- [ ] Write a test documenting the behavior you discovered
- [ ] Example: "Flex API returns 401 when token is invalid"
- [ ] These tests serve as documentation and prevent regressions

### 9. Story Completion (30 minutes)

- [ ] All acceptance criteria have passing tests
- [ ] No tests are skipped or commented out
- [ ] Run full test suite: `npx playwright test && pnpm test`
- [ ] Manual testing in the browser
- [ ] Update documentation if needed
- [ ] Push branch: `git push -u origin [branch-name]`
- [ ] Create PR to dev branch

## Learning & Reflection (After Each Story)

- [ ] **What did I learn about:**
    - Next.js routing?
    - React patterns?
    - TypeScript?
    - Flex API?
    - Loomium architecture?
- [ ] **What would I do differently next time?**
- [ ] **What patterns can I reuse?**
- [ ] **Add learnings to the knowledge base**

## Working with an LLM as a Coach

**Good prompts for LLM:**

- "Explain what this code does and why it's structured this way"
- "What's the Loomium pattern for [X]? Show me an example from the codebase"
- "I want to [accomplish Y]. What's the simplest way to do this?"
- "Does this test make sense? Am I testing the right thing?"
- "Can you explain how [component/pattern] works?"

**Keep LLM accountable:**

- "Don't write code I don't understand - explain it first"
- "Show me where this pattern is used elsewhere in the codebase"
- "Why did you choose this approach over [alternative]?"

## Red Flags (When to Ask for Help)

- [ ] You've been stuck for more than 1 hour
- [ ] You're about to make a change you don't understand
- [ ] Tests are passing but you're not sure why
- [ ] You're adding complexity that feels wrong
- [ ] You're tempted to skip writing tests

→ **Action:** Reach out to Zellers, schedule a pairing session, or ask for a code review

## Success Metrics

After using this workflow, you should:

- ✅ Have passing tests for all implemented functionality
- ✅ Understand the code you wrote
- ✅ Know which Loomium patterns you used and why
- ✅ Feel confident making similar changes in the future
- ✅ Have documentation of new learnings
