# When AI Agents Forget Their Tools: The Hidden Problem with LLM Chat Memory and Tool Calling

You're building an AI assistant. First request works perfectly—the LLM calls your tools, performs actions, everything is
great. Second request? The LLM just pretends it did the work and lies about it. No tool execution happens. Your users
are confused. You're confused. Welcome to the tool calling + chat memory problem that's breaking production AI
applications.

## The Problem: When Memory Becomes Amnesia

The issue is deceptively simple: when you combine chat memory with tool calling in frameworks like Spring AI and
LangChain4j, tool calls aren't persisted to the conversation history. Here's what happens in practice:

**First interaction:**

- User: "Change channel 1 name to ProjectX"
- LLM correctly identifies it needs to call the `changeChannelName` tool
- Tool executes successfully
- LLM responds: "Done! Changed channel 1 to ProjectX"
- **Chat memory stores:** User message + Final AI response only (no tool call)

**Second interaction:**

- User: "Now change channel 2 name to ProjectY"
- LLM sees previous conversation: user asked for change, LLM responded "done"
- LLM thinks: "Last time I just responded with text confirmation. I'll do the same."
- LLM responds: "Done! Changed channel 2 to ProjectY"
- **Nothing actually happens** - no tool is called

The LLM is learning the wrong pattern from incomplete conversation history.

## Why This Matters

This isn't an edge case—it's fundamental to building conversational AI with actions. Without proper tool call
persistence:

- Tools only work once per conversation
- LLMs "hallucinate" having performed actions they never executed
- Users lose trust when the AI lies about what it did
- You're forced to choose: chat memory (better UX) OR tool calling (actual functionality)
- This blocks production deployments of agentic systems

## Investigating the Issue: Is This Real or Am I Doing Something Wrong?

When I first encountered this, I thought I must be missing something obvious. Surely Spring AI, a framework designed for
production AI applications, wouldn't have this fundamental limitation? But digging into the evidence reveals this is
very real.

### The Evidence

**Spring AI GitHub Issue #2101** (opened January 2025, still open): "Model Tool Calls not persisted in chat memory."
Multiple developers confirm the issue. ThomasVitale (Spring AI contributor) acknowledges: "The memory implementation in
ChatClient doesn't currently support storing the intermediate tool messages, but work is in progress to add that
support."

**My Vaadin forum post**: Mixed responses. One developer successfully reproduced my issue. Another claims it works fine
with their setup. This suggests the problem may be model-specific or configuration-dependent.

**LangChain4j**: Similar issues exist. GitHub issue #3133 documents how bulk tool execution can corrupt memory, leading
to invalid conversation states.

### The DeepSeek Factor

Here's where it gets interesting: **The Spring AI documentation for DeepSeek makes zero mention of tool calling support.
** Every other model in Spring AI's docs (OpenAI, Anthropic, etc.) has a "Function Calling" section. DeepSeek's
documentation? Silent on this feature.

Yet DeepSeek's own API documentation clearly states they support function calling compatible with OpenAI's API. So
what's going on?

Hypothesis: Spring AI's DeepSeek integration may not fully support tool calling, or it's deliberately omitted due to
known issues. This could explain why I'm seeing this problem specifically with DeepSeek.

## The Experiment: Testing Across Models

To definitively answer whether this is a framework bug, a model limitation, or a DeepSeek-specific issue, I created a
systematic test across multiple LLMs.

### Test Setup

[Link to GitHub repository with test code]

The test is simple:

1. Create a Spring AI ChatClient with chat memory enabled
2. Register a simple tool (e.g., `changeChannelName(channelId, newName)`)
3. Make multiple sequential requests that should trigger tool calls
4. Verify: Does the LLM call the tool on subsequent requests?

### Models Tested

- **DeepSeek** (deepseek-chat via Spring AI)
- **OpenAI GPT-4o** (via Spring AI)
- **Anthropic Claude** (via Spring AI)
- **Testing with LangChain4j** as comparison

### Results

[You'll fill this in after running your tests]

| Model                  | First Call Works? | Subsequent Calls Work? | Notes                               |
|------------------------|-------------------|------------------------|-------------------------------------|
| DeepSeek               | ✓                 | ✗                      | Tool calls stop after first request |
| GPT-4o                 | ?                 | ?                      | [To be tested]                      |
| Claude                 | ?                 | ?                      | [To be tested]                      |
| LangChain4j + DeepSeek | ?                 | ?                      | [To be tested]                      |

## Available Workarounds

While the Spring AI team works on a proper fix, here are the workarounds developers are currently using:

### 1. Manual Tool Execution (User-Controlled)

Instead of letting Spring AI handle tool execution recursively, you manually control when and how tools are called. This
gives you access to the full conversation history including tool calls.

**Pros:** Full control, guaranteed to work  
**Cons:** Verbose, you lose framework conveniences

### 2. Custom Chat Memory Advisor

Several developers in the GitHub thread implemented custom memory advisors that manually inject tool call messages into
history.

**Pros:** Keeps automatic tool execution  
**Cons:** Hacky, may break with framework updates

### 3. Extract Tool History from ToolContext

The ToolContext provides access to the conversation history up to the tool call. You can manually persist this.

**Pros:** Officially supported by Spring AI  
**Cons:** Requires code in every tool implementation

### 4. Disable Chat Memory (Current "Solution")

Just turn off chat memory entirely.

**Pros:** Tools work reliably  
**Cons:** Terrible user experience, defeats the purpose of conversational AI

## The Architectural Decision: What Should I Do?

Given these findings, here's my decision matrix for Console Whisper:

### If DeepSeek tool calling is unsupported in Spring AI:

→ **Switch to OpenAI or Claude** (depending on test results). The cost increase is worth having a functional
application.

### If this is a Spring AI framework issue affecting all models:

→ **Consider switching to LangChain4j** and reassess.

### If this is solvable with workarounds:

→ **Implement custom memory advisor** for now, plan to migrate to official solution when available.

## Recommendations for the Community

If you're hitting this issue:

1. **Test your specific model** - Don't assume all models behave the same
2. **Check the Spring AI GitHub issues** - Subscribe to #2101 for updates
3. **Consider your priorities** - If you need both memory and tools, prepare for workarounds
4. **Contribute test cases** - Help the maintainers understand the scope

For Spring AI maintainers: This needs to be a documented limitation until fixed. Developers are making architectural
decisions based on incomplete information.

## Conclusion

The tool calling + chat memory problem is real, under-discussed, and blocking production deployments. Through systematic
testing, we can identify which models and frameworks handle this correctly and make informed decisions.

**My next steps:**

1. Complete cross-model testing
2. Implement the best available workaround
3. Update this post with definitive results

**What about you?** If you're experiencing this issue (or you're not experiencing it and can't figure out why I am),
drop a comment below. Let's solve this together.

---

**Update this post with your findings after running the tests!**

---

## Additional Resources

- [Spring AI Issue #2101](https://github.com/spring-projects/spring-ai/issues/2101)
- [My test repository](link)
- [Vaadin Forum Discussion](https://vaadin.com/forum/t/workaround-for-issues-with-chat-memory-and-llm-tool-calling/178500)
- [LangChain4j Memory Documentation](https://docs.langchain4j.dev/tutorials/chat-memory/)
