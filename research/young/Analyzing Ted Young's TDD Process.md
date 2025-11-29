# **The JitterTed Methodology: A Comprehensive Analysis of Predictive TDD, Architectural Determinism, and the Nullable
Pattern**

## **1\. Introduction: The Search for Determinism in Software Engineering**

The landscape of modern software development is often characterized by a tension between speed of delivery and the
reliability of the resulting system. In this context, the work of Ted M. Young, known widely in the developer community
as "JitterTed," represents a significant codified effort to resolve this tension through rigorous process refinement and
architectural discipline. Young’s methodology is not merely a collection of tips but a cohesive philosophy rooted in
eXtreme Programming (XP) principles, evolved to address the specific pathologies of contemporary enterprise application
development, particularly within the Java and Spring Boot ecosystems.

This report provides an exhaustive analysis of Young's application building process. It synthesizes data from his
technical writings, public source code repositories (specifically yacht-tdd, ensembler, and tdd-game), conference
presentations, and community discussions. The analysis reveals a distinct pedagogical and practical framework centered
on two pillars: **Predictive Test-Driven Development (PTDD)**—a refinement of TDD designed to eliminate cognitive
bias—and a bifurcated testing philosophy that strictly separates **I/O-Free** logic from **I/O-Dependent**
infrastructure. Furthermore, this report tracks the evolution of Young's architectural thought, documenting the shift
from classical **Hexagonal Architecture** toward the **Nullable Pattern** (Testing Without Mocks), a collaboration with
James Shore that prioritizes state-based verification over interaction-based mocking.

The following sections dissect these methodologies, offering a granular reconstruction of the workflow, detailed code
analysis, and a theoretical examination of the underlying principles that distinguish the "JitterTed" approach from
standard industry practices.

## **2\. Predictive Test-Driven Development (PTDD): The Science of the Failing Test**

While Test-Driven Development (TDD) is a well-established practice, Young identifies a critical failure mode in its
typical execution: the "False Negative." In standard TDD, a developer writes a test and runs it, expecting it to fail.
If it fails, they proceed. However, Young argues that without a precise prediction of *how* the test fails, the
developer cannot be certain the test is validating the correct behavior. It might fail due to a compilation error, a
misconfigured harness, or a null pointer exception in the setup phase. If the developer assumes this failure confirms
the missing feature, they are building on a foundation of sand.

**Predictive TDD (PTDD)** creates a cognitive forcing function to prevent this. It transforms the "Red" phase of TDD
from a passive observation into an active scientific experiment.

### **2.1 The Step-by-Step PTDD Workflow**

Young’s documented process 1 breaks the implementation cycle into granular micro-steps, each serving a specific
verification purpose.

#### **Phase 1: Clarifying the Goal (Behavior Definition)**

The cycle begins not with code, but with a precise definition of the desired behavioral change. Young emphasizes that
TDD is primarily a design activity, not a testing activity.

* **The Defining Question:** "What should the system do, and exactly how will we know it did it?".3
* **Methodology:** The developer must articulate the "Given-When-Then" scenario. This forces the use of domain
  terminology (e.g., "Given a Player with 2 cards, When they Draw, Then they have 3 cards") before any implementation
  details are considered. This step creates the "hypothesis" for the experiment.

#### **Phase 2: The Prediction Cycle (The "Red" Phase)**

This is the core differentiator of PTDD.

1. **Write the Test for Non-Existent Code:** The developer writes a test case that references methods or classes that do
   not yet exist.
2. **Predict Compilation Failure:**
    * *Action:* The developer explicitly acknowledges that the code will not compile.
    * *Resolution:* Write the *minimum* code necessary to satisfy the compiler. This usually involves generating the
      class or method signature and returning a default value (e.g., 0, false, null).1 **Do not implement logic.**
