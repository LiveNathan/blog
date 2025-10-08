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

OK, I spent some money and time running 5x iterations of LlmToolCallingBenchmarkTest so that you don't have to. Here's
the results:
Need to format this into a nice markdown table.

========================================
2025-10-07T09:42:33.147-05:00 INFO --- [           main] d.n.c.BenchmarkRunner                    : BENCHMARK REPORT:
Simple Channel Renaming with Memory
2025-10-07T09:42:33.147-05:00 INFO --- [           main]
d.n.c.BenchmarkRunner                    : ========================================

2025-10-07T09:42:33.147-05:00 INFO --- [           main] d.n.c.BenchmarkRunner                    : Provider/Model Avg
Time Success Accuracy Avg Cost Tokens Calls
2025-10-07T09:42:33.147-05:00 INFO --- [           main]
d.n.c.BenchmarkRunner                    : ----------------------------------------------------------------------------------------------------
2025-10-07T09:42:33.152-05:00 INFO --- [           main] d.n.c.BenchmarkRunner                    :
groq/llama-3.1-8b-instant 72708ms 100% 100% $   0.001085      19681        132
2025-10-07T09:42:33.152-05:00  INFO --- [           main] d.n.c.BenchmarkRunner                    : groq/llama-3.3-70b-versatile             6058ms        80% 100% $
0.001552 2602 8
2025-10-07T09:42:33.152-05:00 INFO --- [           main] d.n.c.BenchmarkRunner                    :     Errors: Timeout
after 180 seconds
2025-10-07T09:42:33.152-05:00 INFO --- [           main] d.n.c.BenchmarkRunner                    :
deepseek/deepseek-chat 36320ms 100% 100% $   0.000739       2576          7
2025-10-07T09:42:33.153-05:00  INFO --- [           main] d.n.c.BenchmarkRunner                    : deepseek-native/deepseek-chat           33906ms       100% 100% $
0.000675 2354 7
2025-10-07T09:42:33.153-05:00 INFO --- [           main] d.n.c.BenchmarkRunner                    :
google-native/gemini-2.0-flash-001 9984ms 100% 100% $   0.000133       1199          7
2025-10-07T09:42:33.153-05:00  INFO --- [           main] d.n.c.BenchmarkRunner                    : google-native/gemini-2.0-flash-lite-001      8302ms       100% 100% $
0.000098 1178 6
2025-10-07T09:42:33.153-05:00 INFO --- [           main] d.n.c.BenchmarkRunner                    :
google-native/gemini-2.5-flash-lite 9744ms 100% 80% $   0.000186       1375         11
2025-10-07T09:42:33.153-05:00  INFO --- [           main] d.n.c.BenchmarkRunner                    : openai-native/gpt-4o-mini               13944ms       100% 100% $
0.000165 969 6
2025-10-07T09:42:33.153-05:00 INFO --- [           main] d.n.c.BenchmarkRunner                    :
openai-native/gpt-4.1-nano 18587ms 100% 100% $   0.000116 996 6
2025-10-07T09:42:33.154-05:00 INFO --- [           main] d.n.c.BenchmarkRunner                    :

========================================
2025-10-07T10:32:15.719-05:00 INFO --- [           main] d.n.c.BenchmarkRunner                    : BENCHMARK REPORT:
Complex Band Setup with Memory
2025-10-07T10:32:15.719-05:00 INFO --- [           main]
d.n.c.BenchmarkRunner                    : ========================================

