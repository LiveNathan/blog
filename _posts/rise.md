# I Built ShowBook for Six Months. My Customer Found Another Way.

I was waiting for a milestone before writing much about ShowBook. I wanted to get through its first real event so I could tell you what it actually did for someone, not what I hoped it would do.

Instead, I'm writing about shutting it down.

After the initial discovery and a March deposit, I spent about six months building software to help live-event producers turn meeting transcripts, emails, and spreadsheets into a production schedule their crews could rely on. I had a paying customer, real documents to build against, regular meetings, and more feature ideas than I could possibly finish.

Then my customer found a way to do much of the work with Claude and Google Sheets.

The easy headline is "AI killed my startup." That's part of the story. But it leaves out how I got here, the warning signs that arrived before the ending, and the part of the experience I actually wanted most.

## This time, someone paid

ShowBook wasn't my first attempt at building a software business.

There was SubAligner, where I ran into the limits of a small market. AV Sync, where I couldn't establish clear demand. GainGuardian, where technical challenges and the lack of a path to market stopped me.

With AV Sync, I kept trying to build a product by consensus. Business books said to talk to customers about their problems, so I talked to customers about their problems. More than 50 AV managers. When I couldn't find enough overlap, I did more interviews.

I thought I was being diligent. I was also hoping that if I worked hard enough, the conversations would eventually tell me what to build.

With ShowBook, I tried something different: interview five people, pick a specific problem, and move forward. I had seen this work at SquareWave, where we sometimes build a feature for one customer and then generalize it for others.

The problem I picked was familiar from my years in live sound: getting the information out of all the conversations about a show and into the document people use to run it.

A production schedule isn't just a calendar. It tells you which room needs to be ready when, who's responsible, what equipment goes where, how the room should be arranged, and what changed since the last conversation. A mistake can mean the crew arrives without something important, or everyone is working from a different version of the plan.

My first customer was already recording client meetings. For a complicated event, he might have 12 to 14 transcripts, plus email chains, that needed to become a coherent production schedule. He was using ChatGPT to help, then doing the work of organizing and formatting the result in Google Sheets.

He didn't need to be convinced that the problem existed. He could show me the inputs and the finished document.

I made an HTML mockup using his real material. On March 25, he paid a $500 founding-customer deposit.

That felt enormous. With AV Sync, I hadn't been able to get anyone to commit. This time there was money, a specific person, and a specific job to do.

It wasn't imaginary demand. But I would eventually learn how much distance there is between someone paying for the future of a product and depending on the product today.

## The best part wasn't the software

My customer did almost everything you would want an early customer to do.

We met regularly. He shared real documents. He tested things. I would send an email with questions and often get a detailed response the next day. He explained not just what he wanted changed, but how the work happened and why a seemingly small detail mattered.

When I sent mockups, he studied them. When I needed to understand what a technician should see on a room handout, he showed me examples. He helped name features using the language his crews already used.

We became friends.

I want to say this clearly because a story about a customer finding another solution can easily sound like a complaint about the customer. It isn't. He had a business to run. Finding a better way to run it was exactly what he should have been doing.

Working with him was one of the most satisfying parts of the whole experience.

In previous businesses, one of the hardest things was getting people to give a fuck. My teaching business declined gradually over the years. Near the end of one attempt to revive it, I offered free Q&A sessions. Nobody signed up. Nobody came.

That's a particular kind of sadness: making yourself available and discovering that nobody wants what you're offering, even for free.

Every SubAligner subscription includes a private training session with me. Nobody has taken me up on it.

So having someone who cared, who replied, who wanted to think through the problem together, felt wonderful. It gave me energy to keep going.

When I've done career coaching with sound engineers, I ask them to describe success in detail. Not just a number, but what their days would feel like. I've done that exercise myself, and the word that keeps coming up is "thriving." A useful product, enough income to pay the bills, and customers who want to collaborate on making it better.

With ShowBook, I got a little piece of that life before I had a sustainable business.

I think that's part of why it's hard to let go.

## A simple idea with a very long prerequisite list

