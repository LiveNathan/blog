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
- [GainGuardian/DiSP: Exploring Car Audio](#gainguardiandisp-exploring-car-audio)
- [What's Next?](#whats-next)

## Back to My Audio Roots

After spending months exploring directory websites and various SaaS ideas (as detailed in
my [January business plan](https://nathanlively.substack.com/p/building-a-profitable-micro-saas)
and [February update](https://nathanlively.substack.com/p/big-plans-fail-fast)), I've come full circle back to audio
physics—the field where my expertise and passion truly align. This shift wasn't planned, but as you'll see below, it's
where I'm finding the most traction and excitement.

## AV Technician Hire: The Wind-Down

What I should celebrate here is that I put minimal effort into testing this business idea—maybe 6 hours of keyword
research, 16-hour building assets (website, mailing list, etc.), and another 16 hours on updates. The validation
happened quickly, which is exactly what I was aiming for in my January business plan.

Here's the key message I shared with my mailing list this week:

> After four months of running AV Technician Hire, I've made the difficult decision to wind down the project. Despite
> attracting some initial interest (about 20 survey responses), the data shows declining page views each month and no
> evidence that anyone secured work through the platform.
>
> The key insight: The AV industry remains heavily relationship-driven. Every conversation highlighted that the industry
> runs almost exclusively on personal referrals, and that paradigm isn't changing anytime soon. When I proposed a service
> to help match people with qualified professionals, the skepticism was clear—many didn't believe such matching was even
> possible.

What I'm most afraid of is that people will be upset with me for asking them to get involved and support me, only for me
to give up. But I've learned that failing fast is better than dragging out something that's not working. The site will
be taken down on March 17th, and I'm moving on to focus my energy elsewhere.

## SubAligner: From MATLAB to Java

Moving away from directories, I've returned to enhancing SubAligner with a new feature that allows users to upload their
own measurements instead of relying on pre-stored values in a database.

The development process has been particularly interesting—translating audio physics algorithms from MATLAB to Java
requires a different approach to mathematical operations. Where MATLAB excels at element-wise operations between arrays,
Java requires more explicit coding. Thankfully, test-driven development and AI assistance have been invaluable in
verifying my mathematical translations.

The new feature now lets users upload transfer function measurements from audio analyzers and:

1. Organize measurements into location pairs
2. Process files to find optimal delay and polarity solutions for each pair
3. Generate a global compromise solution that works best across all locations

| ![first feature demo](/assets/images/2025/03/leaving-directories/2025-03-04%20at%2012.10.32.png) | ![feature demo update](/assets/images/2025/03/leaving-directories/2025-03-10%20at%2014.57.02@2x.png) |

While single location alignments are working well, I'm still refining the compromise solution algorithm. The current
approach tries to find the optimal balance between all measurement locations rather than simply averaging them—more
novel but challenging to perfect.

This work connects to a fundamental question in live sound: what's the minimum number of steps needed to successfully
calibrate an entire sound system? With constant time pressure at live events, efficient workflows are essential.

## GainGuardian/DiSP: Exploring Car Audio

You may remember GainGuardian, my anti-feedback VST plugin based on Adam
Hill's [Diffuse Signal Processing (DiSP)](https://adamjhill.com/2020/05/27/demo-diffuse-signal-processing-disp/)
research. I'm revitalizing this project with two significant changes:

1. Expanding beyond feedback to address universal sound system issues like comb filtering, room modes, and crossover
   alignment
2. Partnering with Adam to ensure proper implementation and add legitimacy to the project

Our immediate questions: which industry do we target first, and what specific product do we offer?

Car audio has emerged as our leading candidate because:

1. It exhibits all the acoustic problems our technology addresses
2. It has less stringent latency requirements than live sound applications
3. There's an enthusiastic community of technical users

To validate this direction, I created
a [Reddit post](https://www.reddit.com/r/CarAV/comments/1j5s8of/whats_your_biggest_sound_quality_frustration/) asking
about sound quality frustrations. The response was encouraging:

- 10,000 views
- 81 comments
- Many users sharing technical measurements and discussing complex acoustical concepts

Several commenters specifically described issues that signal decorrelation could potentially solve:

> "This is an RTA graph of pink noise on the previous iteration of my car's stereo before EQ. See the dips at ~140hz,
> 400hz, and 1900hz? Those are frequency cancellations due to the layout of my car's interior with the factory speaker
> locations. No amount of EQ boosting will fix them." - **bigpoppa822**

My immediate next step is to create pre-processed demo tracks for enthusiasts to test in their systems, rather than
jumping straight to hardware development. This approach allows for rapid validation before significant investment:

1. Create an information site with downloadable demo tracks
2. Develop a web app for custom track processing
3. Eventually move to hardware solutions if demand proves strong

If you're involved with car audio and interested in testing these demos, please reach out!

## What's Next?

With my directory website plans shelved, I'm focusing my energy on three clear paths forward:

1. **SubAligner Enhancement**: Continuing development of user-requested features and refining the measurement upload
   capabilities
2. **DiSP Technology Applications**: Taking concrete steps to test signal decorrelation in car audio environments, with
   plans to expand to other verticals if successful
3. **Balanced Validation**: Maintaining my commitment to failing fast, but now with projects more aligned to my core
   expertise

In the next month, I plan to release the first public beta of the new SubAligner feature and have at least 5 car audio
enthusiasts testing DiSP-processed audio. I'll report back on what I learn from both initiatives.