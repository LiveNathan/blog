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

## Refactoring Test Code: Creating Test Data Builders

**Video URL:** https://www.youtube.com/watch?v=OJhHdLdDE-o
**Relevance:** VERY HIGH - Concrete refactoring technique for test setup
**Guest:** Solo (Ted only)

### Feature/App Context
Live refactoring session extracting test data builders from existing test code. Demonstrates how to make test setup less verbose and more focused on what matters for each test. Working on member/huddle registration code.

### Problem Being Solved
- Test setup is verbose and repetitive
- Tests create multiple repositories unintentionally
- Hard to tell what's important vs required boilerplate
- Constructor parameters pollute tests with irrelevant details

### Test Data Builder Pattern

**Goal:** Hide irrelevant setup details, expose only what matters for each test

**Before:**
```java
MemberRepository repository = new InMemoryMemberRepository();
Member member = MemberFactory.create(repository, "John", "john@example.com", 
    "johngithub", List.of(Role.USER, Role.MEMBER));
MemberService service = new MemberService(repository);
```

**After:**
```java
Member member = new MemberBuilder()
    .withEmail("john@example.com")
    .build();
```

### Refactoring Steps

1. **Start with existing factory method**
   - Identify verbose setup code
   - Look for duplication across tests

2. **Create builder class**
   - Extract to `MemberBuilder` class
   - Add fluent `with*()` methods
   - Return `this` from each method

3. **Add defaults for common cases**
   - Auto-create repository if not specified
   - Generate IDs automatically
   - Use default roles if not specified

4. **Extract method by method**
   ```java
   public MemberBuilder withFirstName(String firstName) {
       this.firstName = firstName;
       return this;
   }
   ```

5. **Build method creates actual object**
   ```java
   public Member build() {
       Member member = new Member(repository, firstName, email, githubUsername, roles);
       return member;
   }
   ```

6. **Share repositories across builders**
   - Builder holds repository reference
   - Prevents accidentally creating multiple disconnected repos
   - Can query builder for its repository

### Key Principles

**1. Realistic Objects Over Mocks**
> "I'm creating full-fledged member objects... I prefer realistic objects that are executing the real object code than than mocks"

- Build real domain objects, not mocks
- Use in-memory implementations for ports
- Test with actual behavior, not stubbed behavior

**2. Show What's Important**
> "Now it's showing what's important which is i do need the first name because that gets specified here and i need the email because that gets specified there"

- Only specify what the test cares about
- Hide required-but-irrelevant details
- Make tests self-documenting

**3. Defaults for Common Cases**
```java
// Default: member has email
new MemberBuilder().build()

// Explicit: member has no email
new MemberBuilder().withNoEmail().build()
```

**4. Shared State Management**
- Builder can hold services (MemberService)
- Builder can hold repositories
- Prevents duplication and disconnected objects

### Code Patterns Observed

**Fluent interface:**
```java
Member member = new MemberBuilder()
    .withFirstName("John")
    .withGithubUsername("johndoe")
    .withEmail("john@example.com")
    .build();
```

**Default repository:**
```java
private final MemberRepository repository = new InMemoryMemberRepository();
```

**Optional override:**
```java
public MemberBuilder withRepository(MemberRepository repository) {
    this.repository = repository;
    return this;
}
```

**Service creation:**
```java
public MemberService buildService() {
    build(); // Creates member first
    return new MemberService(repository);
}
```

### Benefits Demonstrated

**Before refactoring:**
- 10+ lines of setup
- Multiple repository instances created unintentionally
- Unclear what's important to each test

**After refactoring:**
- 1-3 lines of setup
- Single repository shared correctly
- Crystal clear what each test cares about

**Quote:**
> "The typical main benefit of a builder is you don't have to specify everything if you don't care about it even though the underlying objects need the github username need identifiers um need the roles uh for this test those aren't important"

### When to Use Test Data Builders

1. **Complex object graphs**
   - Many constructor parameters
   - Objects with required dependencies

2. **Repetitive setup across tests**
   - Same patterns appear in multiple tests
   - Only 1-2 values change between tests

