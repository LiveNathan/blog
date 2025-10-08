You're absolutely right. I completely misread your story arc. The real narrative is:

1. You **thought** chat memory broke tool calling (based on GitHub issues and Spring AI docs)
2. You did benchmarking to find the cheapest LLM
3. **Surprise**: it actually works! The problem doesn't seem to exist in practice
4. Google Gemini 2.0 Flash is the winner

Let me rewrite this with the correct angle:

---
layout: post
title: "I Benchmarked 9 LLMs to Find the Cheapest for Multi-Turn Tool Calling with Spring AI"
date: 2025-10-08 08:00:00 -0000
categories: [ spring-ai, llm, java, spring-boot, testing, ai, benchmarking ]
---

# I Benchmarked 9 LLMs to Find the Cheapest for Multi-Turn Tool Calling with Spring AI

I'm building an AI mixing console assistant for live sound engineers using Spring Boot and Spring AI. I needed chat
memory (for conversation context) and tool calling (to actually control the mixer). Based on Spring AI's documentation
and GitHub issues, I expected these features to conflict. Turns out, they mostly work together—but which provider is
cheapest?

I spent days testing Groq, DeepSeek, Google Gemini, OpenAI, and Mistral to find out.

## Why I Expected Problems

Spring AI's docs warn: *"Currently, the intermediate messages exchanged with a large-language model when performing tool
calls are not stored in the memory."* [GitHub issue #2101](https://github.com/spring-projects/spring-ai/issues/2101) (
open since January 2025) documents how this breaks multi-turn conversations.

The theory: After the first tool call, the LLM sees past messages where it succeeded with just text responses. It infers
tools aren't needed and stops calling them.

I also assumed DeepSeek was the cheapest option based on old pricing I'd seen. Time to verify both assumptions.

## The Test

I built an automated benchmark simulating a mixing console assistant that must:

- Execute tool calls (rename channels, read parameters)
- Remember previous context (chat memory)
- Perform multi-turn tool calling across 4-6 prompts

**Simple scenario:** 4 prompts including memory-based commands  
**Complex scenario:** 6 prompts with reads, swaps, and bulk operations

Each test ran 5 iterations with 10-second delays to avoid rate limits. I measured success rate, accuracy, cost, and
speed.

## The Results

### 🏆 Winner: Google Gemini 2.0 Flash

**Best Overall Balance:**

- **Cost:** $0.000123-0.000133 per test run
- **Success Rate:** 100%
- **Accuracy:** 85-100%
- **Speed:** 10-23 seconds average

### Simple Scenario (4 prompts)

| Provider/Model                          | Avg Time | Success  | Accuracy | Avg Cost      |
|-----------------------------------------|----------|----------|----------|---------------|
| **google-native/gemini-2.0-flash-001**  | **10s**  | **100%** | **100%** | **$0.000133** |
| google-native/gemini-2.0-flash-lite-001 | 8s       | 100%     | 100%     | $0.000098     |
| openai-native/gpt-4o-mini               | 14s      | 100%     | 100%     | $0.000165     |
| openai-native/gpt-4.1-nano              | 19s      | 100%     | 100%     | $0.000116     |
| deepseek-native/deepseek-chat           | 34s      | 100%     | 100%     | $0.000675     |
| groq/llama-3.1-8b-instant               | 73s      | 100%     | 100%     | $0.001085     |
| groq/llama-3.3-70b-versatile            | 6s       | **80%**  | 100%     | $0.001552     |

### Complex Scenario (6 prompts)

| Provider/Model                          | Avg Time | Success  | Accuracy | Avg Cost      |
|-----------------------------------------|----------|----------|----------|---------------|
| **google-native/gemini-2.0-flash-001**  | **23s**  | **100%** | **85%**  | **$0.000123** |
| google-native/gemini-2.0-flash-lite-001 | 17s      | 100%     | 60%      | $0.000049     |
| openai-native/gpt-4o-mini               | 53s      | 100%     | 64%      | $0.000245     |
| openai-native/gpt-4.1-nano              | 44s      | 100%     | 64%      | $0.000163     |
| groq/llama-3.1-8b-instant               | 26s      | 100%     | 65%      | $0.000089     |
| deepseek-native/deepseek-chat           | 76s      | 100%     | 46%      | $0.000777     |
| groq/llama-3.3-70b-versatile            | 13s      | **40%**  | 64%      | $0.001417     |