3. **Predict the Runtime Failure:**
    * *Action:* Before running the test, the developer must predict the exact failure message (e.g., "Expected: 3, but
      was: 0").
    * *Constraint:* This prediction should ideally be vocalized or written down to prevent hindsight bias ("I knew it
      would fail that way").
    * *Validation:* Run the test. If the actual failure message matches the predicted failure message, the experiment is
      valid. If the message differs (e.g., NullPointerException instead of AssertionError), the test setup is flawed,
      and the developer must pause to fix the harness rather than implementing the feature.

#### **Phase 3: The Implementation (The "Green" Phase)**

1. **Least Effort Implementation:** The developer writes the absolute minimum amount of production code required to make
   the test pass.2
    * *Technique:* "Sins" such as hardcoding return values or ignoring edge cases are encouraged here. The goal is to
      confirm that the test can pass, establishing a baseline.
2. **Verify Green:** Run the test to confirm it passes.

#### **Phase 4: Tightening Assertions (The Correctness Loop)**

Young introduces "Tightening Assertions" as a bridge between the "Least Effort" hack and the robust production code.4

* **The Scenario:** Suppose the requirement is to draw a card from a deck. A "Least Effort" implementation might just
  increment a counter or add null to a list to satisfy a .hasSize(3) assertion.
* **The Problem:** The test passes, but the behavior is wrong (the list contains nulls, or the card wasn't actually
  drawn from the deck).
* **The Fix:** Instead of jumping straight to the complex implementation, the developer "tightens" the assertion.
    * *From:* assertThat(hand).hasSize(3)
    * *To:* assertThat(hand).doesNotContainNull()
* **The Cycle Repeats:** The developer predicts the new failure ("Expected list not to contain null"), sees it fail, and
  *then* improves the implementation to instantiate a real Card object. This stepwise refinement ensures that every line
  of production code is directly pulled into existence by a specific test requirement.

#### **Phase 5: Refactoring (Increasing Changeability)**

Once the behavior is correct and protected by tight assertions, the focus shifts to "Increasing Changeability".3

* **Action:** Refactor the code to improve design, remove duplication, and clarify intent.
* **Safety Net:** The existing tests ensure that these structural changes do not alter behavior.

### **2.2 Comparison: Traditional TDD vs. Predictive TDD**

The following table summarizes the operational differences between the standard approach and Young's Predictive model.

| Feature                     | Traditional TDD                             | Predictive TDD (PTDD)                                                      |
|:----------------------------|:--------------------------------------------|:---------------------------------------------------------------------------|
| **Mindset**                 | "Test First"                                | "Hypothesis First"                                                         |
| **Red Phase**               | Run test, verify it is red.                 | Predict *exact* failure message, then verify match.                        |
| **Handling Compile Errors** | Often fixed implicitly while writing logic. | Explicit step; fix compilation *only*, then run to see assertion fail.     |
| **Implementation**          | Write code to pass test.                    | Write "Least Effort" (hardcoded) code; Refine via "Tightening Assertions." |
| **Feedback Loop**           | Code correctness.                           | Understanding of the system state \+ Code correctness.                     |
| **Primary Risk Mitigated**  | Missing requirements.                       | False negatives (tests that fail for the wrong reason).                    |

## **3\. Testing Philosophy: The I/O-Free vs. I/O-Dependent Taxonomy**

A cornerstone of the JitterTed application building process is the rejection of the industry-standard nomenclature of "
Unit" and "Integration" tests. Young argues these terms are fraught with ambiguity and historical baggage.5 For example,
a test that checks a class's interaction with a database is often called an integration test, but if that database is an
in-memory H2 instance, some might call it a unit test. This confusion leads to inconsistent testing strategies and slow
suites.

Young proposes a binary taxonomy based on a strictly technical characteristic: the presence of **Input/Output (I/O)**.

### **3.1 I/O-Free Tests**

**Definition:** Tests that execute code entirely within the application's process memory boundaries. They never touch
the file system, network, database, or system clock.5

* **Characteristics:**
    * **Determinism:** 100%. These tests will execute identically every time, on every machine, regardless of network
      conditions.
    * **Speed:** Microsecond to millisecond execution times. Thousands can run in seconds.
    * **Scope:** These tests cover the "Domain" logic—Entities, Value Objects, and algorithmic policy.
    * **Strategic Value:** Young advocates pushing the vast majority (e.g., \>90%) of complexity into the I/O-Free zone.
      This allows complex business rules to be verified instantaneously.

### **3.2 I/O-Dependent Tests**

**Definition:** Any test that crosses the process boundary. This includes:

* Database queries (even local ones).
* HTTP requests (even to localhost).
* File system reads/writes.
* Interactions with System.currentTimeMillis() or java.util.Random (as these are non-deterministic inputs from the
  environment).5
* **Characteristics:**
    * **Fragility:** Susceptible to environment failures (e.g., port conflicts, disk full, network latency).
    * **Speed:** Orders of magnitude slower than I/O-Free tests.
    * **Scope:** Restricted to "Adapters" and "Integration" layers. Their sole purpose is to verify that the application
      correctly communicates with the outside world (e.g., "Did I generate the correct SQL syntax?" or "Did I parse the
      JSON response correctly?").

### **3.3 Architectural Implications**

This philosophy drives architectural decisions. If a piece of logic is difficult to test because it requires a database
state, Young’s process mandates a refactoring to decouple the logic (I/O-Free) from the persistence (I/O-Dependent).

* **Refactoring Pattern:** Extract the decision-making code into a domain entity that takes data as a simple argument,
  returning a result. The I/O-Dependent code then strictly acts as a pipeline, fetching data, calling the domain, and
  saving the result, with zero logic of its own.9

## **4\. Architectural Evolution: From Hexagonal to Nullables**

Young’s public work demonstrates a clear trajectory in architectural thinking. Initially a staunch advocate of *
*Hexagonal Architecture** (Ports and Adapters), his recent collaboration with James Shore on the "Nullables" pattern (
Testing Without Mocks) suggests a move toward what Shore terms **A-Frame Architecture**. This evolution is documented in
the transition from the ensembler codebase to the refactored yacht-tdd codebase.

### **4.1 Hexagonal Architecture (The Ensembler Model)**

In the ensembler repository, Young implements a classic Hexagonal Architecture.10

#### **4.1.1 Structure and Components**

* **The Hexagon (Core Domain):** This is the center of the application, containing the business logic. It has no
  dependencies on the outside world (frameworks, databases, UIs).
    * *Evidence:* The src structure often isolates domain packages to prevent accidental coupling.
* **Ports:** Interfaces defined by the Domain to interact with the outside world.
    * **Inbound Ports:** Interfaces the UI calls (often the Application Service).
    * **Outbound Ports:** Interfaces the Domain calls to save state or send notifications (e.g., MemberRepository,
      Notifier).8
* **Adapters:** Implementations of the ports.
    * **Inbound Adapters:** Spring MVC Controllers that receive HTTP requests and call the Inbound Ports.
    * **Outbound Adapters:** Classes that implement MemberRepository using Spring Data JDBC or JPA to talk to Postgres.8

#### **4.1.2 Testing Strategy in Hexagonal**

* **Domain Tests:** Strictly I/O-Free. They instantiate the domain objects directly and mock the Outbound Ports.
* **Adapter Tests:** I/O-Dependent. These use tools like **TestContainers** (Docker) to spin up a real Postgres database
  to verify that the JdbcMemberRepository correctly maps the Member object to SQL rows.10
    * Snippet 10 confirms the use of PostgresTestcontainerBase in ensembler, highlighting the commitment to realistic
      I/O tests for adapters.

### **4.2 The Shift to "Testing Without Mocks" (The Yacht-TDD Model)**

While Hexagonal Architecture separates concerns, the testing often relies heavily on **Interaction-Based Testing** (
using Mocks/Spies). Young and Shore identified that this leads to brittle tests that are coupled to implementation
details (e.g., verifying that save() was called exactly once).

To address this, Young adopted the **Nullable Pattern** in the yacht-tdd project.12

#### **4.2.1 The Nullable Pattern Defined**

The Nullable Pattern makes infrastructure classes "sociable" and capable of disabling their own I/O. Instead of mocking
a class, you use the real class, but configure it to be "Null."

The createNull() Factory:  
Infrastructure wrappers (e.g., a class wrapping RestTemplate or HttpClient) are modified to include a static factory
method createNull().

* **Production:** HttpScoreCategoryNotifier.create() returns an instance connected to the real web service.
* **Testing:** HttpScoreCategoryNotifier.createNull() returns an instance where the network call is bypassed, and the
  side effect is stored in an internal list for verification.14

#### **4.2.2 State-Based Verification**

Instead of asserting on method calls (Interaction Testing), Nullables allow **State-Based Testing**.

* *Mock Approach:* verify(notifier).send(category);
* Nullable Approach: assertThat(notifier.tracker().output()).contains(category);  
  This decouples the test from the internal implementation of how the notification is sent, focusing only on the fact
  that it was sent.15

#### **4.2.3 Embedded Stubs**

For deep infrastructure dependencies like java.util.Random or specific third-party libraries, the Nullable class uses
an "Embedded Stub."

* **Concept:** A lightweight implementation of the dependency is hidden *inside* the wrapper class.
* **Benefit:** The test code doesn't need to know about the complexity of the third-party library; it just calls
  createNull() and configures the desired behavior (e.g., "the next die roll is a 6").14

## **5\. Case Studies: Practical Implementations in Code**

### **5.1 Case Study 1: yacht-tdd Refactoring**

The jitterted/yacht-tdd repository serves as the primary educational artifact for the transition to Nullables.

* **Before Refactoring (before-nullables tag):** The code utilized standard Spring idiomatic testing with @MockBean and
  Mockito. Tests verified that controllers called services and services called repositories.12
* **The Refactoring Process:**
    * **DieRoller:** The random number generation was a source of non-determinism.
    * *Old Way:* Inject a Random instance or a DieRoller interface and Mock it.
    * *New Way (Nullable):* The DieRoller class became a concrete class with createNull(Integer... rolls).  
      Java  
      // Conceptual reconstruction from   
      DieRoller roller \= DieRoller.createNull(6, 6, 3, 2, 1);  
      assertThat(roller.roll()).isEqualTo(6);  
      assertThat(roller.roll()).isEqualTo(6);

    * This allows the tests to drive the game logic deterministically without setting up complex mock expectations.12
* **Infrastructure Wrappers:** The ScoreCategoryNotifier (which sends scores to an external tracker) was converted to
  use an embedded list for tracking output when in "Null" mode. This enabled the tests to verify that the correct score
  was "sent" without ever making a network call or spinning up a mock server.13

### **5.2 Case Study 2: ensembler Production Code**

The ensembler project represents Young's approach to a complex, persistent domain model.

* **TestContainers Integration:** Snippets confirm the use of PostgresTestcontainerBase.10 This demonstrates the "
  I/O-Dependent" philosophy: when you *must* test I/O, do it against the real thing (Dockerized Postgres) rather than an
  in-memory H2 database, which might behave differently (e.g., different SQL dialect or locking semantics).
* **Hexagonal Boundaries:** The project uses MemberRepository as an interface. The domain logic (e.g., assigning members
  to an ensemble) operates purely on Member objects. The persistence layer (I/O-Dependent) is strictly responsible for
  saving the state of those objects. This separation allows the complex scheduling logic to be tested via high-speed
  I/O-Free tests.8

### **5.3 Case Study 3: tdd-game and create-for-test**

In the tdd-game repository, Young employs a precursor to the Nullable pattern: the create-for-test factory method.17

* **Problem:** Some game states are difficult to reach through the public API (e.g., a specific late-game scenario).
* **Solution:** A static factory method Game.createForTest(...) allows the test to instantiate the Game aggregate in a
  specific state. This violates strict encapsulation for the sake of testability, a trade-off Young accepts to ensure
  all states are verifiable without complex setup scripts.

## **6\. Workflow, Tooling, and Community**

### **6.1 Outside-In Development**

Young advocates for an **Outside-In** development flow, often referred to as the "Walking Skeleton" approach.15

1. **Start at the Edge:** Write a broad integration test (I/O-Dependent) that hits the external API (e.g., an HTTP
   Endpoint).
    * *Goal:* Define the contract and the "shape" of the interaction.
2. **Drive the Internal Design:** As the Controller implementation requires logic, it "pulls" the need for Domain
   objects into existence.
3. **Switch to Narrow Tests:** Once the Domain object is identified (e.g., Game class), switch to I/O-Free PTDD to
   rigorously implement the business rules.
4. **Connect the Loop:** Return to the integration test and wire the verified Domain object into the Controller.

This ensures that no domain logic is written unless it is actually required by the external interface (YAGNI \- You
Ain't Gonna Need It).

### **6.2 The Role of Ensemble Programming**

Young rarely codes in isolation. His workflow is deeply influenced by **Ensemble Programming** (Mob Programming), which
he streams live on Twitch and manages via his Discord community.17

* **Process Impact:** The "Predict the Failure" step of PTDD is reinforced by the ensemble environment. The driver (
  person typing) must communicate the prediction to the navigators (observers), making the implicit explicit.
* **Continuous Code Review:** Developing ensembler live on stream means the code is subject to constant, real-time peer
  review, enforcing high readability and adherence to the architecture.13

### **6.3 Tooling**

* **IDE:** IntelliJ IDEA is the primary tool. Young emphasizes mastery of automated refactorings (Extract Method,
  Introduce Parameter) to make the "Refactor" step of TDD instantaneous and safe.20
* **Assertion Library:** **AssertJ** is critical to the PTDD process. Its fluent API (e.g., .assertThat().hasSize()
  .doesNotContainNull()) produces human-readable failure messages, which are essential for the "Prediction" phase.
  Standard JUnit assertions often produce vague messages that make precise prediction difficult.4

## **7\. Comprehensive Summary**

Ted M. Young's application building process is a discipline of **constraint**. By constraining how tests are written (
PTDD), constraining where I/O is allowed (I/O-Free vs Dependent), and constraining how dependencies are handled (
Nullables), he eliminates the two greatest enemies of software maintenance: non-determinism and cognitive bias.

His methodology moves beyond the "Red-Green-Refactor" mantra, expanding it into a rigorous scientific loop:

1. **Hypothesis:** "I believe this new test will fail with message X."
2. **Experiment:** Run the test and verify message X.
3. **Correction:** Write least-effort code to pass.
4. **Refinement:** Tighten assertions until the implementation is robust.
5. **Optimization:** Refactor for changeability.

This process, supported by architectures that strictly isolate the domain from the infrastructure, results in systems
that are testable by default, where the test suite acts not just as a verification tool, but as a living documentation
of the system's behavior and the developer's intent. The transition from Mocks to Nullables represents the final
maturity of this philosophy: removing the last vestiges of coupling to implementation details to achieve purely
state-based, deterministic verification.

## **8\. Appendix: Code Reference**

### **8.1 Example of "Tightening Assertions" (Reconstructed)**

Java

// Phase 1: Loose Assertion  
@Test  
void handHasThreeCards() {  
Game game \= new Game();  
game.deal();  
assertThat(game.hand()).hasSize(3);  
// Prediction: Fails (size is 0\)  
// Implementation: hand.add(null); hand.add(null); hand.add(null);  
}

// Phase 2: Tightened Assertion  
@Test  
void handHasThreeValidCards() {  
Game game \= new Game();  
game.deal();  
assertThat(game.hand())  
.hasSize(3)  
.doesNotContainNull();  
// Prediction: Fails (contains nulls)  
// Implementation: hand.add(new Card());...  
}

### **8.2 Example of Nullable Infrastructure Wrapper**

Java

public class HttpScoreCategoryNotifier {  
private final RestTemplate restTemplate;  
private final OutputTracker\<ScoreCategory\> tracker;

    // Private constructor: real mode  
    private HttpScoreCategoryNotifier(RestTemplate restTemplate) {  
        this.restTemplate \= restTemplate;  
        this.tracker \= null;  
    }

    // Private constructor: nullable mode  
    private HttpScoreCategoryNotifier(OutputTracker\<ScoreCategory\> tracker) {  
        this.restTemplate \= null;  
        this.tracker \= tracker;  
    }

    public static HttpScoreCategoryNotifier create() {  
        return new HttpScoreCategoryNotifier(new RestTemplate());  
    }

    public static HttpScoreCategoryNotifier createNull() {  
        return new HttpScoreCategoryNotifier(new OutputTracker\<\>());  
    }

    public void send(ScoreCategory category) {  
        if (tracker\!= null) {  
            tracker.track(category);  
            return;  
        }  
        restTemplate.postForEntity("...", category, Void.class);  
    }  
      
    // Test-only method to observe state  
    public OutputTracker\<ScoreCategory\> tracker() {  
        return tracker;  
    }  

}

#### **Works cited**

1. Predicting the Failing Test | Ted M. Young, accessed November 28,
   2025, [https://ted.dev/articles/2021/11/05/predicting-the-failing-test/](https://ted.dev/articles/2021/11/05/predicting-the-failing-test/)
2. Implementing the Feature | Ted M. Young, accessed November 28,
   2025, [https://ted.dev/articles/2022/05/09/implementing-the-feature/](https://ted.dev/articles/2022/05/09/implementing-the-feature/)
3. Clarifying the Goal of Behavior Change | Ted M. Young, accessed November 28,
   2025, [https://ted.dev/articles/2021/03/05/clarifying-the-goal-of-behavior-change/](https://ted.dev/articles/2021/03/05/clarifying-the-goal-of-behavior-change/)
4. Tightening Our Assertions | Ted M. Young, accessed November 28,
   2025, [https://ted.dev/articles/2022/06/22/tightening-our-assertions/](https://ted.dev/articles/2022/06/22/tightening-our-assertions/)
5. I'm Done with Unit and Integration Tests | Ted M. Young, accessed November 28,
   2025, [https://ted.dev/articles/2023/04/02/i-m-done-with-unit-and-integration-tests/](https://ted.dev/articles/2023/04/02/i-m-done-with-unit-and-integration-tests/)
6. accessed November 28,
   2025, [https://burkhardstubert.substack.com/p/episode-40-better-built-by-burkhard\#:\~:text=O%2DBased).-,Ted%20M.,anything%20outside%20the%20current%20process%E2%80%9D.](https://burkhardstubert.substack.com/p/episode-40-better-built-by-burkhard#:~:text=O%2DBased\)
   .-,Ted%20M.,anything%20outside%20the%20current%20process%E2%80%9D.)
7. If you mock, are you even testing? \- Understand Legacy Code, accessed November 28,
   2025, [https://understandlegacycode.com/blog/if-you-mock-are-you-even-testing/](https://understandlegacycode.com/blog/if-you-mock-are-you-even-testing/)
8. Hexagonal Testable Architecture (preso-ensembler) \- Feb 2023 \- Ted M. Young, accessed November 28,
   2025, [https://ted.dev/assets/Hexagonal%20Testable%20Architecture%20by%20Ted%20M.%20Young%20-%20Feb%202023.pdf](https://ted.dev/assets/Hexagonal%20Testable%20Architecture%20by%20Ted%20M.%20Young%20-%20Feb%202023.pdf)
9. Event Bus: Inside or Outside the Hexagon? | Ted M. Young, accessed November 28,
   2025, [https://ted.dev/articles/2022/07/29/event-bus-inside-or-outside-the-hexagon/](https://ted.dev/articles/2022/07/29/event-bus-inside-or-outside-the-hexagon/)
10. jitterted/ensembler: Ensembler: the Remote Ensemble Registration System \- GitHub, accessed November 28,
    2025, [https://github.com/jitterted/ensembler](https://github.com/jitterted/ensembler)
11. Refactoring to Hexagonal Architecture \- Ted M. Young, accessed November 28,
    2025, [https://ted.dev/refactoring-to-hexagonal-architecture.html](https://ted.dev/refactoring-to-hexagonal-architecture.html)
12. jitterted/yacht-tdd \- GitHub, accessed November 28,
    2025, [https://github.com/jitterted/yacht-tdd](https://github.com/jitterted/yacht-tdd)
13. Nullables & A-Frame Architecture Livestream \- James Shore, accessed November 28,
    2025, [https://www.jamesshore.com/v2/projects/nullables/jitterted-livestream](https://www.jamesshore.com/v2/projects/nullables/jitterted-livestream)
14. James Shore: "23/ Nullables are production c…" \- Mastodon, accessed November 28,
    2025, [https://mastodon.online/@jamesshore/109560427847976182](https://mastodon.online/@jamesshore/109560427847976182)
15. Testing Without Mocks: A Pattern Language \- James Shore, accessed November 28,
    2025, [http://www.jamesshore.com/v2/blog/2018/testing-without-mocks](http://www.jamesshore.com/v2/blog/2018/testing-without-mocks)
16. Decision-Driven-Development/output-tracking: Java ... \- GitHub, accessed November 28,
    2025, [https://github.com/Decision-Driven-Development/output-tracking](https://github.com/Decision-Driven-Development/output-tracking)
17. Online version of JitterTed's TDD Game \- GitHub, accessed November 28,
    2025, [https://github.com/jitterted/tdd-game](https://github.com/jitterted/tdd-game)
18. Ask HN: Have you created programs for only your personal use? \- Hacker News, accessed November 28,
    2025, [https://news.ycombinator.com/item?id=31018836](https://news.ycombinator.com/item?id=31018836)
19. Nullables & A-Frame Architecture with Ted M. Young (Part 1\) \- YouTube, accessed November 28,
    2025, [https://www.youtube.com/watch?v=DGQl8Wg4y4M](https://www.youtube.com/watch?v=DGQl8Wg4y4M)
20. An implementation of the casino game Blackjack, to use as the basis for demonstrating refactoring techniques in
    IntelliJ IDEA. \- GitHub, accessed November 28,
    2025, [https://github.com/jitterted/refactoring-blackjack](https://github.com/jitterted/refactoring-blackjack)