3. **Accidental coupling**
   - Tests unintentionally share state
   - Multiple instances of same collaborator

### Implementation Tips

**Location:**
- In test source tree, not production
- Green background tab in IntelliJ indicates test code

**Naming:**
- `MemberBuilder`, `HuddleBuilder`
- Methods: `withX()`, `withNoX()`, `build()`

**Scope:**
- One builder per domain concept
- Can compose multiple builders

**Evolution:**
- Start simple, add methods as needed
- "Eventually I'll assemble multiple test data builders"

### Testing Philosophy

**Real objects preferred:**
> "A lot of the core domain stuff are real objects and that's why they're actually a little bit painful to set up... I'm almost always creating a real huddle"

**What to fake:**
- Ports (repository interfaces)
- External services
- NOT domain objects

**Repository pattern:**
- Use in-memory implementations for tests
- Test actual repository implementation separately
- "I don't have a lot of custom queries yet... I'll write tests against the directly against the repository"

### Refactoring Safety

- Ran tests after each change
- "We're relying on the tests to continue to pass to let us know that we've done the right thing"
- Committed after all tests green

### Notes
- Live refactoring session - shows thinking process
- Addressed chat questions throughout
- Very practical, immediately applicable pattern
- Solves real pain point (multiple disconnected repositories)
- Makes tests more maintainable and readable

---

## Creating Ensembler - Episode 5: "Register Participant"

**Video URL:** https://www.youtube.com/watch?v=_UVD4fZzOFw
**Relevance:** HIGH - Service layer TDD, repository patterns, outside-in workflow
**Guest:** Solo (Ted only)

### Feature/App Context
Building participant registration for mob programming huddles. Shows complete outside-in flow from controller → service → domain. Demonstrates service layer testing and repository usage patterns.

### Workflow Observed - Outside-In Progression

#### Starting Point
- **Layer:** Controller (web adapter)
- **Approach:** "Wing it" at controller to discover service needs
- **Then:** Write tests for service layer

#### Progression
1. **Controller (no test)** → Sketch what the service should look like
   - Trigger: "I'm going to sort of put this on pause so I can actually write some tests for it"
   - Pattern: Create method signature, then write tests
   - Decision: Skip controller test due to security complexity

2. **Service test** → Tests `registerParticipant(huddleId, name, githubUsername)`
   - Trigger: "Now I know what this now I know what the [service needs]"
   - Test: Registers participant, then verifies huddle contains that participant
   - Pattern: "This is more almost more of a sanity test than than anything really driving"

3. **Domain method** → `huddle.register(participant)`
   - Already tested from previous episode
   - Service delegates to domain object

### Testing Philosophy - Service Layer

**Delegation Tests:**
> "I don't feel a strong need to to test this but I'll I'll write a test anyway... these are mostly just delegation right"

- Service tests are often delegation to domain + repository
- Not test-driven in strict sense - more "sanity tests"
- Real value is in domain tests, not service tests

**What the service does:**
1. Repository lookup (find huddle by ID)
2. Call domain method (huddle.register)
3. Repository save

**Test structure:**
```java
@Test
void registerParticipantAddsParticipantToHuddle() {
    // Setup
    long huddleId = repository.save(new Huddle(...))

    // Execute
    huddleService.registerParticipant(huddleId, "John", "johngithub");
    
    // Verify
    Huddle huddle = repository.findById(huddleId);
    assertThat(huddle.participants()).containsExactly(new Participant("John", "johngithub"));
}
```

### Repository Patterns

**In-memory for tests:**
- Uses `InMemoryHuddleRepository`
- Saves and retrieves without database
- Fast, no I/O

**ID generation:**
> "I need the ID so I need to put this directly in the repository"

- Repository returns ID after save
- Tests use real IDs from repository
- Not mocking IDs

**Repository methods:**
```java
repository.save(huddle);           // Persist
repository.findById(id);           // Retrieve
repository.findById(id).orElseThrow(); // Retrieve or fail
```

**Exception handling:**
```java
repository.findById(huddleId)
    .orElseThrow(() -> new HuddleNotFoundException(huddleId));
```

