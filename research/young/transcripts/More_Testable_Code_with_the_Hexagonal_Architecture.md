# More Testable Code with the Hexagonal Architecture

**Video URL:** https://www.youtube.com/watch?v=8fp5GR4jilM

---

## Transcript

hey there everyone and welcome to today's webinar so good morning good afternoon good evening depending on where you are
turn on my webcam so you can see me and so I can say hi so today's webinar is packed full of information and I hope it's
of use to you and so as you may know my name is Ted young I am a Java trainer and technical coach and I do a lot of
teaching of not just Java the language but also had a structure code and this webinar came out of a presentation I gave
a couple weeks ago at a jul 29 and it was popular enough that people were like oh I wish I could have seen it but I was
at something else or I be great if I could have a colleague see it so that's why I'm putting on this webinar so I'm
giving it today and I'm also going to give it again in September and this also forms a large part of an online course
that I'm putting together so this sort of forms the foundation of that all right so let's let's get started so go ahead
and type in the chat how you've heard about this webinar whether it was a colleague or you saw it on Twitter or maybe
you heard about it on an email list go ahead and type that yes and thank you to my chrizzy for telling other folks about
it so one thing I wanted to point out is that there's a slight delay in the time that I say something and you respond so
if it seems like I'm taking a little bit of time to respond that's just the network delays and oh great yes Jeff from
exon awesome oh cool alright so some folks also from from agile 20:19 great okay so in general I'd like you to hold
questions to the end if you can but if you feel like you're gonna be lost for the rest of the webinar if you don't get a
certain piece clarified then go ahead and ask your question so I'll have some time a little bit of time to hold
questions at the end I've timed this webinar to be about a fifty-five minutes and so there's not a lot of time for
Q&amp;A if you've only got an hour scheduled but I will actually stick around until all the questions are answered and
however long that takes so I'm curious go ahead and type in the chat what you were current programming language that
you're working in is and the reason I asked that is while the code samples I'm giving here are in Java I believe and
have actually applied this architecture to other languages such as JavaScript and PHP I've worked with in some clients
who are doing that yeah and all right so you've probably seen this kind of architecture diagram what's sometimes
referred to as the vertically layered architecture or sometimes also referred to as the cake architecture because it's
got layers and built upon layer is built upon layers the problem with this diagram is first of all are all the layers
necessary at all times are the layers of equal importance and from my experience having the database that the bottom
tends to get people thinking about the database first when they're designing their applications and this will cause a
number of problems because it means you are database centric instead of business centric and for me one of the most
important things is getting the the business logic that you need done and getting that the focus especially in an
object-oriented language like Java and c-sharp you want to be able to write good oo code but if you're sort of having
the database forced you to do things then you may not end up in having as good oh oh code as you could otherwise and so
I saw this this comic and it's it's sometimes a little bit scary about like well okay we have all these layers what do
we put in them how do they relate to each other I no longer know what to call some of these layers but even in the
simplified diagram the DB is at the bottom which is kind of kind of amusing so one thing in many years ago we learned
this idea in coming from agile is this idea of implementing third in vertical slices so this gave us the idea of if we
want to implement a small feature or even part of if a feature we would probably have to slice the thing vertically and
this is sort of along with the vertical architecture basically probably hitting most of the layers but not always and
they're not always the same size in each layer and so you know we keep adding features and and doing but what that hasn'
t helped us with is the potential for coupling across these implementations so if we removed one of those features
because maybe we did some experiments and found that we had to rework it did we unintentionally cause code and the other
features to be affected and so we'll see that hexagonal architecture can can help a bit with that the other problem is
that it can lead to organizing your code according to the vertical architecture and every time I teach this I always
sort of say you know show show hands if you've seen this architecture so type in a chat if you've seen architecture and
your code reflected in this way where you've got a package for controllers and a package for models and a package for
services it can make it very difficult to find out where things are and where things relating to a certain feature are
so let's look at hexagonal architecture so it all started with the infamous hexagon and it was good Alastor Khobar
coburn one of the original Angelus folks who really gave me some of my first guidance in some of his early papers and
then in the mid 90s about how to design good oo and I had I had just been starting with Java at the time and coming from
of all things visual basic and really struggling with with just what is good oh oh and so some of the early coburn
papers really helped me out with that and so Alistair came up with this pattern which he originally called ports and
adapters and then which originally I should called hexagonal but then changed it to ports and adapters when he clarified
the use of adapters between the inside and the outside of the heck is gone and this quote from from the pattern I think
is really an interesting read so I'll let you read this for a bit and then we'll talk about why I think so I think there
are two key parts here one is that this idea which I think is still not widely recognized this idea that you can drive
the core of your application equally by sort of its natural use by users and other programs that today that would be
other api's as well as automated tests and the other part that we can develop and test things in isolation from the the
runtime implementations and I think both of those are amazing that that still holds up today and so I I when I was
researching for this presentation a few months ago I read this over and I'm like wow this is this is really awesome that
it still applies today and I wish more people would read it so this was one of his original diagrams from the original
write-up that that coburn created and so you can see here he's got this idea of two hexagons this core thing in the
middle called application and then this outer one which is or the boundary between the inner think between the inner
part and and the outside world and yeah there's this this left-right asymmetry and we'll actually look at that so one
problem that I had with with reading his original write-up is it wasn't quite detailed enough and I found that that it
took me years to figure out all the the nooks and crannies and details of how to get this right and that's why I've been
really talking about it a lot because I'm because I feel like I finally got it so as I mentioned I actually prefer the
the name hex hexagonal architecture over ports and adapters the reason why is because I think ports and adapters focuses
a bit too much on just the boundary and I think that the core or center part of the hexagon basically the inside is
actually also important and I think now that the main driven design has become somewhat popular and known and I'll talk
a bit more about that it works really really well with the hexagonal architecture so we've got the inside which is the
important business bits and then we've got the outside and so that's sort of the way we look at the hexagonal
architecture there's a lot of the stuff on the inside and we'll dive into that and then there's things on the outside
that we need in order to interact with the rest of the world before we dive more into that there's an important question
that that comes up which is do we draw the diagram flat-topped or pointy topped and so I use pointy top because first of
all I want to remove this idea of the ability to sort of stack these things vertically because I think we got into
trouble with that with a vertical architecture the other thing is I really like that the left-right symmetry is much
more pronounced on the pointy top so I go with the pointy top and let's look at the things in the outside world and
they're basically alistair talks about two two types of things one is coming in from the left side or the triggers or
sometimes called the driving use cases and so these are the things that are triggered by actions from people clicking on
a button on a UI or maybe sending a text message on a phone app or some message coming in from a message system and then
things happen on the inside and then maybe or maybe not something happens on the outside and so these are the driven
these are sort of also called secondary things and these are outcomes that might be persisted to a database or further
events generated to send to some other system so on the left you might have a button being clicked some processing
inside that that is all the business processing and then maybe triggers the sending of a message to a shipment system on
the outside and what's nice is that this lends itself very well to some of the event driven events sourced kinds of
systems not quite event source but more more the event driven that is pretty popular in a domain driven design community
so the code and sort of the architecture that I've been using to that'll you be using to talk about this comes from a
product that I've been working on called kid money manager I've been live coding it you can grab the the source code it'
s open source you can look at some of the early videos as they're up on YouTube basically I developed this live on
twitch and so let me talk a little bit about the the product and so here we can see two two different user interfaces
that interact with the system and so the idea is this is something that I wanna that I'm using with my son to keep track
of how much money he has since he's only 14 you can't have his own bank account and debit card and so if he you know if
we're at a store and you decide he wants to buy some Haribo mini frogs candy then it used to be where I'd have to write
on scraps of paper okay he spent 2 dollars and 50 cents or if we've returned some bottles for recycling I'd have to
scribble down that okay he got you know eight dollars for that and that Matt became messy I created a spreadsheet but
then I was a bottleneck for for monitoring all the transactions I said alright this is a great project to to not only
because it's useful but also to demonstrate some coding techniques like this architecture so on the left side we've got
the web UI and on the right side it's actually not an app is actually just text messaging and that happens to work
really well because you basically you know what the wait for an app to open and connect plus I don't have to write both
Android and iOS apps that's cuz that's the application the kid money manager application so the overall architecture
that looks something like this in the context of hexagonal architecture we've got the core domain in the center that is
handling all the business logic and then we've got things on the upper left which are the incoming or driving parts of
the application a web user interface in the SMS text messaging so we'll look at those first and then on the lower right
the lower right and the right we've got the secondary things which is how do we store the data and what about
communicating outwards to other services and we'll look more deeply at the at the port's when we get to that so I want
to mention separation of concerns and it there's sort of a quote that always comes to mind that that's almost exactly
like this separation of concerns is a matter about which a great deal is said and very little done the original quote is
not AB a separation of concerns it's about the weather talking about the weather in New England but no matter whenever I
hear talk folks talk about separation concerns this quote comes to mind because it's like okay yes I know separation of
concerns is important but what do we do about it how do we separate the concerns which concerns should be separated
things like that and that's one of the things I like about the hexagonal architecture is I feel like it's prescriptive
enough to give you those guidelines that are useful so the idea is we want to separate infrastructure and the outside
world from our business logic and so if we sort of look at it diagrammatically it looks something like this right we've
got our outside world stuff on the left our infrastructure stuff on the right and maybe we were sitting using a
framework at the bottom so some examples of that is listening to the outside world it might be a console based app that'
s possible or an HTTP API or a web UI or messaging and that's things coming in from the outside world talking to
infrastructure is database network files of that typical thing and your frameworks spring the the java ee or now jakarta
ee or micronaut and so all of these things are in the outside world and we want to keep those isolated from from the
core domain because in the core domain we want to be domain driven we want to have domain as the focus of our
application and that means we want to be able to write the code and tests that are only thinking about what are the
policies rules complex things that we want to want to do inside the business and so if you're not already familiar with
domain driven design this was the the book that started at all written by Eric Evans and the subtitles importance
tackling complexity in the heart of software so this is dealing with when you have complex business applications for and
when I say business you can substitute complex tools right anything that is basically having complex rules and
interactions is going to be something that that domain driven design is good for and so your domain op may not be the
business it may actually be internal development tools or other internal tools that are not necessarily directly
connected to your business so the four patterns that I just want to quickly go over just in case you you haven't been
exposed to much to domain driven design are entities value objects aggregates and repositories and so we'll see that
entities and value objects work well together as part of aggregates and then those get stored and accessed with
repositories and so again this is not a webinar about domain driven design but I just want to make sure that that the
language is clear so entities are the typical things that we work with that hold information maybe about an employee
maybe about a meal order that has a unique identity that is separate from the thing that the information that it's
holding and so for example if you place an order at a um you know fast-food place that order needs to have a unique
identifier so you can tell apart the different orders and this this became very clear to me when I was in Washington for
the agile conference I ordered a meal from from the Shake Shack over its mobile app and when I got there and was waiting
around they called out the name Ted your orders here and so I was walking up and at the same time this other guy was
walking up and we're sort of looking into each other and it turns out his name was Ted also not only that so we looked
we appeared inside the bag to see if we could tell the order apart based on what we'd actually ordered and he ordered
something very very similar to mine so we couldn't tell the difference between that luckily he was holding a pager that
had a a number on it and that number matched what was on the slip so that was the yueqin unique identifier that
identified the meal and showed that it would belong to the other Ted and not me so identity is separate from the
contents because sometimes the contents are the same whereas value objects are defined by their attributes so the
typical examples are zip codes right nine four four or four or the zip code I live in is very different and is unique
from another zip code one triple o three which would be in New York City and so you don't change those because they are
defined by by sort of their intrinsic properties colors are another example based on their RGB values or the states of
things like the States or something in a process now an aggregate is a group of entities and value objects so entities
usually have value objects so you might have a person that has an email address that's a value object and a zip code
that's a value object and then the bunch of entities are grouped together into an aggregate so you might have an order
for that meal consisting of individual line items and all those are grouped together and managed by the the aggregate
what's called aggregate route so in this case it would be the meal order to which you add those items and again there's
a lot of detail to aggregates and entities and so on that there are great references for that finally the repository
which is used for storing and retrieving the aggregates because you got to find them at some point and you got to store
them at some point you may not need to store them for long so the persistence mechanism can be different but this is the
pattern of the repository you're almost treating it as if it were just some collection that you could search over so the
idea here is that this is in the language talks in the language of the domain so the things you're storing the
repository would be things like meal order or account and not how it's stored in a database or some remote system so
we'll derive it deeper into the repository later on so an example of what might be in the core domain this comes from my
kid money manager application is an account savings goal a phone number which would be a value object the role whether
it's the kid or the parent because my kid being able to deposit money into an his own account that's not allowed so role
is also a value object transactions and user profiles so those are all things in the core domain and those do not then
reference anything in the outside world so what we get from this isolation of separating the core domain from the
outside world is again as Alistair said we can develop and test it in isolation from the runtime components and that
means our tests can run really quickly very reliably without a lot of flakiness due to things outside of our CPU and RAM
and so this fits very well with Michael feathers set of unit testing rules that comes from 2005 because I see a lot of
tests and systems when I when I go visit clients where their unit tests are not unit tests because they talk to a
database or they communicate across the network that seems harmless but that's still susceptible to outside influence
that you can't control or touches the filesystem and again that that is the cause for slow and or unreliable tests so
the principle then is that tests must be isolated and so there are techniques to isolate them so not only from the
outside world but what do you put in place of the outside world is the whole area of test doubles and I'll talk about a
couple of those but by test doubles I mean what are called fakes dummies stubs mocks and spies we'll look at a couple of
those in a bit so back to the architecture let's let's zoom in then on the web user interface and so the important thing
here is that the adapters are helping shield us from changes in the outside world so things an outside world change
often and are usually not under our direct control and so the adapters allow us to buffer and with Eric Evans and domain
driven design calls an anti corruption layer so the adapters provide that that separation between your core domain and
things in the outside world so we've got a person communicating to the application through a web UI adapter and so they
might want to do things like look at what's in my account or deposit some money in the account and so you probably have
something in your core domain that that is a POJO and I'm using the strict original definition of pojo so also called
cocoa in c-sharp so you may not you may have heard the term to refer to things like that has setters and getters and are
used for transferring information but that's actually not the original use POJO is our original ooo business logic
inside of an object so that's also called a domain object and so it has not setters and getters but it has commands and
queries and that's you know how we send messages from one object to the other so in this case we've got a couple of
commands to deposit or spend and a query to ask the account hey what's what's your current balance now the problem is if
we want to take this domain object and send some of the information to the outside world if we're using a framework like
spring that leverages a tool called Jackson and so what Jackson is looking for is how to how to translate the
information from an object into JSON that's kind of the typical thing or to be used by an MVC template engine like
timely if you're familiar with that from spring and so if you look at the highlighted area if Jackson tries to examine
account and saying hey Jackson knows how to look for properties based on getters and setters it's only gonna find one
and it's going to be its ID which we may not even want to expose to the outside world but it's not going to find a
balance because it doesn't form the patterns of what Jackson is looking for in terms of getters and setters and so this
leads us to there's also tightly couples account to the outside world which we may not want to do so we've got two
problems of we don't necessarily want to expose everything in account to the outside world and we don't want to you know
adapt the account object to you know work well with Jackson we want some separation there so this leads us to a rule I
have which is domain objects never leave and so that means that the domain objects only live inside of that inner
hexagon now when I say never that's a guideline there are some cases where you might be able to get away with it such as
for storing in repositories but in general I found this rule to be really helpful both to to keep the isolation barrier
up as well as make testing easier so if domain objects can't leave then what can and so the short answer is a special
type of object a data carrying object called DTO or data transfer object and in Java these are Java beans and again I'm
using the original defined definition of Java being which is a thing that has setters and getters on it and doesn't
really have any business logic in it it may have some transformation logic to move to and from domain objects but for
the rest of this webinar and if you ever talk to me pojos are my domain objects with you know good Oh practices and Java
beans or things that are just data carrying things that have setters and getters and you may talk to people who use the
opposite and I will say they are wrong and that's a hill I'm gonna die on but first before we can figure out how to use
the DTO as these data transfer objects we need to look at the adapters and so the goal here is to reduce coupling
between the outside world and your core domain so this is what a data transfer object might look like it's got some
private properties and then setters and jeder getters which are either generated by your IDE or in Java land by a tool
called Lombok and that's cool we don't really care about a lot of this code it's basically just for carrying the data
across that boundary and so now that we have that we can see that instead of transporting the account outside of our
core domain we transform it to an account view in this case and then Jackson can happily do get ID and get balance on it
transform that to JSON and and send it out now adapters are not just single classes as purse or the the design pattern
the role here is actually a set of classes so it includes any controllers for the web UI or for the SMS text messaging
interface as well as any DT O's that need to be used to transform the objects from our core domain and in fact sometimes
you're gonna have a single DTO carrying information from an entire aggregate right so from entire set of entities and
that's fine so the adapter responsibilities are basically these we're gonna when stuff comes in we want to do validation
there as much as possible and so that's the point where we're converting the JSON or text from a web UI into our domain
objects and that allows us to do the validation and and constraint checking on things that way when we're converting
strings to objects and strings to value objects we're no longer checking to see if they're okay everywhere in in our
code once we've created our domain objects we can be pretty sure that they're pretty valid maybe not completely so but
as much as possible then we're gonna convert so at that's part of converting it to the main object we may send it to
some service that is basically cut you know cross-cutting basically behavior that cuts across multiple entities so we
might have a service and then we're probably going to convert some resulting domain object back to or set of domain
objects back to a dto and then that DT of the outside world and this is really key right this separation is is I found
if you really think about the separation it it it makes a big difference in what your code looks like I know in in my
code when I look at where I've had I've had problems it's usually because I haven't had that good separation so if we
take a quick look at another example with the SMS text messaging it has its own adaptor because the needs of translating
and transforming information from an eczema SMS text message is very different from dealing with the web UI and so I
have another rule which is an adapter per communication mechanism you may further subdivide that into an adapter per
sort of feature or use case and or Alistair Coburn's original pattern talked about this idea of use cases people don't
kind of talk about use case as much anymore so maybe it's more of like features and that depends on the size size of the
adapter and so we end up with the two adapters here they're sharing the service because the service is inside of our
domain but what we want to do is also have separation between the adapters so there's another dependency rule which is
adapters don't depend on adapters and so this rule is in place so that you can basically unplug or plug in new adapters
at any time without worrying that you're going to affect another adapter and so this helps keep things isolated and you
want to keep things small and isolated so it makes it easy to work with and we'll see also makes it easy to test if
there is shared code between them then you can basically create an adapter layer that that has that and that it would be
in place for sharing among different adapters and I'll show you a couple of cases of that so adapters don't depend on
other adapters and that makes actually testing adapters not only easier not only necessary but but easier because they'
re independent so we want these adapters to be testable but what we want is to test them in isolation right that's one
of principles and so to test an adapter we don't need access to the core domain and because we already have good tests
and maybe even we did it using TDD to develop that core domain and so now when we sort of want to create an adapter to
plug in we want to make it testable and so we can test them in isolation so if we look at this example of the
interaction for the SMS text messaging we can see that there's some parsing that needs to happen right so if I say
deposit 13 bottle recycling the system the kid money manager needs to interpret that as depositing 13 dollars and zero
cents and putting in a transaction where the source of that money was bottle recycling and someone we for spend and
similarly for goals at these so it needs to do some parsing that is specific to that adapter so it's not actually part
of my core domain but it is part of that adapter and so I'm gonna have a test for that and this is going to be a
isolated unit test it's because it itself even though it's in an adapter does not touch the outside world it just deals
with commands and text and I can write tests for this and it run really fast now that's not always the case because if I
want to test my web UI I I may have to actually use some part of the infrastructure in order to do that so for example
when I'm testing the web UI in a spring application I'm not really interested in testing how it talks to the service
inside of my core domain and how my core domain works I'm mainly concerned with did properties parameters get
transformed correctly did routing happen correctly to the correct URL and so you can see in this test I'm doing things
like I'm making sure that slash deposit is a valid URL now the view name is correct that there's attributes in the model
or that in a post I posted the correct parameters and they result in a question about dt o--'s live in the app service
no d Chios only live in the adapter and we'll look at on the other side in the flipside when we get to persistence that
anything inside of the core domain does not rely on domains it's all domain objects it's only when we get to the adapter
the adapter includes the DT OS and we'll see some some code examples of that in a little bit so again I have integration
tests on the adapters but I'm only testing what the adapter is responsible for and so if you look at sort of this sketch
we can see that each box or hexagon has unit tests that are contained within those boundaries and so what I want to do
is make sure that I can test you know as much as possible using these unit tests because they are faster and easier to
write and but sometimes I need to test some of the boundary crossing so for example the the yellow lines coming in from
the left and an upper left show that I can test the adapter through the core domain because I might want to do a little
bit of checking that I'm that I wired things up correctly but those are going to be the the minority of my tests right
so those are sometimes called focused integration tests I might have a few then like the orange line that comes in from
the upper left and goes to the lower right an end-to-end test that uses everything that you'd have in in production or
as close to production as possible but again that's in the minority all right so let's look at ports so we've looked at
the adapters to handle incoming things triggered by the outside world let's look at the ports supports are abstractions
and concrete implementations whereas adapters we didn't really have any abstraction x' other than our service which was
inside of our core domain the ports are are an abstraction that we need in order to define how our core domain is going
to initiate communication with the outside world but again the ports here are inside of our hexagon that means they are
talking in the language of our core domain and so forth if we wanted to send an outgoing message or an outgoing email we
would create a port and then we'd create an implementation of that that would be that would handle communicating with
the outside world so if we look at the steps for defining a port because they're a little bit more there's a little bit
more to it as I mentioned then the adapter the step one is to basically define the ideal interface that's in the
language of the domain so an example of of that and this is going to be driven by unit tests is something like this
let's say we want to send out a notification if the balance changes on an account so we can see here the package is in
the domain package and we'll look at packaging in more detail towards the end and here I'm defining an interface how
would I like my core domain to communicate to the outside world that about that the balance changed in this case I'll
basically want to say this accounts balance changed and it changed by this much but it's in the language of the domain
now because the it's in the language of the domain I can easily write tests for it I can talk about it in terms of my
domain but if I want to do some tests that involve it then I use something like a spy and so I'm using a very specific
term here as I mentioned the idea of test doubles comes from Jordan azureus and some others who've defined that things a
bit more explicitly than sort of just using the word mocks so in this case a spy is something that can tell me not only
did some method get called but that it could called with the correct parameters so you can sort of think of a spy as
having a secret recorder recording every interaction with it so that it can report back so what this looks like in an
actual test is something like this here I want to make sure that my core domain code my business logic code has been
wired up to correctly call the balance change notifier when the balance changes so here I create a mock notifier
technically it's a spy but I'm using mockito here and when I create the account if I do a deposit then I expect that the
balance changed method will have been called with the account and $25.00 and that's my validation that I have wired up
my code correctly and up to this point I don't yet have necessarily a concrete implementation of it and that's really
good because then I can write tests and think about my design think about how my objects interact with each other before
I really sort of settle on ok this this I think will work well and once I have that then I can go on and create a
concrete adapter and so this is the outside world infrastructure based implementation of that ideal interface so one
might be a text message version so here I've got an actual implementation underneath it uses Twilio but I've abstracted
out Twilio itself into just a generic text message sender but here we can see at the top that the package it's and is in
the SMS adapter because this is things that deal with with SMS if I don't have SMS in my application anymore then then I
would just unplug this and remove the entire package and so we can see that it implements the balance change method that
takes the domain object the account and then queries it to get the balance and so again it's the adapters responsibility
to convert from domain to the outside world here even there is no DTO it's actually just a couple of strings because the
text messaging SDK only cares about some strings so the text message sender says what phone number you want me to send
it to and what do you want the text to be so sometimes d tos aren't even necessary if the outside world you're
communicating with just needs text the nice thing about this is it makes it also very easy to substitute a sort of no op
version of the notifier and I actually had to do this because when I was testing I was constantly getting texted every
time I was playing around with the deposit and I realized I don't want that always to be the case so you can use
techniques like feature flags so that I start up it can select between a specific implementation and so this is a nice
outcome of having abstracted out communicating with the outside world to a port makes it very easy to plug in and and
and swap around these things and so here I've got using what's called a null object pattern basically this is a do
nothing if when it gets called it just ignores it and so you might also do something similar when you're testing is have
a stub notifier that looks very much like this or maybe you might even instantiate this directly in your chest so your
tests aren't basically going and talking to real text messaging systems and you'll notice that the package that this is
in is in the domain because there's nothing about it that that deals with the adapter it's not specific to any any one
adapter now you could argue this might go maybe in the just a base adapter package but that would be a minor NIT so so
far you can see that that there's a lot of things where the domain vain objects need to stay in the core and that the
adapter is handling the transition from domain to DTO or two strings and vice versa and so this leads us to the
dependency rule which is dependencies only point in words and so what that means is that you can have adapters depend on
your core application and so from a technical standpoint they can import things from the domain so in your adapters you
can have importing objects from your domain package but the reverse is not true you do not want your core domain
touching or importing or knowing about anything that they're in the adapters and so remember the adapters are not just
the maybe controller classes but also include the DT O's or other infrastructure or framework specific things and on the
right side we see the infrastructure adapters which plug into the ports so again because we want the component being
able to talk to the outside world then we have to have some abstraction to do that in this process of our core
application talking to a port and then plugging in implementations from the infrastructure is basically dependency
inversion we're inverting the dependency since we don't want the application core talking to specific adapters we want
we want some some interface in between and so the dependencies from both sides point inward and this works really well
as a rule and in fact there are ways to enforce this that I'll talk about later so the last kind of port I want to talk
about because it's one that is almost always used is persistence and so there's this idea of persistence ignorant so you
could sort of think about the the example I showed before sort of infrastructure ignorance ignorant you know basically
not being concerned with is as being you know as this balanced change notification message being sent by a text message
by an email carrier pigeon who knows and so persistence ignorance is is also the case here which is where we now have
repositories for you know finding and storing our entities and aggregates and again those talk in the language of the
domain so here we have a goal repository so the kid money manager has ways of tracking goals that my son might be saving
up for users because I have user profiles things like that so again we do not want our domain objects to leave they need
to stay inside the core domain so we can't directly talk to a database so instead what we want to do is like we did but
with the balance chains notifier is create a port now this port is probably going to be you're gonna probably gonna have
this be a little bit less flexible in terms of defining it usually because they look very similar your repositories tend
to look very similar right you got save you've got fine maybe delete and variations on sort of on that theme so they
tend to look much more alike but the nice thing is is that once you define the port you can create a fake one and this
might and a fake is basically mimics the real thing but doesn't have some feature that that the real thing might have so
for example you could create a fake repository adapter that stores all that information in memory and in fact when I was
developing kid money manager I did this for quite a long time before I finally implemented the real thing to talk to a
database and that's nice because I didn't have to worry about constantly changing how I'm saving stuff in the database
until my core domain settled down and and I figured out what I really needed to hold an account and transaction and
things like that so once you've got your fake and you've you know got in a certain way then at some point you're gonna
create a real version and this is gonna be your repository adapter so like other adapters it's gonna be responsible for
translating your core domain objects and mapping them to tables and how much of work you do versus your framework does
is up to whatever framework you're doing you might be combining multiple entities into a single entity or most likely
certainly collapsing value objects into into parts of an entity that gets stored but if you let's see here from the
diagram what gets stored or something like DT OS and so that way again you provide this buffer between well I need to
change the way I'm storing these value objects in the database from my core domain and in spring I do this in the
application using the JPA repositories which are super easy to define it basically just interfaces and so I end up with
the interface so that's being sort of the concrete implementation and then I have adapters which for the most part just
delegate and so their responsibility is just transforming the core domain objects 2d tos and then storing those so now
that we have an architecture we know where things go that really helps us with our packaging so this packaging diagram
here is for the kid money manager application so on the Left we can see at the high level we have an adapter an app
config and our domain high level packages and so you can see in our domain this is where all our business stuff is our
accounts our goals our roles transactions things like that as well as repository interfaces and the balance change
notify our interfaces right so those are the ports some people like to put those things in sub packages and name them as
port I've tried that it makes me a little uncomfortable because now I group together things purely for technical reasons
so I haven't found that to be to be helpful I will say though that the number of domain objects I have is probably
getting to the point where I might subdivide them based on features I might subdivide them based on you know here is
user profile related domain objects here is sort of the transaction account related things but you know the application
here is small enough that that I didn't feel the need to do that on the right we see sort of an explosion zooming in on
the adapter package so we've got three packages underneath that we've got the JPA one and and so as I mentioned this is
the one that's responsible for storing and retrieving information from the database and so I've got DT o--'s there for
my goal I got a user profile DT oh and the repository interface so that's the spring data class the interface that I
need and then the adapter that adapts from my ideal port interface to the repository if you look closely you might see
that there's a missing transaction DT oh and that's because that's one that I actually have not separated between the
core domain and the the actual database so there I violated the separation between core domain and outside world and
that has caused some problems and so that's a refactoring I'm going to do under the SMS adapter we can see that all the
stuff relating to SMS so we've got our command our parser our controller things like that and then a concrete
implementation that I'm currently using Twilio for my text message sending and then at the bottom we can see that that
the web UI is in its own package and I've somewhat subdivided it according to a teacher so I've got all the stuff
relating to goals in in one sub package and there isn't a lot else there so that was the only one I had sort of putting
it in its own package and so with this packaging structure we can actually enforce it using something called arc unit
and these are J unit like tests that can basically be a failing test if for example an adapter relies on another adapter
or if you accidentally have your core domain relying on something that's in an adapter and it can basically have a
failing test and so you can really enforce the the package structure and that will help you sort of keep keep your
modularity and this is where it's like I think it's fine to have a monolith and if you have something like this
enforcing the separation then you can get really far with a monolith and if even if you don't like or maybe you have
multiple teams working you can actually have a separate team working on an adapter because there is this well-defined
interface between the adapter and the core domain and that's that's your service that's probably less likely but it is
likely that you that you would have possibly separate repositories for your adapter versus your core domain now there
are a few places where I would say don't bother using hexagonal right even though I think it's it's a great architecture
that that really scales from small micro services up to larger monoliths if you've got a basic credit don't bother if
your domain is pretty tiny don't bother there either or if your app is of it sort of a different type where you're sort
of doing transformation like I was working with one company and it was pretty much they were one part of their app was
taking messages that came in transform them in some way and then wrote them to a database not a lot of logic there so
very much closely tied to if you if you're using domain driven design then you probably want to take a look this
architecture if you're not using domain-driven design and and you're not having any problems and it's really simple then
maybe this architecture is overkill but I still think that that thinking about things is as core domain and adapters
even if it's small even if you just have a few classes just thinking about it that way can really help make sure you've
got your tests isolated so with hexagonal architecture you want to focus on your core domain and as I mentioned that's
where domain driven design is is a really great thing to use to help you get that core domain correct domain AB objects
never leave and you never accept a domain object from the outside world you're always using the adapter to do the
transformation either from strings or from from DTO objects into domain objects and again that that helps keep that that
isolation that protection layer adapters per trigger type it's not a hard and fast rule but it's definitely a good
guideline if you have multiple certainly if you've got web UI versus at you know something like SMS text messaging they
may look similar because maybe they're both accepting HTTP requests but they really are different and I personally
rather have a few more adapters than sort of fat adapters with with lots of intermix stuff ports are the ideal interface
to the outside world and so you define them that way and you can do it TDD I developed all my ports TDD and then plug in
concrete implementations later on and the dependencies point inwards and as I mentioned you can use something like arc
you know to to enforce that and finally package based on that architecture it will make things easy to find and you will
know also where to put them right if you're creating your command parser for SMS text messaging you know exactly where
that goes or where to look when you have a bug so that brings us to the end of my slides and presentation and at this
point I'm happy questions if you need to go that's totally cool I hope this was useful this is my contact information if
you want to learn more the link to more testable comm you can sign up on the mailing list and get information about when
when I get early access to the course I'm working on that goes much deeper into the code how to develop it using TDD and
other mechanisms and it's it's basically a Java spring based type of course so at this point happy to take any questions
and if you need to drop off you feel free to do that but go ahead and type your questions in the chat and as I mentioned
I'm gonna hang around as long as people have questions so if you either have no questions or you're not interested in or
don't have time for hearing other things then have a great day and I hope this is there a dotnet version of assume you
mean Ark unit um there's something called n depending I don't know yeah I know I don't know if there's a dotnet version
of sort of the Ark unit thing it it wouldn't be hard to write and so that's why I'd sort of be surprised if there wasn't
a similar one but I don't know if there there is one great and thanks for it thanks for coming appreciate it and again
I'm gonna do this webinar again in in September so that way if if you or your colleagues want to catch it again and and
ask questions then I'll announce that and again if you go to more testable calm and sign up there I'll announce the next
webinars yes adapters are that are in the outside world they are participating the outside world there they're talking
to the outside world they're sort of the interpreters to translate what the outside world is doing to the safe inside
core domain and vice versa net Ark test all right are any other questions just type a question mark so I know that
you're typing a question but as I said I'll hang out basically until you all leave or I've answered all your questions
and again the the code for this is is up on on github hit me up on Twitter if you can't find the link and this
presentation if you want the slides I will also have them available if you go again if you hit me up on Twitter or if
you sign up for the more testable com email list I will email email out a link and that's okay well we can disagree we
can agree to disagree but and we can use another venue to talk more about what you see differently about the
architecture because I'm always willing to learn and adjust I have been doing so as I've been playing with this and one
thing that's always been sort of key in my mind is how testable is it how easy all right so I think there's no other
questions if you come up with any other questions at any point as I mentioned
