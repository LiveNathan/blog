---
layout: post
title: "Console Whisperer: Seven Months, Three Rebuilds, and the Art of Shipping Something Small"
date: 2026-02-15 00:00:00 -0000
categories: [micro-saas, entrepreneurship, building-in-public]
---

Seven months ago, I thought I was a few weeks away from launching a product. Today I'm launching it -- and it does about
10% of what I originally planned. Here's what happened.

## The Idea That Seemed Easy

Last August, I was setting up a mixing console for the thousandth time. Naming channels, setting colors, routing
everything the same way I always do. I've never been a template person -- too many variations of brand and model, too
much maintenance to keep them useful. So I just do it by hand every time. A couple hours of work I've done a thousand
times before.

I thought: what if I could just tell an AI what I need and have it configure the console? "Five-piece band, three
vocals, four IEM mixes" -- done. I built a proof-of-concept over a weekend using Mixing Station's API and posted a
30-second demo on Reddit.

The response surprised me. 107 upvotes, 73 comments, 32k views. People were interested. David from Mixing Station gave
his blessing. I got emails from engineers who wanted to beta test. I set up a mailing list and started interviewing
potential users.

I was convinced this was going to be a real product.

## The Criticism That Made It Better

The Reddit comments weren't all positive. A lot of engineers were worried about safety -- what if the AI makes changes
you don't expect? What if it mutes channels during a show? What if it configures something wrong and you don't notice
until it's too late?

Fair points, all of them. My intended use case was always console setup, not live mixing, but the concern was
legitimate. It gave me an idea: instead of having the AI make changes directly to the console, I'd build a collaborative
spreadsheet interface. The engineer and the AI would work side by side -- you could see every change before it hit the
console. Upload a stage plot PDF, let the AI start filling in channel names, and edit alongside it in real time.

I built a demo of that and shared it in a follow-up video. It felt like a breakthrough.

## The Part Where It Got Hard

Then I actually had to build the thing.

If you follow my blog, you've seen me write about this in real time. I rebuilt Console Whisperer from scratch three
times. The first version was a web app -- which can't communicate with anything on your local network. Kind of a
dealbreaker when you need to talk to Mixing Station running on localhost. The second attempt was a client-server
architecture that technically worked but felt brittle. Third time I went desktop, which is where it should have been
from the start.

I benchmarked nine different LLMs to find one that was cheap and reliable enough for multi-turn tool calling. I learned
that there's a massive gap between the slick demos everyone posts online and building something that works consistently
in production. Those "look how easy this is!" videos skip over the weeks of troubleshooting to get an LLM to do what you
need, every time, without hallucinating tool calls or losing context.

I spent months just getting reliable communication between the app, the LLM, and Mixing Station's API. Each console
model has its own quirks. Stereo linking works differently on every platform. Bus configurations have different
constraints. What works on an X32 breaks on a Wing. What works on a Wing doesn't exist on a DLive.

## The Scope Problem

Around month four, I started to realize what I was actually building. My original plan was to interview early adopters,
implement their specific feature requests one by one, and sell to them directly. A reasonable plan -- except their
feature requests were huge. Stage plot import. Effects routing. Custom layer creation. EQ and dynamics presets. DCA
assignments. IEM bus configuration. Group-based routing architectures.

To do any of that well, Console Whisperer would need to read every parameter from the console, store it, generalize it
across models, and write it back. That's not a few months of work. That's years.

I thought I'd get there incrementally. Instead, it took seven months just to reliably set channel names and colors.

This is a pattern I've noticed in myself. I start projects thinking they'll be straightforward. I get excited, tell
people about them, build momentum -- and then I hit the wall where the actual complexity lives. The gap between "this
seems easy" and "this is actually hard" is where most of my projects have died.

## The Decision to Ship

By January, I was burned out. I hadn't touched the project in weeks. The mailing list had gone quiet. Nobody was asking
where Console Whisperer was. Nobody was knocking on my door saying "I need this, take my money."

I thought about just shelving it. Thanking people for their interest and moving on. I've done that before with other
projects. Start something ambitious, get 80% of the way there, get tired, move on. The graveyard of unfinished projects.

But this time I decided to do something different. Not because I had a renewed burst of energy or because the business
fundamentals had changed. I decided to ship it because I wanted to finish something. Go all the way from idea to real
product that someone can buy and use. Even if it's small. Even if it only does three things.

## What Console Whisperer Actually Does

Console Whisperer v1 lets you configure your mixing console using natural language through Mixing Station. You type what
you need -- "set up 16 lavs, 8 handhelds, and stereo playback" -- and it sets the channel names, colors, and routing to
main.

That's it. Names, colors, and sends to main. Three features.

It's a desktop app for Windows and macOS. You need Mixing Station Desktop running. You bring your own LLM key -- Google
Gemini has a generous free tier, or you can install Ollama and run it completely offline for free.

It costs $37. One-time purchase, no subscriptions.

[consolewhisperer.com](https://consolewhisperer.com)

## What I Learned About Scope

One of my biggest takeaways from this experience is how much I admire products with a narrow scope. Theater Mix, when it
first launched, only supported X32 consoles. That's it. One console family. And it was useful from day one because it
did that one thing well.

I tried to support every console model through a third-party API while also building an AI interface while also handling
all the edge cases of live sound workflows. In retrospect, I should have picked one console and one feature and shipped
that in a month.

If I'm being honest, I'm not great at scoping my own projects. I know this about myself now in a way I didn't seven
months ago. And that awareness is worth more to me than any revenue Console Whisperer might generate.

## What's Next

I don't have big plans to expand Console Whisperer. It was so much work to get here that I'm not sure I have the energy
for another round.

But I also know I'm bad at predicting the future. So here's what I'll do: if people buy it and start requesting
features, I'll respond to that. If there's demand, I'll build more. If there isn't, it'll just be a small product that
helps a few people set up their consoles a little faster -- and that's fine too.

The signals from a business perspective are mixed. People get excited about anything with "AI" in the name, but
excitement doesn't equal demand. Nobody followed up with me over seven months to check on this product. That tells me
something. Maybe not everything -- but something.

Either way, I'm glad I shipped it. It feels different to have a real product with a real price tag than another
half-finished project in a private repository. The learning journey of going from idea to shipped product is its own
reward, even if the product is smaller than I imagined.

If you're building something and you're stuck in the same cycle I was -- where the scope keeps growing and the finish
line keeps moving -- maybe just draw a line in the sand and ship what you have. It probably does more than you think.

Thanks for following along.

Nathan