The promise sounded straightforward: put in the transcripts and emails, get out an accurate production schedule.

But before that could be useful, there were a few things to build.

A schedule needed to be editable. Importing a spreadsheet couldn't silently lose columns. The software needed to distinguish a standard room setup from changes for one particular session. It needed contacts, crew assignments, room-specific handouts, printable output, and links people could open without creating accounts.

None of these were silly requests. They were the details that made the difference between a demo and something you could actually use at a show.

Even a basic question like "When is the event?" turned out not to be basic. Sometimes there was an event but no confirmed date. Sometimes there was a time, but it was tentative. A spreadsheet lets you turn a cell yellow, add a question mark, and keep going. Software that insists on a definite answer can make the job harder.

I started to understand a production schedule differently. For much of its life, it isn't a finished plan. It's a record of what you know, what you think you know, and what you're still waiting to find out.

Then there was the question of which information to trust.

In an October conversation, my customer described receiving a newer email that referred to an older version of a room-allocation document. The email was recent. The information in it wasn't. Simply accepting the latest message would have made the schedule less accurate.

This was the kind of problem I wanted ShowBook to handle: preserve where a detail came from, distinguish confirmed information from guesses, and make conflicts visible instead of confidently overwriting something correct.

That was a real reason to build purpose-made software. It was also a lot of software.

We had a roadmap that went from a skateboard to a scooter, a bicycle, a motorcycle, and finally a sports car. First import the data. Then edit it. Then make bulk changes in natural language. Then bring in transcripts and emails. Eventually, automate the whole production bible.

The metaphor helped us talk about the stages. It also exposed the problem: the thing he most wanted was several vehicles away.

By late summer, we were still working through the basics of making ShowBook a comfortable place to work. In June, the feedback had already been clear: importing a schedule was useful, but without easy editing it was mostly a viewer. By September, he was testing imports and reviewing outputs, but ShowBook still had not become the place he did his day-to-day work.

The project was moving. Adoption wasn't moving at the same speed.

## Dallas was going to be the test

We had a concrete destination: a November event in Dallas.

I planned to go, work alongside the crew, and see what happened when ShowBook met a real show. Not just another screen-sharing demo. Actual people needing actual information at the moment they needed it.

We worked backward from that. The crew needed room briefs and show handouts before the event. Those weren't decorative reports; they were how people ran the rooms.

The deadline became November 10, one week before the trip.

On October 31, I sent an update saying I'd imported the full 96-row production schedule and manually entered the contacts from his spreadsheet. I didn't wait for the automatic solution. I did the work so we could move forward.

There's nothing inherently wrong with doing things manually for an early customer. You can learn a lot that way. But the distinction between helping someone adopt your product and becoming the person who operates it for them matters.

On November 1, my customer explained that learning another system on top of preparing the show was more than he could carry. He proposed that I drive ShowBook for Dallas: handle imports, keep it accurate, and run it onsite. His spreadsheet would stay the source of truth. We could evaluate the outputs with the crew and discuss the future afterward.

That was a reasonable proposal for getting through a show. It was also a different experiment from the one I thought I was running.

I wanted to find out whether a producer would replace part of his workflow with ShowBook. We were moving toward finding out whether I could deliver useful documents while operating ShowBook myself.

A founder-operated service might have been worth pursuing, but it would not have answered the question I started with.

## Meanwhile, he was solving the problem

While I was building, my customer was experimenting too.

He was using Claude to read emails, meeting transcripts, planning documents, and his production schedule. In our October 14 meeting, he showed me how he was comparing information across those sources, finding discrepancies, and preparing updates.

It wasn't perfect. He still checked its work. Sometimes it misread things. But it worked inside the tools he already knew, and he could change what it did by asking.

If he wanted a new summary, a different way to organize the information, or another cross-check, he didn't need to wait for me to build a feature.

That is a hell of a competitor.

My first instinct was to say this happened overnight. Looking back through our conversations, it wasn't quite overnight. The direction had been visible for a while. What changed was how much he could accomplish without waiting for ShowBook.

