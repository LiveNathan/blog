---
layout: post
title: "I Tested 20 Local LLMs with Docker and Ollama—0% Worked for Complex Tasks On My 2019 MacBook Pro"
date: 2025-10-27 08:00:00 -0000
categories: [ spring-ai, llm, java, spring-boot, ollama, docker, testing ]
---

# I Tested 20 Local LLMs with Docker and Ollama—0% Worked for Complex Tasks On My 2019 MacBook Pro

A few weeks ago,
I [benchmarked 9 cloud LLMs](https://nathanlively.substack.com/p/i-benchmarked-9-llms-to-find-cheapest-for-multi-turn-tool-calling-with-spring-ai.html?r=hhqf8)
for my AI mixing console assistant. Google Gemini 2.0 Flash won with 100% success rate and $0.0001 per conversation.

Then reality hit: Users want offline mode. Especially users in Australia, where cellular coverage can disappear once you
leave the cities. Can't use a cloud LLM without internet.

So I upgraded my test framework to support local models via Ollama—both containerized through Docker and running
directly. I tested ~20 different models.

**Spoiler:** None of them came close to cloud performance on my 2019 Intel MacBook Pro.

## Why Local Models Matter

Console Whisperer needs to work at outdoor venues, temporary installations, and remote locations where internet isn't
guaranteed. When someone's running sound for an event, they can't wait for connectivity issues to resolve.

The feature requests were clear: offline mode isn't optional.

## The Technical Upgrade

I extended my existing Spring AI test framework with two approaches:

### 1. Docker Containerized Ollama

The elegant solution: Start a Docker container with Ollama, pull the model, run tests, tear everything down. Zero manual
cleanup.

```java

@Testcontainers
class OllamaDockerTest {
    @Container
    static OllamaContainer ollama = new OllamaContainer("ollama/ollama:latest")
            .withModel("llama3.2:8b");

    // Tests run completely isolated
}
```

Complete automation from IntelliJ. No manually starting Ollama. No leftover models to clean up.

### 2. Direct Ollama Integration

The practical solution: Run Ollama as a native app, let Spring AI connect directly.

Both approaches use the same test harness—just different connection configurations. The test framework now supports
cloud providers (Google, OpenAI, DeepSeek, Groq, Mistral) and local models through a unified interface.

## The Results: Brutal Honesty

I tested ~20 models across two approaches. Here's what actually happened:

### Docker/Testcontainers: Complete Failure

**Simple Scenario (4 prompts):**

- Only 1 model worked: `qwen2.5:3b-instruct` (100% accuracy, 147 seconds)
- A few hit 80%: `llama3.2:1b`, `llama3.2:3b`, `llama3.2:3b-instruct-q4_0`
- Everything else: timeouts or 0% accuracy

**Complex Scenario (6 prompts):**

- **Every single model failed completely**
- 0% accuracy across the board
- Errors: timeouts, JSON conversion failures, complete breakdowns

### Direct Ollama: Marginally Better

**Simple Scenario:**

| Model                     | Time | Success | Accuracy |
|---------------------------|------|---------|----------|
| qwen2.5:3b-instruct       | 213s | 100%    | 100%     |
| llama3.2:1b-instruct-q8_0 | 109s | 100%    | 80%      |
| llama3.2:3b-instruct-q4_0 | 246s | 100%    | 80%      |
| llama3.2:1b               | 62s  | 100%    | 40%      |

**Complex Scenario:**

- Best performer: `llama3.2:1b` with 32% accuracy (219 seconds)
- Everything else: 0% or timeout
- JSON conversion errors everywhere

Compare that to cloud models: Gemini 2.0 Flash hits 100% accuracy in 10 seconds on simple tasks, 85% in 23 seconds on
complex tasks.

**The Timeout Reality:** Many models hit the 300-second (5 minute) timeout on individual test runs. That's not total
test time—that's *per iteration*.

## The Technical Failures

Beyond slow performance, several classes of errors emerged:

**JSON Conversion Failures:**

```
Conversion from JSON to java.util.List<ApiCall> failed
```

Models attempted tool calls but formatted the parameters incorrectly. Spring AI couldn't parse them.

**Tool Support Lies:**

```
{"error":"registry.ollama.ai/library/nous-hermes2:10.7b-solar-q4_0 does not support tools"}
```

Some models advertised tool support but rejected tool calls at runtime.

**Silent Failures:**
Many models completed successfully (100% success rate) but made zero actual tool calls (0% accuracy). They responded
with text instead of invoking functions.

**Thread Interrupts:**

```
Thread interrupted while sleeping
```

Even the test framework couldn't keep up with the resource demands.

## What "Lower Accuracy" Actually Means

The test sends commands like: "Change channels 1-5 to A, B, C, D, E, then rename channel B to 'Drums'."

Cloud LLMs nail this—perfect execution, 20 precise tool calls when needed.

Local models on my hardware?

- **Simple tasks (4 prompts):** Best got 80-100%, most got 20-40%
- **Complex tasks (6 prompts):** Best got 32%, most got 0%

They don't make *wrong* calls—they just make *fewer* calls. Expecting 20 tool invocations? You might get 10-15.

In practice: You'll send a command, it'll do X and Y but skip Z. You say "You missed Z," it handles it. Annoying, but
workable—for simple scenarios.

For complex multi-step operations? It falls apart completely.

## The Google Models Mystery

I expected Google's local models to shine since Gemini 2.0 Flash dominated the cloud tests.

Every single Google model failed with: "This model does not support tools."

That's a bug—either in Spring AI or Ollama's Google integration. I didn't dig into it. After trying 20 models, I just
picked the one that worked.

## Why This Happens (Probably)

My 2019 Intel MacBook Pro isn't built for this. I can run small models, but not well. The hardware constraints are real.

The solution: Test on actual user hardware. My customers have different machines—some probably better, some worse. I
need to see what models work on *their* setups, not mine.

### The Docker Mystery

Why did Docker performance completely collapse compared to direct Ollama?

**Theory 1: Resource Contention**
Docker Desktop on Mac runs in a VM. That VM has resource limits. Running LLM inference inside a container inside a VM on
a 2019 Intel laptop? Triple overhead.

**Theory 2: Model Loading**
Testcontainers pulls models fresh each time. Maybe the models weren't fully loaded or optimized? Direct Ollama keeps
models in memory between runs.

**Theory 3: I Have No Idea**
The accuracy dropping to 0% on all models is suspicious. Something fundamental breaks in the containerized setup beyond
just performance.

I didn't investigate further. Pragmatically: if Docker barely works on dev hardware, it definitely won't work for
production offline mode.

## What I'm Shipping Anyway

Based on testing, `qwen2.5:3b-instruct` performed best on simple tasks (100% accuracy, 3.5 minutes). But for real-world
use, I'm going with **Llama 3.2 3B** because:

- Consistent tool calling support
- Decent accuracy (80%) on basic operations
- More widely tested/documented
- Ollama's default ecosystem

Console Whisperer now has:

- Online/offline mode toggle
- Automatic detection of Ollama availability
- Llama 3.2 3B as the default local model
- Warnings when only one mode is available
- Clear expectations: simple commands work, complex multi-step operations need cloud

It's not perfect. Local mode is explicitly "reduced functionality." But it beats having no offline option.

## Future Improvements (Maybe)

Some ideas for handling lower accuracy:

**Multi-Agent Workflows:**

- Planning agent: Creates task list
- Execution agent: Runs the tasks
- Assessment agent: Validates completion

**Task Splitting:**

- Agent 1: Handle all channel names
- Agent 2: Handle all channel colors
- Reduces load per agent, might improve accuracy

**Automatic Model Selection:**

- App tests 10 models on first startup
- Keeps the best performer
- Deletes the rest

That last one would be pretty cool. Might build it.

## The Takeaway for Java Developers

If you're adding local LLM support to Spring AI apps:

1. **Testcontainers works—barely:** Great for CI/CD isolation, terrible for actual performance. Expect 0% accuracy on
   anything non-trivial.

2. **Direct Ollama is mandatory:** Skip Docker for real benchmarking. Performance gap is massive.

3. **Simple tasks only:** If your use case involves 1-3 prompts with straightforward tool calls, local models can hit
   80-100% accuracy. Anything more complex? Forget it.

4. **Set aggressive timeouts:** 300 seconds wasn't enough for some models. Simple 4-prompt tests taking 3-4 minutes is
   normal.

5. **Hardware matters more than you think:** My 2019 Intel MacBook Pro clearly wasn't sufficient. Test on your users'
   actual hardware.

6. **Best models for tool calling:**
    - `qwen2.5:3b-instruct` - 100% accuracy on simple tasks (but 3.5 min runtime)
    - `llama3.2:3b-instruct-q4_0` - 80% accuracy (4 min runtime)
    - Anything larger than 3B parameters? Prepare for timeouts.

7. **Complex scenarios need cloud:** Multi-step operations with 6+ prompts? Local models fail completely (0-32%
   accuracy). Keep cloud as primary, local as degraded fallback.

The test framework is ready. I can swap models anytime. And more importantly, I can distribute it to users to find what
actually works on their hardware.

**Production Strategy:**

- Cloud LLM for full functionality
- Local LLM for reduced offline mode
- Clear user expectations about capability differences
- Consider automatic model selection on first startup

## Resources

- [Test Code on GitHub](https://github.com/LiveNathan/cheapest-llm-tool-calling) (now with Ollama support)
- [Previous Cloud LLM Benchmark](https://nathanlively.substack.com/p/i-benchmarked-9-llms-to-find-cheapest-for-multi-turn-tool-calling-with-spring-ai.html?r=hhqf8)
- [Console Whisperer Demo](https://youtu.be/Kpb2Zm6Bd8A)

---

Building with AI: where conference demos show flawless "Hello World" examples, and production reality involves 3-hour
overnight test runs that return 0% accuracy. But hey, at least the Docker cleanup is automated.