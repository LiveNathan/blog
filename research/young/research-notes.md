# TDD Workflow Research Notes

Extracting Ted M. Young's (JitterTed) outside-in TDD workflow from YouTube video transcripts.

**Research Goal:** Document step-by-step process for adding features to Spring Boot applications using outside-in TDD and hexagonal architecture.

**Start Date:** 2025-11-28

---

## Song Themes Episode 1: Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=QvxQuh7rBb0
**Relevance:** High - Contains active TDD coding session with explicit workflow discussion
**Guest:** Mike Rizzi

### Feature/App Context
Building a song themes search app. Episode includes extensive Event Storming (domain modeling) session, then begins implementation with search functionality. The feature being built: search for songs by theme.

### Workflow Observed

#### Starting Point
- **Layer:** Subcutaneous/Service layer (SongSearcher)
- **First test:** `search_for_non_existent_theme_returns_no_results()`
- **Initial code:** `return List.of()` (empty list)

#### Progression
1. **Service/Domain Test** → Tests search returns empty list for non-existent theme
   - Trigger: Starting with queries (viewing) rather than commands (adding)
   - Code written: Created `SongSearcher` class with `search(String theme)` method returning `List.of()`
   - Test structure: Sketch assertion first, then work backward

2. **MVC Test** → Tests POST endpoint exists and redirects
   - Trigger: "Leave a breadcrumb for next time" - intentionally failing test
   - Code written: None (test left failing as breadcrumb for next session)
   - Test: POST to `/theme-search` should return 3xx redirect status

### Layer Transition Decisions

**Starting with queries vs commands:**
- "I always look at it from what do I do when I'm writing when I'm doing tdd is is basically how do I verify if I worked whereas if you start with the searching how you see it how you know it works is because you can see it"
- Decision: Start with viewing/query side rather than command side

**Subcutaneous vs MVC:**
- "I like to start um I don't think I want to write an HTML based test but I would want to write an MVC level test"
- "The only potential problem for subcutaneous test first is you might not have your method signatures set up"
- Decision: Start subcutaneous first, then add MVC test

### Testing Philosophy Quotes

**Deferring decisions:**
- "we could guess what that is but since we're returning what's going to be an empty list it really doesn't matter"
- "start with Primitives until you know what you need because it's going to be relatively easy to create a song object once we have a better idea"
- "make the decision at the last responsible moment"
- "Generally can I defer this decision when I will know more"

**Test structure:**
- "I like to sort of sketch out what are we going to assert"
- "let's create a class...and then let's go ahead and new that up"

**Simplest thing:**
- "doing basically the simplest thing that we can get away with that starts getting us towards what we want"
- "anything more than than than a string to me is more work than than I need to do"

### Code Patterns Observed

