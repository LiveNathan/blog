---
layout: post
title: "AidRunner: I Built a Delivery Router for My Neighbors"
date: 2026-03-09 00:00:00 -0000
categories: [building-in-public, entrepreneurship, java, micro-saas]
---

Two months ago I was sitting in my neighbor Sara's living room, helping her pack
groceries for delivery. She runs the Sunday mutual aid runs in our neighborhood, and
while we packed, she was juggling handwritten address lists and MapQuest trying to plan
the most efficient routes for four drivers. She needed everything figured out before
anyone left the house. The drivers couldn't bring their phones.

It's called the traveling salesman problem. And I thought: a computer would be better
at this.

## What Was Happening

In December 2025, the Trump administration launched Operation Metro Surge -- what DHS
called the largest immigration enforcement operation ever carried out. By January 6,
2026, they had deployed 2,000 federal agents to the Minneapolis-Saint Paul area.
Minneapolis has roughly 600 sworn police officers.

Neighborhoods in south Minneapolis felt it immediately. ICE agents (U.S. Immigration
and Customs Enforcement) were going door-to-door, monitoring bus stops, approaching
people in plain clothes. On January 7, ICE agents shot and killed Renée Good, a
37-year-old Minneapolis woman and mother of three, one block from her home in south
Minneapolis. The city, the state attorney general, and others sued to halt the surge.
None of it stopped what was already in motion.

Neighbors of ours -- documented or not -- started staying home. They stopped going to
work. They stopped going to the grocery store. Other neighbors started organizing to
help.

## The Mutual Aid Response

The organizing happened fast and mostly through Signal -- encrypted messaging, ephemeral
by design, the only platform people trusted. Groups formed. Block captains started
checking in with people on their blocks. A layered system emerged: vulnerable neighbors
told their block captain what they needed, block captains passed requests privately to a
small group of admins, vetted volunteers on a "care team" handled the shopping and
deliveries, and when a request was complete, everything got deleted.

The primary needs were groceries and rent. Organizers were shopping at Costco with their
own money and donated funds. Rent had to be paid in cash -- Sara mentioned there was a
literal cash shortage at Minneapolis ATMs at the time from everyone trying to stay
liquid. Baby supplies. Dog walking. Whatever people needed.

On Sundays, deliveries went out in batches. A handful of drivers. Fifteen or twenty
stops.

## The Phone Problem

People were leaving their phones at home for the Sunday deliveries. Part security
precaution, part belief that ICE was tracking devices.

Sara's fellow organizer Dana, who handles vetting for the care team, had an interesting
take on this. She pointed out that much of the fear around phone tracking was
hypervigilance -- people waking up to the fact that they'd given apps years of
permissions without much thought, and now suddenly paying attention. The real,
documented risk, she said, was social engineering: bad actors trying to infiltrate
groups and gather information.

But Dana also acknowledged: if people feel they need to leave their phones at home, that
concern is real enough to plan around. Whether or not ICE was literally tracking every
device, the fear was legitimate. And the operational response -- no phones on Sunday
deliveries -- was reasonable.

Which created a practical problem. If you can't pull up directions mid-route, you need
printed directions before you leave. If you have four drivers and twenty stops, someone
has to figure out who goes where.

Sara had handwritten addresses on paper and MapQuest open in one tab. (Google Maps was
out -- people had stopped trusting it for this, given concerns about Google's cooperation
with federal agencies.) MapQuest could sort the stops into a reasonable order but the
turn-by-turn directions were unreliable enough that she'd stopped trusting them. She was
mostly just figuring it out herself.

## What I Built

[Screenshot: AidRunner main screen]

I knew of a Java optimization library called [Timefold](https://solver.timefold.ai),
which is designed to solve exactly this kind of problem -- optimizing routes across
multiple vehicles and stops. I also knew that mapping APIs exist that don't rely on
Google. The one I'm using is [Geoapify](https://www.geoapify.com), which is built on
OpenStreetMap.

AidRunner is live at [aid.nathanlively.com](https://aid.nathanlively.com).

The interface is simple on purpose. You enter a depot address -- where everyone starts.
You pick how many vehicles. You add delivery addresses one by one. Every field has
autocomplete, which turned out to matter: address data for these deliveries moves by
hand between people, often without city or zip codes.

[Screenshot: address input with autocomplete]

Hit Solve, and it:

1. Calculates a distance matrix between every location
2. Runs Timefold to find the optimal assignment of stops across your drivers
3. Fetches turn-by-turn directions for each route from Geoapify
4. Returns a printable set of directions, one per driver

[Screenshot: solved routes with printable directions]

You click print, cut the pages, hand one to each driver. They leave with directions and
no phone.

## The Scope I Resisted

I had bigger ideas. I could see that these groups were using Signal as a makeshift help
desk -- creating "tickets" in DM threads, tracking status with emoji (👍 for claimed, ✓
for complete), deleting everything when done. It worked, but things fell through the
cracks. Organizers were carrying a lot in their heads.

I could build something better for that. A proper request-tracking system with ephemeral
storage, no central database, authenticated access through a web of trust. Something that
replaced the Signal-as-help-desk pattern while keeping the same privacy guarantees.

That's a six-month project. Maybe longer.

If you've read my [Console Whisperer post](/blog/2026/02/15/console-whisperer-seven-months-shipping-small.html),
you know I have a pattern where scope expands until I burn out. I recognized it and said
no. Route optimization for delivery drivers. One screen. Print. That's it.

## A Note on Privacy

I want to be precise about this rather than vague, because vagueness about privacy is
worse than honesty.

Address data does leave the page -- it goes to Geoapify for autocomplete and routing.
Geoapify uses OpenStreetMap. I'm not aware of any data-sharing arrangement between
Geoapify and US government agencies, but I can't make guarantees about a third-party
API I don't control.

What I can say: nothing is stored on my end. No database, no login, no analytics, no
persistence. Refresh the page and it's gone. If your concern is "I don't want these
addresses sitting on a server permanently," AidRunner handles that. If your concern is
"no address data should ever leave this device," it's not the right tool -- and I'd
rather say that directly than have someone use it under a false assumption.

## Free, For Now

I'm not charging for this. The Geoapify free tier is generous enough that I'm not paying
for API calls at current usage, and it felt wrong to put a price on something being used
for mutual aid. The server costs me something, but that's my problem for now.

If usage ever hits the free tier limits, I'll figure it out then.

## Who It's For

If you're coordinating deliveries for a mutual aid group -- in Minneapolis or anywhere
-- and you need to split stops across a few drivers and print directions before people
leave their phones at home, this is what AidRunner is for.

[aid.nathanlively.com](https://aid.nathanlively.com)

If it doesn't work for your situation, I want to know.

---

The response in Minneapolis to Operation Metro Surge has been remarkable. Millions of
dollars raised. Thousands of neighbors organized. Mutual aid networks that first formed
after George Floyd's murder in 2020 were reactivated for this. Groceries delivered. Rent
paid. People showing up for people in ways that feel old-fashioned and, right now,
necessary.

I built a small tool that might make one part of that coordination a little easier. I
hope it finds the people who need it.

Nathan
