---
layout: post
title: "Project Update: Convolution, Complexity, and a Part-Time Job"
date: 2025-10-14 08:00:00 -0000
categories: [ gain-guardian, console-whisperer, audio, dsp, llm, ai, spring-ai, vaadin, career ]
---

# Project Update: Convolution, Complexity, and a Part-Time Job

GainGuardian is stuck on a technical challenge, Console Whisperer is slowed by complexity, and I'm now working part-time
on a day job. But there's actually some interesting stuff happening, so let's dig in.

## Gain Guardian: Convolution is hard

Gain Guardian has consumed most of my time this year, and it feels like we're still stuck in the mud from a technical
perspective. The core issue? We can't do successful demos.

All the research in to dynamic diffuse signal processing has focused on the algorithm that creates the kernels. None of
it has gone into the application of those kernels through convolution because it's assumed to be the easy part. Either
it's not so easy or I'm doing it wrong, but either way it's the thing we're stuck on.

I still think Gain Guardian is important. I think it could genuinely help people and make things sound better. But the
road ahead is completely unclear. Another year? Ten years? Until I get some new inspiration or find someone who
specializes in convolution and knows the solution, it's going to sit on the shelf for a while.

## Console Whisperer: Easier to market, harder to build

Console Whisperer has been interesting because it's one of the easiest things I've ever marketed. Every sound engineer
uses mixing consoles, everyone's curious about AI right now, and I can literally just ask people, "Do you use Mixing
Station?" If they say yes, I've got an audience. I have about 10 people signed up as early adopters.

But here's where "easier" is relative.

Development has slowed because I had to reconfigure everything into a client-server architecture, and now everything
feels twice as hard. Every change requires considering multiple things:

- The non-deterministic nature of LLMs (still frustrating to work with)
- Cross-platform desktop app development (my first time)
- Using Vaadin (a web app technology) to build a desktop app
- The fact that all this LLM tooling is still nascent

Nascent. That's the word. Everything feels early. Tool calling works a little. Chat memory works a little. Combine them?
Things break. Not always, but enough that you're constantly fighting with the LLM saying "hey, you didn't do what I told
you to do."

```markdown
You: ch 2 name to cow

Server: OK. I've changed Channel 2's name to cow.

You: no you didn't

Server: My apologies, it seems I had a mix-up. I have now changed Channel 2's name to cow.

You: nope. it still says Ch 02

Server: My apologies. It appears the name was not set correctly. I will set Channel 2's name to cow now. OK. I've
changed Channel 2's name to cow.
```

If you look at the Spring AI GitHub repo right now, there are 176 open issues. That tells you something.

I've published updates that worked on my machine but then broke on Windows. Or Mac. So now I'm doing all this manual
testing, trying to understand platform-specific quirks while simultaneously wrestling with LLM reliability. It feels
like pushing a square peg through a round hole.

The plan was to test each early adopter's use case individually before following up. I screwed that up a bit by not
taking good notes on the best way to reach people. Turns out email is surprisingly unreliable in 2024. My own brother
doesn't see my emails unless I text him about them.

I'm now wondering if I should skip the one-by-one approach and just make it publicly available, reach out to everyone at
once, before this momentum dies. It's been over a month since I talked to the first person. They've probably forgotten
by now.

The good news? You can do almost anything with Console Whisperer that you can do with Mixing Station. Tell it to "name
channels 1-128 as RF 1-128" and it'll do it faster than you could manually. It's getting close to being a real
assistant.

Still figuring out pricing. I was thinking QLab-style lifetime pricing, but my friend Pavel warned me against it. Maybe
annual pricing with a first-year discount makes more business sense. Another open question.

## Joining SquareWave

The big news is that I've started working part-time (20 hours/week) at SquareWave, an Australian company that supports
production AV companies using Flex Rental Solutions.

Last week was my first week of training. I'm joining their team that creates custom reports, which means improving my
SQL knowledge and learning JasperSoft Studio (a tool that outputs JRXML files for custom reports).

I've already had some product ideas:

**The Gather automation problem**: SquareWave uses Gather for internal meetings. It's fun but buggy. You can record
meetings and get transcriptions with speaker names, which is great. But you can't download the transcription. It doesn't
have an API yet. And it silently stops recording after 3 hours without warning.

I'd love to create an automation that grabs the recording and transcription after every meeting and stores them in
SquareWave's knowledge base (Slite). This would be super helpful during onboarding when people are throwing new
information at me constantly. I've made a script that cleans up the transcription, but I need Gather to expose their API
to make the full automation work.

**The JasperSoft question**: On a personal note, I'm curious if I can generate these JRXML files using Java with a TDD
approach, completely bypassing JasperSoft Studio. Not that there's anything wrong with the tool, but I'm just not very
interested in frontend design and I'd prefer to do everything with Java and TDD if I can. That's why I like Vaadin—you
do everything in Java, never touch JavaScript, and the design looks good out of the box. I found a framework called
Dynamic Reports that might let me do the same for Jasper Reports.

## What's Next?

If I'm spending 20 hours/week at SquareWave, I have about 20 hours left for my own projects. So the question becomes:
How much time on Console Whisperer? How much on Gain Guardian? Should I set aside time for new projects?

Seems like a good moment to reassess everything.

I don't have clean answers yet, but I know this: six months ago I thought I'd have a hardware prototype for GainGuardian
by now. Today I'm learning SQL and trying to automate meeting transcriptions. The journey isn't what I expected, but at
least I'm still building things and having a good time.

More updates to come as I figure out what the hell I'm doing.