### Outside-In Discovery Process

**Quote:**
> "What I'm doing is sort of this outside in development I'm trying to figure out what is the what is the web UI need from from the service and then now I can start uh testing driving"

**Process:**
1. Start at controller
2. Sketch what service method should look like
3. Pause controller work
4. Drop down to service layer
5. Write service tests
6. Service delegates to domain
7. Domain already tested

**Why sketch first:**
- Discover API shape
- Understand what parameters needed
- Then write proper tests

### Prediction (or lack thereof)

**Forgot to predict:**
> "Oh I forgot to to predict see I'm out of practice"

Shows even experienced TDD practitioners slip:
- Ran test without predicting
- Caught himself
- Shows importance of prediction discipline

### Application Initialization Pattern

**@Component ApplicationRunner:**
```java
@Component
class DataLoader implements ApplicationRunner {
    @Override
    public void run(ApplicationArguments args) {
        huddleRepository.save(new Huddle(...))
    }
}
```

**Purpose:**
- Pre-load data for manual testing
- Runs on application startup
- Avoids recreating test data manually

### Naming Consistency

**Struggled with naming:**
- `participant.name` vs `participant.fullName`
- `participant.githubUsername` (all lowercase) vs `participant.gitHubUsername` (camelCase)
- Refactored several times for consistency

**Quote:**
> "Clearly I am inconsistent"

Shows real refactoring - names matter, even when technically correct

### DTOs for Web Layer

**RegistrationForm:**
```java
class RegistrationForm {
    private String name;
    private String githubUsername;
    
    // Getters/setters required (not a record)
}
```

**Why not record:**
> "Records were fine but pushing information in seemed to not work not sure why"

- Spring form binding needs mutability
- Records are immutable
- Use regular class for form DTOs

### Domain Boundaries

**User vs Participant:**
- User = OAuth2 authenticated user (from GitHub)
- Participant = domain concept (person in huddle)
- One-to-many relationship
- Kept separate to avoid coupling to auth implementation

**Quote about domain boundary:**
> "I tend not to like abstract classes for stuff that links to things that are not in my control"

### Service Layer Placement

**In domain package:**
> "The service is in the domain... speaks in sort of domain terms"

- Service translates from web concepts to domain
- Controller handles conversion from HTTP to domain types
- Service only deals with domain objects

**Example:**
```java
// Controller does conversion
ZonedDateTime scheduleTime = ZonedDateTime.parse(scheduleTimeString);

// Service takes domain types
huddleService.schedule(scheduleTime, name);
```

**Why:**
> "This information is coming from the browser and so the controller is responsible for translating... this service specifically is speaking in the language of the domain"

### Value Objects Discussion

**Not yet created:**
> "These are definitely things that could be replaced with value objects um and eventually I'll I'll do that"

- Knows they should be value objects
- Using primitives for now
- Will refactor when needed
- Pragmatic approach

### Notes
- Solo stream with chat interaction
- Addressed questions while coding
- Showed real struggles (naming, prediction)
- Very pragmatic: skip tests when expedient (security), write "sanity tests" when unsure
- Application Runner for manual testing
- Outside-in but not strictly test-first at every layer

---

## Testable Architecture Keep 'em Separated (Conference Talk)

**Video URL:** Not provided (transcript only)
**Relevance:** HIGH - Architectural philosophy and principles, not live coding
**Format:** Conference presentation

### Feature/App Context

Not a coding session - this is Ted's conference talk explaining the philosophy behind hexagonal architecture and
testable architecture. Demonstrates refactoring untestable code into testable code with code examples but not live TDD.

### Presentation Context

Condensed version of Ted's 4-day course on testable architecture. Focuses on WHY we separate concerns and HOW to
organize code for testability. Uses a sales tax calculator example to show refactoring from mixed concerns to separated
concerns.

### Key Architectural Principles

#### Definition of I/O

> "IO is anything that runs outside of the current process you're in... anything that's outside the JVM is IO because in
> order to communicate with that, you have to do IO."

**Includes:**

