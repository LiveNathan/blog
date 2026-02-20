---
layout: post
title: "How to Test Embabel Agents – The Missing Guide"
date: 2026-02-19 09:00:00 -0000
categories: [java, spring, tdd, llm, ai, embabel]
---

What's the hardest thing about writing tests?

The setup.

No one wants to write tests because no one wants to stop to think about the setup. What input do you need? How do you get it? What output do you expect?

Luckily, Embabel provides a fake OperationContext out of the box. Unluckily, that won't get you very far. The fake that Embabel provides will help you with a single builder test and that's it. That will help you get started and make sure that you wrote the builder correctly, but it won't help you with the really important stuff – actually testing the agent.

*What's a fake?* A fake is a kind of test double. It is a lightweight implementation of a dependency, typically with some in-memory implementation, used to mimic real behavior without the complexity of the real system.

As Rod Johnson [has famously said](https://youtu.be/yMDw0nlWd7s?list=TLGGY--hTTVlTXAyMDAyMjAyNg)

> we need to attack non-determinism because that is the biggest single problem

To do that, we need to test the agent.

This is the missing guide.

## Embabel, I love you.

Before I met you, working with LLMs was unpredictable and painful. I had big giant tests with 122 assertions. Thanks to your framework, and examples, I found a more reliable and enjoyable way to work. The only thing missing in your documentation is how to test a real implementation of an agent. Please feel free to use anything I've written here, and if I've made any mistakes, know that they are all my own and not because of you.

## The boring stuff

Let's get the boring stuff out of the way. We'll use the fake OperationContext to lock the builder values in place.

Let's build a simple agent to classify user input as a query or a command. We love TDD, so we'll start with a failing test.

I'll show abbreviated versions here to keep things readable, but you can find the full code on [GitHub](https://github.com/LiveNathan/embabeltests).

```java
@Test
void givenUserInput_whenClassifying_thenBuildsLlmInteractionCorrectly() {
    // Given
    String userInput = "What is the capital of Portugal?";
    ClassificationAgent.ClassifiedIntents dummyResponse = new ClassificationAgent.ClassifiedIntents(
            Set.of(new ClassificationAgent.RequestFragment("any", QUERY)));
    FakeOperationContext context = FakeOperationContext.create();
    context.expectResponse(dummyResponse);
    ClassificationAgent agent = new ClassificationAgent();

    // When
    agent.classify(userInput, context.ai());

    // Then
    List<LlmInvocation> invocations = context.getLlmInvocations();
    assertThat(invocations)
            .as("Should call LLM exactly once")
            .hasSize(1);

    LlmInvocation invocation = invocations.getFirst();

    List<PromptContributor> examples = invocation.getInteraction().getPromptContributors();
    assertThat(examples)
            .as("Should provide four classification examples (query, command, other, multiple requests)")
            .hasSize(4);

    assertThat(invocation.getInteraction().getToolGroups())
            .as("Should not require any tools")
            .isEmpty();

    assertThat(invocation.getInteraction().getLlm().getTemperature())
            .as("Should use low temperature for consistent classification")
            .isEqualTo(0.1);
    //  For more assertions, see the full code on GitHub.
}
```

We expect the test to fail because there's no production code yet.

```java
ClassifiedIntents classify(String userInput, Ai ai) {
    return ai.withLlm(LlmOptions.withAutoLlm().withTemperature(TEMPERATURE))
            .withId(INTERACTION_ID)
            .creating(ClassifiedIntents.class)
            .withExample("Query example: Where's the lead vocal?", queryExample())
            .withExample("Command example: Rename channels 1-4 to RF 1-4", commandExample())
            .withExample("Other example: Hello there robot!", otherExample())
            .withExample("Multiple requests example: Where's the lead vocal? Send it to the vocal buss.", independentRequestsExample())
            .fromPrompt(buildPrompt(userInput));
}
```

Now the test passes as expected.

Could this large test be refactored into smaller ones? Yes. But it's not of great importance to me, so I just wanted to get it done.

Ok, now that we've gotten the boring stuff out of the way, let's do the fun stuff.

## The fun stuff

What do we expect the agent to do?

At a minimum it should return the expected output object. Beyond that, the output object should contain the expected content. Let's see if we can come up with an initial list of expectations to drive the design.
- [ ] classifiesGreetingAsOther
- [ ] classifiesQuestionAsQuery
- [ ] classifiesSingleCommandAsCommand
- [ ] splitsCompoundCommandIntoTwoFragments

What's the context? Why am I writing these tests in the first place?

I'm building a desktop app for live sound engineers called Console Whisperer to help with mixing console setup. I want it to answer questions about the console and make changes like channel names and colors, and I want it to do that in a fast, cheap, and reliable way. More on that later.

For these we need a real LLM. Enter `@SpringBootTest`.

```java
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.NONE)
class ClassificationAgentIntegrationTest {
    @Autowired
    private Ai ai;

    private ClassificationAgent agent;

    @BeforeEach
    void setUp() {
        agent = new ClassificationAgent();
    }
```

First test: does it return the right type for a basic input?

```java
@Test
void classifiesGreetingAsOther() {
    String userInput = "Bom dia amigo!";
    ClassificationAgent.ClassifiedIntents actual = agent.classify(userInput, ai);
    assertSingleFragment(actual, ClassificationAgent.RequestFragment.RequestType.OTHER);
}
```

This test will pass because it's so simple. Should we make it more complex or change the test to first convince ourselves that it fails for the expected reason? I'd say start simple. Earn complexity. If the agent regresses later, this test will catch it.

Add a couple more in the same pattern:

```java
@Test
void classifiesQuestionAsQuery() {
    String userInput = "What channel is the snare on?";
    ClassificationAgent.ClassifiedIntents actual = agent.classify(userInput, ai);
    assertSingleFragment(actual, ClassificationAgent.RequestFragment.RequestType.QUERY);
}

@Test
void classifiesSingleCommandAsCommand() {
    String userInput = "Channel 2 should be named kick out.";
    ClassificationAgent.ClassifiedIntents actual = agent.classify(userInput, ai);
    assertSingleFragment(actual, ClassificationAgent.RequestFragment.RequestType.COMMAND);
}
```

With a tiny helper to keep things readable:

```java
private void assertSingleFragment(ClassificationAgent.ClassifiedIntents result,
                                  ClassificationAgent.RequestFragment.RequestType expectedType) {
    assertThat(result.fragments())
            .hasSize(1)
            .extracting(ClassificationAgent.RequestFragment::type)
            .containsExactly(expectedType);
}
```

Now here's where it gets interesting. The real value of the agent isn't just classifying single inputs – it's splitting compound commands and resolving ambiguity. "Rename channels 1–4 to RF 1–4 and make them red" has a pronoun problem: "them" without context is useless to the next step in the pipeline. The agent needs to resolve it.

```java
@Test
void splitsCompoundCommandIntoTwoFragments() {
    String userInput = "Rename channels 1-4 to RF 1-4 and make them red";

    ClassificationAgent.ClassifiedIntents actual = agent.classify(userInput, ai);

    assertThat(actual.fragments())
            .hasSize(2)
            .allSatisfy(fragment -> assertThat(fragment.type())
                    .isEqualTo(ClassificationAgent.RequestFragment.RequestType.COMMAND))
            .extracting(ClassificationAgent.RequestFragment::description)
            .allSatisfy(description ->
                    assertThat(description)
                            .as("Each fragment should explicitly reference channels, not use pronouns like 'them'")
                            .containsIgnoringCase("channel"))
            .satisfiesExactlyInAnyOrder(
                    description -> assertThat(description).containsIgnoringCase("rename"),
                    description -> assertThat(description).containsIgnoringCase("red"));
}
```

This one test checks four things: fragment count, type, pronoun resolution, and content. When it fails, you know exactly which expectation broke. That's the fight.

One more. Mixed types in a single input:

```java
@Test
void splitsMixedInputIntoQueryAndCommand() {
    String userInput = "What channel is the snare on? Rename it to Snare Top.";

    ClassificationAgent.ClassifiedIntents actual = agent.classify(userInput, ai);

    assertThat(actual.fragments())
            .hasSize(2)
            .extracting(ClassificationAgent.RequestFragment::type)
            .containsExactlyInAnyOrder(
                    ClassificationAgent.RequestFragment.RequestType.QUERY,
                    ClassificationAgent.RequestFragment.RequestType.COMMAND);
}
```

## Fast, Cheap, and Reliable

Now that the tests are in place, use them to optimize your settings.

### Fast

Start by finding the fastest model that still passes. Change `LlmOptions.withAutoLlm()` to a specific model, run the tests, and record the latency. Repeat for several candidates.

### Cheap

Filter the passing models down to the cheapest. If you're on Ollama, smaller models cost nothing to run but vary wildly in quality — so let the tests decide. Start with something like `llama3.1:8b`. If the tests fail, go bigger. If they pass, try going smaller. You could even parameterize the model name and sweep across candidates automatically, as I did in [I Benchmarked 9 LLMs to Find the Cheapest for Multi-Turn Tool Calling with Spring AI](https://open.substack.com/pub/nathanlively/p/i-benchmarked-9-llms-to-find-cheapest-for-multi-turn-tool-calling-with-spring-aihtml?utm_campaign=post-expanded-share&utm_medium=web).

### Reliable

What's left after filtering for speed and cost is your reliability baseline. These are the models that pass all tests consistently. Run the suite a few times to confirm — LLMs are non-deterministic, so a single green run isn't enough. Once you've picked a model, commit that choice and let the tests catch regressions.

## Conclusion

Two test classes, two jobs:

1. `ClassificationAgentTest` – fast, no LLM, verifies the builder is wired correctly
2. `ClassificationAgentIntegrationTest` – slow, real LLM, verifies the agent actually works

The IO-free tests catch configuration mistakes. The IO tests catch the stuff that matters: does the agent do what you need? You can't guarantee the LLM will always respond the same way, but you can document your expectations and catch regressions when they happen.

How are you testing your LLM framework? Let me know in the comments.