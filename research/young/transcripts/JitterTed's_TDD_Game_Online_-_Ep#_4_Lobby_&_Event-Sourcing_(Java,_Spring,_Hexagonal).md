# JitterTed's TDD Game： Online - Ep# 4： ＂Lobby & Event-Sourcing＂ (Java, Spring, Hexagonal)

**Video URL:** https://www.youtube.com/watch?v=wiqc-HPBSnQ

---

## Transcript

all right hello hello hello yes not TBL driven development uh test driven development um uh you can use uh a table like
structure for test driven development um there used to be a tool called fit and then Fitness that used spreadsheet or
spreadsheet like structures for tests uh they're still around here and there um be uh although this is a tabletop game
right I mean this is right here it is a tabletop game so we could say it's it's a t it is a TBL driven uh development
because we're developing it based on a tabletop development that's a different kind of let's is hey Jonas astd welcome
folks uh just thought I'd show you an update of um trying to play around with with some mockups for what the game will
eventually look like um there's a lot to squeeze in and I'm trying to figure out uh a good layout this is okay I mean it
it looks nice cuz it has all the nice colors of the cards uh I also have to add in here um what's missing is uh the the
two counters so the counter the commits tracker uh and the um risk tracker so those things I need to include somewhere
uh I'm not going to use this layout um for those because this just happens to be this is a good way to to print a
physical card because I'm already printing cards but on the um here I'm probably just kind of have some some sort of
vertical counter of of of discs lining up um because I like I like it more than just showing a number I like to sort of
see something sort of growing over time um but that won't take up much space I mean that'll you know be something like
uh you know pretty much it'll take up something this yeah so that's about the the amount um oh so first ask about uh
would this game be something people who don't code could play um yes in fact uh when I was play testing it I was play
testing it with folks who are were familiar with with games um but knew nothing about coding let alone test driven
development and they they enjoyed it uh I just gave um my son a copy to play with some of his friends so we'll see how
how that goes uh but yeah totally I mean it's it's uh on on its own yeah sort of you know the terminology might be un
unfamiliar but um it has your you know game mechanics so something like that uh what it's interesting so so um figma
which is what I'm using to mock mock this up when you duplicate something um most other programs that I've used will
offset the duplicate right so basically a copy and paste in place um will offset the duplicate so you realize you've
duplicated it uh figma for whatever reason does not do that and it's it's kind of annoying it's like did it do it I
don't know let me drag it and see if there's another copy um so it's kind of kind of a little bit annoying um are these
not aligned what go actually I should probably just let it do the layout uh so there's there's code smaller so what are
these currently 32x and these don't have to be that far away from each other so let's let's align them and then uh
distribute vertical spacing tidy up what does tidy up do distribute vertical spacing let's see and out that that looks
off that looks be some actually there's there's code risk and there's cycle risk so the um when you're playing the game
the cycle risk is this is how much risk you can take on uh each time around the the board um you basically get that if
you if you pick this and you skip from here down to uh down to here uh you get three um the code risk is how much you
accumulate throughout um I limited it to five because that's all I could reason ably fit on the card uh I may allow a
higher limit um oh no of course I can't a level higher them what am I thinking uh because when you get to here commit
code you have to roll a die a six side a die that's that's the die here um and if you your code risk is at six you will
never succeed uh so there's no point in allowing for for more than so that's risk so something like that and for commits
um that's probably going to be over so we'll duplicate those put those here uh and we'll color those yeah so I'll need
another column of these but that sort of gets the idea uh these are are really squeezed I might have to squeeze them a a
bit more um and I still feel like the this is there's sort of wasted space here so there's some there's still some
juggling I I need to do um to to get this layout sort of done and done done where where I can uh start using this but
we're nowhere near actually we're we're I would't say nowhere in near we're we're not ready for for this yet but it's
sort of um something I you know I toy with you know when I've got when I've got half an so um yeah set of heart yeah it
would be nice if there was a way to to sort of CL and and say nope you can't you can't do that because that would add
more risk um yeah I'm sure these are not align so I'm that yeah they are definitely not align that's cuz this box is not
align with that one there we go now we're happy yes I was like ah I'm not going to fix that it's like no that's that is
itno that confetti uh celebrate is is is actually quite a long video it's kind of funny just keeps going um yeah and I
finally figured out how to how to turn it off so it wouldn't wouldn't go off every time I switched to this view uh all
right so let's um let's go to the code code that's the code so um where we left off last time let's run 20241 do2
preview hopefully that won't problems uh and so we said uh we were going to write a test to make sure it creates the
game and returns a handle for the game so um that's basically testing uh this code so we're doing outside in from the
edge of the system into um into the core uh right so basically you you come to the to the site that triggers this that
redirects you to the lobby um the lobby we basically uh we just show the lobby page the lobby page um allows you to
input a number as a as a sort of name for the for the for the game um and what we want to do is we want to take that
information and uh basically create create a game get the handle return the handle uh and then um when we go back to the
lobby we want to show again uh oh uh I turned off so you can turn off some of the notifications so it might have might
have turned off the um that create pull request I don't I don't know we'll see yes let's all go to the lobby I need to
have that as as a as a little that that's going to be the running joke of of this thing uh so but right now what we want
to do is we want to test for um creating the game and and getting the handle so let's go that will be our regular Lobby
test and look it's empty let's go generate a test uh host new game uh new game game with handle created new yeah when
I'm yeah it's like if I'm pushing to a branch then okay then then then a pull request makes sense if I am pushing to
master what what's the point it's already on master so what you know unless you're doing like uh non-blocking pull
request reviews then that's maybe that's useful um which I totally encourage uh instead of instead of uh blocking PLL
requests anyway uh so what we want is we need to well that'll work not really uh but that'll work for interesting that
it did this uh so I'm still using Cody uh as my uh AI assistant for for code I don't like how did it get that wrong I
don't know um because it needs a principal uh for now we'll pass in no maybe that's not great um what can I create let's
extract this create I'd like i' like to create something that is that which I can't do I mean I could do that that uh
which I'd like to restrict to I mean I could just make one up it sort matter for testing purposes this is probably fine
oh that's interesting it closing missed the close that's interesting uh let's replace that with a Lambda that's way
better um we'll probably pull this out fine seriously hey at least at least uh uh Cody's not suggesting maketo stuff cuz
that would that would that would be rage inducing yeah so kudos to Cody for not does um so what do we want to assert
well we want to assert a couple of things uh this redir to the that's not a concern right here what do we want we want
um so we want to create the games so we want to redirect back to this page and then we basically want it um in the
future that's going to change like again sort of mean maybe I'll like again as as a reminder this game is intended for
for teams who currently can't play the fysical game uh that they're all remote but that at least starting out uh the
these games are not available to just anybody who happens by um uh but um so you will not generally see the list we sort
of showing the list of games just for ease of development right now uh but eventually what will happen is when you host
a game what you'll get back is the handle and then a link that you can use as an invite send to people um and then we'll
have uh when we do the join game that um that link will will basically direct you to join game with pre-filled oh
interesting yeah testing principles yeah yeah yeah well all right so then what we what we need is we need um we need a
model here so we need it uh to put stuff in the model um except this is a this is a post request so it's going to have
to put it in the redirect see it suggests things that that are are not possible um like good good try uh but it should
have that's the second time that it said oh let me just instantiate the interface for you it's like no that doesn't work
um I'm trying not to to think of something else to do for this okay so we got redirect attributes where do we want that
uh let's put that here so redirect parameter and what we want to imports that's interesting I thought I had all those
all right I guess I'll oops I want to exclude all these because these one now you can just import the right um redirect
attributes has no get method about it's get flash attributes uh close it's not quite get name game name um so what do we
want these are going to well actually in this case no uh the get request is going to provide all of the created so uh we
don't want redirect attributes never mind I keep forgetting this is a post all we care about then is this post is is it
does something and then redirects the get request will uh will provide the the the information so never mind um I mean
we could put a redirect attribute saying game created but right now that will be obvious because the game will show up
in the I I love that that intellig is is basically suggesting do you want me to remove this parameter yes please okay
hey dudan thank you for the book CL and talking to a consultant at work and I'm the only person that knows what an
anti-corruption here is good for you uh that reminds me uh we're we're starting to talk about the next book for I will
uh uh uh state that I have a a very strong bias this time around uh uh no dark dark MO is uh is uh uh available if you
if you have the points for it um there you go you got to have the test points for does all right dark mode it is uh let
me just finish it is there what I want to know is is way know is I wanted I wanted to optimize Imports except for that
one like I wanted to always include uh uh my my assertj assertions let's take a look and then we'll then I'll turn on
dark mode um so that's just the warning that's not the actual optimize slow um it's not quite Auto Import exclude from
Auto Import but I want is the opposite of exclude which is like keep even if it's right all right well I'll have to
delete okay uh all right let's let's turn on dark mode uh so what do we want uh I always forget is it darula or youa
that's difference I don't see much of a difference oh dark dark is just a bit higher contrast uh let's go with that
Oceanic is that still dark oh it has a tinge of green or or teal sure let's go with timer uh all right so um so now the
question becomes how do we know that it does anything uh what we want it to do is we'd like it to talk to creator uh and
basically call create new game will so there a couple ways we could do So eventually Lobby is going to need a creator um
we could sort of there so if we pass in a game creator and right now G creator has no dependencies of its own eventually
game creator will have a dependency on um some kind of now who's going to hold on to the game that's created we could
stick it in lobby and then refactor our our way there um and then we basically call show Lobby uh and check that the
model has the game yeah let's let's do we um let's let's back up and start off with with with the base case uh so let me
it's really amusing to see uh uh Cody tried to autocomplete like natural language text um so we want to disable this
until uh show Lobby uh returns all right so let's now write a test that is um uh no games in model when no games exist
sure uh you're just copying and uh let's refactor this to um uh a constant and we'll call this uh because I'm a dummy so
we'll call this dummy principal um surprisingly uh it did not suggest can we ask it to uh where is it refactor bummer
like it should have not intelligent should have noticed that weird yeah I'm a I'm a light mode all the time because it's
much easier on my uh stigmatism um and I just don't really code late at night anyway uh okay so we create the lobby um
if we uh call show Lobby uh lobby. show lobby with dummy principal model variable um we can assert that the um now this
is what do we want the model to be if there games I think if there no games I don't care about the model I actually want
to page because one of the things that I've remove if at all possible remove any kind of logic and uh from from my time
Leaf template Pages um so for example if I basically have the situation like okay I'm just going to show Lobby and then
somewhere in the template there's going to be an if block or an unless block you know uh you know if if the games is
empty then show this basically else show this other thing that's logic in in the template and I want to not do that what
I want to do is I want to return a template that shows games if there are games and a template that says there are no
games if there are no games and that logic then is in the in the back end and that because that's easier to test so
actually in this case don't care about the model so much um so let's again uh we'll get rid of that we're not going to
assert on that and what we're going to assert on is uh uh view name and so what we're going to say here is that view
name is equal to Lobby um so the regular Lobby will show games uh and the no game Lobby which will be a copy of this so
let's make a copy of this well I can run the tests and I know how it's going to fail so let's do that so this will fail
because this um first of all this won't be that um and then it's going to complain because there is no template called
no game Lobby oh really did not complain uh oh of course because I'm not running it through the the spring the spring
test they would complain um so let's run all the tests and we'll complain uh so here it complains because uh the no game
Lobby template might not exist so let's fix that um say no games currently available to join uh and then this will be
that and that's what we fine yep uh and then we can run our our free test so those should all pass as well yep uh hey
Daddy depression nice to see you um is there a type safe way to use model or it's always a key value API it's always a
key value API um because it's a generic model uh sorry it's a gener basically underneath is basically because what the
templates are going to process is pretty much strings right so it can't be anything ways uh I mean this is you know it's
kind of funny this is why I I end up writing some tests on what's in the model and is it of the right type which is very
reminiscent of what do you do when you don't have a type system is you write tests in place of the type system um in
terms of having the key names and tests you could create a constants uh which I have done um where uh in your what's
basically your controller um you would have the the constants for for what gets put in the map and then at least you can
reference those uh everywhere so at least you have it's still not type safe but at least for the names you you have uh
consistent names I generally don't do that for no other reason than it it hasn't been an issue for me uh but that's
because I don't once I create those names I don't change them very very often um oh as has a potential solution for so
inspections so I don't see how inspections is going to work cuz inspections are just reporting um it's really uh uh
intentions um so that's just going to be ignored by optimize as far as I can add that so if we don't have usage of that
uh it's still reported as an unused because it's this inspection that's actually the UN the underlying issue um it would
be nice here to be able to say no leave it in there anyway uh so this one doesn't have have that option so if I do
optimize Imports it goes away I mean it's not a huge deal because um I have a a uh an auto complete that that Imports it
yeah is that the is that the bug I don't I don't consider that a bug I consider that a missing feature let's put it that
way um all right so this test passes uh so it's not no games in model it's no games um Lobby View exist uh so now what
we want is uh another method that Cody um in in this case yes I'm not sure Cody why you're putting in Extra Spaces uh we
don't uh we want to check two things so Lobby view shows game so we want to check the uh the view name um yeah out uh
but one one one one test at a on so uh let's check that this works cuz right now it's always returning this uh we'd like
it to return that if there are lot uh games this can't possibly work though cuz nothing in there in here actually shows
that we've we've added games um so we need some way to control uh the fact that that there are games um so this may
trigger this uh sort of I always think of this as sort of this waterfall of uh other things we we need to do so here um
we've got game creator which creates it but doesn't hold it anywhere so I think I think we're about at the repository
because we certainly could in in the lobby we could create some kind of structure for here and then say create the lobby
with uh with a game um but we we've we've done this before we know where this is going so let's let's just shortcut it
and go straight we could pass the repository directly in because it's just retrieving all the games and that's okay so
there's been some some uh discussion in in the Discord around can an inbound adapter which Lobby is an inbound adapter
access uh an outbound Port so repository is is an outbound port and so what that looks like from a hexagonal
architecture point of view let's see do I have one one so one thing I I really like about uh TLD draw is um not just the
fact that they've got the hexagon shape built in um but also it is correctly oriented it is pointy thicker um so this is
our our uh application inside the hexagon and what we've got hexagon let's move this down here uh what we've got is an
inbound adapter inbound and I'll make the text larger in tiny why is not the come on come on this so this is an inbound
adapter um the repository is repository um I'm trying you know I I've been finding that that there's been some confusion
over naming the port repository um I could call a game repository Port I don't think that helps um so uh one of the
things that uh some folks do um is is sort of give it a more like what's it used finder uh or loader let's try that see
how see how that feels um let's rotate this here so want we want some kind of uh application layer to be in between um
our adapters and sort of outbound right because this outbound should not be called directly by anybody case so that's
that's sort of the idea here um so the question then is is like can we sort of you know go around the use case and have
an uh an inbound adapter talk directly to a port if it's a readon port I actually don't have a problem with it um what
it depends on is what objects am I getting back uh I'm probably getting back games um the problem is is when games are
mutable then there's a potential for for modifying them um but in fact the repository that I'd really want here is
finder uh say Port uh for repository and adapter uh yeah I'm trying to trying to eliminate having the word repository in
both things like um the reason why is I am generally I mean I don't have to name it this way uh with the concrete
implementation so this thing over here um is going to be the you know game bbo Repository I don't have to name it that
way um but the underlying technology which is going to be spring data jdbc uh it uses the word repository and though
that name is really a DDD name and has a very specific tactical pattern reason for existing uh the yeah so so Alisha
Cobin uh uh does use this idea for I I've tried it out I don't like it um like I I don't I don't like it uh but I do
want the names to be a bit more concise because I think I've uh I want my ports to to be smaller um so this one would be
uh a game loader or something like that and there'd be other ones that would uh return so they would be returning
different kinds of objects so I'm okay with so all this is to say is I'm okay with the inbound adapter um uh accessing a
port that is returning um because then there's no chance that it could could make any state changes because all state
changes right the layer that's that's the rule the use case is the thing that decides and then makes makes State changes
um so that means that the inbound adapter can uh access the game loader Port as long as fine um how I enforce that is is
actually a bit of a of an issue uh there's probably some way I could do it with Arc unit but I I I uh I cringe at
thinking how complex that that rule is going to be hey live coding with shelp uh ran to that issue with spring data jwc
unfortunate naming yeah yep y y yeah yeah same here and and I've I've um I've actually had to throw away some some
videos that I'd created for for my course um for that very reason that it was confusing to see like repository used in
in three different cases it's like which thing am I talking to so uh this is this is sort of where um that's what we're
going to this okay uh so all that was to say we need a we need a port um we need an implementation and in memmory um
yeah that's that's what we need and here I'm creating an in-memory implementation not just for tests but when we start
playing around with with with the app um it'll be nice to to have that to to play with and it's very flexible uh without
committing yet to uh specific schema even though I think the right so what do we want to do Constructor uh I think only
tests call this so we can convert this to a factory method um and we're going to do uh crate null um we will retain this
as public because it's a controller so spring needs to be able to instantiate we want to be able to create an instance
of I kind of don't want to return right because we want this to be value objects game is really an entity uh so I don't
want to return games what do I want to return well what do I want to see on the screen what I want to see on the screen
for oops for the games uh that's the no game Lobby I don't care about that for the game Lobby um what I'd like to see uh
so here we have to now go go back um to the uh to the to the view what do what do we want to see here um we pretty much
want to see uh yeah game name uh and game players so I think something like that yeah uh live coding Michelle asks
what's thetion going to be in my currently um uh I think that one actually is away um no that one's going to be similar
to the assertion I'm going to make here it's going to assert that the that the game I have created with the post uh
shows up in in the view here I want to I'm going to prefill the rep the the port repository going to prefill the
repository with with with a game uh and I'm going to expect that that it's in this model so that's it's there do I see
it this one will be if I create it through the in a sense the API uh the UI uh does it so do I want um yeah so I want a
dedicated repository for this what am I going to call it though loader because what do I want to call readon versions of
this I mean I guess I could loader because these are basically just game they're basically po the're they're basically
uh dto I was going to say pojo but that's wrong yeah I find presenter too long a word view um and to me the presenter is
well I guess he calls it interactor I I don't know I don't like his terminology uh so let's call this game view loader
um it returns game views uh and there's going to be underlying it there's going to be a game um so game view is going to
have the name handle what does game currently have uh currently has name um so we just want to create a lightweight
version of it uh so that's what that'll that um sure model is uh views uh let's let's go right to contains exactly uh is
it going to be a list it's going to be a exactly uh can I give it a parameter say of yeah that's what I want and this is
going to be list uh oo that was kind of nice um why is this having trouble importing this that I feel like I've lost
some of my Auto Imports because I never I usually that's that's an Auto Import so then game view let's go create this um
interestingly enough this is a domain record uh so it will go in domain no not API uh so as instance of requires um an
instance of aert factory I don't assertion want I I so rarely use this I I uh I have this I I discussed this one in my
um aarch a presentation which at some point I will finish editing I hate editing videos like it's it's like the most
tedious thing in my world which is ironic because I do a lot of videos um but editing videos not my strong point uh so
this will contain exactly um for now we'll just say a new game view good try but right now game game view doesn't doesn'
t no it little overeager there Cody um want so now the question is is is how could those games possibly get in there now
we have to worry about where do they come from so now we have to go and um but let's run this test this test is going to
fail because the map's going to be oh uh yeah so actually it fails because right now we're always returning that uh so
that won't work here because game views is not a method on the map it's a key in the map and the map is as we've seen
before is untyped um so that here um yep yeah it's yeah otherwise I I I use the function uh and there are ways to use um
I think actually I can actually pass the here uh I don't know if that's more readable right so I can do this uh and
basically get rid of readable um one of the things I like to say is AER a sear has has uh more syntactic sugar than a
than a than a 5B bag of sugar uh it's there's so much well you can do it this way you can do it this other way you can
do it this other way you can do it in three different you know in in in 23 different ways uh so here it it basically
combines both of those so I can extract it it's untyped and then basically say okay now it is of this type um I kind of
prefer to just stack them uh because I think it's a lot more clear um yeah all right so um writing this writing this
assertion was was interesting but actually not useful yet because we're still stuck at this is not working so let's get
this to work um it a game view that it's going to return so let's do that um we'll just um return a new Lobby uh but
this time what we want is we want to uh create something that will hold the game View and so for now we um creating the
the repository by storing it inside the lobby uh and then refactor our way out so let's do so we're going to do just the
simplest it views now why is it suggesting an that was kind of odd that I was suggesting arrays um for two reasons one
is who uses list all right uh we actually want to do all of fail and now what we can do is we can say uh so return
switch on empty uh and now uh what no I thought I was going to add false what's a complaining about selector of type
booing is not allowed oh that's right we don't have yet all right Jonas thanks for hanging out um all right well I guess
that that was just so if game views is empty no else return and then clean that up Turner yeah Turner is fine now pass
uh at least we'll get to here um we uh actually this should totally pass because we will have game views there one uh
although we're not putting in the game view so this will this will still fail because we're not putting in the right so
uh unsurprisingly that failed model uh so let's do that so we'll add um no there's no there's no refractor here uh not
yet um so my policy on uh sort of looking harder at refactors is when uh I finish either uh a a command query pair or a
01 many cycle um and what I mean by command query pair is uh have I finished the ability to cause state to change and
then see that state change and then I'll look for for factoring um here we've only done the the query part right so we
can query for games and they are showing up um but right now we're not able to modify uh Pro you know from the UI we're
not supporting yet and that's what this test is all about um once I once this test passes then we'll look at there'll be
definitely some refactoring to do like extracting uh a port hey swegi um so let's do that yeah so like the the the simp
sort of simplistic uh heris of tdd is you know red green refactor uh which is fine um but sometimes that can cause you
to either refactor early uh which means you might refactor in the wrong way so the sort of the two heuristics I've come
up with is is the zero1 many um then really look at refactoring CU you've probably got now a structure to do uh or
command query is is uh the other heris stic yes and my Reds are are are different shades all right so uh this now works
so um host new game is a post request uh to create a new game uh assert um that when model yeah I mean the four rules of
simple design are are when you're looking at code what are you looking for um the question is is when do you look at
code and so I don't look at code at I I don't take the time to to apply the principles every single cycle uh because a
lot of times like there's nothing looking uh we don't care about the view that uh feel like I'm going to do this
assertion a lot so let's uh and what we want to extract is that much that's actually what I meant to do and then I
realized that's you all right so now what I can do is I can assert that model uh contains sure which means we're going
to need to modify the record uh to create uh to have the information we want what was the information we said we wanted
uh the name the handle and the players but we'll need at least need uh that property so let's add that um why did you
not make this dialogue bigger uh let's see so this will fail because we won't have any games in there I'm just thinking
should I add the other properties no I'm not going to add them just yet uh okay so now now we got a test it's failing
for the right reason uh now we can go ahead and and fix it uh um yes we'll do that and um clearly we're we're
shortcutting uh the process yeah Cody's Cody's certainly doing better than any other um I've only not that I've tried
very many other assistants but it's doing it's doing pretty well just don't ask it to to do Spring Security stuff which
they already they uh they actually uh Source gra actually responded uh and said yeah we we'll we'll prioritize sort of
using newer ones all right I'm going to take a quick break and then when we come back uh we'll um look at some
refactoring um which will be mostly about uh this list of Game view is is insufficient um that and we'll want to we'll
want to pull that out um actually I'm not sure we'll take a look uh but let's take a break and I'll see in a few all
right and we're back uh so the video pauses whenever I switch away so OBS has has a wonderful feature where if you set
up a scene um with a video you can tell it to uh not restart so it'll pause when it goes off screen uh when it's no
longer on scene um and also that it that it will Loop so that way uh you get to see all parts of it yeah cuz usually you
don't see the the actual end do uh and yeah like it's it's hard enough on on humans to to to figure out what is the
latest in Spring Security because even the code examples in the spring examples in the Spring Security repository are
outdated um which I really kind of think is inexcusable to be quite honest I think it's your project your examples are
the ones people look at and they really need to be up up to date I know it takes some work um but like you know that's
kind of the uh so live coding with with Shel uh talks about um my extraction my extraction wasn't about type safety my
extraction was about reusability and abstraction uh and removing noise um given the fact that I'm building on uh code I
don't own which is basically the model and the concurrent mbcu uh I am basically Bound by and limited by by that so I
therefore have to write code that that makes it easier to do what I want so um true it is a a Lobby Model uh and true
model is an interface and concurrent model is extensible um but in reality I don't control the model that gets created
and passed into these methods so that doesn't really that's not a a extend right so if we look at lobby lobby is a
controller this model here and this principle here those are injected by by Spring boot by Spring I have no control over
that um my tests do have control over that uh but I can't just pass in any any model because I need to match uh as
closely as possible do if it were up to me I'd be doing stuff very differently but uh I'm Bound by the framework that
that I have selected for For Better or For Worse uh I hope I understood the intent of what you were saying saying if um
there's nothing really forcing me to uh to refactor because there's still no connection um between the lobby and the
game creator right so we I mean let alone connected to any kind of you know we sort of simulating the the repository uh
the port with the game views um but there's nothing that is actually connecting it to to actually creating games uh so
um we need something that will guide us to to talking to the the game um that we need uh we need to get a handle on the
handle and we need to uh also yeah I think that that would be sufficient to to drive it um there's something about that
that feels a little little artificial uh on the other hand we do need to show because we said that's what we're going to
show here um this actually requires that those let's uh actually let's let's run the app configurations okay much I just
cleaned those it I must have hit enter or I must have hit Escape yeah all right let's try that all right uh so let's why
is it not asking us to log in I still feel like there's something wrong security so I'm not sure model attribute works
that way because it's an attribute it doesn't control the the model um what it what I thought thought you were
suggesting before is creating a custom model that would be more accurately more precisely typed um but does so when you'
re working with restful apis then you're not using Springs model right because the model is is the MVC stuff um when if
you're doing a rest FL Epi then you can have you know the concrete types that that you'd like and then it'll it'll
transform this appropriate um but MVC is using a generic model that is basically string toob mapping and again I you
know there may be some obscure methods to to make that more type safe um but ultimately they get converted to Strings by
the template so I'm not sure not sure I I see much not all right let's log template game and now it's showing the other
template which has been hardcoded to show this so at least we know that works uh so somewhere underneath there there um
do I figure out why what I've got set being why I'm logged in but I'm not logged but there's no principal I don't know
that I want to yeah like clearly I was logged in no sorry clearly so clearly I was I was authenticated uh but there must
be something I'm I'm missing in the configuration and it was a temporary configuration anyway so I'm not too worried
about it so I'm not going to spend any time on that um okay so um that was mainly just to see like does does this code
work as expected and it does uh so what we want to do next is then um display actual actual games uh so let's do uh do
an unordered list um and then this will be a each uh do I want do I want to just do some spring some spring some string
concatenation here or do I want to have separate spans for for let's do concatenation for now so uh game view. game what
did we call it is it game uh I forget how to do string name uh and then just ends with a pipe yeah okay oh that's great
um thank you once once I guess I gave it a little nudge did the right thing um I don't like numb players uh player count
is what we'll eventually call can have that we'll delete that so is that going to look okay now all right so then we're
going to have to add some information to our account all right um I should not have doing uh so what's interesting is is
that once you're in one of these dialogues um no none of the a AI systems are available which is too bad uh so this is
going to be a string uh handle not gandle is uh in uh player count uh default value is negative 1 all fail I don't think
any should fail I'm not relying on any of that information I don't know why it was suggesting additional parameters here
fine so there's going to be no way to predict uh the handle um so that will require us to uh dependencies somehow yeah
that's when we're going to have to inject the the game creator and we're going to have to have game creator we're going
to have to have control over the way it generates handles um but for now we expect that when we create a new zero uh
this will fail because I think by default wherever it's created it gets negative 1 and I tests correct so failed exactly
as I expected uh let's go to yeah so so this is problematic because uh we should never be doing this so games get
created through one mechanism M and one mechanism only and creator uh in fact what I think I want to do here is um what
do I want to do here uh oh hey Hank pink handle really I want to say the handle empty I don't know if this will do it uh
let's just do first and then oh I lost the type that's the problem so this now um I need to so will this get me what I
want uh it yeah I'm going to then have to drop down a layer to test this uh so this empty all right so what we're going
to he so now what I want to do is on game creator uh somehow when you create a new game the whatever represents that
game view loader yeah I don't know Cody likes mocking Because the Internet likes mocking uh where did my oh here it is
so our game view loader will be there's a bit of of uh cqrs going on here because game views are readon uh but I'm going
to be modifying games so that's interesting I don't think I've a so create new game if I then ask the uh the the loader
for game views uh it's going that I don't know if um let's let's try it out let me do a I don't know where it comes up
with some is so yeah we'll create a game View game um and now we have to ask something that doesn't exist which is uh
which is now our asserts that gam view loader Dot um find contains do I want find all returns am I going to have find
all returnal list yeah then we'll do uh uh get first that's going to be a game view um and we're then going to say uh
name is equal to game so create a variable uh which is going to game view exist but sure create one uh that's going to
go up here now we'll create this class well we'll make it a class for now uh and then we'll extract uh an so create a
method find all view uh when I extract the interface that's what I was thinking of putting it in Port um but I guess I
could put it in Port uh in fact I don't even have to do that I can actually say uh contains view of uh yeah hey thanks
Cody uh except I think you've got it reversed you were so there we go all right so this will most certainly fail cuz
game creator has no reference to game view loader I mean I can run it but we know it's going to anyway um we can return
an empty list that doesn't matter it'll still fail because catfish lovely catfish um so now we need game creator has to
have access to the game loader uh Hey goat goat meal is that how you how it's pronounced with the welcome um so let's
pass in a game view loader do think we want to do create so Place Constructor with Factory meth let's replace
Constructor with fat I that's interesting you don't have to have a Constructor to to do the create what I've been doing
is creating a blank Constructor then creating it from there but turns out you could do it right from here that's kind of
cool um so we just want to say game we just want to say create uh and then what we want is we want to create it takes a
game view loader so we'll create another method and then we'll go and add that as a Constructor parameter uh that's fine
I don't think that'll way hey go yes uh very few of us Java spring streamers around uh who's going that's somebody else
um eventually it won't be the game view all right live coding with shelf thanks for thanks for stopping by have a great
rest of your day um yeah game view loader is is read only uh so this is you're right this is not what I want I got a
little carried away um what we want is not a game view loader want um we want a uh I've already got some problems crud
um uh so I intended for I intended to to be using events it yeah it's it it's like better now than than later but uh
game has some State and I haven't it um what do I want to do uh yes hexagonal spring Java what more could you want um
let's see what are my options uh so one option is inmemory cost uh that sorry that avoids my loss aversion um or I bite
the bite the bullet as it were uh and convert game to sourced um I don't know if the events would help me create the
game views uh I think it would actually make it to update the game views right now now cqrs CU my uh store is not the
same as my game PE loader so game uh in fact this is Java 22 not just Java all right I got to do it sooner or later and
as much as I want to get more uh get get get to a walking skeleton with the UI um I think the more I delay this the all
right so uh we're going to have to disable this test yes Cody that's true but that's not all right so don't need that
test uh I might need that test won't need that test jira uh this is actually still all right so what's what do I need to
do for for vent sourcing uh the first thing I need to do is um is I need a static method uh game um and I'll need a uh
game event interface why is that was weird uh oh I bet I bet Cody's Auto Complete was screwing up the the uh the rapping
are we aborting this Sprint um well we're we're abandoning the stories we were going to work on which was basically all
about this stuff uh and so we're no longer commands generate events event events Mantra so commands generate events
what's the First Command the first who creates the handle is the game creator uh so that will be a sign handle uh yeah
and so I was actually about to refer to uh to Blackjack uh so let's look at uh how we um basically this a map of
whatever our Class um this is our our storage mechanism event dto which may as well start there um and then it's the
base class for the event so we'll need that uh and then of course we'll need our it our vent sourced aggregate this
thing so this thing I can pretty much repurpose um hold on I've got too many windows open uh let's close this one uh
we'll close this one keep this one open okay uh so uh I need an event sourced aggregate I guess technically it is the
aggregate route but that's fine uh generified by so let's see so what what did our test look like uh so this is all
about loading events having events remembering events that um but I want to start a little bit account and so what we
had here uh was commands generate events and events project state so this so it's basically a test like this we create
the thing with its initial whatever um and what we get out of the fresh events is that event so it's going to be
something like that so let's that uh so let's go here uh and we're going to basically uh so this isn't going to be
player this and generif it later maybe and it's not register um but it's uh name Cody you're very confused but I don't
blame you uh and then these are going to be uh game events uh and this is going to be uh game name X proof how to decide
if a value object is worth creating or not can't you go overboard the value objects I don't think I've seen code bases
that go overboard with value objects that's one of those things where um I see two I generally see too few value so I
generally create value objects if they have if they're meaningful at all um especially if they have any kind of
constraints or ES and and certainly have any kind of generally uh I think only have regretted sooner all right so let's
go create some of these um create is this going to be a class right yeah so I've got player interface game event throw
that over there um so one of the things I wanted to pull in was um was J ules for some of the domain driven design uh
tactical pattern annotations as well as the Aggregate and entity ID types um I don't know if those are going to sort of
cause some conflict with my aggregate so let's go create our event sourc aggregate um and we're going to need at least
one did we make these final oh we made these okay um game created takes a name so sure that's fine um we need this
method but we're not going to implement it because this will test uh o that's why that what is it saying now oh okay
yeah um so this what I want so creating event and then what we'll do is we'll switch over to it it's Event Source
agregate test I want this so this will be uh uh new game name yeah all right astred have a good night know it's getting
late over there in UTC plus land all right so this test will certainly fail because we don't do none events so we're
going to get it exception yep so game is null so let's at least do that uh commands generate events so we want so we
basically create the thing uh and call a method and then return it uh and of course we need to extend that so we're
going to extend event sourced aggregate uh and then this is going to uh we're going to game right oh we're just testing
the events so okay we can be General uh not sure about that uh so Constructor uh eventually this Constructor is going to
go away so let's deprecate it uh so now we're going to get a different failure so we'll get to line 29 fresh events we
won't get a null pointer exception on retrieving the fresh events uh uh we'll get the null Point exception when we try
to evaluate the events then right so now events is null so let's go events um so now it will fail because we uh was it
suggesting apply well done Cody you've seen some some event um except you put it in the wrong place because we don't
apply here we create the event so uh and then we want to in enq that um wait but that's in the actual method so let's
pull that out uh so oh we're in a static what are we doing here uh so I need uh an in work and mean q is in our Base
Class what I want to call this crate I guess I could just call it crate and then hand name uh but it conflicts with that
one uh Q uh will be created so create the event so event uh and we want to create a right all right uh let's go ahead
and implement nothing Cu uh that will be test driven State new actually should just be create that's redundant create so
create it with a name the event we expect is that right all right so that works um um and we're not going to have IDs
just yet we're just going to have events uh and that should result then in game name being equal to T okay that's what
we want uh we don't currently have a reconstitute exception uh could just return a new game and that will just mean the
name is here so we have another Constructor uh whoa I didn't want to change that I actually uh we don't need to call
Super yet eventually we'll need that them feel like I'm writing a lot more code for this t test than perhaps is needed
um but I think I'm okay with that because I'm copying sort of adopting code that that that works uh did we ever fix the
don't call abstract methods from The Constructor uh uh we're doing it here in in the concrete class it may become more
clear how to how to do that uh when when I have more Aggregates I I I don't know uh so X proof asks which class has the
most amount of parameters I'm not sure what you mean by class having the most amount of parameters are you saying class
having the most amount of dependencies or something else um so we're doing apply uh but we're not applying anything so
that shouldn't really have changed to uh so now we get to actually apply the event which is basically a switch on the
event uh that's interesting it's like let me create let me make the player joint you that that's nice sure um we don't
have these things yet uh but right idea um the handle though uh we don't create here uh who assigns the handle handle uh
so parameters for Constructors are dependencies and that's why I was was wanting to clarify it so you're you're uh so
usually the dependencies they not always um uh probably the most I have is probably around five or six uh I get
uncomfortable at around five or six I think seven is actually way too many in terms of actual dependencies you might be
passing in more parameters um so I'm fine with maybe seven parameters as long as they're not all dependencies um but I
think a class having even five dependencies is is is lot uh oh and we can get rid of succeed and it that's correct um
and generally uh in your domain I don't consider parameters to con Constructors generally they're they're almost are
never dependencies right so in inside the domain it's all pretty much value objects uh that's a that's a good point
right like um even though this Constructor goes away these are all value objects so inside my domain I would expect
Constructors to either be value objects or other entities in that graph of objects that aggregate I would never uh and I
explicitly would not want any kind of dependency because the domain objects by definition cannot be dependent on
anything outside the domain be there might be some cases where you might rely on something but I'd be really suspicious
of that so the so my general rule is doain objects don't have dependencies uh only uh adapters and and uh use case
application layer have dependencies and specific adapters um then I try to limit it to like five hey 10x developer no
this is not a worked uh X proof acts does domain object represent real world thing world uh uh but it doesn't
necessarily relate to a physical thing uh which is where where where some folks get confused uh I know I used to um but
it you know your domain is literally a model of the world that you're trying to you know the small Part of Your World
The subdomain you're trying to model uh in in your code hence domain driven design right what is the domain that you're
in is a model of the world that lists all right so we've got creating game emits game created event uh the to do I want
to create a game without a yeah I don't think I want I don't think I actually want a game to be to exist without a
handle why would I ever want that yeah I mean real world is kind of a like what do you mean right I mean we're not
generally world right I mean this is and this is the problem I have with with all of these uh intro to to
object-oriented programming um you know we're going to have a a a a dog that barks you know when when you ask it to
speak and a cat meows and and a cow goes moo and and you ask them to speak it's like no we don't um we're not simulating
you know uh a barnyard right unless we are and if we are then great then then that's what we want but generally we're
not yeah um so unless you're writing a simulation and some games are very much simulations and you will then see
physical objects represented in your code in in a very in a way that that makes sense for that but most of the time
we're we're we're modeling information systems and we're modeling information uh and what it looks like and the code is
not at all what the real like yeah I was definitely going to G to replace this new game with um with the new Constructor
but I was wondering do I want the handle to be there too and I think I do uh I also want to delete this uh and get rid
of this and get rid of this for now who's calling this um I don't think that's right get rid of that uh so 10x developer
um yes aggregate will it will have an ID it doesn't need yet since we don't have any persistence I don't need my IDs so
the the other question is is when I have a game created event does it have two not yeah that well I mean the handle is a
um what's the word it's kind of a surrogate key uh because it's the one that will be used in in links so it's sort of an
external key um but it's sort of its true ID in the database will will be one that's generated by the by the database
yeah I don't know if I want to emit two events like it's a game created here's the name here's the handle the handle
will never change um but I think the I think the event it like if I were reusing other events then like it's almost the
other way around like uh you want to create it with a handle and then give it a name but a name is required anyway yeah
I I think this is fine yeah uh so let's go back to here and there we expect exactly that and and we'll go ahead and add
string as a second record component um thank you for creating the handle I don't think I need a default CU I don't think
I'm calling it anywhere else why are you and this do handle equals handle thank you Cody uh I think this a pass oh what
right look at that all passed all right um I I don't think care trying to think of an instance where where I care about
that okay um what's next uh so creating game emits game created event what else do we do to a game um we have players
that join so let's do uh method that is the method what oh because it's an event uh yeah I think that did that we did
that here but really it should always be game oh nice uh clearly we made a um I think this is actually more appropriate
uh so this needs to be a person ID so I don't know why you're suggesting a I don't think I care about well actually I do
um so actually don't care about the player in this um uh so this is player Jo new player joined so player joined is the
only uh oh right I want to reconstitute yes thank you I was wondering why this felt here we actually used register
tracking sort of stuff we didn't we didn't need to track game sure all right so let's create the player joined uh that's
going to be a record and that goes in the domain but that was very handy need so this will fail because it won't
generate the in a sense what I want here is sort of create a fresh object thank you Cody um so we generate the event um
oh uh I don't like that how about do okay yeah I don't know what Builder we we need to just yet hey there mono monel uh
what do I think about lib GDX I don't really have much of an opinion uh even though I'm creating a game it's it's not a
it's not a an action game so I'm not using it's not a desktop game so it's not not using lib GDX I've heard good things
about it but I have have no strong opinion on it all right um so now we need to modify join uh so I'm curious how we did
this in blackjack um good we did it we did it correctly CU I was just reading uh some stuff about uh events and like you
always generate the event when you apply it that's actually when you should check if you should if you should do it
actually uh well I guess we couldn't have done it wrong because we actually don't imp we don't we didn't Implement any
constraints in our player account um like money bet uh we actually didn't check to see if you had enough we yeah we
didn't but anyway the right way to do it is you generate the event um and then when you try to apply it um now that's
from a general event standpoint from a from a event sourcing standpoint though yeah from an event sourcing so event
sourcing is is is different from sort of uh event driven so event driven you might generate an event uh sort of like
player attempted to join um but that's if you were sort of Distributing that information from an event sourcing
standpoint uh yeah exactly because the the the player did not join so because what you don't want to happen is is you
persist the event uh and then you can never load it because it blows up every time you try to load it right so if we
basically said um generate the event no matter what here and then you tried to reconstitute it and I tried to apply it
and would be like it's already full what are you talk about so hey there bny welcome testing these were testing through
the use uh well no I don't have to break it I can generate the event as well as store it in the player map that's fine
applying that's going to be interesting all right so let's do that we'll assume if we got to here we can we say um how
do I want to phrase so this I don't want to create a fresh game love how Cody seems to be adding new places um so now
what we want to assert is if everything's reconstituted correctly we should be able to say that um players uh contains
exactly uh I don't think this is ID uh it needs a player ID uh where do I local test yeah all I cared about was they
null yeah so I didn't actually care uh uh so we're saying if this is reconstituted correctly this is what we want um
which will fail because we're not reconstituting it correctly it won't have any players yep X pro do I have any opinions
on not null and nullable annotations uh yeah I think they're they're useful to be honest I I'm I'm kind of hoping that
that uh the push for for consolidating and um sort of standardizing those because there's like five different variations
of them so there's the um I think it's specify J specify dodev yeah uh I'm kind of waiting for for this to to move along
a bit more um so one of the folks behind it or at least involved heavily in it is uh Kevin Buran who got laid off from
Google and is now working for Oracle um and this is one of the things that I believe he will continue to to work on uh
so I don't know if jet brain supports the ones that J specify has standardized on I honestly haven't haven't looked um I
don't know what its status is uh so yeah that's that's what I'm I'm kind of waiting for for this to to stabilize a bit
more before before I I start adopting it uh everywhere um when intell basically generates it for me I basically say yeah
that's fine um this is irrelevant so in fact the whole thing is um uh actually I want to reconstitute the whole thing um
yeah I saw your question sorry I I want to get something out of my head first here yeah the the reconstitute is the out
that and I still don't understand why so uh X proof was asking why I don't extract strings like this um because my goal
is uh if you saw this test completely isolated on its own with no other information it should be completely
understandable why you're asserting what so particular if you just looked at this test um what's the point of extracting
a string like this I want to basically see that oh this comes from here and this comes from here and I miss spelled
handle so I tend not to extract relevant information from from my tests if it's irrelevant like I did here then I
actually don't care about this whole event so I don't even want to see it inside of my test this is a little noisy not
terribly so um if I do this a lot I might refactor this out as well uh so let me know if that didn't answer your
question X proof uh our tests are failing because we're still right so let's go fix that um I think applying is
basically the uh player joined player joined uh hello player joined I need um actually need I don't care about the event
itself about that isn't player join give me do I not have that in the event sure I do oh that was weird it was red for a
while okay uh then that I guess technically I don't need the it but you keep wanting to put it on the uh am I missing a
brace oh it's all the way over there okay I'm going to keep you brace because you keep the formatting in line yeah so if
there were more complex pieces I might create variables but I tend uh but but if I don't have to then then I don't but
you'll see sometimes like I'll have you know first player and second player like I do in in this test um like this one
right I've got first person because it represents an object that has some stuff in it and so then do things like this so
but generally literals if I'm testing against literals I I often just leave them do I use test build data Builders and
object mothers uh yes have you not been watching me over the years um uh yes absolutely but I uh I use them when I need
them so I have this handy diagram which I really should formalize and write an article about uh what I call uh the
ladder of abstraction and tests all right so first I start with Factory method inside the test class right when so when
I'm encapsulating setup or or assertions I'll do this um if I start needing to use them across multiple test classes
then I will move them uh to a separate uh to their own class um uh and then if there's lots of variations then uh then
I'll move to a test data Builder yep so I don't like to prematurely Builders when I don't quite know what what what they
what I need right so the typical yagy um yes certainly Factory methods will have will have some kind of defaults because
the idea is uh I mean right here there's a fact there's a factory meod the default is that there's already a there um
it's when you start having these it uh bnie asks about any book to read not off the top of my head I recommend uh asking
asking again in the Discord um and that I'll have a chance to to do a little bit of looking around and maybe some other
folks have have some thoughts um in terms of hexagonal and there is a book by uh uh Alan Miller that I have not read
deeply but I've read enough where it's like this is this is uh something I I could recommend um uh I'll I'll dig up the
link uh uh I don't I don't think I don't think he uses event sourcing uh I'm like 90% sure um so I off hand I don't
think I know any book um if I ever write a book it will but that's not I've got too many other things going on so that's
not in in the near future all right let's commit um but yeah please ask that question and the Discord cuz uh I'm sure
you're not the only one who' like some answers in that's all the state I currently handle uh so now we need to go and
this which is game creator right so now instead uh game do great does that break and who else is using it this well well
yep and so now I think we can delete right uh moved unded okay uh is this on my GitHub yes um it is uh and it is which
is not an open source license so you're welcome to look at the code uh read it ask questions about it um but there are
are limitations uh so just want to point that out that almost every other repository I have is is open source under
either an Apache or an MIT license um this one is not uh and why because I will be charging for uh for this game so I
don't want people pay all right um what else do we want to of um these are fine these are fine these are all queries so
these are fine this is a to not do this anymore cuz return in queing the event should be sufficient ER this also kind of
violates command query separation uh hios did I say hi I'm doing well how are you uh so cqs not is not to be confused
with cqrs so cqs is command query separation cqrs which Cody already knows uh is actually command query responsibility
segregation these are two very different things they have the same common idea of commands change State queries fetch in
Fetch State and for cqrs they are basically kind of two separate pipelines to to modifying uh and retrieving information
so two separate basically a read path about good o good object-oriented programming um comes from hey Cody knows beron
Meer so uh ber Meer in his book objectoriented software construction which is available for free by the way um this is
one of his fundamental principles so cqrs is my one of my fundamental uh one of my fundamentals for object ared
programming one of so what it basically means is that query only query they don't change state so when you ask an object
for information it should not be changing any state observable State you can log all you want that's not observable
State that's not changing the state of the object you can create an audit Trail that's creating data somewhere but is
not changing the state of the object so asking for name doesn't change anything asking for handle doesn't change
anything asking for the anything asking this question can a player join doesn't change any state this is a command um
this changes state it's actually a request to change state it may not change the state the fact that it returns player
violates one of the principles of cqs which is commands should not return data now there are exceptions to this rule um
and so it's it depends on how strictly you want to follow it uh so for examp example if you have a stack and you do a
pop you would like to get the value that's on top of the stack because otherwise how do you get it um often an
alternative is you do a pop and then you say what was the last value popped um but commands returning state are are uh
are not following cqs in in 99% of the cases I am uh I have commands and queries and and their s seated there's very few
other than stack there's very few examples where that's required now this only applies to domain objects use cases are
different um use case application layer Services those are different uh adapters are different the reason why is uh
often it also doesn't apply apply to Creation methods um this returns a player because it actually creates a player we
actually create a player right here and so um it's not great I'm not crazy about it uh but sometimes you you need to do
it um in it's not really necessary here it was convenient but it's not really necessary because I can always look up a
player by their person ID so that means I can always ask the game after I say join oh hey what was ID um so it can
sometimes mean that's a uh but if you but the the the real reason why you want them them separate no uh are use case a
DDD concept well they're sort of implied um like how do you come up with things that your application does use cases
Alistar Coburn just published he hit the publish button on two books um one is his view since he invented it of
hexagonal architecture I've not read it yet I've read pieces of it um and I think more importantly at least for me uh is
is a book on on use cases There is almost no reason for you not to buy those books bucks so uh store so uh unifying user
stories use cases and story Maps uh use cases certainly 100% precede domain driven design domain driven design was
written in 200 early 2000s published in 2003 um use cases go back to I Jacobson and Alish Coburn wrote some books on it
we're talking late 80s early 90s uh so go ahead buy those two books they're eight bucks each why wouldn't you um I've
seen some some excerpts from from both of these uh so you know it's not through a real publisher so there might be some
things that need to be you know edited uh but it's Alistar Coburn who who who knows this stuff like few few do all right
uh so C says had an interesting discussion with some co-workers question was suited for product that are data domain
yeah yeah the mug is funny um so is there a domain is there and the way I look at it is there things that happen that
causes other things to happen or information to change um there may be no business processes uh uh and so if there's if
there's nothing you if you just collect and organize information you don't do anything with it in the sense of you don't
make decisions based on it right decision- making is what behavior is um then you might do some sort of lightweight what
are our models basically what are our data models uh but other than that yeah this there there's no domain um you know
this is usually referred to as an anemic domain but that's it's only anemic if you actually have behavior that is is
just expressed elsewhere so if you just collected data so like a grafana like collecting metrics um if you're not doing
anything with that information other than maybe then hexagonal is not going to help you uh any of the separation of
concerns useful however it is a slippery slope um because now if you want to start doing things like alerting like oh if
this metric goes over this in this way uh now you've got logic and you want that to be testable and now you better start
having things more separate um but yeah if you're just collecting from a bunch of different sources um consolidating it
transforming it into some maybe some standard standard format and then just displaying it or storing it maybe handing
out to some machine learning that does the alerting for you so you're not actually your code isn't making those
decisions then yeah then then you don't need all the separation of layers um the stuff that's that's making decisions
though that's a domain that's Behavior Uh and that that I'd want some separation so for me it it always and how I ended
architecture is basically one reason testability when if you find that things are hard to test because like GH it's
making a decision on X but I can't control X from my test you have a problem and makito is not the answer you need to
provide that separation um if it's like G it's so hard to set this thing up to set up this test so I can get the thing
into the state I want if it's hard to get the setup done so you can get the thing into the state that you want so that
you can assert on some outcome or output you have a separation of concerns problem it's like oh I can't do that because
it's getting this information from here and I don't have control over that it's it's always getting it directly from
this thing if you can't control it for your test you have a separation of concerns problem and hexagonal clean onion
whatever they are they are separation of concerns architecture they separate things so that they're testable if you look
at hexagonal I have to go read his book um and see see if if if Alis remembers the reason he came up with it which is
testability is the primary concern of hexagonal architecture that's why he wrote about it and it you know it bugs the
heck out of me the people talk about it as about oh look you can replace the database it's like no I don't want to
replace my database that is not why I do this I do this because it makes my code testable I can substitute test doubles
where I need them I can use the real thing if I want uh when I want to but I to uh so proof asks should all application
have some sort of model yes so there's two kinds of models at least um the way I think about it there's there's there's
basically two there's a data model and there's a behavior model what sometimes is called an object model if you've if
you're doing crud with s of minimal validation that's a data model I type this thing over here I want it stored in the
database so I can see it over here you need a data model you need to Define what does your form say which right if you
know if you have a very simple order taking system it's like you have a form what would you like to order I mean I you
know I think about like in the old days you'd go into a store and you'd fill out a form on paper well if you want to
automate that you put it on a on a computer screen and you have an order form and that gets saved in a database and
somebody goes look looks at the at what's in what's been added to the database today so I can ship something out it's
not making any decision so it's crud and there's no Behavior right no decisions no Behavior so if there's no Behavior
then it's just a data model that's fine totally fine once you have Behavior how do you key yeah so kuros that's what
happens right you start out with oh we're just collecting and accumulating and transforming and aggregating data and now
oh look now we're starting to make decisions um and so now you're talking really possibly about two different parts of
the system what you might call two different subdomains uh there's one that's just processing collecting and aggregating
data and there's another that's then the making decisions on that and those are two separate things um the thing that's
then making you know that's just doing the aggregation they can continue to do that but the thing that's making the
decisions basically now you want to test drive that um yeah invariably Behavior starts to infect your system uh and like
a virus it will go everywhere if you don't keep things separated um and so if you're aware that that when that starts
happening like the minute you add an if statement or a switch statement or uh any kind of decision making statement and
you think how am I going to test this and it's hard to test that should start setting off uh alarm bells and triggering
you to say let's take a step back and see what's going on here because something's happening some behavior is starting
to to grow uh and you you know if it's just like a simple thing okay we'll just add that um but once it's in there once
you have one if statement one switch statement you're going to have dozens and then hundreds and then you're going to be
in a real world of hurt if you're not then consciously aware that that's happening and saying how are we going to now
architect this part of the system decisions always happens maybe not always but like usually you start with a crud you
start adding validation you start saying H why are we having humans look at this and make a decision the Behavior
because that's what computers are for they're supposed to make decisions that we can codify in in if um yeah that's
that's why I sort of have a you know you I really think it it helps to have a tolerance um what's what's the word a zero
basically Zero Tolerance when you when you introduce your first if statement into your code that's your alarm not the
second one not the third one not the fifth one because you won't you won't be able to tell the difference between I've
got three of statements and 30 or if you do it's it might it might start it's never too late but it might now be more
difficult to to dig your way out but um I I really think zero tolerance for for that is like separate your stuff it's
you know as soon as you've got a decision-making statement um and even transformation probably has some decisions in it
like how do we handle if this isn't there or sometimes this isn't there if this other thing is there well how you going
to test that you probably want some separation there so zero zero tolerance is is the way I look at it and because of
that I end up then just starting out with I'm just going to assume that that you know I'm going to have separation of
concerns and just start there because I know it's think I would like to not do this anymore so that means we need a
method oh I don't know if I finished uh why cqs is uh why the rule of of not returning information from a command is so
and that's because of uh potency so or it's very much related to to to to that so let's say you call this method and it
returns player um and that gets sort of you know propagated around uh what if the response to your request right I
clicked the join button the join actually happened but somewhere along the way the response of the of lost well I can't
retry the join although technically here I could um this is actually a somewhat item potent thing uh but generally what
you would do is you'd first say uh well can I join it's like yes um did I join is even a better question am I already am
I already joined and so you want a query then that says hey did this person ID join what's the player associated with
this person ID so command query separation even though it wasn't like when ber Meer wrote the book The distributed
systems weren't really a thing that was was barely an interet uh there certainly wasn't the web um and so what you want
is you want a method like this that doesn't return anything so what you do is you say join and then you can go ask game
hey can you give me the player for this person ID and that's the correct way to do it because you can then call join to
get the player but sometimes you just want to access the player hey who's the player for this person ID and you should
be able to query the object to to get that information so that's why we we want Separation um there's some some
similarities between cqs and and so cqrs is systems right it came about because hey if we optimize for reading because
that's what we're mostly doing and have occasional rights and how do we optimize for reading um naturally you separation
uh so me uh that's hilarious this is a hack this is not a hack um wow no I'm feeling I'm feeling attacked by Cody here
uh don't return player violates no separation I'm I'm very amused by by the the text based uh completion that Cody is
supplying it is it is pretty judgy um I mean of course it's going to suggest this is a hack because what do you know
when what what commonly follows in most in in the code bases that it's scanned what Comm ly follows fix me this is a
hack clearly that is the most popular next set of words so it's unsurprised I mean they're they're using the same data
for the most part so of course you're going to get the same statistical modeling and so of course you're going results
uh all great so all the tests pass we've converted game to event sourcing almost all of it uh what's left is and that's
what that's what we'll do um so next time because we're pretty much at the end of today uh so we already got that uh we
got that uh we got that uh I think we're done with sort of all the event sourcing structure we need other than all right
so we'll do that next time and then we can go back to what we were what I was doing before before uh realized that I
forgot that I wanted to do event sourcing um which is uh basically um go back to the inbound adapter um have it create
the game return the handle display the existing ones um we'll need the uh where is it we need the game view loader which
will have a game view repository uh but we'll also see we got the game view loader associated with the game view
repository will also need another port uh actually I'm just going to call it game store not the uh not to be confused
with GameStop that is currently once again in the news because of speculation uh despite the fact that it's a worthless
company in reality um uh we actually will be changing state in this manner we're also going to need uh the cqrs aspect
of once we update so update read andore so that'll be something I haven't done before um so we'll have to see how that
goes uh I probably will do a a more hacky temporary version um and then later on we'll we'll probably need some things
uh to ensure we don't drop transactions or or things like that we could also not do that at all and just when you do the
game view loader it reconstitutes the games and then just gives you the view on that that's that's possible too so you
sort of do it on on pull as opposed to to pushing so we we'll see about that um so that's all for today so thanks thanks
all for hanging out uh and all the the good questions and uh this game is is actually uh what I'm working on and what
I'm putting online but you can buy the physical version you um so that tells you where the that is that um you can buy
your own copy I still have four or five left in stock uh and if you buy a copy you will get access to the the online
version when uh when it does go uh for Early Access um otherwise join the Discord if you're not already a member uh
we're deciding our next we're starting to talk about the next book for our book club so uh join us join us for that
otherwise have a good night folks especially those who who you should have been asleep by now uh in UTC plus land uh and
I will see you next