- Hardware (system clock, random numbers)
- Local files
- Remote services over HTTP
- Databases (even in-memory ones like H2, SQLite)
- Frameworks (Spring, Quarkus, etc.)

**Why this matters:**

- I/O is slow and unpredictable
- I/O makes testing difficult
- Business doesn't care about I/O details (CSV vs database)
- Business DOES care about logic/rules

#### Separation Principle

> "SCOINT - Separating Concerns of IO and Non-IO for Testability"

**Goal:** Split code into two pieces:

1. **I/O stuff** - system.in, system.out, HTTP, databases, frameworks
2. **Business logic** - rules, calculations, domain concerns

**Benefits:**

- Easy to test business logic directly
- Reusable across different I/O mechanisms (CLI → web → events)
- Can change I/O without touching logic
- Fast feedback loops

### Hexagonal Architecture Philosophy

#### Coburn's Original Goals

> "Allow an application to be equally driven by users, programs, and automated tests"

**Key insight:**

- User interactions and test interactions should use SAME code
- No if-statements for "if test, do this; if user, do that"
- Tests are first-class citizens

#### Inside vs Outside

- **Inside (hexagon):** Important business domain logic, no connection to I/O
- **Outside:** All the "other crap" to make it work and integrate

#### Inbound vs Outbound (not Driving/Driven)

> "Driving and driven is the original terminology... I don't like it because it's very confusing... I prefer inbound and
> outbound"

- **Inbound (left side):** Triggers, inputs, requests
- **Outbound (right side):** Outputs, events, side effects

#### Three Layers (Ted's modification)

**1. Domain Layer:**
> "Domain has no idea that the world exists... thinking about things like tickets and concerts"

- Pure platonic ideal
- No knowledge of I/O
- No concept that external systems exist
- Business terminology and rules only

**2. Application Layer:**
> "Application layer says, 'Oh, well, there's some things out there like persistence and I have to notify things'"

- Coordinates domain objects
- Has CONCEPT of I/O but no concrete references
- Knows "notification" exists, not SMTP vs POP vs text
- Orchestration logic

**3. Adapters:**

- Plug into the hexagon (ports)
- Transform external data to domain types
- Validate and translate
- Examples: UI, message queues, REST controllers

**Dependencies must flow inward:**
> "The dependencies must flow inward... domain cannot know IO, not allowed, no can do"

### Testing Approach

#### Test Categories (not Unit/Integration)

> "Those terms are terrible. Every time somebody says unit, I say what do you mean what is a unit?... What's important
> is it use IO or not."

**I/O Free Tests:**

- Against domain layer
- No mocks, no test doubles needed
- Just instantiate objects
- Fast, comprehensive
- Most of your tests

**I/O-Based Tests:**

- Against adapters
- Use test doubles for ports
- Check: did it call the right thing at the right time?
- Fewer of these, just enough to verify integration

**Application Layer Tests:**

- Plug in test doubles for ports
- Test orchestration logic
- Still I/O-free (using in-memory implementations)

### Code Example - Sales Tax Calculator

#### Before (Mixed Concerns):

```java
// Display menu (I/O)
Scanner scanner = new Scanner(System.in);
int choice = scanner.nextInt();

// Business logic mixed in
switch(choice){
        case 1->amount *0.08;
        case 2->amount *0.10;
        case 3->amount *0.05;
        }

// Display result (I/O)
        System.out.

println(receipt);
```

**Problem:** Testing requires hijacking System.out/System.in - "like trying to turn on a light switch with a 10-ft pole"

#### After (Separated):

**I/O Code:**

```java
// Handle terminal interaction
int choice = getChoiceFromUser();
String receipt = computeReceipt(choice);

displayReceipt(receipt);
```

**Business Logic:**

```java
String computeReceipt(int choice) {
    // Pure calculation, easy to test
    return switch (choice) {
        case 1 -> calculateWithTax(0.08);
        // ...
    };
}
```

**Test becomes trivial:**

```java

@Test
void computeReceiptForChoiceOne() {
    String receipt = computeReceipt(1);
    assertThat(receipt).contains("...");
}
```

