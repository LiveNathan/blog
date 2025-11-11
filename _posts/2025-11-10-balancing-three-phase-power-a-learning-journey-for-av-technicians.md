---
layout: post
title: "Balancing Three-Phase Power: A Learning Journey for AV Technicians"
date: 2025-11-10 08:00:00 -0000
categories: [ power, electrical, av-production, live-events, production-av ]
---

# Balancing Three-Phase Power: A Learning Journey for AV Technicians

> It blows my mind that we haven't blown a breaker mid-show... I've been waiting for something to happen.

That's a quote from my friend Marcus (not his real name), a master electrician with years of experience in live event production. He's really good at his job. He can calculate loads in his head, distribute equipment across three-phase power on the fly, and has successfully powered and lit hundreds of shows. But he's also acutely aware that he's improvising critical safety decisions under time pressure, without formal planning documents.

Marcus's words capture something I discovered while researching power distribution for live events: there's a huge gap between how production managers think about electrical safety and the reality technicians face on-site.

I'll be honest with you: I've spent most of my career trying to avoid learning about power.

For over 25 years in production AV, I focused almost exclusively on sound system design and calibration. Whenever conversations turned to power distribution, rigging, or electrical work, I'd find a reason to excuse myself. It's ironic, really—my dad is an electrical engineer, and he tried to teach me some stuff when I was a kid. Maybe that's exactly why I avoided it for so long. We all have our ways of rebelling against our parents.