**Test-first workflow:**
1. Sketch assertion first (`assertThat(songs).isEmpty()`)
2. Create variable to hold result
3. Create instance of class being tested
4. Call method (doesn't exist yet)
5. Use IDE to generate class and method
6. Write simplest code to pass
7. Commit after green test

**Breadcrumb pattern:**
- Deliberately left failing MVC test as "breadcrumb" for next session
- Shows intentional use of failing tests to mark stopping points

**Class creation:**
- Uses IDE shortcuts (Alt+Enter) to create classes from test
- Uses `var` for type inference when possible
- Returns primitives (String, List) until domain objects are needed

### Ted's Terminology
- **Subcutaneous:** Testing just below the web/HTTP layer
- **Breadcrumb:** Intentionally failing test left as marker for next session
- **Last responsible moment:** When to make design decisions

### DDD/Event Storming Context
This episode spent majority of time on Event Storming before coding:
- Started with domain events (orange stickies)
- Added commands (blue), actors (yellow), read models (green)
- Discovered aggregate boundaries through the process
- Key insight: "Commands generate events" and aggregates sit between them

### Notes
- Heavy emphasis on Event Storming/DDD upfront before any coding
- Only ~20 minutes of actual coding in 2+ hour stream
- Very deliberate about deferring design decisions
- Starts with queries (read side) rather than commands (write side)
- Walking skeleton already deployed (continuous deployment setup)
- Commits frequently, even failing tests (but doesn't push failing code)

---

## Song Themes Episode 2: Spring Boot App creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=S100FP9piGs
**Relevance:** High - Active TDD coding with EXPLICIT testing philosophy discussion
**Guest:** Mike Rizzi

### Feature/App Context
Continues from Episode 1. Picks up with failing MVC test (breadcrumb). Implements GET endpoint for search, corrects POST→GET, creates test categorization system, refactors test setup.

### Workflow Observed

#### Starting Point
- **Layer:** MVC/Web (picking up failing test from Episode 1)
- **First action:** Make failing MVC test pass
- **Initial code:** `@GetMapping` + return template name

#### Progression
1. **MVC Test** → POST endpoint returns redirect
   - Trigger: Breadcrumb from previous session
   - Code written: `@PostMapping("/theme-search")` returning `"redirect:/"`
   - Test passed: Returns 3xx redirect

2. **Corrected to GET** → Realized search should be GET not POST
   - Trigger: "POST is isn't doing a state change right uh it's actually a query request"
   - Code written: Changed to `@GetMapping`, returns template name
   - Test changed: Expects 200 not 3xx

3. **Direct Controller Test** → Tests controller without framework
   - Trigger: "I want the fewest minimal minimalist tests that actually use the framework because they are slow"
   - Code written: Test calls controller directly, checks return value
   - Pattern: MVC test for framework config, direct test for logic

4. **Tag Configuration** → Separated IO vs IO-free tests
   - Trigger: "the question came up... it's on brain stack"
   - Code written: `@Tag("io")` on MVC tests, created two run configurations
   - Categories: "IO based" (framework tests) vs "IO free" (pure unit tests)

5. **Service Layer Tests** → Continued building SongSearcher
   - Trigger: Moving deeper from controller to domain
   - Code written: Factory methods for test setup, eliminated duplication
   - Pattern: Hardcoded data first, then generalize

### Layer Transition Decisions

**MVC tests for framework configuration:**
- "the scheme I follow is I want the fewest minimal minimalist tests that actually use the framework because they are slow"
- "if it's something that is basically around configuring the framework so post mapping endpoints redirection... those are going to require the framework"

**Direct controller tests for everything else:**
- "anything I can do that does not require the framework I will do without the framework"
- "I could here in this test... check for where it redirects to um but that would require me to run this test if I change that and I since I can check that and I can call it directly against the controller... I want to do faster"

**Controller testing philosophy:**
- "even though the controller is in hexagonal architecture an adapter class it doesn't mean all your tests have to be integration tests"

### Testing Philosophy Quotes

**Framework vs non-framework tests:**
- "the scheme I follow is I want the fewest minimal minimalist tests that actually use the framework because they are slow"
- "if it's something that is basically around configuring the framework so post mapping endpoints redirection... those are going to require the framework"
- "anything I can do that does not require the framework I will do without the framework"

**Test categorization:**
- Uses `@Tag("io")` instead of "integration" - prefers "IO-based" and "IO-free"
- "basically um the the io free tests are just ones that don't have io on them"
- Separate run configurations for each category

**When to use which test type:**
- MVC tests: "things that you would not be able to test with just directly instantiating it"
- Direct controller tests: "most likely I end up with a bunch of test against the controller that are IO free"
- "I'm still going to be and so most likely I end up with a bunch of test against the controller that are IO free that don't require the framework so I'm just saying given these parameters it should do this stuff call this service"

**Mocking:**
- "I don't want to use mocks... at least not Mockito"
- Preference: real objects or simple test doubles over mocking frameworks

### Code Patterns Observed

**Test categorization:**
- `@Tag("io")` for framework-dependent tests
- Untagged for IO-free tests  
- Run configurations: "IO based" with `tags: io`, "IO free" with `tags: !io`
- All tests configuration with no tag filter

**MVC test structure:**
```java
mockMvc.perform(get("/theme-search"))
    .andExpect(status().is2xxSuccessful());
```

**Direct controller test:**
```java
SongThemesController controller = new SongThemesController(songSearcher);
String redirectPage = controller.themeSearch("");
assertThat(redirectPage).isEqualTo("redirect:/theme-search-results");
```

**Factory methods for test setup:**
- Created `withSongsForTheme(String theme)` factory method
- Created `withOneSong(String theme, String song)` factory method
- Moved from constructor to static factory to encapsulate setup
- Eliminated duplication across tests

**Controller dependency injection:**
- Uses constructor injection (no `@Autowired`)
- Bridge in `@SpringBootApplication` class with `@Bean` method
- Keeps domain classes framework-free

### Ted's Terminology
- **IO-based/IO-free:** Preferred terms over "integration/unit"
- **Subcutaneous:** Testing just below the UI/HTTP layer
- **Framework tests:** Tests that require Spring context
- **Brain stack:** Mental stack of things to remember/do

### Decision Corrections During Session
- **POST → GET:** Realized search should use GET not POST (queries don't change state)
- **Redirect → Template:** Changed from redirecting to directly returning template
- **Test granularity:** Decided one MVC test per endpoint is usually sufficient

### Notes
- Very explicit about minimizing framework tests due to speed
- Controllers tested both ways: MVC for config, direct for logic
- Strong preference for test speed and avoiding mocks
- Frequent refactoring to eliminate duplication
- Uses IDE heavily for refactoring (extract method, introduce parameter, etc.)
- Commits frequently but doesn't push failing tests
- Run configurations critical for separating fast/slow tests

---

## TDD & Hexagonal Architecture Exercise: Supermarket Checkout Pricer - Part 1

**Video URL:** https://www.youtube.com/watch?v=BYHlxsyD288
**Relevance:** VERY HIGH - Pure domain TDD, explicit ZOMBIES, hexagonal architecture
**Guest:** Solo (Ted only)

### Feature/App Context
Building a supermarket checkout pricer from scratch. Pure kata/exercise format. Demonstrates TDD without framework concerns - pure domain logic. Goal: calculate cart total with special deals/discounts.

### Workflow Observed

#### Starting Point
- **Layer:** Pure domain (no framework, no Spring)
- **First test:** `emptyCartHasTotalPriceOfZero()`
- **Initial code:** Created `Cart` class, return 0

#### TDD Cycle - Explicit Red/Green/Refactor

**Red Hat Phase:**
1. Write failing test
2. **Predict** how it will fail
3. Run test, verify it fails as predicted
4. "For the right reason" - must fail correctly

**Green Hat Phase:**
1. Write **least amount of code** to pass
2. Hardcode values if possible
3. Get to green quickly

**Refactor Hat Phase:**
1. Look for duplication
2. Look for code smells
3. Extract when you have enough information

#### Progression (ZOMBIES)

1. **Zero case** → Empty cart returns 0
   - Test: `cart.totalPrice()` should be 0
   - Code: `return 0;` (hardcoded)
   - Pattern: Establish baseline

2. **One case** → Add one product
   - Test: `cart.add("toothbrush", 1);` then `totalPrice()` should be 1
   - Code: Store `productPrice` field, return it
   - Pattern: Eliminate duplication (1 in test matches 1 in parameter)
   - Fake it: Initially throw `UnsupportedOperationException` to ensure test fails

3. **Many case** → (preparing for multiple products)
   - Pattern: Copy test, modify for two products
   - Not yet implemented in this excerpt

### Layer Transition Decisions

**Domain-first approach:**
- "This is pure domain code right this is all about what are the rules process calculations behavior"
- Moved code to `domain` package to create boundary
- "Adding domain to me does these magical things one is it all of a sudden says no code here can reference anything hardware io outside world related"

**When to create objects:**
- "My preference is to extract objects from code that already exists"
- "Somehow that feels more natural for me"
- Waits until he has enough information: "I don't have enough information to know where to refactor"
- Resists creating `Product` class until tests demand it

### Testing Philosophy Quotes

**ZOMBIES (Zero, One, Many, Boundaries, Interfaces, Exceptions, Simple):**
- "When I'm thinking about the first test I want to write I'm thinking about what are the fewest number of elements I can get away with"
- "What's the baseline test what's the zero case"
- "We've done the zero case an empty cart done the one case where we add one so really kind of need to do the many case"

**Prediction:**
- "One of the important parts about both my game and the process is the prediction"
- "We want to predict that the test must fail and for the right reason"
- "Our expectation is this is going to fail because we're going to throw an unsupported operation exception"

**Fake It Till You Make It:**
- "I don't want to return 0 because the test I'm about to write is gonna be assert that that it's zero and that'll pass so I don't want it to pass"
- "Throw an unsupport operation exception that'll definitely fail the test"
- "The least amount of code um so that means this zero is not going to work"

**Test-first discipline:**
- "I want to start with a failing test right i've got my red cap on"
- "Failing because it's failing to compile right so that's the first step"
- "We want to write enough code to get it to compile"

**Incremental steps:**
- "When we're sort of practicing tdd and taking small steps we want to really take small steps"
- "The next level up in complexity from a constant literal... is some either an if statement or storing something"

**No @DisplayName:**
- "I don't use the display name annotation no i don't i rely on my test method names to to be useful"
- "Why not just make the method name descriptive"

### Code Patterns Observed

**Test structure:**
- Method names: `emptyCartHasTotalPriceOfZero()`, `addToothbrushProductThenCartPriceIsOne()`
- No @DisplayName, descriptive camelCase
- AssertJ: `assertThat(cart.totalPrice()).isZero()`

**Hardcoding → Generalization:**
1. `return 0;` (hardcoded)
2. `return productPrice;` (one variable)
3. (Eventually) sum of all products

**Method naming:**
- `totalPrice()` not `getTotalPrice()`
- "Note it's not get total price it is total price it is a query method we're asking the cart what is your current total price we are not getting"
- "Get to me has implications of getting some internal state that's not what we're doing"

**Refactoring under red:**
- "I'm going to do a refactoring even though i've got a failing test"
- "I know but to be really sure i'm going to basically comment out this test"
- Shows discipline: commented out test, ensured green, then uncommented

### Ted's Terminology
- **ZOMBIES:** Zero, One, Many, Boundaries, Interfaces, Exceptions, Simple scenarios
- **Prediction:** Anticipating how a test will fail
- **Red/Green/Refactor hats:** Physical hats representing cycle phases
- **Hexagon:** The boundary of pure domain code
- **Domain objects:** Objects that represent business concepts, not technical concerns

### Hexagonal Architecture Insights

**Package structure:**
- Created `domain` package as boundary
- "Everything inside of it is pure business pure application meaning it has nothing to do with technical stuff for the outside world"

**Trigger for creating domain objects:**
- "Product name being just a string is a bit suspicious"
- "We should really be thinking about domain objects"
- BUT waits until tests provide enough information

**API design:**
- "A lot of people think about apis as just having to do with web apis but api is just a programming interface"
- Thinks about what the domain API should look like independent of framework

### Notes
- Solo coding - different dynamic than pairing
- Uses physical red/green/refactor hats as visual metaphor
- Very explicit about thought process
- Strong emphasis on prediction and failing "for the right reason"
- Resists premature abstraction - waits for tests to guide design
- Domain-first approach, will add adapters later
- Side-by-side layout: test on left, production code on right

---
