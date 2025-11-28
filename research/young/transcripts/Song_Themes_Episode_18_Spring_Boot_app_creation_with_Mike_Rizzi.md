# ＂Song Themes＂ Episode 18： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=j-9GtV5rbuI

---

## Transcript

all right folks welcome to episode 18 of working on the song themes app uh Mich will be with us in in a moment so that's
why he's got that's why there's an empty chair um so while uh he's uh getting ready uh thought I'd discuss a few things
so um first is uh we've got a weekly book club um except for this coming Sunday uh so every Sunday at 10: amm Pacific
Time 6 PM UTC uh we basically Gather in a zoom and talk about uh a chapter or so of a book the book we have been
discussing is the programmer's brain uh and one of the nice things about um discussing books as a group is you get to
really dive in deep on uh you know and elaborate and uh there's a there's a bit of a meta with this book because part of
this book discusses how we learn and how how best to learn certain types of things and so talking about and discussing
and asking questions and elaborating and generating all of these things are great ways to uh to learn and what do we do
when we when we you know read a book is is we want to learn something so uh so this is the book that that we're reading
the programmer's brain um and this this topic is near and dear to my heart because is uh when I went Independence again
to be a trainer seven some odd years ago uh I made a concerted effort to really do some research and figure out how do
how do people learn so I could try to make my courses and and coaching much better and you know dozens of books later
and hundreds of of case studies and research papers later I think I've got a pretty good uh grasp on it but there's
always there's always more to learn uh and I love sharing what what I learn and so it's interesting reading this book
because uh much but although not all the research that that she uh that the author references um I'm already either
familiar with or uh uh have actually you know read about and researched deeply um so with the book club uh We've
basically discussed through most of just chapter 2 so still early days um and so one of the things I like to say about
our our book club is it's never too late to join never too late to join um you can uh just drop right in uh join the
Discord let me know that you want to get in on on the book club you can get access to the previous recordings so you can
play those back and we generate transcripts for those uh and any chat messages or notes that people are taking are uh
available and so um even if you can't join every week or even if you can't join live uh you can still participate in the
discussions of the book um we uh chat about and set up threads for each chapter uh in the Discord to discuss what we
thought about what we learned about questions we have about that specific chapter and you'll find from me I'll be
posting a lot of hey here's an interesting paper hey here's an interesting paper uh you probably can't stop me from
posting uh lots and lots of different papers so I I do try to restrain myself so go ahead and and go to uh ted. deev
Discord that gives you the in information and invite link into the Discord if you're not already a member if you are
already a member uh and you're not in the book club uh then go ahead and send me a direct message and I'll add you to
the private book club Channel That's mainly so that I can sort of verify that you're a real person so the uh the other
thing the other announcement um uh is um my game uh I had a I had a video was great uh discussion with um Mark shed and
and talking through my predictive tdd process and the tdd game itself and doing a little bit of a walkthrough of the
game and uh you can catch that on YouTube I'll I'll provide a link for bit all right welcome Mike hey swegi yeah I think
I think I don't know when exactly my affiliate my twitch affiliate anniversary is or was um but apparent ly it's either
yesterday today or at least yesterday because that's when I first saw the the chat notice um but thanks for the cluest
like myself what does a twitch affiliate mean so uh when you start on streaming on Twitch you are I don't know what the
term for it is you're you're something um and you have to reach a certain number of hours and a certain number of
followers uh before you can reach affiliate where you start making uh very very very tight tiny bits of money um enough
for a few cups of coffee uh and so that's where I am the next level up is partner and that's extremely difficult to get
to um I doubt I will ever get to that uh because not enough people watch this kind of stuff and um there are some
channels so like coding Garden He he'll get you know two two to 300 people or other other more personality driven to a
certain extent uh folks who who will get a lot more um I guess you know the niche we're in of of java right right then
and there java narrows it down to like one 100th of of everybody else uh if I was doing you know more JavaScript or
typescript then then I'd get more viewers but so to get to partner you have to have a lot more hours and and and certain
number of subscribers consistently and uh you earn you earn uh a bit more money but that's okay we're quantity thanks
for stalling for me while I finish that phone call yep no worries all right so um let's check in off sounds good um let'
s see well let's run test to see if we have a uh if we left ourselves a breadcrumb I'm gonna do all just for all I think
we actually um it had you know ended on a good note has everything what we were working on working so I think there
should jira right so we got some parse eror columns deploy to production update the can kind configuration I almost said
kindai I know configuration URLs and then persist to DB yeah so some of these aren't sequential some can be done
independent yeah hey there Net's Vagabond vagabund um I don't have a strong opinion about what next um partially because
I'm still my brain's still processing yeah like I feel like I I we need some a at least a little bit of better uh error
messaging than than throwing an exception uh so I think I think we should um maybe we basically was that oh sorry I was
going to move it up to um be with the rest yeah of the related yeah so I think that's very much related to to 51 yeah
apparently the tabs get weird so when I indented yeah it's off by one figure that out later um you could do the multi
karat thing if you oh that's true but I don't know if it's the whole file or so what you can do is if you move the
cursor to line to the beginning of line 46 all the way at the the head yep um and you double I think this works on on
Windows to uh if you double tap and then key okay double tap control key double tap and then as so so on the second tap
hold continue to hold it down gotcha tap down uh you have to do the double tap quick enough otherwise it doesn't
recognize it so double so the so one two hold try again and you said control control key yeah no so you double tap and
hold and that double tap and then hold the third time or no hold the second time yeah that's what I'm doing tap and then
quickly tap there we go there you go wow that's that's going to be an interesting one to get the muscle yeah it's it's a
little it's a little hard to get the first time once you get it um and so now you can space then it inserts a space on
all those rows right right and then es Sublime I use that feature and Sublime quite a bit for some other stuff hey J us
welcome Hey Okay so we were so I think um I think 51 is sort of a subpart of 52 it so one of the things we'll want to do
is instead of throwing an exception we'll want to um I mean we we could throw an exception but I feel like validation
stuff is not really exceptional because who the heck knows what kind of uh things you're going to get so um basically
holding on uh so basically like it says instead of the parse method throwing an exception if we hold on to uh just sort
of generated error messages validation messages uh and then we can return that as uh what's called the result pattern so
net has has this result thing um I haven't seen it a lot in in the Java world I've seen some attempts at it but it it's
really interesting that the net World in I think in that way is is ahead of of Java's idiomatic of what what people are
doing so um we'll probably want to do that and so basically the pars should either return um and and more uh type
oriented functional languages they actually return in either uh Java doesn't really like it sort of can simulate that
but not quite the same thing and so basically the result would either return the success uh and and basically the the
the par information um or it would parse it and and and store it uh or it would return um basically one or more
validation error messages and so uh to a certain extent what's interesting is this violates command query separation
because parse is a command uh but it it it I think so the way I look at it is is it appears to violate it but it doesn't
because the information that it's returning if it if their validation error messages is not information about hey here
are the songs you parse right so parse parses them and then and then it gives you back you know parsed song objects like
that's actually not what it's doing what it's doing is it's basically um sort of out of band information it's not at all
related to the state of the object it's not revealing the state of the object it's basically saying you had some some
problems um you could uh if you really wanted to be perhaps pedantic about command query separation you could have the
object have a method saying you know sort of was the last part successful uh and if and if it wasn't then you'd say okay
give me the the the most recent validation error messages so return it like an object that is just a success or fail
kind of thing not even that right so if you really want to be pedantic the command doesn't return anything and then you
have to ask the object hey was that was that good was that okay uh and if not what happened um my sequel has that right
or at least the the one I've been I was playing with the other day where um you make your query and then you if you want
to know what happened from an error perspective actually no what a second no it does return it does return yeah false
right yeah is there something in Unix that that behaves like that I feel like I've seen that pattern before maybe it's
C++ where you don't even know whether there an errors happen but you have to query for it oh well yeah out so we could
do that I kind of think that that's overly that's pedantic to the point of like amas pedantic as as more so than than
lots of people um but you also have to balance it with with sort of ergonomics like is this easy to use is it possible
to ignore stuff um you could always return ignore return values but if you expect some kind of success or failure then
then then you should at least check that um and so I think uh I think the result pattern is reasonable um where you
basically have an expectation that quite often you're going to get validation errors because the the data is not great
and so um so I think we'll go we we'll go with that pattern and I think I described it incorrectly here so it's either
success or par info um so it you'll never return the parse info because I was kind of typing what I was hearing so I
think maybe so you either return Su success period end of story um because because it's a command and all we're saying
is did the command succeed yeah um otherwise you return that it failed and uh with with one or more some failed yeah
cool shall we so let's um so all the test passed right uh let's yes um so where are we going to do this validation then
we could then we would know where to write the test to start driving this well so where where do we do the parse is
really the question yeah good point um the other thing we want we we were going to discuss was sort of the design of the
song Searcher but I think we can um I think we can push that off until we get to the to the database stuff because I
think that's that's when it will become more obvious of what we need to what what we need to do if anything okay so
we'll put it right here after the database unit um so let's go to the song Searcher since it's probably oh I was gonna
go to um well actually we want to start at the parse method so let's just start there looks like it's yeah because in
there we do parse song and that's where thrown um which is the that require so that's our first validation is is do we
have nine columns ah there it is yeah so basically we have to Bubble Bubble Up all that information and so this is where
um in these cases or in this case we could leave the paron as throwing an exception uh and then catch the exception in
the parse method and change is in the par song we we don't throw an exception and instead we my space bar stopped
working for a second so it looks like yeah on the you now space bars have a width so if if I'm hitting on either of the
end it's not taking the space so I have to hit oh no dead center because I was like why am I not getting spaces I keep
putting them in intentional okay so we were saying catch the exception one approach was catch the exception here right
and then basically and then basically translate it into uh a result so the result object will be either a so we're GNA
basically mimic either and have it'll either return the result will contain a list of songs which parse is currently
taking right or um on success and then on failure it'll return um indication of failure and a list of the validation
errors right that we had right yep okay and you said that was one approach what was the second approach you were
thinking so the second approach is um not throw exceptions at all from our par song uh and I haven't feeling this one is
going to be where we really should be going is because right now parong only has one check does it have enough columns
uh but later on we're going to want to check that the columns have the right that you know they match up um so I think
uh that you know there's yagy but there's also well we actually do know we're we're going to need it at some point so
right it's not it's it's not yagy because this is a feature we know we're gonna have in really soon not like some
speculative thing like maybe we'll need that ASD yes early stream today so I think yeah so I think uh we'll we'll go
with with approach number two um so par song itself will return uh and what's interesting this is this is sort of the
the approach that languages like um uh goang do is they basically always every Method All or every function as they call
it everything always returns an error uh I think they went too far the other way because then you end up with a lot of
boilerplate of constantly checking errors um I don't think that's I I don't like it um but that's not going to change so
uh so for us then um what we'll want to do is since this is a private method um we have a bit of an interesting
standpoint so do we uh how do we how are we going to test drive this is basically the question could we make well my
initial thought and I haven't fully vetted it is what if par song was song so then it's public and it's testable but it
doesn't really make sense to it makes sense in some way to be on song because we're parsing a song but the data is not
going into song well actually well you you could say that it's a static method on song and so what pars and then
basically you say parse right that's one approach what's I like to think of multiple ones what else can we do I mean
it's already called tsv song parser so what have another class you know song parser parser I mean I I also wouldn't be
uh averse to to making this parong method public um because while it's used by the the overall parse it is there
actually is no State here uh and technically even though I wouldn't do it technically this method could be static um but
I agree with you like to avoid Statics unless we absolutely need them but yeah but there's nothing wrong with it being
public I mean it's a parser and so maybe you just want to parse a single song uh it's it it's not exposing an
implementation detail in the way in in the same way that other private methods might might do so um I I would not be
opposed to to making that public and if we do that then there's no change to the parse method above it right because it'
s the same you know we're not well I guess we'll change the signature oh that's GNA be interesting how is yes uh I just
yes so that might be a reason to do approach one um interesting or we have to change the way parse is written well so uh
it it depends on what we return so if we return something that's a result um what happens when you know basically what
is a result uh and we would yeah this and this is why like if you look at at the the implementations of of an either
class uh in Java it supports all the various streaming like things so for example um you know you can go you you
basically go down One path uh if it's successful and basically it's still a stream but you go down One path if it's
successful and one path if if it's a failure so actually that actually begs a new question if our goal is to collect
going back to jira is if our goal is to uh hold on to the once then this stream will have to have some way of collecting
and holding on to them as we go through yeah yeah interesting yeah so so we'd have to figure out what are we actually
collecting um are we so what object would we collect so we can't just collect strings so if parong returns a result then
we're just collecting those um and then we'd have to do some kind of I don't know maybe a flat map I'm I'm not sure but
if we return if par song is always returning a a result of song oh really it would be a result of of yeah maybe a result
of song of a single song Right of a single song so it's either a song or it's a me or it's a failure with with some some
some message uh then we would filter or we would do like an any match um and then I mean I don't think we could do this
all in one I mean we certainly could do anything but I don't think we want we'd probably want to do it in one stream
pipe line right I think we'd want to uh separately so basically collect into basically a I guess a list of results of
then and then do an any match if any of them report failure and if so then collect just the failures because if they or
or you could do an if no match and then return a success otherwise return a failure I think that's probably the the way
we'd want to go with something like this so we could still test we could other words this returns song result no well I
mean it returns something but it wouldn't be something yeah yeah I'm just trying to think of a name for um something
that isn't either right yeah so so the way it would be actually structured is a result class uh typed generically typed
for song ah okay be the same result song well this method wouldn't return that um oh it would return another result it
would return another results song because the the generic type would always be what does the successful thing look like
because we're we're assuming the failures are always going to be the same in the sense of they're always going to be
strings if we wanted to type the failure results then we'd have to put like you know comma or or something like that I'm
not sure I'm not sure we could do that I guess we could do that I mean I don't know if we need to separate them I mean
just a big spurt with some slash ends between each validation error probably sufficient yeah I mean we're yeah I think
it's sort of the same thing as if if they were all exception mes it it would just be that so the advantage of this is we
could we could test make this public test drive this part right and then test drive this part so that way we're not
right test driving something too big or having a smaller step yeah rather than that big step yeah so AST asks about uh
list of successfully parong analyst of failures I think the idea here is we unless it's either they're all parsed
success ful or you got to fix something and we're not going to do anything so what we what we we actually don't want to
import hey we've we've parsed 99 of the 100 and here's the 100 that's wrong and now you got to go fix up just that one
um so I think at least I think that's what we're saying I don't know if that's what we want um I think that's what we're
saying I think that's what we want because yeah who wants to go back to their spreadsheet and go okay what's the one
that was missing copy just that one fix it's like fix the spreadsheet yeah where yeah good question as what as ask about
boiler plate so apparently boiler plate comes from uh uh they were these roll roll steel that you were used to make
boilers to heat water and and uh you can go back to to look up the history it's pretty interesting um that sounds like a
plan uh is there anything we want to do to prepare for that or should we just start the only prepare that I can see at
the moment is just making this public but that's really minor all right um anything jumping out at you no and now let's
make a test so so still be under song parser test actually there is a trick to get to this without having to go T so
what it looks for when we do control shift T is it's not magic it's not like oh it knows exactly which test uh uh class
is testing against this what it does is it looks for classes that are called t tsv song parser something something test
um what do we call it uh we called it tab separated value song parser test and want to change that reason now I just
want to test it y love it and you should be able to go back and forth so if you go uh control shift T from here uh it
basically says which test subject do you want to go to and here it's looking for if you drop the word test from this
class what what object what classes can it finds that that are in there and so that's why it also brings up song because
there's song in the name in the name it's doing it from the name not from the content of the test yeah it doesn't look
at the content at all it's not it's not that smart yeah yeah that's sweet oh I forgot to switch test and well I don't
have the tab switcher so I can do it quick uh what you can do is you can you can unsplit and then we can resplit the
right way uh but that might be a little bit of I mean you could close basically all the other all the other tabs start
start over because we really just need these anymore yeah well um close other tabs from here I want to leave jir in so
I'll now we want what was it again that you prefer so test on the left code on the right because the test drives the
code right we're gonna go for vertical split yeah but we'll just do split split and move down so we want this one to
split and move down yes there we go sweet all right so we want to test somewhere we have does an error did we have one
that was checking for an exception because we're certainly throwing an exception I would hope we that is it this one
nope the quick list of all the uh oh alt F12 nope oh what is it maybe it's but sometimes command M command maps to alt
and sometimes it Maps control F12 yeah I just I just manually in my head mapped command F12 which is what it is on the
Mac to to alt and apparently that's not always a one to one yeah and rows with not enough columns parse multiple songs
so in a way we could probably the first one yeah how do we handle it now right oh we're looking for the exception right
right right yeah um so for this one we're obviously calling the public method uh or the previously public method of um
parse of parse of of uh a list of songs but um what about we just make a new test versus tweaking this one well this one
is gonna so this is interesting because this one is going to change because indirectly we're uh this will fail yeah so
if and previously we had I mean this it's kind of funny because if I remember correctly previously par song was public
and we said oh that's not good we shouldn't make that public um and so this test used to actually directly test against
par song so because uh but because there was no other reason to to have it public um we made it private and then
retargeted this test against the the parse multiple songs method so what I would say is we retarget this back y to to
the rep to the to the once again public method par song um and then we can start changing the behavior sounds good let
me do some refactoring first this is now going to song and we won't need this oh no we will need that um let we make
this Our Song now this will compile but it won't well actually this if we did pass uh except because what yeah it it oh
because we went from yes so because you have a yeah yeah so let's is there there's a way to uh convert this to I can
just do it manually there probably was a quick fix to uh say make it just a regular string yeah control shift J at least
would would help reduce the number of delete do run all right and I didn't say it out Mike so now we want this to are we
going to use the either class within Java to well we're going to create our we're gonna have to create our own create
our own okay um and so we're going to have to Define what what we want that to to parallel that we don't know what it's
called yet do we well I would I would say let's um R do that and assign it to a local and then delete the current
exception assert well yeah I think you're gonna have to you're you're gonna you're gonna need to get rid of all the
assert exception stuff because that's going to completely go away we'll keep the message because we're going to use that
control shift V work there no oh it's Control Alt huh I want see what that it no we don't need any of this uh we'll hold
on to the message because we'll use that true hey there I am white knife thank you welcome now right now it's called
song but we're G have to convert it to a name right and so gonna yeah I think we're just just going to have to to I mean
there's probably some some other ways to to do it but I think we can just start creating our our result class and build
it from there should we build from the yeah should have done a rename oops create class result y uh is it going to be a
class yes maybe oh we'll start we we'll start with a class destination all right uh and then let's change uh now if we
change the return type here um that's going to going to mess some things up so um oh right but since it's only called
luckily this method was private so the only place it's called from right is is there uh and we'll just need to do a one
more map to to fix it oh okay because I was gonna say I guess another approach or extract all this into a method have
parse called the extracted method we work on the new parse song In Parallel all the other tests keep passing except for
the one we're writing I don't I don't think we need to do that I think if we just I I I think I'd feel more comfortable
if if we continue parse to to be calling the real code and just handle the the new return type because I think it'll it'
ll be one more line of of code in the Stream oh right because we we'll map to par song which will return a result and
then we map um to actually get the the the result we'll assume it's successful got it okay so change return type for
this guy yeah so what I'd like you to do is is um in the test because we want to be compiling after you make this change
is now or just delete it actually yeah could have deleted it that here um and so let intellig make the the change to the
return value oh I uh it's that one right yeah so you see that that it does a preview there on the right oh you can see
what what what is it going to look like after and that's what we want it to look like yeah so of course that broke what
we expected um and then we can just do a map uh we'll still have to do something um because right now result doesn't
have the method we want uh so we can either we can either Define it here or we can Define it there so if you do so it's
not this because it'll be a colon um and so since we don't have the method yet we have to Define it yeah so what do um
songs oh no single song um or song no that I don't like that either why not just song what's wrong with that because we'
re not always returning a song well we're returning a song result oh right because it's it's um uh or is it a song at
this point we're doing that well but it has to be it has to be tight so it's so it would have to be something very
general uh and we could just say I mean we could say result or we could say value uh I guess value because just result
results seem tarpits I'm just looking up what what done fine so let's go ahead and Implement T yep and we can just
return null for now No Control Alt L yeah that's it alt L I'm doing the uh try it from try to retrieve it from memory
first and if it works great if it doesn't then look up sheet so now we compile we could run and but oh actually it's not
compiled ah because we're not returning a song yeah we're returning a result of song yeah yeah yeah so here what we want
to do is um we want now from a from a tdd perspective we could say whoa these changes are big maybe we should go and and
flesh out the result class um a bit more and and test drive that except I don't I don't think result class is going to
have much in the way of it uh sufficient complexity that I feel like we need to we need to test drive it so we'll just
uh push forward here so what we want to do is um we want the result method to have uh a static method called success so
instead of the return song at the bottom what we're going to do is we're going to return results Su success uh and then
pass in the song So result. success because it be a new method and so here we're going to have to get a a eventually we'
ll have to get a little Fancy with with our types um but for now uh what we want to do is we want to return I mean we
could run this and and watch it fail at least it will uh it should compile at this point but it will certainly fail a
whole bunch of things because now we've broken all the yeah foring but that's fine we're getting nter exception so that'
s an expected failure um and so we want our our our static method to do is for now we'll we'll basically treat this
right as sort of a small step we'll treat this as uh just a container of uh of of a song and so we'll just um no no I
was using the word container as the general thing gotcha not as a class name uh so what do we want to do when when
somebody calls success what do we want from result at that point just the song well actually no the yeah the song itself
well no because what's the return type oh result of song right so what do okay now the type is inferred do we have a
Constructor yet or if I do this right that'll that'll Force us to create a Constructor and think that the y um since we'
re already calling these things values so whenever we use T we should use value so instead of song There on line seven
that should be that value and obviously result will need to hold on to that there is a quick create field for parameter
value yeah good I hate that it always seems to like you end up with a blank light in the Constructor no matter what you
do what do that put that are you a fan of this blank line here you Che this one out um I I leave all right so we've got
our value we're we're saving it um this should still fail because we're always returning null for our value but then if
we assign our return the field were there we go um so you were saying sorry you deleted a blank line at seven and a half
so if you could put it back yeah yep oh I ran the test about predicting I said it was it was gonna it was gonna pass
yeah okay everything except for the one we're working on well yes except for the test now that that we are now changing
the behavior right uh we're still throwing the except uh but we're not we're we're we're not asserting anything so what
we want now um since basically all of our other code is working with uh with the result because we've we've pulled out
the result intermediary holder um in our in our when we were doing the stream so that's so everything else is working as
as as it was before and now we're back to the test failing for here and now we can write our assert from what we for
want yes Aster there are places where we have song and we want te um and we'll let our tests tell us that um I like to
be very lazy when I'm when I'm test driving as as as you know uh as as they as I say in my my game least effort uh get
the minimum amount done to get to back to to to where you want and then let the test drive uh drive out future future
Behavior because honestly we could have done not even te at all we could have just done result song and then you know
that might have even been a little bit of a premature uh uh flexibility um but we did it because it yeah so we we sort
of sort of basically intellig offered to to make it t and so we just followed intell's lead instead of making it
strictly song um we could go back and just make it all song and then convert it to a t later that might be an option
what do you think well since we're Midway typing assert we finish the assert and then go sure so what we expect from
this from the assert we want the message well we want something that doesn't exist but an error message right or a
validation message um so this would be before we even get to that we would do something it well we had success so then
it would be what error text so I think I think we want to ask it a question first because before we can pull out whether
it's the error text or the actual song we need to ask it which which one is it because right now we have a result uh it'
s it's success it's Schrodinger's result we haven't looked yet to see if success that's to to build it it's to build it
but it's not to check it yeah and success would not be a a great way to phrase the question right right um so that yeah
I I just I usually stick is in front of it if if I want to make it clear that that it's a question so right success and
so that'll be a method that create oh now again field for this or just if there is least least effort code that's
creating a Field's too hard that's too much work yeah yeah good point true so um and we want to return something that is
going to make the test fail right so we're going to say is success is never false uh oh actually you were right if you
wanted to do true I forgot we're we're we're actually testing failure um right so uh so we actually do want that to be
true and here we want to say that it's false because we're expecting an error yeah and then we'll we get that and then
we'll then we'll implement the error message right sort of the high level next steps okay so if we do this uh since we
hardcoded false we should oh we hard coded true we get a failing test H it's GNA fail because we're still throwing the
exception oh I didn't get specific enough of my prediction you were very no you were absolutely specific but you you as
as happened you forgot that we were still throwing the exception good point got to we never got to the assertion right
which is good right you predicted but your prediction the test failed but failed for a different reason reason and then
you go why did it fail for a different reason right now let's go back and look at the production code and for those of
you who want to know a little bit more of about what we're talking about uh here's the video for uh where I talk about
predictive tdd and why that prediction is so important is that the the the tdd game thing from the other day yep sweet
yeah was a good talk AST so at this point oh sorry you have a question I was gonna say so what what what's so what
what's the good Next Step well we want to think of what's the have well the quickest quickest would then break all the
other tests um change what we returned to be a hardcoded version of failure I guess an easier one would be this doesn't
throw an exception anymore it returns failure so what if yeah uh scroll up the bottom a bit yeah so what if we WRA line
catch Ah that's a good idea really you don't's insert yeah it won't know to do it so you You' if anything you'd want to
do a surround around nope how's the automated surround work I forgot um don't know what it is uh so if you is uh it's
control J control J okay actually I'm going to do it without selecting the whole line see if it that's interesting
that's Control Alt J you don't um you don't want surround with live template you actually want control alt T So controlj
surrounds with a live template but we actually want to T we want to surround it with a tri catch six and what we want to
do is we want to catch the runtime the specific exception thrown and so now we want to return a result that that's
actually a failure what do we call it are we didn't give it a name we didn't get we we we haven't done anything with
failure yet right so would we do parallel like return fail with message yeah so I might either do failure instead of
fail um or or error um both are both are both are fine uh I kind of like failure better but yeah what do you what do you
think originally I wrote was thinking that because it's kind of the opposite of success um the thing about error is it
reads result error message so like as in here's the message but um but at this point this is our own API yeah I'm I
could go either way I think I'm leaning towards failure but all right well let's play with failure and then see see how
that goes we're always playing with failure that's right right two so uh what I would say is is um let's not pass the
message just yet because we don't have a test for that great uh we're not asserting we're just asserting a success is
false and so now y you don't need to put anything in there Constructor yeah I knew that yeah I knew this was empty I was
thinking about what we pass I mean for now we can pass null because nobody's checking the value uh on on failure and one
has to spell returned correctly yeah finicky compiler while we're here song so if we select all the if you uh nope now I
got to look up my list expand code selection no ad selections Alt J I was close I was doing control J yeah that's good
that that means you're you're you're you're you're strengthening so The The J part of the thing was actually stronger
than the than the meta Keys which is not surprising and one more now we got all of them okay so now we can paste I think
it's in my paste buffer we'll find out yeah cool and don't forget to hit Escape otherwise you'll you'll really that's
unhappy static here caller uh what What's the message it's saying it's says uh make failure not static no that's a
suggestion what is the actual error oh uh so run the compiler because um intell won't always give you messages nonstatic
cannot be referenced from a static context so we're in a object not is that because this is not static here on line
seven no it's because um when we went uh so now it actually thinks that that song is is uh a generic type and so it's
actually now bit a bit confused um so if if we if we want to not basically we're saying we don't need to generif this
yet because it's always returning the same thing so we want to do is basically remove all the generic types information
so it's just result way that's all of them right yep yep and then you'll have to delete the I don't know what else the
Diamonds oh done that one the same way be careful you you're in multi multi carat mode so you want to make sure to uh
remember to escape out before you do anything else yeah all right I need to this that's all now welcome good uh except
in in one place which is uh the return value from par song in the bottom pane so I knew that because the tab has a red
underline and so if you just click into the and hit F2 that'll take you right to the error ah yep now we run test and we
think we should compile we're doing this to the compile check oh hey Cataline thank you so much for the for the cheer
appreciate that welcome uh we still got some something that not seeing red anywhere else I'll again good we're back to
now well not back to this is the first time it's failed the way we wanted it to no good point so now it fails the way we
want to pass well the easiest way to make it past is just to say return true but I don't want to do that we want to say
uh sure you do but to make it pass you want it to return false why would you want to work harder than just returning
false good point good point see even that was hard because you didn't have a man there we go so and and this is I I I
you know I a good point in my talk but also like it's possible that there's some path through the code that where this
doesn't work right the whole point of the result thing is is right now it's it's literally just a container for value
all it does is hold value and return false for for Success so the only so it's not doing very much but it's certainly
possible that returning fals could have broken something unexpectedly um whereas promoting it to something more complex
means we'd uh we'd not know is it is it the more complex code we just did or is it the you know is it that it's
returning false now and that's affecting other things and so by taking these really small steps it make it really
obvious happening so I think since all our tests idea how was that I should have said it out loud what I was saying but
start moving towards parong returning um a result so we can return collected pars eror or something like that I feel
like that's a bad sentence what is this thing here um what I usually do is I I put a a break before that because
otherwise it's hard to read oh you you manly put in a break like this yeah this little is always there it's it's always
there um it's just really annoying um because it annoying yeah the only thing that I change is result to be an uppercase
class me uh so full um so right now what we're focusing on with with the bulk import is right now uh as soon as it hits
a line in the bulk import that has not enough columns because that's currently the only thing we're validating uh it
throws an exception and basically the entire application blows up and we don't want that so what we're currently doing
is is making it so that we return something other than exception we could have caught the exception ception but that
means it'll not process all the items it'll pro it'll process until it hits the first invalid one what we want to do is
collect all validation problems so that we can return all those results and so the user can fix them all at once um not
sure what kind of optimizations you're you're asking about though so feel free to elaborate uh do you want to take a a
quick break here would be a good idea actually okay all right so we'll take a quick break and when we come back we'll uh
start expanding on the result um getting towards uh checking for for the different aspects and then uh at some point we'
ll need to generif it so it can hold both a song and a list of songs uh so that we can start start few okay back yeah so
we kind of um set us down that path because we we pre generified the type uh which um led us down the road of of yagy
yeah um that's an interesting idea uh I welcome our community to to do that because that's a that's work that I don't
necessarily we don't necessarily have time for um but that is that's a good idea can they put it in like are there like
notes for the twitch that can be or the recording of the stream that can be added recording of the stream uh uh I do go
back and update a little bit of the YouTube um uh to add a little bit of of what we did um but I don't always do it and
I don't and I'm not always uh very specific um but if you want to leave comments I'll I'll certainly accept um let's uh
where were we were the test was the test the test was passing but I'm gonna again just to double check yep memory right
12 not 10 so we could right now it's hardcoded to yes I'd say we we finish out the message and then we can move on to uh
actually recognizing that at the at the um or having a test that where it is successful and we actually get the song but
let's sort of f finish out the failure branch and then we can go to the success Branch we have to have a new assert for
checking the message then yes we don't have it yet that we would call it message or error message here are you looking
to see what other result objects use yeah um I think message would be unclear that it's the error message error message
yeah that was my thought um and so uh since we called the the since we have the static method failure which creates a
failure um I think we can either have a method that is message I feel like we we don't I don't I mean looking at other
implementations is is is helpful but but they also may have stuff that we actually don't need um so I think failure
message is probably better what do you think yeah it's pretty clear that it's that now here's a message versus failure I
might expect it to be a Boolean um even though is failur is already there like if you were scanning the code quickly or
is failure message is screamingly clear yeah and there there may be some future state where we don't want to return a
string for failure for the failures that we actually want to return some class that holds some some other information
but I don't know when or if we'll even hit that so I think this is probably good enough for now okay let's implement
this sucker oh we want to be a method though yeah so stupendous follow asks uh having a separate repository for every
adapter different adapters need different entity columns right but I don't see why you'd have that in a different
repository that seems really painful so what uh what's your goal in having a different repository so why would you think
that's useful because I think the whole point of ports an adapter is one of the benefits is that uh your adapters are in
the same repository and therefore as you refactor things they get they get updated um putting an adapter in a separate
repository means it's going to be far too easy to break things so for me I I don't I can't think of any situation where
you'd want an adapter in a in a separate repository but maybe there's something you're thinking of all right well our
failure message is Boolean oh wait a second no I needed to uh change signature because the calling side F6 shift F6 what
do you try to do oh change the signature um no you weren't finished creating the method so you could have you could have
there was no there's no need to do that so undo a few steps yep yeah so go back to create the meth far no I did I was
right okay cre method so right now rectangle around Jan that means it's waiting for you to type in it guess guessed
wrong and that's okay ah okay you meant repository pattern uh yeah why not have a different uh data repository uh
aggregate repository or just a read model repository for each adapter sure that's totally reasonable sorry I
misunderstood but repository is specific um did is this too big of a step well you're you're gonna make a pass we haven'
t seen it fail right right so take cut that message and and put it in the test yeah uh is it let's see is equal to yeah
lowercase empty we think this will fail and it'll fail based on so we know it'll fail or yeah that's our prediction we
predict that will fail and spe specifically it'll be because we're going to get an empty string instead of this longer
string test let me rerun all all IO free there we go yep y fails is expected great oh that's why ah I see what I'm doing
I've somehow reverted back to instead of doing control shift F12 to close all windows hide all windows I did yeah
because F10 is useful but does something very different yeah totally okay so it fails as expected so want this to so the
next quickest way to get to Green is to well we are at Green sorry oh yeah yeah yeah yeah are we yeah we're oh right s
sorry we're red yeah see that Sor I was gonna I was I was gonna uh not have you take a a small step here ah I don't I
don't I don't think it's worth it sorry in my brain I was I was I was meaning let's not bother just returning a
hardcoded string because that's not very interesting um I mean we could do that and then do the rest of Factor so it so
now should pass yeah and you've got pns you don't yeah actually does it have a um hey you don't need these pins uh if
you've got too many PRS right closing yeah sweet good to know for next time yep yeah as I misspoke I thought we would we
would already done the step yeah uh so let's um I don't personally feel the need to to do sort of more more test around
this returning we need to populate the message we what does result have again F12 failure message so we have no way to
write the failure message yet or to tell the result object what the failure message is right and that would be part of
the uh I would say that's part of the static failure message uh static failure expect string well I would I would I
would take a smaller step uh I would take a step that that forces us to change this from the from still Ser from the
client side um so in our code let's inline the that and keep or replace no it's we're it um and then what we can do is
we can instead of throwing the exception with that message we can just uh return failure with that message basically no
I'm REM so not throw the me throw the exception just do a return of this no I was no okay I was going to delete all the
yes but you're deleting the if statement we need we want the if block ah because that's the thing that's checking right
right right right right so so replace the throw new not enough columns with result failure right got it failure so you
want to return result yeah and now uh it doesn't expect a string so now it's right so now we can string refactor and now
we can get rid of the tri catch part because we're not throwing an exception anymore is there a quick fix on so now if
we run the test it should still pass because a hardcoded string we're no longer throwing the exception we're not but we
haven't broken anything because of that so that was a a step towards now the next step was we'd like that message to be
real go so that means we need to take this string we'll just call it um failure message I think we can just call it
message okay because it's in the context of the failure method so now set so remember we're in a static method so we
can't I know we can't do an instance variable well what Constructor would we like result to have that that would make
this pass oh one that takes a it now let's create a new Constructor right yes yes and so there I think we'd call message
yep and then you can have intellig create the field and now because both of those are final we need to set other uh we
need to set them uh or we could just make them not final um I understand that making a not final part what is the
setting other values that you were thinking of Oh you mean oh I see so set the opposite when it's not used to something
I don't I don't think I I don't I I actually would say the easier thing to do is remove the final yeah because there's
some other changes we're gonna probably want to make can we delete that blank line from The Constructor yeah oh I did it
again yeah because what happens is when we created The Constructor it starts off with a blank line and then it actually
doesn't get rid of it which I guess it shouldn't so if we run our test it still will pass although we're still not using
the in and now if we actually use the the failure message that was passed then it right and now it should pass should
remain passing yeah yeah continue passing y cool and if we want to see and make sure that the code that we just uh
basically did actually affect our test what we can do is in in the bottom on line 31 uh just sticking like an X in front
of number and then it should fail because desired and that's the way it fails sweet so that's another use of of
prediction when when I want to verify like if if I've never seen a test fail even though that one we saw fail but if I
want to really make sure um I will force a failure uh and then I'll then I basically do a predict on okay if I change it
in this way I expect it to fail in this way uh and that confirms all right let's commit sounds good let's get rid of
some of these comments first I don't think we need this anymore right yeah yeah any other crft I guess we'll find out if
to commit do a quick actually double quick now works the way we want it yep ah do we want to refactor back into a test
and this is sort of the the annoying part the return in the if test yeah this is sort of the annoying part of um doing
the result versus exceptions exceptions as guard guard Clauses that throw exceptions are very easy to refactor out um
guard CLA is as returning result is a little bit more uh uh difficult yeah I mean I guess we could that we could make
this into a method so but yeah so there's there's um what we really want is extract it to a method that returns a result
of its own like a result Factory uh not a result Factory it'll be a method that will actually execute this and then just
return result success and so what we'll get if as we start adding on validations is sort of this this series of we get a
bunch of results back and uh we can then sort of collect those and if if any anything fails there then we have we can H
so that sounds like a refractor we want to just do when we start having multiple yeah I don't I don't think we want to
do it now I mean we could call a method saying you know uh check column um but we'd still have to to to test to see if
the result is a success dot so that doesn't really help us uh it might pull that move the message stuff and move some of
the crft out but I don't okay that okay what do you think uh I don't think that was did so what we did was uh result now
has has a failure message and we converted the exception to returning a result with message stuff that is so freaking
wordy so what I might say is um par song returns a result a failure result instead of throwing an exception because I
think that's really the key part yeah that's better returns a a failure result with a exception so asra the the it's not
a create Constructor template problem it's a when it does the bind or create field and assignment um it basically adds a
new line and I don't I don't think it's so much its fault other than um it would be nice if if as part of what it did it
cleaned up blank lines um I think it's just the way it is I don't think there's any way to fix that there might be some
way but I don't I don't I I it's going to insert a new line no matter what right so we now are we now got it so one we
have one error for one song but we haven't built a test for actually the name of this test is wrong handles Row one row
yes and I think we can say uh returns failure result for row uh with not enough columns instead of handles um I don't
think we need to say one and I think we can just say with instead of four yeah yeah that works better yeah I was trying
to not do the WID with that's why right that's what I yeah so we do have we are do have a hard stop today unfortunately
um so should we maybe create the failing test for the next part which is because this is testing pars song should we now
go up a parse to be able to deal with multiple would that be a next step um or is that too big Next Step well I'm trying
to think of for for failure on a single row uh we don't have and maybe this is this is yeah I think that is the next
step is basically results uh and we can start with with handling the failure or no maybe the success will be will be
good enough that we just want to return that sorry I didn't catch your last thought I was busy trying to get the the
list of tests we already have so we don't currently have a test uh so there there are two directions we can go we can go
we just want to now return a result object instead of a list of song that's One Direction and then if that's just a
refactoring of types uh but not changing any behavior um the the other is a list of uh giving it a couple of rows where
there are one or more errors and so where it would return a failure uh because right now if one of those rows doesn't
parse we actually ignore the failure right so I think that's the more important thing is to have a failing test there
because we have basically broken uh the failure handling right because our tests are other failure them multiple songs
so in a sense we we kind of when we did the retarget we shouldn't have done a retarget we should have left that test
alone disabled it uh and then um brought it back at this point because now it's broken so I would say the test we want
to write is multiple uh basically calling the parse method with that error uh and we expect it to well that's the thing
is what do we expect it to do um I think I think expecting it to throw an exception might be a good intermediate step so
that we to having to return a result should we go and steal that test and bring it back from yeah let's do that do you
know how to do that not necessarily no okay uh so what we can do is we can you can we can either look at the git history
that's probably in this case the most straightforward uh you can also look at the git history for a certain selection um
so if you if so that's so searching for GE history for specific selection is useful for if you know approximately where
in the code uh that was we think it's somewhere um if you just rightclick in the code where you think the stuff was you
can go to uh you can either look at the local history but G history is going to be more reliable you can just say show
history for uh for method and it may not know because we changed the method names but maybe it does so if you go to the
last test so that's useful if you know kind of oh I think the code was somewhere here um and then it'll show you
basically history for for that that area of the of the code if not then you just go back to wrong uh yeah why is it not
recognizing it Well you certainly don't want to create the method yeah um sometimes intellig gets a little lost uh so
what I find is is if you try to run the tests ah that'll force it to it'll get a compile error but then now it'll it'll
start suggesting it yep yep I find that when you paste like a bulk of code it it feels like it doesn't fully scan the
code for in some way where it doesn't track that oh I just import right because we removed the exception so this is the
expected right as it is right now we need to change this test to our new expectation well we don't have a we can't have
a new expectation till we change the return value but I think getting this test to pass um and then treating the
changing the return value to a refactor uh would would be um the way we'd go so we change this we get this to to pass
and then we could uh in fact we might even want to call an uh sort of do a parallel change create a new method that
returns par yeah instead of parse something like parse with result um and then we can uh then we can maybe inline at
some future point so the actually would be a new assert right not an exception isn't that right so be insert that this I
don't know contains or whatever um yeah I'd really get this method actually I guess the contains would help Drive the
method creation as to what the return type would be right uh what do we want that to return that's going to return a
result object um and then we can say that the so that I always recommend do not wait for intelligate to autocomplete
inside of and assert that because it's it's always slow yeah so uh and here we want is false so something like that then
we could blow this away and then implement or at least start to given the time we can create the method so now it
compiles but it won't succeed right and actually we don't like the name of this would be just songs uh well it's still
tsv songs because it's still coming in as ah it was tsv 2 songs yeah we don't yeah not to we get rid the new the number
and we're good and then for now return null which will give us a failing correctly yeah so I I might even go so uh and
this is where we'll have to leave it as something that we'll need to um uh change its type but not necessarily um so
you're saying failure with a particular message failure and then basically pass along that to uh no I think actually we
so I think where I was originally heading uh is we wanted to extract the actual oh results extract the method on the
current parse method into parse with result that's that's actually what I wanted got it well given the time what kind of
breadcrumb should we leave ourselves uh we'll put a semicolon at top uh and then I think just leave ourselves a comment
on on the 57 at the bottom that this method 57 at the bottom second uh just erase what's there and comment uh extract no
because what we want is we want to extract this extract code from pars that result yeah and so next time we'll extract
method we'll get um a result it won't quite be of the right type and that that should Cascade Force us to to to make
changes sounds good yeah sorry I had to have a hard stop for today but y such is the way y all right thanks folks for
for tuning in thanks for your comments and questions as always appreciated uh and um stay tuned for uh our our next
stream um best place to find that out is by joining the Discord and uh we'll announce when we're going to schedule our
next stream probably will not be until next week so uh if we don't see you before the weekend have a great weekend and
see you next everyone
