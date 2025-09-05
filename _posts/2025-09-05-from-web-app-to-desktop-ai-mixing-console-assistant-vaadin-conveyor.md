---
layout: post
title: "From Web App to Desktop: AI mixing console assistant with Vaadin and Conveyor"
date: 2025-09-05 09:00:00 -0000
categories: [ micro-saas, java, vaadin, desktop-apps, packaging, conveyor, audio, building-in-public ]
---

# From Web App to Desktop: AI mixing console assistant with Vaadin and Conveyor

This fall, I'm heading back to live sound engineering, and I thought: why not build something that could make that work
more enjoyable?

## The Problem: Console Setup Tedium

One of the most tedious aspects of live sound engineering is mixing console setup. It's unpaid pre-production work that
involves clicking through hundreds of settings, configuring channels, and setting up routing. Most engineers, myself
included, just try to minimize this work rather than negotiate for compensation.

The typical approach is to work from templates and presets, but maintaining these across multiple console brands and
models becomes unwieldy. When you're working with 8–12 different console types per year, and manufacturers keep
releasing new models, keeping templates current is more trouble than it's worth.

Solution: a chat interface where you could type or dictate console setup commands and watch them execute automatically.
I called it "what if you could talk to your console?" and shared a 30-second demo video.

[![what if you could talk to your console?](https://img.youtube.com/vi/yTGguku-q1g/0.jpg)](https://www.youtube.com/watch?v=yTGguku-q1g)

The response was typical for anything AI-related these days—about a third loved it, a third hated it, and a third had
questions. But enough people seemed interested to keep going.

## The First Shock: Local vs. Cloud

I built the initial version as a single Vaadin web app and deployed it to my server. When I went to test it for the
first time, it completely failed. The app worked perfectly on my local machine but did nothing when deployed.

I was so naive about web security that I didn't immediately realize the issue: a web application running on a remote
server can't access devices on your local network. CORS (Cross-Origin Resource Sharing) security policies prevent this,
which is generally a good thing.

This meant I had to completely refactor the application into a client-server architecture. Suddenly, I needed to learn
something I'd never wanted to tackle: packaging and distributing desktop applications.

## The Packaging Odyssey

What I thought would take a day ended up consuming a full week. I tried multiple approaches, each with its own surprises
and failures.

### Attempt #1: JDeploy

I'd heard about [JDeploy](https://www.jdeploy.com/) on a podcast with its creator. It seemed perfect—a tool designed to
make Java desktop app distribution as easy as web app deployment. I spent about five hours on a Sunday setting it up and
building a GitHub workflow.

When it didn't work, I asked Claude to research the problem. The response was that JDeploy doesn't support Java 24.
Frustrated, I abandoned it.

In hindsight, I should have investigated further. JDeploy does support Java 24. I later discovered there are ways to
debug packaged applications and view console logs that I didn't know about at the time.

### Attempt #2: GraalVM Native Images

Next, I tried GraalVM native images. I'd used them before and knew they could work. I spent another five hours setting
up a GitHub workflow for this approach.

The good news: it worked. The bad news: the executable opened a terminal window every time it ran, and there's no way to
suppress this on macOS (though Windows has a flag for this). This looked unprofessional and potentially exposed
implementation details.

I learned that GraalVM native images aren't really designed for desktop app distribution—they're more suited to CLI
tools and cloud deployments where fast startup and low memory usage matter more than packaging elegance.

### Attempt #3: Tauri

[Tauri](https://tauri.app/) looked really promising. It's a framework that uses Rust for the backend and WebKit for
rendering, making it lighter than Electron while still producing real desktop apps.

I spent two days on this approach and got farther than with anything else. The packaged app looked professional—no
terminal windows, proper app behavior, and support for multiple platforms including mobile.

But then I tested it on Windows and hit a blank screen. The crushing realization: Tauri doesn't package the Java runtime
environment. It's designed for Rust applications with web frontends, not Java applications. I would have needed to
figure out how to bundle Java separately, which defeats much of Tauri's elegance.

### Success: Conveyor

Finally, I discovered [Conveyor](https://hydraulic.dev/). This was the first paid solution I'd encountered—free for open
source projects, but $45/month for commercial use.

The difference was immediately clear: Conveyor is specifically designed to support JVM applications (among others).
Well, it treats JavaFX as a first class citizen, but required some extra work to get it to work with Vaadin.

The packaging process was surprisingly fast—less than 30 seconds compared to the 5+ minutes required for GraalVM native
images. Even more surprisingly, the resulting artifacts were smaller (around 130MB vs 180MB for the GraalVM version).

Other nice features included:

- Usage of jlink and jdeps to create minimal JVM distributions
- Automatic generation of a download page with OS and CPU architecture detection
- Cross-platform builds from any operating system
- Proper code signing and notarization support

The main drawback was needing to adapt Vaadin (designed for web apps) to work like a desktop app—essentially forcing it
to open a browser window and shut down when that window closes. A better choice might have been to restart with JavaFX
or Swing, but jumping into even more new tech seemed like a bad idea.

You can check out my [Vaadin + Conveyor proof of concept](https://github.com/LiveNathan/vaadin-conveyor) on GitHub for
implementation details.

## Technical Details and Learnings

Here are the key technologies I evaluated:

**JDeploy**: The biggest differences between this and Conveyor seem to be that JDeploy is free handles all of the
signing for you. Great for an MVP. Maybe not the best long term.

**GraalVM Native Image**: Great for CLI tools and cloud deployments where fast startup matters. Produces standalone
executables with no JVM dependency, but the console window issue on macOS makes it less suitable for professional
desktop apps.

**Tauri**: Excellent for Rust + web frontend applications, uses WebKit for smaller bundle sizes than Electron. Not
designed for Java applications and doesn't handle JVM packaging.

**Conveyor**: Purpose-built for JVM applications with integrated jlink support and minimal JVM distributions. Fast
packaging, cross-platform builds, but requires a paid subscription for commercial use.

## The First Customer

Despite making questionable business decisions along the way, I managed to get my first customer yesterday. The product,
now called "Console Whisperer" (previously "Quick Console"), landed its first $50 lifetime deal.

I'm not following conventional pricing wisdom—I initially mentioned QLab-style pricing around $300 lifetime, so the $50
price point might have influenced the sale. But I'm more interested in getting the product off the ground and learning
from real users than optimizing revenue at this stage.

## Looking Forward

This journey taught me that desktop application packaging for Java is still a challenging landscape. Each solution has
trade-offs, and the "right" choice depends heavily on your specific requirements:

- **For rapid prototyping**: Conveyor's speed and Java-first design make it ideal while JDeploy handles all of the
  signing stuff for you.
- **For maximum performance**: GraalVM native images provide the best startup and memory characteristics
- **For web-first applications**: Tauri excels if you're willing to adopt Rust

I know I should have tried jpackage. It's the official solution. One minor criticism of it is that it does not handle
automatic updates, but mostly I just ran out of patience.

I'm excited to continue building something I can actually use while potentially helping other sound engineers along the
way. The technical complexity was much higher than expected, but the learning experience was invaluable.

If you're facing similar packaging challenges with Java desktop applications, I'd recommend starting with Conveyor or
JDeploy for rapid iteration, then evaluating other options based on your specific constraints around cost, performance,
and target platforms.