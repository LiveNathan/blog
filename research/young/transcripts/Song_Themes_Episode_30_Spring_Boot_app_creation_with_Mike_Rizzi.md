# ＂Song Themes＂ Episode 30： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=32GaBRX2L0o

---

## Transcript

all right welcome everyone to episode 30 episode 30 third decade we've done we've done 30 we we have done 30 of so uh
hey there fle welcome welcome F first one in yeah first wow awesome uh so we finally got to the database stuff pretty
cool huh yeah and that was um fairly straightforward that's what that's what happens when you when Apparently one of us
knows what they're so um any any thoughts about uh anything before we before we jump into the code um no I don't think
so I didn't have anything anything meta to talk about all right uh then let me move my thing off the screen yeah so you
can share my yeah desktop or want all right so so last time uh um we finished with the uh repository yes we got the
Flyway in there we got the database dependencies um we created our schema and that was that was cool um created our
object and down below there we have our repository which turned out to be um a much simpler expression than than we
thought yeah in the end thanks to thanks to our viewers for for helping out with that hey it's Benny hey Benny welcome
Benny um yeah so that that that select was was selector where's that sounded yeah really sorry I don't have that I
should get that at hand have a a what are they called stream pad or I forget the name of it but the pad how just hit the
button without actually have have a um a tool almost explicitly made for that kind of thing that I should I should get
ready um so there's a whole bunch of uh on the Mac um there's a company called rogba that has a bunch of audio tools
audio rting tools and um one of them uh so I use loop back to basically route route audio around uh and there's another
one um that basically is like this big you know thing with a bunch of buttons where each one is a sound effect or some
kind of sound so I'll I'll set that up for next time you're like a morning radio show yeah exactly so we created the the
con the the sort of low-level technical repository um and we already had uh the rest of our our code talking to the port
um so now we need to wire those those two things together um let me actually show that diagram again you think I was
just about to say Let me show that diagram up and I should probably share the actual drawing thing with you but for now
we'll do idea so yeah so what we've got is um we we have our ports and adapters are hexagonal um we already have all
these tests so we got domain layer tests that test directly against the domain um we have our use case layer or
application layer test the test against the song service and now the song service talks to the song Repository so this
is our Port um and our Port interface uh is by its nature technology agnostic here's not about what technology we use
whether we use the in-memory version that we've got that we sort of refactored into from what we had before um or the
the real one which is what we're going to hook up today um out here we've got we basically have our database uh right so
this is our our post graph Database The Real Thing real as in an actual postgress instant not necessarily the production
one but it's a real database uh and so in order to to talk to that we need some kind of um let me point that to that and
then make it like that there we go so this is the intermediary this is our adapter uh and so uh we have our Port we
actually have sort of um what I think of here is sort of the the technical smaller so this is our technical connector
this is the thing that implements our our spring data jdbc repository and then we need something to take our our our
song objects our domain objects and transform them into the things that that get stored into uh into the database so
that's what we're going to write today is basically sort of the rest rest of this adapter quick suggestion yeah on the
uh where it says real database postgress should we add the word adapter at the end of that I'm going to change that to
say because really actually it doesn't know about anything about post crust it just knows spring GC be nice there I'm
guessing the tool doesn't let you do words rotate words I can but I'm not gonna fiddle with that right now yeah I should
have rotated this differently but that's that's the basic idea is that um I always think of of adapters having two parts
um there's the thing that touches that Imports that directly knows about the concrete library or framework module
whatever you want to call it um and then there's the part that's doing the the transformation and so we're going to be
focused on that that transformation part uh today so uh oh full ala has a has a question uh from time to time I hear
that spring data jpa is a bad practice because developers retrieve all the data without filtering um I don't think that'
s necessarily a problem um I mean it's it's sort of not technically related to what omm you're using uh but there is
sometimes a tendency to to read everything into memory and then filter in memory when you could let the database do that
um I don't think that's specific to to jpa I think jpa is overly complicated from for many use cases that people use it
for uh again it's one of those don't use something more complicated than you need uh don't just copy what other people
are doing make sure you have a good reason for using a library framework technology thing like that so we're using in
this project like I use in many of my projects spring data jdbc which is a much simpler smaller uh om that is because
it's less complicated it means there's there's less going on and there's less ways to sort of go wrong um so I don't
know that it's specific to Spring data jpa is a bad practice but I think if you're reading stuff into like we could in
in our implementation uh we could have just read in all the songs from the database and done the filtering like we did
before in memory um but why read in stuff into memory that you're that that you're basically going to going to then
throw away so um but good good question hey Jenice no not too late oh I think it means late start for us we've been
starting it oh late late stream oh yes uh you I thought you were saying you were late no you're not late uh but yes this
is a later than usual uh at least for pairing stream yes yeah um C hey persistence yeah definitely I think there is a
lack of and I think it's I think it is very much related to using OMS and since spring data jpa is the most popular
thing then probably it it it seems connected that people do not understand SQL and and relational databases and its
benefits um like we had you know we figured out it wasn't terribly complex with one query we got exactly what we wanted
now granted it's one table uh but learn learn relational stuff learn SQL learn joins learn uh indexes um learn that
stuff because it will likely increase performance of uh of your of your system I know Mike is familiar with some
performance aspects of of database recently six seconds why is this taking six seconds oh we should index some columns
yeah oh I was I inherited um this website that a friend of mine had built for was a small company and it worked fine on
this one hosting company and then they had that hosting company was going out of business so it got moved to a new
hosting company and for some reason when they moved over the database they didn't move over the indexes so I was like
why is this slow it didn't used to be slow before debugging the query and I'm like this this is a gnarly query it was
but it turns out it was just the indexes it went from six seconds six and a half seconds down to3 seconds I think yeah
yeah just by adding indexes was pretty cool yep yeah and normalization like if you're going to use a relational database
then you want to normalize your data you may not want to fully normalize everything um but you really want to be careful
about that um I see a lot of people sort of again not being thoughtful about the database technology that they use and
moving to no SQL or document databases without understanding what they're giving up uh what they're getting or what
they're giving up because these days especially uh my my default is give me a reason not to use postgress I mean
postgress is awesome you can throw documents in it um you can treat it if you need to you can throw Json in it and treat
it as as a document database uh so for me it's like and and you can throw on PG vector and do similarity searches which
is what uh uh Dan Vega and DeShaun Carter and some other spring spring folks have been talking about on their streams so
you it's like you got to give me a good reason not to use not to use postgress and there are them there are good reasons
but you have to really really understand why uh and yes full aw it is a bit confusing there's there's spring jdbc which
is a very fairly low-level interaction and you got the jdbc template uh it's not an OM uh it's a thin layer sort of on
top of jdbc uh spring data jdbc is part of the entire sort of spring data set of things so where we have spring data
jdbc which is what we use um spring data jpa which is generally using hibernate underneath uh spring data no SQL spring
data spring data etc etc so easy to get confused um I understand why they named it that way but it is definitely
confusing all right should we uh switch back to to code yes all right I've cleared the deck yep I can see that all right
so we're working on J J Number 96 okay we're gonna work with concrete so uh let's let's run all our tests um and since
we're running all all uh that'll take a number of seconds more than than usual and I remember to bring up the docker
this time so don't have that same problem as last week y okay all right look good accept uh right we commented out a
couple of sorry yeah let's take a look at that one um right so we commented these out uh because these are pro probably
no longer relevant um wait a second why is it not have a disabled Oh we must have disabled we disabled the whole the
whole thing class right right yeah and so this is this is because we don't have test containers set up so um when you
run tests it won't run the docker compose this is on purpose and this often confuses people because uh out of the box if
you run the application it'll run the docker compos and you have your database and everything works fine if you run the
test it's not going to run the docker compose and unless you have test containers set up it won't run those either and
so therefore it'll fail to start because it won't have a connection to a database um let's leave this disabled uh but
let's put in a a comment um I'll add in uh mean as in here yeah as in there um Ted to fill in workaround for this so
there sort of a workaround you can you can kind of import the application so it will actually then start Docker compose
but that would be a special case for this uh this specific test but we we'll we'll do that offline sounds all right um
so let's take a look at um let's start with our Port right so what we want is we're going to want an implementation of
uh of our Port right so when we do ports and adapters in in in hexagonal our adapter our outbound or sometimes called
driven or secondary adapter has to implement the port the port is the The General way that our application wants to talk
to in this case persistence um so let's look at our Port which is going to be inside of our application yep there it is
now there's there's some interesting naming conventions that that folks have have used uh for this um I haven't been
crazy about some of them but there there is some uh idea of saying this is really all about you know uh finding uh
finding songs and saving songs um and so one could name it as uh literally a the class as uh for finding and saving
songs because then it makes it clear what is this port for um naming is of course hard and and there's always this
tension between naming it something that like that that is very descriptive but is also very much not what people are
used to and so there's always this tension of like well I want it to be really descriptive and of a good name but also I
want people to understand what its role is uh and so there's there's that tension uh here um so because the name again
you had you had was four something like four uh four saving and finding songs do it this way for saving and finding
songs and so that you couldn't get the Best of Both Worlds by saying because that just seems weird yeah that that that
that just seems weird and there are some other some other naming conventions uh that you know that just change it to say
well um I'm I'm sort of fine with it with it being with it being this so we want to do is um do we have any
implementations of this I don't think so given the name of the one uh method oh I guess we do right we have our inmemory
one that we refactored so we refactored out the inmemory one and then extracted out of that this port interface got it
but now it's confus yes so this is where the naming gets a bit confusing because we're using the term repository in the
in the domain driven design sense of completely agnostic don't care about the technology it's just a collection of stuff
um for better for worse spring data co-opted that name and used it for the technical implementation of how do we store
stuff in a database and I think it's unfortunate um that they did that but oh well that as they say that that that horse
has left the barn or someone of them we can call song repository repository um yes if we want if we want to to be
pedantic um but you know because this is in the application Port I'm I'm sort of okay with with this uh and um DOTA to
attitude brings up a great point one of the things about that alternate name is it is it seems to indicate that maybe
there are two uh classes or really interfaces one is for finding songs um and one is for adding songs uh and that's
that's um that's not a bad thought that's actually really uh a really since most of the time and especially certain
types of users will never be able to add um and so this is what the inter you know what sometimes referred to is the
interface segregation principle make your interfaces really tiny because you you know just because you're finding stuff
doesn't mean you're necessarily going to want to that sort of same use case doesn't need that the adding in fact those
are really two separate use cases and we don't actually have ad well we have ADD in the interface uh the technical oh
here it is Data implementation can I um do that yes yes okay um so part of our adapter is adapting here's what our Port
wants to call it right our ideal interface from the point of view of the rest of the application and here's the
technical thing that says save so we're gon to have to adapt from add to save and that's part of the adapter's job uh
and yes full nul there there is a flavor of of cqrs um it's not quite full cqs because we're using the same database for
the read and write model um cqrs has separate read and write models uh and that's that's the big difference between just
having nice tiny well-targeted uh you know cohesive interfaces um from full-blown cqs where where you actually have a
model dedicated for writing and a model dedicated for reading that's where you might use it database yeah so if we were
to break interfaces this was the first thought kind of riffing on the ending with repository theme but kind of dealing
with the find and save thing um though I think people aren't used to seeing verbs as the first word in a class name um
like if we did the separate the inter thing yeah I might I might if I were to go this way uh to have it be a uh a song
adder and a Song Finder so oh if um we may decide that once we once we get more once we basically get UI uh well once we
sort of get back to the application we might want to take another look at does the application layer um was right now
our song service do we want to split that along the adding and find and and the finding yeah yeah but for now this
interface is good enough I presume yeah thinking splitting it out now is a little bit early y uh is song The aggregate
yes right now song is the only aggregate yep saor all right so what we want to do is we now uh we have an in-memory
implementation uh what we'd like is to create a uh yes uh is to create a um spring data jdbc adapter so let's go ahead
and and implement this interface you can use a shortcut to do shortcut oh maybe not I thought it was off a refactor uh
it's not a refactor I think it's it's an Alt Enter oh Quick Fix so Implement interface yeah where do we want this to go
well first of all let's not call it song repository imple oh good lord no yeah you can actually change that default in
intelligy you can tell it to stop doing that um I I have mind to set not to put a put imple at the end to put default at
the front because at least that's a reasonable name okay let's go and do that change because I'm sure I'm not the only
one I would like to have that so if you go to I think it's naming big uh maybe easier to find with with uh suffix as the
search suffix where's that just type suffix is yeah so you can delete that and then you can have it as a prefix uh I
usually wear the the fault yeah cool you know what I'm gonna do don't you screen grab this yeah so um there's some other
interesting stuff around test names that uh maybe maybe we'll we'll get to um so Jeff Langer uh recently posted uh
little article about some some different ideas for naming and I've been thinking a lot about test names um so maybe we'
ll we'll look at that if we have time oh cool um I also realized that the book he he published in 2006 was actually uh
foundational for me in terms of tdd because I was looking back at it's like oh this is where I learned that um so he's
publishing a new a new addition oh wow that's great which is nice yeah this you want to stick with that name or U no so
what we're going to want is um uh the way I generally name it as I put since it's an adapter for specific technology uh
I basically uh call it I would call it something like adapter and would it go in the port package no it's an adapter so
where we it go is outside oh so it go up here and um adapter out jdbc right um yeah that would be jdbc okay so let's get
this one and that's not the test section good very funny as yes all all implementations should be suffix uh all right so
um what we want to do is we want to uh drive this through tests now there there are couple of ways we could do this um
one way is we could write tests um the other uh the other way is drive layer um so why don't we uh open up our Our Song
service on the top so we have oh so let's go down to some of the methods that actually do stuff so we've got ads which
is basically two of them right we've got ad song we've got import songs um and import is just sort of a more General ad
so let's scroll up a bit to bring the other method into view yeah so we pretty much have two very some you know methods
that look very much like what are what are in the adapter um so what we can do I think uh I think instead of testing so
if we sort of go back to the the diagram I'm again so we have a choice in in how we test um this this adapter here right
so this adapter we can test directly we can write tests directly against it say add song is a song in there um and add
some songs and then can we find them by their themes the other way is again we use these use case layer tests to test
against the song Service uh but instead of using the inmemory fake adapter we actually plug in the real adapter and so
uh it should work right once we get this stuff to work it should it should just work now at that point yeah that's going
all the way out to a real postrest database correct okay yeah so um if we do that I'll make that green so we can we can
do that um the upside is we don't have to write any other tests and it should just it assuming we implement this stuff
correctly inside the adapter it should work the downside is is we kind of uh have to do a bit more setup in our um but
not a lot okay it also seems like a big step but maybe it's not well we can we so we can do it and see see how it feels
and if we feel like it's it's actually too big of a step then we can then we can go back yeah that makes sense so I'll
put you um so let's look at the song service test at the top oh it's already open oh wait a second uh there isn't one on
the top song service test you want me to open it go yes I was about to say you're you're doing the thing that computers
are good at of of looking for stuff when you said on the top it implied there was already up there that's why it was oh
I would never imply go search for an open tab yeah okay uh no if oh got you what are we open song Service Test that's
yeah so you could have done Al shift t or sorry control shift T oh true true um you have an accidental breako on
something that's not break pointable no so accidental complexity so let's uh let's let's get a high level view of the
tests here there many yeah so we've got added songs are saved bulk ad using tsv malformed multiple songs are found by
the theme save songs loaded on Startup um so what we need to do is uh we need to figure out how to plug in different
implementations of the um of our our uh repository absolutely uh so how do we do that so I see how we do that in the
first test using Create null how do we do that in the in the next test aha so there we basically create uh the uh in
memory directly um we could do the same thing for the or is there going to be some complexity regarding Well we'd like
we'd like to do that for all of these tests um what what does what does crate null actually do now does it internally
create the in memory I mean it must um I think we actually want to uh inline that because uh in our in our tests because
we're always going to want to pass in anory repository yeah I just seeing what the other ones looked like yeah it looks
like all the other ones are using and this one's using cre oh this using Create empty which is basically verion yeah
remove inline all uh no it's got five occurrences we only want to inline okay and then let's extract uh the repository
to a variable so what we're so it be int well yeah introduce variable yeah I was my brain was thinking extract so we
want well I call it extract until J I think calls it introduce ah so we want just the not the create empty part or you
want the whole thing including create empty no whatever what do you have and you can just call it repository or actually
here we go I don't know why I I guess I I I understand why they call it introduce variable but I call it extract
variable because that's actually I don't know what I don't know what Fowler calls it there's inconsistencies between
what Fowler calls it and what intelligy calls so before we can parameterize the test I think what we want to do is is do
this one by one so maybe clone this test do it with the other one and then parameter roll it parameterized um or you
think just starting by parameterizing and that might be sufficient I think I think I want to parameterize it and then
have uh another so parameterize it and then actually have another test class so because what we want is we still want
this class that is IO free that uses the in memory the new one we're going to create is going to need to have
annotations for the the test container database stuff um and we don't want to we don't want to com we don't want to sort
of combine the two so we want what we want to end up with is sort of two um two tests that that do the setup one just
instantiates the in memory version the other one does all the setup for for spring and then calls these tests uh as as
uh as test methods um so we won't be using the parameterized we won't actually be using the parameterized test
annotation yeah got it okay yeah now I know where you're going yeah uh FR we're we're basically uh creating the adapter
to be able to so last time we created the database storage the omm level um and now we're application and hello this is
to have a base class to have the tests here as the base and then the subclasses provide the the repository um so that's
another uh another way to do this oh interesting so making like an abstract Base Class yeah so this would become an
abstract Base Class and there would be a the abstract method of provide the the repository provider can you T and you
can tag them each separately one is tagged as well that's what I'm trying to figure out slow could you do that uh so
yeah so IGI asks is is uh is that what we're doing it's like yes that's doing and we want excuse me and we want then to
be tagged slow and fast yeah so um let's let's go that way because uh the other way I've done it is more of a a sort of
composition this yeah this's I'm trying to think of like some other ways that you can use junits parameterization
there's some more compli uh more let's say sophisticated ways of doing parameterization um but I don't think any of them
allow us to tag them differently which is really what we want right because we want the one that uses the in memory yeah
because parameterization it's going to be run under the sort of the the same thing so um yeah so let's let's let's try
this see how it goes okay with is this is our Base Class um so let's extract out the repository creation to a method so
that all of these tests call uh call the method that creates a song Repository so almost undoing what I did generic uh
see this one calls create passing a song list this one's calling create empty so I think the ones that are passing a
song list we're gonna have to do differently okay we've got two empty three empty three empty to a song test so let's
let's fix the ones that that pass in a song list because that's not really part of the repository's interface um I think
that should also be empty and it should just add it directly through the repository instead of passing it a list W so
let's let's make those change I mean it should it's a fairly minor change let's make those changes okay so let's start
with the first one um well the first one's create empty so that's saying create with null instead right go what are the
terminology using Create empty so that would be basically change this to create actually I didn't need you to do ad um
yeah so what I would have done is is cut line 32 pasted it and changed song and then you can get rid of that and then
you can get rid of the unused array sneeze yeah there's there's already repository already has a method to add so we
don't need to sort of encapsulate encapsulate that uh I mean we still might encapsulate that as our setup uh but we
didn't have to um we'll see if we need do that I'm back y uh so let's do the same thing for the yeah I wonder what do
this will grab far uh let's run our IO free test to see that we haven't broken anything we shouldn't have but we did
there yes all right okay looking good uh is that it I thought there was yeah there was two and then the other three were
just using straight up empty all right uh so let's do a commit so we can commit that change uh let's not commit the
adapter though because we're not we haven't done yet what did we do the repository we changed oh right we I think you
just added some white useful we do here oh we add dis so the only thing significant is literally what we just did was
yeah add the songs to interface uh so frer asks a question and I'm gonna say it depends or what what is the goal yeah
what so what do you want what do you want to learn what do you wanna what do you already know uh you're going to have to
provide a lot more context um because that's like saying I write which is a slightly broad topic which is not not
specific enough to to to answer um and by the way this kind of question is really awesome to ask in the Discord because
you'll get answers from us but happy to answer it but you're going to need to to narrow down your bit um all right so
let's uh let's now factor out the create test get empty uh well of course um actually before we do that I think it might
be easier uh if we change the the Declaration of all these repository variables to be the more generic interface right
which I already forgot the name of that one it's just without ah go change all of them I presume actually that one is
using yeah because that one we extracted so it's using that one that one is not it should just be two of them nope that
one's using uh hold on hold on hold on uh you you whipped right past the fact that we just broke something ah okay back
ah uh so apparently our inmemory has an all songs method um which uh is fine um but we need to use the one that's
actually defin that we want to explicitly Define uh so let's go to that method that implementation let's move that up to
the uh to the interface as well um although we don't do we want it as a stream sure let's keep it as a stream so move
this to or move U make a move it to the b or well you want to you want to extract it to the to super class it now the
other the other yeah uh so we up and that's what we want and that's that's fine it's basically saying if you're going to
pull it up to the interface you have this other implementation that's going to need to fine since we haven't really
implemented it anyway uh so let's just go to the song jdbc adapter did it added for us or did is it gonna make us do it
it looks it's weird but it no no the song jdbc adapter the one that was complaining about this one yeah yeah so let's
just fix that method uh that's fine we can we can we can uh stream empty and we can leave fine so let's uh let's go back
uh and continue replacing this is why it's good to replace uh what all our in memory definitions with with the
decorations with the the interface yeah and a little bit slower okay that one looks like let's test okay no I'm just uh
imagin redeemed a hydrate so I'm going to go hydrate oh nice oh that reminds me I forgot my water bottle I'll get it the
next break okay and was that the last one already all right uh do the test pass I'm pretty sure they did but I'm Gonna
Run them again because they're commit so welcome uh is it imaz or imaz is it a short eye or a long eye but welcome uh so
J ask one testing using real database do I empty the tables between each test class no um not generally uh if I'm
concerned I might do um uh you can if you're using test containers you can have it restart the container uh and so I'll
do that for for for some applications I'll I'll do that so basically it's not emptying the tables it's completely
restarting the database from scratch uh which is surprisingly fast um I was surprised when I when I set that so you can
you can set that control so uh because you can either set it and I think it even does that by default for test
containers you have to work you have to do a little bit of extra configuration so that it could reuse the containers um
but I think that's that's uh and it does run stuff in a in a in a transaction um so it should be rolling back yeah so it
should be rolling back anyway but if if you're doing stuff that maybe is already doing transactions um I I guess what I'
m saying is I I've not run into the issue where I've had tests fail because there's bad data in the in the database
usually the tests are fairly isolated um yeah do you think I'm curious when it says using real databases do you think
that might be meaning production like the're running against production well I Jonathan I assume when you say real
database you mean an actual database instance running on your machine not production right yeah uh but are you using
test containers or not I think is really the question I would question yeah and if you're not using test containers use
test uh uh the the creation of the repository into yep create song create um I would just name it song Repository but
I'm so used to I'm a littleg I'm a little allergic to get uh oh I'm with you with get I don't disagree with that I'm
just so used to verbs starting but it's not it's it's just a habit doesn't mean yeah I I think that's fine okay and yeah
let's replace all so that should have replaced all um like literally all there should be no anywhere oh this one oh
that's that's the one we just expected yeah so do a search and there should only be one yep only one okay great no I
just did within this well it's anyway yeah yeah did you want that kind of search no I wanted the search in the file but
not but not within the selection so do search again okay yeah I can turn the case off but basically it's I wasn't
worried about the case but um you if you select something and then do a search depending on what's Happening you may be
only searching within that selection oh I didn't think it was that's what it was doing but uh was want to be sure I
wanted to be sure yeah yeah all right so now um let's uh this is a new feature which which what okay so I'm gonna scroll
up oh the sticky lines yes between 16 and 18 yeah the sticky lines are are are uh new in 24 that's interesting so then
so it's to give you so it's when you have a long method which you shouldn't have um then be able to yes know your
context correct even though it's out of view that's kind of cool yeah so uh as is asking what I was going to ask you to
do is inline I don't I don't know why intelligence doesn't do this by default um so inline that uh and now let's um we
want to we want to create we actually want to right we don't have a down yet to go to we don't have a tar well we can we
can create a down uh so if we do a refactor um it may not be available here you had to go for the menu might have to go
down and that's the one we want uh and we want to keep it abstract because we want to push down the current behavior
into a specialized subass so check the under keep abstract in the table keep abstract in the table so there's the table
the table header has member and keep abstract ah there it is okay got it uh and then hitor over here that's not a table
that's why I was confused I uh uh would you like to create a new subass yes uh and default is is at least a a better
name than imple um but we'd like this to be the test it's so funny it's like I so rarely deal with sub classes that I'm
like it's somewhere I just don't remember where uh okay so that did exactly what we wanted it to do um let's go back to
the song Service Test command uh control e will get you back there quickly yeah and then just enter um so now that's
that's abstract so that's that's great uh let's now if we so we can't run this test because this is now abstract this
class um so if we go into the inmemory song service test does it run everything does it does it run everything yeah just
yeah let's see what it does I hit the check mark above yeah so yeah so it run all the tests great cool um yeah so
inheritance and junit is not something I often deal with and in fact in 5.11 so folks if you use junit and you have
anything around inheritance in your tests right if you've got subclasses of tests um in and you're using junit go and
test the the the Milestone release of 5'11 because stuff changed um jid had its own sort of way of inheriting stuff and
now they're abiding by sort of more standard Java ways of doing things uh so go go try it out and give them feedback um
otherwise when it gets released and it doesn't work um you could have head headed that off were uh okay great so um let'
s run all uh let's run the io free test just to make sure that everything is still passing oops damn it when I clicked
it it moved the um because IO free was less words this drop down got smaller as I was pressing at that point this was
that's why I should use keyboard shortcuts instead of that's another reason to use keyboard shortcuts yes prizing sonar
liy complaining about inheritance hierarchy ex sees limit of seven oh dear God I think three should three or three
should be the limit I am so sorry de my condolences oh it's funny it's like why are those pink red squiggly uh stuff in
the gutters like you must have accidentally run it with code coverage yeah that's what I commit and basically extracted
in memory specific version of our Ser song Service Test and by the way froster I have not forgotten about your question
I thought I'd handle it during during our upcoming break which is actually coming soon or now say hi to someone too
unless you did it and I missed it I did it and you coughing um should we take our our break now sure uh well it's either
that or we could create the the jdpc uh specific sunclass um I want to get my water so let's all right so let's let's
let's take our break yeah all right so we'll take our our coffee break uh and then when we come back we'll we'll start
uh implementing the jdpc spring data jdbc version uh that will help us drive that that implementation so see you soon n
he all right um so just wanted to address uh basically I put together that uh that that coffee break video yesterday
because I was like oh I wanna want something fun more fun so I realized I didn't have I wanted to add also a timer in
the in the lower right and I forgot to add that so I'll be adding that and I'll turn down I do now want coffee now for
some unknown reason uh so froster and um I was asking about a programming book uh and so now got got some more details
uh so what I would suggest is um and I think I've mentioned this before I know I've mentioned it before I'm not sure if
I mentioned it to to you um so uh Kai horse horse Horseman not hzman I always want I always get sometimes the S and the
T t- swwa Horseman uh he's been around for for a while writing writing books um uh so Kai Horseman I'll provide a link
for for the book uh the the book that I think is actually the most useful for and actually I'll just share my screen uh
and let me hide the comment now uh CA and the impatient what I like about this book um it's been updated through Java 17
I'm hoping he'll update it through 21 U but even so even updating through 17 is is great uh and what I like about it is
it's not every doesn't try to be super Complete because he's got other books for that he's got the the core Java volume
one and volume two if you want like real completeness um but this one has like he says it's got um no desktop UI because
for better for worse I think for worse but I am in the minority in this world um no desktop UI stuff um uh it's not
going to give you the basics of of variables and loop and stuff it assumes you know that stuff uh what it does is it
gives you uh kind of the core stuff stuff you need um and as I've mentioned probably every single stream I I've ever
done you need a project of your own to work on what you want is something that is going to be used by someone where you
can get feedback within a day or two uh what you don't want is to build something for like a friend who you only talk to
once every couple of weeks or you know something for a relative that you talk to once a month what you want is something
where you're going to get feedback on how useful this app that you're going to build is um so that you can then take
that feedback and then Implement whatever it is that's missing or needs to be changed or needs to be added to um that is
the that is a must you're not going to learn by reading a book right like learn in in terms of being able to write code
the way you learn how to write code is you write code the way you learn how to write code and and get good at it is you
write code um a book like this is a great reference and a great thing to to like make you aware of the things that are
available that's important because you can't write code if you're not aware of how to use string right so you want to
know how to use streams you're not going to be able to write code that reads from files if you don't know how the file
API works so reading a book like this and skimming through it and getting an idea of what's available in the language is
useful but you have to uh um you have to come up with with an idea uh that is your own um do not you can take tiny
trivial apps that come with some tutorials that you may find but what you want is an app that's your own uh so I'm not
sure what you're looking at in terms of intendance management system is this something you care about is this something
that somebody's going to use because if you don't care about it and you don't have anybody using it don't do it do an
app that is personally meaningful to you or someone close to you who will Pro will provide some value and it doesn't
matter what it is it doesn't matter how important it is it's just something that you will use and and maybe it's it's
you just you know you want a a to-do list that's specific to your way of doing things maybe you already used to list but
create another one but create one that is not just those here's a bunch of to-dos do things where it schedule things do
things where it prioritizes things do things where it you know things you know uh you want to group certain types of
activities together um a board game app that keeps track of which board games you like and your ratings of them I mean
be a one of the and so coming up with a project can be very difficult what I find helps is being aware throughout your
day and your life and and and the week in your life what things annoy you or what things like oh it' be cool if that app
existed or maybe there is an app but it kind of sucks create one start out small but but again the ultimate uh thing
that's important is that it's meaningful to you that you are interested in um I can't I could imagine things that are
more boring than an attendance management system but not easily um although you know when my mom was a school teacher
that might have been interesting because then I could get feedback from her uh but again find something that's
interesting and useful and doesn't have to be terribly useful it's not not like something that's going to change your
life just something that's like you know tracks your gym workouts you know tracks your your whatever it is something
that you know it's a hobby in your life it's something else um pick that project start small uh the hardest part and
this is something you won't get from books I don't know how uh and so I coach uh a bunch of of of of folks and this is
actually the hardest part is taking that first step what do I do first yeah so start out small like what is the really
pairing it down into into really what is the smallest thing that might be useful and again useful in the sense of it
does something um and that can be difficult uh that's probably to be honest is the hardest part especially when you're
starting out or when you're uh not an experienced developer heck as an experienced developer sometimes that's I find
that really hard um and so I coach a lot of uh uh developers who are who are you you'd probably consider um junior or
novices and this is the hardest part is what is that first Essence the first thing that I can say oh look I have
something uh and then breaking it down into into pieces that you can get that that you can get Fe feedback on whether
it's feedback from yourself or feedback from somebody else who who you're for so you mean like a website that uh
searches songs by theme something like that yeah and what you what you w to ER and and I'll reiterate like erir on the
side of of making it too small rather than too big it's amazing like you know we're in episode 30 and this app that
we're working on doesn't sound that complicated but you dig into it and you start implementing it it's like there's a
lot there um there's a lot of you know and it's not like we we Code 100% of the time there's a lot of thinking that's
involved uh and that's that's just as important as as any coding you're going to do the website that website could have
been a spreadsheet funny that um but that is another source for for ideas if you have like spreadsheets that you keep
track of things uh whatever those things might be um app to keep track of it instead not saying it's necessarily better
but it's something that uh that you you know about like my son was saying hey what board games do we have and I'm like I
have no idea they're scattered all over the place maybe we should have an app that keeps track of them and then you can
do things like okay this board game takes has you know every time we play it it takes an hour and a half um so maybe
that's not good for for like a short casual thing or this one is really difficult uh we you know like you know again all
these things pull you have to pull them from your life which means you have to start being a little bit aware of the
things that in your day in in your week um are like where it's like H I wish I could that yeah if you don't have anyone
who who's going to use the thing you're going to create do not do it again the the number one absolute most important
thing is that you or someone close to you will use it and give you feedback because if you don't use it you won't get
feedback and if it's not used and you don't get feedback it will be you're not going to work on it because who wants to
work on an app that nobody uses and that is uninteresting to to you I can't imagine anything more boring than working on
an app that nobody wants and that I don't care about like what's the fun in that like it because part of this is it has
to be at least enjoyable in in some sense of and don't be afraid about sort of copying apps right reimplementing apps
for your own purposes uh is is great if if if you're have if you're struggling something yeah track books yeah if you've
got a lot of books like also don't don't do something where it's where the administration of it is is is difficult um uh
but it may be something where it's like hey from now I want to keep track of books that I read and and and and some
notes on them great sound you know in other words if it could have been a spreadsheet or a document maybe make it into
an app lots of apps are right so we've got our our our inmemory subass of this test and it runs fast um uh a database
specific version of it um test the one that wasting yes that one um let's grab uh sort of the the setup stuff so all the
all the annotations yeah keep going yeah you may as well copy all that yeah that's fine good enough at that point yeah
and then let's create another uh subass of what's now our abstract song service test and we might want to rename Our
test how would we name it to be uh song service test base or something yeah something to indicate that it's like it's
it's it is the base class for for right uh that's gonna uh I presume no we don't want to what is it what is it renaming
um it wants to call this in memory service oh oh oh oh no no we don't want to do that yeah that's my my int take of it
at least right here it is yeah yeah no we don't um so now let's create another subass that'll you do that off here yeah
quick fix no no Quick Fix You had it oh this one yeah but you gotta look down a bit yep that's a fun name default song
sure that it uh well let's put it in the right yes and that's correct interesting uh oh uh let's make make it tell it to
fix whatever it is because I think it was not a public class oh yeah because normally when you create junit test it
doesn't have to be public but since we're in a different package public all right so uh one should paste up well that
made a mess of worse is that everything uh well the stuff you cut you need to now paste line 20 right yep thank God I
did a cut so that looks good implement uh no actually it won't be easy to implement sorry I forgot that we're not
returning the jdbc repository returning a song repository so we want to do is we now want to so now we're sort of in in
test drive mode so we're Switching gears into we are now test driving the implementation of Our Song jdbc adapter so the
adapter sits between our our port and the concrete uh uh song jtbc repository so the we've got the the the thing that's
talking to the database directly that's being autowired in um what we needed to supply is an implementation of the port
the thing that does that is the adapter so uh let's create our let's instantiate Our Song jtbc adapter now clearly this
won't work um but that's fine we will expect test to fail uh so let's let's run this happens so the way we expect this
to fail is doesn't have any connection to the actual database so it's funny that the the the failure test the failure
mode test worked failed um that's weird and concerning uh can we take a look at what that's what that's expecting so
what did it what did it expect uh a failure oh okay that's fine um because when we call import songs uh import songs
doesn't do anything so it's failing but for a different reason it is underneath it's it's failing for for some uh so
what is our what does our current jdbc adapter do for uh for ad it just ignores it yeah so it just ignores it so when we
do um oh because it never even even never even tried to save them because they were malformed so it fails even before it
tries to do do the save but I think if we wanted because technically we do want this to fail so we probably should have
ratcheted up this failure method well let's do thatt so let's uh let's be more precise that it's not not just that it's
a failure but we want a specific kind of failure message so what are our failure messages want to find out that's let's
find out that do a characterization test yeah so let's say uh contains well we have to assert something here oh uh so
let's say uh just that's wrong it would be no no it would be failure messages um we then have to continue contains um
let's say is not empty really we'll find out right we'll find out um I don't know what it may still be okay uh yeah we
may have to be more we may have to be more precise than that oh wait it's actually saying what it's saying here scroll
down well that one's the one that actually failed oh sorry this one right it's not goingon to say anything uh so let's
say failure messages so let's say yeah so let's let's say it contains exactly and characterization actually we should
probably have run it from um you should have run it from the io free version of it to see what what it what it actually
produces oh uh do you want to yeah so let's do that let's go back to to the in memory test and let's run that I guess we
could have just run the so now do the same thing on this one oh wait a second oh it's the well the thing is there's not
going to be any observable difference whether we're writing to inmemory or whether we're writing to the database because
we never write anywhere um so there's no way we can ratchet up this test in a way that's going to differentiate between
the two scenarios so um oh I wasn't thinking about differentiating between the two scenarios I was thinking that that
this tests over in the uh jdbc version should have failed let me rerun it so was this one right yeah yeah you'd have to
change the test back if you want it to to pass again oh right oh wait second no it still fail oh pass pass right right
right right you were saying it incorrectly pass and I'm saying there's no difference between whether we're using a
database or not because it's doing validation it's validation so it doesn't even try to save it right right so let's
undo that so I think I I think we can just leave it and it's it's passing and that's fine capability yeah because it's
basically a right but I think there's something I need to revert I think yeah so go into the song service test this one
yeah you can close the the window yeah uh song Service Test base right and then just click on the gut her there and then
y uh so let's run the song jdbc the jdbc version of that test that's this one right uh no uh yes oh no sorry no it's
that one yes this is why I don't I I try to I actually limit the number of editor tabs I have open to to like four
because otherwise it's very easy to start scanning through and looking for them and and get confused I'm G to close all
everything and as we need it we'll open it up all right um so this fails otherwise this fails as expected um so let's uh
let's do a say um and now we can commit the song jtbc adapter because that's now being test um so adapter class and uh
so which test do we want to tackle first I'm not sure what the difference between those last two are there added songs
are saved and then saved songs loaded on Startup I feel like the way things are currently same ah the second one uses
all songs um I don't feel like both those tests are necessary and where's the startup 33 yeah so because we changed sort
of the structure of Our Song Searcher these these tests don't make as much sense yeah both of them are just well so the
first one is searching by theme to see if what we added was found but that's no longer what the test method says um the
second one is definitely verifying the simplest case of if we ask for all the songs did we do we find the songs that we
for uh multiple songs are found by their theme so we don't really need that first test there the save songs loaded on
Startup I actually think we can get rid of it because we have a test that searches this one just happens to be it's
finds yeah and what do you think about the second one you think we still need that one so now this one is the one we
want to start with is like if we add a song is it is it is it saved to the repository but I think we should uh this is
really adding a song to a repository that already has songs in it and so this not simple enough so we should pick see if
there's another one simpler no there is no simpler one so we have to we have to make this this is sort of the many we so
think it's something one this L this line essentially although I'd say um uh yeah that's fine I was gonna gonna say like
save single song to repository no I was GNA do something else but it turns out not to be any better so yeah uh not a
void yeah I don't know what keystroke I had to do that but yeah I did want something uh sui suggests this I I did want
something about uh empty repository yeah let's do that so I don't think we have to say single song I think we can say
add something like that you uh well it's not is saved I think what we're saying is that um maybe if we write the assert
the name will be well that's what I'm thinking the assert is basically going to be is found let's go with that we can
change okay so uh GNA do this yeah pretty much uh yeah except we don't want the ad there we'll want to move that after
uh we'll actually want to yeah and 47 on 47 because we want to add it via the song service not directly to the right uh
and then we caner on we what uh what do you want to do oh you were sorry I was pausing because you paused my sence oh um
you were going to say assert on then you paused yeah so because I want to let you do it oh um can we ask the song
Service uh so we could except the song service doesn't I mean we could do it that way songs don't uh except song service
doesn't expose that ah right so we're looking is is in a sense effect have a good night and yes feel free to uh if
anything goes wrong uh blame Ted you could also blame chat but um it might be more more believable if you blame me
there's a joke about always blame test the side effect or do we want to test the direct effect when you say side effect
meaning which like asking the repository yeah so we can ask the repository give me all your songs and there should be
well yeah which leads us to say how do we know that there are any songs in there so uh I would say we're missing the
zero test so let's Let's uh let's disable this test which is basically uh new in a sense this is not quite um deserving
to be here but uh we might have we might want to move this somewhere got that's who you thinking um what is all songs
returns to ah run the whole kid Kaboodle or just um well so this is uh so we can't test from here uh we need to test
from the jwc song Service Test oh this is going to fail well it's not going to work at all because it won't have song
repository so copy or cut this and move um well no no we're in the base class we subass right so isn't this the subass
jdbc yeah and so we just want to run that oh run that oh I was thinking we cut it over is that code applicable to both
uh yes it is okay it should be got thinking okay so that that works because we're basically returning an empty fine yeah
I don't know what happens if we try to what happens if we try to run that test right here it's in an abstract us ah
interesting that's actually good um so we can run one test at a time because it says basically which one do you want to
run so pick that one yeah pick the jdbc one so does that just run the single test but using the subass I it we'll find
out that's handy yeah that is Handy that is nice yes it is nice not do yeah we we'll probably swegi um probably want to
talk about that as well all right so we've got our our our zero case um you want to run it too um we could just sure why
okay uh so let's go back to the next it um and I agree that is found is implying that it's found through the song
service um do we want to test it just that it's saved um perhaps that's actually what we want to do let's yeah so my
suggestion was wrong is saved is what we want uh let's yeah so let's run this one through the um let's run first through
the inmemory work okay and now we can run it through the jdbc which should not work because it'll end up with zero
because we're always returning an empty a long way to get to a a zero instead of a one yep all right now we can finally
that we have a failing test and failing for the right reason as predicted we can now write some code and the failing
test was I should check it again it was the Adon yeah right yeah yeah so it's a little confusing because there's a
little green arrow on this test um which really there shouldn't be because it it failed right this one yeah oh right did
it do it to the base class uh because I think we R can we run it again sure run no no run it from the base but select
the jdbc one this one yeah we may have done the in memory I think we might have done the in memory yeah oh interesting I
think that's a bug I think that's a bug because if it's gonna show oh actually there's no indicator at all it's just the
Run button huh okay that makes sense right there's actually no indicator of of uh there's no check mark and so therefore
it it's as if it hasn't run it at all which I guess is not technically correct but I wouldn't consider it a bug at least
it's not misleading all right let's move on um so let's uh for all songs let's um let's actually what we should have we
we need to test the zero case but jdbc so um let's go back to our jdbc song Service Test uh and let's pass in a
reference to and you can quick fix that yep create the Constructor and uh quick fix that so it it yep and then uh uh for
all allall and we're going to need to map the song dbo to a song so let's do on on why is it not uh because we forgot to
turn into a stream oh crap find all returns in iterable uh which uh can we go to this to our song jdbc repository don't
don't scan for it just go through it uh so we're extending crud repository repository looks like it doesn't exist when
did they introduce that can you Mouse can you hit the right arrow key right arrow key yeah oh because it's list crud
repository ah tab not enter adapter uh so for find all what does find all return can you hit control Q on the find all
so we can see what it returns thanks yeah I trying to figure out how to get that okay so that returns a list so that's
what we want um so let's now now we can do a mream do map cool I think I have somebody here asking me a question hold on
a second all I wonder if we could create our own find that okay I'm back so you were saying to do a two list and then
map uh well it already is a list so we just need to do a stream.map like that yeah formatting and what we want to map is
we want to map um so we're getting song dbos we want to map song dbos to whatever the method is that I forgot the Syntax
for that uh so it's going to be colon um sorry not this uh song dbo colon colon uh uh do we have a method that down no
we don't I guess we don't let's uh right so we just created the object so we can save it we never we never uh uh
converted it to to a song um so let's let's do that let's provide a method do you want to put it like after the
Constructor and before the Getters yeah song and I usually name this uh to song yeah split splitter rators are are
annoying there's a way that to convert iterables into split into streams but it's annoying and if we don't have to do
yeah let it auto complete plate sweet all right so now we got um now we go back uh can you insert a line on 42 and a
half yeah good idea yeah now we can go back uh now we can use the method we just created yep uh and since we since we
returning a stream already this is all we need to do oh right it's already is but it does oh the two domain returns
stream of songs instead of a stream of song DBS right got it now normally if the conversion between the dbo and the
domain object were more were any more complicated I would write a test for that but it's pretty one to one right now um
so we can we can just drive it this way um so let's go ahead and run uh the zero test um actually let's run all the jdbc
yeah and so we expect the sort of the zero case to continue to work because it got nothing from the database uh and it
Maps it and which basically should be empty right so new repository zero songs that's fine the Mal form we know Works um
the ad song uh doesn't work because we're not adding yet but we verify that at least we get nothing back for an empty
repository so that works now we ad sorry brain fell out uh we need I was reading the chat and that's what distracted me
uh we need to implement our ad method at the bottom oh oh yeah clearly uh okay so and so it's it's pretty much
delegating to the so most of what this adapter does like many adapter is a lot of Delegation to thing we have an ad uh
so the repository the JBC save um but it expects a song dbo so we we need to right so we when we pull it out of the
database we convert it from dbos to songs this we need to do the opposite is there a actually I forget a a from I guess
you would call it uh it does not we might want to create one but for now we can just put that in the adapter yeah right
here we'll say new I have to just extract one at a time oh it's wants the ID first oh no so I'm surprised the machine
learning didn't kick in and say oh let's just do that because it is a onetoone yeah it's mapping it clearly knows it
because it's um highlighting as the most obvious choice the correct Choice yeah is that right yep okay so now if we
rerun the test so now our expectation is that that test should pass the one that checks for so first I asked why do we
have architecture on our tags um mainly because uh there are essentially two different kinds of tests there are tests
that are testing against the the core of our codebase um uh which is our domain and application layers and those are
what I call IO free and they run fast um and so what I end up doing is I end up tagging tests that are slow so that I
don't always run them and then as uh Mike has shown here I have different we have different run configurations for
running IO free tests those are all the tests that don't require external connections infrastructure iio whatever you
want to call it um and then there there are tests that are specifically database and if we have other dependencies on
other IO then we'd have tags for those as well so that way when we're doing behavioral development in in our domain um
we're not running a tests it makes life so much nicer froster to have the fast tests and run them most of the time let's
see do we have a failure so test oh we're not clearing out the repository between tests yes and this run it again the
order should be randomized the order is is pseudo random there's a somewhat of a predictable but it isn't defined um so
if we run again again do you think there's a chance it it'll pass I don't I don't think so and it doesn't matter anyway
but this is actually what what what Jonas was talking about earlier and I re and I remembered what I what I do is in the
before each I do a delete all or truncate either way um there is a way to say uh dirty's context and for each method but
that's test and so um and the reason why I forgot is I actually have a base class for sort of all of my test container
ones then it implements the the the before each to do that already um so I think the transactions are there but we don't
roll back um so un unless we have to add them yeah the dirty context don't I don't like uh because it it actually
dirties your application context which is terrible um uh there might be a way to do it uh some um I'm looking at my test
to see what I do uh are you doing it before each and do actually I don't I don't interesting I guess because I generally
don't do a find a find all uh which is um yeah I'm a little bit confused now I'm looking at this a little closer so we'
re for each one we're calling song repository which for the jdbc version each time is calling new on song jdbc adapter
on the rep oh the repositories right why it's still okay never mind yeah can you scroll up to see what the annotations
are yeah yeah so we do a database replace none so that we don't have spring automatically start up an H2 database uh
there might be some other settings or must be something I think we I think we should just do a before each and and just
delete the database okay you might do that at the base Well it can't be in the base because we need access directly to
the to our injected song jdbc repository so let's add a a a before each method do that here well you'll want to do it
after 27 true I was just wondering if there was a oh there is it before well they call it a setup method oh because
that's what called yeah yeah name uh and let's rename the method to match thank confusing so I want do is just call um
song jb3 okay did it autocomplete that for you or did you it did okay so it it knew what we wanted um I think I think if
we want the transactions we have to mark the test as at transactional um I wonder if we should first up here as a is it
a separate Yeah so basically uh yeah say say and then transactional um and let's comment out oh you already commented
out the before each yeah so let's try let's try that because I think by default it doesn't actually turn on transactions
per test method it does it maybe not at all I guess let's see nope I guess not yeah so let's just let's delete that and
go back to the I know I I thought there was some way to do the the transaction but let's not let's not worry about that
let's just get it to work okay letter rip yep we're using J jdpc Test uh Jonas and there might be some I have to go look
at this again there might be some every time I look at it stuff changes who now a bunch of green unsurprisingly um yeah
uh except of course the one that we haven't implemented yet right because the other ones are using uh just the right so
the first one the first test um doesn't work because it's using search by theme which we have not implemented yet um
what and the second test is uh just for empty so that of course works then the next test is that one works because our
ad Works um right because we're saying ad song and we're creating it and so all songs should return that basically
because we have a we have save and we have our our ad turns into save and our all songs turns into find all um so
anything that uses all songs or or ad song will work so that of course test uh so this is bulk add it doesn't import um
and so then it does an all songs to retrieve them yep and the Mal form fails prior to anything else so yeah so we got
one test left which is basically can we find them service should we take a break uh yeah this probably good good time
for for a break so um we'll take a break and then we'll we'll implement the last piece of it um then there's probably
some wire other wiring that we need to do to get it to the application itself to use the real database uh and we'll see
that when we come back cool so here's our our coffee he all right um so suiga mentions this which is what I suspected
because I looked at the docs and actually transactions should be enabled um but because we're running from a subass the
tests are actually in the base class and I don't know how that works um we could try putting transactional on though
that's generally bad because we're mixing uh we're crossing the streams we're mixing uh our spring Bo framework into um
nonframework stuff uh so let's let's let's just try that um Let's uh comment out the uh the delete subass so in the
before each for this in the um you're saying uh you're you're saying put transaction on the base class yeah it's let's
try that and then let's and we'll try one other thing and then we'll it so let's yeah let's run the jdbc song service
test because what I'm not sure is how annotations get uh oh okay let's just be again so it does feel janky having
transactional in yeah that's not a if that's yeah that's not a good long-term solution um are we did learn but we've
learned something yes yeah so that's valuable uh and this is why I haven't run into it because I didn't do it the subass
where I did at the delegation way where I where my uh my base where I didn't have subass I basically had a class that
had the database transactional annotations on it and it's it had the injected reposit jtpc repository and then it just
called over to to to the actual Test implementations passing into a parameter awkward but uh but it doesn't run into um
what we could do if we inject the um what is it inject the platform transaction manager and call a method that basically
turns on method um and we're doing all this in order to not to avoid putting well to avoid putting transactional on the
base class well that's for sure but I mean can't we do this without even and just not have transaction in the base
subass just have that to delete all well but that's extra work because we could uh we could just turn on transactions
and then that like this works okay because this is a single table um but it's not as reliable as as as transactions um
let's try that so let's autowired all right Jonas have a good night yeah work from home tomorrow yeah uh so let's do
another autowired below have and we're g to uh autowire the platform transaction manager that and then in in the method
let's all because we only want to turn on the transactions once yeah before class oh but we won't autowired all right uh
yeah undo that um so let's put in the before each let's manager um or is a test transaction that we need um never mind
there's there's there's other stuff we need to do that with the test cont test test transac template and stuff like that
so let's let's not do that what we can do though instead of uh um uh instead of doing a delete all um is we can autowire
so instead of autowiring platform so keep the autowired but replace the platform transaction manager with Flyway yeah
that and then on Flyway I believe we can call clean yeah let's try that do you like double spaces after the uh or single
I don't generally have double spaces yeah I don't either I just were there so let's there so what Flyway clean does is
it basically asks Flyway uh no to clean oh but it doesn't migrate um I think we want to do that after each or do we want
to do that after class no that's not going to work you know what never mind let's let's forget that um because that's
actually going to slow the test down a bit so I I think what we have is fine for now um and we'll eventually want to use
the transactional so I'll figure out a better way to do that so get rid of this yeah get rid of that bring this back in
yeah uncomment that and let's make sure that everything excellent um all right so now this this one is failing because I
can't find anything because our fine by theme doesn't do anything so let's and let's write that code and it's very easy
code because it's just connector code find by thing you mean search by them well it's search by theme in song adapter
it's fine by theme so we need to adapter is there a way to say yeah you can you can jump to implementation if you want
yeah if I do that I'll jump over oh that's see memory one uh you have to there's this different keystroke to to find
implementations B wonder if Control Alt click Works yep yeah so that shows the implementations I just think of of that
as sort of heading going down the the implementation hierarchy right um so we don't want to return a list of uh we'd
like to return uh something from the database and then we need to do the same mapping before oh I see right right right
right so you could probably extract that and and since we're doing that multiple times and where is it this okay yeah
although it's really just one yep I need to do stream map because fine right and then we need to do a two list because
that's what caller is expecting all it because we know that the query works because we have tests directly against that
um we know the song service works so therefore assuming we connected things up correctly which we did that all works
that's it cool so one thing you'll notice about our adapter is it doesn't do very much it's very much uh transforming
objects to and from the database objects and the domain um and then calling the right method on the underlying
technology to do the right thing you want to turn this into a factory method uh we probably want to have that as a
factory method on the song yes no did I pick uh because you selected the wrong stuff so don't select want and then we'll
move it over to S DPO MH so we call it what um R domain no um create well it's a factory so create song um create song
dbo I I think from is fine because it's transforming from a song to a method that will be obvious once it moves once go
uh you'll want to make it static first otherwise you won't be able to move it right all right suiga have a good night
see you right yep yep so what does it look like on the side so now we can get rid of the static uh well no it's method
it needs to be a static oh right it's a factory method on the two domain is not a static method because it's it's you're
asking it give me a you are an object give me the domain version of you but here we're we're going the other way right
and this is because of the direction of dependencies that um our dbo can have a domain because you might think well why
don't we just have a two dbo on our song bad um let's run all our tests and if everything goes well we can all right all
of our tests not just pointing but implementing uh we finished implementing yeah yep I guess we should use the exact
name John S jdc sure song jdbc adapter these afternoon ones are a little bit rougher for me I'm definitely starting to
fade I was going to say I think we're we're pretty much done um we can look at the uh um we can look at our startup code
because right now I think we're using an in-memory repository and we're not going yep right so there on 18 we're using
an inmemory what we want to do instead um is have uh so we want spring to provide the concrete jdbc repository um and
then we're going to create song service with that repository p in so the way we do that is as a parer to this method to
song Service uh we want to reference the repository we going to create a new Constructor um I'm sorry we don't want the
repository we want our adapter uh we need to create our adapter which is the thing that implement this is where some of
the naming gets a little confusing so that's what we want because spring needs to provide that then we need to wrap it
first what does that take for parameter and that takes the the concrete jdbc repository yeah and then that is the that
implements Our Song repository interface um so I'd rename before you do that rename the parameter to be song repository
uh and then you can wrap that yep and then that we're going to pass to s Service instead of yeah if you change the the
the Declaration uh and not have it a song jwc adapter but have it a song repository that will make it more clear because
it's the adapter that implements the port and song repository is the port um but the names are a little little bit
confusing here uh we might want to fix that think think about fixing that um but now so now if we run the application it
will use uh a real database to run the app not a did you run it Oh I thought I did no you just selected it oh you're
right age old problem well that's why I don't use that because it doesn't run it when you select it um the shortcut to
to the Run configurations will actually run it because you'll select it and it will it uh Why didn't it why does Flyway
not happy back to the top and then come down um no no no it's it's fine uh looks like the migrations got messed um uh
let's go to your Docker desktop and we'll just delete the container and start over actually we could do that from in
here uh although I don't know why Services aren't showing up it's so weird like on your intell like who windows are just
missing it's so odd I don't understand why that why that happens because what I have at the bottom of my intellig one of
the tools is Services which you don't have um you can go to services and then and then connections from contexts no uh
which we want is Docker services and I don't know why it's not showing up in search you have to escape out of that yep
um and look for docker and then in parenthesis want and if you uh just want to pin it yes like once it's there it's
there but I don't know why it it doesn't show up by default interesting there's no okay so there's not a pen to keep it
here no because it's here it's just here um there's a way to remove it which iend end up having to do with stuff but uh
um question is why is it not showing uh I don't know which one it needs to connect to um let's go to your Docker desktop
because I'm not sure on Windows how how this works so look on let's look at containers there on the left so we've got
two containers they're both exited but we want do is get rid of the container so it gets recreated um oh this so let's
yeah let's trash that one actually well you should probably delete both of them that's just a welcome container and then
delete the other one yeah all right so now let's go run the application again what happened was the container was there
and so the container had all database stuff uh and Flyway didn't know how to migrate because the different and now it's
now I've got to do the um all right let's paste some stuff in okay now this one we want to do I guess we can do a
certain number of um as long as it's got the required ones a work oh go do the header don't I yes top interesting to see
what this how Point ah there we go and we just added something about them I think if you take off the the query part it
will show the form UI or not there's probably a different that's probably the actual search endpoint there's probably
another endpoint I don't know I don't remember what it was unless we didn't implement it I don't remember I don't
remember if we did or not either Let's see we would be able to find that right yeah in our templates resource templates
scroll down scroll up resources templates uh I guess we don't we have the results page but we don't have the the search
page right right right we were just doing it VI the URL and just yeah yeah so um all right let's update jira and then uh
and then call it for a good yep so we did that then that y did we run them both yes we run all of them yeah oh right and
all because they're and we wired up yep and so we can Mark jir 89 are are are epic as being done epic jir 89 cool uh so
next time what do we so we're done with our persistence what do we want to do next time have a search page search page
we could do AR Arch unit or Arc unit let try to pronounce that one um I pronounce it Arc unit because I figure it's the
first four letters in architecture ah um we could I mean could to the search page I think I think we should focus more
on features than than yeah an arc unit I can throw an arc unit um so I think this is a new theme right so this should be
a top level thing right do we have anything for is persisted datab totally yeah oh there's this one right um it's done
right now I mean maybe we want to pull that off but I would I would close persisted database so you're saying pull this
out as this yeah because that doesn't matter until we actually do like it says um until we have modif song proposals and
stuff like uh so we got our UI stuff so we add so done uh no these are oh these are individual that's an indivual this
is not this is not the bulk no right the adding songs in bulk we'd have done 122 no that's songs not bulk but well I
guess oh adding adding multiple rows I don't know what that was all right well then if we don't know what it is it's it'
s not well defined enough so we should delete it yeah I'm just taking it through my as the product owner I'm as that for
a second um he talked about adding a song so is adding songs in any way different than bulk no I can't think of a way
that it out um so then yeah I mean we want some convenient way it's like I want to add three songs but I'm not copying
it from the spreadsheet I think we can tackle I think we can discover that requirement if we need it head search page to
UI yep and we were taking that one all the way up to zero zero col um that one will take us all of like 10 minutes uh
yeah so maybe next time we'll start out with looking at our all the way going back to our mirror board and saying what
next major feature do we want right because we finished song Imports and database since now we have a real application
right you could use it um and we could deploy uh yeah that's done 31 is is it's not deployed right that's the one thing
we haven't done yeah we haven't deployed it um the to production uh will they'll if we want we that Y and then next time
we'll uh yeah so as part of that we'll need to to figure out what that um just skimming ahead to see anything else jump
I think we can drop 118 because that totally changed because we're persisting in the database so I out yeah all right
cool I think we need probably commit yeah let's commit and push and then uh then that'll be it what did we do in themes
uh oh that was that that was that was the final wiring it up to the application yep it's going to run all the tests
before it does the push right that's the annoying part well we told it to we could not tell it to we could tell it to
stop doing that but yeah were there any other questions that we Mr so it thinks it thinks some test failed did test
actually fail I think it considers oh because we're now hooking it up to the application we might actually have some
test failures yeah yeah uh we'll we'll figure that out uh next time but let but do a do a push push yeah and then push
we're not doing CI out to production deploy right I don't think we are no been so long since we me I mean if if we were
then we'd push and the wouldn't change production because the CI would fail right yeah all right cool so part is
figuring out what these are oh I know what that is it's it's it's the same problem as before it's it's uh uh the MVC
tests are trying to bring up stuff that needs ends up needing a data it's it has to do with the database stuff um so I
I'll figure that out offline just fix it all right so that's it we we finished our database that that didn't take very
long really yes um awesome it was uh we'll have to figure out some of the trans the transaction thing is kind of
frustrating I'll have to see if it a a better way to do it um other than adding at transactional to the to the base
class which I think I'll I think I like better just doing the delete all I think that's fine yeah for now I mean when we
for now yeah yeah yeah and then are we uh confirmed for our next one uh I don't see it's on the calendar but I don't
know if we've did we confirm um well the tenative for tomorrow you said was no yeah that a no morning you right but you
said the Tuesday morning was not good no no no a week from oh a week from tomorrow yeah um because then you have CSS the
rest of the week maybe we should yeah we'll we'll we'll figure it out it probably will not be this week so yeah so I
think it's next week when we're back y all right folks thanks for hanging out with us uh and we will see you see you
next