2025-10-07T10:32:15.719-05:00 INFO --- [           main] d.n.c.BenchmarkRunner                    : Provider/Model Avg
Time Success Accuracy Avg Cost Tokens Calls
2025-10-07T10:32:15.719-05:00 INFO --- [           main]
d.n.c.BenchmarkRunner                    : ----------------------------------------------------------------------------------------------------
2025-10-07T10:32:15.720-05:00 INFO --- [           main] d.n.c.BenchmarkRunner                    :
groq/llama-3.1-8b-instant 26158ms 100% 65% $   0.000089       1744        150
2025-10-07T10:32:15.720-05:00  INFO --- [           main] d.n.c.BenchmarkRunner                    : groq/llama-3.3-70b-versatile            13200ms        40% 64% $
0.001417 2362 21
2025-10-07T10:32:15.720-05:00 INFO --- [           main] d.n.c.BenchmarkRunner                    :     Errors: Timeout
after 180 seconds, 400 - {"error":{"message":"tool call validation failed: attempted to call tool 'setParameter' which
was not in request.tools","type":"invalid_request_error","code":"tool_use_failed","failed_generation":"
\u003cfunction=setParameter\u003e{\"apiCall\": {\"path\": \"ch.5.cfg.name\", \"value\":
\"Guitar\"}}\u003c/function\u003e\n\u003cfunction=setParameter\u003e{\"apiCall\": {\"path\": \"ch.8.cfg.name\",
\"value\": \"Overheads L\"}}\u003c/function\u003e"}}

2025-10-07T10:32:15.720-05:00 INFO --- [           main] d.n.c.BenchmarkRunner                    :
deepseek/deepseek-chat 69991ms 100% 36% $   0.000720       2530         17
2025-10-07T10:32:15.720-05:00  INFO --- [           main] d.n.c.BenchmarkRunner                    : deepseek-native/deepseek-chat           76286ms       100% 46% $
0.000777 2713 19
2025-10-07T10:32:15.721-05:00 INFO --- [           main] d.n.c.BenchmarkRunner                    :
google-native/gemini-2.0-flash-001 22874ms 100% 85% $   0.000123       1124         22
2025-10-07T10:32:15.721-05:00  INFO --- [           main] d.n.c.BenchmarkRunner                    : google-native/gemini-2.0-flash-lite-001     16589ms       100% 60% $
0.000049 595 17
2025-10-07T10:32:15.721-05:00 INFO --- [           main] d.n.c.BenchmarkRunner                    :
google-native/gemini-2.5-flash-lite 36675ms 100% 64% $   0.000294       2061         55
2025-10-07T10:32:15.721-05:00  INFO --- [           main] d.n.c.BenchmarkRunner                    : openai-native/gpt-4o-mini               53113ms       100% 64% $
0.000245 1500 23
2025-10-07T10:32:15.721-05:00 INFO --- [           main] d.n.c.BenchmarkRunner                    :
openai-native/gpt-4.1-nano 43944ms 100% 64% $   0.000163 1495 23
2025-10-07T10:32:15.724-05:00 INFO --- [           main] d.n.c.LlmToolCallingBenchmarkTest        :
============================================================
2025-10-07T10:32:15.724-05:00 INFO --- [           main] d.n.c.LlmToolCallingBenchmarkTest        : OVERALL WINNER
ACROSS ALL SCENARIOS
2025-10-07T10:32:15.724-05:00 INFO --- [           main]
d.n.c.LlmToolCallingBenchmarkTest        : ============================================================
2025-10-07T10:32:15.731-05:00 INFO --- [           main] d.n.c.LlmToolCallingBenchmarkTest        :
google-native/gemini-2.0-flash-001: 167.79
2025-10-07T10:32:15.731-05:00 INFO --- [           main] d.n.c.LlmToolCallingBenchmarkTest        :
google-native/gemini-2.0-flash-lite-001: 160.71
2025-10-07T10:32:15.731-05:00 INFO --- [           main] d.n.c.LlmToolCallingBenchmarkTest        :
openai-native/gpt-4o-mini: 160.45
2025-10-07T10:32:15.731-05:00 INFO --- [           main] d.n.c.LlmToolCallingBenchmarkTest        :
groq/llama-3.1-8b-instant: 160.42
2025-10-07T10:32:15.732-05:00 INFO --- [           main] d.n.c.LlmToolCallingBenchmarkTest        :
openai-native/gpt-4.1-nano: 160.24
2025-10-07T10:32:15.732-05:00 INFO --- [           main] d.n.c.LlmToolCallingBenchmarkTest        :
google-native/gemini-2.5-flash-lite: 155.04
2025-10-07T10:32:15.732-05:00 INFO --- [           main] d.n.c.LlmToolCallingBenchmarkTest        :
deepseek-native/deepseek-chat: 154.55
2025-10-07T10:32:15.732-05:00 INFO --- [           main] d.n.c.LlmToolCallingBenchmarkTest        :
deepseek/deepseek-chat: 151.54
2025-10-07T10:32:15.732-05:00 INFO --- [           main] d.n.c.LlmToolCallingBenchmarkTest        :
groq/llama-3.3-70b-versatile: 122.70
2025-10-07T10:32:15.733-05:00 INFO --- [           main] d.n.c.LlmToolCallingBenchmarkTest        :
🏆🏆🏆 OVERALL CHEAPEST RELIABLE LLM: google-native/gemini-2.0-flash-001 🏆🏆🏆

Hmm, I wonder if I should talk about what the test does? Maybe just share that each request is either a command that
should call a tool and some of the requests require that LLM use the chat memory to complete its task.

I should probably just share a note about caching. Several of the LLMs tested include special pricing related to
caching. I'm not going to say much about it here because, based on my current understanding, it does not affect this
test because each new request is new. Well, maybe that's not true because actually, when you inspect each request, most
of it is repeated because the system message statys the same along with all of the tool calling information, but I
probably still won't talk about it much because as far as I can tell spring ai only supports caching for Anthropic
models at this time.

Ultimately this would have been a better story if I could have proven that tool calling never works when using the chat
memory, but actually I'm happy that it's not true because I can move forward with my real work on Consoel Whisperer. I
thought I was clear on the problem. Even Spring Ai docs warn about it, "Currently, the intermediate messages exchanged
with a large-language model when performing tool calls are not stored in the memory. This is a limitation of the current
implementation and will be addressed in future releases. If you need to store these messages, refer to the instructions
for the User Controlled Tool Execution." So I figured I would have to make my own custom workaround or wait for them to
fix it, so I'm surprised and happy that it works, but I'm also a bit confused in the end.

The Vaadin forum post: https://vaadin.com/forum/t/workaround-for-issues-with-chat-memory-and-llm-tool-calling/178500

github repo for this test code: https://github.com/LiveNathan/cheapest-llm-tool-calling

Console Whisperer demo: https://youtu.be/Kpb2Zm6Bd8A

This stuff now is left over from the outline I started with. I don't know if it's useful, but I'll leave it here for now
in case any pieces might be useful.

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

