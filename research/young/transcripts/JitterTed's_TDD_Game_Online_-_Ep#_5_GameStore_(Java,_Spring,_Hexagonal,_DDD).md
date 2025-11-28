# JitterTed's TDD Game： Online - Ep# 5： ＂GameStore＂ (Java, Spring, Hexagonal, DDD)

**Video URL:** https://www.youtube.com/watch?v=fNohT8Z5KcU

---

## Transcript

Al righty welcome folks hello astd hell Jonas sorry about the later start I try to start early but didn't work out today
or at least earlier uh let's see let me push the right button right all right welcome folks um this is episode four or
five already I've lost count um so one thing I've been doing is uh uploading uh all the videos to YouTube um unlike uh
previous series uh where I've failed to do that when I'm streaming only on Twitch uh I'm trying to do that for this one
and then sort of catch up on on other stuff it just takes so long to upload takes so long to upload and then for it to
process it uh so it's like I can only get two a day so we'll see we'll see how that goes uh let's see let's go here
there we go yeah so if you're subscribing or getting notifications uh you'll you'll get notified so there is a playlist
uh let me go dig out the link for that that's not it that's not it oh good yeah so that's that's that's my intent is um
especially for this series because I'm kind of this is more a a play little bit of play than than work Embler I enjoyed
but it was a bit more of work oriented so this is more working playlists and there it right uh and eventually I'll get
streamyard to be able to work properly um we'll we'll see how that goes I'm trying to get it so that I can multistream
to both like I do when I pair with with mik uh but um doing it through OBS which is what I use for for this layout and
and so on doesn't quite work as okay all right um so uh let's see where we left off let's go to Tada so for those of you
who are joining fresh uh this is the game I'm working on and um basically I when I have a few moments of downtime I'm
basically try and juggle juggle this layout still feel like I have a few more juggling to to go but it's got just about
all the information that that I need one thing I realized is when I was doing um uh the the the risk and commit tracker
layout is oh I guess you need you probably want to know that for for the other players and I'm like oh so all right I
guess I've got I guess I've got room um here under underneath to to to display that so I'll have to add that to my to my
mockup uh what else is change that's pretty much it um I haven't 100% decided whether I want these sort of as visual
indicators which I I do like like um so saying that I think I'll probably keep them as visual indicators but of course
as in everything else that's not where we're going to start where we're going to start um uh so my my goal my sort of um
my my near-term goal is is to get a playable version uh of of of this game um in it doesn't have to look good doesn't
have to have the graphics although those are fairly straightforward because they're just images uh so that I can that I
can play it remotely that's my number one thing um yeah I I I don't know I'll I'll play around with with some variations
on on this uh I certainly over here I I might just have a number um otherwise it gets it might get too hard to see for
individual players what they're and really that's that's all I care about we'll see I might display both number and and
sort of stuff like that but that's that's a bit a bit of bike shedding we're nowhere near ready to do that um so where
are we uh right so when we had left off last time um we were I had remembered oh yeah I want to do event sourcing for uh
for the game so now it is uh it is event sourced um so one of the the key aspects of event sourcing is uh commands don't
change State directly commands generate state uh so let's see um so we did all the fense source aggregate stuff I basic
um went quickly with that cuz I stole uh a bunch of the stuff from um the blackjack game that we did event sourcing on
in an ensemble that I run and realize that this command method this join method so command methods as a reminder are
things that request change in uh according to command query SE option from Burch and Meyer um and I talked a bunch about
this last time uh you generally don't want commands returning values um because it makes it hard to get at that value
later like how would I get this player if I didn't happen to save it uh how how do I get it back how do I retry things
all sorts of things like that so um what we want is actually to provide a method that returns a player based on the
person ID so in order to do tests so it looks like all our tests are tests uh that one we might be able to enable this
one not yet um so let's before we fix the join thing let's just see if we can get this test to pass so game view done
because we need the read model um so one of the things about event sourcing is um with typical State sourced or state
based storage you store an object and you retrieve that same object and you can and you can view it so if uh so if I
stored a game in in the database as as an object with the values in a table row then I could easily query that uh but
since we're storing events you have to basically play back all the events to find the current state um now we'll
probably do that using the same model to start with with but eventually we'll want um to separate our our our read model
from our What's called the WR model um not as in right and wrong but as in the uh State Change Model um but I think
we'll I think I'm going to defer this until uh this is complete so let's go back here um and so we're using this join
method in um not too many places we're using it in a couple of tests those are going to be straightforward uh those don'
t use the return values the only one that actually uses the return value of join is well besides the production code
itself uh is this one um except even here we don't pay attention to the return value so uh so what if we so who actually
is holding on to the return value here all right so then here these tests are change um actually no these won't have to
change um this is playing and so one of the things I'm doing in this project is trying to use names that are not with
the typical suffixes so this is actually a an application service or a use case um but it can be hard to tell what it is
by just looking at it um what was the what was the a uh so do I want to include some lightweight annotations on this so
I have been thinking about including molecules uh and is oh and no application yeah yeah no no no service manager imple
stuff um uh so the J molecules DDD has so the architecture has the layering things I don't think I want to do that yet
uh but the DDD stuff um yeah has the entity value object Repository um so let's see so it's got the identifier aggregate
stuff which I do want to add but not yet um does this have application service it's really interesting because like I
use a layered hexagonal which isn't true hexagonal so uh it's a bit different um so let's look what here uh they're not
types cuz all the types are around identifier aggregate service and so that'll just be an yeah I basically just call it
testable architecture because that's that's that's what it is um but uh but it's it it's it's not as I don't know doesn'
t doesn't evoke the same the same kind of identifi so huh so what's interesting is this service what I really want is in
the application layer I want a use case because so it's not a service because it's not a domain service um and the
reason why is domain that uh I might have to talk to to to Oliver about this uh because I'm curious what um what his
thinking on that yeah I don't uh honestly I'm I'm a bit I so alist Coburn came out with a book on hexagonal architecture
that he self-published um which I basically bought but I have not looked at yet so I don't know if he talks about the
options for what to put inside the hexagon uh in his original write up he basically just says application goes here um
but for me it it totally Mak sense to layer it as domain and and um so if I go though I kind of have it's unfortunate
that I kind of have to pick from one of these and and none of these actually fit cuz it's not really cqrs and it's not
really hexagon as we um there's sort of onion which is which has two modes but even there like there's application
domain and infrastructure so here application and domainer are are separate um but in hexagonal uh there's just um
application with with no domain CQR hex yes it uh this is this pretty much is going to be CQR to I might I might end up
working this project um and creating my testable architecture uh cuz I don't use primary uh I don't use primary ports so
that's the other difference I don't I don't I don't I I don't name them explicitly as primary guess I guess this use
case is the primary Port but I I find that I find that confusing um all right I I feel like I'm bikes now so my main
thing was to say this is uh uh it's it is basically an inbound Port but it is a class um but it's also very command
oriented uh so cqx might might be the right name for this um anyway at the application layer so we talked about command
query separation uh I find that it mainly applies to things that have state if it doesn't have state those rules don't
apply so all this is to say that you know my my main intent in saying that this is application use case is that I am
allowed to return an object method so game itself should not not must not but should not um but this absolutely can
return object cuz there's no state in this class it might have dependencies but there's no there's no domain return uh
uh value uh man query so what I can do then is I can split this method uh into two pieces or sorry split this so instead
of returning this directly because I can't do that um I basically want to do something like uh call this and then uh
return something like game uh players Dot and I'll refactor this uh but players dot what is it f um not filter want I
guess we'll stream find uh well that won't work because we're just doing a fine first um right fine first basically uh
Returns the first element of the stream but we got to narrow down the stream first so if I do this this is not a
refactoring because I will likely have broken something uh I'm going run all the tasks because they're still pretty
pretty quick so I C certainly expect something to break yes all right um so what I want to me uh what's the type of this
oops that's parameter in info type info context info what is the type that this is what is the type of players players
is a list of player okay so there's a player thank you I don't know where my inline hints are for stream um and we want
where we want to keep where person equals ID that's what we want I don't know where my inline hints are hold on a
annoying so that's inlay chains I don't know why I had the turned go uh X proof do API requests and database entities
end up getting converted to domain objects in my app otherwise I don't have a domain if your app is taking API requests
Andor writing to a database and you have Behavior you must be converting and transforming those domain objects to in
from uh what I call sort of generally Edge objects your database objects your frontend or or API dto those all all need
to be converted into value and and domain objects that provides decoupling which is important uh okay so we got our
players this is terrible of course we don't this is feature Envy but that's fine we're we're we're in sort of refactor
mode of focusing on on fixing so that all works um then we should be able to go here signature uh excellent so I don't
need this and it uh X proof asks how do I deal with breaking changes um can you define what change all right so now the
collar is still ugly uh so let's clean that up so what we want to do let's refactor this to a method which is um player
4 uh we don't want to declare this static and now we can uh we don't want to do the get uh but we'll write some tests
for that so we're going to move this to game method uh and so now what we have is we have what is a fairly typical
sequence of methods in uh our application use case methods which is perform a state changing command and then do a query
against against the object so here we're saying join and then we're saying uh can you tell me what the player is for for
that person uh technically though we shouldn't be asking for person we should be asking for the person's ID so let's
pull this out parameter and run our tests uh so says the a your API has a new required field and there's no default
value um who's requiring that field is the server saying hey clients I need you to pass me a new field or are clients
this uh so I don't like breaking changes um because clients then get into trouble um this is where if you have to do
that you may have to so if if you own the client then that's fine um then it's a new feature and you do what you do when
you do new features which is test drive it outside in so the real question is is what do you do with uh with the client
do if you don't own the client um then you're going to have to uh provide Backward Compatible API methods and verion
version your apis so I guess the short answer is this is not an architecture problem this is how do you implement new
features right so saying that the server you're there are requirements that require a new field that's a new requirement
what do you do when you do new requirements you start with a failing test so your failing test is UNP passing in this
field and I should be able to observe that that field is some something does something to your system maybe it just is
stored and I should be able to find it that test will fail and then you basically implement it system yeah so these are
all questions about API and and backwards compatibility and deprecation and and migration and all these kinds of things
um the architecture doesn't have an have uh what it does allow you to do because you got your dto separate from your
your domain objects is it does make it in some cases easier because you would have the dto for your old API and that
remains uh and then you have your dto for your new API uh and that you upgrade um but as you said if you don't have if
it literally is a new new requirement uh then you can't do that um but you can always do that that's a business decision
not a technical decision so somebody saying X is now required there is no default they have to understand the impacts
that that's going to have on whatever clients are out there and again that depends on do you control the clients or
these outside your control and by you I mean your you and your team um what we'd like to do uh uh let's let's actually
finish this refractor so this is is oops that's not it this is um commit this uh so game all uh we should test that uh
when a player joins we can we can find them um we can Pro because I'd like to simplify this this seems really uh
unnecessary because we literally have so events project State uh so that's new game player join results and player added
to assert that uh game do player 4 um that uh Returns the player um do I care about the contents of the player no I just
care about the player uh its person ID is equal to pass because it's just adding an assertion onto one we sort of
already have so now what I should be able to do uh player map ID excellent uh so X proof ask for breaking change any
concerns that the domain objects can be in a weird State API requests and database entities get converted to domain
object objects so when you return receive an API request convert to a domain object domain object will have the new
field when you fetch from the database may not have that field uh we don't do that you got to migrate your database as
well um that's part of of that um again there's no getting away from that so even if you didn't convert stuff to domain
objects adding it to an object that is shared by the API in the database uh you're still going to have to migrate your
database so you're not in any different shape it just means that you can more easily do one without the other so for
example if there is a good default you might be able to read in a domain object and have uh that field filled in with
the default if it's not available but if it's truly required like like you propose you got to migrate your database so
what do you do with all the ones that didn't have that value that's why I think this idea of a required default brings
up the question of then what do you do about all those objects that didn't have that value there must actually be a
default unless you're calculating it from something else uh or you need it from something else and and you're going to
slowly migrate um it's not an easy issue but the business uh is is the one that's making the decision because what field
is now required that wasn't required before do you then version your your objects themselves um so migrate depends um by
migrate I mean update your database schema so that it's now compatible with whatever you need but somewhere you're going
to need that data um it's actually not a hard problem it's a wellknown Well understood problem what makes it hard is the
business doesn't like to make those decisions because they may not understand the impact so if we said uh we're going to
now require passport identifiers for these people it's like okay what do we put in for all those people who for whom we
didn't ask that information uh well uh right I mean that's that's a business um because what you don't want to do is is
have to version your database um and by the way this is where uh event sourcing can sometimes be be helpful this is a
business so so I want to reiterate this is not a technical decision this is not a technical problem this is a business
problem they have to understand the tradeoffs of doing it one way or the other uh and often we're not as developers not
often good at expressing that but this is literally a business decision they have added a new requirement okay I've got
500,000 entries in the database that don't have this value what should I set for that and they have to have an answer
they can't leave it up to you decision and there are lots of decisions like this that that developers make assumptions
null might totally be valid it might totally be valid um I probably want something else but null is is totally valid uh
I might want an actual representation of that um but databases are are are are great at handling NS much somewhere that
N I would hope gets translated into something more useful um it may be that you have you know to use like my random
passport ID thing it may have a passport number that is well defined as being we don't actually have one but again
totally a a a business decision and if the business is not willing to make that decision then we developers will say
okay if you're not willing to make that decision we're going to do what's easy for us and then you give tell them what
the repercussions are I would not actually use null I mean it can handle it but I would not use null because now you'd
have now you have to have well what does that mean inside domain you the last thing you want are are sort of null checks
all over the place right that's that's you know been there done that uh you want some value that is interpreted as we
don't have it could simply be blank depends what the blank and where where different kinds of business process comes in
is it may be something like you know we have a new requirement because of whatever that we have to get like I said your
passport ID well now you have objects data that are in different states one is completely up toate and valid the other
one is we haven't collected that information yet and so the next time the person logs in you take them through a process
that collects that information and over time most people are then converted and then at some point you have to write
this is this is what another form of migration um but again it's it's it's totally all like you can tell like do we put
people through this process do we force everybody to go through this process do we contact everybody to to have them go
through the process do at some point we say you know this is just the way it is and it goes on decision the way I think
about null architecture is the only place nulls can exist are in the edges in dto maybe in database objects so even
there I'm reluctant to use them but once you got a domain object there shouldn't anywhere yes and replacing a null chick
with an optional is present is uh sex proof in terms of an OB so I I I don't think it would I'd use the terminology up
to date um I think what I'd probably say is uh has all has has this information um and then there's some process there's
some part of new part of the system as part of this migration you might have to implement code this is very um this is
this is to me it's it's very similar to to feature Flags you're putting in a bunch of code that may not be used all the
time uh that it depends on context um but instead of sort of putting something in to turn it on here we're sort of
putting something in to transforming from one state to another uh you've basically got two you know domain objects that
either has valid passport or and does not yet have valid passport um and then that will affect some other process like
post login you might say hey we need your passport and takes you through that that process um but the only the place I
do null checks is at the edge this the same place I do validation at the edge all right so I set up basically I treat
the inside of my hexagon as no nulls allowed because if I get a null from an API nope not allowed um unless it's unless
that null comes in because it's implied to say don't change this the state of this thing like if you're doing a a put um
but that's an API question at no point domain so validation happens at at the outer edge because once you get into your
your uh your application layer you're now working in in domain domain objects and so that's another reason to transform
these things is you validate your incoming request and from that you create value objects and as part of creating those
value objects you're doing that validation uh and then that becomes domain objects and you don't have any nulls this uh
so passport ID is not is is has a type right it's likely going to have not just an ID but but things like what is the
country of or you know of this passport and then some identifier so it's an object uh you can have uh what I would uh
consider an sort of a an empty or or or blank version of that and this is the null object pattern and so you basically
create an instance that is the uh invalid passport instance and so it's going to have to have some special value in
there so you know and so part of that object might be you know have we validated this thing or is it not you know or is
it empty right so so even that little what what seems like a single field becomes this Rich object of a little State
machine right it's not been entered yet entered but not validated and then validated and that's all in that uh passport
object and so then you can represent it for everybody who hasn't entered it yet as a passport object where has not been
entered yet and so your database repository adapter is responsible for translating however you decide to store that in
the database to a domain object which is a passport and the instance is not yet entered and then when the person answers
it it's now entered but not not validated um and then eventually it gets represent well nothing's ever always but more
often then then you might think is you have to figure out what does it mean for this to be null what does that mean and
then you create an object that all right um so we are now uh in event game so we've got uh so let's bounce out to the
lobby and by the way speaking of Lobby I looked at uh uh I wanted to to grab the the music for it except that it's not
clear if it's still in under copyright so I don't want to get a copyright strike uh so I'm not going to um have the
music play until I get a little bit more clarification about about whether the um whether that song with a little
cartoon is is copyrighted or not it appears to still be copyrighted but it's unclear okay so um in our lobby what have
we got we've got show Lobby which shows the name and uh game views and so right so now we should be able to go through
at least one of our dis tests uh which one so if we if we try to run this can we run it directly even though it's
disabled yes um um if we uh uh host a game we should be able to get um new game with handled is created upon host new
game yeah hey swegi uh so and so we're currently doing is we're Faking It by storing the game views here what we like to
do is actually pull those repository um we got our game view anything all right okay so we don't have um me add that
back uh we don't have assistance for a game we added event sourcing but we actually didn't save that information
anywhere so let's go do that um let's go update jira so uh we're not actually done with with our persistence so what we
want oh I forgot to turn Cody back on I'll do that in a uh which will require us to uh and then the implementation uh I
think though for now is oops this is for the real database thank you for your name generation skills astd okay so let's
start there um right because once we have that um then we can uh move on and then uh once we have uh doing that yeah
except if you redeem those points I have to name it exactly that in my code so Choose Wisely uh okay so let's put that
aside uh we're going to put the lobby aside um don't need that don't need um actually I can't work at this level yet
because I don't have repository even though there's not much there I still don't have a repository for that uh so if we
go here um so what we want is uh if we create a game we should be able uh so that one not just yet uh so this want this
is basically we're doing this because we actually are trying to get this to work and the only way this is going to work
um is if we've got uh repositories so I am doing a bit in sort of middle in cuz it's at the level of the application
service I mean it's basically because disabled so I think that that's what's triggering this one so I think that's fine
uh is this going to be disabled uh no because it well hm can I do it without introducing repository yet no cuz I so this
is very much more like a command in cqrs uh game creator has basically a method to just say create new game I don't know
that this use case I don't know if there's anything case in which case then not going to disable it because there's
nothing else to do other than create the repository yeah that's what I was thinking of game creator holding on to the
state directly temporarily um but if the only way I can observe what it what it did is by looking at what's it going to
do uh it do I could do output tracker but that right and that's why I was thinking like if I add a method here that's
you know find game by ID or find game by handle that's a different use case um so I wonder if that means I want to start
somewhere else because if I so I could write this test um right which basically says you know create game and then is
game in repo well how do I determine if the game is in the repo do I do a find by game ID or by yet whereas if I uh and
so basically I'd be defining the repositories um API in a test now the test does give me some sense of it but I'd like I
I like to to have those kind I'd like to have that interface uh be defined needs um so the question is is what part of
the code needs to find games and then I can go the other way around is uh in a test directly put stuff into the
repository um and then convert those into game a like I feel like um adding on this yeah I mean essentially I'm creating
an in-memory version of the repository as my yeah I I think I'm I'm with suiga on this like uh probably just repo I can
always add on other things as as needed so let's do that um so so we want to create the game via the game creator and
then see if the game is in the repo uh so let's do that so repo aha okay we can't find things in the repo uh alth I
guess if we do a find all then matter so uh now we want to do is we want to ask a game repository so we'll say game
repository now the name on this is going I've been struggling with the naming on repository stuff because in Spring
whether it's jdbc or or jpa or whatever uh the spring data stuff they call the technical implementations repository now
I don't have to call my um is a game loader it's also going to do a save so it's not just a loader uh now I remember
what I was going to use this is a game store because it's storing a ventri and stuff hey there singular singular atarian
uh so we're going to create a and we'll go ahead and create that class where is that going to go uh this will eventually
be a port start I don't know you can go and buy storage and so I'll do that yes grocery store is that where you store
your groceries that's where I groceries um and then we can go ahead and say uh game store doert that uh actually it's
game store find all uh contains exactly game uh that's going to be tricky because the equals is broken so we can
sidestep that for the moment um uh by extracting uh well let's let's create this first no it's not Boolean what is find
all we're going to return I'm fine with a list of game uh yes that's fine um let's just check that the name same not all
groceries need to be in the fridge I guess that's it hold on I wanted to pantry uh okay so this will clearly yeah this
will clearly fail because because the game creator is not talking anyway right um so game Creator um I'm going to rename
this one to be create null and then this one is going to be a create with uh the game store the reason why I'm doing
that is I want create null to create the repositor basically obtain the repository on it on its own uh so that way the
other tests don't care about directly accessing their store uh don't don't have to deal with it so let's go anything
should still fail with null uh and now what we can do is we can uh pass that along to the Constructor so Constructor um
no we're just going to create a new game store and that that should still fail in the same yeah I'm going with n nulli
for this because I uh I found that NBL are really um there's some part some aspects of testing without mocks that are
not quite compatible with um hexagonal testable architecture uh but the nullies absolutely absolutely um for cases
exactly like this like most users of game creator at least right now don't care about the store uh just get it from
somewhere um and so that um is there a way to find out which commands are available in twist chat uh if by commands you
mean the exclamation point commands no I'd have like I have like 50 commands so I don't think there's any way to get get
a list of them yeah and so uh James for recently made um at least sort of the the code base and and which is basically
the work shop Labs uh uh freely available yeah you uh so displaying all the commands that are available is not available
sort of on purpose um because there might be commands that are only executable by me help um yeah and the the Java
version of the output tracker uh I'll be publishing week um yeah so Discord that command Works uh okay so this test
fails why because the game store doesn't hold on to anything uh um instead of that we could return an empty list to just
change the quality of correct well it's not lying even if we switch to dark mode is that I use the light theme
regardless of what my audience thinks uh I just triggered dark mode indirectly didn't mode what did we say did we did we
like Oceanic or do we want something here usually when I select the new theme it changes this dialogue right away uh I
don't know sometimes I've seen it just so I think the Violet is is like I think the colors is like these accents here so
like if we switch to uh Oceanic there's a little so there's the accents and a little bit of the tint uh storm is more is
a little bluish and violet is a little more yeah it looks like it didn't quite it yeah it's a little broken uh let's
back and then we change it yeah it's not it's like it's not changing the theme I don't know I wonder if they broke that
uh CU I'm using the 20 broken cuz I bet if I causes yeah that's the way it should look so I think there I think there's
actually a a bug oh right blame me I'm oh there's an update I'll update you later okay um now that we we're officially
in dark timer yeah we've hit our our our quot of stream I think that's a minimum quot I uh okay so where were we uh the
test fails because we're returning an empty list um I'm not going to hardcode the return value I actually want to drive
the uh is it really a lie is it is it was Cody no it says there's an update to what they fix I know they changed they
were trying out the 40 oh great it's on GitHub all right never mind that's to Too Much distraction okay uh so what we
want to um no not create create new game uh this should be stored in in in the database maybe you're already up to date
I don't know are you on 559 or game um and gam store. saave game wow that's actually kind of impressive because yet a44
not found uh Jonas redeemed dark mode so it should still fail in exactly and I could you know go and test directly
against the repository but I don't see the need to do that uh so let's go uh we'll do a prepare ref Factor we'll turn
this into games oh yeah I guess it doesn't like you and we'll return oops I didn't want actually instead of empty lists
let's do list then we'll create a field from this and we'll uh field declaration is fine and we'll make this final so
that should be still the same result it's an empty list and and now we can do game now this isn't quite right um because
this is not using the event sourcing uh which is technically wrong sure so that's right that's done uh and yeah it's
good for for now uh so that's can stop faking the lobby can I move on test so create null it should use then ah so now
now we what we want to do is we want to basically have a test that creator and so here's what's interesting about this
controller is this controller is essentially will end up with at least two dependencies one for the game view loader uh
and one for basically creating games and so the question is do I pieces because this is going to use game loader test ah
okay so I think what I'm going to do then is not have this Constructor instead uh do I want to do a crate null with a or
I get rid of that completely uh and use the host new game directly let's let's do that so let's null uh and instead what
we're going to and then do uh a host a host new no I think I need to focus on host new this handle thing is is is
bugging me that's that's sort of where where I'm getting wrapped around the axle um let me take a break and then we'll
figure out figure out what the what the next break all right uh so let me switch back to light hang on to your hats as
they say see that work that changed everything interesting all right so let's take a step back what do I want from the
front end because that is basically driving everything what I want is uh to be able to all right trus take take care I
know it's getting late for yall uh what I want lobby so the test I can write is host a new game and then check the
repository because basically uh I mean I could do an output tracker on the game creator but it's going to have to talk
to the repository anyway so may as well just do that so the test then we want is that so so we're going to end up with a
game store uh eventually that's going to get handed in name uh Asser that the game views from that instead what we're
going to do is find all uh so for now I can just extract the name and then check that the name is there what does find
all return a list of game uh oh this is not game view it's game thanks yeah I was going to do the H size one first but
um why is it not why is it not finding game that was so weird it was like stuck in yeah the extracting should have
worked confused uh okay so this will fail anything um in fact we don't care about the model that uh actually since we
don't care about the mod we don't care about showing the model so that's all we need so we create the game store use it
we say host new game we expect that to store oh I already did that research you can I can tell you who it is I I have
the game in my have had the name in my notes um I mean I could probably use it on YouTube anyway I may or may not get a
copyright strike but I'd rather not risk it all right so this will fail because is uh so now um is anybody using this
yes okay yeah actually that's what I was going to do I was going to say hey do you mind if I use it on this on this
stream on YouTube if they uh want money for it then I'm not going to do it um but it's possible they might just give it
uh give the license to me because I know other people have done that uh so let's pass in the game store here uh let us
create that Constructor so who's calling this Constructor I think it's just this one so we'll basically say new game
store it so create knob by itself will create its own game store uh this one will take that uh this won't change
anything but it's should all still compile in the test will pa uh test will test will fail in the same way uh and now
instead of calling this these two if I delete that do other tests fail no okay squiggly oh because uh spring is not
happy we'll we'll fix spring later uh that's not what I yes I do not I have not because we were starting over so I don't
have the uh so we don't want that instead what we that and then it h my great type um all right so we' got crate all
which does the right thing we' got create with a game wrong all right that shouldn't have changed anything it should
still fail but it should be the only test failing because it doesn't have size of one has zero okay now I can call the
right thing which is from that okay so we know that game creator create new game does the right thing so therefore uh
host new game is now pass yeah it's like I'm fine with with with giving me suggestions that are compilable that would
not have been compile ability is overrated maybe your woods all right so now now we can host new game names they're stay
they they're stored um I don't I don't know that I want uh so what test is using this is this test um so now I think I'd
like views so here's a case where I don't I could create a game store store a game in it and then pass that to the crate
null or I could just do crate null of a that ah interesting so the Constructor takes either no I do not have a oh do I
have a crate factory I do have a crate yes thank you I forgot that I had Constructor I don't think should be
reconstitute uh so that's what I want yeah so what's interesting about nullies is nullies in the test in the CQR hex
architecture can not just can but really should only um and so what I'd like is uh the one view um that's interesting
that it thinks I want that one I don't want that do I not have a conversion method for game view I do one that's
fascinating where the heck did it get that from I mean I can guess where it so clearly Cody is scanning uh projects that
are open because I've got my Blackjack open and that's the only place in any of my shoe fascinating uh all right so what
what does game view take it takes the name so you got that wrong right away uh it's game not get name oh come on you
can't even do the right method this wrong uh so this is just game. count Z one no let's do zero because that's valid uh
and then let's oh should we the players. this uh this is the first time I'm oh did I just remove it thank you like as
soon as as soon as I hit the button I'm like that's not where I wanted to go game view that's still kind of cheating and
then I want to save the game and that that so I didn't want that there because I I want to stop storing these game
Constructor and we'll get rid of this in fine okay um this test should Now fail because it's we're not going to get this
game view in fact we're not going to get any right so let's um let's actually get game right yeah so let's inline the
field and remove fascinating store uh oh so now I do need something that is not the game store I guess I could use the
game store I don't have access to the game store I guess maybe I yeah I think I want a construct that takes a game store
where I don't need access to the game want uh I don't want this so let's inline I what I want is to pass in I want right
now I need Lobby to hold on to both even though the game store is not going to be held on to this for much longer um so
I need this create to pass in game store and that one uh this one has to create a game store and uh oh I didn't change
the Constructor that and I think we can make this final uh this is spring errors uh so create if we just get a game
store passes that along and wraps it with a game creator create null basically does both so we can actually uh replace
that with create store uh this one I need the game store so I can save it um but then I can call game store because I
don't right um XB ask how did I get the knowledge I have today uh yeah working on projects reading work working on
projects learning what I need that's why I always recommend the best way to learn is work on projects um starting with
simple ones and then starting to get more complex where you start needing databases and front ends and adding bases so
the purpose of create null is basically uh asking Lobby hey can you give me one where I'm not going to give you any of
the dependencies and you just own and yes always yeah always looking for ways to improve um which requires being aware
of wow this is awkward how can I make this better uh and for me a lot of that comes from um wow this is kind of hard to
test how can I make this easier to test all right so create null will create everything for us we'll create uh the game
store which then eventually creates the game creator um create now if we give it a game basically we're saying give me a
Lobby where there's already a game I don't know where it goes you figure it out so the idea is is uh whereas I used to
encapsulate some of this what I consider sort of test setup stuff in my test classes um James sh talks a lot about why
this is better to put this in your uh in your production code because then when you refactor um it basically does two
things it sort of shields you from having to them refactor a bunch of tests um but it also means that if you change oh I
don't use game store in this way um I store it in a different way uh the callers don't don't care about it do yes what's
not to like about it there's nothing not to like about it it is a a a well-used well-known uh pattern so there two
different things there null object pattern which we talked about before um with like the passport thing uh this is
nullies which is um perhaps not the best name and James sure admits this um but James TR talks about in his uh um
testing without mock uh stuff yeah and so n logic pattern really encourages you to think what does it mean to be null CU
just putting null what happens when it's null how do you treat it you probably have some if statements somewhere if it's
null you do something well make that part of the object itself instead of putting that everywhere so it's it's really
another form of of of encapsulation all right so now that I had the game store now I can ask game store it's a little
law Dem meter not quite a violation cuz I'm getting a a collection and so it's fine but this is a little awkward but
that's fine because this is going to go away um so now uh we should get the lobby know there was the lobby with games um
this will then fail because that's not what we have in our in our crate game so what we're doing here is we're we're
going from one red hopefully to a different red red so now we're getting basically uh views which of course makes sense
uh and that's not what I predicted because what I predicted was we're going to get a game view but it's going to have
these values uh sorry it's not going to have these values um now I'm expecting so my my prediction uh because I forgot
and did not notice uh this new array list I noticed it before and then I forgot about it and now uh now I need to do the
right thing so here what we want is um game store find all games um to certain extent there's no point in putting this
attribute in if the games so I'm going to turn this back into an if statement um and then move this up so now what I
don't I don't want all transformed into game to list and then this will extract back out so that now should I should
have one game view in there uh it'll be game name shiny Chrome 12 and since we didn't add players that should be zero I
guess I could change my test to say that so how we change the test to say that game name shiny Chrome 12 12 and this
should be zero example uh what is an empty Constructor to represent an an empty passport um I might I probably to make
it more clear I would have it perhaps a named Constructor um that creates uh you know how however you want to call and
refer to the the passport that's not filled in yet so maybe create password. create empty and then um it it would be
very optional like you could do that although i' probably more uh I'd be very careful with that because um I'd probably
if it only has two states that it's basically empty or not empty like you're not doing anything el else with it then I
might be okay with with a Boolean for saying is empty um in my experience it booleans often turn into three or more
States and then you'll want an enum so I honestly would not leave as a Boolean I would just go directly to have an enum
with two states uh empty and not empty or filled in or valid because what that makes easier is um at some point you're
going to make likely be making a decision based on uh based on on that and it's then you can use Java's switch
expressions and closed switch and stuff like that that makes it really nice all right so let's commit now yeah and then
and partition you don't want to part ition into a map that's Boolean that's just terrible because event because what's
nice is if you do the if you do things like partition you have two states now when you have three you're not going to CH
to change very very much code I mean I really I I've gotten to the point where suspicious that having very clear enums
representing what really is because almost always booleans are are state in the sense of a state machine and you may as
well that make make that yeah make that clear upfront two you can always write you know query methods that make that
simple to to to have is this and is that uh but so frequently it turns out um either you're going to want to add another
state or it's not clear sort of it's it's related to a missing yeah maybe maybe it's missing missing abstraction that
Boolean you know you may you're you're you're relying on the name of the variable and the name of any methods that
return that Boolean um to sort of hold and support that abstraction uh pulling it out into an enum that makes it really
clear that's so I don't know that I want to do any refactoring I think what I would like to do is move this from that
games and then I can inline this that's better yeah absolutely then you then you if you if you saying you know this
thing is called empty and this thing is called valid there's confused and it's really kind of amazing when you start
really looking at booleans in that way how very few are actually like is this a true or false um that false doesn't mean
this this thing is not true it usually means just this other standpoint all right so what next uh or did we actually we
handle um yeah we don't we didn't actually test that yet uh do we need to test that from here actually no this is good
enough we could convert this into Alpa tracker but again it's like I don't know that that feels like overhead I don't
need um so I don't think I need to test this um let's really test to make sure that to make sure test to make sure host
new because the fact that that the handle is level now show Lobby um well it certainly provides the game views that has
that information does it it should uh I think we now have to fix the fact that right so uh oh I don't need that yeah I
think I have to do that as a uh attribute because you click on the on the C you click on the host game information
unless it's HTM X but we're here let's see so type in the name I click a button what do I want to see um I mean I could
just for now it'll just display here and enough if somehow there are a lot of games and I might be confused about the
game I just hosted then I might redirect to a separate page uh but I think this uh yeah I mean I could do a redirect
night so we are showing handles because that's what we're showing uh so let's let's go and change our unlike what I've
done in the past I'm going to basically config for now and uh this a actually I don't calling uh oh no that's fine all
right so we'll Nifty uh it created exactly the beans I way uh right I don't my game simple yeah that that was that was
nice okay so now I should be able to run all the tests and assuming I did the configuration right everything should run
not um right because I need a test this uh I think that's fine I think we um why did I make this a component
configuration uh thinking so that still fail because uh because this is in a separate class it won't automatically get
loaded uh unlike if I put it in the spring boot application startup uh so that's fine um what we can uh not test
configuration we want like import uh and then it's uh CD Game right yeah and then if we ever want to override it then we
can create our own these I'm going to just say suppress for is it a cookie it is a cookie so I've got a session I forgot
that that's something I going doesn't think I'm log why does it why does it think I'm logged in is really issue okay oh
I know why uh there's something about uh clearing session IDs or something like that that I'll have to look into all uh
it's interesting that we got zero here uh so old Fox Zero tricky bird 94 both have zero great all right um so that works
so what's next uh that's done um so now now we're up to join game so once we finish uh join game from the UI which is
our inbound HTTP adapter um then we'll have sort of caught up with our what we did inside the domain uh and then we'll
uh do this although we probably won't get to this done so we need um we need a text box that's going to say which uh
which game would you like to join um I'm going to take a break and then when we come back we'll we'll do all right so
the next step is um I'd like this to be displayed a little nicer uh even though it doesn't really matter um mainly
because uh was a little hard to read um I'm curious if I can get Cody this so let's see whoa what's up with the coloring
I think that's that's a still an intelligy bug code all right that was a that was a good start I wish I be replace it
cursor that I don't think I want these as line do I items that's okay for now uh because what I want is uh and this to
style uh font it all right and so what I want is join uh I think this is just join because this will be as the result of
an in invite so I will send that send somebody an invite link uh and they'll just enter that or uh well the link will be
a get request redirect to something else else uh we'll just start here so what I want with join um is we want and set it
they'll already be logged in so we'll know who they I think that's what we want yeah so let's preview that that looks so
that's host new game um that will do a post to that endpoint uh controller well it's still part of the lobby um but it's
a certainly a new endpoint y uh so X proof asks is the definition of domain and domain driven design the subject just a
subject area the problem you're trying to solve yes note that it's the problem area not the solution area so what is the
problem or so problem sometimes causes confusion so I I usually call it either what's the problem or the need that you
fill all right so let's go commit and let's go and create another Lobby MBC test join uh X proof uh does it does
everything have a domain yes otherwise what are you just I don't know what you'd be doing if you're writing code that
doesn't solve a problem it may not be a complex domain um not all domains are complex but you're writing code for some
purpose so what is that purpose right even a game has has a domain has a purpose I mean what could say you know if
you're doing like lead code and you're solving individual little problems then that's the that's your domain but there's
not much of a domain there but there is like like you know I mean those are those are too small to to be considered sort
of a a full-on domain in domain driven design Bor yes uh code can create problems so you might write might but creation
uh so let's see is this what we want so Lobby join game not quite Lobby I don't think but it will be the um we don't
know where it's going to redirect here at this point so we don't care Cody no don't you remember I had join over there
how quickly they forget uh yes we will join game with the principal and uh we will have a request PRM that is game
handle uh correct uh we'll just redirect here I don't know whereare what the URL is going to be of the game just yet
yeah bdsl I have no idea where why it thought that um I was expecting it to to to have a little bit of context of like I
just wrote a test that does a and then it forgot what the the URL was and just hallucinated again what it thought it
should be um but the rest was was pass and it does so I'll go ahead and do oh before I I don't know I don't yeah I don't
know I'll to do this offline I was hoping was a simple thing yeah I don't know why it's not logging test uh this one is
is um that's interesting that's way too much but some of that's useful uh I don't need that I don't need that I don't
know where I got some of those words it's so funny like code I can figure figure out where it get that from but like
some of those some of the text it's just interesting all right so we got a Lobby uh with a game already created now we
want to join so we want to say Lobby uh in this case we don't want dummy principal we actually want um some now uh we oh
pretty soon we're going to want to create a person repository but right now will throw in temporary person fun the
question is where did where do we redirect to that's going to be the trick uh but that's a separate a separate question
um so we've joined the game and so now to uh principle the interface doesn't have a lot in it in terms of things that
you have to implement um so yeah so the basic principle from and this is Java security not even there's more
sophisticated method uh interfaces authenticated principle um that has a lot more information and we'll eventually
switch to that but for now this is this is all we want really what I should be doing is not using principle um but
eventually what I'll use is person the actual object I want uh and then provide a method a lookup method that spring
will use to convert whatever comes in into that thing uh and so this will likely that um I mean I guess it's serves uh a
marker but um it really is the base class or base interface for for a whole bunch of things in the principal area as you
can see all the stuff it's like authentication is um really the token that we want to work with I've just been using
whatever the is so this work because it's it's uh what we call a Sam uh single abstract method so the interface has a
method uh that method is get name um and that's the only method that's undefined right the only method that's abstract
and so therefore the Lambda mean this is what it looks like as the so because this is the only method that's abstract
then the Lambda does does that so sort of the magic of what underneath um so in a sense this is the implementation or
not in a sense literally this is the implementation of uh of get name yeah I don't think they call them Sam anymore I
think they call them functional interfaces but really principle is not is it technically a functional interface no
because it's not marked as a functional interface it just happens to be one um but there are specific interfaces that
are more meant for for functional stuff right so it's basically like whatever method you're implementing here I'm going
to return whatever value you give it uh and I could write more complex code like I could say return blue and that's
that's valid um but then there's short hands which is like well we don't need return because we know whatever thing you
give it here is a return so we that yeah as an old school Java developer for for quite a while I had to do this to see
what is it doing cuz I'm used to Anonymous inter classes this is an basically an anonymous anonymous inter class um I
just have looked at like what is it doing it yeah it's kind of a weird side effect if your interface happens to have one
method um it means that it's easy to Lambda Lambda IFI so what we expect is if if we join a game uh we probably want to
pull this it uh we expect that players um let's just say hot size of one in which case we may not even need this this
principle but we could start with that and then we can say uh extracting players uh that that uh this that's returning a
list why is it extractor something's not quite right here I am confused players and then I can say contains one yeah
that wasn't working either it's oh because I'm already got players uh duh I'm extracting on players that's that's the
problem when I want to extract is that's why it wasn't working cuz it's it's game it's not game. player name it's player
name I don't know why I think players uh player does not have the name so I have no idea what this is going to to be ah
crud uh I guess I can get the ID and I can say the ID I don't know what the ID be zero so it was it was correct in uh I
guess I yeah because I was calling game players I and I forgot that I was doing that all right uh bdsl uh building is
wrong in that regard um there's an at functional I mean the way I'd have to go look at the Java language spec but I
believe the spec is saying there are specific interfaces that are are functional um they're sort of implied functional
and then there's marked as functional differently all right so this is well this will certainly fail because we're uh
I'm just going to say 9 99 here uh so what I wanted to say also was has size of one is is actually all I initially care
size intellig can't figure out what it is what the return value of that is that's now we need the other thing because
what we want is we want player joins player uh Joins and on that we want to say ID do I want it to also support taking a
game handle that would be that yeah me the chains like help me out uh yes if you have an interface that had one abstract
method and people were using lambdas to implement it you had a second abstract method you can no longer use Lambda yep
you would break any code that did that and I that's why uh why you want to Mark things as atun functional um because
basically it forces is you and you will break your code if you add a method that uh breaks interface so just because you
happen to have one method yes you can use it as a functional interface um but that class is basically saying it it makes
no guarantees that it uh so we can look at the Java language spec 9649 yes I like to read language specs 9 6 4 9 so
there you go so it facilitates early detection of declarations and so therefore it's compile time error if you mark it
with functional interface but it turns out that it's actually not so if you really mean it to be a functional interface
annotate it uh to protect yourself changes if you want it to be always functional uh then yes absolutely annotate um
well if you try to add a a second abstract method uh onto one that had a single one you will get if you and you annotate
it with ad functional interface it will immediately compile if you did not mark it as at functional interface um then
any code that tries to implement it with a Lambda will fail to compile if you're a library and you add a method like if
somebody went into principal and added another one it might break a whole bunch of code uh but to a certain extent that'
s on you for using it and assuming it was interface yep yep absolutely you could change it not realizing people are
using it uh as such um and we know whose at fault is it's space for heers um so I want a game find uh I think I'm going
to have to put put I'm gonna have to disable this test because I can't implement this in one step I mean I could I could
basically find all and do that but that doesn't really prove anything so uh and we'll method that does um push and
That's all folks uh so next time um which will likely be Friday uh we'll pick it up from here as always you can join the
Discord to discuss this or anything related to the stuff we do here on stream um we are starting the conversation or uh
continuing the conversation for selecting the next book for our book club um so don't forget to ask about that if you're
not already uh a member and what else uh I think that's it so thanks for hanging out appreciate it um always appreciate
recommendations for folks to to come on and stop by and uh have a great rest of whatever day is left for you and I will
see you see you
