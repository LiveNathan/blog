# Ted M. Young's Outside-In TDD Workflow - Synthesis

**Status:** Comprehensive synthesis from 7 high-value transcripts
**Last Updated:** 2025-11-28 (Enhanced)
**Source Material:** Song Themes Eps 1-2, TDD Exercise Part 1, Test Data Builders, Ensembler Ep 5, Hex Arch webinar

---

## Executive Summary

Ted's TDD workflow is characterized by:
1. **Outside-in progression** - Start at the edge (web/API), work inward to domain
2. **Test categorization** - IO-based (slow, framework) vs IO-free (fast, pure)
3. **Incremental steps** - ZOMBIES progression (Zero, One, Many...)
4. **Prediction-driven** - Predict failures before running tests
5. **Defer decisions** - "Last responsible moment" for abstractions
6. **Domain purity** - Hexagonal architecture keeps domain framework-free
7. **Test data builders** - Refactor complex setup for clarity and correctness
8. **Realistic objects** - Prefer real implementations over mocks

---

## The Core TDD Cycle

### Red → Green → Refactor

**Red Phase (Write Failing Test):**
1. Write test that doesn't compile
2. **Predict** how it will fail
3. Make it compile (create classes/methods)
4. Run test
5. Verify it fails "for the right reason"

**Green Phase (Make It Pass):**
1. Write **least amount of code** to pass
2. Hardcode values if possible ("fake it till you make it")
3. Return literal values before generalizing
4. Get to green quickly

**Refactor Phase:**
1. Look for duplication (between test and code)
2. Look for code smells
3. Extract objects when you have enough information
4. **Don't premature**ly abstract

---

## Outside-In Layer Progression

### 1. Choose Your Starting Layer

**For Queries (Read Operations):**
- Start at MVC/Web layer OR
- Start at subcutaneous (service) layer
- Rationale: "How do I verify if it worked? By seeing the results"

**For Commands (Write Operations):**
- Generally start closer to domain
- (Needs more data from additional transcripts)

### 2. Layer Sequence for Web Apps

```
MVC Test (framework)
    ↓
Controller Test (direct, no framework)
    ↓
Service/Domain Test
    ↓
Adapter Test (if needed)
```

### 3. When to Use Each Test Type

**MVC Tests (@Tag("io")):**
- Framework configuration
- POST/GET mappings correct
- Redirects work
- Status codes correct
- **Minimal number** - "I want the fewest minimalist tests that use the framework because they are slow"
- One or two per endpoint usually sufficient

**Direct Controller Tests (no tag):**
- Business logic in controller
- Parameter handling
- Model population
- Return value checking
- "Anything I can do that does not require the framework I will do without the framework"

**Service/Domain Tests (no tag):**
- Pure business logic
- No framework dependencies
- Fast execution
- Majority of tests here

---

## ZOMBIES Progression

**Z**ero - Baseline case (empty cart = 0)
**O**ne - Single item (add one product)
**M**any - Multiple items
**B**oundaries - Edge cases
**I**nterfaces - Different implementations
**E**xceptions - Error cases
**S**imple scenarios - Simplest path

### Applying ZOMBIES

1. **Start with Zero:**
   - Empty list returns empty
   - Empty cart has price of 0
   - Search for non-existent theme returns nothing

2. **Move to One:**
   - One item in list
   - One product in cart
   - One song matches theme

3. **Then Many:**
   - Multiple items
   - Multiple products
   - Multiple songs

**Quote:** "We've done the zero case an empty cart done the one case where we add one so really kind of need to do the many case"

---

## Test Categorization System

### IO-based vs IO-free

**IO-based tests** (`@Tag("io")`):
- Require Spring context
- Touch database/network/filesystem
- Use MockMvc
- Slow
- Examples: MVC tests, repository tests

**IO-free tests** (untagged):
- Pure unit tests
- No framework
- No external dependencies
- Fast
- Examples: Domain tests, direct controller tests

### Run Configurations

Create separate IntelliJ run configurations:
1. **All Tests** - No tag filter
2. **IO based** - Filter: `tags: io`
3. **IO free** - Filter: `tags: !io`

