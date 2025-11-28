# JitterTed's TDD Game： Online - Ep# 6： ＂Game Joiner＂ (Java, Spring, Hexagonal, DDD)

**Video URL:** https://www.youtube.com/watch?v=8n51vEiCX6Q

---

## Transcript

all right hello folks welcome to another episode of Jitter Tad's tdd game putting it online and so that's what we're
doing uh so for those of you who haven't seen earlier episodes um the tdd game is currently a physical board game um Let
me show that to you so this is what it looks like um basically has the hex tiles is the is the board got various kinds
of cards action cards here test result cards here that's part of the game um and uh some cards to track how you're doing
uh and so my goal is to get this game online since not everybody is always in the same physical place and so the current
mockup looks like this hey there Vicks welcome um look something like this uh this will likely not be the final layout
um it's got almost everything that that I need from the game in a size that is fairly reasonable uh so this is uh a
figma mockup um and I basically set it sort of fit in a in a 1280 x 720 screen so that way if you've got you know a
13-inch laptop you can still uh play the game without having to uh zoom in on everything so but we're still a ways off
of getting something like this on the screen my my initial sort of immediate goal is to um even if it's just text based
to get something that is playable by multiple people who are not in the same physical location uh mainly uh because I'd
like to use it I don't know if it'll be ready when I need it uh I'm actually doing uh a playthrough of the game for for
some folks and it would be nice to have this I probably will not have this um certainly not looking like this but
something minimal that's my that's my goal uh so VI says interested in refactoring some Enterprise apps in tdd what are
some books um I would I would say uh so there a book by Alan Miller about basically tdd and and a bit of hexagonal
architecture uh and I think there's a development with Java um but it's actually uh it's got some stuff in there um not
just about tdd but also design and hexagonal architecture uh and and things like that so um here is the link hey Jonas
and I forgot there's a bug in not OBS it turns out uh or I can't paste into OBS um I also have a course on on the topic
um nowhere near as as as uh inexpensive as the book um but you can check that out uh I will be reopening sales for that
I had hoped to to do that last month um but it's looking like I've got something else that that came in uh so I'll
probably not reopen until next month but you can sign up for the mailing list if if you're not already on there and I'll
let you know when it's ready yeah time flies I do I should update that though it's not at least not lie anymore um right
uh so um let's get into the to the code uh so one thing I figured out um I was having some problems with login it was
was really weird and I was very confused why it was happening it turned out that uh and I'm going to blame AI uh the
llms for this when it had created this line for dispatcher type matchers so one of the purposes of this line of code um
I'm totally blaming Cody actually I'm not sure if Cody did this or one of the other but um I'm going to blame chat GPT
since that's I believe what they're using underneath uh they added one too many entries here so the idea of this is look
if you're going to show an error page don't worry about security if you're going to process a forward don't worry about
security like those shouldn't be secure I need to see those um what it had actually added was requests which is
basically every sing thing that happens and so the request would basically be ignored except when I actually hit the
endpoint um and it would just be permit all right because that's what what what it says permit all and then the
principal would be null uh and so it's like why is the principal null and so I'd log out and log back in and it would
work fine so the problem is that it wasn't basically I it had essentially turned off security for all requests ASD so
anyway that's fixed um and now it works a lot more the way I would expect where where uh stuff stuff gets logged in yeah
so for the dispatcher type matchers you can do sort of um uh string based regex or ant matcher MVC matcher like things
to say error and so on but um from what I understand these are better because these don't rely on specific strings but
are uh more about what kind of proc what kind of request am I processing so anyway so that's that's uh so we don't want
dispatcher type I have no idea what that is it's packed I don't know what they're doing generally I have a very low
opinion of packed books because for the most part they just find an author who can churn out stuff and then publish it
with not a lot of sort of production editing and and Technical editing uh I've seen some really bad books uh and when I
see really bad books um a lot of times they're coming from from P so PCT in my head has a has a pretty poor reputation
this book though I know the author uh and I've looked at the book and so um so the book I I link to I I I can kind of
recommend uh but I have no idea what whatever whatever this thing is yeah is so I was here okay it's Cody's brother by
Cody's more like Cody's okay yeah who's this Al person why they uh okay so we can close this we're done with that um
let's run our tests I don't are I've had meetings all morning and then uh I'm like well I do want I still want to start
as early as I can so I'm just going to Dive Right In um oh right so this performance thing is actually uh is new so I'm
actually on the um 20242 EAP uh cuz I like to live on the edge um and so they added this uh which probably is not what
you want for for tests but um might be useful for for other things so uh but how do I close it I don't want performance
how do I turn you off that's interesting um I must have to look at somewhere physical books yeah I don't know I I I used
to buy a lot of physical books and wouldn't read them so uh yes it's easier to to ignore ebooks um but I'm just as good
ignoring both physical and and ebooks all right so this test is failing uh oh cuz we don't have an endpoint so what's
going on here um because this is null yes uh so let's go fix that because uh we currently now have in lobby um it uses
this player Joins game to do its job so let's go um mock that out the tool that's hilarious it's suggesting song service
which is from a totally different project you may know what that that is uh so what we want here is we game okay uh so
that should that should fix that hey DAV yes it's Cody null uh I probably need to not use mock Bean probably need to
have a test configuration all right let's do the right the right thing let's create a test configuration so you already
have it as an ebook good thing you game oh that's CU it's not injected well that'll do it so all right let's not uh
let's do then the minimal possible um let's go ahead and and add that as a Constructor parameter uh uh yes um this is a
new SE dialogue sequence I haven't seen this one before um and I'm curious if it reset one of my continue so that's all
fine um and yes now player join game is not going to be happy so let's make that game there we go I don't know why Cody'
s ask adding a new line uh and because I I like my autowired annotations even all right um I need to check some settings
because I feel like uh something might have gotten reset so what am I looking for I'm looking dialogue did they take it
oh they better not have taken it away refactoring Ires so many freaking settings this is a problem with like tools like
they they just grow it's key map code editing oh no okay that's weird so I looked for modal and it didn't show it didn't
show this okay so that's still there um that's fine uh pre select CS I think I want uh okay that's interesting so the
reason why I was checking that is because I was surprised when I told it to add this parameter uh and it went through
what's basically the change signature refactoring that it dialogue so um but yeah it couldn't find it couldn't okay uh
let's see all test pass let's do a command it's funny I I I don't read I don't read eBooks on my computer I pretty much
read them on on my iPad um except for the book club then then I read read them on my computer uh but I have a Mac so I
can't help you with the windows so I've used caliber on on the Mac I haven't used it as a reader I've used it as a
converter let's see uh so uh player Joins game uh we were going to split this weren't we all right well let's let's uh
push rejected oh right uh let's merge I updated the read me online and I that all right so we should be good yes that's
all set okay great uh right cuz joining only requires this it does not require the game creator uh and it does not
require the the game store that we had created last time um so yeah I think we should we should move um I'm going to
make this static even though it's broken let see if it'll let me move it anyway what I want to move it to is not lobby
but something next to thing Joiner um game no they're this is when they're actually sitting down to to to play the game
um so SE I saw uh something on on Twitter flash by that I saved to read later uh about naming things like this as noun
adjective um this is more noun verb game starter the game might have already start is a tricky word the M the game might
have already been created ated um this will not start the game though uh so the sort of order of operations is game's
created people join and then the game starts so I'm just going to say game Joiner until I come up better and we'll move
that there and we'll create it um I don't care refactor anyway and then uh uh you didn't open up the target um and then
let's um but this is going to be not lobby but game Joiner and we need the mock MBC which I'll just let Cody do for me
uh that inject uh so we're going to delete this oops so it removes the field but it doesn't uh update this uh so we'll
save delete that and then we'll go to our game obvious uh and gosh I haven't been to anything where I guess it's an I
guess it's an usher but yeah they don't they don't do that they don't do that in movies anymore they do that in in um
for some concerts uh vicus have I ever used Vim I and I certainly appreciate it as an as an editor I also appreciate the
the quick man maneuverability of the keystrokes but my fingers are too tied to uh intell uh let's initializing
Constructor or add Constructor no I want to add a Constructor parameter then we'll autowire oh right because this needs
to be a complaining uh and why is this now red all right all that was basically split class along dependency lines um so
everything should still now work because except oh when I made the method static uh uh that got updated so we want that
variable quite uh we probably want to do a create Joiner um right and this test now has to move this uh actually let's
go here we'll create a new test which is that and then we'll basically grab that and move it over to here okay and we'll
flip that over and game Joiner got put in the wrong place no oh it's green it's not background good yeah no it wouldn't
be Pit Boss um yeah if you walk into a casino and sit down at a game I don't think there's anybody I mean I don't think
there's anybody who leads you to a table except maybe I don't know we'll we'll keep it as this um hey there Magic 79
want to see the game I'd like to see the game too um we're still bu we're still building it this is the mockup so this
is something what like what it'll eventually look like um but we're quite a bit ways from that all right so everything
still passes after uh okay so what we want from join uh the purpose of join and why are you not format it right there we
go uh the purpose of join is to join an existing game so what takes is basically who you are um and the game handle
which is a human readable unique identifier um which is generated when we create the game uh so this sort of SE the
highle sequence did I create a a state machine for a game I know I have it at the the the player for basically for for
sort of the playing playing the game but I don't have a state machine for game um as sort of the aggregate uh that's
let's do that because I think that'll um make it clear in my head what's what's going on so that's the board State
machine uh what we'll do is we'll create a machine so start uml o Cody's also completing here that's going to be
interesting to see what um what it does here see now Cody's just cheating because here so um the basically the nothing
step to the game uh all right I can't do that I have to do this thing uh and also let's not do that uh State uh bny asks
do I usually prefer using at controller uh at controller at service or explicitly beaning up the adapter um so I think
if what you're asking is uh so here this has to be a controller um there's kind of no way to to avoid that CU this this
class not only is a bean but it's a special kind of bean where it's going to look for post mapping and and things like
that so I'm not sure if that's what you're asking though the only thing that um I use at Bean for is for things inside
the hexagon that need to be injected into uh that need to be passed to the to the adapters um but these this is in and
in the adapter so I totally let spring do its work um but then in the uh tdd config I provide these things which are uh
inside inside the hexagon I mean these are all classes let me know if that didn't pass and they do um we didn't really
do much we just created Boy Cody is just not going to be helpful in this in this uml state machine I can tell uh where
we want to go to is joins uh player joined oh well that was helpful Cody um except what it goes back to is actually uh
not player join but actually uh cuz we don't leave game created uh until the game is started started do I need a
separate state for game in progress versus game started I'm going to call it game in progress and we'll see how that
works and how you get there is yes host starts game thank you um what are you complaining this is a really interesting
message because it says syntax error question mark is like it's not sure if this is a syntax error what that was weird
that was and and I've seen intellig do this recently where where there's like a uh until you like move the cursor it's
like it's not reprocessing uh the data um I'm not going to I'm not Fally bug for that because I have no idea how to
recreate that those are probably the most frustrating bugs of all because it's like R happens randomly or pseudo
randomly heye welcome so um let's create another state State that's helpful thank you um so the question is is who
starts a game can anybody start the game can only I think anyone should be able to start the game because the host might
not even join the game they might have just created it so I think it's going to be player starts game and this this is
so this what we're doing here is is this is really important like I I am I am very much in favor of doing planning
especially when it involves State machines doesn't Define the code that we're specific code that we're going to write
but it helps us think about like who can start when can they start things like that can someone join late no I don't
think I want to support that um at least not for my uh first first first release uh so one of the advantages of State
machine is it tells you what what you can or cannot cannot do so the only thing so player joins can only happen uh when
the game is C been created but not yet started so once it's started then the only thing you can do is is so player
starts game um and then I into basically the it the other state machine because that's uh Joins turn no it's it's this
is the state machine for everything a player can do so it's started um so this is sort of the entry yeah I forgot how
you do an I'm just going to leave it as this because this is this is because I'm trying to figure out what are the what
game um yeah so the other the board State machine is is per player um or per per player right now as I've mentioned
before the definition of a player is a is as it's really Pawn uh but I'm not going yet because you because because the
variation is you're mobbing and there's only one pawn and every so there multiple players controlling one Pawn so uh but
I'm not uh you know that's one of those where it's like I I I know I will Pro I know I will need it I don't know if it's
worth the complexity to introduce that early um feels like it's going to that that would slow me down to introduce that
level of interaction how do I want to do that so when the game is over you don't want it to go to some other screen you
might want to stay there for a bit um but then you're probably going to okay something like that that's good all right
uh okay so this test is disabled because we need to have join on the player Joins work there should be nothing needed to
support hey let's put the game on hold and we'll come back to it later um because a player if they join and they were
already part of the game they will just go into the game screen and so if everybody does that uh then the game will pick
right the game is persisted so it will pick up from where it left off um I mean really endgame doesn't do anything other
than put it in in a state I don't I'm I'm not sure what what were you thinking of the the that were the two different
types because an in progress game is an in progress game whether like we disconnected and left it for a month and then
came back um it'll pick up right where it left off um oh I see one that's created and yet to start that's possible um so
sort of a a bit of of of possible and so you basically say uh uh created that that's since I'm using event sourcing it's
it feels like that's going to make it more complicated um there might be some state state yeah I I'm I'm not sure so I'm
basically see all right so we're basically uh and I should have marked this as deprecated because we want to use not
this join but this join so let's go look at uh these tests so there we go um to to a game this is this is wrong this
would always be some kind of some kind of identifier uh of which game handles an identifier which we may want to not
have a string ID right uh this isn't being used yet is it it is uh that's wrong I'm going to fix you ID and this person
ID okay uh that anything yes did you write that before I said perhaps game handle should be not a string or did you
write that after I didn't I didn't see but yes as soon as I was looking at this like that probably shouldn't be a string
okay same time um I don't want to introduce it just yet uh but it's GNA come pretty pretty quick oh good so we're just
going to have to replace um so this one was just me figuring out what I wanted it to look like from here um but when I
got to when I got to this point I realized that it wasn't this one uh so I'm going to be test driving this I'm basically
right now test driving in a sense doing a refactor of pointing this to this so I'm going to translate all these tests to
to to point at this because when I got here and I was trying to connect it to to the game I didn't have a game here and
that's what so this so if I can't so if this is a command and I say join uh what is the impact on the system I should be
able to ask the joined yeah and that's going to lead me uh I may not be able to deprecate this just yet I mean I may not
be able to be this and then game handle and person. ID uh this will not yeah I think this will this will this will be
now test driving new Behavior um so this will this will fail because there's no connection clearly there's no possible
connection uh between a gay game handle and an actual game because this has no references to game uh so that fails as so
let's so in game creator we've created a new a game why you want the wrong side um which does save it in the game store
so that means if we inject the uh private final oh you're right it is game parameter and now here we should be able um
oh look we don't have a fine game by handle which Cody is saying that that you should that I should use um looks like
we'll have to write want uh although I want to call it just fine by handle so we're going to disable this test um and
all of those Constructors don't that let's create uh an empty Constructor um but what we'll do is we'll basically say uh
think we can do that and then I'd method and then I can basically grab this put it in here and then get Constructor so
that should work other exist excellent all right uh I need to take a quick stretch Break um and when we come store go to
the lobby of the game store no just kidding um and then test drive uh the the fine by handle oh is the background music
stuff I'll skip it all right I'll be right back enjoy back uh so magic S I have the feeling to understand the project
understanding yeah I mean as Astra says like if if you got if you're watching this and you got questions you're not
interrupting me more than happy questions uh okay so let's go to our game store test do we I guess we did it indirectly
um with the game creator so so I find it interesting um that Cody was willing to write the first part of the test and
not like the whole test that's just interesting not at all helpful um uh as no it is not possible to sort of donate uh
the passing test points to to at least as far as I know um yeah as far as I know there's there's that doesn't mean you
can't like redeem store I wonder if Cody is sort of interfering with intell's ability to update itself wonder if that's
what's going on game um yes that's what we want uh and that will be equal to game so create the method certainly not
Boolean I don't game I don't think I have a unique identifier uh Eagles is probably not work yeah it's basically like
did you find it that's all I need to know um so this will certainly fail cuz returning null uh but we're going to need
some string uh do I want I don't think I want the events in a two string that would be not map maybe uh so that should
give output yep oh thanks thanks that's interesting that uh it thinks this is somehow a generated file and so it won't
load the diff I mean not that I care uh I just find that interesting thank you for that yeah that's my guess um and so
it is a generated file but it's curious I guess that makes sense uh okay so now do I have to close and open the that hey
where'd it go why is it all the here excellent thank you for that swegi uh what plugin are you trying to update oh I'll
update you uh we don't need person ID open we don't view yeah so this color scheme is is basically what I use in all my
hexagonal architecture diagrams um so uh yeah and I have a a video up on YouTube to show that's weird that's not that's
these are not the files I had open when I closed it all right um so we got game here uh but what we want is no not that
um where is game store is uh okay so this fails fails for the reason uh yeah those those files you can you can totally
copy um can also get them out of Embler yeah um so I'm probably going to need an equals which means I'm probably going
to identifier uh do I want the identifier I probably want the identifier at the event sourced uh oh that's weird I seem
to have uh intellig seems to have gotten confused configurations there is a bug somewhere in intellig and I've run into
this before where it somehow gets confused about the Run configurations and doesn't load them um no because they're
stored they're stored in in a known location with a known file name uh there shouldn't have directory uh I bet if I
close the work this what is what does validate oh validate intellig because I'm nothing without my oh why is Cody
unhappy oh now Cody's happy no Cody's unhappy Cody and counter an unexpected Cody oh I got I got a g all right I'm not
going to do that now I have to re uh exiting and restarting right turn off and on um all right so uh I am unhappy though
about it kicking out my my my presentation assistant I thought I did it for 2024 dostar but I may not have oh no worries
to totally not your fault 3G um well I'll do this for Fork how you doing Cody all right Cody looks good so let's tests
uh right we were so we were looking at adding an identifier for aggregate um boy I hate the new presentation assistant
maybe Hate's too strong I I dislike it so do we want to put an identifier uh do oops Yeah so we as part of the
Constructor and eventually I probably will need this last event ID as well um creating uh I mean I I could cheat and I
could say if the game handles are equal that's identifier so um I'm going to do that I'm going to cheat and when I get
to P to actually persisting stuff that's that's when I'll need identifiers uh or at some point I will need an an a non-h
handle identifier and then I'll I'll use that so we're going to create an equals and hash code um it's interesting that
there's no easy way without the keyboard to say no no this uh yes null because you cannot create it without a handle
okay so that'll that'll work um this will still fail because we're returning null H but now we can go here and we can I
think I'm just going to do a uh a prepare refactoring let's do that uh so we want games not to be an array list we would
like it to be here I am looking for a refractor can you change this to a map I don't think it's going to do that for me
uh so what we want is a final um uh map game um and that's our game map and that's a map and then find all if we return
games dot uh uh game map. collection so we'll do that that's kind of map that uh and yes we are probably going to want
an optional on on and then I can get rid of this uh so I should have not broken anything else and this current test
should y uh so now let's write yeah probably put the um the in the create method it would it would do a uh constraint
check there empty which won't currently work so this can I migrate this to an optional present uh and then in fact I
don't need the is present because it says in it's it's an abstract object optional uh I wonder if it doesn't know let's
see yeah that works I think it just doesn't know the type because of this weird thing so I if I wanted to I could put in
uh uh what is it instance of assert Factory um what is it uh in sub assert class I still don't understand why it thinks
that's an optional this is most certainly an object assert on confused uh I mean yeah I could say yeah uh the question
is what is the failure going to look like um so let's look at the failure mode uh okay that's reasonable expecting the
optional to contain what I was looking for but was empty fine uh I mean if I really wanted I could say is present as
better yeah I think it's actually what is what is that error MERS look like I always think of optional though collection
I wonder if internally it delegates one of these delegates to the other yes so has value just delegates the container um
so I'm going to keep it as contains that's funny yes all right so let's return this to reconstitution um we do not
though have a we are not currently at our game stor yet yeah yeah uh we'll we'll get there but not not for a long all
right ASD hope your hope your bad all right so this test will fail uh sorry this test passes now optional okay uh what
else do we need what did we need from need uh we don't need that we don't need handle and we can VAR that right now I'm
going to uh say or else row so that gets us our game to join then we do the save technically the test isn't asking me to
do the save um but I'm just going to do it anyway in test but this not probably because create new game did not save is
my guess no it here oh because it doesn't it's not so I'm just I'm just thinking about all right so let's actually and
game creator okay so then we should be actually calling the constructors on these go all right so that works uh I don't
think I need this cuz I get that assertion um says first ID game handle uh and we're going to need to do the same thing
that we did here what I think we can assert instead is uh players um map them to the person ID contains exactly that and
then I don't know what Cody is doing in terms of adding curly like yeah that's not what I cuz I don't actually need the
person I okay pass because this now refactoring because I'm I'm ret I'm targeting the new uh join method which is this
one and this is the third time we're this uhoh error error error uh so this is a fixture are you not going to finish the
refactoring now wow that was interesting that took forever uh so yes clearly there is some somewhere whoops extract okay
I think I'm going to restart and open up nonap because this dead won't even let me report interesting buug oh is it
literally uh reporting a those I I I reached my quota for the next two three months I'm counting that as one one bug
report and that's not really a bug report that's that's a self-monitoring edge too bad I don't get paid by the by I'm
actually a little surprised that that the limit for the bugs that it's sort of self-tracking is all right uh tests that
All Passes uh so we're basically removing use usages of this method so let's go here right so we had just created the
fixture so we want to do that again fixture looks like this will need to use the fixture as well may as well replace
that one while we're at it uh and it looks like it didn't replace any of the other bummer well that was the so to be
fair what I was using was the the not even beta not even release candidate Early Access version of intellig um in
general intellig is is is super stable um and I'm sorry if you're a Java developer and using a clipse I'm sorry I think
if you try intell you will you will be and get used to it I think you'll be happier uh so let's fix this um so Dot and
then we can dot oh gosh yes yeah I I I Eclipse I know of a a project where their framework is based on basically osgi
and there's some the clip stuff and mess uh 44. found uh what's the purpose of fixture so the purpose of fixture is
because Java cannot return multiple values from a method um and so I'm creating the same setup every time which is
basically create a game store pass that game store or into this player joints game and then create the game and save it
uh or create the game VI that game creator which uses the game store um and so if I extract the method since I'm using
multiple values that are being created here um intell is actually smart enough to do basically a two-step refactoring
create a record to hold the two values that I need uh and then create the method that then creates that record so then
in my tests um I basically just create the fixture and now I can reference the game uh and reference the basically the
target object so that's that and then we'll do place that with fixture um normally when it works correctly it will find
duplicates and then refactor the other ones to look like it but because it crashed uh it didn't do that it does make the
um it doesn't it makes the readability of the test a little bit a little bit worse trade-off uh so let's let's fix these
now one by one uh this one we don't need person we just need person uh so in this case my assertion is not this um but
basically that the players has size of okay uh so sui says I may not need the um well the game creator is the
application Level which is doing the assigning of the handle and saving of the game so I kind of am okay with that
because otherwise I have to man sort of manually create a game and then manually pass in a handle when I don't really
right this is technically more is not added as new I think that's it so I think join is no longer used oh it's used here
uh let's fix that uh oh look we don't need this this map we can just do person ID and then this a player Joins game and
then this is person ID uh and this is game handle uh what's going on Longs there we go all right join us have a have a
good hello oh right cuz I'm not using the fixture uh see do feels like at some point I want to have a game Factory or
Builder instead of going through the application every time possibly I mean right now layer it's a little bit of work
eventually that that'll get harder and that all right so all our tests are now passing uh this method is no longer being
called right um and so now we can delete uh what did we not set up properly here we probably didn't set up um join
because game handle this game handle doesn't exist uh so now we'll need some that magic that's not something I ever
worry about um no no manager that work for would come and say show me what it looks like when they know that I'm doing
development because I would have proven myself time and time again that I release stuff that works almost always the
first time when you look at it uh let's fix this so the problem here is that um we're sending in this parameter this
handle does not exist sorry do I have these reversed uh no game handle this is the game handle um this does not exist
and so therefore it's failing to find it uh let's go and uh we're importing this game config uh we probably want to make
a copy of here and then we'll call it test config not turst um actually I'm not sure that's necessary and yeah I mean
all the tests are passing there isn't much to show because the um there's not much in the UI um but we could certainly
show it and yeah they wouldn't and it's true we would be I'm using CI so they'd be able to go look for themselves uh and
I just realized I didn't need to do this so let's go undo this because I don't want to mock it I actually just want to
autowire it creator uh because in the config it will use a game store that is shared oh it's not take store and we'll go
ahead and have that injected yeah so I'm I'm honestly you know still getting used to using nullies um I'm also not quite
sure if I'm using them 100% correctly uh but absolutely I do not want create null um used from from production code and
since I've learned how to do that rule um yeah I think what what I'm wondering about is do I want these create methods
or do I want production to only use the finding I am finding uh and I found this when I was when I was pairing with
James as well uh that I was getting confused null I really feel like Crate N should test so then I can call instead of
nullable testes um I know James was was not like 100% happy with with null being in the name so uh all to um let's
actually add that as an issue so one thing I I I found is that um uh not here what I want is where's my jira know uh oh
maybe that's that that makes sense in JavaScript it's probably um it probably makes more sense because any
non-dependency injection environment maybe that distinction makes sense uh thanks that that like confirmed my feeling
that using the Constructor is do since as spring boot a lot of times okay uh I'm going to take another quick break uh
and when we come back what we'll do uh oh is we'll check to see that this fixed uh because right now this is broken we'
ll fix this one up uh once that's done I probably want to pop back out I think I have a disabled test so we'll take a
look at that as as well so uh I will be back shortly all right we're back um I caught myself like staring at the the
coffee video for for a minute and coding um yeah I think there's uh like even though I pair with with James on on on the
nullies I don't consider myself an expert either um I think I need to adapt it to how I'm and I need to probably sit and
think about it for a bit um but anyway what we wanted to do here was we wanted to say uh really it's strange that that
like Cody chose create game as opposed to create new game when the code literally says create new game I wonder how much
context it's providing uh cuz that's a that's a game and then this we can say game. handle see like handle's right there
there is no yeah the configured responses is really where where things um become really yeah uh all right that worked
let's go commit um yeah I I mean I agree that create new might seem redundant somehow it feels more explicit um and if
Cody were just randomly saying you know uh game creator and I'm going to return a game I could totally see it saying
create game but like the codes there in game creator with a method called create new game that returns a game and so I'm
just like does it not have enough context is it not using this context to decide what to propose and clearly the answer
is no it's not um so that'll be that'll be some more feedback I'll I'll provide to to the source craft all right so all
the tests pass let's go test um this one is uh is a separate thing let's go to this one um this is now Avail so this is
nice and I don't know maybe I I might write my own annotation um actually I had been looking into this I totally forgot
I was looking into this where you would be able to disable a test until another test passes and you'd specify what that
test was uh and last time I looked at it it was like oh that's not as straightforward as it seems because there's no
standard order to how tests are run um they're sort of pseudo randomized uh so it is possible to write a junit extension
that would say disable this test until this other test passes uh so it's possible to do that but it's not as
straightforward as as as I had hoped there are conditionals in junit and there's the junit Pioneer Library that extends
some stuff but none of those do do what I want which is disable this until this other test passes and then run it
because then it will will either pass or fail and and I'll know about it but um since this now exists we can go ahead
and and delete that and this will not work because um because the game that's created is not in the store uh but let's
run it sure oh better error message for like I probably what no value present is not obvious um I mean this yeah this
this was temporary eight anyway so um do I want to throw an exception or do I want to return a failure result yet but I
think at least for now a better error message would be nice let's full oh these are lambdas so it's a little Annoying
that all these arrows uh all these uh uh expandable tree nodes look the same but they are of a different nature this one
is a record these just are lambdas and like if they're just Lambda them um and I guess I could uncheck this and that
does configurable is this configurable like on a because what I'd like is is for test classes don't show me the lambdas
I don't know if I ever use it anyway let's leave it like that all right anyway I was looking through the test because I
wanted to see um if I need to start splitting them and into nested uh since I'm about to write a so let's see so what do
we want to do here we just I think there's an illegal argument want I like how it chose 42 that's that was that was a
nice uh that's probably the message we want um throws no such element exception is that what it throws we'll get that
instead of the illegal argument yep no such element uh that's interesting um oh that's the that's the test that that
kicked off the fact that all right I'm like why is that test failing now we just have a better a slightly better error
message although not yet uh and now let's actually get the message so this will fail because we're message along with
the other think that should pass yep and now we get the nicer error message for here that uh and now we can go to the
failing test and hey look at that it's don't blame me 9999 bringing a bringing a party over welcome folks doing some
development trying to bring this game which is currently this physical game trying to game uh to the world of most
people are remote so they can't play this game when it's physical or at least not as easily and so trying to bring it to
this um but still early days yet this is only like the six episode of me sixth stream of me working on this but welcome
thanks for bringing over so uh this fails because we are creating the game outside the context of uh the game here so
right so uh we want a couple of things to happen uh when you join a game we We join the game which we'll have to fix uh
we'll also have to deal with the redirect where do we want to redirect them to to so in our when uh so the game's been
created you join the go uh because you're because you're no longer in the lobby right because you Jo you've joined a
game so now you're in the uh as asterid suggested are you now in the foyer are you now in the hallway um or basically
oops not that are you basically here and then waiting you're just waiting for these folks to to fill in because you
might it's a it's a single it's a single floor um I actually think it makes sense to to you're here uh and you're just
waiting and you're just waiting for the other players and so something like uh you uh something like that in some I
think I think that's that's what I'll do so the so things like shuffling the deck dealing the cards uh right so the
cards would not have been dealt whether I shuffle the cards now or when this when you click the start game button I
don't think matters um so these will all be empty anyway uh and I'll probably just highlight them different when it's
when it's waiting for for a player to join the game so then we are redirecting you to uh which is what we said here um
no so game created uh so this is the game state but what you see is you see the game when it's not yet in progress uh
and you have to start it yeah that's fine so the Crea game is where where we're at to that and that's the page that will
be have all the HTM X goodness and websocket connections and things like that um boy I really as tempting as it is to
say like oh shouldn't we have a chat area uh I am trying to not do that again sort of my assumption is if you are
playing this game you're using some other mechanism such as Zoom uh or Discord or slack huddle or whatever uh to
communicate verbally um and see webcams and stuff like that uh if I ever make money off this thing then I would
certainly look to integrate that but that's sort of a solve problem so I'm not going to do that uh okay so this is
failing because this does not exist in the game store um so here's where the I think the NBL this is the right thing to
do is basically just say and treat this game as already existing uh because in a sense this is a pre-configured guess so
let's create another method that takes a game um and I guess we pass that down wonder if this is how I should have done
it before no I think I needed access to multiple things uh null just does new game store but it's H so let's see so what
are we testing here we are testing that the game Joiner talks to the rest of the system uh so if that's true then what
we're saying is we game uh so I guess that is the one that has game that makes sense here we go so I have to admit as
much as I like the names like game Joiner as the controller I I actually am finding it a little confusing um that it
doesn't have the word controller in it so it's nice and meaningful but I do feel like I am uh I am not able to like that
what's basically secondary notation um that we talked about in in our book club uh the color help a little bit um but I
wonder if if if I've sort of gone too far so uh game loader no it's not a game loader it is a game Joiner um it is the
controller for that adapts between the outside world and allows players to join game so so the name is correct it's just
not uh what's missing is is an is some kind of secondary indicator that uh it has a role of being the controller or
being the adapter all right well I'm going to let that stew in in the back of my head uh in the me time what I'd like is
to method um create a game store save the so now um this is not a valid uh player ID uh I don't think I can assert on
the um and of course I can't because I'm like how would I even know what that is uh it's because I don't have any
relationship now so what I'm missing now is a person store um so there has to be a way to translate the principal uh and
actually I think I can get I think I'm going to need more details than um because I am going to need their their
identifier uh so I'm going to need uh I'll have to look I'll probably need a custom custom authentication fine uh but
for now this is this is he all right so somewhere I am not uh so ah yeah these are two different IDs uh so what do I
expect um this is not the ID I want because I actually have no idea what the player ID is going to be so we're getting
players but we we swegi so let me do something uh I feel like something was not as obvious as it no I just think it's
it's at something other than than person user having something that doesn't start with a P I think that's this is not
the that well nothing's coming to mind other than user and I really dislike that that term but I may have to use it no
pun intended for count um account is as bad as user but maybe be I mean of account or user I think user is probably
better because it individual uh yeah problem with individuals is is it is more it is more it is less like player ID um
but it's actually just too many too many syllables I'd like to keep it to to to syllables so member is another
possibility I use that in ensembl um or user what else you got Cody no we've got just yeah uh all right that's going to
be a so now that we've clarified thanks to sui's help um what we are trying to determine is is the player joined of
course we don't know anything about this this principle um because that's too generic uh what we really want is an
object so yeah so probably um user details I'd create an implementation of that um so user is a reference implementation
that I could use the question will come when I oo authentication where do I correlate the username with this ID well I
guess I'll I think I can worry about that later I think i' I'd need my custom oops I think I'd need my custom uh
implementation uh let me make the rest of the test pass and then we'll worry about that so this is currently failing yet
oh right I didn't refix it uh so this should be uh person ID ah uh no it's still player that I'm extracting from but
it's person ID that I'm okay so that should now pass we should get the redirect being wrong all right and I can fix that
and that so that's so we basically uh had gone outside in everything works all the way to the to the game store to the
persistence um so I believe we our template and we can actually so we can uh host a new game that works uh and I think
now we can actually join a game and that will redirect to a page that doesn't yet an endpoint that exist progress that
endpoint needs to indicate which game you're you've just joined um so it won't be a won't be a straightforward or
redirect uh I'll need to have some identifier for the game so so uh because of course we're going to have multiple games
going on at the same time uh but for now this should I think in now that works uh no games currently available to join
host a new game so we'll give it a name host game uh now we got Chile Swan 97 is a game we can join so go ahead and do
that and as expected we are redirected to game in progress so um that's exact exactly what we expected so hey now if my
manager says hey how how's it looking we can say look you can you can host a game and you can join it you can't see the
game there's nothing in the game but we've got the lobby at least the most basic feature is done um and look player cat
has won and if I it player can is still won out and I log back user um oh the player ID is hard the person ID is
hardcoded so of course it's always I'm just rejoining the same game I forgot yes no static resers game in progress um
because there's no end point for that which is okay next um this is now game store uh does not use the Event Source yet
um I am doing that so I'm going to check that off so let's see so post mapping that does creates player in the game for
the person that happens underneath uh redirects to the to the page that shows done uh and therefore well for the most
part uh there is still the whole idea of multiple players so the next thing I could do is actually start the game but I
think before that four uh well Cody you're close it's not host starts game it's uh waiting for a um it it's funny it's
it there like do I want the host to invite specific people and then the game the game is ready to start when those
specific people have joined I mean that's certainly a future feature but I'm not going to worry about that now so what
do we want when we're waiting for the game to start is um so the game was created one person I think you can only start
the game at so I think what I want is when you're here and you're waiting for other players to join uh I think I want
kind of of kind of a modal dialogue or at least a modal thing um not quite sure what I want that to so this is waiting
for game to start uh let's fix this font because this font is pretty terrible for something like that to to to notify
you um uh let's do this and then there'll be some kind of button oops come on there we go uh where' the is and this will
be I don't know um this will also this will be green good enough yeah there's no room in the game bad so something
something like this um and that's that's the uh game waiting to start um if I had more space I'd like put it to the
right or put it at the bottom or something but uh I think this is what I things and then when the game starts then you
get the the rest of the stuff annoying uh unless there's a way to tell complete so this is a text file where would text
files be plain text yeah so the icon doesn't do anything uh there's nothing here I don't understand that well there's no
there's no way to I mean as far as I know there's no way to to like I would have expected like disable Cody to be an
option here and it's not doesn't just nothing here so I don't know if if that's a bug or if that's uh I think it's a bug
or certainly a missing feature because I'd expect to be able to like uh disable the thing quickly which is what I'd
prefer because sometimes I just want to turn it off and then turn it back on rather than having to go into the plugin
settings and and disable it so that's definitely something I'll uh tell the source craft folks about um so I join the
game when we redirect to the uh game in progress page um so initially the modal will be the only thing that appears um
we'll show that uh and then um so that so that's our next sort of highle feature um that'll Force us to do things like
well now you need to have more than one person joining because the person ID is currently hardcoded uh and so that'll
Force us to uh with so whether that's a custom user object I'll have to I'll have to look at that I'll have to look
around and see will I need a person store so I think when they join then uh in I think when uh they join the player yeah
I'll probably want to store in I don't care about okay so some stuff I need to figure out for the security um I can
probably still fake it for now authentication um when I create a user rolls so that's using the standard user I'll thing
yeah so I'll probably start with uh and then I'll get the first name ID or do I look up in my local database maybe I
look up in my local database I have to know who they are locally anyway the oo is not going to tell me that it's just
going to really just going to use the ooth for authentic ation what's really authorization I'll keep locally the so then
I can get the name so I log in I have their username which by definition has to be uh uh unique can look that up in my
person store grab their first name grab their identifier hand that in to to um so I here I would get the user uh
actually principal is good enough because the name is is all I'm going to be looking at so principal is good enough from
principle I can get their name which is their username that I think once I have that then I can actually work then I can
go work on um the the modal which is ADD players join uh I'll be I'll be hooking up a HDMX uh and that's what I'll do
next time yep all right that's all for today so thanks so much uh for hanging out thanks to don't blame me 99 uh for the
raid appreciate it um and so uh stream schedule uh I'm going to be streaming just about every day this week um as always
if you want to know the most upto-date schedule join the Discord in the announcements Channel you'll see uh the at least
right now the 10th of the schedule um I believe I'm streaming tomorrow and then pair stream with Mike on Wednesday uh
but stay tuned uh to the announcements channel for that uh otherwise thanks for hanging out thanks for your help suige
uh thanks for all the the comments and questions I appreciate it and I will see you next time
