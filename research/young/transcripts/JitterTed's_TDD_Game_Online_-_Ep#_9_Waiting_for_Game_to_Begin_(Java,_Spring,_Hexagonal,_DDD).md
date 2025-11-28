# JitterTed's TDD Game： Online - Ep# 9： ＂Waiting for Game to Begin＂ (Java, Spring, Hexagonal, DDD)

**Video URL:** https://www.youtube.com/watch?v=fNohT8Z5KcU

---

## Transcript

yes that works so that's the physical game right this is what we're bringing online this is the purpose of these series
of episodes is take this game uh and put it online so we can play it remotely and so again on that note or trying to
keep in mind my my overarching goal uh what we call the you know you might call it an MVP or um minimal lovable product
what whatever you want to call it it's what is the minimum that I need in order for multiple people to be able to play
remotely assuming that they're already connected using something like a zoom or a Google meet or God forbid Microsoft
teams um so I don't need to handle things like whose turn is it uh so I very much want the physical experience because
it's much more flexible uh and it's also less code so I'm not implementing um any enforcement of turn taking uh I might
want to do things like count how many cards you've played or discarded because one of the things that happens when
playing the actual game is sometimes you lose track of did I play or discard three cards cards cuz that's my turn I
don't remember uh so that's something I might want to put in but again even that is is nice to have uh hey no raccoon
long time no yeah yuck teams um I always think of the situation where uh someone at Microsoft wanted me to give a talk
and because it was Microsoft they required me to use Microsoft teams and I simply could not get it to work just would
not work yeah so I don't know of anybody who who actively likes it that doesn't mean they're not out there I just don't
know them okay um so let's take a look at where we left off yesterday so where we were uh working on is the join game
screen so uh let's bring up our good old mockup no it's not that um I feel kind of silly okay so this is not not uh not
the game um but I thought i' I'd bring this up because I'm like there is a few things that I do um not a lot uh when I
start streaming one of them is start OBS uh the other one want to start pretzel that's the background music um and turn
my focus to streaming and I realized okay it's not hard for me to do those things it's literally uh a few clicks but oh
yeah Mac OS has this thing called shortcuts so I created a shortcut to do this and I'm I'm inordinately proud of myself
for finally finally doing that because it's like and now I'm going to attach that to a button on my stream press all
right nauy re go go write some code thanks for stopping by hey Jonas all right so um let's go look at the mockup that's
why I was taking us and I got distracted I'm likely to be very distracted today uh so what we're trying to do is
recreate this although much will actually look like not that uh let's switch to the right window which is this go why
did you come out over there it's so weird uh so this is what we're we're working on um the idea is it's a we're waiting
for everybody to get ready uh uh sort of going into the game room as it were um and uh we're going to show who's joined
we're going to show notifications we're going to show a little bit of status around people who who have joined the game
but have not connected although usually as we saw the time between those two should be tiny um but it could be you know
their websocket doesn't work for some reason uh so there is joining the game which is a domain issue uh and there's
connecting to the server which is a technical uh concern um so in order to do this we need websocket support so that
when this page loads uh one one of the things we wanted to do was have it connect to the websocket on the server and
then send a message saying hey I've connected to yeah slow internet connection could be yeah um so after dealing with
two two two issues making it hard to figure out which was at fault um and it's basically everybody's fault um uh we
finally got something to work by writing uh a little bit of JavaScript um I did do a little bit of looking I actually
looked at the source code for the HTM X websocket extension and uh it appears to prevent default which means that the Ws
send if it's working properly should not actually do an actual post if it works properly um what we I couldn't figure
out why it's doing that um there's uh but whatever um so for now I'm basically not g to uh worry about it I am going to
leave this this in here um but I don't I don't know we'll we'll see maybe maybe at some point later we'll we'll go back
to the form once once I figure it out once I have a smaller example uh so one of the things I'll probably do is uh
another stream on just the websocket HTM X stuff using my smaller project that will make it easier to to out yeah ew
JavaScript but hey it's literally like what I mean depending on how you count this you know one of those is a console
log do we count that that's not really code um one of those is a variable that's injected by time Leaf so okay fine
that's one line of code then the ad event listener is two line of code and then the uh send is three lines of code so
it's three three or four or five lines of JavaScript I think that's okay um if we can figure out uh and I did look at
the issue that we saw yesterday uh on the HDMX websocket extension um and I basically commented on it the one that was
open since December it looks like there are a couple of others that are related to it when there's going to be progress
made on those there was sort of no acknowledgement um of the problem the issues were filed but nobody said yes this is a
problem uh so yeah so I don't know there there's some kind of timing issue um order timing ordering issue that that we
basically worked around by manually adding the the event listener here instead of using the one that was uh down here
over here so can we do that no I don't think we can um I'm going to put that above here so there's some more playing
around I need to do here uh to see if I can come up with a little bit of more of a cre create reproducible issue all
right you'll have one line of a JavaScript okay good because if I have if this works um then we could go to just calling
a function which is then just this and if we could get the W send to work then we actually get down to no it is
certainly not worth wa wasting any more time on it okay so uh so what we want is now that we've got a connection right
and we saw this do I still have it again oh 330 is that I meant to update to 330 uh I'll probably I'll see if I do that
at some point if not it's a trivial update I had already tested out the Milestone release milestones and release
candidates so we're all good uh let's all go to the lobby uh but first we'll have to log in and I was finally able to
figure out how to disable one password from trying to autofill that because that was very annoying uh we host the game
our good old soft Impala join the game uh so we are connected um this is real data uh this is the fake data this is fake
data um so that's all working and what we see here is our payLo details um this is the message that we received uh with
the connect saying which game they've connected to we already know who they are in the sense of their IP address because
we got that as part of the act of the um connection established so we can tile that together now we know uh their their
session ID uh and we know which game they're trying to connect to um as I'm saying that out loud I'm realizing it's
probably easiest going forward when we finally when we get to actual game play to just send the game handle every single
time um that will make routing easier rather than having to look up in the map which session are you talking about
because there might be some websocket reusage that I don't want to I don't with uh Jonas also had issues with HDMX and M
sockets earlier uh so you stopped trying yeah I don't I didn't have the choice of well I guess I did have the stubborn
um I have to admit though it's it's a lot it is easier for me to be a bit more stubborn uh doing this as a stream
because I feel like I'm not alone as opposed to doing it alone and saying I give up uh okay so we've got our payload
here it's uh it's what we want um so now what we can do is we're basic right when one of the things that can can be hard
to learn when you're doing development in general and specifically test driven development is uh outside in so this is
outside in we're basically saying what what's convenient for the front end in this case using HTM X to send to the back
end I can send anything but I'll send connect a colon and uh the the game handle um once I have that now I can write
tests against the thing that's going to receive that um and basically figure out what to what to do with it which will
be um pass along the uh the principal and um and the the the game handle that will parse from this um so I could from
the front end I could send the the username because I do have that uh but the back end already has the principal so
there's no point in re in not using that especially since the principal is going to be much more secure than whatever
random websocket message I get all right so we've got and I've got some cleanup that I need to do on the back end uh
because I basically copied code from ensembl the ensembl timer um and so up uh but we'll go ahead and commit we can
close this uh I could probably style that and make like I know I'm getting I'm worrying about things that really don't
matter uh let's do this as item and this would be an unordered like um so we want to get rid of that and that and let
the list item provide that uh so what class do we want CSS as I said yesterday I'm not sure if I'm going to use uh I
probably will not use Tailwind in the final product but certainly while I'm still doing design work uh it's the easiest
thing to sort of play around with um this is the CLI what if I don't want to use a CLI what if I just want to use this
uh why not what why not use Tailwind in the final product is that what you're asking uh that mainly because uh if that's
the question which I think it is uh it's very verbose which by itself is not a problem I don't have a problem with that
um it's the duplication that's the problem so really Tailwind is very awkward when you've got the same things like I've
got a button I want to make sure it's looks the same everywhere it's you're really not supposed to use and copy and
paste the classes from button to button to button because if you do that well you change one it doesn't change all the
others when you probably want that to change all the others uh so unless you're using some kind of component mechanism
uh you want to get them out of the HTML uh if you have some mechanism that generates that like if you're using a a a
react or view or something like that then you're only going to Define it once and then every time a button comes up it's
going to get those so I don't mind if the classes are there for each thing in the HTML I just don't want to be writing
it multiply both times in that in that way since I'm not using uh a react view or angular um then I either need to put
it in CSS or I need to find another way to to to generate it yeah so if if I if I go down to the level of fragments and
treat those as there they're not really amenable to that but if I were to do that um you could do that right you could
use the that um it's what I will likely do uh because I've been reading up on on web components and they're not hard to
write um I might write some some web components uh the other thing is is like have yeah anyway so uh and I think that's
that's that's all yeah yeah and and so Tailwind you you C you you don't have to copy these like right here it's
basically because I pretty much copied and pasted it from the playground um but once you have these set up you can take
these same classes and just put them into a CSS file using an apply and it's the same thing uh and and that's and so in
a sense you're using the Tailwind classes to shortcut um and to sort of make sure that that you've done it correctly in
your CSS file uh and I used to use bootstrap um but I I want uh especially for something like this this is not at all a
standard UI right it's it's this uh where there's almost nothing here that's that's standard except for maybe the start
game button so um right so I was going to add where is think there we go um so now I don't need need my I'll leave my
static CSS file hanging around but for now I'll use Tailwind because it has all of the things uh and so now I got my
list dis uh except I would like do ah list inside does the appropriate indents okay that's actually what I want there we
go actually that doesn't quite look right what does list inside do it's interesting that that this is where like I get a
little OCD um you may not be able to see it there's more space with with the N here than with this than with the the
dots uh list I might have to I'll leave it as this uh but I'm not going to use list inside because I don't think that's
enough we'll use a margin left four there we go whatever the browser is setting it's like it it's like a pixel or two
off and it just bugs me okay uh so we got our notifications orange okay 8131 I used to be able to read SVG paths um but
it's been a while so I've forgotten some of these uh Flex none Phil Red Stroke two okay good uh because this really
shouldn't be mark but I will um but just not to confuse me in the real app I just want to make sure that hardcoded there
we go uh okay um what else uh all right so that's that uh okay so now we can go back to our our uh sequence diagram like
thing so we post to the Joint endpoint let's endpoint that's the join end point uh so we find out who they are uh
they've joined the game we provide their nickname um then we redirect that's when we get the want is this really not
used let's get uh so player joined we did that part uh we redirect to the game with the game handle we've done that uh
we've done the connect um and what we want to do is the connect we want to broadcast right so that's now the next step
we want to broadcast when we get a connect we want it want to broadcast everyone that they've connected all right CU we'
re working on um I think I want to do that in the other order so um so we're going to do the notifications first so
first we're going to have in this notifications component which I just closed but basically the the list items those are
going to be uh what we're going to work on now okay now we um so uh the adapter that's going to receive that is our
websocket Handler um which we now need to clean up a bit so let's clean this up uh we will still likely need a session
map um we don't need this uh we don't need is just logging so we'll we'll keep that around um okay so uh let's move this
to the correct place um this looks like an inout adapter and so this is where it can get be a bit confusing with uh the
hexagonal like architecture um let's focus on first so we're not actually going to send in here uh this is totally about
inbound so let's move this to the right package because we basically just copy pasted this so let's move this to the
right package so this is adapter it's an inbound adapter um but this is the web socket oh let's spill out web socket uh
that all looks right we Factor uh yes we create it um uh this let's rename it because it's it's inbound Handler I'm open
to better ideas for names but with uh the session map is currently useless um it's going to need some dependency on is
pretty much handle message uh what is on I just want I actually want to delete them there we diagram so this is our uh
web UI adapter um this and end says my bit rate is good so unfortunately I think it's your end luckily that means uh
you'll be able to watch the recording so the use case player connected uh but is that a use case uh it does need to
change the state in the do the uh so this is an inbound adapter this is the uh web socket room that's what we're going
to call it connect um I I it's starting to feel like I do need a representation of the waiting room uh inside of my
application I'm going to call it waiting room service just for now um so the idea is that uh someone connects they get
to the page it does a websocket connect shared so this thing is so there's basically some kind of shared thing um yes if
if I were working on an Enterprise team I would not it's even in a diagram it's not even in the code yet so we'll leave
it at that um so there is a a shared websocket session so uh so you connect here we sa save that here um because then at
some point what we do is we so we've got our websocket broadcaster uh which also shares this um let's move this has a
reference there as well as this well so sort of the flow is going to go you map why do we save you in the map because uh
when we Bas when we tell the use case hey this person has then let's put this in what color this will be solid make this
yellow so we save it off here because then what happens is uh we connect to the use case we say hey this person is now
connected um that tells the websocket broadcaster we'd like to tell everybody that this person just connected which then
basically says Hey broadcaster message and then it basically then sends it out so unlike a typical request response
where you might send something and then it return turns with information in this case it's sort of going this roundabout
route through uh because we want to broadcast everybody not just the one who sent it in uh and works uh I like you uh
I'm not quite sure what you're saying I think so um because we have with each incoming uh message we get actually we get
the whole session information so that has the principle inside of it um but we also get that and that's what we'll store
in the map when when they connect uh when we broadcast we will basically broadcast to all these websocket sessions
except when we have multiple games and we want to refine these is going to be uh in a sense oh there's going to be some
interesting refactorings here because as handlers uh there there's going to be not there's going to be one websocket
inbound Handler but inside of it there's going to be multiple things that represent game sessions so likely out of this
is going to come a game I'm not sure do I do I have the websocket Handler deal with that or do I just use the fact that
I know who's joined in the game and ask the websocket people uh yes that's correct yeah so there is a a websocket
session but I'm I'm holding on to it in the adapter not that's all right um okay so this is the adapter it's also going
to eventually Implement uh an interface which is going to be the websocket broadcaster which is a bit of name um because
it is it is identifying a technical implementation by saying websocket uh so really this should not be called that um
and so then there is a concrete oh lines don't move oh that's a bummer go so really the shared websocket session is kind
of inside uh it's kind of inside the um the websocket broadcaster because it's the know who to broadcast to and that's
pretty much how I had it set up in the in the Ensemble timer so timer um and we look at the websocket broadcaster um
it's almost exactly the same the same pattern it it implements broadcaster uh and what broadcaster has is basically um
these send methods uh and that that's what uses so the only uses sort of the only references to this map um is basically
for sending the oops so this is for sending uh this is for putting after connection established and then if they con if
they disconnect we remove them uh and for all those we want to broadcast notification events uh which right now is
basically two so that's that's what we're going to so what we want is we're going to uh tell well yes yes Cody tell all
clients that new players join I do want to do that but I'd like to be more specific room I guess we just call it waiting
this handle message is going to be different sorry I'm I'm just like thinking do I have a different Handler for the
waiting room versus the game and actually no that's not true um so if this is not waiting room service uh I I think I'm
overthinking this because I'm not I'm not writing code anymore but um even though connection is a technical concern the
idea of connection is still something that the application needs to be aware of uh so mainly what I'm trying to figure
out is um if you connect and the game is going uh we're not going to tell the waiting game and if it's in waiting room
mode that's to I I know I'm going to need multiple games and so am I confident that I'll be add able to add support for
that or do I have to think about that now um I think I might need a map of session of sort of the reverse of this which
is to which game because if they disconnect it's not like they're going to broadcast hey I'm disconnecting from this
game um although they might but that's a different kind of Disconnect then oops I so this is the question how do I know
which game they were connected to when they disconnect um I think when uh when they connect I add them to this map when
we get a connection handled message that's when I map the the the the game to the the session the session hey swegi so I
think that's that answers that question uh when we get a connect and if they connect multiple times with the same game
that's fine uh if they connect multiple times but with different games then I've ma them to different games um and if
they disconnect then I will disconnect all of games and this is just a sketch so it's going to be a map handles uh I'll
probably use real multi map for multimap I could use the Google common one uh obviously I have to use an multimap I don'
t have a I think I have a uh I certainly don't have a direct dependency on this so I'd probably have to pull this in and
so I have to decide do I want to depend on Google common collect guava uh what jar is this coming from lip client uh I
don't know which which where that's coming from um I might use the eclipse collections I'd have to see how big it is um
I'm always hesitant to pull in I think I have my own implementation because like I just need the multi map uh what's the
multivalue map it's thing um this one uh which must be there's an that lots of implementations of that because it's just
an interface so probably the linked one is one it's not thread safe I I wouldn't I I might I might write M I feel like
I've written one before have I written not no I haven't I think I have a right one cuz I know anyway I'm not going to
worry about multi um I'll have to see how how big that is in okay let's go back to our diagram not this uh we update our
our shared we talk to the use uh this person's connected so what did I want to call the service because it's yeah game
connector sounds more like something that connects games to something here what am I connecting I am connecting so yeah
player connector I like that thank you uh so we tell our player connector that a player's connected um I got to stick
manager in there somewhere uh uh player connector tells the broadcaster right so we connect um updates this shared
session we tell the player connector the players is connected how do we know who they are we look them up in the service
um in the uh uh player repository uh we broadcast the player is connected there's nothing actually in the domain that
changes so this is this is always this interesting case and I did the same thing with the ensembl timer where the timer
itself is transient um and here sort of by definition because these are web soet connections they're by definition
transient if the machine crashes and restarts those connections are meaningless uh so it's interesting that that this is
a p a recurring pattern of application state really app System State oh no cluster job schit do yeah don't commit those
no yeah should have been called like feel like I want another shape what feels backwards let's try that there we go let'
s also paint that yellow uh and so this is sort of our uh connection our application so there is this this thing that's
part of the application layer so this player connector is is intermediating between uh some stuff I don't know if this
application connection state will actually be represented as a class but there's this idea of connection state that the
application needs to know about um it doesn't have websocket connections but it is the sort of um so that's that's
that's kind of something that's interesting because there is no domain effect here uh so then we broadcast the players
connected that sends this out and so that um that's going to be put that a solid line purple so from a test point of
view here so player connector uh will need and and How Will I Know It broadcasts um do I do an output tracker
broadcaster uh I have not I I have not published the output tracker Library yet so I can't reuse it which is something I
got to work on um so James shw and I uh wrote an output tracker with the output listener and tests for it uh and I've
extracted it to a library but I've not published it so I can't reference it here oh generating security uh I may ask for
for a review of it um but it's more I just I just have to uh set up the keys and whatever in the maven Global repository
so I can actually push it and publish it as a public artifact that's uh and I want to set up J releaser to do that and
I've never done so um so player connector uh I don't think I want to do an appat tracker just because I don't want to
copy and paste that stuff um so I'm going to do I'll write a mock so what we want is given player connector connects so
that means from need connector um so let's really tell player connector that new player is connect Ed handing it uh game
sloth uh yes I don't actually have um uh specifics on my site uh because everybody wants something different um but uh
shoot shoot me an email um uh or you can uh if you're on my Discord you can hit me up and we can get contact there but
that so best if you don't have my email I whispered it to you but um it's basically my first name at my website that'll
get to me hey there x shadowfire uh what's the principle that's the security principle so inside of uh the websocket
session one of the things we get from it is principle so one of the nice things about websocket support in in general
but specifically with with spring uh security is I don't have to deal with that like because you've already logged in so
your principal's already there so you logged in through the typical HTTP scheme um the websocket is just an upgrade from
that same connection so it has all the information in terms of security that it had before and so now we get that every
time which makes life really easy uh because we can then say I know who you are who sent this message uh so here if we
get a connect message uh we do that um technically so which one of these counts as an actual connection it can't be this
one game cuz all we get here is just your website ET connection I have no idea which game this is um maybe there's going
to be some Global thing that tells me who's connected but I don't I I don't know that and that's if uh okay so if we get
a so one of the things that that and I mentioned this before uh the handle message here is going to need to delegate to
to all sorts of routing um because this is like the the bottleneck point for all incoming messages over the websockets
and pretty much everything is going to websocket yeah so one of the things Spring Security decided is they were going to
uh a minimum every authenticated uh thing will have PR principle in it um most uh one of the nice things that spring MVC
can do for you is you don't have to um do the lookups of the principal username and find out other user details uh it
can do that for you uh so one of the downsides of websockets is like all of that support that the MBC sort of code does
for you the serlet MBC code does for you you you get none of that with the websockets so um I will probably be
extracting uh stuff into some some libraries that that will help um because it's a it's too bad is there there's not a
good way to reuse that mechanism maybe there anyway so we get for so the handle message we get a connect message um
because the connect message gives us a game handle um we add uh to our websocket to to game is it to game or the game
handle I uh the main thing is is that we tell the player connector that a new player has actually connected this is the
player um basically their principal username uh game yes I can I can create a nullable uh so bdsl I mean that's totally
up to you a principle is simply you have been authenticated what you represent that's you and indeed that can be
problematic uh if you're not prepared for that but because that's pure authentication it has nothing to do with
authorization and so usually that stuff is handled at the at the authorization exception all right so what we get um and
the reason why I did this so I've I've made the slight mistake before of not pushing enough on what does the adapter
have and what does it send in right basically what is this call um and not looking in enough detail to figure it out
because then when I write this test I'm basically writing the test for what I believe the adapter is going to use
because I'm not going to test through the adapter um uh but I want to make sure that that interface is right so now we
can finally start a test so let's go um where do we want to start will create our play your connector normally I create
test first but I find it easier these days to create the class an empty class and then create the test from that because
then it creates it using my test template all right finally get to write a test an hour and 20 minutes into the stream
um so we're gonna basically um what's our output our output is sure uh no there's not a missing feature to create a
class from a test it does that um the problem is if I create the test class first uh then I don't get my uh assert J
manually because the go navigate to test symmetrical um or I just reference a class and and let intell create it that's
usually what I do all right so we want to assert that the broadcaster sends a a green connected which means we want uh
player with username okay so uh so let's create so at this level stuff is is sort of all strings right so that's um
there's not a or maybe value objects there's not not a lot of uh I don't do I have a value object for username no it's
just a username so by the way if you've got a subscription to S to O'Reilly learning what they used to call Safari um
you have access to all the Manning books and the second edition of the Spring Security and action book uh is pretty good
um and it might have need cuz it was just released not that long ago uh okay okay so um let's go ahead we'll say string
uh player user name is green thank you for reading my comments Cody uh and a game handle is that thank you Cody I guess
it I guess so this is some I mean I haven't used Cody a lot um but it certainly seems handy if you write your comments
it can it can write um yeah you're not going to find agreement on what some of these terms even the fundamental ones
like principle mean uh everybody does it different uh and it ALS so often depends on where is that information stored is
it in ldap is it in Windows author uh Windows Manager is it in uh okta is it in you know other tools you're you're you'
re not if you're looking for the one true answer you're so given that user uh when they connect and so we're going to
have a player connector and this will be our mock um is that the method we want do I want so need so we'll need our
right so do I write yeah so I decided I was going to write the mock broadcaster I may refactor this to use uh so uh and
I guess I want to make this a true mock a self-verifying mock um we'll create the interface uh this is a directory and
we will create an implementation here and and um we can now create our Constructor and then we can create that method
and so our mock broadcaster uh right now uh I want to verify that the connect was whatever because the broadcaster is a
higher level thing so it's not player username it's actually actually going to be a player broadcasting well I'm not
sure what I'm broadcasting but I am broadcasting the player can't wrong although I might just be able to push that into
all right let's do one thing at a all right so this required me to think a little bit about what is the interface of
broadcaster so the interface of broadcaster uh is going to be um basically player connected so it's very it's good sort
of very event event like um and later it might be actual events but for now I think it's just that uh broadcaster oh
thank you for the hydrate Jonas yes broadcaster it won't be broadcaster connect it'll be broadcaster I don't have
anything left it'll be broadcaster uh something like player connected because there'll be messages of uh player joined
player disconnected uh and then there'll be a bunch of stuff around players uh game state um which I'm not sure is going
to be a probably yeah yeah yeah that's why I was like I have to I was requiring me to think a little bit about I had to
sort of think a little bit up front because I had to figure out how I want the the mock broadcaster to verify and we're
just going to now what's the difference I always forget what's the difference between fail so uh I seem to have lost my
uh assertions import because it keeps optimizing and so there we go okay um all right so can take out those so this will
certainly fail on the on the verify yep and uh great so now um let's go here uh let's go ahead and Constructor and we
basically want to say broadcaster guitar um do I cheat and just create the game that matches and the player that matches
uh I think I'm going to do that and then we better uh so what do we say that yes except uh uh there are there might be
confusion about Connections that are not game uh and there's that too that I want uh I think it was more the ladder of
like this is I am connecting to a game not just some random connected kind connection method um what happened to player
username that's not used that's fine uh except I would like I would like some please thank you so that's really handy I
I don't write soft assertions often and so I often forget the syntax and so having Cody uh write that for me uh was nice
nice uh So Soft asserts means that it won't fail immediately uh sort of collect it and then them uh and yes I do want to
assert here fast um and let's try we'll do that to force it to fail um and then um and here I am violating one of my
bullion static all right so our expect is uh I think this code is right but we forced it to to fail in this way so
happens yep so we get because we did the soft is we see both failures so we see the failure here about the game not
being equal uh and then we see the failure here about the player not being equal um let's fix that because that's
actually let's make it correct and now it should pass all right MP exception right uh so what we've now figured out is
we've figured out um how player connector talks to broadcaster so that's this thing and how it talks to broadcaster uh
we figured out how to talk to player connector which is uh connect um now we need to generalize it a bit so that we can
look these things up uh so we've store uh and lookup to do this um do I want to create a member finder because I'm not
thrilled with accessing directly yeah I think I want a member finder so let's let's extract let's see what that feels
like uh so we'll extract this to find um do I want to pass the principal security but that's annoying so no uh so by
username we'll make this public we'll make it static um we'll leave principal and then we'll extract it so we'll
refactor this uh let's pull this out as our parameter finder there is no player finder there is hey game give me the
member for this player that might turn out to be awkward um yeah so here's the member ID uh oh that's not right uh
because I didn't do the last step of the member store uh so member finder store can I turn this into a field no I and
going back here well this is okay yeah uh player is just an entity not an aggregate root correct they are an entity
reason um actually yes reason so uh because this returns optional right now the member finder uh wraps that and throws
an there I'm not sure what I want to do in terms of handling uh that kind of thing but that's not a responsibility of
the memb store to throw an exception if and we want this and let's see what's going on here uh oh we got a member for
that so ID so the player connector has a reference to the finder so it can translate username to member ID uh we don't
need that this player uh and then we don't want uh see higher order nulles everywhere um curious what what what which
ones you have in mind and if they match mine I honestly have probably been doing less NBL than you so I'm curious what
you interface well it's going to be a new class um actually we have this somewhere I should have refactored to it but
we'll this so this ends up being uh game finder oops uh game finder uh by handle game handle and then game game equals
great field for that okay yeah I'm doing a fair amount of of work um that uh is not at all test driven uh and not using
as much refactoring as I normally do uh yes that's that's I I was also uh so I think we're going to have some failing
which is the player connector does not yet have final because we don't have a game finder um and so this uh nullable
that right and now it's not found because uh we don't have a good nullable um that's I guess you know if nothing else
having Cody around gives you blame uh oh that's interesting so configure nullable uh so let's see so we want to replace
this because we don't care about the member store um in fact in this case we might not create null with our member uh we
don't have a member we'll have to create one I could just give it a member ID and let it figure it out but let's do it
the a variable for this I know where it got Snippets name which I am using somewhat inconsistently but we're use an
username because that's what principal gives member oh you actually imported it what away all right because we still
haven't found the game that's nulles yeah I'd be interested in that boiler plate too if you have an example so create
that uh we'll create our game store and then we'll save it like already this is boiler plate all right so now we've got
a different failure um uh and that's because we created the is that something I want as part of the crate maybe maybe uh
what does this expect uh member ID name which is uh my name is green oh wow Cody can you fix this for me you oh yeah I
should actually just be um and it feels like the nullable I could pass in the player and it could figure that out the
player's ID doesn't match because we don't ret oh because right we should not be doing what we want is Cody uh so this
is a little messy I'll clean this go that was a little bit more work than I wanted but um here uh the mo broadcaster
needs to know the player and the game although this right uh this should all right so that works um there might be some
further cleanup I can do uh like the player connector certainly I could create an even higher level um feels like
there's stuff I can simplified first no I can't cuz it needs the the mock broadcaster um I don't need the member ID so I
I could even simplify this matters game but I think I'm at the end of my brain capacity which is why I was planned on
doing a short stream today uh but we got a failing test so our next test then is going to be uh well there's probably
some stuff we need to um spring point of view because we introduced a bunch of things oh really it's happy I thought I
saw a red squiggly but it seems to be mind um so let's do our commit and oh my uh yeah did some doesn't know anything
about connected um this I moved that ah oh no the configuration's right and for this just introduce Tailwind it all
right we're at the end of another stream uh so next time which will be next week um we will now that we've got uh our
basic we've got our our Port interface uh we've got our use case our player connector um we've got test so we know that
something that happens here is actually broadcast I think then the next step is actually to create the real broadcaster
we've already got most of that um and then hook it up to uh the incoming websocket waiting room I'm not it's always DNS
jonice right always DNS glad you got that sorted all right so thanks for hanging out thanks for the help folks um and uh
as always join the out in a little bit more Advance uh and a little bit more reliably find out when the next stream is
um also as a reminder we're starting we're we're in the we're going to be uh narrowing down the books to to vote on for
our next book club uh so check out the book club Channel and um that's it so have a have a great rest of whatever day
left for you uh have a good weekend if if I won't see you in the book club and I'll see you on the bye