### Reusability Benefit

**CLI → Web API:**

```java

@PostMapping("/receipt")
String createReceipt(@RequestParam("choice") String choiceStr) {
    int choice = Integer.parseInt(choiceStr);
    return computeReceipt(choice);  // Same logic!
}
```

**Web → Kafka:**
> "If you separated it out, easy peasy"

Didn't have to change domain logic, just add new adapter

### Example Application - Ensembler

Ted's mob programming ensemble management app (open source)

**Ports/Adapters:**

- SendGrid emailer (notification port)
- Zoom scheduler (scheduling port)

**Test Types Shown:**

**Domain tests:**

```java
// No mocks, just objects
Ensemble ensemble = new Ensemble();
ensemble.

addMember(member);

assertThat(ensemble.members()).

contains(member);
```

**Application layer tests:**

```java
// Plug in test double
EnsembleService service = new EnsembleService(testRepository);
service.

cancelMeeting(meetingId);

verify(testRepository).

delete(meetingId);  // Or use spy pattern
```

**Adapter tests:**

```java
// Did it send to Zoom correctly?
ZoomAdapter adapter = new ZoomAdapter(testZoomApi);
adapter.

schedule(meeting);

verify(testZoomApi).

createMeeting(/* ... */);
```

### Testing Philosophy Summary

**Fast feedback is critical:**
> "If I run a test and it takes less than a second, I'm going to be running that pretty frequently... the second I make
> a mistake, I will find out"

**Separation makes tests easier:**
> "If you find code that has lots of mixture of these concerns and it's hard to test without doing lots of mocking...
> refactor"

**I hate mocking frameworks:**
> "I'm on the record as saying I hate them. They have their use but I hate them because they lead people to do things
> like not separate concerns"

**Testing in isolation:**
> "I can test that domain logic in isolation. And I can also isolate other parts"

### Related Architecture Patterns

All these are "the same thing except for the details":

- Clean Architecture (Uncle Bob)
- **Hexagonal Architecture** (Alistair Cockburn) - Ted's favorite
- Onion Architecture
- Imperative Shell, Functional Core
- Boundary Controller Entity (BCE)
- A-Frame (James Shore)

**Common goal:** Important business/domain logic separated from I/O

### Trade-offs

**Increase testability → Lose simplicity:**
> "It's not all in one big file. I'm okay with that"

**Continuum:**

- Some teams stuff more into domain
- Some teams break into more pieces
- It's all trade-offs
- Pick what works for your team

**Ted's position:**
> "If you want your code to be easier to test, keep them separated"

### Key Terminology

- **Hexagon:** The boundary of pure domain + application layers
- **Ports:** Interfaces the hexagon exposes
- **Adapters:** Implementations that plug into ports
- **I/O:** Anything outside the current process (hardware, files, network, frameworks)
- **Domain:** Business logic with no knowledge of outside world
- **Application Layer:** Coordination logic, knows I/O exists conceptually
- **Inbound/Outbound:** Triggers vs side effects (better than driving/driven)

### What This Transcript DOESN'T Cover

**Not workflow-focused:**

- No step-by-step TDD process
- No "start here, then drop down to service layer"
- No red-green-refactor cycle demonstration
- No live coding or test-first discipline

**This is philosophy/principles:**

- WHY separate concerns
- WHAT hexagonal architecture is
- HOW to think about I/O vs domain
- Test categorization (I/O-free vs I/O-based)

### Workflow Implications

While not a workflow transcript, this provides the FOUNDATION for Ted's workflow:

1. **Domain-first when possible** - Pure logic, no I/O
2. **Application layer for coordination** - Knows about ports
3. **Adapters last** - Thin translation layers
4. **Test at all layers** - Mostly I/O-free (domain), some I/O-based (adapters)
5. **Dependencies inward** - Domain can't reference I/O

### Notes

- Not a coding session - conference presentation
- Provides philosophical foundation for his workflow
- Explains WHY he structures code the way he does in other videos
- Good reference for architecture principles
- Example code is simplified for presentation (not real TDD session)
- Open source Ensembler app available for reference

---
