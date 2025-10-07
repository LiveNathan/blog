Well, I thought this was going to be a blog post about research I did to find the cheapest LLM api supported by spring
ai that supports tool calling and chat memory, and it is, but I guess the story starts on shaky ground. I started
building an AI mixing console assistant for other live sound engineers like myself. At some point along the way I
discovered while running the app that in a conversation with the assistant that it would only reliably perform tool
calling once. Any further calls in the conversation would not trigger the tool. The frustrating part is that the
assistant would still respond to the user with a success message, claiming that it had performed the action. I started
to suspect that the issue might be connected to chat memory.

The biggest issue with Spring AI right now that it seems like no one is talking about is that chat memory interferrs
with tool calling. It seems like this would be ruining everyone's projects right now. Maye there's something I'm
missing, but to me these are the two most important features needed for building with LLMs and they don't work. AI seems
to always over promise and under deliver.

I built an automated test to prove this. All it did was make multiple calls to the LLM that should require tool calling.
With chat memory enabled, the tool calls would only be made on the first call. Removing chat memory fixed the issue. I
checked the Spring AI github repo and found this github issue
title [Model Tool Calls not persisted in chat memory](https://github.com/spring-projects/spring-ai/issues/2101). Now it
makes more sense. On the first call to the LLM, the LLM sees that it has tools it can use and no chat history. On
subsequent calls, the LLM sees that in past messages in the chat memory that the user made a request and all the LLM had
to do was to respond with a success message, so it infers that tools are not required to satisfy the rquest. Or at least
that's my theory. By the way have you looked at the number of issues on the Spring AI github repo? 725 open issues!
popurlar tech i guess.

I had to remove chat memory from my project becuase the tool calling is more important, but of course it makes for a
shitty user experience, especially when the app did have chat memory and now I have taken it away. The next feature I
need to work on involves more testing against tool calls so I decided to do this research project to get to the bottom
of it. What is the cheapest solution for my use case? I also got motivated because I was working on the assumption that
deepseek was the cheapest solution. I was wrong. Turns out that deepseek had very low promotional pricing for a while,
but was no longer the cheapest. So I decided to test deepseek, open ai, Mistral, and google genai and groq to see which
one was the cheapest.

The tl;dr is that google won with its flash 2.0 model. I assumed groq would win since I think it's technically cheaper,
and it w9ould have won i think if I had only done a single iteration of the test, but once I started doing multiple
iterations, groq started returning some strange errors. The other surprise was that I didn't have to do anythning to get
multi-turn tool calling to work with chat memory. I don't know why. At first I thought maybe this was fixed in the newer
versions of spring ai, but when you log the requests and responses to the LLM you can see that the tool calls are still
not being persisted. This is where I should go back to my original tests against chat memory but at this point I have
already put multiple days into these tests and I'm just happy to have a working solution to move forward with.

If I'm honest, it's been a pain to work with these LLMs. Making it such a core part of the applications just makes it
feel so flaky. There are days when I start up the app and it just doesn't behave as expected. I waste some time trying
to debug the problem, change nonthing, then the next day I start it up and it works. Maybe these are just the growing
pains of learning to develop against an LLM, but one of my big takeaways is that when someone makes something look so
easy in a demo in a video on YT. It's not. Real production uses cases are never that easy. Maybe a good example is the
SimpleLoggerAdvisor. It's super easy. You just add it to your prompt builder, set
`logging.level.org.springframework.ai.chat.client.advisor=DEBUG` in your application.properties, and you're done. Makes
sense at first, until you realize that in most cases where you might want to log and debug requests nd responses to the
LLM, you actually want to do that during a test, not while running the app, so you try to create an
application.properties file in the test folder, but it doesn't work. Finally you get it to work by creating a
logback-test.xml file instead. Maybe that's not the most compelling use case, but it's just a lot of little things like
that that I can into while trying to build this test.

One final big challenge was that calls to the google genai LLM started to fail and in the same way every time. The
simple test case that only included three messages would always pass, but the complex test case with six messages would
fail. The error was, "Unable to submit request because it must include at least one parts field, which describes the
prompt input." This was initially confusing, but once I got the response logging working I could see that the LLM was
return multiple messages and one of them was empty, like this `textContent=,`. I was pretty sure this was a Spring AI
bug so I [created an issue](https://github.com/spring-projects/spring-ai/issues/4556) (number 726) but i don't want to
wait for the Spring team to fix it. Who knows how long that will take. Luckily there is a way to create your own custom
advisors, so I asked Claude to write me a EmptyMessageFilterAdvisor and that did the trick.

The only LLM that I set out to test and was not able to test was Mistral. I kept getting the same bug about the system
message being in the wrong place. I can see that there's already an issue in spring ai github so I decided to give up on
it for now. I left it in the test, just commented out, so if you want to try it yourself you can.

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
