# Got My Refactoring Hat On - Experimenting with Automated Refactoring

**Video URL:** https://www.youtube.com/watch?v=5jt0gQD-S6g

---

## Transcript

all right hello folks welcome to a rare weekend stream uh it's morningish my time on Saturday um and I'm trying to do
some more streaming now that uh uh basically I have have more more time and energy to do so so welcome uh today I don't
have anything specific to get done other than uh playing around with some refactoring uh some other minor things um I
have this uh I have a few repositories that I call a playground uh where I basically just dump stuff into it uh stuff
that I see from Reddit occasionally or other things that I'm working on or somebody asks a question I need sort of a
simple project to play around with um so I've got some stuff in there that I'm going to be doing um so one of the things
let me switch to and may not be able to see it because of the way this this hat is uh but it's it's my refactor hat so
I've um so uh this code here was posted on Reddit and I thought it was interesting because it's it's sort of what I what
I see from those who are sort of new to to programming is lots of redundancy lots of of repeated kind of code um and I
just thought it was it was just fascinating because somebody had asked about uh sort of you know hey why doesn't this
work and so on there we go I thought this was really interesting because like they created classes but the didn't quite
understand what the purpose of those classes are so for example um they create this world it's like okay great so
there's this world there's a player there's a dragon there's an orc right so it's basically sort of a a a roguelike kind
of thing with you know text-based and that kind of thing um but then they call World print map and then pass in like
details from from those objects and you may think like oh that's silly just pass in the objects yeah high quality code
transfers it's but you know this is it to me I am always fascinated like I am always so curious like what is your
thought process what what sort of mental structures are are you missing uh and for me is is just you know uh someone who
who wants to help people it's like what can I do to help you understand what what you actually need to do um and code
like this is is really great for uh for refactoring because I can I can take this and just refactor like there's no test
for for this um which is why there's there's some bugs in it uh and basically you just refract my way and and clean it
up um using straightforward refractions and this kind of stuff applies to any any code base um you know maybe the code
bases that that most of us work with are not this bad uh but you know we see similar you know maybe again sort of not
this bad of passing in you know these kinds of specifics especially passing in to the world its own information like
that okay that hopefully you don't see I mean this is this is hopefully not something you see in in any kind of real uh
code base although I I should never be surprised I you know so transfers you ask about like do they care about making
good quality code um for people who are learning I I don't I don't get too concerned about whether they care about
quality right because at that level they're just trying to get stuff to work and I think that um focusing almost too
early on quality can can make it really frustrating for people to learn um and and so I I want people to focus on look
get it to work here are some techniques that you can think about uh but then yes pretty quickly get to the point to
recognize that this just is not good this is there's no encapsulation here the names are fine right at least the the
their their names and there is an attempt at classes uh uh but clearly you know there's there's missing knowledge about
about how to how to um and so uh I've also been working on um doing a bunch of stuff with characterization tests
recently because uh in my refactoring taxological architecture course uh that's what we're sort of working on right now
is doing some characterization for the game before we uh basically start splitting out uh the i o from the non-i o
separation of concerns um anyway so so there's this uh which I'm gonna do some some practice on for for refactoring
because one of the things I always tell tell my students I tell people in in my coaching uh situations like you know you
have to set aside time to practice uh to learn how to use the tools that we have and we have awesome tools like IntelliJ
at our disposal you have to to practice and uh you also have to experiment and so there's practice which is let me do
something you know uh what sometimes called a Kata how do I refactor this let me try this way let me try this other way
uh always trying to to you know same starting point and then try and doubt different things trying out different
constraints can I do this only with automated refactorings can I change this code so there are no if statements at all
things like that um but then there's there's the experiment of like what what happens when I do this uh how can I do a
refactoring to do this this other thing so that's what I'm going to be spending time on today there's also some other
miscellaneous stuff oh I should turn off some of those are about uh nightbot is happily promoting stuff that is not a uh
relevant right now it's disabled okay uh so um so this other thing that happened it's kind of funny that that nightbot
mentioned James Shore because uh one of the things he has is a setup for his testing when he's doing tdd uh he's got a
back basically a process that's that's always running the tests and it it emits a sound when the test passes and when
the test fails and I was like I'd like to do that uh because I think it has some really interesting uh psychological
aspects but also like you can um you can just be work and if you set up a background process where it's always running
that um then you almost don't have to stop and explicitly run the tests for me it's one key stroke to run the tests
maybe two or three um but then you have to sort of wait and think about it whereas if it's sort of running all the time
uh then then you can just sort of stay in the flow a bit more so um so at first I started playing around with some sound
stuff using wav files and spent far too too much time listening to probably you know 200 different sounds but then I
realized like why am I doing that and then I have to worry about where the WAV file is so instead I basically uh did
some playing around with the midi support that that Java has did you know Java has built-in midi supports had it for for
many many many many years and uh so you can you can play notes so it has synthesizer stuff built in but it turned out
that actually the the midi midi stuff is is a bit easier to get it to play certain things so so I've got my um my synth
version of this so here uh you basically get a synthesizer get get the midi synthesizer it has a bunch of different
instruments about a I don't know it sounds like there's only about 80 different instruments even though there's 127. um
and then you can you can basically just play notes so this is using the the straight up just direct synthesizer uh and
then using uh sort of immediate immediate um so this one so it's kind of what you know the sound you're going for is
like the negative sound is the first one and then sort of the positive you know so negative you know sort of fail
failure sound and then the positive part of sort of sound it's just a little bit too quick so I can so let's change this
to 200 and then this to 400 . so the problem with with this technique hello J Walter the problem with this technique is
it's basically using sleep to define the length of the note because it doesn't note on uh and then it sleeps and then it
doesn't note off and that's really not a great way to get sort of like consistent uh playback and it's you know to me
it's such a it's such a small thing um but you know but but it seems like such a small thing but but it really doesn't
matter hey whiskey Sierra I see ya so instead um I basically landed on on the uh so I can actually do where is it the
The Sound Player yeah so this one um uses the sound effects so it's actually kind of nicer uh but again it's sort of a
little bit of a pain because I have to make sure that these wave files are available so the idea is I want to have this
uh packaged up in in a in a small Library um because one of the things you can do and this is uh is you can have sort of
a plug-in into junit where you can listen to things that happen so what you can do is you can listen and be notified
when the execution of of an entire test Suite happens um and so here uh if I so I have this plugged in so let me run
this test so right so I ran the test it passed and we got the passing sound uh and this test failed and so it played the
failure sound so what's happening is is we're basically plugged into the the test results the test execution listener
and basically just uh we find out if it passed or not and then um when the execution is finished we can then find out uh
we can then say basically if a pass then we play this sound if it failed and then it played uh transfer is really
interested in how you make this if fixed and not quite so anyway so this is this is like not a lot of code um but it
plugs nicely in and the way you configure this is um you create a meta INF resources uh and I'm blank account who had
the article about this I'll have to find it so I'm going to write up how this is done Oh Oh you mean in in the yeah I
mean there's a I'm not necessarily going to get rid of of all ifs that's not I don't you know that's not going to be my
my practice my practice is basically just gonna gonna um so this class then you basically say hey I want uh this class
to be used and loaded at for junit when it starts up um and then junit will call it as appropriate then I'm basically
just using my my Sound Player which right now uses uh these these sounds um and add a bunch of system operators because
like something was taking a little bit of time to to load up I think there was something where it was not loading things
up uh the other thing is you also have to sleep at the end because otherwise um the sound gets cut off because you have
to give it because it's running on a non it's non-blocking so you have to basically wait until uh the sound the sound
completes there may be a better way I I spent probably far too much time trying to figure some of this out and I figured
uh does it fail in a pipeline without it on your device I have no idea I haven't run it um I haven't run it on anything
other than locally this prop I would not be surprised if one of these things through an exception uh so I mean so there
might be an it might be an unsupported audio file that's fine these are wav files so that shouldn't happen line of it
unavailable that could certainly happen if it's running on on a VM or container or something that that doesn't have that
support or perhaps so probably throw this kind of exception if it weren't available and then it just so that's something
I want to uh integrate this so there's sort of like three different things I'm combining one is playing sounds two is
having this uh Notifier listen when when the uh when the full test execution completes um and the third is running uh
Maven demon so Maven demon is relatively new uh it's basically instead of having to to start up a jvm cold start execute
it uh and then you know build and run the tests may even D sort of keeps keep stuff warm um and so it can can run a
little bit faster well let's be honest like the startup time is is really really small like on at least on this machine
so which is all I care about uh anyway so that's that's something I'm gonna work on uh uh set of size and some time to
to work on um the so my main goal for today uh which is the refactoring practice is fixed primitive obsession um so I've
got great techniques for for fixing primitive obsession uh that are just scalar values right numeric or string or
something like that or for collections but when it's a combination of the two then it then it's a bit more more tricky
yeah I don't I I think I I think it's I don't know how to package this kind of thing um because I I don't want to make
an IntelliJ plugin because that's just it's really not fun to make IntelliJ plugins it's just I I've done it uh and
every time I think like I want to do it I look and I'm reminded of how awful it is uh so it's probably not going to be a
plug-in I'm really just waiting for IntelliJ to um to finally to someday Implement as an open issue where right now what
you can do is with any run execution you can say uh where is it before launch you can add a before launch task what I
want and I'm not the only one is I want an after completion task because what I want to do is I want to be notified by
IntelliJ when it runs the tests did they succeed or not because I actually want to do several things if code changed and
test passes I want to do a commit uh uh otherwise I want to be able to run like if it if it pass and play play a happy
or sad sad sound so there's all this stuff as a result of the the running the unit tests that I would love to be able to
do but IntelliJ does not currently supported it doesn't have that option and there's an open issue it's been open for
some amount of time um don't know if they'll ever do it there are plugins that that do some of this as an old one called
infinitest but it hasn't been updated in in years I don't even know if it still works last time I tried it I don't think
it worked uh so I'm not going to package as a plug-in I don't know what else to package it as because I guess I package
is that a package it as a library um because the meta in service is just in the jar and as long as that jars I'm not
sure um probably would be it would be a tiny tiny junit plug-in yeah Astrid uh I'm saying this works fine on Clips yeah
that's a price I'm not um and I think part of that is because uh Eclipse works very differently in terms of how it it
compiles and runs things like your you can you can run stuff even if not everything's compiling it sorry uh all right so
um I was talking about primitive exception primitive exception primitive Obsession you can have primitive obsession with
exceptions but that's a separate issue uh so one of the weekly ensembles that I that I run we've been working on this
blackjack game which comes originally from my course uh up and we've been working on it for for 92 sessions um and last
Friday which I guess is yesterday um uh uh we ran into an interesting situation around uh primitive Obsession so one of
the things that you do in in um and in the game when you do lace bets so there's a method Place bats that takes a list
of integer yeah trampstars you can you can go ahead and start campaigning for that that's so place bets takes a list of
integer now this is this is problematic um because of two things and so this is basically primitive Obsession first of
all one of the things that you have to do is is you in fact I'm gonna go to so magically I'm now back at a point right
before we started fixing this problem one of the things that we have to do when we get a list of of bets is first make
sure that each individual bet is a valid amount what is valid Well it can't be negative can't be zero and it can't that
means anywhere I'm I'm operating on the other part is if you look at this you get you get no information code smells
that that once you see it you start seeing it all over the place especially in a language that has that has static types
like like Java or c-sharp integer tells you nothing about this it can be anything and so therefore you you have to
figure out like what do they mean by integer here you can tell by the name of the method it's probably something to do
with bets but you have no idea how would you get information about what kinds of things are going to be done with it you
would have to look through the code so exactly so it so this should be a value object right and value objects is is a
perfect is one of the most common ways to fix primitive obsessions you create a value object sometimes an enum is fine
if it's if it's something that uh like you know suits suits or or ranks of a card um but exactly with scissor it's it's
it's missing it's this idea of putting domain knowledge and abstractions right into the code and the more we do that the
more it's clear what you're supposed to be doing what its range and maximum values but really like what's it about give
me give me some kind of name some kind of handle so I can focus on on other things so one of the things we did uh uh
earlier in this code base is there's a way to specify when you start the game how many players are basically at the
table and at some point we'll probably rename game to be table because that's really what it represents in in the
blackjack game um and so when you say uh where is it uh number of players but then we had to validate it and in fact we
were invalidating it so you could have a hundred players uh and that was probably not a great idea or you could have
zero players and then yes absolutely transtars I tell people sorry not sorry once once you really start getting
primitive Obsession you start seeing it everywhere and start wanting to fix it everywhere so here what we did we
basically turned an ant and any validation that we had on it into uh in this case a record so the validation is built in
um and there's some interesting stuff about this validation so James Shore and I uh have talked about some of this kind
of thing and um I've been thinking a lot about do we want to blindly throw exceptions that the caller might not be aware
of that are going to be thrown because we don't declare them right they're not checked exceptions uh so runtime bug
which would show up that you that you might not be expecting uh but I think in this case it's fine there are other cases
where where where maybe um we'd probably want to have a a validate thing because eventually like and this is to me the
fundamental thing this gets into more about validation which I don't want to go too deep on but like where does in how
would it could possibly be less than one or greater than five well somewhere we got information that came from outside
of our code base right it was typed in on a UI it came in through a message was read in from a file somewhere we got
data that was outside of our system and we need to make sure that it's correct um and what what this does is is not only
protect us from now in this Constructor I don't have to check to make sure that player I just accept it and it's by
definition valid because you wouldn't have been able to create it unless unless it was valid um the other thing is is it
makes it cleared right sure the parameter name tells you what it is um unless you have sort of the code inlay hints that
show you the names of parameters and honestly I I can't stand that that drives me crazy uh when I see it I just like I
don't I don't need to see that and yes I can ask for what you know what are these parameters um but it's a lot easier to
to just have IntelliJ say hey when you want to create right and you you know you start typing um it's already going to
suggest what the thing is and then I can go in and do that so yeah if you're if you're in a language with named
arguments um still think it helps to have a type because the name of the argument may or may not be intention revealing
enough um it can only go so far so it can tell you sort of the concept but everything else you still won't have right so
number of players right that's really a nice name and if that was there uh that's certainly a great start but it does
not tell you right it's still missing to me key information it's this idea of we want one place for Concepts right to me
that's that's the whole idea behind like cohesion I want something where I can still get in one place and say what does
this thing mean what does player count mean and we know what it kind of means casually but like okay what are the
details of it is you know what are these well these players okay that that's fairly clear but what's the range oh it's
one to five how do I know because there's one place in the code that I can go to it's not strewn throughout throughout
the place uh and also one of the things that it does is we start to see as we raise a level of abstraction of of our uh
of things in our class we we may start to see hey look I've got this players thing here and I've got bets and as you
raise the level abstraction this is really about player bet it's like oh I've got players and player bets maybe there's
actually a further missing abstraction domain concept or maybe this is just the bets are actually belong in player who
knows um and there's some interesting questions about that that that our Ensemble is going to have to figure out because
when do players come into existence right now they come into existence when the game starts but really they should be
longer lived because they'll be their account balance associated with them which can span multiple different games
multiple different rounds so there's some really interesting things about you know what's the life cycle of a player
versus their bats and how does that relate to game and then it turns out there's a missing concept of table and rounds
and things like that exactly transfers right I mean that's that's what we want to do is we want building blocks of
meaningful things and those meaningful things they have to be meaningful they have to be meaningful from from a domain
concept it's long those are not meaningful those are those are meaningless uh someone had mentioned the other day to me
um object calisthenics so there's these rules about sort of you know applying good good one of the rules I think in
general the rules are okay one of the rules was classes shouldn't have more than two instance variables and I'm like
okay I get the idea and I and I'm and I fully support the idea that most of the time classes have too many instance
variables too many instance variables means the class is too large and it's likely not cohesive because what is cohesion
cohesion is is how many methods do you have and how many different instance variables do they work with if you've got 10
different methods and five of those methods are dealing with a few instance variables and the other five methods are
dealing with a completely separate set of instance variables that's two classes that's not cohesive and probably should
probably be split and so we want at every level until we get down to the level of player count we want we want meaning
so player count was easy we just took we go through a mechanical process of extracting a delegate doing similar
factorings and getting to the point list of integer is interesting because what is the abstraction here and if you've
got ideas I'm I'm open to them the integer certainly is a bet it's a player bet although I don't think we have to say
player because who else is making bets in this game it's only players make bets so it's a bet this list of integer
though there's no domain concept here what is what do we call all the bets on the table they don't that's not meaningful
from the domain uh point of view and in fact the fact that we can't find a domain concept means that there's something
wrong so uh to me sort of constantly looking for primitive Obsession like list of players what does that mean is there
something missing there and this is very much that same feeling of it feels like there's something missing yeah so
there's this table or something there that that's missing but I'm not quite sure what it is but certainly uh the list of
of bets has no meaning yeah so I would think that um some future future abstraction would be a table that has players um
table has players and has a dealer uh and most of what's currently in game would would become table um but then there's
sort of the the game in progress uh and that's where some of the code that's currently in here would go for example the
player iterator that's iterating through the players this actually has to do with a game in progress the shoe uh the
shoe technically could be used across rounds across games um and then it gets reshuffled when it when it comes out so
maybe it's across multiple beings this one um also across multiple names this one is is definitely game in progress
although there's there's dealer behavior and then there's the dealer hand the hand itself is is is for a specific game
um what I'll use them for what I use the bets for the bets are used uh I assume that's what you're asking the bets are
used eventually uh to figure out how much we pay them um and that's the feature we're currently adding is like at least
in in this Ensemble we're adding the feature of betting so we are able to place the bets and then the next step is to be
able to then say Okay based on the outcome how much do you win or lose I'm sorry that you discovered that I don't know
yeah TVs are not meant for from for for showing this kind of of um uh uh game has table and table has bets uh the way
I'm currently thinking about it is a table is sep the table has players and players have bets lexler is my thinking of
tackling game in progress no no not I'm just pointing stuff out or I'm not I'm I'm not doing anything with uh um uh uh
what was I saying yeah so so my current thinking about the abstractions is there's a table and players basically
attached and themselves join and leave tables um and then a game starts and then sort of the table is in game playing
mode so there's some um but in terms of bets I very much think list of of integer doesn't have a domain concept and it
actually must match so there's actually a validation when we place the bets that the number of bets placed matches the
number of players so there's this relationship there that to me clearly bet belongs to to player because it's a player
placing bet except they're doing it in the context of a game so there's it's a bit tricky who's who's holding on to that
it's a play does the BET actually belong to the player what if the player is betting across multiple tables right
because in the real world you couldn't do that although you can do multiple spaces right they're multiple slots at a
table you can actually play multiple hands uh but in a virtual world you can play multiple virtual tables but you're the
same player um although are you the same player or the same user that's associated with multiple players right there's
all sorts of I was saying I was saying the other day like it's amazing how what seems like such a simple thing hey write
some code to play Blackjack right I remember you know it was one of the first things I wrote in basic copying it out of
the computer games book you know back in the in the 70s but like when you start saying okay we got to handle betting we
gotta have multiple players we've got to have multiple tables and things are going on simultaneously it is yes it's it's
it's definitely uh lots and lots of complexity even though it's like yeah asteroid players have seats and there are
current cards set in the back yeah so the guy so I think it's sort of like player player sits at a table and so table
has seats and so at least you know the first cut would be a one-to-one association between players and you know so it's
a world of players users kind of things and then you you'd say join this table um and then once the game is in progress
the table sort of locked uh and then um I actually think the bet is because if you look at how uh how again it it works
even in you know virtual games you don't hold the bet in your hand it's not like it's in your pocket it's literally
right there in front of the cards uh on the other hand where are the player hands right now they're in player so uh so
since the hand the bets are really associated with the hand and this is something that we'll find out when we when uh so
so let's cover your eyes this is something that that will come up eventually um when you split so Blackjack has some
complexity about things like if you've got two cards that are same same rank right the pair of eights you you can split
them into two hands and then then the bets are associated uh you basically have to put up put more bets in because now
the bets are associated with each hand um so really bets are associated with hands not players and it's it's a it's a
subtle distinction uh but yeah that that that and what I love about again sir I you know you never know how how Stuff
how complex stuff is up front right this is sort of the biggest problem in software development you never know all these
details up front uh uh and even if you do you're like you can't implement it all at once and so finding these details of
you know sort of as they reveal themselves and the relationships that are revealed to me is all right Lexus you can
uncover your your eyes hmm yeah right it's it's like here Implement Blackjack Implement betting right that was the story
right that was that was um so uh at least for now this has no meaning um all that said I'm not doing it I'm not going to
be doing any of that refactoring the refactoring I'm I want to do is how do I reflect if this was just an INT again it
would be easy to to refactor because then I could just extract it as delegate and move method to to move stuff to to the
new place um but when it's a list of integer and I'm only interested in replacing the integer part this is this is much
harder so we uh in The Ensemble we started doing it mainly basically manually I mean still refactoring but not using
automated refactorings and I'm uh and I wanted to spend a little bit of time of trying to figure out can I do this go to
attitude wow 18 months thank you so much for for resubscribing for 18 months uh OSL is why we invented also for
architect to produce expected to go off in a room and draw box scenarios to capture the complexity inside yeah it
doesn't work I've been done that been there done that set with people trying to break down the work trying to estimate
the pieces of the work it just doesn't work you can you know the planning is important but the plan itself not not
terribly helpful right the design is important the designing is important but the design itself is is not terribly
useful yeah exactly with Sarah it's like it's it it the the details and level of complexities is this fractal nature of
it that um I don't I think is is one of the things I like about about this stuff uh no you didn't miss the effect I've
um all right so um so we got this place bets method so what right we'd like to end up with some method like this that is
place bets that takes a list of that that's what we want and so how can we get can we get there using automated
refactorings I have no idea I don't know um so one thing that we uh that came up as an idea remember what happened to
the world orc thing I'm gonna come back to that one I might have to do that on another stream uh because this was the
one I wanted I um so one of the ideas that came up with uh that came up during The Ensemble is treat this as that the
bets are something and then see if we can go from there uh and and I had trouble sort of conceptualizing that that
second or third step so we're gonna we're gonna uh and don't stick to the plan when circumstances yes yes exactly do not
do not stick to the plan just because it was the plan so uh what we can do is we can basically oops that's not what I
wanted I wanted that they're essentially the same outcome what would extract delegate look like so that would pull out
the whole thing and delegate the place bets and current bets to something else so if we did that then we'd have we could
call it a bet Handler right I want to I want to try this one though uh but not yet so let's let's do the um so I'm
puzzled by this keep method so here so this is this is why experimenting with the automated refactoring is so important
is because it's the documentation on on these things are not great because it's really hard to document these
refactorings because you'd have to write like pages and pages of well if you do this and this is the situation then this
is what it looks like but if you do this and you check this checkbox and this is what it looks like and so you have to
kind of experiment hmm yeah exactly whiskey as the meeting is is useful because you can find out what you're assuming or
what you don't understand especially uh if different people estimate differently but the estimates themselves are are
not terribly interesting um oh yeah yeah that's that's the question uh I I tend to try to not do very much playing at
all um but that depends on sort of how quote agile you are all right so our new class uh we're gonna call it bets plural
because it's a list of them um and uh we'll create a new class I don't know that that helps so let's create a new class
and just no lexlers this is this is uh reset back to the to the point where we uh uh uh didn't yet introduce the the bet
the BET class and this is bets plural yeah and I'm I'm shaking my fist at IntelliJ that decided adding the number one
was was important here because it is not um uh uh so now we've got so let me open this class up and I'm going to flip
this over so how does this help us does this help us at all this um oh interesting I created a record uh do I want a
record no I think the record I think a class is uh let's take that out so yes I could use dollar sign that um hmm
encapsulate Fields but that's the whole field uh yeah so this was was this was where I was stumped it's like okay so we
extracted out bets um but how do we get from here to a list of that right does this does yeah I don't think there's any
automated refactoring that's going to get us to change the generic type of this list and so what's sort of so so what's
going through my head is like what if I had like some variables right and sort of manually uh do that then I could
migrate each individual one and that might help yeah the type migration every time I try it's like oh that doesn't do
what I thought it would do uh so type migration whoops um we could try we could introduce bet and see if the migrate
works every I remember the reason why I I sort of discarded it but I haven't tried it in a while so we could try that um
so let's create uh let's create an inner class or let's just create a class here we'll call it uh wow that's bad and
it's got an internet uh um like a private uh uh you want to get our insetter for it and let's see see if that if that
does oh you didn't rename the things darn it was that intelligent uh yes okay um so let's see if we can we do a type
migration yeah so it's a it's a migration I honestly think this is not useful because it can't convert the expression uh
um so I just go and see if I miss anything Chad uh so what would happen if I introduced list bet as a second parameter
uh oh that's interesting Astrid about um so that would be an interesting thing to uh then replace it I don't know about
this this isn't gonna work uh we propagated list bet from the place bets method um yeah so that was that was the uh that
was the the next one right yeah so so by just introducing the parameter object that didn't really get us anywhere
because it only changed this method um what we really want is we want to change anywhere it's used to to that so let's
roll back uh we'll delete that um so so it still requires us to create the BET class so I don't think there's any way
for us to go manually there well actually we could do that here we could introduce parameter object for this and of
course it replaced it with some um yeah I don't think I don't think making makes us any this process any easier or
harder um let's see uh um I don't know if I want to do this though uh so we want a new I want bat new lists so this
won't this will help us fix the public method we'll have to probably fix the private method separately right so if we if
we introduce this as a parameter all the places that this currently exists um will be replaced by uh creating this list
but then we need to to change these to use it so I don't think so because there's no um and here is if bet we're a
subtype this won't work uh yeah whatever because there's no there's no way to convert an integer to a bat um bet
extended so if we did uh public uh we can we extend it sure I've never even tried can we actually extend it the great
costume super sure yeah I don't care oh it's marked deprecated marked for removal um yeah introduce the final class
that's what that's what I that's what I I suspected is that the the boxed classes integer and so on are are final um uh
yeah it's it's too bad we do number I don't think we can do number because numbers is abstract so I think this is the
wrong way around I think so and this is where again like the the documentation for um let's go back to a record let's
convert this to a class because I don't want it as a record um see I would have thought that because this has a
Constructor that would have figured out how to but it's not a direct conversion um it's like the documentation for this
is not very helpful this is basically the documentation uh so this is the documentation for type migration uh lets you
automatically change a member type um and this is kind of what I wanted to do but because it seems like this is what
this is what it should do right because that's that's kind of what it says right especially the container one right um
right from I to string to to I to integer is kind of what we're doing Maybe yeah I still don't understand why it's just
not letting me do this because it seems like that's what it what it should do I wonder if it's because it thinks it's
yeah I could I could ignore and continue and see what it does uh let me set a let uh created us so interesting um so
here okay that's fine because we were converting from one to the other foreign it did change the types of our methods as
well as the type here uh so maybe and this is fine we can actually delete this because this was temporary anyway so this
is weird um I mean this will go away anyway because the is invalid bed amount will be functionality that will be on BET
itself Astrid you you've read my mind I was thinking what if there was a copy Constructor uh would that so that is one
one so there's one error here we're also there are compile errors that's fine because that's a conversion uh is that it
just those two places I don't believe that um but let's let's try fixing this one uh yeah we should just fix it because
it doesn't need to new BET at all it's so let's do that let's just save that so that's a manual change I I lose a um we
got the Blackjack controller here bets um in the form of yeah so we need some kind of conversion method here which we
which already had and I deleted so we can just actually slam that in here that uh did I put that in the wrong place um
all right let's I'm not seeing why this is such a Mike wow that was weird okay you all saw that right it's like it so uh
so you have to to to remind me of the the move you're talking about luxler's I want to try different things and that's
why that's why this is experimenting is I want to do do different things so yeah so now we've got a bunch of places
where uh place bets was taking a list of of a number um and that just won't work because uh we need basically a list of
of bets so we'd have to replace those with bet of so this is we could make that change and we'd have to make that change
anyway um but I feel like this is uh and so this is this this is you know the situation that I talk about in my classes
where I say take small steps um that are that are safe because once you get into compile error land uh right once once
there's a single compile error you really don't know how many compiler errors there truly are right look like they're
only two but then we fix those and now there's what um a whole bunch more uh right now there's there's these and and
some these are warnings this one uh uh these are warnings that's interesting I don't care about the warnings um but now
they're like six different and this may be it uh from what IntelliJ reported I think there's still a few others um but I
think that's why the the method that uh that I use a lot which is introduce parameter to push out the type that I want
people to pass in uh I think would work better than than I still don't know what was up with with IntelliJ where it was
just not recognizing bet it had imported it and I think it's like it almost didn't realize that it had imported it or
something all right so going back to uh here back to um to our to the timeline what did you want yeah let me um did I
make any changes oh I did that's fine yep um so what do you want to want me to yes from here right and that's what that'
s what I was going to redo is is this manually um so yes that that works great once we're here but how how we get here
better is um no yeah so from here yes right because place um of updating this method to take a list of bets and that's
what I'm trying to figure out is uh uh is how can we get here without doing a in this time in this in this point right
we've got place bets that takes a list of integer that's fine if we could figure out how to push this out as a parameter
yes that fixes that fixes all colors yeah I guess I don't use hot swelling um I don't I I never never find myself these
days having to debug in production as it were um so so from this point is what I'm trying to figure out a better
refactoring for than or or at a more automated refactoring uh than what we did manually in our Ensemble which is how do
I get um and basically this as well and so that's um it would be interesting if I if if I could just so let me look
these around uh yeah so what I really want is and this is where I kind of feel like I want to push the conversion and
the usage uh yeah I could I could introduce parameter here um that I know but that doesn't help me it was your original
number was correct when you said it um so I can't I can't can't introduce this as a parameter but that means uh it and
that's um that's what I'm trying to to address right now is now one thing I could do is basically um this one doesn't
care about the type so this one is relatively straightforward because it's really about how many bets are there and does
it match the player count this one converts it to the bet this way uh and I don't um so yeah I was thinking now if we
introduce a proud or what what happens I don't think it's going to be smart enough to figure out what to do with with
this year but let's try it so let's so that pushed it out everywhere um but I still have to basically stop that's that's
the that's the step that I don't yeah so you only you can only get rid of this one during that introduced parameter if
you stop using it so let's push it back um so I have to stop using I have to basically replace so I can do that it's no
longer an automated refactoring um but so far what have we done we've inlined that's a refactoring somebody needs to
somebody needs to keep score so we did an inline on the two that's that's automated those are those are basically zero
points um we created the BET class manually so I don't I don't see any way of avoiding that uh yeah I mean it's all it's
all contained in this method we don't have to change the signature to private methods so I think that I think that's
where we are yeah is it's right it's like now now I'm basically doing a manual change inside of a method um and so the
reason so the reason why I focus so much on the automated refactoring is is I'm always trying to think about when folks
have code bases where they feel like the code they're changing isn't covered well with tests my preference is Go cover
it better with tests but sometimes you can't do that and so are there automated refactorings which are generally though
not always more reliable uh uh but I think here we basically just need to um uh but actually not that one so we need to
and then this is a manual change because and then we can just make it a Lambda um still means here we have to make this
uh but then we might be able to to do a a type migration because the type migration didn't work well uh because we had a
lot of places that were passing in a list of integer but if we introduce parameter to push this code out uh that might
that might be okay so so what's our score so basically create bet was manual um inline inline uh uh so the problem is
we're still storing bets we could and so here I'm trying not to change the instance variable type so we could say domain
we could do this in the form of domain bats so domain bats um and then basically map it uh uh uh so bet amount or get
that what was it that was in our vet class oh did not want to call that amount uh and this has to be actually this we
can then just say we don't need a copy of we can just do a to list because that will create our copy um so that was a
manual change but it's an equivalent change now we connect now this is the only usage of bats so now we should be able
to introduce parameter and yes and we'll remove bets because it's no longer used uh uh and then rename this to drop the
word pram so now we've changed external usages of this um current bets is still returning list of integer but I think we
can do a tight migration on that all our tests should and now the call sites against this are a bit ugly a list of one
stream map bat new to list uh uh but we should be able to um uh we'd have to clean those up manually um we could use the
uh structural search and replace to replace those but the point is is we haven't broken we haven't broken anything we
haven't stuff compiled and and works may not be great uh but it compiles and and works so now the question is is uh so
let me put a placeholder here um there it is it's odd that it says it can't convert the empty list because empty list
works with any list type which is too bad because actually it it could it would just drop the stream part um the six
here that's going to be a problem uh uh the assert that that's going to be a problem so this might but I think this is
fewer than we had before so let's ignore and see what happens so got one compile error here but that's an easy fix
because we just say uh in actuality we basically just do uh this copy of our domain bets so that and now we've got a
compile error here um but that's fine we can basically do a bit and I presume you were streaming earlier I'm sorry I
forgot I don't know what your schedule is I was just randomly streaming welcome thanks for thanks for I should add to my
I should add to my calendar like when when you're streaming because I know you're more regular than I try not to stream
the same time as people like you so sorry about that I'll I'll make sure to watch out for that next time uh so here I
think we can do um an extracting and it's basically bat uh uh no bet I don't know why it's having so much uh but let's
go ahead and then convert um yes it does assume bet is immutable and bet is immutable so that's fine yeah uh that
actually wasn't so bad so the first doing the introduce parameter to get this to be list of bad so inlining these to get
rid of the private methods that would have been awkward to change then we can now re-refactor these uh and then doing
the type migration converted this for us automatically leaving us to do a manual change down here but it was a very it
was a trivial manual change and then fix up a couple of places in the code in the test code but not that many um so I
think that's probably the best that so this is this is where the game of refactoring golf comes in right it's it's like
okay we did a manual change to uh here let's look at our commits so we created the BET class that was manual um and then
we changed uh no wait no we actually didn't do that manually right we actually extracted uh we did that as a an extract
parameter object so on the is invalid amount we extract parameter object and we get a bet object and so that creates our
bet class right because it did it yeah because it created the record and then we converted to the class so that was
automated um uh then we oh because that's game service uh this is what we're interested in yeah so then we basically um
took took domain bets Define so here is where we had to do the manual work to define the con Define the conversion what
do we what do we what have we got we've got list of integer what do we actually want the parameter to be we want it to
be a list of BET and so creating this and then changing the code that uses it to use domain bats then introduce
parameter so manual work to change this but we inlined it so it's a little easier and then introduce parameter that got
us to the point where we then um only remaining thing was we were internally storing it as a list of integer type
migration got us over that last hump within some some minor manual cleanup um yeah and so now we can now so when I do
these kinds of refactorings there's this um sort of large granular large-scale changes and code is getting messy as as
you're doing it and so for me there's always the tidy up face like okay what were the things that that I knew I was
going to have to to clean up so I know I'm going to have to clean up things in my test where they were converting
needlessly things back and forth as well as the um these uh preconditions we can now re-extract them and they'll do the
right thing so this one was um well this one we want to leave because actually we're not done yet so we've done uh we've
we've solved primitive Obsession and always what happens once you solve primitive obsessions you now have feature Envy
so now we have feature Envy right here we're basically streaming through um we're calling this method invalid bed amount
but this actually belongs on on BET uh introduce field on the new list of bets um you're talking back at at this point
Astrid um I think at the point where and I didn't capture this as a commit I'll probably do this again uh and and do
more frequent more even more frequent commits at the point where this was this uh uh we could have introduced a field on
this I'm not sure that would have helped because the the type migration did did the swapping of the type of of the field
of bats for us so I'm not sure what what what that is that true are we going to have no more list of integer um I'm
still I'm still like why IntelliJ thought that it couldn't do an assignment of this to uh for the conversion of the type
migrations like that just works um so uh primitive obsession creating the BET class revealed now feature Envy for the is
invalid amount we know it's primitive we know it's feature Envy because it's making a decision based on information
pulled from another object not supposed to do that so we can take this we can do an F6 move move it to bet and now um
now it's basically just just a slightly slightly nicer so now we can uh take this extract this to require all bets valid
require valid bets um let's be more specific that we want better mounts uh this one goes back to being required um and
there we go so now these which were list of integer before now of course their list of bet because we extracted them
after we'd already already changed that and so now if we look at bet um we might also want to make it easier to create
bets uh and so converting this to a factory method that's another clean that we can do uh we're doing this require valid
bet but why should we even do that right the whole idea of fixing primitive Obsession for this integer was to make it so
that if you have a bet by definition it's valid so uh no you shouldn't have to call it manually right um again this is
this is now a manual change uh we want to make sure that you can't even create a bet unless it's valid this currently
requires it to call amount which is kind of silly so one of the things that happens is when you do a move method to to
cohere the method to put it where where it belongs to fix feature Envy a lot of times it'll you'll end up with stuff
weird stuff like this where we don't need to call a method we can just do do this um except we want is invalid amount to
be uh to not be a method on really on the instance anymore we want to move that earlier so we're gonna have to create it
make it static so you can go ahead and make it static we're going to add the parameter for the field yes I could have
done the inline turns out in the in inline is actually more keystrokes than just deleting the parentheses but yes um
field amount is not accessible really um what would happen if I do that ah yes so I shouldn't have actually done that
that you know any raccoon you missed the part where uh you can't extend uh integer so not a crazy idea um but it doesn't
work yep um so now I wanna but I don't actually want Ben as the parameter so let's not do that uh see here's where doing
it the the um the inline way I have to do this and I have to say inline only and keep the method and then I have to do
the same thing here uh turns out just deleting the parenthesis is easier and then I can uh so if invalid that amount
amounts uh we'll throw extending objects everything extends objects um this should be equivalent so here I'm um I am
relying on my tests huh okay uh IntelliJ should have changed that to me is a bug but easy enough to do you not do it any
everywhere what was the point of doing the refactoring if you're not going to fix all right um uh now we don't need this
required valid bed amount anymore because you can't create right and how do we know well we can go and comment out this
method so this is our this is where we're treating our tdd as uh an experiment platform so our hypothesis is we don't
need this method anymore and our experiment is run our tests and see the result everything still passes how do we know
that it's actually checking for the exception well we can actually stop throwing this exception and see if stuff fails
the stuff was expecting that exception to be thrown and so that's now yeah so I I'm not sure what happened when uh when
I converted to a factory method um I'll have to go look there may be something I missed uh but yeah so they'll why do
they make into your final uh performance reasons and uh other reasons that are probably much more useful than what we
would have needed um the eval bit amount in terms of the exception I'm going to get to that in in a second uh and yes
amount is now public but now uh now I'm gonna go clean up so now that this is no longer needed we can go ahead then and
get rid of the method uh we can go ahead and make this private again run our tests everything should still work um and
then uh re-extract it to be required um uh uh I don't feel like I need a two string or actually I'm going to regenerate
this stuff oops oh I don't check for null um this is an artifact of what it was a list of integer but this can just be
an INT um oh because we don't have equals great perfect so now uh and this should be integer in two now I can generate a
proper uh equals and hash code okay and I'll generate a two string just now all our tests should pass because we've got
a proper equals awesome okay um I don't think there's anything else to I think that's fine uh now we can go ahead go
back to look at place bet so now placebets doesn't need to check that each individual bet is valid because now that's
done by bed itself and so now we're just requiring that it matches the number of players and then basically a more
Global uh check that cards have not been dealt because you can't bet after cards at mendelt that's not what the game of
blackjack is about um pay it up bad to use instead of insecure concretion um yeah I mean maybe the uh the required valid
amount should be in the Constructor that's a good point uh here it doesn't matter because it's private but sure it is
certainly possible that somebody could unintentionally make that public uh and one of the things we want to do is try to
prevent future silly mistakes like act basically prevent accidents uh so maybe in the future to prevent that kind of
prob problem from cropping up um I don't convert to factory method until I've already gotten all the validation done in
the Constructor uh I uh asks about cards dealt belongs on player cards cards dealt is a table game oriented thing we
don't care that cards are specifically dealt to anyone we care that the car the initial deal has happened and that's
what it means the fact that we're checking it on a current player is uh and we talked about this in our Ensemble where
basically it looks like we're missing some a concept of what stage are we on what state is the game in uh I thought I
had a file no I remember what happened I was I was trying to use chat GPT to have it create a mermaid diagram for the
states of of a game and I gave it the states and it just couldn't do it I said no I want the player turn to be a sub
State and the dealer turned to be a sub state but the overall thing to be this and it just could not gen no matter I
tried for like 20 minutes and it could not generate the right syntax I have a feeling partially it's because it there's
just not enough examples in its database for how to do substates using mermaid um and that's possibly also because it's
it's database it's its database is a couple years out of date uh but yeah no matter what I said I said no you've created
the state diagram I wonder do I let me go let me see if I have that chat yeah so uh you can see how how long I was
trying like it was like here create a state diagram I was like okay um I want a higher level diagram includes the
betting phase because it forgot the betting phase okay and it generated this thing with with sub graph it's like sub
graph is totally wrong like okay try again okay well now you did it uh uh but it's state oh okay I'm sorry um and now
now I need to show where the decisions are and then it just like it could not create the right thing it's like this isn'
t even write syntax let me try again well now you're not using this the sub State let me try again it's like okay now
you didn't create you lost the states for the player in the dealer turn and I was like okay no I don't want it it was
just like this back and forth like I it's like and and now you just ended up with stuff that still does not work over
and over and over and over again um and I was just cracking up because I'm like you you just don't know what you're
doing because you're just copying predictive text so sometimes chat GPT can can help with but in this case I I really
honestly I expected better from it and I um so anyway all that's to say is that they're uh uh getting back to what what
triggered This was um we don't in the game currently have a concept of what state is the game in right because it is a
state machine it it's and it pretty much is uh something like this right place bets deal player turn and then dealer
turn and then determine outcomes yeah I know my expectation was too high I figured something I mean this is right up its
alley though right it's not like I I expected it to to um it's like this is supposedly like what what these kinds of
tools are for and it just it just couldn't do it I don't know why it got confused about the syntax it shouldn't have
gotten confused uh and hikers welcome um so it's like this is sort of technically correct but it's not at all what I
wanted uh and I ended up I think I I was trying to do it and it's like oh the problem is mermaid actually doesn't draw
it the way I want to draw it and that's not the syntax problem it's just I don't um yes so uh that is a good point about
we really shouldn't be making a decision based on sort of internal information so I agree that that that actually should
be a has cards um we could ask hand value but really has cards is the right question uh so I agree that that that that
that would be a slight Improvement um but the real issue is we don't what we really want to know is did the initial deal
happen and that would be a state transition um and we just we just don't have we don't generate that kind of information
we don't store that kind of information what's interesting about this and this goes back to um uh some other interesting
conversations we had around the game class there's all these methods on it not all of them are valid so let's look at
its public API um so we've got um dealer has a query events as a query initial deal is a command but once you do initial
deal you should not be able to do initial deal again in that's not great um place bets well that's what we're just
talking about you shouldn't be able to place best if initial deal happened and so this is where the state pattern as
ugly as the implementation is can be really useful because you can say look we are in betting game right you can't do
anything but place bets there's no other operations that are valid at that point right you can't you can't even ask the
question of like what are the player cards you can't even ask the question of what is the dealer hand because it makes
no sense to do that at the betting phase then once you're out of the betting phase you're now in the initial you know
the game I won't use the word game started because that causes all sorts of confusion but you're in the phase of now
game in progress the cards have been dealt which means you can no longer call Initial deal and you can no longer call
play place bets makes no sense to do either one of those those are completely invalid commands and even some of the
queries like what's the player outcome that's invalid unless the player is done and so one of the things that I think we
I see and and I don't do enough of it myself is really think about what is the proper allowable things we can do to an
object what is the protocol what are the preconditions what are the allowable operations and they're actually much
smaller right it's we've got all these these methods and this is kind of large but only some of these are valid at any
um let's go thank you for another sub for right Lex Liz and that's the problem with the state pattern at least as as one
one way to implement it you can basically have an abstract implementation that throws for all the methods then the the
implementations only have to implement what uh what they actually support there's no there's you could um because that's
you you need them to all be polymorphic you need them to all have basically be games uh if you want to go a little more
complex then you um you'd have to go a different route you'd have to have now different types for each phase and that
gets a little trickier however uh there are some ways to to deal with that um that uh I'm gonna I'm gonna be yeah so the
the throwing of the unsupported operation exception as a way of implementing this the state pattern really bugs the heck
out of me it just feels so wrong because you're basically throwing a runtime exception you're not but um in my in my
head um specifically the hypermedia part uh where um you present options based on what the current state is so imagine
the UI would would detect would be would be saying okay you can do a hit in a stand because the game said these are the
allow you know it's it's again very much that um so I'm showing my age you know the books where you had player on
adventure right says hey if you choose this go to page 45 if you choose this go to you know page 132. right those
decisions then lead you to other decisions but they're they're fixed decisions right if the game starts the only thing
you can do is place bets it knows that from the from the domain some of you are also showing your age by if you remember
those um and that's what we want is the domain knows exactly what's allowable and what's not allowable and so therefore
uh presenting that to the UI or as an option through the apis here's here's the links you can go to where to get that
the controller didn't care it's just translating whatever whatever's in the domain um then then it's just the technical
aspects of how do we do that um and so that's connecting those and so now you end up where if you can do that then you
don't have to use the this ugly version of the state padding you basically just have different objects how do you get
those objects into memory those are retrieved from a repository how do you know which object to retrieve well you're
calling a certain method on the use case layout right so the command uh that you're sending to the to the use case
layers to the service layer uh that that's something that that is really interesting because it prevents all these these
invariant problems um now I haven't implemented that all the way through so it's just this fuzzy idea in my head I and
there are other uh place there are other Frameworks that I've seen do this kind of thing although they've always felt
really heavyweight uh axon is one of those um so anyway so that's something that that I'm that I'm going to be exploring
uh on on future streams uh uh Swedish came in for your final closing thoughts now I I we basically just finished the
refactoring um and we were talking about uh uh the problem with with cards cards dealt yeah I mean if you if you exactly
that that is definitely what you want is the UI doesn't have to do anything anymore assuming you're using um actually I
think an Spa a single page application or or server side generated would be the same thing the the choice is really up
to to The Domain and and trying to copy that logic into the UI is such a waste and so prone prone to error when it's
really just like the domain knows what's available let it expose it yeah through however however it does it it can it
can expose here the the next possible things um that's where it can get trickies how do you expose it what does that
look like um but then there is no logic on the front end it's always saying what's available what do I do in fact right
now even we have a bit of that although it's going to get much more complicated and then it's going to have to get
easier because we're gonna We're not gonna like it how complicated it is right now what we do in the controller is we
redirect right which page do we go to which right the logic is is basically asked in the game where are we in the game
there are only two current states in the game it's either not over or it's over and so if it's over we redirect to done
if it's not over we redirect the game be in progress the in progress page once we add betting in um and once we add
especially more complicated versions of betting with uh splitting and uh and so and insurance this mapping because
that's what this is It's mapping state to just what page do we go to uh will just need to be expanded and that's where
we'll need to have some states uh exposed by the the game service so that we know how to map them um so that's that's
that's what I what I want to implement uh because um uh Captain Survivor and some some other some other folks on the
Discord we've been talking about this in the Discord by the way if you're not in the Discord you're missing out on some
great discussions like this uh and so I was talking about you know just the the simple idea of when you're playing like
a game like chess there's at least two states from a from a technical standpoint there's you know the players putting
the pieces in the right place um and then there I mean maybe the computer does that for you but if you're really just
saying I'm implementing where I can allow you to set up the board or maybe it's some other kind of game where there's
the setup phase uh once it's set up you don't have those operations anymore um and I see this this pattern time and time
again of objects go through different states where certain things are allowable and certain things aren't and they
transition and they really should become different objects because the things you can do to them and ask them are
different and this is where the data in the database may be the same but how you look at it through the lens of what
object does it become in memory it's not a one-to-one relationship and this is uh this is key so um there's been on and
off debate about map objects domain objects to some other kind of object in order to store it in a database and on the
one side it's well I like clean separation but if it's always one-to-one I could totally be convinced that's Overkill
that's really not necessary but what if the same data is interpreted and loaded into memory as different objects
depending on what you're doing yeah exactly Esther there's there's there's a whole set of of these sub games the um
place your bet game you know place bet game there's the uh uh ready to Deal game there's the cards dealt game which
becomes then as soon as the cars are dealt well then now you're in the in progress game then there's the dealer turn
game right all the players have gone but now it's the Dealer's turn and then there's the game over game and they're all
game and right now it's that's all currently represented in one large object that's persisted in a certain way I this
this timeline does not persist games um there's another timeline that does I have like six different uh Ensemble Series
where we work on the same project they're all often in different directions so we call called the Multiverse the
Blackjack Multiverse um but the data is the same right what cards the players have what cards the dealers have if they
have any how much what are they what bets have they placed the data is the same and if you just look at it's like well
it's just the game object and we store it as a game object in the database yeah that's one to one and and why bother
with the overhead of mapping but if they're different objects and so there's sort of views in some cases maybe even
literal views of the data that are now different objects in memory so chorus asked about who's the persistence
consistency Authority one of the nice things about these separate states is a lot of them are are read-only views so you
get rid of some of the the persistence consistency the other one is is is if you tried to for example let's talk about a
game you you couldn't retrieve it so I'm assuming that the database is owned by the application right if somebody else
is also modifying the database you've got other issues around consistency some so I haven't thought about that and you'd
have to do some of the stuff that James short and I have been doing about database consistency about making sure that
it's valid but if I tried to read in a game right and we had these multiple different states right so we had right and
then the uh in in progress player term players turn game dealers turn game and then uh completed game all right so let's
say those are the those are the four phases uh there's gonna be some enum or some information that tells us what type it
is so if we are currently in in the Dealer's turn game and you try to read it in as a place bet you couldn't read it in
in we're in the end game now you couldn't read it in and try to operate right you couldn't TR you know because if we
were in place bet game the only thing you can do is place bets when you're in players turn game there's no such method
so if you try to read it in and now dealer's turn and again whether these are the phases if not is is separate issue if
you try to read it in and it's currently in dealer's term but you tried to read it in because somehow there was a UI bug
and you tried to do place bets it would blow up upon reading and say sorry I can't do that there's some data corruption
um or there's a there's an error somewhere um so I don't think the the persistence you know the type because you you
somebody asked for it to happen right so um because assuming the UI works properly it once you've submitted the bets now
the the game in the database is in players turn and so what is the UI presenting it's hey player one do you want to hit
or stand and so you click on the hit button it does the hit command that use case that service method goes to the
repository to retrieve the player's turn game because it knows exactly what type it should be in um that's hard-coded in
the service layer I don't think that's a big deal I I don't know um there might be another way to map it but it's always
the the application layer knows what's what what object to retrieve and since since it is in charge of retrieving that
object I think that will just work uh and absolutely you could if you wanted to have a separate repository for each sub
game absolutely uh and there's then you could then your command then the method becomes then a command that has the only
repository it knows it needs to know how to retrieve from uh and these things then become more more isolated uh so to me
this is I don't know and you know a lot of this stuff has been done before in different ways I haven't seen anybody do
explicitly this way and it just could be good that I'm not aware of it there might be a uh it's a lot more activity in
the c-sharp community uh c-sharp.net Community for some of this stuff than there is in Java uh who knows about the
transition from one game to the other the game does the game knows about if you do this right so when we do operations
right when we do commands we do actions right they're all the same thing right is a command and it and then when you ask
the the game what are you what's what's your current state it will tell you what its current state is and each
implementation it would be hard-coded uh yeah there would probably be an interface that would have something that all
games oh that's off the top of my head I don't know if that'll work but that's sort of what I'm thinking is that uh then
you can ask generically what state are you in uh and then that's how you'd know so the command would still not return
anything because I really do like true commands uh being not returning any values and then there's just a query that all
games know and they would return a hard-coded piece of information so each game knows its own State because it's
literally identified by by its state and they'd all be uh the game interface so you could ask any of them what state are
we in because I think that's something that is indeed common and so show me the current game um well that's going to
differ depending on what what state it's in if it's place bets even that question of show me the current game all it's
about is we're waiting for you to place your bets there's no other information that that's gonna have because other than
you know we know who the so what I need for this um Fork this uh The Ensemble blue timeline um because it has actually
either this one or another one because I need the betting support but I also need the persistent support um so I'll have
to merge a couple universes and and get to the point where I've got betting and I've got persistence this universe I've
got uh persistence yes in this universe we have persistence with snapshots which is now the the way I do it uh this one
actually also has betting it um actually yeah so I'll probably I'll yes so this universe the the Wednesday Universe does
not have multiple players do I care about that I don't think multiple players is actually as important for for what I'm
thinking of I don't think that that affects the main goal of having multiple states with games retrieved differently
from persistence yeah I'm not mixing blue and orange glad to have you yes I'm one of the huge streamers who still does
Java and and um there's always things I don't like about anything uh yeah so I think actually this this one which is
from uh an ensemble I did for a company uh we got all the way to the point where we can place bets there's some stuff
I'd have to clean up yeah I don't know what happens if you um those are incompatible types you can't combine them so uh
I'll throw an exception um yeah so that's that's my my plan for that okay JavaScript right uh so probably start with
with this Wednesday one clean up some of the stuff that uh that we didn't do um but mostly it has everything I need it's
got persistence it's got betting um uh uh yeah so it's got everything I need yes Java is the best except when it's not
I'm very excited about like Java 20 is coming out what in a week or three um Java 21 is the one I'm excited about
because uh we're gonna have the the preview for the long-awaited uh string interpolation uh string templates not string
interpolation string templates so um it took off forever but they got it right so I got that judgmental look from people
every time I say I like Java yeah you know I don't know I I always have to laugh because like what you see with other
languages is this creeping towards the stuff that Java has like static typing um and yes Java's got some verbosity got
some things missing like string templates uh can I briefly talk about snapshots uh blizzard am I mentoring here uh I'm
answering questions uh I do private coaching uh if that's what you're asking about but I don't do a lot of it because um
I don't have much time these days uh anyway I'm looking forward to string templates um uh sequence collections also
looks interesting uh but it's a minor thing um but but the stuff that's going into to uh so what is a release date uh
March 21st so that's when 20 comes out 21 they there's they're starting to Target stuff for that uh so I'm looking yeah
I know the the the I'm always like uh I happen to remember 4 30 because uh one of the Bruno on I think it was Bruno on
Twitter tweeted about it but he got the number wrong because he was talking about long long ones um none of them are as
long as the loom virtual threads one which will have yet another either preview or or whatever for that I don't know
when that's going to be final I don't think it's going to be final for um yeah anyway I don't want to get sidetracked by
that um I'm really excited about Loom but I'm fine for them to take their time and make sure it works right because once
it's out and if it's if it's right and I think they've got the right thing uh I am I will be yeah rattling on it's like
and 4 30 and 431 and 8382 yeah no walk the work walk the board not the not the people and use names for things so but I
won't I won't go down the road of of jira numbers and and stand-ups and stuff like that uh yes Loomis is is fibers
lightweight threads uh there should be a jump for it though um virtual threats 436 so the second preview um my guess is
21 will have a third preview although maybe they'll get it right and early enough and it'll go into 21 since 21 I think
it's supposed to be LTS so 436 is the second preview of virtual threads uh it's pretty long if you're into thread stuff
boy there's all the information you need here um so that's coming out in the second yeah I don't know I don't know when
when that's expected to go final I I don't think it's going to be 21. um yeah so 20 has a bunch of of previews um but
that's the way Java works slow slow but sure get it right when it um oh I was gonna talk about snapshot and then I'm
going to end our end our stream uh mainly I was streaming this morning because like do I go out for a run oh it's
raining uh really stormy Thunder you might have even heard some of the Thunder before uh but now the rain's um well type
of ratio wasn't a mistake really really really hard to I mean it's one of those things where it's like you know could
they have broken back with compatibility to do it better and would that have been worth it um maybe but the intent of
java was always to be um what's your Universe am I in oh yeah so um this uh so I very much believe that separation of
concerns especially between domain logic and I O is really important for testability to me testability is my primary uh
goal and it um when we want to persist game sort of the the the old way I was doing it and and it was annoying and so I
feel like I I reinvented the wheel when the wheel had already been created uh it's very easy to take that information
and persist it assuming you have access to all the internals right there's a bunch of internal State here where there
should all be here or there should be a sub-object separate issue there's a bunch of internal State you need to restore
that that means there need to be some kind of query methods for each one of these and maybe you don't want to actually
reveal all that so you may have to break encapsulation in order to persist it if you just try to say let me pull all the
information off of game and then I'll persist it and then when I recreate it well then what do I do do I drive the game
through its its normal process dealing cards off the no that that doesn't work uh so you have you really do in a sense
have to break encapsulation a bit to do persistence unless you want to use like Java serialization object serialization
and that's just that's just a bad idea 15 years ago maybe we thought that was okay but now we're just like no don't do
that um so what you do is you need to create an intermediate object that's just pure data and that's what I've been
calling a snapshot so I call this the aggregate snapshot pattern because what we're aggregate what we're Snapchatting
the entire aggregate and then we need some way of of uh restoring from that snapshot so we create the snapshot very easy
and it's in an inner class because it's very it's appropriately coupled to to its parent class um and so by by its
nature it's very closely related uh blizzard I have a lot of questions every time uh feel free to ask and and I think I
mentioned my Discord uh feel free to ask good questions there uh when you look at the code you can understand oh great
yes it's nice when you can read something it's like hey I yeah so the the sub States the game will be interesting so
anyway so the snapshots just basically it's a dto it's a type of data transfer object uh that is very closely related
and connected to the object that it's persisting so that's why it's that's why it's an inner class and so then it just
has um and a way to restore uh right because when we load it from the repository we have to create a game and what do we
create it from what do we store in the Repository we don't we don't store um game objects we store snapshots the other
thing I like about storing snapshots and having that be as the interface as our repository interface of what we're
storing uh is it prevents a whole host of problems that I've encountered in the past if I stored game directly then
that's just a reference and then you see all of the changes along the way right that you really wouldn't like the
database doesn't get automatically updated when you make changes in memory there have been systems that do that they are
bad don't do that um most systems right have a clear separation between what's in memory and what's in the database and
you have to explicitly say I've now changed this in memory let me persist it to the database the problem with in-memory
repositories that hold on to the object directly is it looks very different you make a change in memory and this
repository sees those changes but by forcing you to go through the snapshot it sidesteps that problem completely and
makes it much easier to get and to to save and restore the object so for a whole host of reasons um I look back at what
I used to do and I'm like why did I ever do that that was that was just dumb um it was causing all sorts of problems so
why did I do that an example of of how dumb I was or how less I knew and now how I know um yeah then the in-memory repos
is still trivial to create but you don't have to worry about that seeing changes that you shouldn't that the repository
shouldn't see this is still wrong so this was my my uh attempt to add snapshotting to the repository but this is
actually still wrong because I'm saving the member I shouldn't be saving the member I should be saving the snapshot uh
and pairing with jamesford made me realize that yes that's that's the right way to do that here I do convert it to a
snapshot but the conversion back and forth is is just awkward um the bad example uh let's go here jdbc ensemble dvo so
when I when I convert from a domain object to the object that gets stored in the database it's fairly straightforward I
have to do some conversions to Strings grab some meeting IDs to convert them um convert and map just to the identities
and there's a bunch of stuff I have to do that I kind of have to do anyway but restoring it uh taking a database object
and restoring it and converting it back into an ensemble that's annoying because I have to do because I can't set
there's no method to say set State because that would be bad that would break encapsulation um so what I instead do is I
basically look at was the stored as completed as a string which is horrible uh all of these are enum so it's not as bad
but basically then I'm basically saying complete and this actually has side effects complete and cancel actually have
side effects uh so that's the other problem is that by going through sort of the typical routes the typical methods
right the typical command methods on the object as a way to restore the object that's really bad because these cause
side effects um but reconstituting it through the snapshot causes no side effects and that's what you want because
complete what does it do uh well it has some requirements right now it actually doesn't do anything else although it
really should um because there's some functionality that I'm missing that when it's completed uh uh well if the object
level at the Domain object level there aren't any other side effects because events happen at the service layer so that'
s not a big deal um but anyway it's it's annoying to have to to do that snapshot is a domain object yes um it is a it is
a value object it's just as much of a value object as anything else um but it is part of the part of the domain that's
my current thinking ask me in six months maybe I'll have changed my mind um because the snapshot can be used for
multiple things uh especially if you have to just to but yeah but really what I what I mainly want it for is for
persistence and um uh because you have to expose the ability to get the snapshot as a public method anybody could use it
so there's always some danger right there's always this trade-off right what is software engineering it's all about
trade-offs there's always this trade-off of well if I expose this somebody could go grab a snapshot and then you know
investigate internally you know and find some stuff instead of actually adding a proper method onto onto game but I'm
just probably trying to prevent accidents I'm not trying to prevent um well I always call them snapshots regardless of
the domain uh yes because in context what it looks like when when you call snapshot what you get here it looks like
snapshot but on the call site it's game dot snapshot and so I kind of like that so here at snapshot it's it's local to
this it's always called snapshot but from the outside you're always going to reference it as because it's an inner class
is game snapshot member snapshot Etc uh listen to Googled me yeah that's cool um yeah you can find me on LinkedIn you
can see a little bit about my history uh yeah yeah no we're not going to cryptographically sign our snapshots all right
um that's all for today uh thanks thanks you all for for great conversation well I've got the Monday stream with with
James Shore um that'll happen at its usual time which is uh one to four pm Pacific which is at eight hours because we
haven't hit daylight savings time yet so 9 p.m UTC right yeah eight hours nine PM UTC uh I may stream again tomorrow uh
but I if not I will be streaming during the week um and what else yeah join the Discord if you haven't um have a great
rest of your weekend uh stay warm and dry because I know in some places it's cold and wet so stay warm and dry and I'll
see you all next
