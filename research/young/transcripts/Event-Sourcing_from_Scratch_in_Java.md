# Event-Sourcing from Scratch in Java

**Video URL:** https://www.youtube.com/watch?v=DA0R0FD2DW4

---

## Transcript

Welcome folks. Uh, as you know, my name is Ted M. Young. Um, I am a, uh, longtime Java fan, uh, trainer, coach, live
coder. So, I've been doing Java for 30 years. Um, uh, currently I I do individual and team coaching uh, for basically
helping teams make their code more testable. So one of the things that is uh uh underpins almost all that I do and how I
think about design and architecture is from a point of view of testability. How do we make our code more testable?
Things like that. Um uh just general note if you want your uh webcam on that would be great. Um but no pressure. Uh if
you want to leave it off that is fine as well. Um, but sometimes it's nice for me as a presenter to see folks faces. And
so, uh, I've been doing event sourcing for for couple years. Um, and there's a, uh, one of the things that's that's, you
know, always helpful is is, you know, when you learn stuff, uh, that you teach it as well. Um, and I gave this
presentation uh last month at the DevText conference in Colorado, which was great. Um, had lots of good questions. And
so, uh, so welcome to my TED talk. I always forget to say that, but as uh TED is my first name, I can say this is a TED
talk. So, welcome. And, uh, you can see all the places you can find me. So, TED.dev is my website. Um, as uh mentioned
before, recording of this will be available. So, um, if you don't want your your face and/or voice to appear on the
recording, uh, then you probably want to mute and and hide yourself. But otherwise, the recording will be available. Um,
I will make it uh available at the TED.devtalks. You'll you'll see the uh recording slides uh source code. So the source
code is fully open source and it's actually I continue to work on it um as I mentioned on my live coding stream. Uh so
one of the things we're working on now is uh what are called projectors and I'll talk a little bit about that. Um I'm
also doing another talk on testable architecture. So as I mentioned testability is is the underpinning for for how I
think about coding and and design and and architecture. Uh so there's an online session uh with the Calgary software
crafter group crafters group. Um and so you can uh go and sign up and I'll throw that into chat for the link. And so
that's coming up uh on December 10th. Um probably too late for those of you uh not in sort of east of the eastern time
zone. So, you're open. So, it's probably going to be too late for you. It'll be like 2 AM for at least for for some of
you. But that will also be recorded. Uh, and uh, I'll let you all Let's see. Why is that? There we go. Uh, so I don't
want this to be just me talking outwards, even though I I do that a lot. Um, and so if you have questions, uh, ask them.
Um, throw them into chat, uh, raise your hand. Um, whichever you prefer. I I I'll monitor chat and if I see, uh, a
question pop up, I'll either acknowledge it and say I'm going to talk about that, right? So, uh, I reserve the right to,
um, defer the question uh, if I know I'm going to get to it. If not uh then then I'll answer it. In addition uh the the
time that I've set up for this it was 90 minutes because when I did the talk it was about an hour and a quarter. Um so
90 minutes will give us time for questions. Uh and at the end I will basically hang out until there are no more
questions. So if you want to discuss further and deeper uh then uh there's going to be time available for that. All
right. So, um when I started looking at at event sourcing, um one of the things that I was looking around for were
frameworks and libraries. Uh and so in Java, unfortunately, um and I find it to be a little strange that really the only
framework that is gotten any kind of widespread Mind share is Axon IQ. Um it's really a framework. You have to buy into
it. Uh and there's a lot there and it's well supported and and and the folks are are who are behind it are knowledgeable
but it is it is big and I think uh from a learning standpoint it's overwhelming. Um so it's not where I would where I
would start. Uh but there's no there's a couple of other ones. Um there's OpenCQS, but that's uh coming from uh a vendor
that has their event store database product. Um and I'm always a a little wary of being tied to to something something
like that. Uh but the clients and some of the other stuff is is open is open source. uh in the net world is Martin and
uh there seems to be a lot more event sourcing going on in the net world uh that I I just find fascinating from a social
you know point of view of like community point of view is like why is why isnet you know adopting this and I don't see
as much talk about it in in the Java world other than sort of you know axon IQ um PHP has event s sauce uh which is
always fun to say when you're used to saying event sourcing. Um and uh I've learned a lot from from actually just
looking at at their documentation. So looking at the documentation for for both Martin and Event Sauce uh was was
interesting. Um I am obviously writing code to do event sourcing from scratch and we're going to look at how you
implement it. It's the technical parts are not that difficult. What what's difficult is the mind shift and that takes a
while to get used to. Um if you're familiar with CQS and you've done that without event source s event sourcing uh then
the shift is going to be a bit easier. Um but one of the big shifts is this idea of not using the same tables for
reading and writing. That's like the fundamental So as I mentioned going to do this from scratch, right? So I'm not
using any libraries other than uh Spring for uh Spring Ja data JDBC for for storing rows in a table, but you could
totally do this using almost raw JDBC. There's not uh there's not a lot there. And so um really want to to to come at
this from what does it look like to to implement this from from scratch and then how does that uh help us help us
understand what what's going on. So the first question is how do we persist data? So we'll talk about what I we'll call
traditional ways of doing that right the ways we we probably do it right now. Um, I'm going to define some of the terms
because, you know, terms like event and event stream and and event store and and all these kinds of things have lots of
different definitions in our our industry. And I struggle sometimes to come up with better terms, but sometimes it's
like, well, this is the only way to describe this. uh I'm also going to clarify some some things around uh the different
architectures or designs or or mechanisms that also use some some of some of these terms. Uh and then I'll talk a little
bit about the domain for this example application because one of the things I think is really important for learning and
and talking about this stuff is having an example application that's non-trivial. Um, on the other hand, it's also
useful to have one that's not huge and hard to understand. Uh, so jitter ticket is is my example app for a concert event
uh ticketing domain. And and for better or for worse, it has the word event in there. And so uh event even has now more
meanings. You got one from the domain, you got one from uh uh the the actual event sourcing and and other things. So,
um, it might not have been the best domain, but it was one that, uh, I love going to concerts and and and so there you
go. Um, and then we'll dive into the code. Uh, so it's one of those like as I mentioned like learning how to do this. I
think it's for for me it was you know I I got into this um so there's uh a project that I'm working on is is bringing my
TDD game online. So I have a board game called Jitter Ted's TDD game and I want to put it online so that people can play
it remotely and I wanted to use event sourcing because uh I'd you know done a lot done a bit with it. Um, and then
someone asked about, hey, do you have a simpler out uh example cuz there's a lot of of stuff that is nothing to do with
event sourcing, but that's in the TDD game online. Uh, and so basically, I took a detour and that detour has lasted uh
coming up on almost a year, maybe nine months. Um, so we'll we'll dig into the code. We'll also dig into the tests
because I think the tests um you know as I mentioned test I'm all about testability. Uh everything in this codebase and
in most of my uh code bases are test driven. Um and so we'll look at the tests and see uh how you actually test an event
sourced application. One of the nice things is that it's actually really straightforward. Um so so we'll look at that.
uh I'll touch on some related topics because to cover everything that's in the world of event sourcing would take way
longer than than just 90 minutes. Uh so there's some stuff about that I've already mentioned like CQRS. Um there's some
ways of modeling things Uh I'll touch on that a little bit. Uh then there's event storming which is not directly related
to event sourcing but is very useful. uh um and there's some nuances between the different kinds of events and I'll I'll
also talk about that. Uh I think the popular topics also are versioning and schema migration. I'll touch on those a
little bit. Um and performance always comes up. Uh I'll I'll talk about that a bit as well. Um and uh there's some other
interesting things in in the area. um something called dynamic consistency boundary which I sort of fell into myself and
then found that there was uh ax the folks from Axon IQ actually came up with a name for that. Um there's also decider
there's also uh privacy issues in terms of of what if you need to forget information. So in a typical traditional
application um how do we persist data? often we map our objects to database tables, right? We use an ORM of some sort.
Maybe you're using Hibernate through Spring Data JPA or you're using uh something like Juke or different ways of or
sometimes you're you're just writing raw SQL which is But all of these are are trying to map the data that we have in
memory that we're operating on to do things right. So I'm very much um I like a good domain model, right? So I love
domain driven design. I love good good domain objects. Those don't always map well to relational tables. Uh and then we
sometimes get issues in retrieving them. Um, and depending on the OM that you're using, you may run into issues, you
know, the N plus1 select N plus1 problem, lazy loading, things like that. Um, I tend to use Spring Data JDBC because I
don't need all that stuff. I don't I just want to load stuff. But even there, how do we persist data sometimes as an RM?
If I have a domain object for me, it must be fully encapsulated, right? That's the whole point. Uh so I run a book club.
We just finished uh reading balancing coupling and really what that book is about is modularity and encapsulation is a
way of enforcing modularity boundaries. I don't want other parts of my code to know how I store data inside of my
objects. Yes, the book from uh Vlad Connotes. Yes. Uh really good book, highly recommended. Um and so one of the issues
I always ran into with having this really rich domain model in memory is how do I get the data out and then how do I
reconstitute it in memory when I need it. Right? So typically you know some action comes in from the outside a user says
buy a ticket. So I need to load load the concert to see can I are there tickets available is this in the future right
you can't buy it's very difficult to buy tickets in for for uh concerts that have already happened uh unless you're eBay
and selling vintage tickets or something like that but typically you'd want to load the thing up it are can this person
buy the tickets and there are all sorts of business rules but I need that data loaded in memory so I can make a decision
and how do I reconstitute objects and how do I store them? You know, so we've sold tickets and so therefore things like
available tickets have to be reduced. Um if there specific seats, we have to allocate those and then we need to save
data. But if you really encapsulate your objects, how do you get at that data? And this is the mapping problem. Um I
have come to uh uh a solution that I like which is I basically grab a snapshot and so the objects provide a snapshot
which is going to be just um a simple class or or record in Java and it's just going to be the data. So it's just a bag
of data. um it breaks encapsulation because now somebody could go and call that method and grab out all the internal
data and fuss with it or look look at it um at the compromise. Uh and so what I do is is I use a tool like Arcuna to
ensure that the only code that can call that invasive intrusive method is my database repository. So at least that way I
have a test that when it fails if some code is trying to access that and and it's not the repository then it shouldn't
access it and basically the test will fail. So therefore I I basically then in a sense map my my domain objects to
objects that can that then get stored in the database. So what does that look like? It looks like this. Right? So here
I've got uh a concert service. Um and so here we want to do some uh we want to get it loaded. And so what happens is we
we basically do a find uh that gets forwarded to a repository adapter. So I tend to use a hexagonal like architecture.
It's not pure hexogonal. Um I do hexagonal plus uh domain driven. And so the adapter then turns around and and calls the
the technical implementation in spring. This would be a repository uh interface uh does the find and it does the select.
It figures out how to do the select. It then gets a result set from the database. Uh that gets converted by the the OM
into some data transfer object. I often call these database objects. uh and then that gets returned and then we
reconstitute the object the domain object uh from this DTO and now we've got an object an entity uh in this case it
would be technically an aggregate so this is the process right so we've got a couple of uh we've got a transformation
that happens sort of behind the scenes by the OM right takes whatever the result set is and converts it into an object
and then we take that object because it's just a bag of data and recon constitute our object that has the all the
behavior around that data. Uh and that's how that works. This works well. Um but there is a problem. Uh and maybe you
don't encounter this problem, but often what what people ask is like why should I do event sourcing, right? State
sourcing, CRUD sourcing, whatever you want to call it. I sometimes call it overwrite state sourcing to emphasize the
fact that we are overwriting any previous data that was there um is we have no history information gets thrown away. Now
if you don't care and if you never care about history that's totally fine. uh but we don't have any knowledge of how or
why the the state changed or when sometimes and what we end up doing is we often add stuff maybe we've had long
experience of like oh somebody's going to ask us for the audit trail or the history of these changes let me go write
extra code to store that and maybe you have some automatic stuff that the database does or maybe your RM you've
configured it in a way so that it automatically saves off changes to another table. But these are special one-off things
and you have to know them up front. Right? So, right, we've got a concert, it's got an ID, it's got a version, right?
So, we use that for optimistic concurrency. Um, and then we decide that uh we need to change the ticket price because
somebody did a typo and it shouldn't have been 135, it should have been 35. Version number changes. we persist that um
we figured out a way to fit more people in. So we increased the capacity uh from 100 to to 120 tickets available right
but was why did why is it 120 you know somebody said I thought it was 100 what happened why what's going on who changed
that when did it happen &gt;&gt; yeah and so uh Hussein mentioned sort of you know uh auditing is important in some
domains where you must have an audit trail of what happened for legal compliance, whatever purposes. Uh, and unless you
again explicitly code for this, that information is gone, right? We have no we've lost all those changes. All we see is
what it currently is. We know that it's version three. So, we know there were two previous changes. And again, we might
have long experience. We might even have the requirements that we need to save these things as an audit trail. But then
now that's extra work, right? That's extra work that again maybe you have a good library or or the framework and and
configuration can set that up, but you have to know which pieces need that audit trail because you may you probably
don't want to do it for for everything. So there are three fundamental pieces in in event sourcing. There is the past,
things that have happened and we call these events. They are in the past, they are facts. In fact, uh I almost prefer to
use the word fact than event, but it's an event. Um the present is what is the current state and then uh sort of future
kind of idea is that uh we're we then want to do something against the current state. Right? So command is a request to
change state. That's really all it is. Right? And if you know command queries, you know that there are two types of
things. commands are requests to change state and queries is like what is the current state. Uh another way of looking
at this is commands I always more and more I I I think of systems as basically being big state state machines and so
we're pushing it through different parts of that state machine through commands. Sometimes they're allowed and sometimes
nope no concert uh tickets left so you can't buy tickets or there aren't enough So an event is a fact. Something that
has happened. Not will happen, not might have happened. It happened, right? Customer registered that happened and we
have the information around that customer. Probably their name, probably their email address, maybe some other
information, but that's a that's a fact. And so you'll see that like in most systems that use events, they are in the in
the past because they're recording the outcome of some decision that was made. Uh concert scheduled, ticket purchased,
ticket transferred. All of these things are facts. They happened. They may have happened incorrectly if we have a bug.
uh or maybe we change other things and and it turns out that we need to somehow undo them. But the fact is they they
happened and you can't just erase history uh and replace it with something else. So these events are generally
considered immutable. They're facts. They're they're stored somewhere. Um and depending on the context, sometimes
they're temporary. Uh in event sourcing they are uh persisted always. So those are events. Uh and this generally applies
to any place that's using event whether it's event sourcing, event- driven architecture, event streaming, all these
kinds of things. They are generally like this happened and it could be sort of passive things like temperature changed,
right? So if you got sensors and and IoT and you got lots of events, they could be just like this is the the the
temperature at this point. And this is our data model needed by the application so that our behavior can do stuff right.
So uh we want to we want to see what is the current state. This is the current state of of the system. It has data uh
and somewhere behind that is behavior that then the command uh executes against. So, it's a request to change state and
these are often sort of imperative. Hey, go schedule this thing. Go reschedule the concert, purchase tickets, right? All
these are commands. They may fail or they may succeed in odd ways. Uh, and by odd, I mean sort of, uh, you purchase
tickets and there aren't any available, but it's going to sit there and wait for a bit. Uh, and, you know, maybe some
will be freed up. Um, but all of these can fail and can result in, "Sorry, you can't reschedule this concert. It already
happened. Can't reschedule this concert. It's only 24 hours away and we can't do that. Purchase tickets. There aren't
enough tickets available." So, these are requests to change state. And whether that request is allowed is is the So
there's sort of two general things that that I I like to think about in in event sourcing. There's sort of two pieces
for state to change. And this is it. This is the hard part. This is I'm used you know for decades I always thought of
good OO as like the object is there I execute a method against it and then now that object state might have changed if
it was allowed it changed and now that's it and I can store it and so on but that's it you know if they're sitting in
memory for a whileve I've done desktop systems and so stuff is sitting in memory for for a while and So you make the
change, it now has a new state. Make another change, it now has the new state. Right? Sort of it feels like one thing
that I do. I execute a command and now I can ask the object, hey, what's what's different? In event sourcing, this is
split into two pieces. Commands generate events. Not always, right? Because there's always a possibility a command could
be rejected. But if it's successful, a command generates one or more events. typically one, but it can generate two So,
reschedule concert, if it's successful, generates a concert rescheduled event with the information that we need to
reconstruct what exactly happened, right? Probably the new date and time. If the artist changed, hopefully it didn't
change drastically, but maybe we added a new headliner, it would be, you know, update uh artist updated or opener added,
right? And these are domain terms, right? These are things But again, if we can't reschedule a concert and that behavior
is again up to the business, maybe we're allowed to change it. Or maybe, right, the there was a snowstorm and the band
couldn't make it over the mountain because they didn't uh because their bus can't can't make it and so we've got to
reschedule it. Um or no, it's starting in an hour, we can't reschedule it, right? So whatever the business rules are, we
implement those. And so in this case the command is not successful because remember it was just a request uh and so we
don't generate events or we might generate an event of rescheduled attempted right so even failures can also generate
events it depends if that's that information is useful or not yeah so uh uh so hopefully that that addressed your your
your question George if you if it's important to understand that this was attempted and failed then you record it as an
event. if nobody cares and I think probably most of the time again it may depend on do you have regulatory compliance
and there's potentially security things like somebody attempted to do something those possible um but in general uh you'
re probably not going to record the failures but again this is up to the business do they care about that stuff um and
so ask asks if there are multiple events generated Are they part of a a single transaction? Absolutely yes because they
are this the actual state that changed what happened and so it must be part of of the the same transaction. Um but we'll
we'll look at that and this is actually one of the benefits of event sourcing is it actually makes some of this stuff
easier. So we've generated events but that in-memory object state actually hasn't changed yet. And so when we execute a
command on an object in memory, events get generated and then immediately they get applied. So commands generate events
and then events update state. And it's important to separate these because when we want to rebuild that object in memory
so that we can ex right from you know take it from storage and rebuild it in memory so we can execute a method against
it we need to have the current state. Well how do we build that state? We take all the events that ever happened and
apply them and now we have the current state. Now a side note I am talking about all this stuff from an object-oriented
language point of view. I do this in Java. It's going to be similar for other object-oriented languages for functional
languages and whether JavaScript falls under that or not. That's a debate for another time. Um, but for languages like
Elixir uh and so on, it's slightly different. You're not uh rebuilding the object and and it has the behavior on it.
you're you're still rebuilding the data and then you're basically passing it into a function. Um there's a book uh and
I'll have some resources uh at the end for for you to to to look at. There's a book called real world event sourcing
that uses elixir um for the code in in the book. Uh and so you can sort of see how that works um from from a functional
standpoint. Uh really good book and and I'll mention again later. So events update state which means if we want to get
the current state we need to grab those events and then apply them. So we get a concert rescheduled event we update and
now the new state of the concert in terms of its date is now November 2nd And so you don't just have one event, you have
multiple events. So if we want to build the current state of what is the current state of this concert entity, right?
I've got an ID. What's the current state? Well, if there were these three events, then this is the current state.
Concert was scheduled, right? We we saw this before from the data point of view, but now we're looking at it from from a
series of events. Concert was scheduled. The band's name is Sonic Waves. They're playing on October 30th, $135 a ticket,
and they're 100 ticks available uh for this venue. Then we changed the ticket price and then we rescheduled the conf uh
conference concert uh to November 2nd. And so we apply these events in order. So order is critical. Uh but it's also not
that hard. Events uh databases and other mechanisms are really good at generating numbers that that increase. uh you
don't have to worry about there not being gaps as long as it's increasing and you can get the order correct that's all
that matters and so when we what we call project uh sometimes called fold or apply whatever term you want to use we are
taking all these events and just applying them and so we end we start with an empty object we apply events it changes
its internal state apply another event it changes internal state, apply another event, and so on and so on until we get
what is considered the current state. So instead of loading the full state from the database and saying here's my state
in memory, you load the events, apply them, and now I have the current state. So a projection is a function that
constructs our data by replaying events from the event store. The event store is just someplace that I can store the
events immutable and that is that that sounds like a log, right? An appendon immutable log and that's it. So it's just
record these events in an everinccreasing amount. Can never change the past. You don't want to because those are facts.
They happened. It might have been a bug. We might not have, you know, we might have had an off by one error and
shouldn't have sold that last ticket because we were over capacity. That's a bug, but the fact is is is it happened. It
was allowed to happen. It happened. We may need to go and create a compensating event to adjust for that. So it might be
we have to refund their purchase. Um or we might go go in and increase the capacity so it's no longer sort of a problem.
We've checked with the fire department and they're okay with that. Uh and it is exactly like an immutable ledger. And so
for those of you who've ever done accounting systems, I I worked on a billing system for insurance software uh and we
implemented double entry accounting where you never ever change the past. you just created new transactions to And so an
event store is a is a is this place to store and you can store it in a commaepparated file. And actually the jitter
ticket has an implementation of that that stores it in commaepparated file. Um, if your file system is fast enough and
and structured in a way that it's quick to append, then that works great. Um, some file systems have to go and seek to
the end and that can take some time and then you have to append and then that can take some extra time. So, it might not
always be a great place to store it, but you can do that. Uh, you can also obviously store it in a database, but here
now you're not using any of the relational features. It's a single table to a certain extent ever growing um that Now
each event is going to be different in structure, right? So if we look back at at these events, the ticket price changed
has probably the ID for the concert that we're talking about and then the new price and that's it. So it's a tiny event.
rescheduled might be a bit larger because it has uh in addition to the to the identifier for the con concert, it has the
new date and time and when the doors open. So, two or three fields. Um the concert scheduled event itself might be much
larger, right? It's got the artists, you got the openers, it's got the date, the ticket price, the maximum capacity of
tickets, how many pe how many are you limiting purchases for, and a bunch of other information that that it might have.
Uh, and so that event might might be large. And so when you're storing it in a in a table, you are not using a schema
that you normally would, right? You might have, you know, different schemas for for different objects. here all all
objects eventually get stored as events and then those events are widely varying in terms of their size and content uh
and so you probably want a database if you're using a database that can handle that um Postgress and similar databases
allow you to have a column that is just text uh or JSON but if you're you're not generally querying inside of it so
whether you store it as JSON or not is sort of not relevant uh but the point is is you're not using the schema of the
database to define the content which of course is you know is is good and bad but I think in in general uh it's uh the
So to me, this is one of the biggest creating the system. For example, in the concert ticketing system, how many
customers are transferring tickets? We didn't think we needed to know that upfront. And so, you know, we implemented the
the transfer ticket. Uh, and if we were using uh an override state sourced system, we might not know that tickets were
transferred at all. Maybe there's some tracking of it in some transactional thing because maybe there's money in
involved, but maybe not. And maybe all we know is that well, customer C now has B's tickets, but we didn't know that B
originally owned them unless we go look at the payment history. And so sometimes you can recreate some of that history
by looking elsewhere because maybe there were side effects, right? Like payments. Um but maybe you don't have that. You
may also want to know not only just how many customers are doing it, but when are they doing it? Are they doing it the
day before? Does that tell us maybe there's some scalping going on? Right? And so there are all sorts of questions that
that you might not think of at the beginning when you're designing how data gets stored and how this information gets
stored. Uh and you may decide we need to know this and now you only know going forward and you might have to do some
invasive changes and that can that can be really uh that can be really timeconuming uh and effortful to do since they're
all immutable and you never delete events. You never lose information. Now, of course, if you never created the event in
the first place, obviously you you can't uh you you can't retain it. Um which is why when you design events, you
obviously need to at a minimum have the events needed to recreate the state because the state is purely coming from
events. There are some other things that are that are interesting. Whether they're how useful they are is another
question, but you can see the state of the system in the past. And I'll actually uh de demo that. I can say what was
what was the state of the concert a month ago. What events happened after that? Uh and then there are uh different kinds
of projections. So as I mentioned the entity or the aggregate itself is a projection right we we to load into memory we
basically played a bunch of events. the events that we played were specific to that identifier, right? Concert with this
identifier, load only those events and replay them. But sometimes you want information that's across aggregates, right?
I want to find out I need to see all the sales. And so that is a different kind of way of looking at the events. It's a
different projection. And these projections are another huge part of of the event sourcing So I want to give a little
quick run through um uh from a domain driven design tactical patterns point of view just so that when I'm talking about
the different parts of of uh uh the different patterns aggregate and so on Uh so these are the ones that are important
because these are the ones that have to do with persistence right so we've got entities um these are the things that
that have identifier and change over time uh value objects aggregates and repositories so entities are unique right we
identify them through identifiers right so a concert has unique identifier even if the band same band is playing the
same venue three nights in a row they are um they have history, but if you're not doing event sourcing or not specially
writing out an audit trail, you actually kind of lose that history, but you know there was history. You just don't know
what it might have been. Um value objects are descriptors, right? So they're immutable. They don't have a separate
identifier, right? The number 100 is a value object. one value of 100 versus another value of 100, we don't care about
the difference. So these are the things that are often used inside entities to quantify, describe and and measure. So
how many tickets are available, what the ticket And so an aggregate is a consistency boundary. Perhaps it's just one
entity with a bunch of value objects. Or perhaps it's an entity that has other entities uh and then those have value
objects. So you might have two, three, four entities that consists of an aggregate. So a concert might be an aggregate.
All of the tickets purchased transactions maybe you store as a list of those. So you've got basically kind of line items
of of ticket purchases for for the aggregate. Um, and you you need those perhaps to to find out uh am I allowed to buy
more tickets? And so often we refer to the main object that we talk to like concert as the Um, so this is just a diagram
to to show we've got two aggregates here. We've got an order aggregate and we've got a buyer aggregate. Um the buyer
there's just one entity. It has some attributes. Uh the order aggregate actually has uh three objects. Um the aggregate
root which is order uh an address which is a value object and then an order item which is an entity uh but also has
value objects of itself. Uh and so we don't just go in and and modify address. we probably replace it because value
objects are I always think of as these small throwaway things. We can easily recreate them or create new ones and throw
one old ones away. And so if we want to find out uh who placed this order, the only thing we have, the only connection
we have is uh an identifier. And so this is if you've done domain driven design this should be common knowledge of
aggregates refer to other aggregates through their identifier and then the repository it's responsible for storing and
retrieving aggregates. So when I want to load an order um I don't load order items I load an order and then order items
get pulled in with that. And so repositories are used for storing So aggregates to me are still useful although there
are are uh some folks are finding that aggregates are are too rigid um in in the world of event sourcing. But we can
totally use the same idea and the same structure with event sourcing versus uh overwrite state sourcing of our data. So
aggregates combine those those two things. One is how do I get the current data? So how do I project that those events?
So it has a ability to project right. So again fold over or accumulate aggregate over all the events replay them. That's
a projection of data. And then it has uh what's sometimes called the decider the thing that actually makes the decision.
So there might be one method, there might be a dozen methods that are making decisions based on the current state, the
current projection or the current projected state, right? So it's making the decisions of do I generate an event or not
based on the command and the current state. So it's always replay project to get the current state then execute or
attempt to execute a command and then out of that is not a completely new state. It's just here's the little bit that
changed So I want to touch on on some misconceptions or confusions not necessarily misconceptions per se but but often
are sort of conflated. And one is event- driven architecture. Event- driven architecture is much more about how
different systems collaborate and Um, and so I call these events, sometimes they're called public events. I tend to call
them collaboration events because usually they are uh sometimes they're they're almost commands like um but then they're
no longer events, they're really messages. Uh and so all these kind of get get conflated but event- driven architecture
is just how am I organizing multiple systems or multiple parts of a system? How am I comput communicating and
collaborating across these module boundaries? Events in event sourcing are private. Nobody should be looking at those
except projectors and right an aggregate is a special kind of projector, right? It basically loads all the events for
its identifier. Nobody else should be looking at those events because those are are private internal event sourced
events. They may change, right? I may decide, hey, that concert rescheduled event is no longer sufficient because we
needed to store an additional piece of information that we didn't store before. And so I'll I'll now have a different
concert scheduled event. And there were various ways to to to version that and change schemas. Um, but the fact is is
anybody relying on how those events are stored for event sourcing, uh, that's what Konov would call intrusive coupling,
and that's bad. So event- driven architecture, you're designing these events and sometimes they're called domain events.
And the problem with the word domain events is uh often they're used both to talk about event sourced events and also
these integration or or collaboration events. Um, and so I don't use domain events as a term by itself because I need to
communicate is it something private to that aggregate or is it something that I'm explicitly making more public for
collaboration? Uh, so George asked an earlier question about uh uh addresses. Um, we throw them away because they're
easy to create. Uh, we wouldn't reuse them. That's one of the things about value objects is we tend not to reuse them
because there's no way to point to them. They don't have an identifier. If you were picking from a pool of all possible
addresses, which there are systems that do that, right? E-commerce, you might start typing your address and it autofills
it maybe using a Google or some other API, then you have a fixed identifier associated with that address, right? And
then becomes an entity. So CQRS is often associated with event sourcing for good reason, but it is not a requirement.
It's not a requirement either way in the sense that event sourcing does not require you to do CQRS per se. Uh although
it certainly leads you in that direction. And CQS does not require that you use event sourcing. In fact, I've
implemented CQRS without it because what CQS says is we're going to have separate read and write paths, right? All
right, we're going to optimize for for separate read and write paths perhaps because we're heavy writes and we want to
optimize for that and get those written and persisted as quickly as possible and maybe a little bit of a delay what we
often call eventual consistency on the read side. Um or vice versa or both where we have you know a few writes and lots
and lots of reads and so want to optimize for that. uh and we do that with our current systems, right? So it might be
timeconuming to load up a bunch of data because of joins and it's a lot of information and so what we typically do is we
cache those in some way. We might set up an explicit materialized view in a database to do that for us. Um or we might
use an in-memory cache or Reddus or or something else. Um, but we're always trying to optimize for read if that's what
the system is is uh meant for, right? Because if we want to show here are the concerts that available, if we have to go
and search through all of the concerts uh in the database and all the times and all the places and all that kind of
stuff. Well, if we're constantly doing the same thing and that's timeconuming, what do we do is we cache that. and
whether we cach it in memory or in a database, but we're basically restructuring the data because a we don't need all of
it. And uh right because there's stuff that's in inside the concert data like what equipment does a tour need. We don't
need to know that for showing which concerts are available for sale. Um and in fact, we don't want to have to then
filter out ones that that are in the past. So we might even, you know, update that on a on a daily basis, right? We're
so we're optimizing for being able to quickly show which concerts are available, but then they're limited by which ones
have tickets. So maybe we we have some extra work to do there. Um, but we're always doing that kind of thing. All right,
so let's take jitter tics. Um, so this is my uh event source ticketing system. Um, let's take a a quick look at uh the
design. So, let me switch over to here. Not that, but that. So, what we've got It's an aggregate route. It has a couple
of value objects, artist and venue. Uh, it also has tickets remaining, which could also be a value object. There's some
other information that it has. Uh and then we have customer which is a separate aggregate route. Um it may have ticket
orders. Ticket orders have tickets. Uh but they point via the ID to the to the concert so we know which concert you
bought tickets for. And what I have down here are sort of um uh what you might call use cases or user stories uh or
simply tasks. So a promoter or the one who's running the venue would create the concert. Uh they might reschedu it. They
might cancel it. Uh all these kinds of things the promoter does. Uh customers buy tickets. Um and they may transfer
tickets. And then we have views, right? These are the things that would appear on a screen. Um, so we might have the
concert status view that the promoter can look at that tells us information about the events, uh, artists and so on. And
here it's combining two pieces of information. The core information from the concert and then all the information about
sales. And then we have a view for customer. I can look at my uh what tickets do I have for which concerts and I might
have multiple uh events uh concerts that I bought tickets for. So if we look at this from uh and I'm going to use uh a
very event modeling like way of of looking at uh some user interactions. Um if I want to buy a ticket I'm a customer. So
um probably use you know here I'm using a a web app and so it's going to do a get request uh back on the back end it's
do going to do a query for give me all of these concert projections right give me all of the concerts that are available
uh for ticket purchase and we're going to get a read model. So this read model is again right optimized for this
specific use case of presenting concerts that are available to buy and then they want to perform some action like I want
to buy tickets for one of these concerts and so uh we then do a get request to get details about the concert. Right? So
here we didn't have all of the details, right? We may not have even bothered to load up ones that are sold out or
differentiate between that. We just load them all up, at least all the ones in the future. Uh and then we get to so we
query for details of this concert and likely here, you know, we might load up the aggregate uh and then we display it
and it's like how many tickets do you want? and then you click complete purchase. Um, if you implement your system with
reservation like like most large ticket vendors like Ticket Master and Live Nation do uh when there's lots of
contention, you might lease the tickets for a certain amount of time, but our system is meant for smaller venues that
don't do that. Uh, so you complete the purchase, it does a post which generates an event, right? Because I just clicked
the buy, sidest stepping all the payment stuff, assuming that that worked. um we will generate a ticket sold event from
the point of view of the concert. The concert sold a ticket or multiple tickets perhaps. In addition, the customer
purchased tickets. So remember I said commands generate events. Sometimes they generate But when the concert was
scheduled, a concert scheduled event was created that was specifically targeted at that concert aggregate. But here
we're actually doing both because we're we're basically saying in a sense there there's two points of view that we need
to record facts for. We need to record a fact for the concert that some tickets were sold. In addition, we need to uh
record a fact that this customer purchased those tickets. that's done as a transaction, but it's not a cross table
transaction. It's a single table because we're just And then as a result, we do uh uh a query against the the customer
store to find out what the ticket order was. We retrieve that information uh and then we display it. And so from a high
level, one of the things that this event modeling like diagramming gives us is a sense of what do we see on the screen?
What do we need to see on the screen? Right? So intentionally this kind of modeling is intended for user uh based uh
interactions. We see these swim lanes for the different aggregates that are involved and the and then we see the events
that get generated as a result of each command. So this is a command right here. It generate it causes two events to be
generated uh and then those are stored in in the event store. Uh and we see these different green ones are different
views and these are optimized for those use cases. Uh and here we see uh a separate read model. Um this is a projector
that is not associated with an aggregate. It's not looking at a concert with an identifier. It's not looking for a
customer with their identifier. It's looking across all concerts. What were the sales and uh that's a separate
projector. And the way this projector gets generated is basically replaying all the events and then updating things that
it cares about. So everything is always about scanning through events and then accumulating, folding, projecting,
applying, whatever term you you want to use. I like projecting. Um, we now project a certain state. All Uh, actually
before we dive into the code, let's actually look at the application. So, uh, we can see which concerts are available.
Um, this would be the, uh, the listing of available concerts that a customer can purchase. Uh, real system would have
something a bit nicer and a bit more information, but this is pretty much the information you'd want to display. You'd
probably not show the concert ID, but that would be embedded inside of the the thing so that when you click the buy but
buy tickets button, it knows which concert you're talking about. Uh but we have information about the artist, the date,
the time and the and the ticket price. And so we can go ahead uh and and buy tickets. Uh it shows us when it is, how
much it is, how many tickets we want to purchase. We can go ahead and purchase the tickets. And it tells us, right? And
so this is basically the implementation of that diagrammatic flow that we saw before. And so what we can do is we can
look at the events. So let's look at uh our concert events. And let's look at the one for uh the sonic waves. And so
here we see um bottom up the bottom most event is the oldest. The one at the top is the newest. Uh and we see on the
right the current projected state. So all these events happened. This is the projected state right? There are 78 tickets
remaining. Uh this is the show time and this is when the doors open. And so we can look at the individual events. We can
say this was the original event when the concert was scheduled. uh we can see that uh the date was uh December 20th and
the doors were opened at at 7 p.m. So we can see that that's different. How do we know that that is why that's different
is there was a concert schedule a rescheduled event defining the new show date uh time and the and the new doors time.
And then we can look at the tickets sold events. And this tells us there were eight tickets sold and then four and then
two and then one and then two and so on. And so we see the history of these things. We can say well what was it um what
did the state of the system look like before that? So we can time travel. We can say show me the state of this aggregate
at this time period. And so now we see the original what was it like when it was originally scheduled, right? 100
remaining tickets. This is the date and time. Uh and we can say, well, okay, what happened after we applied this one?
Okay, we can see the date and time changed and the doors time changed. And then we can apply Oops. Come on. event gets
applied, we see that the And so this ability is to sort of go back in time and and just see what the state of of the
object was at different points in time is possibly useful. Um, it's certainly useful for for getting an understanding of
how did this entity change over time and seeing what caused it to to change. And we can also look at other projections,
right? Other aggregates from their projected point of view. Whoops, I want to look at uh customer and we'll look at
first customer. So we can see the customer registered right at that point in time. They didn't have any ticket orders.
They placed a couple of ticket orders. So we can say what was their state as of when the first ticket purchased
happened. And then we can look at the state which is now the current state. And so we see all of our ticket orders.
Right? There are two ticket orders. There's one here and one here. uh and other information about the customer has has
not changed. So these are the projections of entities of of in this case of aggregates right so they were we load the
events we rebuild it and we can see how the the state changes um as I mentioned there's a different kind of projection
which is more like I want to see what are the sales and so here we can see the concert sales report and so this is
generated by basically a projector listening for events that it cares about. This one doesn't care about customer
events. It only cares about concert events. Uh, and it might also be that you limit it in time. So, you don't care maybe
about concerts that happened last year. Um, or maybe you want to show monthly reports. And so this projects, right,
basically applies all of the events, all of the the concert events, so including reschedules, uh, all the ticket sales.
And basically, we see the Sonic Waves is is selling, nobody else is selling. Hopefully there's a good reason for that.
Um, and so we can see that that uh information. If we decide that we want to see additional information like sort of
what is the rate of sales, right? Uh we can write another projector or we can maybe say we're going to replace this one
with monthly reports and so throw away the projector and write another one. And so the projectors are are are very much
how do I want to look at the data in a way that's convenient for for viewing. And it might not just be for viewing on a
screen. Often this is your integration point. Right? So remember I said before other parts of your system and other
systems should certainly not be looking at the events the raw internal event sourced events. That's a no no. But
projections would explicitly be for sharing. So maybe another system needs to see some information about the current
state of of things. And so you can project that onto a separate table that then would be explicitly shared. And that's
your your contract to share it. And you know that it's being shared and you know that nobody's going to muck with it.
The only thing that writes to it is the projector. Everybody else Um, I'll get to your question in a second, Marcus. Uh,
so you can have all sorts of different projections. Um, when you create new ones, what's nice about it is you basically
start it up. It goes through all the events. Maybe it takes a little bit of time to get its initial projection because
maybe it has to process a few thousand events. Uh, but now you got a new projection. You don't like it, you throw it
away. you want to modify it, you throw it away and create a new one or basically just create a new one and deprecate the
old one. And so you have all these different ways of viewing the data. And again, you can say, hey, we want to see this.
Well, we've got all the events that created the state, so we &gt;&gt; Uh so Mark has asked about um would I use event
sourcing uh for every app? Um it truly is like I am allowing people to edit data directly with little validation and and
almost no business rules in which case I would just codegenerate that thing um but if there's any non-trivial uh state
changing things right non-trivial rules non-trivial you know and where I would be applying domain driven design Um, I
would my default is now event sourcing. Not to mean I won't do something else, but that's my default. If I'm integrating
with there's already a bunch, you know, 100 database relational tables that we need to interact with and access, then I
probably wouldn't. Um, on the other hand, you can do this on a per aggregate basis, right? And so if you have a system
and there's, you know, 25 aggregates, there may only be five aggregates where you ever think you'll ever care about
events and so each aggregate can be stored using what's best for it. Uh so asks um processing events and project them in
real time is is too heavy. So uh this is often a question about performance and so I'm going to group it under the the
general performance. This projection for example um right now is actually running through all the events every time I
view it. Uh that's probably not the way you want to do it. Um but it might be good for prototyping. But why? But there's
no reason to do that. You can store the projection. It's just data. And so that the projection itself, even if it's only
for viewing, you store it in a database table just like you do anything else in traditional ways of storing information.
In fact, that's the current code that I'm working on on stream is storing this stuff in a database. So instead of having
to process through a 100, a,000, 10,000 events, you do that once when it when it's first created and then it's now
incremental. As events get generated by changes in other parts of the system, projectors become listeners to those
events and then they just update incrementally. They load all the concerts, apply the new event, maybe only one or two
new events, and then do an update on the database. And that's super fast. Um, and so this idea of you and sometimes this
is called a snapshot, right? So the idea of we only have to now once we calculate the current projection, we now only
have to calculate as as the new events come in and that's generally really fast because it's loading a few K of data
applying it in memory which takes really no time and then right you're your cost is basically persisting loading some
rows from a database and saving some rows to a database. there are no joins involved. So the database is going to be
really quick. Um and so all your your overhead is is just loading loading and storing and all the projectors uh are
listening for for these events and only applying the ones they care about. Right? So customers registering customers
changing their email. The concert sales report could care less and so it doesn't change. Uh so Mark asks recommendations
for using event sourcing for client sending data from time to time to a server. Uh can you elaborate on sending data and
feel free to unmute if you'd rather do that? &gt;&gt; Sure. &gt;&gt; Uh thank you very much for uh picking my question.
Um I'm thinking about uh a client maybe on a mobile phone. uh where you can enter your data until uh the data processing
is finished and then you send it off to the backend server. &gt;&gt; So it's doing some processing locally and then
sending something. &gt;&gt; Exactly. I mean that from the backend point of view that's very credike. &gt;&gt; Mhm.
&gt;&gt; Right. Because it's not executing a command. It's just here's some new data. Um I mean you could use event
sourcing for that and just say you know let's say they were measuring something here's the square footage up update. You
could do that. um probably not the optimal fit because one of the things that event sourcing kind of leverages is the
idea of a little bit about why or more than just you know let's say I'm measuring an apartment to move move into and and
I measure the square footage and all the measurements are done locally and we just update something on the back end and
so it's like okay square footage updated it feels to me like that's not um leveraging what what event sourcing gives us
which is a bit more about business important events. So things like customers registering, buying tickets where the
decisions are being made on on the back end is probably uh more in line with with the strengths of of event sourcing. Um
and so just updating data. Uh so uh someone in another context asked about sort of uh IoT systems and they're just
sending new temperatures. It's like, well, that's probably not useful because really we want to know the results of
decisions that are made on the back end as opposed to just new data. So, you could use event sourcing. It the events
wouldn't be very interesting. Not to say you you uh don't get advantages from the other aspects. So um being able to uh
have different projections of views um you get some of that you get some of the the things around uh optimistic
concurrency. Um but for me that would be a weaker argument to go event sourcing than to just why am I not just storing
this data in a table. &gt;&gt; Thank you. Yeah. Yeah. So Fran says uh event sourcing makes sense when you can model user
intent, right? So there's some actor, it might be another system, uh it might be a user that's taking action based on
what they see on the screen. They're taking action. Uh and then the back ends is deciding whether that action is allowed
or not. Um and I agree that that very much domain driven design. Uh and and getting the events event storming helps you
get those surface those events from the business. What does the business care about? Um and so I think that and those
are the kinds of systems I generally work with which is why I tend towards my default now being event sourcing. Uh but
if I come to a data only thing then I I might I might rethink that. And again right you don't have to convert your
entire system into event source. You can say if you've already got a domain driven design tactical patterns and you're
already using aggregates and repositories your repository is is your place to say I'm not going to store this aggregate
using a standard basically state sourced uh you know repository. I'm going to replace it, unplug it and plug in. And not
that it's necessarily that simple, but since the aggregate is a boundary, you can then say I'm going to store this
aggregate using event source. All right. So now let's look at the code. Uh so let me minimize that. Um so the first
thing you need to figure out is your events or one of the first things you need to figure out um is your events. Uh and
so here this is the hierarchy of events for jitter ticket. Um so there's a base event class. Uh and all events need to
have an event sequence, right? So they need to have a sequence so that when we rebuild it, we rebuild it in the correct
order. Order matters. Uh then we've got sort of a division between the aggregates that we're storing. So we have a whole
bunch of uh whole bunch we have two here events associated with customer event. And so therefore because it's a customer
it has a customer ID. Similarly for concert event it has a concert ID. Uh and then each event has different details
right so tickets purchase has a bunch of other details. Connections to some ticket order and concert ID. Uh concert
scheduled has a bunch of a bunch of things. Tickets sold doesn't have as much. Um, but we've got this this hierarchy uh
of of events. So, all events are going to have an event sequence. They're actually going to have in addition uh a global
event sequence because that way for things like for non-agregate projectors like the concert sales summary, uh you want
to be able to say I have, you know, what was my checkpoint? The last time I was updated was at this global event
sequence. And then when it starts up again, maybe after a restart or it got another event, it can say, "Have I seen this
event?" It's global event sequence is larger, so I haven't seen it yet. Let me process it and then update my checkpoint.
Yeah. So, so, so George uh Menz uh mentions um distributed with with sites that could be offline. Uh and so there's a
whole interesting area of of conflict resolution. This is something I'm I'm I'm looking at. uh there's this area of what
are called convergent uh or conflict free replicated data types and there's convergent there's merging there's uh other
things that you can do that if I one system saw events up to a certain point and another system saw a different event
can I just merge those right and we see this with our version control systems right sometimes the merges are are like
totally fine there's nothing they don't you know this one changed data for this aggregate this one changed data for this
aggregate they don't have anything to do with each other. They're independent. We can just merge those automatically. Uh
and CRDTs and so on um are ways of defining you know what is basically an ever growing list and ways of defining to to
handle those merges automatically which helps with bringing everybody into sync when you have a distributed system. So
that's a whole interesting area. I'm not going to go much much deeper than that. Uh so Husim asks about a different
event store table for subset of aggregates. Um I mean now you're starting to get into some optimization issues which
which I'll cover uh in a bit but I want to get into a little bit more of the code. So one of the most important things
is you have some kind of event store and an event store instead of saving an aggregate as a whole it's saving basically
what are the events that were just generated right so if we look at our use case let's start there right we've got a use
case what is the use case purchase tickets. So if we want to buy tickets, we need a concert ID. Who's buying the tickets
and how many are they buying? Again, payment stuff all aside, assuming that that that goes through fine. So we grab the
customer and then we grab the the concert and we basically uh on the concert aggregate we say sell tickets to. And so
behind the scenes when we do this, it doesn't just update the state of that object in memory. It generates an event and
the event that it generates is ticket sold and it incues it. So anytime an event gets generated and so this is now
getting into implementation details when we execute a command and it succeeds we incue it. And so all event sourced
aggregates have in common two things. One is in quuing the events and two is applying those events. So in quuing does
does both actually does two things. It saves the event because we're going to need to store it in our persistence and So
any aggregate events invent source aggregate is therefore going to have kind of four types of methods. Two you probably
already have right you've got your queries and commands right commands to execute things queries Then you have your
event application. Pretty much your apply method is going to be where the action happens. Now remember this is applying
facts. So there's no decisions here. This there should be like no business logic here. This is just saying given an
event that was concert scheduled, we're going to update our internal fields. For concert rescheduled, we're just going
to update a couple of fields. For tickets sold, we're going to basically just update the available ticket count. No
logic here about decision-making. the decision that was already done when it generated the event. Right? So when we sold
the ticket, we generated the event, we incued it, which again does two things, holds on to it, what's called uncommitted
events because we haven't committed it to persistence yet. And then we apply it so that our internal object is now up to
date in terms of its state. Right? And so at some point then in our use case, right, it's going to basically save it.
And so what happens with the save is it basically says, hey, give me your uncommitted events and then I'm basically
going to go and persist those uncommitted events. Right? So an action came in, we generated events, applied it to
itself, saved it, and save says what were the new events since the last time you were loaded, right? So it's basically
the I'm just saving the diff persist that uh and then and then we're done. And of course at that point uh we would
notify our projectors. Hey, go go go update here the new events uh since And so from a testing standpoint, I tend to
then divide my tests into these two sections. Commands generate events. Events project state. So given a concert
scheduled sorry a concert uh scheduled event I want to make sure that given this concert scheduled event that when I
project or reconstitute that those events into getting a concert object and that if it rescheduled so here I'm basically
scheduling it and then rescheduling it. And so my tests are dealing with and working with events. Create a couple events
basically apply them to reconstitute my domain object and then check that it actually did that. So um my tests are
separating events update state from commands generate events. And so in my commands generate events I can focus on the
deciding the decision the business rules. Right? This was all about did I update the state correctly, right? The
internal state of the object. These are the ones that are testing what I consider the behavior. And so now we can just
focus on the behavior, right? So reschedule. And there's not a lot of behavior here. I don't have a lot of rules around
this. In fact, I actually have no rules around this. um given the original concert scheduled when I reschedule it. So
now I'm executing a command I expected to generate a single event. So I can literally do that. I expect you to have
generated a single event. Similarly for purchase tickets sold generate the event call a method invoking behavior and I
expect it to generate a ticket sold event. Now, these tests are a little ver more verbose than I would like. And so, one
of the things uh I've been working on is creating a nicer DSL for this lends itself very much to it because there's a
lot of noise in here when when there's only a few things I care about. And so, uh you can look at the uh code code base
for that. Uh so, we saw the event hierarchy. You can in Java if I started out doing this as records. Um, but records
can't inherit from storage from from parent classes. And so it's kind of messy. Uh, so I went It's unfortunate because
with records in Java, you get some nice deconstruction patterns. Um, with Java classes, you don't. But yeah, it's a it's
all all things are trade-offs, right? Uh, so I did the code walk through. Okay, so that's the bulk of this presentation
and now I'm going to talk about some some little topics. Um, if you have to drop off, no worries, the recording will be
available. Go to ted.devtalks. Uh, but I want to talk about a few things. One is versioning, right? Your events, just
like schemas in our databases, sometimes we add new functionality and can use what we have. Sometimes we need to store
new data. Uh and so literally there is a book uh that consists of some of these patterns by Greg Young uh no relation uh
who actually was the first who popularized CQRS and coined the term and and event sourcing. And so there's a bunch of
ways you can do this. Um I won't go into details but there's there's uh ways you can do this. Uh a lot of it's just
about you're changing the content of events. Are they sort of Uh I sort of already mentioned CQS, right? Separated data
models and CQS uh again fits very nicely with that because you've got your write API. Uh and it's it's just emitting
events and writing those out and that's all it's doing. Uh and then your read API you're reading either from the
aggregates or from projections. And so you may have uh specialized places to store these projections. Maybe they're just
a table in a database. Maybe they're in memory. Who knows? But it's optimized for exactly what you need when you want to
look at it. Uh so I showed my little diagram of event modeling. Event modeling is a whole thing. Again, really useful if
you have basically task based UIs, right? Where you're going to present information. Uh it's going to generate a
command. The command generates events results in an updated view of current state. We show that and then we again
execute, generate an event, update a read view and so on. And so this kind of diagram is really nice uh especially with
the color-coded little post-it kind of things. You can really see what's what's going on, how does this get where does
this get the Uh, so this is this is courtesy of of uh uh Eve Golvin on LinkedIn. He writes a lot about this stuff. I've
learned a lot from him. He was also the one who mentioned the CRDT stuff that I've been looking into. So recommend you
follow him. So that's it. That's event sourcing from scratch. I hope that it gave you at least a taste uh of event
sourcing and and what it can do. and and I really feel like it's my default now. Um the mind shift is the hardest part
to change. Right? If you look at the code for this codebase and uh the links are are uh on a talks page, um it's not
that difficult. The implementation isn't that complicated. The biggest part for me was the shift to I changed I executed
a command and now the state is immediately changed sort of in one big thing. Now we're splitting that into two parts. Um
and the idea that you don't look in the database the event uh store you look at the projections if you want to look at
what the current state of things are or if you want to aggregate information. Uh Mark I'll um uh when I post this
presentation I'll have links to uh EES go 11. Uh it's basically go 11. Uh uh you can look for him but I'll I'll post all
details and links and stuff like that uh on on the talk page. Um so you ask how do we handle concurrency command
maintain a unique constraint for usernames. Um so for something like usernames that's part of the decider right there's
kind of no difference in your decision. It's just where you're getting the data from. So you would likely have a special
projection that's just usernames, just usernames. And then you can you might even have that in memory if if if it's
something that happens often enough. And so you basically as part of your uh uh use case, right? The first thing you do
and it's kind of part of validation is you go and see is there that username in the database. Now there's obviously some
concurrency race conditions that are that are potentially there. Um but the projection will always know what was the
last event it saw, right? It's the global event sequence and so it knows what was the last one it saw and you can say
are we up to date uh when we try to try to write it out. Um and so all projections uh are going to be serialized in one
way. They may be just stored in memory likely you're going to serialize or store persist if that's what you mean by
serialized uh your projections right so my sales summary projector currently is an in-memory version uh the on the the
one I'm working on on my live stream is actually storing in a database and so what what's nice about this is it gives
you that control you you know most traditional systems have this as well for things you need really quickly might have
an in-memory cache, right, that you use often that you need quick access to. So, it might be something that you have in
memory. And if it's not a lot of usernames, then you might just store in memory because it's easy. When the system
starts up, it's going to replay all the events looking for customer registered events because that's where the username
gets defined and then accumulating those. If there's a lot of those, it might take some time. So, you might just write
it out to to a table um or to another database, maybe like a Reddus if if that's faster. Although I'm a big believer in
in sort of use Postgress everywhere. And so again, because we're we're not storing the latest state in the database in
traditional relational structures, we can't and don't rely on database constraints to enforce things like unique emails
or unique identifiers. So we need another way to to do that. Um, but with event sourcing, you basically project, here's
all your usernames. You project, here's all my email addresses. Uh, and then you can you can optimize for that. What
other questions do you all have? And if you need to go, just drop off. Uh, I'll send out a link to the recording and
information page, but you can always go to ted.devtalks. Uh, so I'll mention performance just a little bit more detail.
it's not an issue. If it is an issue, there are ways around it. Um, snapshotting so you don't have to process 10,000
events. Uh, but businesses tend to have a natural time period, right? Like in accounting, we used to close the books.
Why did we close the books? So that we didn't have to sum over all the transactions for the entire year. We close them
quarterly or monthly. Uh, and then we basically now store the summaries for that month and we don't need to look at the
transactions again unless we find something wrong in which case we can go back to the transaction. Same idea here. Any
other questions or or thoughts? All right. Then thank you so much for for uh coming by and and watching and asking good
questions. Really appreciate it. Um as I mentioned, the recording will be available uh probably later today. Um slides
and links to stuff uh will be on the site. So if you go to ted.devtalks, uh you'll see that. Um, and as I mentioned, if
you're if you're interested in watching me further code some of this stuff and introduce other projectors and so on, I
do that on my live coding stream, uh, jittered.stream. Uh, if you're not in my Discord, go find out about it. Uh, we
talk about this stuff. We have book clubs and and other such uh, community kinds of things that uh, I think are really
good. Um, just go to ted.dev about and you'll see all the information there. So that's it. Thank you so much for for
attending and and