**Quote:** "The scheme I follow is I want the fewest minimal minimalist tests that actually use the framework because they are slow"

---

## Key Principles

### 1. Prediction

- **Always predict** how a test will fail before running it
- Ensures you're testing what you think you're testing
- "One of the important parts about both my game and the process is the prediction"

### 2. Fake It Till You Make It

- Return hardcoded values first
- Throw `UnsupportedOperationException` to force failure
- Return -1 or null to ensure test fails
- Generalize only when you have duplication

**Quote:** "I don't want to return 0 because the test I'm about to write is gonna be assert that that it's zero and that'll pass so I don't want it to pass"

### 3. Last Responsible Moment

- Defer design decisions until you have enough information
- Start with primitives (String, int) before creating domain objects
- Extract objects from working code rather than creating upfront

**Quotes:**
- "Make the decision at the last responsible moment"
- "Start with Primitives until you know what you need"
- "My preference is to extract objects from code that already exists"

### 4. Minimal Code to Pass

- Don't write more code than needed to pass current test
- Resist temptation to handle future cases
- Let tests drive the design incrementally

### 5. Test-First Discipline

- Never commit with failing tests
- Can leave failing test as "breadcrumb" for next session (but don't push)
- Commit frequently when green

---

## Testing Patterns

### Test Naming

- **Descriptive camelCase** method names
- NO `@DisplayName` annotation
- Pattern: `searchForNonExistentThemeReturnsNoResults()`
- Pattern: `emptyCartHasTotalPriceOfZero()`
- Pattern: `postToSearchEndpointRedirectsToResults()`

**Quote:** "Why not just make the method name descriptive"

### Test Structure - Arrange/Act/Assert

**Ted's approach:**
1. Sketch the assertion first
2. Work backward to setup
3. Introduces variables as needed

```java
// 1. Start with assertion
assertThat(songs).isEmpty();

// 2. Add the call
List<String> songs = searcher.search("applesauce");

// 3. Add setup
SongSearcher searcher = new SongSearcher();
```

### Method Naming in Production Code

- Query methods: `totalPrice()` NOT `getTotalPrice()`
- Rationale: "We're asking what is your price, not getting internal state"
- No "get" prefix for query methods
- Emphasizes behavior over data access

---

## Hexagonal Architecture Integration

### Package Structure

```
src/main/java/
  domain/          ← Pure business logic, no framework
    Cart.java
    Product.java
  application/     ← Use cases, orchestration
  adapter/
    web/           ← Controllers
      SongThemesController.java
    persistence/   ← Repositories
```

### The Domain Boundary

**What goes IN the domain:**
- Business rules
- Calculations
- Value objects
- Domain entities

**What stays OUT of the domain:**
- Spring annotations
- HTTP concerns
- Database access
- External service calls

**Quote:** "Adding domain to me does these magical things one is it all of a sudden says no code here can reference anything hardware io outside world related"

### Bridging Domain and Framework

**In @SpringBootApplication class:**
```java
@Bean
public SongSearcher songSearcher() {
    return new SongSearcher();
}
```

- Domain class is framework-free
- Spring wires it up via @Bean method
- Controllers use constructor injection (no @Autowired on domain classes)

---

## Controller Testing Strategy

### Two-Level Testing

**Level 1: MVC Test (Framework)**
```java
@WebMvcTest(SongThemesController.class)
@Tag("io")
class SongThemesMvcTest {
    @Test
    void getToSearchEndpointReturns200() {
        mockMvc.perform(get("/theme-search"))
            .andExpect(status().is2xxSuccessful());
    }
}
```

**Purpose:** Verify Spring configuration (mappings, redirects, status codes)

**Level 2: Direct Controller Test (No Framework)**
```java
class SongThemesControllerTest {
    @Test
    void searchReturnsModelWithEmptySearchResults() {
        SongSearcher searcher = SongSearcher.withSongsForTheme("applesauce");
        SongThemesController controller = new SongThemesController(searcher);
        Model model = new ExtendedModelMap();

        controller.themeSearch("", model);

        assertThat(model.getAttribute("emptySearchResults")).isEqualTo(true);
    }
}
```

**Purpose:** Test controller logic without framework overhead

**Quote:** "Even though the controller is in hexagonal architecture an adapter class it doesn't mean all your tests have to be integration tests"

---

## Refactoring Patterns

### When to Refactor

1. **Duplication** - Between test and code
2. **Code smells** - Long methods, primitive obsession
3. **Three strikes** - Third time you see the same pattern
4. **Green tests** - Only refactor when tests pass

### Refactoring Under Red (Cautiously)

Ted occasionally refactors with failing test:
1. Comment out the failing test
2. Verify all other tests pass
3. Do the refactoring
4. Uncomment the test
5. Make it pass

**Quote:** "I'm going to do a refactoring even though i've got a failing test I know but to be really sure i'm going to basically comment out this test"

### Factory Methods for Test Setup

**Progression:**
```java
// 1. Initial - explicit constructor
new SongSearcher("New Year's", "Auld Lang Syne")

// 2. Extract to factory method
SongSearcher.withOneSong("New Year's", "Auld Lang Syne")

// 3. Hide implementation details
SongSearcher.withSongsForTheme("applesauce")  // don't care about songs
```

---

## Common Mistakes to Avoid

### 1. Starting Too High-Level
- Don't write full story-level tests first
- Break down to smallest testable behavior
- ZOMBIES helps with this

### 2. Premature Abstraction
- Don't create domain objects until tests demand them
- Start with primitives
- Wait for duplication to emerge

### 3. Too Many Framework Tests
- Minimize MVC tests
- Most tests should be IO-free
- Framework tests are slow

### 4. Skipping Prediction
- Always predict how test will fail
- Ensures test is actually testing something
- Catches copy-paste errors

### 5. Not Committing Frequently
- Commit after each green
- Small commits
- Don't push failing tests

---

## Ted's Development Tools

### IDE Usage (IntelliJ IDEA)
- Heavy use of refactoring tools
- Alt+Enter for quick fixes
- Ctrl+Alt+M for extract method
- Ctrl+Alt+P for introduce parameter
- Ctrl+Alt+F for introduce field

### Test Organization
- Side-by-side: test on left, production on right
- Jump between: Ctrl+Shift+T
- Run configurations for IO/IO-free separation

---

## Open Questions / Need More Data

1. **Starting layer for commands** - More examples needed
2. **Adapter testing** - Database/external service adapter patterns
3. **Integration testing** - Full stack test strategies
4. **View layer** - Thymeleaf/HTML testing approach
5. **Refactoring triggers** - When to extract classes vs keep simple
6. **Event Storming → Code** - How does DDD modeling translate to first tests?

---

## Quotes Collection

### On Test Speed
> "The scheme I follow is I want the fewest minimal minimalist tests that actually use the framework because they are slow"

### On Framework vs Non-Framework Tests
> "If it's something that is basically around configuring the framework so post mapping endpoints redirection... those are going to require the framework. Anything I can do that does not require the framework I will do without the framework"

### On Controller Testing
> "Even though the controller is in hexagonal architecture an adapter class it doesn't mean all your tests have to be integration tests"

### On Deferring Decisions
> "Make the decision at the last responsible moment"
> "Start with Primitives until you know what you need"

### On Object Extraction
> "My preference is to extract objects from code that already exists somehow that feels more natural for me"

### On Prediction
> "One of the important parts about both my game and the process is the prediction. We want to predict that the test must fail and for the right reason"

### On ZOMBIES
> "When I'm thinking about the first test I want to write I'm thinking about what are the fewest number of elements I can get away with"

### On Method Naming
> "Note it's not get total price it is total price it is a query method we're asking the cart what is your current total price we are not getting"

### On Domain Packages
> "Adding domain to me does these magical things one is it all of a sudden says no code here can reference anything hardware io outside world related"

---

## Next Steps for Research

1. Process more Song Themes episodes for:
   - Adding data (commands/write operations)
   - Database integration
   - View layer (Thymeleaf) testing

2. Process Ensembler series for:
   - Different domain
   - Event sourcing patterns
   - Different architectural decisions

3. Process Kid-Bank series for:
   - CSV import (file I/O)
   - Cloud deployment considerations

4. Look for episodes covering:
   - Adapter testing
   - Repository patterns
   - Error handling/exceptions

---

**Synthesis Status:** This is a preliminary synthesis from 4 transcripts. Core workflow patterns are well-established, but additional episodes will add nuance and fill gaps.

---

## Test Data Builders Pattern

### Problem Solved

**Verbose test setup** pollutes tests with required-but-irrelevant details:
```java
// Before: Unclear what's important
MemberRepository repository = new InMemoryMemberRepository();
Member member = new Member(repository, "John", "john@example.com", 
    "johngithub", List.of(Role.USER, Role.MEMBER));
MemberService service = new MemberService(repository);
```

**After:**
```java
// After: Crystal clear what matters
Member member = new MemberBuilder()
    .withEmail("john@example.com")
    .build();
```

### When to Use

1. **Complex object graphs** - Many constructor parameters or dependencies
2. **Repetitive setup** - Same patterns across multiple tests
3. **Accidental coupling** - Tests unintentionally share state or create multiple disconnected instances

### Implementation Pattern

**Builder structure:**
```java
public class MemberBuilder {
    private MemberRepository repository = new InMemoryMemberRepository();
    private String firstName = "DefaultFirst";
    private String email = "default@example.com";
    private String githubUsername = "defaultuser";
    private List<Role> roles = List.of(Role.USER, Role.MEMBER);
    
    public MemberBuilder withEmail(String email) {
        this.email = email;
        return this;
    }
    
    public MemberBuilder withNoEmail() {
        this.email = null;
        return this;
    }
    
    public Member build() {
        Member member = new Member(repository, firstName, email, 
            githubUsername, roles);
        return repository.save(member); // Auto-persist
    }
    
    public MemberRepository getRepository() {
        return repository; // Share with other builders
    }
}
```

### Key Principles

**1. Build Real Objects, Not Mocks**

> "I'm creating full-fledged member objects... I prefer realistic objects that are executing the real object code than than mocks"

- Use real domain objects
- Use in-memory implementations for ports
- Test actual behavior, not stubbed responses

**2. Expose Only What Matters**

> "Now it's showing what's important which is i do need the first name because that gets specified here and i need the email because that gets specified there"

- Default values for common cases
- Explicit methods for variations
- Hide required-but-irrelevant details

**3. Share Repositories**

**Problem:**
```java
// Accidental bug: Two disconnected repositories
MemberRepository repo1 = new InMemoryMemberRepository();
Member member = new Member(repo1, ...);

MemberRepository repo2 = new InMemoryMemberRepository(); // OOPS!
MemberService service = new MemberService(repo2); // Won't find member
```

**Solution:**
```java
MemberBuilder builder = new MemberBuilder();
Member member = builder.build();
MemberService service = new MemberService(builder.getRepository());
```

### Benefits

**Conciseness:**
- 10+ lines → 1-3 lines
- Only specify what's different

**Clarity:**
- Test shows intent clearly
- Required details hidden

**Correctness:**
- Prevents repository duplication bugs
- Consistent test data

**Quote:**
> "The typical main benefit of a builder is you don't have to specify everything if you don't care about it even though the underlying objects need the github username need identifiers um need the roles uh for this test those aren't important"

---

## Service Layer Testing

### Service Layer Role

**Orchestration, not business logic:**
1. Retrieve from repository
2. Call domain method
3. Save back to repository

**Example:**
```java
public class HuddleService {
    private final HuddleRepository repository;
    
    public void registerParticipant(long huddleId, String name, String githubUsername) {
        Huddle huddle = repository.findById(huddleId)
            .orElseThrow(() -> new HuddleNotFoundException(huddleId));
        
        huddle.register(new Participant(name, githubUsername));
        
        repository.save(huddle);
    }
}
```

### Testing Philosophy

**Delegation tests are "sanity tests":**

> "I don't feel a strong need to to test this but I'll I'll write a test anyway... these are mostly just delegation right"

- Service tests verify orchestration, not business logic
- Business logic tested in domain layer
- Service tests often written after implementation (pragmatic)

**Test structure:**
```java
@Test
void registerParticipantAddsParticipantToHuddle() {
    // Arrange
    long huddleId = repository.save(new Huddle(...));
    
    // Act
    huddleService.registerParticipant(huddleId, "John", "johngithub");
    
    // Assert
    Huddle huddle = repository.findById(huddleId);
    assertThat(huddle.participants())
        .containsExactly(new Participant("John", "johngithub"));
}
```

### Service Placement

**In domain package:**

> "The service is in the domain... speaks in sort of domain terms"

- Takes domain types, not HTTP types
- Controller translates from web → domain
- Service orchestrates domain objects

**Example:**
```java
// Controller handles HTTP → domain conversion
@PostMapping("/schedule")
public String schedule(@RequestParam String dateTimeString) {
    ZonedDateTime scheduleTime = ZonedDateTime.parse(dateTimeString);
    huddleService.schedule(scheduleTime); // Domain type
    return "redirect:/huddles";
}
```

**Why:**
> "This information is coming from the browser and so the controller is responsible for translating... this service specifically is speaking in the language of the domain"

---

## Repository Patterns

### In-Memory for Tests

**Always use in-memory implementations:**
```java
public class InMemoryHuddleRepository implements HuddleRepository {
    private final Map<Long, Huddle> storage = new HashMap<>();
    private long nextId = 1L;
    
    @Override
    public Huddle save(Huddle huddle) {
        huddle.setId(nextId++);
        storage.put(huddle.getId(), huddle);
        return huddle;
    }
    
    @Override
    public Optional<Huddle> findById(Long id) {
        return Optional.ofNullable(storage.get(id));
    }
}
```

**Benefits:**
- Fast (no I/O)
- No database setup required
- Tests run in milliseconds
- Can be shared across test classes

### ID Generation

**Repository returns ID after save:**
```java
// Test uses real ID from repository
long huddleId = repository.save(new Huddle(...));

// Later in test
Huddle retrieved = repository.findById(huddleId);
```

**Don't mock IDs** - use real ones from in-memory repo

### Exception Handling

**orElseThrow pattern:**
```java
repository.findById(huddleId)
    .orElseThrow(() -> new HuddleNotFoundException(huddleId));
```

Creates specific domain exception when not found

### Testing Repositories

**Test actual implementation separately:**

> "If I'm concerned that the repository that maybe i don't understand the repository implementation or either sql or object like sql then i'll write tests against the directly against the repository"

- Test JPA/SQL repositories with database (tagged @Tag("io"))
- Use in-memory in other tests
- Assume repository works once tested

**Custom queries:**
> "I don't have a lot of custom queries yet... I'll write tests against the directly against the repository"

If you have complex queries, test them against real database

---

## Enhanced Outside-In Workflow

### Discovery Process

**Quote:**
> "What I'm doing is sort of this outside in development I'm trying to figure out what is the what is the web UI need from from the service and then now I can start uh testing driving"

**Steps:**
1. Start at controller (adapter layer)
2. Sketch what service should look like
3. "Pause" controller work
4. Drop down to service layer
5. Write service tests (if needed - often just sanity tests)
6. Drop to domain if business logic needed
7. Return to controller and wire it up

### Example Flow

**1. Controller (sketch only):**
```java
@PostMapping("/register")
public String register(@PathVariable Long huddleId,
                      @RequestParam String name,
                      @RequestParam String githubUsername) {
    huddleService.registerParticipant(huddleId, name, githubUsername);
    return "redirect:/huddles/" + huddleId;
}
```

**2. Service (test-driven):**
```java
@Test
void registerParticipantAddsToHuddle() {
    long id = repository.save(new Huddle(...));
    
    service.registerParticipant(id, "John", "johngithub");
    
    assertThat(repository.findById(id).participants())
        .contains(new Participant("John", "johngithub"));
}
```

**3. Domain (test-driven):**
```java
@Test
void huddleCanRegisterParticipant() {
    Huddle huddle = new Huddle();
    
    huddle.register(new Participant("John", "johngithub"));
    
    assertThat(huddle.participants())
        .contains(new Participant("John", "johngithub"));
}
```

### When to Skip Tests

**Pragmatic approach:**
- Skip controller tests when authentication blocks testing
- Skip service tests when they're pure delegation
- Focus testing energy on domain logic

**Quote (Ensembler Ep 5):**
> "I'm going to wing it which I would not normally do"

Shows even strict TDD practitioners make pragmatic choices

---

## Application Initialization

### @Component ApplicationRunner Pattern

**For manual testing during development:**
```java
@Component
public class DataLoader implements ApplicationRunner {
    private final HuddleRepository repository;
    
    @Override
    public void run(ApplicationArguments args) {
        repository.save(new Huddle(
            "Mob Programming",
            ZonedDateTime.now().plusDays(7)
        ));
    }
}
```

**Purpose:**
- Pre-load data on startup
- Enables manual UI testing
- Avoids recreating test data manually

**Why:**
> "I'm going to actually persist uh the the huddles because constantly recreating them"

Before full database persistence, use this for manual testing

---

## DTOs and Value Objects

### DTOs for Web Layer

**Use mutable classes for Spring form binding:**
```java
public class RegistrationForm {
    private String name;
    private String githubUsername;
    
    // Getters/setters required
}
```

**Why not records:**
> "Records were fine but pushing information in seemed to not work not sure why"

Spring form binding requires mutability

### Value Objects in Domain

**Primitive obsession → Value objects:**
```java
// Initially: primitives
public class Participant {
    private String name;
    private String githubUsername;
}

// Eventually: value objects
public class Participant {
    private PersonName name;
    private GitHubUsername githubUsername;
}
```

**Timing:**
> "These are definitely things that could be replaced with value objects um and eventually I'll I'll do that"

- Start with primitives
- Refactor to value objects when needed
- Pragmatic, not dogmatic

---

## Updated Open Questions → Answers

### ~~Starting layer for commands~~ → Answered

**For commands (write operations):**
- Start at controller (outside-in)
- Sketch service API
- Drop to service tests
- Drop to domain if business logic needed

**Example:** Register participant (Ensembler Ep 5)

### ~~Adapter testing~~ → Answered

**Repository adapters:**
- Test separately with @Tag("io")
- Use actual database
- Test custom queries directly
- Assume it works in other tests (use in-memory)

### ~~Service layer testing~~ → Answered

**Service tests are delegation/sanity tests:**
- Not strictly TDD (often written after)
- Verify orchestration, not logic
- Business logic tested in domain
- Can skip if pure delegation

---

## Remaining Open Questions

1. **View layer** - Thymeleaf/HTML testing approach (needs more examples)
2. **Event Storming → Code** - How DDD modeling translates to first tests (partially shown in Song Themes Ep 1)
3. **Full persistence** - Testing with actual database, migrations, transaction boundaries
4. **Error handling** - Exception testing patterns across layers
5. **Refactoring at scale** - When to extract classes vs keep simple (needs more examples)

---

## Updated Synthesis Status

**Source Material:** 7 high-value transcripts
- Song Themes Eps 1-2
- TDD & Hexagonal Architecture Exercise Part 1  
- Refactoring Test Code: Test Data Builders
- Creating Ensembler Episode 5
- More Testable Code with Hexagonal Architecture (partial)

**Coverage:**
- ✅ Outside-in web flow (MVC → Controller → Service → Domain)
- ✅ Pure domain TDD with ZOMBIES
- ✅ Test categorization (IO vs IO-free)
- ✅ Test data builders for setup refactoring
- ✅ Service layer testing patterns
- ✅ Repository testing with in-memory implementations
- ✅ Application initialization patterns
- ✅ DTO vs Value Object decisions

**Ready for blog post creation.**

