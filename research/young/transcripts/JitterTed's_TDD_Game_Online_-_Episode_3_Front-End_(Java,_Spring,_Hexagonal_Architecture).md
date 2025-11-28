# JitterTed's TDD Game： Online - Episode 3： ＂Front-End＂ (Java, Spring, Hexagonal Architecture)

**Video URL:** https://www.youtube.com/watch?v=cBJ2tchRKh0

---

## Transcript

all right hello folks and welcome to another episode of uh working on getting uh my tdd game online um let me see here
so let's go take a look at play um so uh this is actually uh a new mockup I'm making yes that's for you ASD blew the
surprise oh well um this is uh uh a mockup I'm working on in in figma um to try and figure out uh what what the layout
is going to going to look like um this was my other mockup here um and again sort of I'm I'm trying to figure out how to
uh how to fit things in um it's really interesting because there's a strong strong sense of want the board in the center
and players around the edge which is sort of typical for a lot of these online games uh online versions of uh but I'm
finding I may have to to to shift that because the play area and and my hand is just too large to to to put this at the
that uh I just stopped talking to to no so uh so let's see so that's sort of the mockup stuff um we're not anywhere
close actually well we're not really uh ready yet for the game the other thing I want to be able to uh like one of so
one of sort of the architectural principles so let's let's go switch over here um sort of one of uh sort of underneath
to I I just know that once I get sort of an initial version up and running um I'm going to want the layout to change
because I'm going to get feedback from people and they're going to say oh this was unexpected over here or this was hard
to read or it was annoyed to have to drag and drop over this and and and things like that um so I I do want to have Yeah
so basically I want I want I want to figure out a way that that if I decide to move things around it's not going to
require a lot of rework hey there Jonas welcome I don't think that's going to be too big of an issue because each one of
these things here on on the screen this is this will be basically an image so this one's not going to be hard um well I
take that back uh at some point I'm going to have to figure out like where you are um I probably will not use this image
I will actually probably use uh this image because this is a bit easier for me to control this is actually um svgs um
but things like you know highlighting where you are uh where the other players are um yeah so there's there's a whole
bunch of of UI stuff that that we'll have to figure out but where we left off last time um was uh basically just just
starting to to test drive it and we'll scavenge from from the previous uh previous code as as as needed um so we got to
the point let's tests um oh no I didn't see the pull request that's weird uh how could I not H I'm just I'm actually
looking at my email to see why didn't I get an email notification of a of a pull request that's weird uh all right well
I'll figure out why my email isn't isn't showing that that's why if I didn't look at it GitHub boy there a lot of PL
requests I bet most of them are the automated stuff um so let's this I got to say one thing that that so annoys me about
sites that are showing something about when something happened like this committed yesterday well when yesterday like
and like it really drives me crazy especially when it's like last week or a few days ago or earlier today like don't
give me like some people may like that I really you know there's many kinds of people in the world um some people like
that kind of General ambiguous kind of thing I like Precision that um I have a feeling that um Gmail has learned the
wrong lesson from some of my GitHub interactions my GitHub email interactions and so I expect that it is not putting
them in my inbox uh like it should um let let me do requests um actually hold on uh what I'm going to do first is
basically for all of these them because we did a whole bunch of updates the other day uh and basically all of these are
irrelevant because we're not most of these are in front end as you know as you can see um so uh we don't care um and
this one we can close as so ah so yes there's a hover except this is another annoying thing like how would you know that
that's hoverable um and apple I feel like is one of the ones that that started this terrible idea of like I understand
like you don't want to you know under line everything and and and bold everything on the other hand discoverability
affordances is one of the most fundamental principles of good user interface design affordances how do I know what to do
if you don't give me a for and Apple's gone gone off the deep end with this they they've become terrible like that I
I've lost all respect for for them in terms of human computer interaction because they've just they've Dro they've
they've lost their way um anyway so let's see uh so 6:30 6:40 my time just want to check my email for when that was oh
look well now I got a whole bunch of you've closed all these delete um yeah no it didn't get in my email it probably got
filtered out all right I will check that later anyway yes there are times I want to play a game and there's times I want
to done uh okay there it is see another discoverability thing it's like I'm used to there being a refresh button in the
toolbar um but there isn't you have to know to rightclick and refresh list all right uh so let's go ahead and wait this
is is this the that's not the pull request though let's see um why did this look different to me yesterday because now
the the join game is is up here maybe I fix um did this change cuz now now I'm confused okay so this is this is the same
uh but it's not pulling in again I don't do pull I haven't done pull requests using this UI in a while ah okay so I had
to check it out as as a reviewer now it's now it's uh now it's yeah this is this is much better you were able to sort of
get the the the clockwise cycle which is great uh so how do I feel about the end points um I don't feel strongly so I'll
keep them um so yeah so this is it's too bad this there's no way to like quickly easily do a uh a visual a visual diff
um but no I think this is this is much better so let's see so join the game what should it do your only choice to to
discard your only choice to discard uh here you can add three to cycle risk right code feature the only play way to get
out of that so my guess is that adding the end points made it easier to manipulate the um the larger things because you'
re not depending on you're not having a single ones and so here we've got the two cycle risk that's weird this uh this
label is sort placed um no that wasn't the problem yeah all right uh but who knows all right well I'll take it as is
that looks good yeah I imagine like I mean there's a certain amount uh that state machines are the layout doesn't
represent anything other than these are just the states um but the ility to make it look like this so it actually
reflects the underlying layout of the game is is awesome all right so let's uh let's go ahead and go back to our pull
request um we'll approve go back where is the zoom out there it is okay and we look yep that all looks good so um yeah
so so what I did was uh I was on you basically the fork of your commit I did a merge which told GitHub to do the merge
um basically closing the pull request doing the merge uh and then I had to do an update to get so it was not a local
merge it was basically push it up to GitHub say yes merge this pull request and then basically drag it back down so well
done everyone um except for me who's who's quite a bit Rusty in uh so the pull request is gone uh and it's been merged
and we can see that uh here in the excellent all right um so let's go and close that what I know I'm going yeah so yeah
I'm GNA have to probably uh uh what I'm going to is I'm going to not print it out although I actually might print it out
um but I'll certainly I'm going to export it to to a diagram so I can get it sized full screen uh because we're going to
be referring to that thing a lot all right so let's see where we left off um um we were working on uh did I run the
tests I forget if I actually I'm funny this way it's like I like to see all the green check marks for all tests some
people turn that off and I only you only want to see the the red stuff but I like seeing all the green checks
constraints uh a person can't join the same game twice um because if you join a game that you are already part of it's
considered a so let's do that uh I think I said I wanted this four player uh maximum per game constraint uh so we'll
we'll do that one uh it's funny you say that astd um that's exactly the way I think of it uh um it might have been I
don't I don't have a picture of it I'll have to see if I can dig it up uh one of my very very early prototypes was
basically done on on a a a basically a pad of whiteboard paper so you could you know do things and and and erase was
brainstorming play testing with with with with someone and I think that that exact thing came up like here's how how you
exit what magic spell do you have to uh encant to to to get out of here yeah yeah or Keys yeah I think we were using
magic spells um and the the risk was was basically hit points like oh you've received damage uh hope you recover um yeah
so that that's a that's that's it's a great way to think about it all um of a person cannot join the same game rejoin so
what do we want here we want um machine um although it's it might not be wor worthy of a state machine is is the the
player themselves has certainly has State um but that's why I'm thinking like Central uh what do you call it decider
that receives the commands um uh and then then changes the state of of the player know but the choice but the choices
that are available very much come from uh from the state of from where they are in in the state machine so I kind of
think of of it like like we're saying like uh the player is is in one of these states and this is how this is your
choices and this is what you can do any I mean and and that's also like hyper media uh because at any point that yeah
exactly the the the the room you're in the state you're in you know exactly what your what your options are because it's
a combination of both what you need to do to exit the room as it were um but also what cards you have available uh so
let's go here let's go here uh well allow me to paste this in here no uh can I paste as I can copy ined upload media um
well I was hoping I was hoping that second what it's using up all my CPU I don't do is just save it as an SVG file
because I do want it to be like not lose resolution so let's uh oh it won't give me an option to save it as an SVG
that's a bummer all right I'm not going to worry about it let's go pictures oh actually you know what I in feel like I'
ve not looking up today here okay and then I can go uh do media uh ideal projects tdd yeah so the downside of a PNG is
is it is is it's not transparent and scales differently enough I might have I might go into a tool and and have it uh
and create the SVG because the the nice thing also about the SVG is I want to make the the text a bit larger in in
relation to sort model yeah I'll I'll play with the SVG stuff later yeah um I am very happy with the way it turned out
too all right so uh person joins is rejoin when already player when all R player in game all right so let's uh let's
minimize game uh so um this is part of the setup so they've already joined we already got them as a player and we're
saying that uh when we do player Joins this is the join again player um what are we saying we're player I forget do we
have a proper we here um is this going to pass no because it does not look to see if they're already in there right we
just we just created we just basically create a new player no matter what so this will fail because the IDS will be
different for each player right all right so that fails is expected uh simplest thing that could possibly work is um oh
look we're going to have to linearly search through the players that seems bad um but hey we'll do the simplest thing
players any I guess it doesn't matter fine first makes makes more sense so fine uh but first we got to filter uh player
the players person ID right uh and now we want we'll just do a get and then we'll return that um no uh we want to not
say get we um so this needs to create a player and let's do it as a loop because I'm sure there's a a nicer way to do it
with a stream with this other stuff um but right now I'm trying to do the simplest thing that that will possibly work um
basically look through the players right linear search to see is there one with ID matching if there is we return it if
not then we go and create a new one so I think this should pass and it inell yeah it's not going to make any suggestions
um clearly if I'm going to be doing this kind of search a lot uh I'm going to want um I'm probably going to want a map
list the map to the map is going to be then here uh you can play with six players I think for the online version mostly
about screen real estate but I also feel like it's much harder to to play games remotely and so if you have if if they'
re more than four people I I feel like even four people is is I feel like four people is about the maximum I'd want to
have in a remote online game um just because of the back and forth um you're missing body language you're it's harder to
interrupt it's harder for people to speak over people um so I feel like six six is too many I mean it'll it'll just be a
number um but I'm going to initially limit it to four yeah it's not about performance though right I mean obviously yes
even if I had 10 20 honestly even 100 it probably would make no discernable intent and I think the code will be simple
simpler right so here it's not a performance trade-off it's it's a a readability train tradeoff um so if we convert this
to a map then um what does that look like uh that's that so basically say person um what is person ID are we going to
are we at the edge of oops of creating an ID class yeah so that's a long uh the longer we wait no pun intended the
longer we wait to convert this uh although this conversion is is relatively straightforward uh so we'll go we'll go a
little bit longer and and so we're going to basically make this backwards compatible so instead of returning players uh
we're not going to modify that yet here map uh first uh player person ID to player anything uh but now if we say instead
of players we say player map uh list that should be the is uh and then we can replace this now um so now we should be
able to delete this ad that should still work because we're not looking at that anymore oh nope I broke it because the
loop right so let's fix the loop so now we've got a failing test um to to sort of guide us on what we need to change and
so this is uh if player map uh contains key of player of person minute right person ID right and here's another reason
why using long is is is is not good anymore is because uh the map would allow me to store any kind of ID right this
doesn't say whose ID is this it's not player's ID it's actually person ID uh all right next step is we're going to we're
going to do that refactor um so if it contains modifications all right so now we're back to passing I think this should
be final uh so let's go do a commit we haven't done a commit in a while somebody please remind me to do commits more
often because I have a bad habit of not doing commits what's my unversioned I'm pressing the wrong keystroke that's so
what we want to do instead is um player absent uh and so what we want is the key oh I said I was going to change the key
all right let me do this and then I'll change the key uh so it's person ID uh and then this is um a mapping function so
the mapping this uh oh person is overloaded uh so we'll what is the type of what is this map's this Maps Bel to a is is
it on oh it's two inputs that's why I was like what right so it's not a a a multi- input function uh the player return
took me longer to write return than anything else so I think that's it right hey reduced we just reduced what was
basically I don't know 10 lines of code to what's essentially one line of code much nicer uh the benefit of of of our
map right so again the um who cares about performance this is is way better right so we look up the player uh if they're
already there otherwise we go and create a new one and we could even function uh uh what would this be uh static we
should be paid by the number of lines we delete and with preserving the functionality all right so all of our tests pass
go um I don't think I want to I think I that comment was probably more than I uh okay so um I don't really know that
that was needed I think it's just as clear this way um the be uh so the next step is I I I need to to change this long
uh so let's go to player is it player person let's go to person um it's not a type migration I guess though so what does
that look like if I extract a delegate uh and I call it person ID it's funny I never use the preview cuz I I I always
whenever I do it I'm anyway right so what we're going to do here ID wait person ID doesn't take a parameter say what
record I don't know why that's a problem like I've got a getter unless there's somebody relying on that the factor
anyway that's what I ID is that because now uh assuming I didn't break anything else yeah cuz now what I can do is I can
introduce this is the parameter no I ID there we go and if we go back to game ID wait oh this is problematic um I'm just
going to break it well how much is it used it's used in one place so I'm going to break it change the return ID yeah um
and then person uh what does player take oh player hasn't been adapted yet so let's player um I think this one will just
do I do another extracting no I think I'll just say new person ID yeah that's why if you wait too long to do these
things yeah I'm totally losing on on my uh only use automative refactorings just because there's like so few places that
it sometimes it is so this is going to have to be player ID as well uh we'll change that in a second is it suggesting it
can be a record yes yet um so that's person ID person ID person and um create a pull request why would I create a pull
request when I push the commit to to origin that's funny uh okay and let's go ahead while we're here um let's go every
time I look at like type migration it's like I want to do it so let's let's I don't think it does it never seems to do
what I want which is like take all the Longs and convert them into this other thing uh but we have to create the object
first um but let's go ahead and try that so let's go and and uh extract and so can I migrate this let's see because what
I'd like to migrate it ID yeah it's like it can't convert the long to the player ID is that because the player ID is not
correct it is not correct um uh and I love how the the file it created is actually wrong because it I don't know why it
created this empty Constructor and I've seen it do this every single time I do create delegate when it makes no sense to
have that Constructor um because really that Constructor should be and then there should be no Setter is anybody
actually calling the setter yeah that so we'll have a compile error CU we setter uh I feel like there's there there
should be an easier set of refactoring steps to do this and I think I'm going to have to take some time to explore that
because extract delegate doesn't quite do it cuz it's type either like rap method return value it type burrito um yeah
maybe the create parameter let's try that we back to passing you haven't made any changes yet I could have just done a
revert um so if we say on this create introduce parameter object that actually makes more sense yes uh well what will it
change though um is this just going to unwrap it because what we want is also for this long to change but let's do so
we're calling this uh player ID and the parameters to extract is just the oh refactor anyway yeah so it so it changes
the Constructor here but it leaves us still with this and still with this so now we have we've we've at least changed
the colors to this so we've change the outside view of player um and now we need to change the internal storage of
player uh and what I'd like to do is I'd this this one always frustrates me encapsulation again uh yeah does everything
still pass yeah but at least the caller to player which is this one um does the new player ID so that that's helpful the
problem is now we've got the class uh and so now I can't extract delegate because you can't extract delegate into an
existing class you could do introduce parameter object into did we try that oops that's not what I want that's what I
that that's right you're going to suffer while while I try a few different things here all right so back to player um so
we said we wanted to extract this into a delegate that we're calling player or factor uh so it's going to need a getter
getter all right fine you want to you want a getter I'll I'll give you a getter but then it creates a getter and a
Setter which is not what I want but let's try this um yeah so it does it does this which is great uh but I could ID can
I tell it to initialize in Constructor yeah so so basically it created this player ID with Getters and Setters except
this is not valid because it created this as final and this conflicts with the fact that that it's not coming in in the
Constructor which is just I I think this is a bug like if I extract the if I extract delegate it should at least create
working code like Why didn't it create a a a um one bug did I meet my one bug report per stream minimum this is a bug um
so sui suggests uh create a new field player ID with a query player ID use that an ID and inline ID um could also create
the field and yeah it's like when it did this this is just not right um all right well I think I'm going to call it here
we're just going to say ID uh and then we're going to create a that and then we're going going here setter sign been
that battle I I don't know that's that's that I'm not I'm not going to fight that one um let's go parameter uh so what
are the um everything passes are are we where we need to be so we've got person I to player um player has player ID uh
person ID oh this one we need to can I what happened to my menu bar that was uh see like rap method return value is what
I'd like but I never know this is I think part of the extension thing and I never know like what do I need to to select
to get able Oops why did ARG let's try that again we're here we're here Factor ah rap method return value uh use
existing well yes it does yeah I was going to do the delegate and inline but I wanted to try the the rout the middleman
um it's like this is a record you know that records have get field uh that's the second bug um we're going to refactor
anyway work see is that a bug or is that just like I mean it's a bug because clearly when it did the refactor it knew
what to do right because it it did this thing although it didn't need to unwrap it um that's kind of funny uh they could
have just returned it whatever um and then it did the right thing like it gave me a warning that this is a problem but
then it did it and it and it worked uh we don't need to create a copy so we'll just return player the pieces of the
refactoring that we'd want are there like some combination of of what it's doing to get the return type correct to get
the internal State correct to get to to wrap things as a parameter object like it feels like if I could munge those
together if I if I had the heart to to write a um but that may be request um the the wrap return value uh map method
return value is is actually I believe I'm where is it I don't think it's not refactor X but it was thought it was a
plugin yeah additional ja staring me right in the face um so it provides uh these refactorings um and that's open source
so I guess I could look at that I don't know we'll see well I expect jet brains to to be a little bit further ahead but
there is still quite actually there's there's quite a number of places where it could have created you know the the old
this this meeting could have been an email this class could have been a record when it generated it um like when we did
the extract delegate it could have just gone the additional step of just gen or even off the option of generating a
record on the flip side it's one you know quick fix away from turning into a record anyway so but there are some other
places where it'd be nice if it created the record right off the bat but creating the Constructor that was empty and you
had a final field no that's that's a done yeah I I wouldn't be opposed to that but I would assume that um that's harder
because if you're working on an older code base then it has to know not to like pre Java like Java 8 or Java 11 uh that
it can introduce a record um so I think it's easier for them to basically say we're g to assume you know lowest common
denominator and then you can you know sort of modernize fixes yeah I don't need help that's what chat GPT is for for
generating non-comp ilable code if I want non-comp ilable code I'll yeah nothing can create create uh an abomination of
uncompilable code faster llm uh all right so our test pass we got this working uh because this one's pretty quick let's
just do it uh I did commit thank you I did not push at this level it would be an exception Throne if you try to have too
many people VI I think it's started doing that because I I I I processed asteroids pull request earlier and now it's
like everything is do you want to create a pull request it's like no actually I so I think what I'm going to do first is
basically Are You full because my rule is um and it's not just my rule uh very much the uh the can execute pattern um is
if you're going to throw an exception because you did something or attempted to do something there should be a way to
detect whether the thing you're going to do is going to throw an exception concurrency aside um so if we're going to say
that if you try to add a player if a player join when it when there's already four players you need to have a way of
asking the game how many are you Are You full um one could do that by just saying hey game how many players do you have
um but deciding game in my mind like the only time an exception should be thrown is because of concurrency like two
people tried to join a game at the same you know at almost the same exact time first writer wins the second one says
boom um as unlikely as that is but that's sort of my mental model uh what's interesting though in combination with this
is not all joining persons are new players so if there are if it's full you yeah exception message uh did you check if
it was full before you tried to add so and usually I write the code and then extract it but I was kind of thinking of
the name first so I decided to to do it um so we're going to say for uh long ID equals 7 team way and I really shouldn't
be generating this by hand I think that's five uh four no 3 um I guess let's inline this back and right 1 two 3 4 yeah
yes I I could do an instream or a long is intell would intell suggest that let's see uh interesting so it would collapse
the yeah uh and I guess I could do uh now a long 11 I think that's harder to understand but we'll still create a uh uh
yeah never mind I'll just do an in stream I was going to make this from from 8 to to to 11 or 8 to 12 and I'm like that'
s going to be harder to read to figure out how many that is even players um I don't care that they're concerned I was
just going to generate the long and that way I don't have to do the addition here that was what I was avoid uh so each
player joins the game game I think I I'm not sure how much I like this better than the for Loop um but certainly uh it's
it's not worse all right so we um and what we're saying in this test is if we ask uh is that assert that the that's
range closed is unfamiliar yes range closed is unfamiliar if you're not familiar with it it's not a tautology if you use
it a lot you're familiar with it if you don't use it a lot then it requires thought so it has not become familiar enough
that it's automatic for me uh we'll create the method and it's a false uh except this makes me realize that uh we don't
have the zero case so so yeah sorry now that you're yeah it's it it's I mean it it it this will go away when value
classes uh finally come in so so not much longer before we can stop uh but what so so the other alternative was was what
suiga suggested we could do a stream of objects as objects yes it does okay so then we could just map I wasn't sure if
if it if it would these uh so value classes are um part of Valhalla which is the so there a bunch of these umbrella
projects that are doing a bunch of things so H includes value objects so we which brings a number of around getting rid
of the differences between objects and Primitives for the most part um a lot of other features too um so for example in
jdk 23 the Primitive I think primitive pattern primitive um pattern matching is coming as a preview uh but but there's
stuff about layout and memory and optimization and and so on that uh is all around value classes which are basically um
what you'd think like I can create uh something that is sort of as compact but also lacks an identifier um so we can
safely say that you know uh 7 L is equal to 7 L right if we do a comparison for these two we know they're the same
because they have the same 7l right the these are still the same they're not the same instance although they might be
for optimization purposes underneath it does some optimizations right it's not going to cash C there's not there are
some optimizations for like you know not creating new instances but even though these are technically separate instances
they would be treated as equal equal so all sorts of interesting stuff comes out of that um but I think I like the
stream better than the pesky in stream all right um if we're going to say this is true uh uh we're going that uh let's
put this on hold for a second I'll leave the method there even though that so we'll create a new game does it pass so
that passes um now we can go fail and the only way to fix it is to basically make this computer Ed in some way um which
is uh Map size four and that is now passing uh yeah so the next test I'm going to write is you can still join if you're
full but I had to establish that um yeah that was suiga that was that was basically gonna going to sort of be the next
discovery that is full is not enough I need to basically say can join that um but that becomes more complicated because
then I have to pass in yeah the person ID right so I'm gonna uh I spell encapsulated wrong encapsulated yeah whether an
admin can can add players to to te a technically full game is uh yeah not I don't know that causes all sorts of problems
like how many can can the admin add uh the bigger problem is where the heck do they appear on the screen remember we're
working with with a with limited space um there is an adapter aspect to it but I think it's and so I am predicting bit
what I need um the alternative is I have to ask the game is this player already in the game and then do something
different uh but if it's in a to a certain extent item potent if I add a person three times I'm always going to get the
same player and I think that will make it easier um cuz I think the connection handling stuff is going to be separate uh
I could say player 4 and honest this is this is sort of the problem of of inside out writing writing ahead of the known
needs of of uh of of the UI um so let's let's mark down this this as we'll see so we'll we'll go back and say you know
were we were we right to was I right to to to predict this this need or was I wrong and then we had to refactor our way
around it I don't anticipate any refactoring they have to do is is going to be difficult but um yeah yes definitely the
the digging the uh yeah I may have I may have have gone too far um but that's it this is this is the last one uh before
we move on to trying to um so if we create a no I don't want to do that that yes I want to do that uh IDs might idea can
I pull these out in as parameters it let's do that uh and then can we convert that yes uh because then what we can do is
that that they're a different one okay great so I did that because if this wasn't visible then I wouldn't know that this
is a new a new person ID um yeah 42 I I normally do but uh it that so the post the custom postfix uses an assertion that
I don't like to use um assert that illegal State exception that's our temporary go-to uh is thrown yeah yeah in this
case I mean I can make it 42 but I yeah I actually do care so this will fail because we're not exception uh so we'll go
ahead and throw an exception when we try to it's not an illegal argument exception it's a legal State exception oops uh
so yesterday somebody was showing me some code I haven't seen this in a really really really like I can't remember the
last time I saw it uh where they had uh no opening and closing brace and the intention was for this code to be inside
the if block um like that uh that's not good uh luckily intellig marks that but the their code wasn't wasn't marked um
be careful always put that's why we have a rule and um luckily intellig uh also warns us about that which is um this
should pass and other other fail uh equals on different types that's so here we'll actually um we'll make this 11l but
we'll pull variable so this will fail cuz it right um going to disable this for a second because I'd actually like to
with CER IDs I don't know what it's 13 something like that that's going to fail cuz we're not throwing a here um uh
we're going to extract this as um IDs and this one will'll extract as ID is it player ID or person ID I'm getting it uh
does that work and then I'll have to uh let's actually change this to oh I didn't take it out of here either okay so now
it should match and now we'll change it uh so that this is the player map Keys key set to string that's probably not
going to be close messy I don't disagree suiga I'm just not sure what other names to clearly I I hesitate to go to user
that's why I have it as person um but it uh okay so that passes um so that we have better error messages uh when this
test right oh no it doesn't cuz I disabled it now it will'll fail and we'll get the the message okay so that's what I
expected even though I didn't say it out loud um what's interesting is that now we get pressured to to do what sui said
before before which is is full is not fully a function of how many players there are but who's trying to be added um so
this is not really is full anymore join um although it's not really can let's do that um I didn't commit cuz the uh test
customer feel like they're in a different subdomain certainly customer uh and to me member has a the connotation of of
they're special in some way 404 not F yeah sleep if you're tired go to sleep um all right so let's let's fix this
because what we'd like is uh to so new game um uh persons can join new game so we'd like a method called can join and
we'd like that to be that and we're going to basically return the opposite test um what else is calling cannot join so a
person cannot join a game with that that uh from I want can join this should be oh I just need to flip this this is can
Jo not can join right and then this isn't used by anybody oh now we can all right and then we can say so commit that and
now we can say at least more easily say uh so hold on do we still have the word full anywhere yeah so exception of throw
in a player game okay uh yes accept uh expect that no exception is thrown yes uh assert that no a there are two
variations of this there's assert that no exception is thrown and there's also uh assert code that say whatever and then
you can say does not throw any exception so this one is is sort of Inver is phrasing it in the opposite order um one
thing if you're with with a search a is there's lots and lots and lots and lots and lots of different ways to do the
same thing and this is one of them um and all of my assertions that I use everyone uh is all using a search a and so
there were a bunch of uh ones that were and spring the spring project uses a search a as well and they've actually some
of the folks at at um that are spring Engineers have contributed like we would like it this way and so they've
contributed back like assert that uh This One S that illegal State exception since that's such a common thing um they
sort of elevated it to a top level assertion and those were those were uh um committed uh suggested pull requests were
were came from from Spring folks so uh so I've I've actually I used to do it this way you know startt that whatever
throws exception um but now I I yeah it's not often that I that I say something like this um but it is a quite a
targeted test uh you could say well any test that does the join where it's valid won't throw it but this is a lot
explicit yeah yeah when it's a no op and there's like nothing you know like you could say well again this is part of
this test they're doing a joint and no exceptions throw is thrown here um but but if it fails this is going to be a lot
more so right so we are now here um where we want to say that we don't want to throw an exception right now there's no
way to say that existing person so we need to do is change our now I could change this first uh but in reality I am
changing the behavior of this so I need to test drive this so we're going to Red test um we're going to go back to our
fundamentals around can join uh we're going to say can join should now take a player um yeah I'll do it do it manually
so we're going to just say player ID um H so one of the other problems with doing inside out here uh is I have not been
clear about boundaries person because a person is a separate aggregate I haven't sort of drawn that out in uh and right
now person just has an ID so that's why there's sort of no difference uh but yeah this should be person ID um which
makes sense because that's all I I use from it um which of course makes sense because there isn't anything else in in in
person uh and it it does not actually hold on to person right so we got person here but we grab the ID as the key and
then we grab the ID as part of what what attaches itself to to player so there is no reference to person in this class
in terms of of data um but we should make that more clear uh let's finish this no let's let's make that change um this
should be person ID uh so parameter and it will remove the parameter and so all should be good uh yeah whatever go ahead
refactor it's not as readable uh I'm not going to now technically I could just ignore it this coloring is is is
interesting so this you may not be able to see it uh this one matches the one looks like it's a field but um so
something that I'm going to be adding pretty soon is the J molecule stuff that will make this uh at least the the the
the not necessarily the DDD stuff and not the modulus stuff at least not yet um but there is the uh DDD stuff for
Aggregates and entities and IDs and aggregate references and things like that yeah this is an a closure and so
misleading I mean it's a Lambda and so this is referencing if we if we go to it where does it go it goes to right if we
we start here we go find the Declaration and it's this um I don't like this color because that's confusing so something
uh that you know which is why when whenever I switch to dark mode I get lost is because we are pattern matching against
colors um and I'm going to go on a little tangent let's go look at our editor color scheme what field it is a Lambda
parameter but no in this case it's not the Lambda parameter no I didn't say dark is I guess this treat isn't implicit is
yeah bdsl exactly that that that's every time I I do this I'm like which thing do you think this is so I can go color
like I don't I don't think there's any way to do see let's try that so the question is will it actually change that
color yes it did um no actually that's way too close to parameter but that is it is treating as this implicit Anonymous
class parameter blue it's like all the colors are taken I remember when I I I've done some customization on some uh some
things like I actually color my interface differently um it's like there's only so how about enough yeah you can
italicize it you can you can bold underscore like uh well you have to border it with color yeah I don't think I want uh
underscored that's that's okay and then I think if I make that the um what is the not type parameter uh what was the
color E11 there we go so make it parameter but it 85169 underwa no I'm not going to under wve it no I'm not strike
through it either no the reason why I did underline is because um that's what it does when you reuse a parameter so if I
tried to do like an assignment like if I said person it so it's kind of the same thing but you have to be careful about
that so this isn't quite that but it's obvious see what were we doing we were going to Uh something's not oh right when
I basically converted the parameter from person to person ID this this that uh oh and it looked like it did that
everywhere okay so here that's here now I'm finding that underlining a bit too strong so let's let's give it a it okay
right so we changed it to be person and now we can go back uh and add this in here so what we want um so this is an we'
ll add this as a be sure let's try usages by the way the other day I finally like fig figured out what anyar means um
for the longest time I honestly like didn't know what anyar meant what anyar means is if it can find a variable that
matches it nearby it will use that and so that's why this worked it basically said oh you want a person ID well it turns
out I've got one in scope so let me use that um and then the other usage down here was well I don't have one that's in
use uh and this should really be new person anything so now we're done with our prepare refactor and now we can go to um
why isn't disabled it's funny I think I kind of think like disabled should be a warning can I make disabled a warning
today must be editor configuration tangent day or something uh so we want warnings not color scheme be there probably
one oh look at that there is one yes I warning uh only report annotations uh no I want you to report all all of fine
there we go so no need for a custom inspection I mean I I kind of would like a disabled without a string to be an error
um not sure I can set it up that way cuz there an option for this one like I can mark it as an error but there's no way
to say uh but if it's got a reason then that's a warning yeah that would probably require a new a new custom inspection
I guess I it uh I'm not going to do that right now I didn't see a duplicate but it no I'd probably have to go into the
uh way um and it's powered by the junit plugin so I have to go look and see how that so I want a Jun error for disabled
without a reason cuz too often I've been burned by disabling something and it's like why disabled okay uh so now we can
uh until conjoin Tak it can take a person ID which it does so now we can reenable this uh this will fail cuz we're not I
really hated writing that Buon expression um push ah thanks for the caffeinate that's probably the last of my caffeine
for today let's see did I miss anything in the chat um yeah there's there's zero chance that uh there's going to be any
any refactoring of intelligy to get to CSS for some of these elements um there is way too much code for that kind I mean
this is why they did the um the fleet stuff and uh the code with me lightweight client is they basically my
understanding is those are sort of rewrites using a more modern architecture um but they have their own problems oh
four4 not found thank you um speaking of which I'm going to take a quick break uh so those of you who have not enjoyed
not um in Game Dev we used wacky magenta textures to find stuff yeah a common thing that I that I do a CSS is like let
me set the border of everything to Red because I'm really confused as to where stuff is uh this was before the um the
dev tools got good enough where you didn't need to do I don't need to do that anymore uh all right I don't think I
missed anything in chat if if I did if I didn't respond to anything you said feel free again yeah setting the board to
outline yeah yeah um all right uh I'm going to take a quick break and when we come done um I I'll I'll let I'll let you
all decide so here are here are the two so option one is work on start game 91 uh the other option is basically create
the UI the adapter all that stuff to actually connect the outside world to that so you go vote while I go take a break
and enjoy the coffee break you that all right thanks for the two vote early and vote often is that what you're doing ASD
one one one H yall are making this hard two why fix it yeah okay we'll celebrate every time I come because if I switch
back and forth between this and and the drawing uh the the physical game camera then that's going to be annoying to me
if nothing else so I didn't I I I'm not sure I see a clear uh so let me clarify um what choice number two is uh there
will not be oh there may be a poll thing yeah I tend not to use the the twitch tools uh it is one um the UI is is is not
going to be the final UI right so for those of you haven't seen uh this is my starting uh mockup um this is I'm using
figma to to you to start laying out the the real thing but since I am nowhere near done with this um it is going to be
like a Texton UI so just sort of representative of the information it is not going to be anywhere anywhere close to and
I I don't I don't even know when I'll get to something that is sort of you know like this although this isn't hard
because I have all these images so this isn't this isn't hard um uh but anyway like not not getting to one uh yeah I'm I
I'm kind of with you sui I I I I'm a little uncomfortable inside inside out see uh is that it no oh there it is poll and
I did not turn on the option where you could stuff the voting The Ballot Box by spending points so go ahead and vote
this will be the The Binding vote now that it's much way uh no no comment as I and and this is this is a binding vote
and we will take it at face value um this way anyone who didn't want to appear in the chat can can also vote and not
feel exposed draw all right well then I yeah then I get to break the tie uh in which case uh um let's do it I don't I
don't get a vote I get I get uh so I guess I'm like the um uh vice president I I I I'm I vote to to break the tie and
you all tied so uh I break the tie and I'm going to vote for uh working on the adapter all right so this is what we're
going to work on now next there's um not I don't know we'll see how much there is here um so the first thing we got to
figure out is uh our player Joins game requires two here I also uh probably just want the person ID but I think we have
to add some stuff to the person before we can get to the ID which um least well actually I didn't want to put the names
uh well figure that out um so let's see so what do we want uh for the for the initial screen so the initial screen we
said is um you have to pick we have to pick who you are so we have to know who you from um yeah technically both of
these are are identifiers uh that'll become clear uh cuz one thing we're not seeing is creator uh so we create a game we
get a game but really we get the game's ID so uh so 44 now found asks why text based game well because I I don't want to
uh because basically I haven't I haven't finished this this is this is not done yet um one of the issues is you need to
see your hand you need to see your play area you need to see the the deck so you can draw another card um you need to
see the board which is a little on the small side right now um but you also need to see everybody else's cards uh and I
have not figured out yet how I want to squeeze that into this area um I may have to raise my lowest common denominator
of resolution this is currently based on uh 1280 x 720 which would fit anybody's screen even small laptops um but I may
have to raise it because I may not be able to fit it uh on on on the small of a screen it is a lot of info um and even
with uh basically 1080p right 1920 by 1080 there's not all that much more yeah so one of the things I can do in terms of
tightening things up is you can see so over here um you don't actually need to see the actually not show that in this
sort of zoomed out view because really the only thing that's important is what is the title of the card the rest are
instructions and you're you clearly cannot read that I can't read that um and so the idea would be you know some kind of
click or hover and you'd be able to to sort of or actually i' probably have a special key to sort of zoom in to to in
right then then that then that's readable um but that's sort of a temporary temporary kind of thing uh so there are ways
where I can sort of you know compress this to be smaller Um this can be a bit a bit smaller uh at least sort of hor
horizontally but anyway like all that stuff and deciding that stuff and figuring that stuff out is why I don't want to
do this now because uh that's going to take me a while to to get uh to get to something where I feel like all right this
is a uh I don't know what it is in in inches it's basically um res resolution yeah so many so many bike so we want a
page where we show way uh so we need a all right so let's yeah so let's go ahead and create templates I'm going to call
it login even though it's not really I guess it's more of a pawn picker but Pawn is equal to person why are these all
start starting with P we've got player Pawn person D yes this is this is this is the the sud sud pseudonymous P anyway
um version of of of login uh because I I didn't want to add security right off the bat pile okay so pick your Pawn what
we want here is basically I think these are just going to be a um pawns and the th text will be here oh that's true I
could hard code idea let's see so that would that that would give experience sure let's do um basically it's login with
your name but your name has to be one of these four I'll I'll just validate on on the on the side if I thought that that
showing like a bunch of uh player names um would be useful um but yeah so on the other hand uh uh well let's let's start
this um what are my colors blue green red and yellow and we'll add in a couple more colors that we have uh for other
games black and white those match the colors I use for these and I I would love to sell enough games that I can start
switching over from plastic to to Wood uh as it's a bit more sustainable yeah exactly Astra that that was the reason the
reason why so if you're picking from it um uh uh you could still do a post like craft a post of your own but then I can
just quickly validate on the back end uh what do I want here uh I want name is uh Pawn well we'll call it this it's
really interesting like I I almost never use search and replace anymore um because I either do a refactoring or I do
multi multi Carro stuff different wood species uh you overestimate uh how much I'm selling the game for I I I could do a
special edition and it would likely increase the cost by like four times it's amazing how hard it is to source some of
that stuff I guess it's not amazing but it's hard to Source some of that stuff me yes uh okay so basically you select
one um and presumably we need to put this in a form uh and the action is going to we're going to post to somewhere uh
but the default action is that the th action is we'll just call it login for post uh I don't think I need anything else
what doesn't not like about that th action is not allowed here sure it I believe yes that the default action uh submit
this is the default the attribute is not specified yep if is associated button uh do we get a name and value back from
those I believe we out so what does this look like blue looks that's fine except for the yellow white asterid suggestion
of coloring them differently than the color they say mean uh so we said white was no good um let's change the background
to um dark gray all right so do you all spell gray e that's what I'm curious about uh the yellow let's gray so clearly
they prefer the E version no they have both okay I was going to say they prefer one version but we'll just go that way
all right what that looks good looks a bit weird but you know what uh I am not going to focus more I think I used to do
a for in Gray and now I go and now I go the eway E route but all right so let's write a controller um I'll test drive it
uh uh let's test out drive the controller class and this is going to be adapter in http um yeah we'll call it web uh and
this and yeah I think both I think it's gotten to the point where A and E are just interchangeably uh acceptable um
because you'll notice that in HTML and CSS color does not have a u in it uh but both gray with an A and gray with an E
are acceptable um so there you go test uh and this is a web MBC test class why does autocomplete not work that's a
bummer um and we want to is uh what did we say our endpoint was we didn't uh we basically said log pick player now what
do we want to do when you click post uh we want chooser although at this level we just uh so we'll do a mock MBC form
player uh with um person redirection uh in a sense I'm implicitly starting a session when you when you have picked a
player um because what do we do when we authenticate is we're trying to figure out who you are what your identity is and
your identity is your color so that's why this is very much like a login form uh yes to the lobby um uh so this will
fail because we got and I think I already have this set to MBC hey uh and we'll duplicate this to be MBC tests and that
are only ignored ha I'm like what I'm like oh yeah I did not set this up as a spring group project uh well I did uh but
clearly not quite because I don't have an application file so let's go create an application file do I even have I don't
even have web MBC uh so let me add a few starters here hold on uh uh should I add lumbo I kidding I'm uh oh spring web
is already in there it okay uh anything else want to add at this point um may as well add uh actuator while we're at it
what's wrong with Lumbo everything is lumo um what's wrong with Lumbo is it is a clu it does things that it shouldn't be
doing in terms of the way it generates classes um it generates code at weird times uh and makes life miserable for
refactoring tools yeah no uh where is web there's web socket o all right that's bug number three so remember when I said
I didn't remember seeing spring boot web right you think it's transitive through websocket ah it is transitive that's
interesting so it is transitive through uh I mean I guess that makes sense there's no point in having websocket if um
that's that's interesting I hadn't thought about that uh but that means happens nothing oh what the heck where did this
come weird but every time we go in here is it so I guess we have to add it manually I mean I mean I could rely on it
coming through transitively but uh that's probably not a great idea all right but that's interesting um so the edit
starters is looking transitively at everything that Maven Imports I kind of think that's a bug but I've exceeded my
stream uh all right let's try running um a Java game application configuration and now we can run our tests and it
should fail because it's a 404 right that's what we got okay great added yeah it's it's sort of an interesting Edge case
like technically that starter is not part of my Maven file but it is brought in and if I drop websocket then all of a
yeah all right um so fails fails for the right reason uh we'll go to our and um did I turn off the machine learning
because it doesn't seem to be doing any completion anymore so I must have turned it off uh huh oh I probably have do I
have the it no Cody has turned off that's interesting because I haven't seen uh anything so this is a get mapping I don'
t know I I I I probably have some plugins that need to be updated maybe because it's in the you need to restart your IDE
state that I don't know uh we're going to do a public what are we going to return here we're returning a redirect so
we'll do public for now we'll keep that as empty um and right now we'll return uh just a plal oh 405 this is not a get
mapping this is failed me add to my list of fail to predict so this is May 10th oh first R first rule of of improving
process yes this answers the question of tests because do exactly that technically that wasn't a failure in prediction
uh it was a failure to get it to pass which according to the game though was still a failure to um now we can add that I
haven't pushed in a while let's go that uh no that's fine so that'll be valid oh I knew where you were joking and that's
that's why I was like and that's exactly why oh you're joking about something else well uh so let's go test that's
interesting that's a different way to get there uh player picker test this is not an MVC test this is a regular old test
um so one of the things I want to do is make be post does a redirect to the lobby um there'll be some other stuff too
but I'm not sure what that is let's start with that uh posts to pick picker and uh player redirect uh is equal to so we
said we're fail CU we're just redirecting nowhere or root to root uh oh um this is actually a a proper failed to predict
I predicted it was only differ by the redirection but I'm actually all cuz I was so focused on the destination I forgot
the redirect so now the only difference should just be the lobby instead of the slash that's that put in the right all
right so now what I want is what do we do information so we're going to get some string here name technically I shouldn'
t be writing this but I've already got a test that's already sending in the parameter which is uh uh the MBC one um I
don't remember what I call the variable I think I called it something else let's run all the tests I don't have one for
all the tests let's go run tests I expect yes I expect this to f because it's a 400 because we're missing the that so
the test is correct we just need person uh that should get those tests to pass name and so here's where it gets a little
tricky without having security is session I wonder if I just should just security cuz if I don't then I have to manually
track your session and I could support um and i' I'd like not to do work that I basically I'm going to have to undo
later if it's not that much more work to add the left when I hit an endpoint weird uh because if I don't let web if I
don't let Spring Security manage the the principal I have to track that myself in a session which means I'd have to add
session support which isn't hard but I once I use security I won't session or I won't need to be explicitly using I mean
the other way I could do it is I could pass along the player name using the flash redirect attributes sorry not the
flash the redirect getting what's essentially the user in a different in a way that I'm going to have to throw away and
red do security yeah that's what I was thinking bsls I can I can add security and I can add details because right now
the point is like I don't I don't care if anybody just logs in once I deploy this because a primary goal is I want to
get this deployed and available as soon as possible um so I can start doing continuous deployment uh but I didn't want
to just have any be able to log in um so we could predefine users with General passwords I think that's what we can do
and this is where I'd want uh AI to to just generate it for me like can you generate a login with user details because
that's pretty well known yeah pretty much that well admin admin I would not do that uh because right now I don't have an
admin role so I don't need that at the point where I actually do need a real admin then I will actually go to real a
real security uh o client um likely uh it'll be you know Google and GitHub are the ones I'll I'll do that all right so
should we try out uh should we try out Cody see what it's going to generate I haven't actually ID well it may end up
being basic off um but Spring Security will handle that stuff for me so I don't have to anything uh that's fine uh oh
all right sure let's go update take me there update update update update update uh they are really nice aren't they my
uh uh clean up my my InDesign manual because I've got a bunch of pages to add and it's exceeded my tolerance for for
working with Adobe and design um well all right uh nothing here how do we turn Cody on hi Cody straightforward all right
let's get oh I should probably before I ask Cody to do that uh we probably need to go into our security uh we'll add
Spring Security we'll add the o to CL no we won't add need I don't think there's anything to well it's going to sort of
um it may do the bcrypt hashing for me uh we'll see what it it depends on what it generates but um honestly again for
this I really yep yep that looks good thank you but I already added Spring Security but I um that looks fine uh and yes
it did encode the password uh and yes it is using HTTP basic uh all right so insert a cursor well you can't insert a
cursor curs can you my cursor is not in any place let's put my cursor here and what happens if we say insert a cursor
yeah I was afraid it was going to do that it's like no it really should have an A create new file um yeah that would
have been nice thanks Co appreciate the here uh because what we can do is I can click here and I can click paste and it
will create the file for me I was going to say uh I think it's outdated uh because it's not this anymore uh isn't it
security whatever um does coding no let's see does hey it knew about security filter chain Why didn't it discover that
this is why I don't hire AI to do all my this and we will just replace it oops well now no it's like no don't um uh
let's see so can I ask uh that looks better let's grab that I don't know why it didn't generate that before defaults all
right uh so we want um blue is blue uh R is user whatever that's fine uh this seems like a really slow way to us um what
was it uh blue uh red green yellow black and white instead see the thing is it uh it didn't let's see what it does and
then I'm yeah all right that's not bad uh where's the create user okay you well I'm not going to thank it until door uh
and we lost blue all right well um do we think this works uh so we're basically authorizing any request uh we're using
basic did I say instead of blue yeah but it meant uh okay so we got our security config um this will likely fail now
because this doesn't have uh but we don't care um uh we have a home page no we don't yes we do what do we have we we got
our person picker which basically we're basically going to is obsolete um but let's see if we can hit that end point and
what happens uh in this case we're just going to wait why Imports yeah Cody you should have known what I meant not what
I game password uh all right let's go see what happens there shouldn't be any such endpoint but it should should get us
to log in credentials is that the name of the right oh you're kidding you're how many times I've done that and that one
I basically just clicked in the wrong place oh restart uh let's try it again aha sure uh I think it's because um well we
said basic we weren't kidding uh we probably uh what is it we want dispatcher type matchers um error forward and I mean
it did say htb basic we could uh say well let's let's see if let's just oh right that's a post end point all right well
that's that's that's good um because that now tells us we can get error Pages uh so we actually can't redirect anywhere
because we don't have a get um we can close that and we can close that uh so after you log in where do we want people to
go we want them pretty much lobby and if you don't have uh let's all go to the lobby going through your head um You
probably haven't been to the so if we're going to assume that login gives us user then we need to kind of throw this
away so it's not pick your player it's now um choose or host a game and I know it says a stream will went in shortly uh
I'm going to reset my timer although I amazed at all of you who are still awake go I might go until um another four
hours I don't even know I could do another four hours uh I'll keep going until my brain is is dead yes let's all go to
the lobby thank you for that um all right so uh let's rename this file uh we'll just call this Lobby um the action here
uh uh is so this is we need to uh not which uh I'm just going to put that as a placeholder um because the first thing I
want to do part uh so you log in you go to the lobby you buy some candy um and then uh you there no game so you're going
to um that new game popcorn yes has another P what flavor popcorn do you want uh so this is going to post to um game the
because we are basically creating a game uh and it's going to be a post and all that stuff goes away all that work all
that hard work wasted actually I could have had Cody generate it so the the the llms are great for like the the this
kind of repetitive stuff um mushroom flavor uh so what do we we want here we field uh and there's a text uh and that's
close Cody but we're in a Time Leaf template button I prefer button though can you complete with a button you actually
Cody's not bad here like it it took my my my direction um although Cody we don't need the type equal submit we learned
like looks just fine so this will post um okay so now what we want is after you post it should create a game and then
redirect you uh okay yes I I love natural templates and I don't understand the usage patterns of people who so there's
um some interesting other templates template libraries uh jte is one um Thomas shuy uh uses it in one of one of his
libraries but it's not a natural template and so I always wonder like then how do you work with designers all right uh
bdsl just did an update of all our angular templates to use the new feature that makes them further away from natural
templates o well I guess you haven't lost much if they weren't but I just like how do designers work I I don't I don't
understand it maybe it like I want to be able to at least view the the template may not have all the information filled
in although there are ways you can do that with time Leaf but yeah Spa is make make that just so much worse because it's
not even all in one place uh okay um this test goes away this is no longer player picker uh um so you've logged in and
you go to the lobby so let's uh let's delete this test and let's delete this and this is now not player picker um lobby
all right so the test we want here then is uh when when we hit the root of the site yeah I'm taking this this CSS class
and so one of the things is like when using in in a sense implementable yeah um and I'm not saying that all designers
should be Cod ERS uh but certainly designers the more aware they are of the constraints and benefits and limitations of
what are basically components the better off you are bye again um I have to say Cody is certainly way better uh uh so
far than than the jet brain's AI system um because notice that it that it correct uh it assumed because of the redirect
that I that I wanted to post but actually I want to get but I'll accept most of it um um it also did redirected URL
which I guess I'll do get what oh because it pulled this this okay uh so this will most certainly not nothing uh does
this even compile what happened here um anyway okay so if we run our NBC tests this will because we're I don't know
where it's going to redirect to uh it may even have a security see yeah so we got it unauthorized so let's do uh with
mock user and uh blue uh because the eror the the error 404 uh oh I didn't actually do an expect on that I'd like the
status uh to be uh all right so now I've got uh a 404 we are logged in with the principal blahy blahy blah username blue
yeah so that's that's all good roll user not that I care all right so what do you think Cody can I can you mapping nope
good good good try though um pass all well that's true yeah GitHub doesn't uh render HTML um I assume they don't want to
bother with making it assumption all right so we can stop with and I can't amend because I just committed pushed so
we'll just uh name um now what we want is when you actually go to the lobby you get your return actually this we just
want to say uh that's very nice thank you that will fail because we don't have a get at that end point so we should get
a 404 because we do have a mock user and that's what we get so now we can go ahead and do a get mapping that's
interesting that it let me autocomplete something that didn't all right um well that's going to fail uh because we're
not returning a name I may as well just return Lobby that's yeah well big corporations that have lots of profit just
because they have money to do things doesn't mean they will do the real question is how would that GitHub because if it
doesn't benefit them they're not going to do are something something capitalism uh okay so we now have a get mapping for
show Lobby um so which is an actual page uh let's try tests I don't know why it did all in directory I just want like
all in package thing that's fine um but I did want to edit center all right so that all works that what's the onversion
file oh that's weird on all right um now what uh I was going application so let's go here we uh here um so we're going
to do a p hello of uh name and so now what we'd like is uh in if we're going to have with mock user so not only is
status view um no not the view we know it's model uh attribute of person fail yeah well that's what big companies like
like Google and so on have done is they've just let go thousands of developers cuz that saves them money uh and maybe at
Google that was fine because maybe they weren't really doing anything terribly useful uh but other companies maybe they
were and maybe you'll you'll stop making as much money as you did uh okay so this will fail um because uh we're not
pulling anything model so it's basically not there yeah so let's go let's go to the lobby I'm going to laugh every time
um so what we want here is uh some um is that the right way to do that I don't think that's the right way to do that uh
but we also want the model oh look thank you why are you suggesting log back I principle oh okay so they've already been
so authenticated principle uh so let's see so what can we pull out maybe uh I believe this has to have any fixes you'd
like to to give me here I think it this requires authent authentication principle that see this is the kind of thing
that I want AI to do more of is like this won't work by itself you need this this this out I didn't because
authentication authenticated principle supposedly has equals uh although that shouldn't still difference um but I'll
also try yeah I feel like it's it's not uh not logged in well we could go look at the Docks while the test runs we'll go
look I could do that um I thought The annotation would be right and now works authenticated tries to give me something
else with uh I don't know why this doesn't resolve to the same thing what does our uh security config look like I mean
I'm not going to worry about too much because this is likely going to change used is this really never used that's a
little yeah I think it's yeah there's there's something wrong there uh and I'm not sure why it thinks I'm oh that's not
the yeah that's the um like this is literally the stuff that I want the AI to do for me because I do it like once and
then I never set it up again um and I can't get it right because stuff much uh over the years um this and in here here
uh why is this an example there's no security here unless this is just like default security here's a security we got to
enable web security got our security filter chain uh oh we can add form login that's what I'd like to do because that's
a with you feel like you do this multiple times a month I'm sorry um the user Detail Service should be the that yes uh
with default password encoder let's try uh then we don't need whoops then we apparently well so why uh oh it's not with
it's not with username it's just username that's why well it's acceptable for demos and getting started that's fine uh
other stuff that's fine um the yeah the way Springs sometimes seems to but not always instead so I feel um let's see if
I can log out yeah I'm looking for the cookies but I want to see if I can log out okay so I think because I now have the
form based version the log out the log out works and I I think it it I was logged in but it doesn't seem to have enough
it might not have had the principal or something I don't know because there we go uh and it knows who I am which is what
I was trying to get to okay um I don't know I for I forget where the cookies are there somewhere uh but this is what I
want um and once you turn the form based login on then you can actually get access to the log out otherwise I don't out
uh what's all this stuff this is principal uh indeed and so you can go away you it all right so what's next so we've got
our lobby um we display this that's fine um now uh so that means we display this page we can wait for you to type in the
name of a fine uh okay so when you host a page uh page host a game uh it should create a game and then we should have
some way uh I think it would basically create lobby lobby uh we can close our MBC test for where uh oh we need a post
end point so we can't do this to uh games uh I like how it keeps getting this wrong post of whatever we said the thing
was clear and note that um I'm using type number because uh initially at least when I deploy it um I don't want an open
text field since authentication um no I literally just changed it to new game name use that as our game name uh and yes
I need another close pren should still be a 300 fine yeah and since this is a number there's sort of limited you know
the worst people can do is do this which I care less about or 420 or something like that um so this will fail because we
don't have um is it 403s yeah I mean you could put 69 and I don't really care again there's there's there's limited
attack surface um that's interesting that uh oh yes a csrf because I didn't turn csrf off thank you um so where does
that go not here I think it goes here with yes oh now you tell tell me Cody thanks 404 again it's one of those like when
I was doing this kind of stuff it's like csrf Cody's been pretty helpful I got to let's create the endpoint Cody please
create the endpoint no it like has a very limited uh window of the code it's looking at like if I were creating such a
thing sort of targeted at at tdd you'll be looking at the test you just wrote to figure out what code might get that to
nope I said post uh I'll accept you but only because you and that's all this test needs but it's not show games it's uh
post new game uh yes I would like the principal but I would also like not the goes there we go game name except it's new
game name like I keep trying to tell you uh and just to be sure this a new game passes uh technically Ah that's
interesting so when you host a game do we care who did store maybe but for now um let's run all the tests uh and let's
see where are where are we in where's uh post CR game uh instead of using default game uh I basically have numeric post
um so we got that and then person join game stop what are you doing uh no that was weird Okay cut it out um so uh so in
the real application you will not see a list of games you um so when I dis so displaying the games uh yeah so you'd
either receive um you you'd get a link but you'd also get the handle uh which would be an easy to type thing because
we've got these human readable names um you would not until I get to the point where there's like teams and
authentication groups and things like that uh which is way down the line um so for now uh and so then join game is
basically that uh the text box for the handle and a join game button that does the uh which uh creates player in in the
person and then redirects to the page it shows the game page uh yeah the handle would be embedded in a link it would
just be a query string yeah um not for now but but for I like how Cody suggested ITC it's like thanks Cody good good I
was like is that all you got to say really you couldn't come up with anything helping all right I can tell I'm running
out of gas it's also 4:30 my time on a Friday I don't know how all you all are are are still here um I think this this
is good enough for now so next time here with um yeah I know it's way later for for you all uh so thank you for sticking
around appreciate it um so I think we' made made uh good progress um The Next Step is once I get these things done I'm
going to deploy it CU I think um yeah and then we'll once now that we'll have sort of you know an adapter connecting to
to the core um stuff will get connected uh and then um then we'll be able to go back and basically continue with the
start game stuff so dealing the cards to the players that are there showing in a very basic way using HTM X and
websockets hear your cards um and then starting to to to flesh that out how do you uh how do you play a card how do you
discard a card uh how do you move tiles and and things like that yeah I'm trying to think of a reason not to deploy to
railway I'll probably deploy to railway oh Jonas thank you so much for for uh your your sub I really appreciate that you
didn't have to do that but I appreciate it um so there's a chance I'll be streaming this weekend we'll see um I have to
get a long run in I've got a half marathon coming up in four weeks uh so I got to do some long runs tomorrow or not some
I got to do a long run tomorrow um so we'll see how how I'm feeling uh if not then what's my calendar for next week um
yeah so very much we'll then uh do some streaming on on Monday so if not this weekend then definitely Monday as always
of course uh um if you're not already on the Discord discord's the best place to keep track of uh where uh where and
when I'll be streaming um I'll probably also be doing some pairing streams again with Mike uh I'm not sure of a schedule
we'll figure that out this weekend um and that's it so thanks for uh for hanging around so much and with all the great
help really appreciate it um and all the good chatting makes it makes it fun for me uh so have a great rest of your
night or evening or afternoon um if I don't see you this weekend have a good weekend and I will see you next