**Key Finding:** Groq looks cheap on paper but has reliability issues (timeouts, tool validation errors) that disqualify
it for production.

## The Surprises

**1. Multi-turn tool calling actually works**  
Despite the documented limitations, tool calling worked with chat memory across most providers. When you log the
requests, tool calls still aren't persisted in memory—but somehow the conversations flow correctly. I don't fully
understand why, but I'll take it.

**2. DeepSeek isn't cheapest anymore**  
Their promotional pricing expired. They're now mid-tier in both cost and accuracy.

**3. Groq failed at scale**  
Single iterations looked great, but multiple iterations exposed timeouts and `tool_use_failed` errors. For one-off
tasks, maybe fine. For production? No.

**4. Google had empty message bugs**  
Gemini started returning empty messages causing "must include at least one parts field" errors. I wrote a custom
`EmptyMessageFilterAdvisor` to filter them
out. [Reported as Spring AI issue #4556](https://github.com/spring-projects/spring-ai/issues/4556).

**5. Mistral never worked**  
Kept hitting "system message in wrong place" bugs. Spring AI already has issues open for this, so I gave up.

## Technical Implementation

**Test Stack:**

- Spring AI with native integrations (DeepSeek, Google, OpenAI)
- OpenAI Proxy pattern for Groq (uses OpenAI client with custom base URL)
- `MessageWindowChatMemory` for chat history
- `SimpleLoggerAdvisor` for debugging (pro tip: use `logback-test.xml` in your test folder, not
  `application.properties`)
- Custom validation scoring based on API call accuracy
- 180-second timeout per test iteration

**Scoring Algorithm:**

```java
private double calculateOverallScore(TestResults tr) {
    double reliabilityScore = tr.getSuccessRate() * 50;        // 50 points
    double accuracyScore = tr.getAverageAccuracy() * 30;       // 30 points  
    double speedScore = Math.min(15.0, 15000.0 / tr.getAverageTime()); // 15 points
    double costScore = Math.min(5.0, 0.05 / tr.getAverageCost());      // 5 points
    return reliabilityScore + accuracyScore + speedScore + costScore;
}
```

## Recommendations

**For production Spring AI apps with tool calling + chat memory:**

1. **Go with Google Gemini 2.0 Flash** unless you have specific needs
2. **OpenAI GPT-4o-mini** if you need maximum accuracy (100% on simple tasks)
3. **Avoid Groq** for now—too unreliable for production despite low pricing
4. **Don't trust promotional pricing**—test with current rates
5. **Run multi-iteration tests**—single-shot benchmarks miss reliability issues

**If you're on a tight budget:**

- Gemini 2.0 Flash Lite is half the cost but accuracy drops to 60-80%
- Consider whether accuracy matters for your use case

## The Bottom Line

Building with LLMs is messier than demos suggest. You'll write custom advisors, work around API quirks, and deal with
non-deterministic behavior. But if you choose the right provider and test thoroughly, it's absolutely workable.

The "chat memory breaks tool calling" problem? Less severe than documented for most use cases. Google Gemini 2.0 Flash
handles it well at ~$0.0001 per multi-turn conversation.

## Resources

- [Test Code on GitHub](https://github.com/LiveNathan/cheapest-llm-tool-calling)
- [Console Whisperer Demo](https://youtu.be/Kpb2Zm6Bd8A)
- [Vaadin Forum Discussion](https://vaadin.com/forum/t/workaround-for-issues-with-chat-memory-and-llm-tool-calling/178500)
- [Spring AI Issue #2101](https://github.com/spring-projects/spring-ai/issues/2101) - Tool calls not persisted in memory
- [Spring AI Issue #4556](https://github.com/spring-projects/spring-ai/issues/4556) - Empty message bug I discovered

---

**Want to see this in action?** Check out [Console Whisperer](https://youtu.be/Kpb2Zm6Bd8A), my AI mixing console
assistant that uses these findings.