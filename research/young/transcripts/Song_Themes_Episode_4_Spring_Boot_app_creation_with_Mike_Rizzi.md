# ＂Song Themes＂ Episode 4： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=S100FP9piGs

---

## Transcript

all right folks welcome to the song themes development stream with with Mike Rizzy howdy morning afternoon yeah morning
afternoon uh perhaps evening for some of four of working on uh Mike song themes app and uh do you want to do the the 30
second summary of of what this app is about sure it's um I'm a um a community music DJ on a local community radio
station and I've been collecting songs and themes so for example I don't know crazy idea Christmas songs yes or lists of
songs about um vampires or um political songs so forth so I've got all these lists and uh some are in spreadsheets some
are in Ticky notes some are in uh text files and so I thought it'd be fun to collect them all together but why not make
an app and share it with the world of all these lists I've been making literally over decades I think I 19 probably 81
wow um so a long time when I was in college um and I realized there aren't that many theme websites out there and if
there are the ones I found are usually like not so much a complete list but like here's the top 10 songs about caps
right or whatever and they usually filled with like a buttload of advertisements and are really annoying um so I thought
it would be fun to have something that's easier to use and a little bit more inclusive and the idea was to start off
with my list but then create the concept of a contributor where somebody could contribute songs to the site and then we
could get into some some interesting little bit more interesting software development stuff than just you know
displaying lists based on tags um and we could have the idea of members so maybe a member could be able to save off
their search results for whatever reason to generate a playlist and so forth so um there's a less than 30 second tour
and uh so you can watch the previous episodes there's a YouTube playlist I'll post a link for that uh in a bit into chat
um and so you can see this is uh our mirror board where we were working on event storming it before we we started
development but now we're we're into development um so where are we oh also on the event storming board there's also our
ubiquitous language yes yeah so we've been we've been updating our ous language with things that come up uh verbs
generate nouns just like commands generate events all right so oh what else I was gonna fill you in on something right
oh you've already show my screen okay cool yeah so this is our jira board um this is our jir j. txt um and this is sort
of our list of stuff to do on the near Horizon and then at the bottom there's also some random notes um it's a mock free
zone here um and then references when people bring up stuff in the chat I write Tom um so then we got some early stories
which we talked about in previous episodes um some Next Level stories and then some grouping of Next Level stories like
inviting someone to be in the site or contributor adding songs or contributor updating songs then Ted hasn't seen this
um this morning I sort of blurted out some of the ideas we talked about before but then some new ones like the member
could save the theme search result as a play with so they could come back and get it again um they could edit their
playlists maybe remove items like I don't care about old jazz songs or um they can reorder it so that it's actually like
a playlist in whatever order they want um we also talked about and I'm adding it now member can generate a I'll say
Spotify for now Spotify playlist YouTube um or any music player right um yeah there's still that one that Windows has
what's it called Windows Media Player that's thought is that a streaming service that's not a streaming service no but
you can still generate a playlist for it and import it right um so yeah um I was also thinking about the idea of you
know flag songs as favorites like okay I out of these like say I was only doing a one- hour show these are the ones I
would do versus I have a three-hour show so I increase the list right um and then you get into some stuff that you know
starting to mimic what you see in other systems like yes rating songs right um or they can share their playlist with
anyone to the outside world um yeah and you also get into um optim basically fit this into an one hour sequence yes yeah
I'm not that style of DJ but there are DJs that do that it's like I've got my my shows you know I've got an hour you
know or probably you know more like 42 minutes of songs and so mat you know basically optimize the list to fit it into
this time slot that that um takes me back to uh an interview sort of homework assignment I had when I was interviewing
with thought Works many years ago um which was basically optimize the times for a conference given these these talks uh
and I remember spending way way way too much time because that's who I am researching what is the propriate algorithm um
and it's basically bin packing uh and so there's some some good algorithm that that can that can do that because you
want to maximize the number of songs but you also want to ma minimize the waste um and it's and it's a tradeoff that hey
swegi nice to see you hey swegi hey Muhammad tkes tokes nice to see you um and then here was an interesting one I
realized it came out from looking at these ah yes a contributor should be able to view their own contributions right
like what have I contributed over time yeah you're yeah with some of the rating stuff it's like you know it's very easy
to fall now into the Trap of of doing some of the Social Media stuff of like right well now I do I do I rate this
person's doeses this person's contributions generally rate high or not and do I then oh no this is members rating their
own songs so this would be only visible to that member not visible outside of these two were just to themselves right
right not a larger thing um in other words thinking of it as a tool but they're rating they're they be rating the songs
that they contribute or just the ones that they find when they find so they are rating songs that somebody else
contributed yes so that's what I'm saying you could take that information and then determine whether this contributor is
for me is is you know and that's not it's not a bad thing uh it's it's my tastes are very much like this contributor
show me more from this contributor um there is there is that road how do I want to phrase that one yeah yeah for that
for that interview I I I overdid it like I they didn't really need me to to to solve the napsack problem yeah but I did
test drive it and they did they did like it but they didn't end up hiring me yes a Java stream in a world of of
JavaScript and typescript and Python and other stuff so that's all I wanted to show you yeah yeah I mean you know this
is this is one of those things and this is this is again why I always tell folks who are learning the next step after
following a tutorial is come up with a project of your own and it can start out as something like let me just create you
know songs by themes like it sounds simple but once you get into it there's often an endless supply of ideas that you
can Implement uh that for um but that will always sort of stretch your abilities um and the nice thing about doing it
doing a project that is yours and has your ideas is it's likely you're more motivated to to continue with it um finding
up hair really helps uh but uh if you're on your own finding a project that has you or meaning for you is the is the
best way to go is there a Play Place on your Discord Channel where it would be appropriate for someone to search for a
pair like hey I'm working on this um I don't have a specific channel for that uh so Post in the general Channel there a
couple times people people post there um but if if there's uh if there's certainly enough interest I'm more than happy
to set up channels on my Discord speaking nightbot all right um I'm gonna run the io free test I was about to say Left
Behind let's run our tests that's what we do yeah we've got two um disabled tests and we do have this jira breadcrumb
right so that's our that's our in yeah so working at which level do I think we were doing this level not yeah so we had
finished that test which was about um right we were we were switching the implementation of Our Song Searcher from
basically an if block to uh to a hashmap and we didn't finish that yet uh we didn't yet handle well we kind of no so we
did finish it from a prepare refactor point of view we are still handling only one song to fine uh because that's the
only Behavior we had before uh and now we want to um do we want to now extend that yeah I'm trying to I should have
looked at this before we got on but um let's see we left off with search for them does not exist returns no results
right parameterized test which deals with the thatal with the case issue yeah the case issue um and we might want to
update the test name to IND name I was just gonna say that let's do that first yeah um you can just tack on ignoring
case at case I know hey do attitud thank you so much for your your subscription 28 months holy cow 28 months you've been
a cool and then the disabled test was search for theme finds multiple matching songs right and so we disabled that
because we were basically kind of taking a step back um to do that uh prepare refactor um I think we we could clean up a
little bit more uh before we we proceed to to undisable or reenable the test I noticed that I think the uh a couple of
the fields in song search are too yeah oh has one usage let's see what that is oh we just assign it yeah ah okay yeah
that's not really that doesn't count okay delete anyway so swegi mentions uh when we when we switched we could use a
tree map with a case and sensitive comparator um we could uh but yeah I think we'll eventually go where theme is is
something that that is normalized um especially since it's not going to be it's probably going to be select from
existing themes unless it doesn't exist because otherwise uh one thing I've learned from from tagging and attribution
stuff which I've been doing throughout my career is is you want to not have you want to have themes that are cure very
very highly curated um otherwise you get a lot of overlap you don't you don't want somebody spelling out Christmas and
then have another tag that is exmas problems says I've been measuring code coverage the tdd stuff has a high level
coverage kind of mean List yes you will end up generally if you do tdd properly uh you will end up pretty much at 100%
varing getter Setter kind of Constructor kind of kind of stuff um and so yeah 98% is you know 98 plus percent is is is
well it's meaningful in that you've got really good test coverage but it's meaningless in that it doesn't mean you've
covered all uh branches and that's where um might want to look into mutation testing because that that'll really show uh
how well your code is covered um how how well your code is actually the decisions are actually exercised and asserted
against the outcome of those decisions that's something that code coverage does not tell you um so it looks like you've
got compile error in s Searcher uh did you delete it and then not delete the so if you hit F2 okay well I'm gonna do it
anyways just to F2 one usage we know where that's going to be I need you look at it so we'll just yep run the test y
shift F10 yeah should we do a commit yeah absolutely okay not a Juro one no I have removed unused fields yeah so I was
using um the AI assistant on stream yesterday and Midstream or towards the end of the stream I Bas basically my free
activation expired which was kind of funny one of the things that that it does is is offer to write your your commit
message and it's such this typical llm of all this unnecessary words like you know this this you know like 12 words to
express what really you can just say in three uh and I just I just that's the stuff I hate about llms is so Bose like
get to the point fella come on so yeah so when I when I'm thinking about code coverage uh I'm thinking about sort of the
most precise code coverage um which is did you cover all the branches and even with that it um they don't always check
for example if you've got a complex Boolean expression did you cover cover all you know n combinations of that you know
if you have one Boolean okay there are two possibilities and then you can that can be checked with Branch coverage but
if you've got two booleans um did you cover all four options and if they're three booleans did you cover all eight and
that's not something that um I don't use the tools enough to know if if if any any allow you to to set that uh but
that's what you really want you want to say for every single expression where you're making a decision did you cover
every single possible value um and mutation testing can do some of that but uh they they have their limits in terms
mutate yeah so Branch coverage is is always what you want to look at if um back to uh yeah can you can you make the yeah
can you make the um bottom window a little bit bigger yeah actually I want to get rid of that on line 43 and 44 I want
to reformat that thread me crazy because it's off screen majorly so reformat would would fix that once you out yeah on I
do one of them oh not performance logging that performance logging speaking of performance um once you outdent once then
the format knows what you wanted to is that what GNA say yes yes because it aligns the um the the indents uh so on the
bottom can we look for uh that I think it's the last method the one that actually does the search so by theme yeah so I
wanna i w to I wanted to point this out because um this is what folks mean and maybe you caning bring up um if you right
click and and maybe do the local history so we can see what it was before or you can look at this so you can do yeah
local history uh and let's go back you want me to go back yeah you want a specific one I just wanted to go back to to
when you had the um for the method for the method yes perfect uh so it'll probably go back to uh let's go back to yeah
let's look at that one let's go back further do a Buon search there we go okay so what um this is this is what what
folks mean when we talk about testing Behavior rather than implementation right this is two different implementations
one is using an if statement and we held information in a FEI field and the one on the right is storing stuff in a map
and then looking for it in the map those are implementation details uh what always puzzles me though is is sometimes
people talk about yeah I write tests and then I change the implementation and and then the test fails and I don't know
about about you Mike but that that almost never happens to me and so uh but I want to point this out like what would you
have to do to um to actually be testing the implementation here where the when you moved to the right side
implementation work and maybe this this code is too simple to to figure that out but that's that's sort of in my young
younger naive days last week um no few years back before I started understanding um really deeply understanding oh
design um is I would have that where the test would break and the problem was I was I can only talk about it
conceptually not with code obviously but invariably I was testing some implementation detail that I as a developer knew
and should have been OB fiscated from the collar and not be viewable right but was viewable in some way where I could
you know Pierce the veil of encapsulation if you will right um and with less than desirable IO is that diplomatic enough
I mean less than desirable object-oriented design yeah um AKA procedural yeah um yeah I remember vividly remember that
aha moment when I was like oh that's what objectoriented design is about it was actually a Ellen Hollow class on oo that
I was taking um and at that point I'd already been doing o development I thought for like 10 years I took that class and
it was literally the clouds parted The Light Came shining down it was like I knew nothing it was like like yes I have to
start all over again yes yeah um uh yeah I remember many years ago many many years ago around the design patterns book
times that's when when when some of the O stuff really started to to click for me so um but you know if you do so so for
me it I asked because I I see this come up fairly frequent as as an objection to to tdd but to me I'm just and I always
ask for examples that I never get any um of like what tests were brittle enough that when you tdd them and then you
changed the implementation you had to go and change your tests there are some cases where you're changing the structure
so for example if we weren't returning a list of string we were returning a list of song okay we'd have to change that
um but that's a structural change the test wouldn't fail if it compiles it probably is going to work you're just
changing types um so mostly around changing types and if you you know so if we change the requested theme to actually
theme object it's a type change but behavior is still the same um but if you're doing tdd first and you basically are
looking in from the outside that's the whole idea of that's that's sort of the the the test driven part for me is is and
that's the design process is what do I want the thing to do what's the behavior and then you leave the implementation
for for last um so that anyway just wanted to bring that up because we literally sort of changed changed the
implementation and all all our tests passed other than the the case which we had lost um but uh that probably was was a
case no pun intended of um insufficient testing on uh and and this is this is the hard part about tdd is how many tests
do I write sometimes you're F focused on Behavior but then there are details like oh is this a case insensitive search
we wrote it that way uh but we didn't perhaps perhaps we actually wrote too much code when we wrote equals ignore case
so right so that's the danger of writing you know even just a few words more uh can lead you to a place where there's an
assumption between the test and the code that's not captured in a test and so therefore you can change the code in a way
that's compatible with that test but broken uh so do to attitude says it's not clear to me the behavior of by theme
shouldn't mean Name by theme um so we're in Java so method names start with a lowercase letter uh but tell me more about
what's unclear about the behavior so we theme should I click out of this you can uh yeah so I think I think you can see
the collar maybe make it maybe look at the collar here that might make it more obvious song Searcher by theme and you
pass in the theme yeah yeah and so MOX can get you into this situation yeah exactly and and know we won't we won't go on
a tangent there I guess this could be four theme too might be a little bit more englishy uh I would interpret that
differently so so the way I would interpret if it was for theme is you're going to give me a Searcher basically a thing
that does things as opposed to the results I want a specialized song Searcher for this scene and now go now and then
there would be sort of an execute or find or something like that so that's the way I would inter I would interpret that
yeah yeah I'm sold yeah yeah which would be an interesting uh design but we don't need that so yeah no yeah um all right
so we had disable this test uh in order to do our refactoring um I think we've prepared as much as we're going to be
able to prepare uh so let's reenable it and it song yep so it only Returns the first song so I think we might need
another prepare refactor yeah I was just gonna say uh I like that the The Crickets of Silence there okay so bring back
disabled um I presume so so what what was your reason for for coming to that conclusion because I I came to it for
something that I'd forgotten about just remembered oh I was like it's returning a song singular we don't even have this
do we even actually I was still saying myself do we have the ability to turn this into song's plural and that's where my
head was at at that point when you when you spoke up right so the pro the problem is is we've got is our underlying data
structure is not quite good enough um it's it works if we want to have two different themes each with one song but if we
want one theme to have multiple songs a map is insufficient because a map is a onetoone relationship so we need a on to
many relationship um and we have a few choices uh one is we can change the map to store uh for the value we could store
a collection that's one option um but that will require us to to write some data structure code um another option is to
bring in a dependency so basically and it it it it's really interesting that um the core Java framework uh the core Java
Collections framework doesn't have multimap and I always thought uh as I mean unless they added it without me knowing
about it um there is NOA multimap um because you at least as far as I know multi that's spring though yeah so there's
multivalue M which we can get from Spring but if we do that then we're we don't want to pull in uh the dependency on on
the framework here yeah um there's uh mult there's a multimap implementation in guava uh but I feel like guava is
generally not obsolete but like a lot of it uh is is sort of it's not a dependency I want to bring in because uh it's
actually a fairly big dependency um and it has a bunch of stuff that um we we just don't need um so there is a library
that uh I've been actually wanting to play with more and that is Library right is this it yeah um we'll need this one
now yeah you want and and that's actually pointing to an old version uh why don't you click on that one yeah because
that's the one we actually want so that's the actual implementation but that's the library the eclipse collections uh so
if you go up to the itself uh so what's the latest version 11 11.1.0 okay um so your project what should we do should we
pull in this dependency or should we write our write ourselves I guess depends how complicated rolling our own is going
to end up being such that we I I've definitely gotten bit by the not invented he syndrome and so I'm slightly wary but
uh what are your thoughts I mean we'd probably want to test drive that thing um for sure and uh I mean it's not
complicated it's it's basically a manner of how do we um we basically have to pull out the list uh so we before we um
when we try to add it to the to the to the map um the first thing we have to do is say is is that key already there
right is that theme already there if it is we have to go go and grab the list and add it to the list and then for
completeness sake put the list back even though you're changing the reference so you probably don't even need to do that
um where and I don't think persistence is gonna well persistence it'll depend on when we get to persistence how we how
we do that so it's not I mean you know it's probably half dozen 10 lines of code um but you said you were kind of
jonesing to try this Library so I'm yeah but I'm not sure that that justify I'm not sure replacing 10 lines of code with
with a with a library is is worth its worth its weight so um on the other hand it it is you know a distraction in the
sense of it's not not part of our primary goal not part of our primary goal yeah um so I I could go either way depend
you know if you're interested in in writing that code and then you know doing the necessary factoring that'll be
interesting otherwise we could just pull it um so I don't know if chat has an opinion do you have an opinion chat on
whether we should pull in the depend read it from scratch we could almost probably crickety over there yeah I was
actually wondering like what does their code look like for yeah well let's look at it so I think you're actually there
uh so if browser because that's that's the implementation uh that might be the interface so so scroll down yeah so
that's the interface so what we would want to use is there's um multimap so we got one vote from chat uh scratch um yeah
and so one of the one of the things that that uh is nice about this Eclipse collections is it has a bunch of uh it has
pretty much immutable and mutable support for almost every uh H yeah so I'm going to take suiga that that as a vote for
uh uh hand hand roll it ourselves all right let's let's let's hand roll it it's not gonna take that much sounds good oh
navigate on this one keep this around for stealing or oh no I mean I we're I mean so the advantage of rolling at your
own is you're only going to implement exactly what need like there's all sorts of other stuff that we could support like
how would you handle deletions we don't need deletions yeah true because deletions are tricky um because you're
specifying not just you'd have to spec you'd have to figure out what is what is the uh behavior that you want from a
deletion you want to delete you don't want to delete the whole key I mean you might want to delete the whole key um but
most likely you'd probably want to say I want to delete this song uh in which case you'd have to look for the key in the
so searching for a song gets trickier because uh with a regular map if it's a one to one you just say give me all the
values and you have a list of songs or a collection of songs but if it's stored as a list now you say give me all the
values you got a bunch of lists and you'd have to sort of concatenate those lists and separate them out but we're not
searching by song and even if we were searching by song we would use a different data structure so it doesn't matter
because we will be searching fairly quickly find a song with any song attribute right and so this is where we get into
do we do this in memory or do we rely on a on our persistence um and I would say uh let's rely on our persistence to to
do that because it's very good at that yeah uh yes um different read models because uh because we'd have to iterate
through all the lists and find it um and it then it gets even trickier with yeah so we could certainly do it I mean
basically each way of so it's interesting how how sort of indexing and and read models and and things like that like if
we were to do this in memory we'd basically have one map that's themed to songs and another map that's whatever
attribute we're searching on to song um and so you build and so I've done this where in my inmemory repositories I I
create a couple of these Maps because sometimes I'm searching by ID and sometimes I'm searching by some some attribute
uh and maps are basically indexes from if you think about it so um and the downside of that approach is you have to keep
everything in sync yes which means anytime you add something you have to make sure that you update all your your indexes
um and then you're going to startop start wanting to not do that anymore and MTI um but one of the nice thing then is is
actually once you get to that level of complexity you should be able to then just substitute it uh and everything should
just work so um so all right so let's let's implement this from scratch which means that uh we actually want that test
to fail so that will force us to to deal with it um although I guess we could do a little bit more prepare refactoring
um can we go up to the definition of the map yes yeah so we could do an additional preparation of uh making it work
where the value is song right so um I don't know that there's a r factoring that'll get us there so we compile like this
was your me y yep uh and then yeah what you GNA say uh I was going to say let's rename the field but let's get back to
compiling before we do so we need the that song to be a list so let's just do the simplest thing to make list did you
get what I meant or no I didn't sorry okay so right now there's a compile error for the song yep and then you leave
final P yep uh and likely there's another compile error somewhere so if H F2 we'll jump to that okay actually I want to
try something if you don't mind yeah undo that you gonna do you gonna do the ARG yeah I want to see if that works so
just yeah just do post.org that's that's the sui's favorite move yeah it's a nice one so I wanted to I wanted to
practice s's move yeah yeah after use start typing it it's like oh we should use.org but you already typed so yeah um
cool y awesome and it was one of their place to yeah so hit if you hit F F2 two yeah uh so now we need to what we get
back is a song and uh we can rename that in a second or you want to rename it now requested or we can't do song plural
well let's not rename anything until until we get back to to compiling so now we can't do list of song title uh but we
because song is not a a song it's a songs maybe we should rename it let's go rename it to songs uh we can't look on the
right side of the well these would be found found matching songs either found songs or matching songs um let's do
matching I could go either way let's do matching I like matching yeah uh and then let's we can pretty much replace that
return with uh a stream and a map so do matching songs dot y just start over delete the whole thing yeah you can delete
the whole thing and we'll just rewrite it yeah so matching songs. map and what we want to extract is the title uh so if
you do song colon colon uppercase s right because it's a method handle and Y title and then you got an extra pren I have
an extra or you have one too many list right so this is a disabled test so it's really just about compiling might as
well run the test well so this was another prepare refactoring so all the tests that were passing should still pass um
and it's I was I was trying to I was talking on somewhere it might have been LinkedIn about sort of what percentage of
time during tdd we're actually writing new behavior um and sometimes especially like when when when writing a lot of new
code it feels like very little percentage of the time are we actually like how much new Behavior have we introduced none
yet yet right and we've been you know we've been streaming for for 45 minutes and okay maybe only coding half an hour or
20 minutes of that but we've been doing a lot of refactoring because especially early on in features you end up you
start with something very very simple uh and you you end up having to to refactor to prepare for for what it is now on
the flips side the people who say you know you need to do more upfront design um they could have said look you you knew
you were going to get here so why didn't you just start here right and and there is a certain validity to that like had
we spent maybe you know 10 15 minutes sort of planning out what what do we need what are the you know when we get to
searching for multiple themes oh we'll probably need a data structure that supports that um and you know and and there's
there's something to that um but even so I find that even if it's not something that you would have you could have
foreseen uh there is still a lot of refactoring that's happening versus Behavior Uh so prepare refractor is a refactor
therefore it is not modifying behavior um the idea is to change the structure of the code to prepare for the implement
um and yes it's the infamous k ISM uh make the change easy and then make the easy change and what I invariably find is
when we then do make the change uh to support it it's very very very few lines of code yeah and so there's I think
there's a balance of how much do you want to sort of take for granted and and sort of say no this is the structure we're
going to need these are the objects going to need these are the classes we're going to need um and you can take bigger
steps but it means if you guessed wrong you then have more to potentially undo um let's do a commit since we did a
structural change and all our tests are passing seem okay um I don't know what happened with the I would I would say it'
s we're not returning multiples well I isn't prepare for returning but I would be more descriptive about what we
actually did which was um change the uh prepare refactoring by by changing cool all right I think now we can uh reenable
the test it should still fail in the same song good so fails in the same way and that's reassuring because uh when I
found when you do prepare of factorings you may Implement a bit of behavior or you may change Behavior that's not
observable by the test that we're passing but that is observable by this test so I could see a a place where now we got
the second song and not the first somehow um like if we had used a set instead of a list uh it's certainly possible that
we would get that because set set has no ordering um but since we did a list it defines the ordering as how they were
added so uh We've retained that thing and so that's where uh when we do a prefare factoring it is reassuring when the
test that was failing fails in the same way it did before um so it does and so we're pass okay what are we how are we
populating this sucker we're doing it that way we're passing in both create song Searcher yeah so here's here's our
here's where our imple where we need our our our implementation of the multimap so all the calling code is fine um uh
it's all variable VAR args all the way down and so it's pretty much in the it because it's a map oh I see we're just
putting one would this be a a loop through the VAR args yes okay um why don't we rename why don't we do some renaming
actually uh which we should have done before so let's uh disable test again no I think we're we're fine this is just a
rename um field uh I think to better indicate that it's it's U so what I generally do is um I might say something like
songs by theme uh or theme to songs map depending on how how much information about the structure do you want to put
into the into the name I've been trying to move away from uh Hungarian which means have the word map and the name of the
if say we changed it to some other structure we don't have to then change this name that'd be the advantage of that
right I don't know what structure we would change it's not a map but yeah I mean that's the thing it's like and that's
where when when it comes to Maps I don't I don't mind having map in the name because that is its purpose um eventually
you know it might get encapsulated in something else but right now that is the main field for song Searcher is basically
a map um so if I were to do if I were to do if I were to put map in there I might say theme to songs map yeah uh but it
it's theme it's theme singular to songs plural plal right yeah I think I like that better what do you think okay that
that would be my my my first choice okay I wanted to type both to kind of get my head wrapped around the two options and
choose okay yeah set would better indicate that we don't care about the order um we might change we could change that
later yeah um all right so now uh let's change the the argument on line 12 and that plural uh and now we now now we need
to Loop old school loop um if you type songs. four it'll do thing yep and we basically put that in the loop you can just
push it up ohol what's the push-up shortcut um sorry I could just copy cut and paste uh control shift up Arrow go and so
now you can just replace any of the ones that we're song Now That still won't work but it might fail differently because
we're still overriding uh we're not appending anything to that list so we haven't actually but but this is a step in the
direction let's see what it looks like it's probably going to show the last song yes so it will Now fail differently
right but in your predicted way right cool so now uh now is the hard Behavior so uh what do you think we should write so
you don't think an ad would work unto itself that's the missing Behavior no multimap so when do when do we want to
basically create a new key value entry which is what we're doing now and when do we want list now this Constructor oh
it's when the theme changes so right now the Constructor is just a pile of songs they happen to be all the same be yeah
so we could we could do the simplest thing that could possibly work since right now it's uh it is only the same theme we
can make that assumption because that's what the test is saying so that's a simplifying assumption um so how do we take
advantage of that simplifying assumption if we're always assuming the theme is is the same yeah wouldn't this be um is
it ad well so there's no ad because it's it's AAP you're always value so there's two ways we could do this one would
take advantage of the what are the two ways so one way is uh convert the songs to a list and put that and no Loop oh the
other which so that and and that will work um then we will have to write a test where we have songs with different
themes and be able to to find those um then we will have to put in some some checking hey have we does this theme
already exist if it does grab the list add the new song to it uh and it's not really necessary to put it back but you
could put it back so that basically that's the beginning of the multimap well that's the beginning of of adding when the
when there's already a theme theme theme theme there basically checking to see if that theme is there so so if we just
say and and what's interesting is we could do this without for Loops at all and we can do basically a stream that that
does the mapping for us um but let's do the simplest thing that could possibly work that's what I was leing towards
because then we write a test that forces us to deal with yeah their stuff uh not sure what you mean by edit by theme uh
would map merge work maybe I think we are not we're never modifying the map at least we currently do not have a way to
do that uh no test and no behavior requires us to add songs to an existing song Searcher um at some point we will have
to do that but that will likely be when we get to persistence so that won't be right now it's all coming in through the
Constructor yeah um no one of the nice things about the way we implemented our by theme method is this will just work it
already handles the assumption that there's multiple that there could be multiple matching songs because it results yeah
I'm not sure but all we get we don't have a uh uh a map incoming um right so uh we need to convert it we need to convert
it to a map but right now let's do the simplifying assumption to you said it was instead of putting uh build the list
first basically convert the the songs to songs um and then just put that in the right I need another temporary name for
um I would go with this for now and then we'll fix the name unless you have a now and here we can just use uh Java's
list yep okay ISJ suggesting something else no okay was it you go it was it was yellow for a second I was wondering what
it was thinking but it it went away I think it was a semicolon was missing was that it no no it wasn't oh and so we can
get rid of the for Loop because we don't need that anymore yeah uh but we do need some of that code that we had sorry I
meant get rid of just the right uh we're not returning anything this is a Constructor oh it's a Constructor okay so we
still want to do um and we're going to make the simplifying assumption that the first song is right is the same for them
for them that needs to be s y but the list is our temp songs yeah and we could probably just inline that inline it yeah
that's what I was thinking yeah Control Alt in there we go all right do we think this will make the test pass think it's
gonna pass but I feel like we changed a lot of code in a see we ended up only basically changing one that one line um
Bas because we had gone into the for Loop we we went to the for Loop realized that that's not what we what the tests
were asking for for right um and so really the only thing we changed was instead of list of song of the first song we
just convert it to to an array list so we've made very few changes to this line right and you can click in the gutter to
to actually see what we've changed yeah so we renamed the the the variable but really the only significant change was
from the list of the first song to the array list as list of all the songs right um and that it and so so I want to
pause here and say we made the change easy and now all we had to do was make the easy change which was not even a full
line of code everything else just worked and refactoring I don't mean to do this to keep it this is not intended to keep
it assuming all incoming songs are same thing right this is our assumption we're now GNA write a test to crush that
assumption right and this is how the the code feeds back into our next um but before we do that let's do a commit okay
yeah you want leave it in yeah so we could we could do this as a as a buy function I was thinking eventually we would
probably use a stream um group buy to to convert those list of songs into a map of the appropriate type although I'm not
necessarily sure that's see because grouping by especially grouping by something that ends up having a m list I don't
really like my comment but okay cool now a new test now we write the new test should we break it's I think we're at the
one hour Point aren't we uh oh yeah that's actually a good time to break all right we'll take a five minute break okay
was say seven but oh you want a seven- minute break we can take a seven minute break that'll so uh at 40 minutes past
the hour we'll come back y so just a reminder for those of you who um are not yet already uh in the Discord um go to
ted. Discord and join the Discord we talk about uh all this stuff uh you can ask questions uh and it's it's a great
Community um so come come and join if you're not already a member if you want to find me on the socials the best thing
to do is go to ted. Devout and uh you'll find me on LinkedIn on um I'm even though I'm technically on Twitter I don't
post on Twitter anymore uh Mastadon is the place I do it uh there and Linkedin um and that's the the way to find find me
back um rock and roll there you go I have the talking headset it says your mute is on oh yeah thank you all right one
thing that's interesting with streamyard is it doesn't connect the headset mute to streamyard whereas like Zoom they
connected to each other so this I mute the headset it'll mute Zoom vice versa yeah that's yeah um so we're gonna write a
new test right we're gonna write a new test to get rid of this hideous comment yes so if you feel like writing a comment
like that use that as a springboard to write a test exactly um by the way uh whenever navigating let me know and we can
we can oh mob it up so just wanted to put that out there yeah maybe let's do it next time so we can make sure we got the
mob stuff set up correctly yeah because you'll need to you'll need you'll need to push the code right yeah so you could
push it on on a I mean you could push the code and we we could figure out a way that none of the behavior goes live that
that's easy right sounds good so we want to call uh oh I don't like it I'm just gonna do now I don't know how to phrase
it actually I was G to say where I don't want to say dat mentally I was thinking where database has multiple themes um
so here I think the key is is we don't care about multiple matching songs that's not right the aspect we're testing yeah
we're we're sort of testing that finds all themes I mean again you know we can always refine that what sort of gets that
idea across s with multiple themes search find all themes or or do we want all is that the next baby step or is we just
find a single theme but the data in other words do we want to populate it with like a third song at a different theme
and then we wanted to for example if we changed 42 and or added at 43 and a half a new song that's a different theme but
now we want to still get back the same results as we get in the assert on step or were you thinking returning multiple
themes I I think I was thinking um if we add two songs each having a different theme we should be able to themes yeah
pretty much what sui said two songs two themes can find both yep okay so for songs with multiple themes search or search
finds all songs I mean yeah I'm not gonna I'm not gonna I mean I'm sure we could find a better yeah I can't thinking for
that but yeah yeah okay and Year's if we ran the test we would have found out really fast you hadn't seen that uh yes we
would have themes so I guess we'll yep is there a song for take down your tree already um take down your tree already
there is be there is that song okay close enough which is a great it's a country and western song it's really yeah okay
um I was on the air Christmas day so right I got to did you play that song oh yeah definitely okay cool there was a fair
amount of irreverence in the show not completely one one a friend of mine's stepmom said it's a bit too aggressive for
me or at least a particular set it wasn't the whole show wasn't that way that particular set was so okay so we are now
want to search by multiple yeah see it's taking a single theme so have yeah so I think we would be doing just two I
think we need to do two asserts on the on the on the search oh meaning search twice search by one assert then ah okay
versus because ultimately we are going to want to like I want songs about vampires and um yeah yeah that's too big a
step that's too big a step yeah okay so here so what's interesting about this one though is I do we care I guess may as
well use the title but from from a certain point of view we actually don't care about the title anymore we just care
that there one but checking for the title is probably good a good idea because are you talking about a comment in the
chat no I'm talking about your assertion you're doing it contains exactly when when theoretically you could just do a
has size of one um but I might be concerned that it's returning the same song both times and we wouldn't know so right I
retract my my simplification okay and I'm actually forcing it to go to the the purpose just to you know mix it up where'
s the last test going for New Year's yeah I guess I might have in this test I kind of feel like I'd want to have two
assertions and so I'd inline 58 uh and then duplicate it and and and make sure for New Year's we oh that but this one
this one is is actually good enough to to go from from failing to passing and then we can ratchet up the test by adding
another assertion yeah see I was thinking if we were I was about to do duplicate that oh okay but let's stop let's stop
here yes um and I'd probably push the the found songs because that's the action so I'd stick a right right I knew there
and then we can then we can do that so this should fail because um it's going to still return the original one yeah
not's returning nothing because right because it's a different theme right because Christmas was never added yeah so if
we had done this with new years's it would have passed would it have let's do it let's actually do search by by theme
New Year's it doesn't matter what what we check the contains exactly as so fail because I need to think about that a bit
more both because we added all songs based on the first song's theme right so it's actually good that we tested both
because it helps yeah yeah inform implementation okay might just continue with this one with New Year this one pass or
do you want to do Christmas and make that one pass well once we uh once we make one of them pass I think they both
assertions would pass add want to add a third song um no I was thinking of of putting in the other assertion but no let'
s just make this pass all right so let's let's let's let's attempt to make this pass okay so it's not going to be in the
search aspect it's going to be in the constru structor y all right we're only putting the first one in so songs so right
now we're just putting the first first one in we need to we need now we need to do the loop well or maybe not we could
do it through streams so depends on how big a step we want to do do we want do we want to take a step where it's like
look we know we're going to basically just in a sense map this list of songs and sort of collect and group by the theme
um or we could take a smaller step and just do a for Loop and a um or B actually not assume just just do it as a as a
for Loop uh so we could do it this the for Loop way which is going to be uh complex in one complicated in one way um and
then maybe we could convert it to the to the stream um or merge one of those which which is either one of those is going
to be a little bit more more complicated uh or at least maybe complicate is not the right word uh less familiar than uh
than the for Loop version why don't we try both yeah so I think let's we're we are streaming right so why don't try both
for folks let's do the for for Loop um first yeah so suiga mentions that uh for Loop that will need some if statements
and we'll have a bit of we'll have some logic um but I think that is probably more familiar to folks and then we can we
can show the difference yeah and possibly can shot a refractor to it it's always possible intellig will say R this way
um presumably the AI assistant if you had it working would would certainly be able to do um I mean we could do it as for
each I think we should just do songs okay and I think we'll find the the grouping yeah something's not right um so you
can't just put it you have to statement H actually I'm not so we want to do before I'm thinking so so let's write this
as as comments okay without getting getting lost in the syntax so what's what is the first thing we want to do we before
we add we want to check is this theme already in the matap and so if it grab the value for that which will be a list so
we do a we would do a uh basically get the list for for that key so if you do a get what we're going to do is we're we'
re getting a list of song so if it is then we we get the value for list Tech technically a new array list mutable um and
then add the song to that sorry and then add the song to that list and now that we write this out we see some
commonality so we could probably pull out um the add song to that list we're always adding a song to a list it's just a
question of where we get that list from 16 right so basically are we adding it to a new list or are we adding it to a
list that already exists if it's already in the map it's to it's there and we want to add to it if there's no entry then
we need to create an entry by creating a new list and then we do a put so in both cases we'll need to the last thing we'
ll need to do is then put uh do a put back to the to the map right so let's add that as our last 17 yeah I would just
say put put list into mat yeah because it's a put right okay pair yeah and so suiga mentions um uh put if absent and so
instead of checking to see if the map has a list and then and then grabbing it we basically say put an empty array put
put the empty array list in if it's not there then we can always know that a list is going to be there for that entry so
that's kind of a an an bit of an uh use basically would get rid of our our our uh if check I would say let's do it all
the ways all the ways all the ways so for let's do it the way we just we just did it then we'll change it to if absent
and then we'll change it to using the group ey collector yeah it's always like map is super powerful there's all sorts
of stuff that you may not use on a regular basis and so there was it using uh Group by uh yeah by is it grouping by or
group by I guess we'll find out uh it's grouping by grouping by okay because it's a verb well I guess Group by could be
considered a verb but anyway it's grouping by cool all right so let's one that so let's see how do you so the key the
key needs to be the key needs to be lowercase right so if we're GNA put two with two lower case we should we should uh
and this is going to be a question basically a query query against right we're doing a query against the map hey is this
in there so question contains key right yep was so if it contains the key I got no I don't want and you're missing a
Clos pen that's why it's having some problems go if it contains that means the theme is in the to my notes Here uh we
have to that theme so we have to you drop the word get so we need to get the value for that get got some duplication
here huh uhhuh um there's three occurrences yeah because there's one in the original line as well replace it all we're
going to anyway want to call it lowercase theme um perhaps normalized theme oh even better normalized theme I mean we
could have used just theme but um we're it's not yeah and we're going to clash into it if we don't okay so normalized
theme that's the theme we get it then then we're going to put to the map we can reuse this get get Returns the right
yeah I might just do song list yeah and what we'll end up doing sorry go that no you go ahead I say have to pull that
out of the if block because we're need it yeah is there a way to refactor to do that or and paste yeah I think you can
do that if does it make it um I I don't think it's going to be a refactor refactor I think if anything it's going to be
a quick fix oh see what quick quickens uh no it probably doesn't know where what scope to push it to yet if we use it on
line 22 so instead of arrays as as list songs if we use it there because that's what eventually we're right um You don't
need the array as list anymore because it's already a list I was just trying to get it to go be now quick now you can
now you can sweet I want to make sure this is right though let see put for the theme are we in a giant for Loop we are
okay yeah given that I want to get rid of this crft so now we can write the else part of that block oh do we want to do
an L if or just an else just an else yeah it's there no why did it not oh well so you want to assign the the new array
list to song list right so song list we either get from the map because one so creating a new one so in this case it
would be a new right mhm okay but you don't need to to do that list yeah I think my instructions are getting me confused
um what are you saying this it right so if it's already there there'll be a list that we can add to if it isn't already
there we create a new one that we can add to and then we'll map got it but we are so there's one more step yeah we're
missing we're missing that step yeah now outside mhm to what thinking what are we adding song oh right we're in the song
Loop oh sorry this comments are so they push the top off let me make this taller right right yeah add the song I Like
There's No song in scope and I was like because my this was y all right we did all that and now you can drop the you can
drop the null assigned is there a quick fix for that let me that's a quick fix y remove my done initializer y awesome
and I believe we can get rid of this comment just want to double check yeah and I think what I should have done was had
it outside the for Loop so that way I I saw the entire scope yep so lesson learned so do we think this is going to work
should should it was a fair amount of code to write while while a lot for but that's one of those where if you were
doing it with your you know less familiarity than than than mine um steps but it worked cool um do we want to add an
assertion to make sure that when we search for Christmas we get that song I think that that should just work the so I'm
I'm curious about that so if we do that we're now combining the assert and the action yeah I I I don't I so yes so one
could argue we should put both search by themes into two separate variables and then assert them separately um and I
think that is uh giving up readability for it must always be three parts right right so I'd rather have so I'd rather
inline the queries and then and then it's really clear that that we're not technically the the code we're testing is
actually the Constructor and so the Constructor so line 53 to 55 is really yeah so now it should also work it pass all
right yep excellent sweet so now we want to yes um experiment well it's not an experiment but implementation quy uh the
word multi- theme query it's a multi- song results or multiple songs for query but we're only getting one song per query
uh so you could say um yeah because really what we did was we supported multiple themes right so that's what we did mult
themes cool uh I find that confusing because it's not a multi- theme Search oh it's a m it's it's uh searching being
able to search for uh multiple themes being able to search for themes is it yeah the search song songs with multiple
themes uh we don't have any songs with song There Is No song that has two themes search for songs with separate themes
okay yeah I agree that multiple themes there is Al is still confusing yeah yeah so that means we should fix the name of
the test too uh yes probably separate yeah I think separate is better or different either way maybe different is better
search finds all songs yeah because it's not just more than it's not just more than one theme it's that there are for
each theme for each song it has a different theme so I think different is good here what's fascinating about this is
that message uh ended up changing the name of a test which I think is super cool yeah and it's helping us refine our
language right songs with different themes search songs four songs with different songs we could make that longer by
saying by their themes but I there there's a point at which I think like test method names sort of have diminishing
returns because ultimately you're gonna say I don't understand that let me look at the setup okay okay right shift F12
sech works for more than a single Fe I thing yeah I mean ultimately some of this might uh will will likely change
because we're implementing stuff in memory um that we may not do in memory after a certain point although on the flip
side why not have it in memory uh the only the only place where that we're we're in having so so this is this is sort of
a a larger question of why rely on the database if you can just load everything into memory like why talk to the
database at all load it upon startup and and read it from there um and and I see this again it's sort of this idea of
well that won't scale like really how many songs do you need to have before you before you exceed even like one of the
smallest virtual machines that you would deploy to which has a gigabyte of ram how many songs can you fit in half a
gigabyte like a lot because we're not storing because we're not storing the songs themselves right we're not storing
digital data for the mp3s or song that's still a lot of songs in in in 512 megabytes and then we have to have some sort
of persist we persist to a flat file well at that point it's it's you still might persist to a database because it's
convenient but you wouldn't do the searching in the database because right why why why talk to why talk to the world
when you already have it in memory yes now the question would then become well how often is that is that basically map
updated um because then you'd have to figure out how to both mutate the database and reload the map at the appropriate
times um and how long does that take but even so like let's say is 10,000 songs how long does it take to load 10,000
songs in from the database if you're only updating it you know a couple of times a day still way faster than doing the
search every single search through the database right in a sense you are caching right and so all this is all about like
caching and if your cash is big enough you basically cach the entire database uh and at that point you might say well
we're doing updates frequently enough so let's just rely on the cash to do the work for us um and then it's still in
memory but you're you're work and so I mentioned this constantly about like uh and and I and I know um Paul Tevis talked
about this technique on on LinkedIn about how many you going to store you're going to store 10 100 a thousand a million
um and at some point you'll say a million no we're not going to have a million we're going to have a thousand right and
so by by going you know jumping orders of magnitude with the question you often say no a million that's ridiculous we're
never going to have a million or maybe you will have a million um but when will you have a million well we probably won'
t have a million for for for a few years like okay then a thousand no we're going to have more than a thousand right and
and so by jumping these orders of magnitude you get a sense of what what are we talking about because even a million
songs you could store in memory and and it really becomes then about how often are you changing it and modifying it but
if it's read mostly just load the whole thing into there you what's the spelling for Paul T's name uh Tevis uh K I'll
find a link cool he's a guy I I know from uh Consulting Retreat and actually K back sort of reposted it cool um all
right so that's our our complicated but at least well trodden path for implementing this does intellig help us at all if
we do a quick fix on the for Loop is it going to write the correct code uh no that's not either I bet the AI assistant
if you had it activated would probably come up with Alternatives um but be yeah so what we're going to do is is um
instead of our if else we're basically going to let's um let's take our our normalized theme declaration and move it all
the half oh second control to move it up no no control shift shift so to there no down one uh down one yeah um and uh we
won't need uh actually uh let's delete um let's combine 13 and 14 so you can do that with uh a J that's a new so the
reason why you do control shift J especially there is note that it dropped the extra song list it didn't just
concatenate the lines I'm going to do it again just right little so I use control shift control shift J as much as
possible for two reasons one is it does that and the other is often you have a lot of Whit space indent that if you just
deleted the end of the line and try to to concatenate them together you end up having to delete a lot of white space
control control shift J does that for you so this is what we had before yep and now and cursor anywhere I presume cursor
anywhere yeah control shift J so it's basically a smart join lines right um let's delete the else uh delete that let's
move 14 above and here's where we'll do the put if absent so um what we want to do is on the theme to song's map so
instead of song list equals let's delete that um 13 oh the whole line or no just the song list equals got equals uh and
now we can say thong theme map uh dop put if absent I think you lost the new but that's fine I know I thought so well
okay absent uh and you can yep and normalized key and then comma and then that's 12 and you can replace the key on 15
theme control W would have been slight yeah I know I'm gonna undo it and do it so control W yes is it any different was
it a little bit faster I'm G to do it again it's so this was I was doing this one two three four five five six seven
yeah you're right yeah so so because it's stopping at each camel case two three four yeah it's much less so the the
other reason why it's fast if if you overshoot uh it's pretty easy to to go back and sometimes it's a little harder um
and also you can be anywhere along that that phrase that expression and it would it I could be here yeah then it's
actually faster because all right so what we're doing is we're basically so we normalize the theme we basically say hey
if this isn't already in there put in an empty map then we go get the map uh get the list so put put the empty list in
if it's not there if it is there line 12 is a no op so line 12 takes care of basically our if statement so it it
eliminates that logic from our code and puts it into the method name um otherwise it should be the out fart voila sweet
so slightly less code um fewer or we got rid of our ifs uh so it's a slight Improvement so let's commit that uh we can
eliminate maybe line 18 y we could count the number of lines I don't know if it very slightly or very anyway that's fine
yeah I was just being a wise yeah fine commit hey this is gonna be in your commit stream not mine want all right and now
we can go and our uh wonderful stream capability um this I will need yeah I'll just I'll just give it's not uh so this
is going to replace the for Loops let's insert the code above the for Loop um so we first need to get a stream from our
songs since that comes in as an array we're going to need to use uh uh forget if it's off of arrays as stream I think
it's arrays. arrays and then uh yeah stream and then songs so that gives us a stream so now we're gonna put uh on a new
line dot um now we're going to do uh basically a collect so we're not mapping we're not modifying anything we're just
going to do a collect and let's put this on a new line uh collectors. grouping by so no no inside the collect oh sorry
get rid of that doco that's going to mess us up um so inside the collect we're going C o collectors I know grouping by
yep and inside the grouping bu this is basically key um song. theme. lower to lowercase right so we could uh it's
basically right here we're normalizing the theme oh could just um but we need to express this as as a Lambda ah okay so
sorry on again so uh so we could do it as a as a method handle let's say we didn't want to normalize it but we would do
is we would say um uppercase theme uh so that would be fine if we didn't want to normalize it but we do want to
normalize it so ask and tell J Lambda with a quick fix replace method with Lambda yep um uh then let's and then yeah and
now you can do the two lowercase uh we might want to replace the song one with just s I'm fine with that as a local
variable or we could call it song actually there's no reason for this to be song one this is right because we get rid
ofe um so now it's grouped by that um and we now we just assign it so just do a VAR boom and just assign it to uh we
don't even need the Declaration now we can just literally assign that to themes map um and you don't need the
Declaration because we're assigning it directly to the Fe yeah yeah and it's complaining because of all this yeah you
can say this dot or you can get rid of the other stuff I would dot that oh because Mark final yeah um we Pro uh we could
do that um or we could yeah yeah that's let's let's so the only problem with the collect is it might create uh an
unmodifiable map I don't think that's going to be a problem now uh it might be a problem in the future um so instead
what we could do is uh on just think we can just say put all we do a put all meaning after map. put that and you can do
a reformat to get that to look a little nicer uh yeah yeah and if you don't like it that far indented you might put the
arrays. stream on a new line yeah I mean right now because we're using this horizontal split yeah but we still might
want not so annoying but it will drive this crazy eventually so if I do y performance log yeah I mean uh and now we
should be able to get rid of the get yeah I'll leave that there for a second uh priest auro yes we could have also done
instead of put if absence we could do a getter default um basically the same it's still the same problem of having to do
the loop uh so it would have resulted in one less line of code yeah um but that's that's one of those that's a local
optimization we're going for for more Global optimization by using our streams and letting in do all the work running
the test uh yeah let's make sure that works AC see camera yep does all right so we've gone from a bunch of lines of code
in a loop to in a sense one either one long line of code or a few lines of code depending on how you spread it out but
it's really the the the main thing that is driving that operation is just line 14 yeah we can get rid of this now yeah
we that should have made a difference but hey run the run all the tests all exactly commit yeah I assume we're going to
keep this version and not the other ones I think so you sure all right um what's next jir EST returns model with
multiple song matching so that done that yeah I think that's uh that's the the disabled test at the outer layer um um
and we needed to support uh so I think we actually did stuff that we didn't have on our list I think we did too I was
just gonna say um which is if we want to get the dopamine it's it's actually up above because it's part of the domain
layer as opposed to the right maybe maybe you want to label these two sections sure the B the top one is is domain and
the or application actually um and the bottom one is is adapter and that might uh and maybe next time we package up
according to hexal architecture oh right yeah we could still try and do that we have time all right suiga have a good
good youi uh I guess officially we've hit the two-hour Mark but I'm cool with going a bit longer if you are uh yeah I've
got another 10 10 uh 15 minutes I can I can go 15 okay yeah um so we were going to yeah and this one was a result of
Just The Way We implemented it that's why we didn't write it as an initial feature because we expected to be able to
store songs multiple songs per theme and store multiple themes so it's probably find so multip themes or didn't we set
on different oh right we did yes thank you aitous language yeah find song that have different themes yeah and we can
check that off dopamine yep and close that J so then we're g next we're going to tackle this one um time or do you want
to do the um the packaging stuff since you only have 15 minutes the packaging will take all of like a minute yeah so
let's see how far we can get with this one okay turns model with multiple song matching that's this one right right does
this disabled test represent that now uh indeed it does and so this one we could have probably undisabled earlier
because we'd actually technically finished the code that this needs because this doesn't talk about different themes
right um but that's fine so we could run it prove that assertion yeah will it work I don't know I didn't read it that
closely I have to look at the implementation let's just run it and find out yeah okay good so so it doesn't so it's so
basically we are probably not uh processing all of the results because we certainly are returning multiple results we
know that from our inner layer from our application layer test um so we probably just need to fix our controller which I
expect to be easy okay oh did you want the results back up or you no no we know that it them um oh okay all right that
actually is unexpected then uh you were thinking it was not getting a list I didn't so we were doing the right thing um
all right let's look at the results now sure we don't actually have a application layer test that returns multiple s of
the same of one theme do we uh yeah we do isn't that the test above it oh yeah we do okay right so if we so that getting
that test to pass was the the necessary what what's needed to get the controller test to pass um let's look at the
controller test again uh so we create uh is our crate song themes controller broken maybe yeah so we should probably
look for our uh create song Searcher that takes a single song and get rid of that uh oh no that's variable arguments oh
that's right so so this will be an easy fix this will be a really easy fix yeah okay so just delete this sweet so that
means in jira so in fact other than having a little bit of broken test code once we had our application layer doing the
doing the right thing the adapter just worked because it already did what it right let's find multiple songs that match
the theme this one we we should have checked off uh oh yeah I guess so yep triple dopamine today yeah love you gonna say
something I love when commit we only changed the test uh we only changed the test so we we re-enabled the test and then
we fixed the broken setup and the broken setup was in test code not right Factory methods that okay enabled uh do we
want the exact name no I think that's totally fine okay cool committed and we're green and we are green and are we are
we uh very green as in no disabled tests let's go very green yeah we are very green well we wanted really you have any
Nonio free tests I can't remember yeah we probably have a few so those I I suspected that we might have uhok a broken
MVC test because we made some changes to the controller so now our get request requires uh and this actually we can fix
in one of two ways um one is we could write more tests at this layer to say what happens if you try to do a theme search
without putting a then because that would just I mean we could just return a 404 technically which you could sort of
twist and say you know not found is applies um or we so so we could either so I think there's a little bit of what do
you want it to do uh that we may have to defer till next time but what we want to do is get back to to Green so we need
to add a query parameter uh let's go to our controller I just want to check what what the parameter there is did we mark
it as a parameter we did not so let's go do that so this is good that this failed um in fact let's make it fail the
correct way uh by having an actual query parameter in our test so uh at the end of theme search in the string we're
going to add a query parameter inside the string uh which is a question and uh now we get to decide uh what we call the
parameter we can call it requested theme yeah seems like it's good enough for now so requested theme and and then equals
and then applesauce or pants or something doesn't matter so let's run uh let's run that or let's a different way just
that one so either it's gonna fail in this in a in the same way uh or it's going to pass and this depends on uh how much
Magic Spring is is adding so let's run it yeah you might as well run all them because what I'm not sure is does can it
detect the name of the parameter by the name of the parameter which it did ah so because we matched the name yes um
without doing it I generally don't like that much magic uh because change the mapping so it's not a mapping thing it's
it's basically the requested theme parameter we need to put an annotation in front of right what so C see camera asks
about uh this applesauce thing and so uh the purpose of applesauce or pants pants is shorter um is the idea where it's
like I don't care about this thing so sometimes we'll use it you know maybe it's a value that we just don't care about
um it just needs to be something uh or also if we have a method and we don't know what to call it yet it's almost it's
it's often better to give it an obviously wrong name than something that might be only somewhat wrong uh so applesauce
pants um and I what attribute are we doing uh so this request for request pram uh and then it takes a parameter as a
string and it's going to be requested theme oh okay so with so this is the magic that it does spring says I know the
name of this parameter I can figure that out at runtime um but what this but by specifying it this does two things one
is it makes it clear that this is a request parameter so makes it more readable the other is it protects us against
renames yeah so if you didn't have this and you did a refactor rename you would have broken your code right so now we
could rename that if we wanted to and it should still work but we're not not like I don't feel that I don't feel the
need to test that no fixed BC test better way of saying it uh by adding parameter yeah I know some folks use use um I I
I I don't like using underscores especially to differentiate between things because I find that hard hard to read
although sometimes I will just use a bunch of underscores um but it is it is somewhat hard can be somewhat hard to work
with a bunch of underscores uh single underscore though is actually no longer a valid name uh because of some upcoming
features in Java I guess if you if you did like a random number of underscores at the end that year well I guess
something would can compile if you got the wrong one but then if you did shift F6 to rename it yeah I don't know I'm not
sure I like that approach yeah I mean it does have the advantage of of it's ugly and you want to get rid of it so I can
I can see that yeah yeah um all right so all our tests pass um we've got a few minutes left should we refactor to
hexagonal project so let's uh so what you want to do is select all the ones that are domain objects so song yep and song
searcher and that's it no song views dto right right dto uh and now F6 and we'll move it and so at the end of that we'll
basically say dot domain oh sorry that's what you wanted right yeah yeah okay do I need D search no I mean you can leave
it it's not going to matter not do created and now uh all the stuff that's in the adapter let's move that um technically
yes that's adapter but that's that's not really part of our feature so yeah th song themes yep control F6 no F6 oh F6
that's problem and so this is adapter you want to do do in and then do web yep yep that's it uh and now we want to align
our tests so that they are also at the same that's the only one yeah I think it's the only one right that goes to domain
F6 and now move uh yeah controller and web I think we did adapter in then web yeah sorry that's what I said oh at least
I thought I said that I missed the end ah brain could have been parsing slowly all right let's run all our test just to
make sure nothing's broken and these two stay at the outer layer aha thought something like that might happen so now we
we can ask the question um is it okay for configuration to and so here's here's where and I think this came up in my
stream yesterday here's where it'd be nice if if package if nested packages um if you could sort of align things because
I because we want application which is basically configuration startup to be able to access domain objects directly um
although actually any layer should should be able to access it so let's just fix that okay uh oh it just didn't have an
import oh so it was fine I thought it might not be public but actually it is it just didn't do the import so let's just
run it again yeah when you move stuff it doesn't go and update all the Imports for you uh and so this is the same
problem if you open up the file it will just autofix it because we have Auto it always it always bums me out that it
doesn't fix this for you because it's an obvious fix um before it didn't need to import it because it was all in the
same package but now that we move packages around it actually didn't quite update all of the Imports interesting so it's
not Savvy enough to do that huh I don't know why it didn't do that for song it it yeah I don't understand why I didn't
do that as soon as we moved song into domain it should have added the necessary Imports as part of that move factoring
um I don't know if that's an open issue but I might go look for it all right uh so for the stuff that's left over we can
leave it at the top level um which is kind of where I I leave it uh but also acceptable and I go back and forth about
this is um put it into config yeah um this homepage control is just a special case of of it's not really part of our
feature it's just a part of the walking skeleton right so it' be this one that would go yeah and you go go back and
forth on that one yeah if there's not a lot of config I tend to just leave it at the top level if there starts to be
like five you know three four five files which you which we will get to once it gets more complex once we're setting up
um the web web uh security stuff and and database some database stuff we might end up having several config files and
then I'll put it into into its own package I'm wondering about if we put in a config package now but and but then just
for that one file but Le homepage controller where it is will that help sort of remind us oh yeah homepage controller
skeleton is there any value in doing it now to config that's what I'm saying not really okay there's no real harm either
so yeah I just tend not to to like packages that have one thing in them unless it's really going to make something more
clear um but I don't think I I think it adds much value here cool okay um we have to commit I generally just say
refactor to Packaging right and let's check it out let's go into jir and close that jira which one was it the last one
there 23 I forgot we even had that there oh don't put it in quotes it's jera come on all right cool finished just in
time here we go ah where we going for top of the hour Perfect all right um so next time we'll continue with our adapter
so now that uh our application core code supports everything that we need to at least initially uh we can start
generating some HTML um and then we'll figure out what the following stories are from there sounds good and that's
tomorrow right uh that is tomorrow um what time did we say it's 30 minutes later than we started today right so 10: a.m.
Pacific uh 6 PM UTC uh and so just as a reminder if you're not already part of the Discord where we talk about the stuff
and where I announce um feature streams go ahead and join friendly bunch and That's all folks so thanks for thanks for
joining us today uh thanks for all the great chat and comments as always uh and Mike I will see you tomorrow yeah thanks
bye