We discussed a pivot: make ShowBook the structured source of truth and let Claude read and write to it. There were still reasons that might be useful. Reliable structure, change history, and traceable sources don't stop mattering because a chatbot can edit a spreadsheet.

But those advantages would have to be valuable enough to justify moving his information, learning the system, and maintaining another tool.

By early November, when I asked what was still missing, he said he was starting to feel a decent groove and less was keeping him up at night in this area.

I was glad the work was getting easier for him, even though it made the case for my product harder to see.

The problem hadn't been fake. The solution no longer needed to be mine.

## Did Claude kill ShowBook?

I think Claude helped make ShowBook unnecessary for the one customer whose demand I had actually established.

That's a narrower claim than "AI killed SaaS," and a more useful one than pretending technology had nothing to do with it.

ShowBook was built around using language models to do work that would previously have been difficult to automate. The same improvement that made my idea possible also made it easier for my customer to assemble a solution without me.

But I can't honestly put everything on Claude.

The product wasn't ready quickly enough. We spent months on the prerequisites. I had one paying customer, not evidence that a whole market wanted the same thing. I also let a small, valuable tool grow into a much larger system.

I always wanted a micro-SaaS business: something narrow enough for one person to build, sell, and support. I didn't set out to replace an event producer's entire working environment. Yet a series of reasonable decisions took me closer and closer to doing that.

Could faster delivery have changed the outcome? Maybe. I don't get to run the alternate version of the experiment. It's also possible that getting him into ShowBook sooner would only have postponed the same question: why use this instead of improving the workflow he already has?

I'm not going to turn a business I couldn't make work into a confident prediction about everybody else's business.

I decided to stop rather than invent another reason to keep building. I shut ShowBook down before the Dallas field test. The event we had been building toward would go ahead without it.

## What I want to remember next time

**A payment matters. So does what happens after it.**

The deposit was a meaningful signal. Someone was willing to spend money on the problem and trust me to work on it. I don't regret taking that seriously. But it wasn't proof of repeated use, a successful switch, or demand from a second customer. I need to keep those questions separate.

**Feedback and adoption are different kinds of progress.**

A thoughtful customer can give you enough good ideas to keep you busy indefinitely. There are still more than a hundred open issues in ShowBook. Many are genuinely good ideas. The existence of more useful work does not tell me whether I should do it.

**Compare against the customer's current alternative, not the one from the first interview.**

When we started, I was competing with hours of manual synthesis and formatting. By the end, I was competing with a person using Claude in a familiar spreadsheet. The comparison changed while I was working on the product.

**Technical advantages have to earn the switch.**

I still care about reliability, source tracking, and making uncertainty visible. But "this could eventually be more robust" doesn't pay for the work of learning it today. My customer wasn't failing to appreciate good engineering. I hadn't made the overall trade worthwhile enough.

**Put a boundary around the next experiment.**

Five interviews was a useful boundary for discovery. I needed an equally clear one around building: what behavior am I trying to observe, by when, and what will I do if it doesn't happen? Dallas gave us a date. It didn't keep the definition of the test from changing.

**Remember what I want from the work.**

I want income, independence, useful work, and people who care about what we're making together. None of those are unreasonable things to want. But enjoying the collaboration isn't evidence that the business works, and ending the product doesn't make the collaboration worthless.

## What's next?

I don't know yet.

I could revisit GainGuardian if better tools help with the technical obstacles. I could help businesses with AI and automation, since I've become pretty obsessive about both. I could also stop trying to turn every useful skill into another company for a while. I'd probably have more free time, and quite possibly more money.

Right now, I don't want to rush into a new idea just to avoid feeling disappointed about this one.

My first reaction was that I'd spent six months and had nothing to show for it. That isn't quite true. I learned a great deal about building software, working with a paying customer, and the difference between making progress on a product and making progress toward a business. I also made a friend.

I wish those things had come with a sustainable income. They didn't.

The part I will miss most isn't closing issues or planning the next feature. It's sending someone a question about a problem we both cared about and knowing I'd get a thoughtful answer back.