But here's the thing about production AV: there's not much room for hyper-specialists. The industry needs people who can handle multiple disciplines, or at least understand how they all connect. So when I started working at [SquareWave](https://squarewave.com.au/) and pitched the idea of building a power calculation tool, I realized I couldn't keep avoiding this topic. If I was going to help build something useful, I needed to actually understand what I was doing, at least enough to build something useful.

This blog post is the result of a week of research. I did discovery interviews with four friends, posted questions on Reddit and social media, and did some reading about electrical systems. I don't have formal training as an electrician, so if you spot errors or oversimplifications in what follows, please let me know. This is as much a learning document for me as it is (hopefully) helpful for others.

Tool break: Tools are fun. I've really been enjoying Notebook LLM. My favorite way to learn is through audio, usually podcasts and YT videos. In Notebook LLM you can drop in a bunch of documents and links and generate an hour-long audio deep dive.

## What I Discovered: The Gap Between Planning and Practice

My research revealed a striking disconnect in how different people in the production world think about power. I talked to Derek, a co-owner and technical director at a production company, who told me frankly: "power is not that complicated." For the many repetitive corporate shows his company does, they don't need to "reinvent the wheel" every time. For a lot of people like Derek that I talked to, they've done so many shows and with their specific collection of equipment that you can pretty much do it by feeling. Most production AV companies only have a small number (1–3) of distros, so you get the big one for big shows and the small ones for smaller shows. A larger problem, actually, is bringing the right number and length of power cables. 

It also reminds me of something I used to say a lot during my trainings on sound system calibration: If you're not aligning your system, that doesn't mean that it's not aligned. You just don't know where it's aligned. Similarly, a power plan always exists, even if it's not explicitly documented. I think maybe I stole that idea from a Noam Chomsky quote. "If you do not do politics, politics will do you." So maybe I could tighten it up and say, "If you do not do a power plan, a power plan will do you." Too much?

It's a different story for the technicians in the field that have to execute this plan. Marcus described his typical workflow: "we don't necessarily plan anything, I just kinda usually figure it out on site... I understand what all of my equipment draws... and then just kind of go from there." He's doing mental calculations in the field, trying to distribute loads across three-phase power while the show is being set up.

And here's what really stuck with me. Marcus admitted: "it blows my mind that we haven't blown a breaker mid-show," and then added something even more sobering: "I've been waiting for something to happen."

That's the reality for a lot of technicians. They're bearing the responsibility for improvising safe electrical solutions under time pressure, often without formal planning documents.

I should stop for a moment to point out the fact that the most challenging thing to do as a novice on any subject is to understand full context. Therefore, I may be overstating the importance of this topic. It may be that it's not really that big of a deal because safety standards and hardware build in lots of headroom, so maybe we're never in real danger. From some sources it seems like this stuff is critical and from others it seems like a minor concern.

## The Hidden Problem: "Normalization of Deviance"

What's happening here is something safety researchers call normalization of deviance—when shortcuts become standard practice because nothing bad has happened yet. When you successfully power hundreds of shows using on-the-fly calculations without a single fault, the perceived risk diminishes. The informal method gets reinforced by repeated success, even though it's masking latent safety risks.[^1]

The technician successfully figures it out every time, so the project manager can maintain the view that power is simple. The complexity gets outsourced down the chain to someone improvising under pressure. The show still happens without incident, so there's not a lot of motivation for management to change things. It works—until it doesn't.

## It's All About Balance

After all these conversations, here's what surprised me: most production companies aren't particularly worried about sizing generators or calculating whether they'll overload a specific distro. As Derek explained, they typically have just a few distros—maybe a 100-amp and a 200-amp—and they know which one to use based on show size.

What people *are* doing manually, often with mental math or spreadsheets, is balancing loads across three-phase power. This is the practical, day-to-day challenge that kept coming up in my research.

## Why Does Balancing Matter?

Three-phase load balancing helps prevent reduced efficiency, tripped circuit breakers, and shortened equipment life. When your power distribution is significantly unbalanced, you're not just being inefficient—you're creating conditions that can damage expensive equipment.

Here's what happens: In a three-phase system (most commonly a Wye configuration in North America), you have three "legs" of power (L1, L2, L3) that are 120° out of phase with each other. Loads like your amplifiers and projectors are typically connected between one of these legs and the neutral conductor. When everything is balanced, the current flowing through these three legs is roughly equal, and the neutral conductor carries minimal current.

But when the loads are unbalanced—say you've plugged all your LED fixtures into L1, all your audio gear into L2, and left L3 barely loaded—problems start to emerge.

## The Worst-Case Scenario: What Actually Happens

When I asked Marcus what happens if you don't balance the legs properly, he said power goes down the neutral. So I asked, "What's the worst-case scenario?" He didn't know.

Fortunately, I posted this question on Reddit and got an incredibly detailed response from a German production technician whose company uses formal load calculations (they're even required for apprentice final exams in Germany). He explained there are two main problems when phases aren't evenly balanced:

First, the neutral conductor overload: In a balanced system, the currents on the three legs cancel each other out, and very little current flows through the shared neutral wire. But with significant imbalance, the difference in current must return through that neutral conductor. If the load distribution is very uneven, the neutral can carry more current than it's rated for. When that happens, the conductor heats up and can eventually burn out—creating a fire hazard.

Second, and more catastrophic, is neutral point shift: This is the scenario that really got my attention. If the neutral conductor becomes disconnected (for example, from a loose connection) while the load is unbalanced, it causes the voltage reference to be lost. This leads to increased voltage on the lightly loaded phases, potentially causing a voltage surge that can approach the higher line-to-line voltage (e.g., surging from 120 V up toward 208 V) and instantly destroying connected equipment.[^1]

I've never heard of this actually happening in a production environment, but understanding the physics helps explain why we balance loads in the first place. It's not just about efficiency—it's about preventing potentially catastrophic equipment damage.

## The More Common Problem: Efficiency and Heat

Even without neutral failure, unbalanced loads cause several practical problems: increased neutral current leading to line losses, reduced efficiency in three-phase equipment like motors and transformers, and excessive heating. For distribution transformers, every 8°C increase in temperature can reduce service life by half.

## How Much Imbalance Is Acceptable?

This was one of my key questions during research. The industry standard for unbalanced voltage is a maximum difference of 3% between phases. For current, I found references suggesting that keeping phase currents within 20% of each other is a reasonable target, though perfection isn't required or realistic.[^2]

Marcus, the lighting tech I interviewed, told me he typically does this balancing in his head while plugging things in. For smaller shows with a single distro, he'll mentally distribute the loads: "These fixtures to L1, those to L2, the rest to L3." It works because he knows his equipment and has years of experience.

But for medium-sized shows where you want documentation and confidence in your power plan, having a systematic approach makes more sense. You want a record of what you planned, especially if something does go wrong. Plus, as shows get more complex, it's harder to hold all those calculations in your head.

## A Practical Example: Medium-Sized Show

Let's walk through a realistic scenario. You're setting up a corporate event in a hotel ballroom. The venue provides three-phase power via a cam lock connection—typically 120/208 V in North America. You connect this to your distro, which breaks out the three phases (L1, L2, L3) and the neutral into multiple 120 V circuits you can plug equipment into.

Commonly you'll distribute your departments across the legs:

* Lighting: LED fixtures, moving lights, hazers
* Audio: Power amplifiers, mixing console, wireless rack
* Video: LED walls, projectors, media servers

The goal is to ensure each leg (L1, L2, L3) carries roughly the same current load.

## The Regulatory Reality: More Than Just Best Practice

Something I discovered during my research: proper power planning isn't just a good idea—it's actually required by federal law. OSHA's regulations (29 CFR 1910 Subpart S) mandate that employers use approved equipment, follow safe work practices, and have properly trained personnel.[^3]

The National Electrical Code (NEC, or NFPA 70) provides the technical specifications, particularly Article 590 for temporary installations and Article 520 for theaters and performance areas.[^4]

What struck me is that generating a formal power plan isn't just about preventing accidents—it's about documenting due diligence. If something does go wrong, having a documented load calculation shows you followed proper procedures. Without it, you're exposed to liability, even if nothing bad has happened yet.

This is part of why "normalization of deviance" is so problematic. Companies can run hundreds of successful shows without formal planning, but that doesn't change their legal obligation to have documented safety procedures. One safety researcher described it as "the gap between regulatory theory and on-site practice"—the rules exist, but many companies operate on experience and improvisation instead.[^1]

## What Power Values Should You Use?

This was one of the trickiest parts of my research because equipment manufacturers rate power in different ways, and the actual power draw varies dramatically based on how the equipment is being used.

### Audio Amplifiers

#### 12dB Crest Factor

For professional power amplifiers, "1/8 Power Pink Noise" has been historically used for typical real-world power calculations—this is pink noise at about 9 dB below the amplifier's clipping point.[^5] (The conversion: 10 · log₁₀(1/8) ≈ -9.03 dB)

This 1/8-power measurement provides a good approximation of typical speech and music signals being driven as loud as possible without clipping. As it says in the d&b D40 Reference Manual, "This represents the use case of live music or less compressed recorded music."

The reason 1/8 power is used comes down to the signal's Crest Factor. Crest Factor describes the ratio between the signal's peak energy and its average (RMS) energy. Live music and speech have a high crest factor (around 12 dB), meaning they have large, short peaks but low average power draw. Planning for the full power (like a constant sine wave) would result in a grossly oversized power plan that the client wouldn't need to pay for.

If you see an amplifier rated at 2,000 W, don't use 2,000 W for your calculations—that's a full-power sine wave rating that will never happen in practice. Use the 1/8-power pink noise specification if available, or estimate it at roughly 20–30% of the rated power for realistic show conditions.

Let's look at an example a d&b D40. There's a bunch of information in the user guide about the amplifier's power draw, but the number we want is Noise CF 12 dB. As it say, "This represents the use case of live music or less compressed recorded music." If you are running a single d&b V-SUB, which has a nominal impedance of 8 Ω, you would use the 1350 W value for your power plan.

![CleanShot 2025-11-07 at 08.39.52.png](https://raw.githubusercontent.com/LiveNathan/blog/58bfbaa2a774624cf945bfed9a8f4e4b4d799295/assets/images/CleanShot%202025-11-07%20at%2008.39.52.png)

#### 18dB Crest Factor

Not every manufacturer still uses a 12dB crest factor for music. Let's look at the example of a Meyer Sound 750-LFC subwoofer by way of the Amperage/BTU Calculator. If we add the 750 to the calculator at 115 V then we see its current draw is 5.4 A. There's a helpful note that say, "The minimum electrical service amperage required is the sum of each loudspeaker’s maximum long-term continuous current." 

How is maximum long-term continuous current measured? 

...eventually link to AES75, which has been adopted by many manufacturers including Meyer Sound, other manufactuer, other manufacturer. 

#### The risk of balance by category

There's a potential risk in simply attempting to balance the loads across all three phases by loudspeaker model. What if we put all of our tops on L1 and the subs on L2? On paper they may be balanced, but now we have exposed ourselves to frequency dependent risk. 

...more explanation...

It's interesting to note that in the operating instructions for the 750-LFC... (I don't know, can we draw some conclusions from this example or maybe not?)

### LED Lighting

LED fixtures typically list their maximum power draw, which is what they pull when at full intensity in all colors. This is actually a reasonable value to use for planning, since you'll likely hit maximum draw at various points during a show. (Lampies, check me on this.)

### Video Equipment

Projectors and LED walls usually draw relatively consistent power during operation. Use the manufacturer's specified operating power consumption, not the "maximum" spec which often includes unrealistic scenarios.

## How to Actually Balance Loads

Here's a simple process for single-phase loads (like most AV gear) on a 120/208 V system:

1. List all your equipment with realistic power draw values (Typical power draw in watts).
2. Convert to current for each single-phase device: Current (Amps) = Power (Watts) / Voltage (Volts)
3. Assign devices to phases (L1, L2, L3) trying to keep total amps per phase roughly equal.
4. Check your balance: Calculate the percentage difference between the highest and lowest loaded phases.
5. Adjust as needed until all phases are within 20% of each other.

## How People Are Solving This Today

Through my research, I discovered several approaches:

Vectorworks for big shows: Many (most?) AV companies use Vectorworks for their larger productions. The software can calculate power and generate load balance reports, but it's a separate tool from their quoting and inventory system (Flex, D-Tools, Lasso, etc.). So there's this disconnect—the power planning happens in one place, the business planning in another.

Spreadsheets everywhere: The German production company I connected with on Reddit has built a comprehensive Excel spreadsheet. It's pre-populated with the electrical data for all their equipment, and they can assign gear to phases and see the balance in real time. They've even added voltage drop calculators. But it's completely manual—you have to enter everything by hand.

Mental math on site: This is probably the most common approach, especially for smaller shows. Marcus's method of calculating in his head while plugging things in works when you know your gear and the show isn't too complex.

One user on the Flex community forum summed up the opportunity perfectly when I asked about building this into quoting software: "awesome and super useful, if you can get it to pull the right info." That's the key—if the power data is already in your inventory system, why enter it again?

## A Tool to Help: AmpLogic

While researching this topic, I was contacted on LinkedIn by Dom Trotta, who built a web app called [AmpLogic](https://domtrotta.github.io/AmpLogic) specifically for this purpose. He told me: "whenever I'm PM'ing small jobs, I always want to make sure the power is balanced across the right phases. I kept doing the calculations on my phone, so I thought—I should just build a small app to make it quicker."

AmpLogic includes features for:

* Building equipment lists with wattage, quantity, and phase assignments
* Real-time checks for overload conditions
* CSV import/export for documentation

Another Reddit user shared their company's spreadsheet approach, which shows the total load for each phase at the bottom so you can balance evenly. These DIY solutions show there's real demand for this kind of tool—people are building them because they need them.

## The Middle Market Sweet Spot

After all this research, I've concluded that systematic power balancing is most valuable for medium-sized shows. Here's why:

Small shows: The loads are light enough that rough balancing is enough. As Derek said about his routine corporate events, there's no need to reinvent the wheel—experienced techs can handle it.

Large shows: You likely have a dedicated designer using Vectorworks or similar tools that already help with power planning. These productions have the budget and complexity to justify specialized design software and dedicated personnel for power planning.

Medium shows: This is the gap. You're not using full design software like Vectorworks because it's overkill (and disconnected from your quoting workflow). But the show is complex enough that asking a tech to figure it out on-site creates real stress and risk. You have gear from multiple departments, significant power draws, and clients who expect professionalism—but you're trying to manage everything through your rental management system.

This is where tools integrated into quoting and planning software could be genuinely helpful. You can plan your power distribution as you're building your quote, print a balanced power plan, and show up to the gig with confidence. The tech isn't scrambling to figure things out under pressure, and the PM has documented their due diligence.

One of the video technicians I heard from on social media made a great point: it would be valuable to get a warning when the number of devices requiring dedicated circuits approaches the capacity of your planned distro. That's the kind of system-level thinking that's hard to do in your head but easy for software.

## What I'm Still Learning

There's still a lot I don't fully understand:

* The exact physics of why neutral loss causes voltage shifts
* How different distro configurations (Wye vs Delta) affect balancing strategies
* Best practices for balancing when you have both 208 V and 120 V circuits
* What value to use on a spec sheet for any piece of equipment for a power plan
* How power factor correction fits into all this

If you have experience with any of these topics, I'd love to hear from you. The production AV community is full of people with deep practical knowledge, and I'm hoping this post starts some helpful conversations.

## Final Thoughts: Bridging the Gap

For someone who spent decades avoiding anything electrical, I've found this deep dive into power balancing surprisingly interesting. But more importantly, I've gained a real appreciation for the stress that technicians like Marcus carry when they're "waiting for something to happen."

The disconnect between the office and the field is real. Project managers can maintain that "power is not that complicated" precisely because experienced technicians are handling the complexity on-site, under pressure, often without formal documentation. That works—until it doesn't.

What I've learned is that we need better tools integrated into the pre-production workflow, not separate systems that require duplicate data entry. When a Flex user says power calculations would be "awesome and super useful, if you can get it to pull the right info," they're pointing to the real solution: leverage the data you already have.

The key takeaways from my research:

1. Balance matters for equipment safety (preventing catastrophic neutral point shift), efficiency, and technician peace of mind.
2. Aim for within 20% current difference between phases.
3. Use realistic power values based on actual operating conditions (1/8 power pink noise for amps, maximum draw for LEDs, operating specs for video).
4. Document your plan rather than relying on field decisions—even if it's just a simple spreadsheet.
5. Tools exist to help, but the best tool would be integrated into your existing workflow.

Whether you're using a spreadsheet, a purpose-built tool like AmpLogic, or just keeping notes, the important thing is moving from improvised solutions to systematic planning.

*Have feedback on this post? Spot a technical error? Want to share your own power balancing strategies? Please reach out—I'm still learning, and I welcome constructive input from the community.*

[^1]: Synthesis of regulatory and practical analysis on the "normalization of deviance," the "gap between regulatory theory and on-site practice," and the neutral point shift worst-case scenario (Source: AV Electrical Safety Code Research & Power Calculator MVP Research Analysis).

[^2]: Industry best practice consensus on acceptable phase current imbalance, with a conservative default threshold set at 20% (Source: Power Calculator MVP Research Analysis, referencing industry thresholds).

[^3]: U.S. Occupational Safety and Health Administration (OSHA), 29 CFR 1910 Subpart S - Electrical (Source: AV Electrical Safety Code Research).

[^4]: National Fire Protection Association (NFPA), NFPA 70: National Electrical Code (NEC), Articles 520 and 590 (Source: AV Electrical Safety Code Research).

[^5]: Industry standard for audio power calculation, referencing Crest Factor and 1/8 Power Pink Noise, as outlined in manufacturer specifications (e.g., d&b D40 amplifier manual) and the Common Amplifier Format (CAF) standard (Source: Event Power Calculator Data Needs).