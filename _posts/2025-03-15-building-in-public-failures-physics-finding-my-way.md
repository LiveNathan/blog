---
layout: post
title: "Leaving Directories–Back to Audio Physics"
date: 2025-03-15 09:00:00 -0000
categories: [ micro-saas, entrepreneurship, building-in-public, validation, audio ]
---

I'm back with more updates: some wins, some losses, lots of learning.

## Contents

- [AV Technician Hire: The Wind-Down](#av-technician-hire-the-wind-down)
- [SubAligner: From MATLAB to Java](#subaligner-from-matlab-to-java)
- [GainGuardian/DiSP: Exploring Car Audio](#gainguardian-exploring-car-audio)
- [The Tax Adulting Update](#the-tax-adulting-update)

## AV Technician Hire: The Wind-Down

What I should celebrate here is that I put minimal effort into testing this business idea—maybe 6 hours of keyword
research, 16-hour building assets (website, mailing list, etc.), and another 16 hours on updates. The validation
happened quickly, which is exactly what I was aiming for in my [January business plan]({% post_url
2025-01-31-new-personal-blog-and-business-plan %}).

Here's what I told my mailing list this week:

> Hi everyone,
>
> I wanted to reach out with an update on AV Technician Hire. After careful consideration, I've made the difficult
> decision to wind down this project.
>
> ### Why I'm Making This Decision
>
> When I launched this site four months ago, it was an experiment with two clear goals:
> 1. Create something that genuinely helps people in the AV industry
> 2. Build a viable business model that could sustain itself
>
> After reviewing the data and feedback, I've realized that despite my best efforts, the project isn't achieving either
> goal effectively. Page views have declined month over month, and while around 20 people filled out the survey form,
> follow-up conversations didn't translate into meaningful connections or business opportunities.
>
> ### What I've Learned
>
> The AV industry remains heavily relationship-driven. Every time I shared this project online, I received numerous
> questions about how I was validating or authenticating the technicians on the site. These conversations highlighted a
> fundamental challenge: the industry runs almost exclusively on personal referrals, and that paradigm isn't changing
> anytime soon.
>
> When I reached out personally to those who expressed interest, only one person responded. When I proposed a service to
> help match them with qualified professionals, they expressed skepticism that such matching was even possible. This
> reinforced something I've learned in business - when people believe a problem has no solution, it's extremely
> difficult
> to sell them on one.
>
> To my knowledge, no one has secured work through the platform, and no meaningful connections have been made. After
> four months, these results suggest the current approach isn't working.

What I'm most afraid of is that people will be upset with me for asking them to get involved and support me, only for me
to give up. But I've learned that failing fast is better than dragging out something that's not working. The site will
be taken down on March 17th, and I'm moving on to focus my energy elsewhere.

## SubAligner: From MATLAB to Java

I've been continuing work on a new feature for SubAligner that allows users to upload their own measurements. It's
essentially a tiny portion of the full application pulled out so users can use it independently, rather than just having
it generate pre-alignment delay values stored in a database.

On the development side, it's been fun translating my code from MATLAB to Java. There aren't libraries for the kind of
element-wise operations that are so easy in MATLAB, where you can just do math from one array to another without nested
loops. It's tedious but fascinating to consider exactly what's happening in each operation. I'm immensely grateful for
AI coding support and test-driven development here—they've been essential for checking my math and algorithms.

The feature now lets you upload transfer function measurements from your audio analyzer and organize them into location
pairs. It then batch-processes all files to find the best delay and polarity solution for:

1. Each individual location pair
2. A global compromise solution that works best across all locations

| ![Image 1 Alt Text](path/to/image1.jpg) | ![Image 2 Alt Text](path/to/image2.jpg) |
|-----------------------------------------|-----------------------------------------|
| Caption for Image 1                     | Caption for Image 2                     |

The single location alignments are working great, but the compromise solution is hit-or-miss. I thought I could apply
the same scoring mechanism I'm using on the single locations to also find the best compromise, but sometimes the result
is way off. I'm considering whether it might be easier to just generate an average between all measurements and find
alignment for that average, but I find the current approach more novel and interesting since it tries to find the
compromise between every measurement location.

My first beta tester complained it would take too long to use in the field, but if you number files sequentially before
uploading, the location pairs are generated automatically. Plus, any tool gets faster after you've used it for a while.

This project ties into a larger question I've been exploring for years: what's the minimum number of steps needed to
successfully calibrate an entire sound system? This is a crucial question in live event production, where time is always
scarce, and there are countless fires to put out. One of the most common questions I've gotten over the last decade is "
What would you do if you only had X minutes?" People are constantly looking for shortcuts and more efficient
workflows—and so am I.

Here's the workflow I'm proposing with this new feature:

1. Take at least 8 measurements of your main and subwoofer system
2. Load them into this tool to find alignment solutions
3. Generate averages based on that alignment
4. Perform EQ against the combined system

From a business perspective, I'm not sure this will significantly impact SubAligner itself. My first beta tester already
has a subscription, so for them, it's just a nice added benefit. The second tester said they're already happy with their
current alignment method. What I've found is that if people have dedicated years to learning a tool and workflow,
they're often not just uninterested in new approaches—they can feel threatened by them.

## GainGuardian: Exploring Car Audio

You may remember an anti-feedback VST plugin that I was selling last year called GainGuardian. It was based
on [Diffuse Signal Processing (DiSP)](https://adamjhill.com/2020/05/27/demo-diffuse-signal-processing-disp/) research by
Adam Hill. I'm rededicating myself to this project with two big changes:

1. Focus on applying DiSP to more general problems that affect every sound system like comb filtering, room modes, and
   crossover alignment.
2. Partner with Adam to make sure I'm getting the implement right and bring more support and legitamicy to the project.

The two biggest questions we need to answer are: what industry do we start with, and what do we sell to them?

Car audio (a.k.a. mobile audio or car hi-fi) is at the top of our list because:

1. It exhibits all the symptoms our technology treats
2. It has less intense requirements on latency than other applications
3. There's a passionate community of enthusiasts

I've started reaching out to students and colleagues who work professionally on car audio systems to validate that they'
re aware of problems like comb filtering and room modes. I also made
a [Reddit post](https://www.reddit.com/r/CarAV/comments/1j5s8of/whats_your_biggest_sound_quality_frustration/) to
understand how people talk about these issues and gauge their technical understanding.

The post got significant engagement:

- 10,000 views
- 81 comments
- Multiple users sharing RTA measurements and discussing complex concepts

The responses strongly support our hypothesis that car audio presents an excellent market opportunity. Many commenters
described issues that could potentially be addressed by signal decorrelation:

> "This is an RTA graph of pink noise on the previous iteration of my car's stereo before EQ. See the dips at ~140hz,
> 400hz, and 1900hz? Those are frequency cancellations due to the layout of my car's interior with the factory speaker
> locations. No amount of EQ boosting will fix them." - **bigpoppa822**

One user even conceptualized a solution similar to DiSP:

> "The only magic I could think of in a vehicle would be to somehow reproduce extra audio during playback that would
> cancel out unwanted reflections." - **ifixtheinternet**

The next step is figuring out how to get some demo tracks to these enthusiasts so they can hear the results themselves.
Rather than investing months in building hardware, I can pre-process audio tracks and send them for testing, since the
car audio environment is primarily about playback. My rough plan is to:

1. Put up a site where people can get information and download demo tracks
2. Later implement a web app where they can upload their own tracks for processing
3. Eventually develop hardware they can buy and implement in their systems

I'm not smart enough to predict exactly which industry will embrace this technology, so my approach is to make a
prioritized list and test as quickly as possible. Getting the technology into people's hands fast and seeing their
reactions is crucial.

If you're a car audio enthusiast or work in mobile audio and would like to test a demo, please reach out!

## What's Next?

I'm still figuring that out. After my big directory website plans collapsed (see [my previous post]({% post_url
2025-02-28-big-plans-fail-fast-looking-for-a-new-direction %})), I've been trying different approaches:

1. I'm continuing to improve SubAligner with user-driven features
2. Exploring the potential of DiSP technology in car audio
3. Asking for ideas and validating them quickly

I'd love to hear from you. What would you do if you were in my shoes?