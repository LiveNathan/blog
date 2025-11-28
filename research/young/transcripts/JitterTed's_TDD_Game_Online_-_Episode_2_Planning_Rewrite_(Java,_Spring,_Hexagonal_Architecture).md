# JitterTed's TDD Game： Online - Episode 2： ＂Planning Rewrite＂ (Java, Spring, Hexagonal Architecture)

**Video URL:** https://www.youtube.com/watch?v=PnuWxdVwKFY

---

## Transcript

all right hello folks good afternoon good well uh so welcome to uh another episode episode two I guess if we're going to
be counting of working on getting my tdd game online as a reminder uh of what the game looks like looks something like
this uh so this is the the board layout and yesterday we were working on basically turning the the game into into a
state machine so uh what I'm going to do today is basically just review that and go back to to jera and start planning
out some some steps to do um yeah and that's that's what we're going to do so let's get to the code uh no I didn't I
didn't do a get push I should do a get push because as I mentioned uh yesterday the um let's here um that's the Ensemble
timer we're not GitHub yeah that's fine um right it did not do a good push uh there hasn't been a g push for three years
that's that was basically the last time I I worked on it um before yesterday uh so one thing as I mentioned yesterday I
I'll I'll reiterate is um the project is not open source so open source has has a very specific meaning um despite some
people not being clear on what it means uh if it is an open- source project that means it has an open source license
which means uh usually you are free um not in terms of price but free in terms of what you can do with it I think the
word free in English is actually unfortunately very confusing um people say free is in beer not as in so not that that
makes any sense to me but basically you if it's an open source license you can take the code and put it in your stuff
and reuse it and do whatever you want with it uh as long as you abide by by the license and there are various open
source licenses that are that are approved this is not open source if you take it even though there's not much there
right right now if you take it and run it on your own I won't know about it but if you try and sell it or provide a
service around it uh you're going to hear from me um this is under uh what's currently uh a fair Source license um so
the idea is that you can see the source which you can see because you're watching it on the stream anyway uh but it's
not yours to to do as you will um if you want to license it you got to talk to me um whether that will change I don't
know but that's the that's the current license and I just want to sort of put put that out there yeah Freez and freedom
is not in beer is like I I I prefer the free is in Freedom and and not as in puppies um just cuz I find that more more
amusing hey there Jonas welcome um anyway so I should do a push because there's no reason not to so let's go ahead and
do that uh actually let me do a commit and then I'll do a so this has all of the uh stuff we did yesterday uh in terms
of upgrades and and such um so let's close that uh you can go away you can go way with trying to format this a little
bit better let's see if I can do that uh will that make it will that better uh yeah all right I think that's that right
uh that that that this is sort of in the center here it's like why isn't this at um I don't know how much I want to I
want to I don't know how much I want to bike that oh you wanted to play around with that yeah sorry well now you can
down uh predict test will fail that really goes here I don't think that makes any any difference in terms of of stuff um
I wish plant yl could do is sort of export it as I know it can export as a PNG it would be nice if it it could export it
something that's more manipulatable maybe an SV G or something know uh if I put an up between predict see one I guess
that's somewhat better uh can I do an R here there we go thank you that helped um so still long I would like it I mean I
almost kind of want it you know where it where it looks like like this um and that's the state state diagram but I I
don't know and I don't really want to spend the time trying to get it to look that way um but at least uh at least the
entry Point's in the right place and it sort of goes down and then the last step is is here that's that's fine um and
there oh that's even better there we go all right that's it uh uh it's it it fits on the screen the decision's a bit
weird worse yeah that that's okay that that's that's good at that's good enough yeah and if if as if you want to make
some suggestions um but I think this is uh there's no Crossing of lines which is really what's important to me um
because I just find those really confusing uh so this is this is more than good enough so it these no all right I'd like
them to disappear but okay um so we've got our diagram uh let's see can we zoom in a bit um and command causes change uh
so each player I guess has its own copy of the and so let's see so the commands that um draw card um and also draw full
so basically after your turn is done you often draw back up to to to five cards uh the other things that happen are you
card play a card so uh the board has nine separate tiles it also has so going back to sort of my mockup where is my
mockup too many windows open there it is so uh there is this is let's annotate annotate text I might want to use a
different um this is the player's hand let's make uh this I I've been calling the workspace um but I think I'm just
going to call it area and so this is where um so as where is the button there it is so as you're playing that so if you
wanted to exit here you discard so let's say we did that already so those are so we've discarded two cards to get from
here to here um we play a right code card so that's a play uh so that goes here and then we move so that's uh a
transition that takes you from one tile then you might want to play a less code card so that doesn't cause any state
transition but that does cause uh uh clearly a state change so your play area is active and then if you play um a
predict card that then triggers the test is this one which is if you have one or more less code cards to play then it's
as predicted um so this gets put in the uh test results discard pile and then your prediction came true so you um so
that transition is actually dependent on the the tests as expected that's what we that's what we had um yeah I think
Inplay is is is what I call it or the play area so once that happens you discard your play area yeah so that's what
that's what we'll call it I think I I originally called it workspace because I wanted to sort of have this sense of you
know that's your your your codebase your code workspace um but I think play areas is what I've and um text I really
should switch tools but area um there is one other um thing that happens which is your um so for example the the tech
neglect or Tech Deb cards like those um those stay in your play area uh but they're really in a different area because
um they basically stick around until you um so I think I think I want an even separate area for that so like when we're
playing the physical game those are are kept separate from uh the area your play area cuz the play is pretty much for
your writing code less code um predict um these stick around though uh as I said until you until you resolve them St of
Shame um so this basically the tech neglect area uh and so maybe is so we'll slice this here uh why is that that color
that's a terrible color make it uh and of course like anything else names are can can always change um yeah I'll switch
cameras in in a second uh so that that yeah okay so so we've got play area and Tech um I think those are the two areas
here uh so so there's the uh tiles there's the um your uh pile there's uh and then there's the results and I think
that's it for sort of that so it's per game and then we have per player we've got uh your hand your um what do we just
call it your play area and your Tech neglect area uh you also have your commit tracker tracker uh and is also six die uh
and I guess technically you have a pawn sure so you got a pawn you got a hand um you got your play area got your
technical act it so those are sort of our our our objects as it so player is on a tile technically it's the pawn that's
on a tile um but I don't know if I want to differentiate that so player is on a tile um yeah Pawn is just a
representation um so players on a tile players command so we got uh draw card discard card play card is there any other
action that they do um I think that's it you either move play uh well you can't actually do nothing so uh you must end
your turn um there's there's a little bit of of uh uh variation in in terms of can you just skip your turn um so I've I'
ve played it where you no matter what you have to play or discard three cards and that's your turn uh I and then I think
I and I have to go back at the rules that I wrote um it may be that you could I I don't know if I even specify this
again I have to go back to the rule book um the other option is that you could just say there's nothing I can do given
the cards I any uh so you I guess you could just end your turn I think because I want to make this flexible over uh like
I don't want to restrict anything if people want to play Play It That Way um I think that's okay so basically end
command um so then there's then there's something keeping track of um so we have sort of the the state machine for the
board itself uh but what we need machine I don't know if I need us full fullon State machine diagram uh but the things
they can do um basically what Define what defines a term yeah I don't I don't know how I'll end up implementing it I
don't I don't want to pull in any kind of libraries for this because I don't think that's that's needed um if it turns
out that that it's there needs it does need to know though like uh is is your turn still going or is your turn up um so
I'm going to delete this because I don't think that applies so maybe it isn't a I mean you could probably put anything
in in a state machine uh I don't I don't I mean it may yeah I'm not sure what what to call it um we'll leave it as the
so either they player discard three cards or explicitly and so I'm kind of envisioning processor and so so like do I
Define commands as their own objects that then go and change the state as appropriate or do I have sort of one place
where commands come in and then it sort of dispatches I don't know that I have a uh a sense for which one is is better I
kind of prefer the latter I think Java especially with with switch expressions and things like that I think might make
the latter one better um but I don't I see started the more I'm writing this the more I'm wondering like do I start over
like I've got a lot of code I don't know some of it's useful I don't know how if if all of it's useful I probably keep
because those work well yeah I'm tempted I I'm I'm very tempted to just start over and then uh scavenge code from from
this project um so let's how am I going to do that uh I don't think I want to start a new much change this to be a not a
multimodule project put all the dependencies up here uh and then those subm modules in a sense are ignored they're just
happen to be just directories where there's uh oh creating a new sub module that too um that actually has the advantage
of so if I if I remove black backend as a module uh and it's just a directory of code then I actually lose all of the
the parsing right cuz it doesn't consider it part of the project anymore um although that might be a standpoint do I
care I don't think I care let's try that uh so let me do a commit um oops uh and then let's let's say we end I don't
know what you think you're doing okay um let's look at the Palm um think I can just this so if we get rid of that and do
packaging and reload uh let's do a I'd like intell to really reload because shouldn't be picking up anymore I don't know
why it still thinks front end is part of this project unless it's just looking at the pal file so let's let's rename
this um actually go yeah and I I don't I didn't quite understand that dialogue um but that's fine uh this pal is no
longer recognized as a um and we could probably delete this just sort of unparsed java code which I problem so let's go
look at our project structure so that's fine modules that um that's fine we can just yes please create all of these oh
that was awesome thank now what do we want in our pom file so we've got uh the websocket we got the dev tools we've got
test I think there's a more recent version of this yeah so I'll update that um now and I need to tell it to please stop
asking me to import and at some point I'll bring in Arc unit and the other stuff but for now that that's fine so uh so
let's go ahead and create some packages create uh I'm actually going to use my other domain uh to really clarify that
it's adapter and that's all we need for now um all right so what's the first it's have a whoops and I can close that uh
so let's see um so uh I divide adapters into inbound it so for example um like here so everything uh I basically split
it down the middle uh and everything on this side are inbound adapters aliser Cobrin calls those uh um driving or
primary adapters I call them inbound um Fetchers and so on are yes are Fetchers notifiers and persistant are outbound
adapters so any kind of user input is always going to be on the inbound side because it's always going to trigger
something to happen in the application um outbound are or what aliser calls secondary or driven uh where the application
initiates it the application initiate input it can't by sort of by definition does that answer your question uh do I
differentiate between the in oh I see do I differentiate on the inbound side no because they're all triggers so the
reason why I differentiate on the outbound side is because that's where you need test doubles so you need spies or fakes
or stubs um but on the inbound side you don't because you're talking you're initiating or triggering actions directly uh
I guess I call them triggers that's what they do but um that's all they do there there are there's nothing else that
that on the inbound sign that doesn't trigger because if it doesn't trigger then what's it doing um but sure yeah the
inbound the inbound application so what's the first game player creates game because there join uh have I assume you've
watched my um astred remind me to uh to contact you offline about about something um this has to do with a thing I'm
working on with with CLA subury which is very much relatable to to hexagonal um do I want to do this before I get to
this so somebody needs to if you're going to join a game the game has to exist if a game doesn't exist somebody's got to
create it uh and somebody is going to be uh what did I say um not this account do I want a play player to be able to do
want someone who's not going to play to create a game do I treat player and account the same thing I don't know that I
have the answer to that we'll just assume that game um but I think right now I can uh oh host um maybe that's a better
name so you so I Envision uh that let's say a company has bought bought a license for you know a team whatever size that
team team is um any one of those team folks can initiate a game uh and then invite others with a link um or if I know a
game is is happening uh I can go say show me the games that are available for me to join and then I can I can choose one
of those one um so let's also start creating uh ubiquitous language there's player and there's host um obviously things
like game and deck and card uh and tile Etc so that that we have we have I think I'll call them team for now can't
decide on teamer teamer or group uh goal I don't think there's a goal um I mean there are sort of what do you what is
the wind condition uh I'm not quite sure what you mean by that the goal is to have fun I know um yeah cuz wind condition
can change box um so one thing that I I think I'd like to think about earlier rather than later is before uh we had Pawn
that indicates where a player is but there is the variant of the game where there is a single Pawn so the pawn is not
directly connected to a player in that case it's connect connected to what do we call everybody who's in the game are
those just players because I want to treat them as a group so there's team uh which is so can and then there's Group
which is set of players currently playing a specific game yeah I agree that's true for for uh sort of a development team
but I think we're in a different domain um but I do want to differentiate those because there's um and it's certainly
possible that a player representing sort that that an account representing a player uh that that an account can have
player representations in multiple games but the reason why I want this term group of like who is actually have game or
they're they're members of the game um is that uh again that variation of either player has a single Pawn uh no they
wouldn't have more than one Pawn um I mean I can conceive of a variation of the game where where you actually
controlling multiple pawns that that would be very much sort of to simulate like I am a developer and I'm actually on
multiple teams and I'm or I'm contributing to multiple code bases um I mean if we if we go there then what a many to
many relation pawns higher more dos that's always the answer um that is interesting because if I mean that's sort of
ultimately game um for example you got six people who want to play the game uh and you group them into two Pawn that
sounds really complicated like I can I can totally visualize that happening with the physical is that yagy that would be
middle um what I'm trying to balance here is like what decisions do I make now that will be hard to reverse later um
because if you're going to have two people playing the same game then it's then it's basically sorry if can have sort
two sets of three people playing the same game or are they not just playing different games because we I do those things
with a physical game because there's certain restrictions but with a virtual game I don't know uh one player playing
more than one Pawn I actually see the opposite I I I can't I can't see a single player having multiple pawns but I can
certainly see multiple players controlling one Pawn so that's the that's the main variation I have is that if you've got
four players everyone is moving one Pawn um so yeah so I'm going to call this yagy for now you ain't going to need it um
although we might um maybe this is just premature I don't know I don't know if it's yagy I feel like I can totally
conceive of rules and variations that that use that but I think that's support where the group controls a single with
that variation comes a whole bunch cards uh which is not something that I have in my rule book right now uh it's in my
variation rule book which I haven't published yet I need to do that um cuz pretty much the the yeah so so very much
switching it from uh uh a versus what's it called um what do you call a typical game not adversarial necessarily but
basically turning into yeah so competitive versus Co-op um so this variation where you have everybody controlling a
single pawn and they can trade cards then it's a and so then there are obviously V that so there are lots of there there
are quite a few board games that that are Co-op um and I hadn't actually when I designed the game I hadn't thought about
uh co-op in fact it was much more adversarial uh in in its original original incantations um so the for example the uh
these red cards could be used sort of as Attack cards and you can play them against an an opponent um versus the way I I
I think about it now is when you when you get one of these Tech neglect cards it's like you discover that in your in
your own code base yeah pandemic is is a great example uh so right now I'm just going to have two variations and of that
I'm going to focus on the the competitive variation first um so somebody creates a game the host do they have to be part
of the team sure I think that's an okay restriction um yeah passing cards around uh would be in the co-op version um but
I I want to make sure that I as when I get to when I get to yeah I don't see that as as something that is sort of an
architectural decision that I think is just implementation um the thing around uh player to pawn ratio that that feels a
bit um because now it's pawn yeah so that that might be more involved um so the order so uh the flow of the happen yeah
I don't know if I'd call it owned by the game as versus owned by I I could add an intermediary object right so I could
create for purposes of of internal structure um literally uh a thing called a group that very much is um from a pawn
point of view the group owns the pawn as opposed to a player and then players are belong to the group but I think I can
I think I think that we we can figure that out uh it wouldn't be owned by the host because the host just initiates the
game it's really the group that's act actively playing it because it at um yeah uh do I want a game master view I um cuz
certainly you know while I'm testing this thing or even while I'm you know I might be uh I might be a coach who's
facilitating four games that are that are being played and I want to take a take a look at them and I would like sort of
an admin version where I can uh Force things to to well there are two reasons for that actually so maybe it's not just
admin um so this is really interesting because um as a coach this is literally what I do kite hold on I have to switch
to this view it is a kite okay that looks like a dragon to me all right um I really like this so this is so it's
interesting because one of the things I like to think about is um as an operator of this system uh I would like to have
observability and be able to see things and control things but it turns out as a coach I want to do that too um and this
creates some complex permission stuff issues that eventually I'll have to figure out whereas an admin is you can sort of
think of as like a super coach uh they so one of the interesting things um that I really want for the implementation uh
is very much replayability um in the sense of how did we get here what happened so a little bit around analytics because
I want to Foster uh basically provide data for for a retrospective that you want to do either while the game's playing
or at the end um and and a replay like show me the game how it progressed um you know at at obviously faster than than
real time speed um so I want to make sure that possible um player joins a there um and then at some point the game
starts because obviously not everybody's going to join you know at precisely the same time so there has to be some
trigger right uh to say let's start the game it uh that's annoying game and we start a game um so as part of start game
uh first so since it'll be looking something like this you know there'll basically be people around clockwise if anybody
knows what that is anymore uh there was something I don't know whether it was a TV show or something else where it's
like uh they said clockwise but they actually motioned man so I was like did I put enough sweetener in my coffee this a
little so decks are shuffled cards are dealt starting player is chosen uh pawns it and so once the game is started now
plays yes CH children these days are very much used to swiping to get stuff um unless anyone has a better idea I think
I'm just going to implement these pieces so uh or maybe I'll start with one I was going to start with two that and and
internally one so what do we want that to look like interaction you start with three um the thing is like this code is
almost all all code yes I'd like to start with four um but that's going to require a whole stuff um I don't think this
will take that long uh so what do we need to create a I like to give things names so we'll I mean I can think of other
things like I don't want more than four people to join or things like that but I'm not game that hasn't started yet
because there definitely right so for a game that hasn't started yet is that just a game that's not in that St state or
do I create a separate object for that I don't know that's probably overthinking um so so I want to show um want to ask
for uh uh so we create do we whatever we create um so now I want uh players to join I'm starting out I'm starting off
with game uh provide identifier that's right uh so player so this way I I Sid step the um show me all games that are
available basically type in the ID for for the game hey there do attitude game you seem to misunderstand what Co-op so
uh DOTA attitude had to reference the refactoring book today sounded like they wanted to rewrite the whole project oh
yeah well refactoring is hard it's easier it's often easier to to just rewrite it if it's small um which is a form of
refactoring depending on where test what's our first test um what do we call uh yes there are there are Cooperative that
so let's go ahead and create game of fire and we'll just create a class uh and I'm creating the the class first even
though we're doing tdd uh just so I have something to start with so we'll call this game creator and then we immediately
jump to creating a test because then it will create the correct packages and things like that all right um let's keep
this uh somewhere uh let's oops put that over there uh we'll go commit and I pushed it two remind me to push if I don't
push um I'd like to keep it um so what we're going to get from the outside world is game there's nothing it provides so
I don't need to start there uh so really the first thing that um a host created a game with a name need to attach it to
a host I think I'm going to put that aside for now so our first test is something like um creator and with that game
creator with actually I'm just going to call it because that's really kind of not relevant uh so that that fails let's
go and create the method um we actually do want it hold on game uh we will have to create that domain why is it not
sinking that's really weird see that put it in the right place did it put in the right directory put in the right
directory I don't know what was up with that uh that will flip over to here go back to here create this thing um yes yes
why are you not oh it put it ah did it was staring me in the face and I didn't realize it all right let's try that fine
which will fail because it is null so that's easy enough uh let's go ahead and start uh creating some test
configurations can remove that and remove that and this will be our iio free tests which will'll store the project file
file uh and we'll save now unsurprisingly fails for the right reason now we can do a new I think we can say that the
created Game's name is assigned Boolean and that that is equal to uh name of pass uh we can refactor we can basically
promote this to a field here this will Now fail because we've hardcoded it um but then we'll be able parameter now that'
ll is uh so I want to optimize but I want to commit without I just want to commit uh push I mean I want uh all there we
go all right so that's um that's basically that uh now we need uh a game to have uh some identifier um this is not
necessarily the entities identifier um this needs this I'd like to be more of a um and I've used this elsewhere um I
think I can drop down to over uh so this is uh new game has human um I think I want to use uh a library for that uh but
let's write our test first and then we'll get that uh get that um there's no way the test can define whether it's human
readable so I'm just going to say uh nonnull identifier uh New Game signed identifier yeah the windy dolphin right yeah
I'm going to steal it from from the format hero uh whatever the game um and we'll say and we'll assert that name uh I
want to call this ID because it's ID can't think of a better name right now so I'm going to say human readable ID uh do2
attitude asks why not start um because I'm I'm trying to to do so one thing I found is is sometimes if you start too
deep uh you end up in in in a somewhat awkward state so I really want to do at the start of the what do you want to call
um especially since these steps are are are really not not very this before we create it I want to see if I say is uh is
not empty is not not null and is not empty or blank blank let's create this I was hoping that if I had those asserts it
would intellig would offer something other than Boolean as a return value but clearly it's not so we'll just say string
um blank okay well I don't want to use name handle yeah one thing I want to do with with this is I I kind of want to
have I want to pretty quickly get to something that's that's visible because it's nice it's nice to see Vis visible
progress display name I'm not sure that's any better uh yall keep working on that let me know what you find um so null
oops blank well I I will need an actual ID uh that's going to be completely separate generate a more readable ID from
the ID um so the the idea behind this identifier is I want something that's easily typed into a box a text box so that
somebody can say hey can you join the Wy dolphin 68 game and they type that in um so like you could easily share that in
in other ways might be a bit of yagy but that's yeah so there there a lot of uh these kinds of things where it's you
want something that's sort um let's try it on for uh game one human readable name okay so that's an interesting question
how does the game get a human readable library port um is a bit of o a bit a bit of Overkill right now so this test will
certainly fail because we're always returning the same handle I guess I like handle let's rename it I don't need a
library um I could do uh why why would I do it myself yeah I don't think I I need to I'll I'll introduce a port a port
later um so let's go let's go grab that Library I forget which one it was uh it there it is oh I wonder if the library's
been updated I forgot I hadn't checked in a is there an updated let's go take a oh they're on V4 okay what what what
came out in interesting yeah so I actually contributed um some stuff so that it could be incorporated into a native
image but now they're up to V4 all right yeah so just to be clear this handle is solely for I want to find this game
with something that's human readable versus here's what's basically a random number uh unique identifier that's for the
database um all right so here what we want to return instead uh actually we probably want to make this a handle um may
as well have this injected into the game so that way the domain object itself is not referencing the class uh so let's
out um we'll go to game creator uh and so here we'll extract this to a variable um all our tests should still say um we
can basically say I forget how we call it I can just pull this this port over there we go uh so now I think that'll pass
no what did I do wrong um uh yeah then this doesn't make sense at this level um so let's move this test to where it
belongs here uh so this is instead of new game okay right so many people might call game um but they'll still be unique
so this should now work yes okay all right so we'll check that off we commit uh games now have sure yeah you can if you
you can put Emoji in there if you want now um now we want a player to be able to join a game so this is going to require
us to player so let's clarify what we mean by player uh and then I need to take a um that um so the idea is that you
could certainly would support uh for someone who's in the account uh they could play one or more games well they could
play Zero more games um but when they're in a game they player all right so that's what player means um so there's going
to be all sorts of stuff around this other subdomain uh not this this so all this this subdomain stuff um teams player
uh so this is really account not player and so in here why is that blue um in here we've got uh player and game yes
subscription as in payment game yeah there are there are some uh uh data Faker uh which is a tool that will create a
bunch of interesting and data uh we're going to be event sourcing all the things so one thing uh uh one so from an
architectural standpoint uh I'm um might even have a flavor of cqrs even though there there'll only be one one database
there'll still be uh two pipelines um yeah eventually it will be linked to stripe and PayPal but that's getting way
ahead of um it's interesting you mention subscription because one of the problems with using something like stripe for
my subscription handling while that means I don't have to develop it uh it does mean that um I now can't use another
payment service without having to write the subscription stuff myself so I will unlikely be using that in fact actually
um what am I saying I'm not going to be using strip uh I will be using uh a merchant of record um so Merchant of record
one of the one of the advantage of a merchant of record is I don't have to deal with taxes um thatat GST sales I don't
want to deal with it and uh so I don't have to um and so I will be handling this internally yeah uh one thing I have
learned uh over the years is don't do yourself are they dealing with time zones too uh time zones aren't going to be a
problem here um unless you're saying end that's actually an interesting question question um but if we're concerned
about an an my subscription ended 8 hours earlier than I thought uh I'm really not going to that all right let me take a
quick break and when we come back um so we've got the human readable handle being generated uh but now we want to be
able to do something with with that game um give give to handle so I'll be right back after this a all right and we're
back um and yeah I suspected you were you were you were mostly joking suige about the time zones but uh time zones are
everywhere and yeah like if you run into problems it's either DNS or time zones that's what it um so we've got that we'
ve got uh the handle um so let's see so the next thing we want taking a step back and thinking about Aggregates um game
is an aggregate I think this very much going to be like uh for those of you in the Ensemble very much going to be like
the the blackjack players um in this case players by definition only make sense in the game aggregate so uh they will be
a full full-fledged object they will likely have some kind of account ID that links them to another aggregate uh because
that's in subdomain all right because these These are basically our our our subdomains so what so players join game what
is that made yeah aggregate in English means a number of different things um but in the context of domain driven design
it has a a fairly specific meaning um and it's mostly about your transactional boundary so I want to be able to modify
game modifi game State um but while that's happening while the game is being played uh somebody could pay their
subscription and those are two completely disjoint transactions yeah separate documents in a in a mongodb is is is
another way of looking at it because those are for sure separate things they may have copies of information um but
they're certainly separate transactions so I think there's a deeper question of here is what what does it players and is
it a list of players or players hey I already agreed with you that that cars are value object no I'm kidding uh because
there's a lot there's a lot here so player players join game um means that game has to track players uh that does not
require a repository except that it does because they're joining using an identifier whether it's a a database
identifier or some other identifier it's an identifier and whenever I see identifier I always think where you who who
knows all the hand there's no other way I can do this repository uh player needs reassign ID um tell me more I don't I'm
not sure I see that uh players will have identifiers but really they'll be sort of the scope of their identifier game Ah
that's an interesting so that's a restriction that a player again um let's add that as a sub substep uh so this is this
is misleading players don't join because players don't exist until you yes Jonas Jonas uh uh uh picked that up um
players don't exist until they join a game so we just said that uh there's team subscription and there's oops let me
finagle with this for a second users yeah either um and teams are made up of multiple accounts join uh and right and so
if I so which is a separate thing than than reconnecting although they might look outside yeah well we'll get the months
uh so it's not players join game not sure if this is a separate item yet well so I was going to write uh a person can't
join the same game twice in otherwise they can't control two players no so um a persistent game always reloads right so
that's the thing about any sort of these web apps is you're always loading the game doing an operation then persisting
it and it's gone from from memory um but a game that's in started uh so again there's a difference between a person
joining a game and becoming a player uh and a disconnected um yeah I wouldn't I don't think I'd be going by by IP uh I'd
be going by you have to log in right so there's login stuff which I'm not going to worry about uh and now we know who
you are uh as a person um and now if you want to join the game you say join the game you give it the ID and it says oh
you're already there so I anything yeah connecting is is technical uh and reconnecting is technical um but the
operations that you do look the same to the user right because the steps are if if I just got disconnected how do I
reconnect I go to the site I might already be logged in because I have a cookie if not I log in now it knows who I am as
a person uh and I click the button that says join game and type in the ID and it would recognize because the person has
a unique identifier oh they are already in this game as this player who has an identifier so there's a mapping between
so the the player has who's the user that is is you Puppeteer that concept might come in handy but I I don't think so
just yet uh does the Game Stop when a player um if it's their case well I'm thinking both both ux and and domain at the
same time uh cuz I'm thinking like what does it look like to to the outside but internally um there's person how do you
join a game a person joins a game and they are now a player in that game yeah there there's going to be some kind of
timer um for you're going to have some kind of time limit uh my my Baseline assumption though like that's a nice to have
my Baseline assumption though is that these are people who know each other um and are likely connected using Zoom or
Google meet or something like that so this my intent is not to create something where there's no other communication um
my intent is that this is uh you're playing the game together with at least audio um and that this is the platform that
you're playing the game on but that there is the the main channel of of of of at least audio if not audio and and webcam
yeah I don't know that I want to get into text chat I think I'd like to stay away from text chat um and yes if I wanted
to create a timer I've already got one that code was I mean because honestly like that's the main point of of of of the
game is is like it's not just the game while you can enjoy it on that level um really the power is is fostering th those
discussions of you know what happens if you you know darn it I my prediction was wrong again maybe I should write less
okay so what do we so if we have um so a game exists we want to join it uh that means I need to know um that means the
game needs to have an identifier we already have that that's the um so what do we observe we ask the game so it's no
longer the game creator use becomes so the idea is uh there's a person uh and I say game joins handle identified by uh
estra says isn't a isn't it a player Joiner like I think of it as as the player but I see what you're saying uh player
why I think it's okay for now but uh I think player Joiner just I mean really if these are are more granular use cases
it's really player Joins game if I want to phrase it that thing yeah I mean I guess you could read this as I'm joining
games together or player join it could be I'm joining players together but it's really uh player join Joins game did I
want to phrase it that way it's not the way I usually do it um but mean yeah game Joiner joins games together that's not
what we want let's let's phrase it this way um so it's so we're actually being a bit like uh so let's see so for this
we're create that class uh that goes in the there and so now we create and so we basically give it the handle we need to
come up with some other ones besides this but this will work for now uh so that's the game um although I guess I should
want uh what is this return I think this should return yeah if you really get down to this is a command object then you
pretty much do just do execute or something um so there's two things we want here player uh the other result is uh
player has the person's ID okay that's annoying okay I just turned you off still I turned you off why are you still
complaining whatever uh so I think the first thing I player uh no first thing I'll ask is the um uh which means I need
to create a game that is this actually this will be game I really do wonder what the algorithm that intellig uses in
this situation like it can infer here's a good variable name for this class I yeah I don't understand that that rule
either like it doesn't recognize new lines as being a an appropriate case um so create a game um oh right we give it a a
handle so here's where we can say ready dolphin uh or do I just go through the game's Creator I think I yeah I'll let
I'll let it come up with it yeah confused Turing yeah yeah it um so here uh and we can then game do I ask the game do
you have this players I'm going to need the players ah um technically players the the list of players is a a um actually
I'm I feel like that's a big step uh so I'm going to go back to this I may I I will likely need group but I'm not ready
to commit to that yet okay um so this test will fail because the player is going to be null because we're returning null
and that's indeed how we are failing uh so let's go to our join method um right so it expected this to not uh so what
work yeah I could return an empty list but I'll I'll go one step further this won't work because they're not equal yeah
uh so let's go into player and uh hey he's he's approved of of taking big steps it um I was about to add an ID here and
I'm wondering if I want probably not now but very soon I think I will incorporate uh some of the J molecule stuff around
identifiers but for a uh I'm going to use long even though normally I'd use an identifier because I'm not sure if of
that of that transition so it's probably simpler to ID and we'll create uh a getter for parameter okay oh the whole
point of that was I there we yeah thank you all right so we got our equals and uh if they're the same instance true if
they're not the same instance if it's not even an instance of player false uh if this Dot ID matching I I was under the
impression the the clearly wrong impression that the scope of this variable was this true I just learned something new
about pattern matching I I guess I kind of assumed that when you do an instance of you basically can define a new
variable but I thought it would be this the scope of this block um but it's clearly not huh so what this is saying is
that if you got two new objects that don't have equals yeah all right yeah I was I was I just saw that I'm like we
should have an equals there's not going to be much to say other than at least right now uh the identifier oh wait you
stream Joiner seriously actually that's not so bad okay so J you think if I remove this even though that would change
his behavior that the scope of this would no longer interesting the scope rule on that I I guess I can I guess that
makes sense from a from a data flow unexpected I mean it's cool um but it's certainly a gotcha cuz I can imagine what
the bik code generated looks like no the B code won't matter because this is at the comp I don't know that's just thank
you for pointing that out because at least now that makes a bit more sense in fact does that mean that here that's
unexpected makes it makes sense now that now that I see it this way um but yeah uh that would not be my initial guess
for for how that works but of course right so it's basically saying yeah okay yeah there's a little bit of a of a of a
sharp edge um luckily compiler helps us a lot okay um that was so um so when a player joins a player uh ID so it's not
just that player is not null I think we can put that aside for now and I think we can say that the ID fail so we need to
give them an ID when um yeah I don't think you can have a player with a null ID that doesn't make any sense cuz a player
cannot exist outside the scope of a game and therefore they must have an identifier yeah so let's uh let's nail that
home so you can't do that uh and then therefore this is final um and yeah so then it can't be null which means we can
back off on our equals but I'll leave it there it doesn't hurt uh so now we need to come up with an identifier it is it
suggesting turn into a record yes it is okay but we're not um this should one um no because my test is saying that
that's what it's going to be right so the player ID should not be uh player with IDE of one okay so that should actually
now pass no it won't because the player will not be null it will be assigned an ID um but when they join we don't do
anything with the game so from The Game's point of view uh and I wonder if that's maybe a different test well it's
really about joining the game I think I'm okay okay with that yeah I don't think I need to do a null check on on an ID
because eventually um that will structure uh actually here now we should list so it'll fail because it doesn't yeah I
guess I guess for for the way I way I've done things that internal Constructor is not exposed to anything outside the
application and so it should never sort of be poisoned by by bad input um but I could totally understand wanting to be
overly protective uh so Shand do 16 how to master oop I think that's a great question uh to ask in my Discord you'll get
there's a bunch of resources and you'll get re resource suggestions from there um so if you're not already a member of
the Discord uh because it's not something I can basically give you the answer because the answer is essentially right
code um and get feedback but you probably want some good guides for for that and that's a great question for the Discord
yeah exactly destroy destroy all bad data not just nulls but basically all invalid data uh as as early as possible yeah
and if you're using makito to do do that well you deserve what you get um so uh let's promote this to a field this is
Constructor um we can basically say this is uh actually let's do this um we can fail and then we can promote that to our
Constructor that's a bummer uh we don't need that fail um except what I wanted to do was move the assignment to the
field um so I've been kind of wondering about this is it the player Joins game responsibility to do the lookup of the
because if I make it the player Joins game responsibility uh then it has to know about all game handles and have a map
of handles to games yeah the 1l uh hard coder search will certainly uh uh go away um once identifiers um yes the here's
a handle give me the responsibility I've been sort of of trying to avoid uh creating a repository further uh except
because I've got game creator separate from player Joins if they were in the same class then I could basically hold on
to this game uh and then this could use it without bothering to look up the handle is yeah this I think I need I think I
need the repository yeah um shandu 16 uh that's where you that uh is DDD only relevant to microservices No in fact DDD
uh works well with any complex uh any non-trivial domain so if you're doing a crud like thing where you're just reading
and writing to a database you don't need DDD you probably will want it anyway though um and microservices is not
anything you should be starting with if you're if you're thinking about getting started break nothing all right so do
that yeah if you want to get better at oop and get experience with it uh you should not be worried at all about those
deployment architecture level things um Mo I will put my usual rant in one line which is don't do microservices unless
you uh have at least 20 people who are who are engineers if you have fewer than that you have really kind of no business
doing microservices in for the most part where you have to be really aware of why you're doing them I came I know I just
said I wouldn't do a rant but I came across something on on LinkedIn and they were it was explaining microservices and
I'm like the number one reason you go to microservices is because your team is too big period and a story Java grunt I'm
dissing microser no um all right so player joins the game they join the game uh so when they join the game um it's
actually the game that generates the player not the game yeah you know it I I I really do feel like um all the good
stuff that that has served me well over over the decades nobody cares about because they just want to do microservices
uh not do tdd um and organize their code in in ways that that make no sense I really do feel like I'm sometimes swim
swimming against the tide because yeah anyway uh all right so what we want to do is we want the game to actually
generate the player so let's I can't think of a better name I'm just going to call it join um uh and working that's
weird I don't know why work uh so let's take this method we'll move it over yeah the Sam Newman book uh I think is is
pretty much on target um so what we want is we want game join but what we want is person actually let me undo that I
want to do this a different way uh let me hand in person oh actually let me hand in person in game and then what I'm
going to do is say on let me make this un unstatic unstatic ify it uh pass in person in I've let's try it one more time
join game and this is join game and this is person and game it wanted me to write a recursive method an infinite
recursive method uh okay so let's change signature because what I want is I want to prep compare this method to be moved
over to game want um yeah so AI microservices um I consider those fashion uh and eventually they focus um all right so
now game and that's what I want it so now join uh this should still fail in the same way and now I can go pass awesome
hey there b1g Blaster um I don't usually get compliments on on on light okay uh so we now have the player with a player
ID it's hardcoded eventually that'll come out in the wash um now what we want to make sure uh is that looks great looks
great on the TV look mom on TV player ID uh is equal to whatever this is which yet oh it dark mode it is uh which one do
I want um did they change something here because now there's two separate things there's the theme and then there's the
color scheme that must be new shows the last time I changed appearance dark does that just change what does that change
oh interesting it it literally just changes the editor color scheme all right let's not do that uh let's go to the theme
default oh that's that's really interesting does that hey it's dark um no let's go to Jerry okay no darker uh do I work
with other languages not really um I do some JavaScript typescript stuff uh but Java's Java's my main gig um all right
let's set our dark mode timer you redeem 10 minutes and so there we go ah Java grunt thank you so much for your 100 bits
nice to see you um all right so let's do that and let's do that I gotta say I'm going to Fumble around a bit here
because dark mode is different how many points for 10 minutes of dark on black I think the only person who probably has
enough points for that um which would be almost infinite is probably weat L because he he might even um because he I
don't think he's ever spent any points uh okay so we're saying is that player player uh person ID um is going to be the
same ID as as it uh what's it complaining about oh okay uh and let's create a it what's the problem here I didn't return
see I can't even write a regular method in dark mode uh transar probably has a bunch of points too yeah um and now we
want player to have person ID so we'll go ahead and uh create that be the more I type long the more I'm like I need to
move over to to to J molecules uh we'll return null sh sure uh let's move you up though and anyway you should be on the
right okay yeah b1g Blaster it's it's one of those like I've been doing Java since and there was never really a language
that like when C came out it was pretty much a copy of java so I'm like why would I switch um JavaScript wasn't much of
very useful as as a language for for for quite some time uh and the companies I work for they were all doing doing Java
so I continued doing Java and now Java is is awesome I mean it's always been awesome but once once they went to six six
month release cycles that that's where we stuff really started getting good um it does mean we won't see string
templates though until next year which bummer uh okay so this will fail because um we're never storing person ID on
player uh so person ID null right um so now what we need uh when we create a player it gets an ID but it will also get
um a person this uh suggest in a couple places do we wait where where else did it player Joins game test oh right there
um so we use it here is the only other Constructor um yes I I I said I was old my last name is Young so I'll always be
young but uh but I've been around for a while okay so um add in what we expect this to be is actually change that to
zero uh and this is person ID so let's rename so this will still fail because this will work fine uh turns out that this
value might not matter but it's equality I'm all right with that for now uh this is the one that matters and this right
uh and but now we can actually pass uh no it won't pass because when we actually add the player we give it zero so we
expect it to fail because it 27 is not zero look at that uh so now what we can do is say this comes from person ID now
that should pass voila all right um so now we look at jira so person joins the game um we don't have the human readable
handle thing we'll worry about get either when we get to the uh inbound adapter or uh maybe some high level application
service I don't know um so person becomes a CL player when they join the game yeah that's what this does this is turning
a person into a player poof you're a off uh this does not exist yet if a person tries to join the game twice we will end
up with two players yeah b1g Blaster I I totally um let's do commit uh cuz we've done a things so to me you know at
least in the programming language world like cool for me sort of uh is associate with with fashionable um and Java is
definitely not fashionable uh but I think fashion is also something that you know doesn't have solid core principles or
something I don't know and yeah so the so it's a good question of why have a separate identifier for a player if it's
always uh going to be that a person can't join twice so there's definitely for me a feeling of like uh I don't I don't I
don't like that there's something not quite right um and if I do end up saying huh you want to join two games you want
to join person but be two different players that's okay and then if that happens I I don't like reusing um uh so even
though yes technically I don't need a separate identifier I'm uncomfortable not having a separate entity uh all right so
uh oh look dark on is that a threat Jonas hey what bug I know I selected that and it's weird that that became effective
immediately I didn't have to apply it then when I went back to intelligy light that was weird it it had the the stuck
you got the points I'll uh I'll abide um do you want your celebrate points back Gast because we were you celebrating
light see I don't have my confetti uh uh set up for uh for OBS which is what I use for streaming here uh I have the
confetti set up for for when I pair with with Mike um I have to I have to get my confetti over here Grant yeah Bas BL
map absolutely I mean JavaScript I know for me when I when I finally went back to it it's like oh this is actually an
okay language uh a lot of the the yucky stuff was cleaned up and I think there's still a lot of outdated opinions for
for Java as well um all right uh oh just desan triggered the the dark mode all right okay um so what are we doing next
uh so person becomes a player when they join the game um technically this isn't true it um you would not Tri dark mode
twice why not um what what do I want to do next uh or would I that's why I say is that a threat to let's see so player
Joins game we do that um because we're being given the game and as I said I'll handle the no pun intended I'll handle
the handle later uh we've got game creator that's fine um game has a list of players uh I players so that way we can
sort of force identifier yeah so that basically gets us even though I'm I'm already at the many stage um that gets us to
the to the uh we didn't have the zero stage we could say a new game has no players but I don't know I feel like this is
good enough okay persons plural person yeah uh join existing game a yeah I'll pretty much copy that uh both added at uh
as yes um so this is person uh this person uh yes I do have these lines separating it cuz I found that when there was no
line separator so was actually harder to read um and here the Whit space isn't going to confuse anyone to say oh well
there's white space around this this must not be the assertion part of your test I think that's pretty clear that we are
now from here and Below we're in the assertion part so person uh sorry first person I know that's what went through my
head as like first person and and third person um so this is first player second person and so our expectation is um
player IDs are going to be assigned um do we want to say that they're not I guess that's what we're saying is uh assert
that uh first player is not equal player I think that'll fail because they're uh that's cuz see okay prediction uh
prediction failed yes so prediction failed because the test is right so yes pass for the wrong reason unexpected that's
actually because my test was wrong all right so this this is this should fail because they are right so one the things I
I've been trying to do is log when um when that happens cuz what I want is is to to go back pull out the the fragments
of video where it's like look prediction fail for this reason look prediction fail for this prediction uh failed because
test was broken yeah test test coverage and tests that are passing if if they're broken aren't really helpful have I
ever tried playing the game while coding uh no um but we will once the game is is it um and I'm pretty much going to op
imiz for uh getting the web sock like I really do want to do uh as full of vertical slice as I can to get in all right
uh so test fails fails for the right reason um so let's go fix that uh so who gets to generate this ID um I think this
is just going to be like an atomic integer or something an that uh oh what's what's prestol uh playing so the player ID
generator uh we want increment uh so that should so that passed uh unsurprisingly I broke L that is now I think what we
can do is we can say uh one um and then player uh person exactly that and I feel like this might even be um I'll leave
it but actually I think it let's we're going to be ending soon anyway oh 25 minutes uh I'm not going to be streaming for
that long so I'll I'll give you you can redeem a 10 minute if you want but I'll time let's figure out what we're doing
next time uh where that go there we are um so they join person cannot join the same game twice uh we did that so we
basically did one and many I uh um so next time we can do this um are we game so let's look back here uh host creates a
game player joins an existing game I think we are ready to start the uh and so sort of underneath that is constraint uh
H I was going to put in a constraint that you can't add players when once you've well so I may want to relax this
constraint later but right now to sort of protect myself uh I'm going to say players can't be uh can't join once game is
started so you show up late too bad um but likely I will relax this constraint uh certainly I want to allow for um
people being added after the game starts uh it's not a big deal it just means I need to you deal some more cardss and
assign a pawn and things like that uh if they drop it's a little bit more difficult but that's not a huge problem the
cards go to the discard the pawn goes away uh so that that's all so once start game is triggered shuffled and cards are
dealt to each player and basically all Etc all the other is that count as dark mode it's against a dark black mat uh
let's see so we have taken our persons we've turned them into players we've added them they get their Pawn assigned they
get put here um yeah good uh What else um so what gets me to a walking skeleton uh I think I actually want to once um I
guess I just said that but that's really part of so I think then next what I want to do is um start implementing the
adapters uh so um uh inbound adapter game um so this is going to be an HTT P adapter so once the game has started
everything is websockets uh and HDMX of course um but at this point um it's still all HTTP so so poost create game and
uh person HTTP all right so you see a page you button does a post person join game text boox for hand handle and submit
button uh also does a post uh how do we are um I am going to need some kind of login like thing I don't want to pull in
Spring Security because then that just starts making a whole bunch of things a little bit more difficult uh in terms of
hand yeah I was so here I am thinking about um attack modes of people who are allow uh if I allow you to supply your own
name I am opening myself up for uh not safe for work names let's put it that so so my pseudo login pseudo um so my
pseudo login is uh pick which person you are so I'll generate a bunch of yeah I'll generate a bunch of windy Dolphins
mean sure that's probably easier than IDs are game or not or I could go with uh okay so you pick who you are as a person
um you can then choose to create game as a host or to join a game uh if you want a crate game then say crate game uh and
then game no I don't want yet a drop down for for available games the reason why is is there's a lot of uh that requires
me then to identify sort of um teams and and things like yet um so you pick who you are you create a game then you
probably join the game you just created somebody else comes in to join that game as well uh I probably need to limit how
uh so that'll probably be the next thing is think think I want to limit it to four for now so one of the things I'm
trying to figure out is and sorry this is no longer dark mode but dark Mode's over anyway uh I'm not sure on on the
screen can I fit six players because one of the things you you you kind of need to be able to see hands um the other
person's play area with their Tech neglect area um uh and I just don't know if I can fit six people on the screen
require ultra white screens you must have a, monitor in order to play this game no um to be honest I don't I try to
avoid more than four player games in person because it gets really slow um so I'm going to limit it to four I mean it'll
be easy enough to change from a domain standpoint um it'll be the UI that'll that'll be the the tricky part uh for now
it'll it there won't be much to display um yeah uh okay so once that happens once everybody's joined or at least once
the game is adapter technically it's also an outbound so actually I don't need the inbound just yet I do need the
outbound uh because what'll happen is is redirected that connects the web socket and now everything is handled over the
websocket um and the initial thing we'll uh etc etc uh so initially that'll that'll just be a lot of text uh and then um
it um then we can at least connect and and that uh it on one yes it it will um uh a duplex adapter um but I don't need
the inbound stuff yet so that's why I didn't I didn't add it once I add the inbound it will share the um the underlying
implementation the the adapter I like the I like duplex uh I duplex this duplex is fine um back to my modem days uh yeah
so once once I have the inbound then then the implementation will have to obviously share the the websocket connection
um but I'm trying to think of like what's the minimal I need to get it up and deployed um I don't have my I don't have a
Raspberry Pi yet I do uh uh I am going to place an order for one um but uh to get this deployed this is all I need to
get it to the point where all right the game started and we see the starting point we can't do anything but but we can
do that we can get that far um and then I can deploy uh new versions with um then being able to to to start playing the
start playing the game all right I think that's it that's all for today um my next stream will be will it be uh I might
be streaming tomorrow uh if not tomorrow always uh oh thank you commit and push I will commit and push thank you for the
reminder Comm and push commit and pushed um so as always uh the Discord is the best place to find out when I'm going to
stream next uh I give it a 5050 shot whether I'll stream tomorrow actually probably even less than that uh Fridays is is
much more likely um though it'll be slightly later start than today uh Jonas you made the whole thing all right um yeah
so uh thanks for joining uh and thanks jaag grun for for your for your bits appreciate that and thanks for not sure if I
should say thanks for all the dark mode um but thanks for uh participating and uh making suggestions as always it it's
what makes it it fun for me um I really do do appreciate uh I appreciate you all um so that's it uh I will see you next
time have a good uh afternoon evening uh or night um for those of you on UTC plus you should be asleep by now or close
to it uh and I will see you
