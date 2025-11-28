# ＂Song Themes＂ Episode 38： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=_6rkm461Fis

---

## Transcript

all right hello folks and welcome to uh episode 38 of working on the song themes app how's it going Mike good good and
you all right uh so last time you had some internet problems I'm assuming all those are resolved yeah actually it was my
Orbee mesh router had died like completely died which is a bummer because those things aren't cheap um so yeah the fiber
coming into the house was fine I had to call Orbee and they are able to access it remotely and go yeah it's the hardware
is dead oh wow so I ran out to Best Buy and took me about six hours to get back up to speed so so yeah I don't even know
where we left off we were probably we were literally in the middle of of writing writing some code to um I think it was
to return multiple paragraphs to represent the autocompletion options right right so should I switch to the code sure
yeah I actually just ran all I can see the failing test which was the failing test is this one right here right and it's
expecting paragraph Halloween paragraph and instead it's getting Halloween and this is the method we're testing
autocomplete themes so I think we're in the middle of maybe writing this return stream collect yeah so if you look at
the test output um what we were working on is notice that it's actually not doing the joining the way uh the way we want
it to ah and so that's what that's what what we were working on um so the the the the joining takes three parameters the
delimiter the prefix and the suffix we actually don't want um the delimer to just be a new line we actually want it to
insert also opening basically closing and then opening paragraphs because right now even though there are two items and
that's wrong the fact is is the New Year's and Halloween should be separate paragraphs they're not right so it's
expecting delimiter used between each element oh I see so we would so I think what we should do is is get the current
test to pass and then when we write a test that um returns multiple themes we'll we'll pick up that that problem and fix
it then uh so you're saying let's do the because this test because once once the filtering works then we won't have
evidence that the multi paragraph thing works is broken right yeah and then we'll write a multitest for that yeah that
makes sense y so would we do a before we do a collector we do a filter or so my streams are thin My Stream knowledge is
thin um well I think the question is that the theme finder starts with should should work properly right right right
right I just noticed as soon as you were saying that I noticed that I'm like wait a second we we should already be
filtering this oh okay it's the so you want to hit um in this case we want to look for the implementation uh and so
that's Control Alt B and right now that's our implementation yeah it's not filtering so right yeah pretty clearly so I
wonder if we took too big a step in the test and instead just wanted to fil actually this is the implementation me bring
this down below if we wanted to just see if it filtered before we get into the formatting part um yeah I mean we could
uh test more closely or more narrowly against our stub theme finder um but it is a stub and so I don't I don't feel like
testing that directly is if it were much more complicated and there were maybe more layers in between I might be tempted
but I think we can just do basically do the filter here uh in in the stub theme Finder right because this is a stub for
ultimately a repository um right SL database right yeah uh so here we can just do uh do convert stream uh themes to a
stream so now do it do it at the end of and then we'll do um I don't think there's any special filter so filter uh which
I always say every time I use it it's like this is a terrible name um because what it means is keep and they should have
just called it keep so basically keep if true uh so what we want is we want a predicate um and here we can just put the
the theme CER the basically um whatever the incoming parameter is which is a theme uh starts with uh the theme basically
and so the Lambda takes a parameter because we're going to uh want to do something with that parameter and you don't
need the parns if if you're just doing a simple parameter so you can just say theme and then an arrow ah right so theme
is is the streamed from themes so it's pulling out the string and now and now we can do the theme so we pull out that
string so it's already so so theme is already a string in the in this in this scope gotcha and so then when you say pull
out what do you mean uh so we can just call a method on it query when you say call a method on it um so theme dot
clearly the coffee isn't kicked in uh basically theme dot right so we're gonna call a method on so theme is a string and
so we're now going to say theme Dot and we're going to say start starts with oh there we go theme query right right so
that's that's a predicate it's basically saying if the theme starts with then we're going to keep it otherwise we're
gonna get rid of it and you don't need and you don't need the curly braces because the thing is already directly
returning a Boolean right um and so once we do the filter then we need okay so if we do that that means the now will it
pass I think I think it should pass it's whether this well the join because it's only a single line because only single
one it'll work yeah uh so let's let's let's do a commit since we yeah you could see the commit message I used last time
um I I wouldn't a simple version I implementation even though yes it's relatively them autocomplete theme right probably
better way of putting it sure yeah okay oh I'm sorry when you finish typing I I realized that's not what we did yeah we
can do aend right yeah now so the stub impementation is of of the stub theme finder so just a stub mation of of the
starts withth oh right better whoa uh it would not surprise me that um the broke that we yeah that we broke sort of
spring uh framework tests um dive into that now well let's just see what what uh does it us the results in the Run tab
there at the bottom no uh so let's yeah so let's run um let's just run the MVC test that should be sufficient if it's 12
failing then we'll it oh I wonder if that message was out of date let's run all the tests just to be sure wonder if that
was from the last time when you right because then it was all mid yeah yeah oh one no all right so they're all in the um
oh of course it's in the repository ones when we ran the NVC ones was a slice test so it didn't involve the uh
repository stuff and of course the repository ones are going to fail um because there's no finder we haven't built it
yet well uh we have the the interface we don't have one that's that's injectable so if you look at trying to try to
inject it yeah so if you make the stack Trace bigger we can we can see that uh creting let's go let I mean yeah so JBC
theme finder basically doesn't work um because uh it it the if we go to the jdbc one it doesn't actually have um the
ability to automatically uh Implement so what it's trying to do is it's trying to say oh look starts with uh is the name
of a method let's go so we say notice that we're on line nine there we're inter uh we're implementing the theme finder
interface so what spring is trying to do spring data is trying to do is saying oh there's a method in theme finder
called starts with let me go and try and figure out how to create a query for that automatically um but that doesn't
work got it so that that's why it's having a problem and it's doing it just because there's an interface and it's going
through all the methods of the interface right even though it's not even being used it's just going in well it it's it's
in the interface so it's got to implement it and if it can't it yeah which you would think would then be a compile error
it's not a compile error because it's not a concrete implementation it's an interface right so the generation of the
code is is at runtime yes right the generating of the um the spring generation is when that's happening right hey there
swegi welcome heyi and unal XYZ hello welcome so yeah punt for now until we get to the repository or should we get the
repository impation up and running I our basically finish the formatting and then we can write tests against uh the the
jdbc either the theme yeah either the jdbc theme finder directly or um I don't know if we need a an application layer
test for that but yeah we can we can defer that okay just to make sure we're all that all good now going to expand this
one to be more than one should we have a separate test thing more than one I think in this case it' be useful to have a
separate test that shows more than one I'm just G to clone it then complete returns HTML with multiple yes we yeah we
should probably clarify that the first one is a yeah H mail with single theme singular right with multiple themes
matching so uh what do you think New Year's again or Halloween again well we we want a different theme ah that starts
with that starts with one of those similar letters yep let me go look at the spreadsheet and it can be totally different
examples two you have a hallway theme no that would be pretty funny hallway got happy though okay we' search for AJ y so
now let's see alphabetical I should probably reverse these uh well that won't matter because it should always be
alphabetical although now that's starting to get into tests that maybe we should be writing against the the theme finder
itself but um we can do that when we get there so for now leave it like with uh to to return things in in um
alphabetical alphabetical order yeah so then this would be we're looking at new lines what we were saying right uh or do
we want that for the okay yeah we do we do I mean this is again temporary HTML that will eventually get replaced by
other HTML right okay so now we run that run I'll test this one should fail right it should fail because it's going to
be missing the closing p on Halloween and the opening p on happy we should still get the new line but yeah that that'll
excellent failed as expected cool uh so let's go fix the string concatenation joining so how would we so the thing I'm
not grocking is how this joining is working it's the delimeter is between each element be that other way around because
it's it's it's closing new line yep and then so if that's the case that's the that's the delimiter and then the prefix
use at the beginning mhm and suffix so that's still y pathetic yep okay so now it should work yeah excellent sweet ship
it okay how about we just check it in that's fine too um oh you have the amend check boox checked oh yes thank you
that's weird that that remained checked yeah you would should have been reset that's weird all right returns multiple
matching themes um I think it the more important aspect is we format multiple themes uh uh correctly in HTML or create
right so what should we do next should um the other failing tests as far as a goes actually let's look at jir and I gon
say let's look at jir and then we can uh yeah so we're still we're still working on the J 22 yeah yeah um I think that's
that might be done once we can get the real thing to work so yeah so we have to fix the the the failing tests right so
okay so let's so basically we want to implement this one correct so we need to go into the jdbc uh I mean we should
drive this through the test so we should go to the finder test um and add a test now for this finder test the JBC theme
finder test okay yep yeah because we wanted what we want to do is if you implementation so the jdbc yeah so here's
Control Alt B is g to BEP this one right yeah so what we want to do is we want to have uh what we're going to implement
is basically another method like that one with a with a custom query okay um but we'll we'll test drive that I got too
many windows open let me stuff yeah this is why I have my my tab limit set to like four five because anything beyond
that is pointless and you should not be looking at the that many that many anyway yeah I think you can close the stub
well yes in intell you can set TBL limits and that means it'll basically do least Rec I think least recently used yeah
if you want to go to the settings limit I did type more than L there we tabs there it is oh interesting and so there's
the rule of when does it close um either closes unused or unchanged um not sure what it means by unused other than it's
the opposite of unchanged my my assumption is it's least fre least unchanged but if it changed because it Autos saves oh
it knows that it Autos saved it okay yeah so it so it knows whether it's changed since since sort of presumably uh start
I'm assuming last commit I don't know what yeah you probably have to go to the help and say exactly what does this mean
but anyway the the real the important part is that the tab limit um I think 10 is way too big yeah what did you say you
do four uh four or five yeah do five just yeah soel basically um even with the limit of 10 it's it's not going to open
up tabs infinitely right at some point it will close a tab and so whether you set that limit to to to 10 or five or one
um it's going to close something it's not doesn't like it it deletes it so there's no reason for it to give a prompt it'
s just closing the tab so you don't have some uh if I could get away with with one or or two that that that's usually
fine like I actually I actually want to try like what happens if I just have two two because you should not because in
general you just shouldn't be clicking on tabs and looking at and searching sort of scanning through tabs because that's
slow right it's faster to do the control alt or control whatever yeah control n or control shift n or whatever yeah yeah
or command uh control e control tab e oh control e is this one right yeah it's the recent that one's pretty cool isn't
isn't there an F12 one too that's interesting I haven't used it while oh that's file structure control F2 yeah file
structure is just within the file as opposed to yeah as opposed to recent file e is recent you can also it's recent
control e yes yes e for recent um there's also the the uh control tab which is the switcher which is basically a faster
form of of control e control tab so now as soon as you let go of the thing it's so it's very great if if if you know
you're sing back and forth you just do control tab control tab control tab oh that's cool um sometimes people will do
the back and forth navigation but I just find the control tab to be usually what I want right so if I just clicked in
the implementation now it's just going to go back and forth between the two oh that's sweet control tab I hav my cheat
sheet of things to learn see Control Plus tab oh I do switcher okay cool okay we're gonna write a new test right yeah
that's right that's right suiga it's like you know e for recent and N for inline absolutely yeah there's only so many
letters so you gotta but now you'll never forget recent because it's e for recent yeah yeah so let's write let's write a
test um so now we're writing a test against the method that doesn't exist so I think you can pretty much copy the setup
above this one yeah yeah I was working on the name still oh I'm sorry that's right just working on the name full square
box thingy yep um filtered I mean I would say uh uh theme starting with query in alphabetical query yeah that makes
sense now we can steal right okay and the theme we got money we heart so let's go back to the assert well actually let's
do this with I guess I should start with a single one for now yeah I mean we could start with money yeah then we should
get two back or should we do heart which um well this is returning themes not songs so we should still get one is so
that case doesn't really matter just pick yeah I mean it doesn't yeah it doesn't really matter I mean you could do just
the letter d and get two two back but let's just try one and see I was thinking of starting out with one and then yeah
going to that yeah okay so now this won't even comp well this won't you won't yeah you won't even be able to like it'll
compile yeah but it you won't be able to run it right um so let's uh uh let's at least Implement something in order to
get it to run you want to over override oops sorry about that there we go control o I was close yeah control o and just
hit hit enter and that'll be the one and so what we want is um we want to add some query because it won't be able to
figure out query uh now we want just something to compile versus yeah I want to copy what we got on 11 so it's wrong but
at least it will run yeah good point okay let's run so we can expect this to fail because it's not going to have all the
themes in alphabetical order we or it will have all the themes in alphabetical order instead of just the one that we
want and I think we did contains exactly not yeah we did yeah yeah so yep fails expected okay so now we want to know how
to filter down from this so um that's a good question so we've done a select so we've unnested the themes as theme and
we select them as distinct um so yeah what is the query uh is there something like where starts with or uh so it's I
think I think we can I like okay so if we say um yeah we can just say uh as theme from songs or so after the from we can
say like uh uh how we going to do that we except uh can we just put how does it get the theme query in there uh so we
need to do uh colon and that I always forget every single time you think it has to do with the unest yeah I think in
yeah I think intellig is is just wrong because that should be to because we said as yeah I think it just doesn't
recognize that it just doesn't recognize it okay so just run the test um so we need to add a percent at the end because
that's what the like query treats as a as a wild card so we want is a theme query followed by a percent sign uh what I'm
not sure of is how to query so um this is the problem with doing doing uh searches for for this stuff is is 99% of the
information is about jpa it's let's see C methods let me share my screen while we good so query so that's where the the
colon comes from uh we'll have to add an app pram but right now I think it it infers that from the name of the variable
um ah no we don't want those are name queries modifying query maybe it does need the pram why don't we just do the ad
pram and see if that helps it um well no was so spring was complaining about sorry intellig was complaining about theme
uh theme is not the problem um what I'm trying to figure out is how to do concatenation unless it's literally string
let's try that um so let's switch back to your screen give me a second yeah and we're good so let's do uh um right after
the colum theme query let's do string concatenation uh plus and then in single quotes the percent sign oh single quotes
oh now you got a destroy double quote there you go um let's try work didn't like it so what didn't it equals error
column theme does not exist which is kind of what um perhaps you meant to ref song. themes I wonder if because of the as
theme there's like a a scope issue like we know what theme here yeah I think we might need to do some kind of sub there
was a subquery did we have one in the other there is a subquery fix oh Quick Fix uh I don't see where the that might
give us a hand yeah let's do that okay which one first one or second one right um oh it just that's what it's going to
do yeah it's basically going to add a add it's going to add a select star up front with the from and that's kind of what
we want so we want um what's the end hold on a second what's that St at the end uh be that was weird it looks like it
didn't parse something again oh even in the in the uh example it's going to add the St that's a bug I don't know where
it's pulling that St from it's like it from the beginning of the method name I don't know anyway we'll do that and then
we can just delete the St I'm not sure what yeah so uh we want to select distinct unest names as theme from songs and
then we want to I think we want to close the select there uh and then I think the now it's happy because now we've got a
single thing uh which is just going to return in a sense a a single column table as it were uh where theme is like that
what is it um why is the select distinct Orange that uh each derived table should have alias what does that do for us oh
that's what it was doing oh required so let's try that I I I feel like that's still not there's something still not
right about that when you say try that I mean take do the thing no do the run test try it as we got it yeah because it
wasn't clear that at St failed uh so doesn't like the grammar so can you scroll down because there's another error
caused by subquery in from has to have an alias oh all right I guess I guess it has to have an alias all right okay
introduce Ali Alias now run it again operator does not exist oh the asy operator doesn't exist so what are we doing with
the plus percent thing that part wasn't clear to me what the goal was uh what we want is so if you want to do a wild
card search you say like and then the characters that you want to look for and a percent at the end so it's like a star
but it's it's just different syntax oh I see so you were thinking that this would make this versus doing just that so
yeah because that won't work are you looking up concatenation within yeah nothing obvious is coming up um um oh so there
is a concat it's just not plus it's called Kat right yeah yeah let's try that okay so the Syntax for that one yeah and
then that's presume yeah that I going to say if we were iterating on this much more I might say let's let's go into the
SQL console and start that was getting basically doing more of a reppel but hey we got it working that was it amazing um
let's go modify our test so we get two do just D the letter D be well not all of those right work yes because we're
putting in that data we're just now yeah I mean yeah if you want you could you could drop uh well even if you dropped
the order by it would still be out ascending excellent cool um we probably though want a case insensitive excellent yep
uh and now we we change yeah that's a pretty funny name I like and it works all right um can we format the the select
from I know some people like at least let be consistent in terms of case talking about case sensitivity oh over yeah is
there a uh no there isn't there is a shortcut to uppercase things but it's not worth learning gotcha or it's worded
shift F3 I was about to do shift F3 and I'm like nope wrong tool it's something something you I I don't remember what it
what the meta key combinations are I I don't use it frequently enough but you could do it um so technically as should be
uh yes and we might want to give it a and it was control shift U all right I just did it uh we might want St rename that
to something as as uh where did it get St from song theme starts with song I have no idea I don't know where it came up
I mean if you want we could experiment but no I'm not interested so what is but what is it really so we can give it uh
those are basically kind of we can kind of call it either all themes or unique themes it's not unique it's actually just
all so we yeah let's just make sure it still works I was hitting shift F10 at the same time saying let's make sure it
works we're both on the same page on that one all right cool let's let's and now we know it's control shift U right
which we'll remember we'll remember that for another couple minutes and then we'll not remember um let's run all the
tests good point just to be sure they should all work most of them were failing because nobody else is using this method
but they were failing implementation hey Jonas hey welcome an X proof by Ser bit okay now we commit oh wow so it doesn't
show up on on uh streamyard but um on Twitch uh Jonas big gigantify the the dancing Dragon the dino dance thanks sorry
streamyard GNA you so much if you're on Twitch you see it in the chat so there you go all right um hey look at that all
green yeah let's let's ship it okay or at least commit and oh you know what as as you type in that I realized we
probably want to throw in uh uh ignoring case at the end of the point no yes yes Shi you want yeah re refactor base
method because we want to change the one in in theme finder itself because that's an interface uh starts with ignores
case uh ignoring so I'm I'm specific in that way because that's how uh spring data generally sort of looks for when it's
when it's driving it and so consistency is what I'm there like should we probably rerun everything just to be safe not
aor yeah I don't expect any there we go all right look at that we're up to 80 tests all right um I it's running all the
test again of course you you could stop that if you want I'm okay we're gonna you want uh well because I was gonna say
let's let's run the because I think this I think we're using the right method and and we are now doing the starts with
correctly so we should see at least the uh the paragraphs that we paragraphs okay and this is left over from last time
let me restart it y MH so now actually what themes does it have okay we could start with like G or something yeah just
see what we get G okay so G look at that and now R should go down to two yeah a y b excellent cool Tey bit slow though
well uh what's slow is we have a half second delay before it notices what's changed so we could change that yeah
certainly not the database it is not the back end that is slow yeah um so we could adjust it we could we could do 250
milliseconds see what that feels like where did we add it that in the setting it was this one I think yeah there it is
right yeah ah there you are I'm I'm here no not you I this browser window okay so I'm restart that and you can do the
same thing g r a b that's pretty quick yeah oh nice even when you back up it's yeah because every every change whether
it's you're adding or or taking away you see sweet that's pretty cool so that's interesting what it just did oh went
back to everything so it it's now showing I don't think we do we want that in our drop down to show every possible theme
before you start narrowing it down I don't think we want that like it's fine now but when there's what you know 100
themes we don't want that right right I mean if we go back to the original not the original but the um screen right here
it's showing it all well actually this one's showing it all but well actually maybe that's fine my original the one that
I was using which I can't show because it's um it's got some private stuff but this other version of this kind of you
know MH kind of um multi- select was it would it would never have the drop down it would just be filtering actually how
does that work actually no it must have the drop down yeah I'll have to go check yeah so so let me share my screen
because this is the one that we're sort of basing our stuff on okay chair away so this one um when you click into the
area to start typing the autocomplete it doesn't show anything until you start typing a letter so now that I've started
typing now it starts Auto basically doing the drop down so it letter and then as you type yeah does that so um yeah I
that from a UI standpoint uh so the only question is is do we want to prevent that from uh sort don't so there's there's
two things one is do we want to change anything about our database query uh to prevent that from happening I don't think
so uh and the other thing would be do we want to prevent the the controller let me switch back to you um do we want it
to have the controller not run the query so let's go let's go to the controller class the song theme Searcher be at the
bottom yep find it um well it says if blank it does all oh you know what sorry that's not the that's not the one we want
we want the autocomplete not the theme search ah and that's up there no where is it line 27 ah I scroll past it yeah uh
so basically the default value is empty and I think we're getting empty anyway when you back up um do we want to just
not return anything everything I mean I think ultimately we nothing at the moment it's such a short list it's not a big
deal but I do like I think the UI is a little bit cleaner where it doesn't show anything until you start typing so then
let's let's do that let's fix it so that would be just a if default value is oh not if value is empty then if if theme
query is blank string oh right sorry I was looking at the I was looking at the wrong part of the yeah if theme query is
blank then just return an NP string right let's do now this yeah got a test for this we have tests for that this test we
doesn't matter where we put it I'd probably put it at the top um we I think we might want to Nest yeah I was thinking
that there's a lot of tests in this class and yeah some of them are are about the search and some about the autocomplete
F12 yeah so the first two are about autocomplete and the rest are about the actual search yeah let's this would be an
autocomplete test so let's move autocomplete into a into a nested class yep we have to manually do that or is there a
way to say uh it's not worth the time it's not worth trying to do refactor because we're literally just going to put an
I don't actually think there is a a There's No One Step refactoring as far as I know so you'd have to do a move into an
inner class and then put an at nested and you may as well just type the at nested and no no no just class you don't
public I mean you could public but there's no point to yeah test no I don't I don't put test at the end of that um the
only thing I the only thing I might do is oh on the outer one you do but not in the inner yeah and somebody uh who was
it um oh I'm working on on something with with Claire subury and she said why why do we have tests at the end end of
this I'm like historical because now you know basically once annotations came into play we don't need it anymore right
it used to be that's how they would know as a test versus a Helper but that's been so and so the only thing I might tack
on at the end if I were to tack on something at the end is returns HTML with name and then you can delete that from the
beginning of the name of each test oh like width and so what's nice about this is then you know you still get the good
the useful output um but the individual names are then shorter right that's cool um so let's run the io free test just
to be sure that that yeah is nested a y they run so fast uh so now we want another test yes that is to me that's sort of
the the zero case yeah so that would go first yeah although you could look at it as as a an unhappy path but it's not
throwing casc um so this is interesting because we want to almost we almost want to say autocomplete returns empty HTML
yeah so we could say we could say all right HTML width doesn't apply to all of them and push it into each individual
test or we mangle mangle this with I I mean we could say with empty string but fine when query is empty or when query is
it query is blank or is it really a query or is it really the starts with parameter well we call it a query oh theme
query yeah okay I mean we could change that if we're not happy with it but that's what yeah so how about we just call it
when theme query is blank just to be consistent okay so that we can steal the same that can be yeah we'll just do empty
and we want no parns nothing right just a complete empty string not par I mean paragraph right right so it' be like that
yes okay so we run this it should fail right because we're going to get a whole bunch of them instead of none Y and by a
whole bunch I mean the two two because that particular test only has two yeah yeah okay so now we can go to is oh
actually we want blank right we want blank yeah that should do it it should we're past our break time yeah I figured
we'll take a break after after uh let's what are you gonna say I was going to say let's clean up our our test names and
then we'll commit or we could take a break and then clean them up either way what were we gonna clean about the test
names uh so um the other test the Single theme matching and the test after that so below okay they both say matching
request and that's not the term we just used in the test we just wrote oh we wrote we wrote something about theme query
whereas versus request ah now I'm not sure if I like query request better frankly do you have an opinion well request is
sort of a higher level thing because we are hitting a controller so request makes sense um but it's also uh a little
ambiguous perhaps of what that request is um yeah good point request is kind of General whereas yeah so we could say
think Single theme matching query or matching theme query if wanted to be as for Bose or is that too it's a little
unclear what the sing yeah yeah it doesn't this nicely yeah yeah no I agree it took me a second to get there yeah I
think that's I think that's better yeah it's verose but I think it's clear yeah um so one the other thing is is the uh
static helper method is that used the one 108 um is that one used I think that one's used only by our autocomplete ones
right so was the first one maybe not no it's used by others okay never mind I was thinking we'd pull it into the nest of
class but if it's used by others then that's fine and this is used by others oh actually wait a second 37 and 49 yeah
yeah chose BS it's chose BS okay so that one um can we normalize the the SEC the first helper method 108 normalize
meaning uh so at not null should be above the method and it should be a static oh goodness how did that happen I'm sure
it refactoring yeah and then let's run them excellent all right now we can commit um so this was all about the test that
is which is exactly what the test says MH I guess we wanted to be really and you've been using uh hash right yeah all
right cool not the greatest comment but whatever how often do we go back the test the test says what what it does yeah
that's why we wrote it um all right so uh we'll take our our break now um when we come back uh I think we gotta get back
into the the front end HTML CSS stuff I let respond to X proof when we get back yeah I'll do uh X proof if you're still
here I'll respond to you uh before we restart but in the meantime uh we doing five or seven for the coffee break uh five
five okay but you can take a long because I'll be answering X proof's question sounds good okay see you in a few n all
right so uh let me answer X proof's question so X proof says says uh when you use class inheritance are you supposed to
inherit behavior from the parent class um if there's no behavior in the parent class does that mean using Clans class
inheritance incorrectly um so the definition of inheritance is you are inheriting Behavior Uh but um there's a I think
Michael feathers is is where I first sort of solidify the idea of in general you don't want to change the behavior
inheriting so you want to inherit Behavior if you're not inheriting Behavior then why are you subclassing is really the
question so um in my experience uh you want to make sure that the inheritance make sense from a modeling standpoint so
is this thing really this other thing and I'm just needing some addition behavior in uh the the subass just about all of
the demonstrations of inheritance that I see in sort of you know introductory articles are just wrong because they're
they're modeling sort of trying to simulate the real world which is not generally what we do we model the real world so
um the Michael feather sort of humoristic is you inherit Behavior so B so there's some bass class that has behavior that
you want to share across multiple different implementations but um you don't want to change the behavior in the Base
Class what's called overriding right so overriding is you implement the same method uh and do something else um and
generally that gets you into trouble because that is the tightest coupling and sort of the worst kind of coupling is
coupling your subclass behavior based on the superclass behavior and your changing the super class what the super class
is doing and and it's just that just leads to to just terrible code um so generally theistic is inherit behavior and
then add on behavior in addition to what you're inheriting so the places where I see sort of inheritance being useful a
lot of times is like in in graphical or UI component kind of structures like well all these things have you know borders
around them and they all have you know text on them um and then some of them Behavior so XPR says if you don't need
additional behavior in the subass can you still use inheritance and I would say what are you doing why are you why are
you creating a subass if you're not adding or adding or changing Behavior so the whole the whole idea of inheritance and
again sort of modern Java and modern o you just don't do it as as frequently you know the whole idea of you have a
person based class and then you have an employee subass is just bad modeling uh we used to do that and we found that it
didn't work so we stopped doing that and so if you don't need to Define additional Behavior why would you subclass so I
need an example to to see where where where where you're sort of going off but um using inheritance means you are
subclassing so if you're not inheriting any if you're not providing any concrete additional Behavior Uh why create a new
class in that well but that's usually the marker is at the at the top level not so a marker would be an a marker
interface that doesn't have any methods right so like serializable um is one that's sort of old um but there a lot of
there functional interface which is also the same kind of thing it doesn't force you to implement anything um but that's
I don't see that as inheritance I see that inter think if there's any use of a inheritance concrete inheritance is a
marker type thing yeah I can't really think of an example of that yeah I mean if you don't need the additional Behavior
I don't know why you you are creating another class so the whole like what if you're not putting code in a class why are
you creating that class yeah yeah and and this is this is in general why the the fistic of only add and Implement
Behavior do not change existing Behavior you don't want to subass some random class again sort of unless you have to I
mean there's always situations where where uh this is just what I have to do but if you're designing and modeling things
um you want to make sure that uh it's modeled and intended to be used that way um because yeah if you if and so you know
when I do do inheritance um there's often uh I think almost always there's there's an abstract Base Class and so it's
abstract in some way there's some methods that simply aren't implemented and you're expected to then Implement Implement
those yeah if youve got if you've got if you got data holders um because you have no behavior in your system uh and
they're basically just representing rows in a table well there's no Behavior so why there so you shouldn't have any sub
clossing I'd question why you're doing that but um hey no they it's sort of like in my opinion if you're if you
literally have no Behavior why are you writing code why not just use a tool that generates the code for you based on
your tables if you're creating a crud app that truly has no Behavior you shouldn't be writing code because that can be
autogenerated it's when we write behavior and create Behavior that's when we want to put the behavior somewhere and then
we then we write code um but there's things like you know like or not but there's there's things like you know if
nothing else like J hipster um which will generate code and you know it may not be the code I write but for very you
know where there's not a lot of behavior and you just basically want something that's a front end to a table I mean
honestly that's what ruby rails was was invented for just point it at at your database and have it you know make up some
screens and and you're done um so much effort goes into to basically write boilerplate code that you may just as well
have something generate that code for you since it's boilerplate you will regret it when not if behavior is needed and
you will regret not having written things uh that way but if you know that might happen for a while um then just
generate your code what other tools are there besides J hipster for that kind of there's I mean there's a whole area of
what are called Low code or no code tools um which are you know anything from uh spreadsheet like things to uh you know
to the old you know draw draw your UI and and connect it to tables and sort of visual kinds of things um I don't know
how well they work but for certain constraint situations they're still around and they're still you know uh popular um
they were popular years ago because AI didn't exist yet now that AI exists everybody thinks the AI can generate it and
it can't so um stop doing that llms are are not meant for that but whatever um so uh if you find yourself creating a
class that has no Behavior why are you and it doesn't add anything while you while you subclassing question all right
back to the code sounds good all right where did they leave off J I think so we were talking about justplaying in a drop
down list at first before we go to the the UI widget right um it looks like we did Implement filter filter I guess
that's what this means has narrowed down yeah I guess I don't know what we meant by Implement filter we just delete it
yeah yeah X proof happy to happy to help um one thing about sort of inheritance and subclassing is uh the details matter
so you know it's hard to talk about this generally uh you really have to get into the specifics of so um so let's see so
what do we need next um what's our dropdown going to look like um so the drop down idea is you only get to pick one
existing theme yeah I mean we kind of already have that um because we we are popular the drop down when the I mean so I
guess the question does this does this give it I guess my my real question is we actually aren't narrowing down the drop
down but does that take us in the right dropdown right what will the the UI is there value in creating the drop down
yeah that's what I'm saying I don't think there's value in creating the drop down because we're we're moving away from
that and we're not uh we're not going to use the drop down element so see here it's not changing the drop yeah and I
don't think we wanna I don't think we want to do that I think we want to head towards um the component you were showing
the one that um already grabbed that again uh if you want it was this one so what this one does is uh in fact it's
useful to to look at what it's doing um item uh basically creates a list item so what it does is it is it takes an
unordered list and as you're as you're typing it starts adding uh uh list items to it and so what we'll do is we'll have
the back us so what we want to generate right now we're generating paragraphs we want to generate list items um that's a
minor um we should probably create the container for those items so right now we're basically showing just a whole bunch
of paragraphs right and it takes up as much vertical space as we want so what we want to do is now actually I think
start to put it in a box as it were right um so that it's basically not uh and we talked about ultimately having where
you're typing to be the same box where the yeah so yeah yeah so we want to stick that over here um but that's that's a
relatively easy change the harder stuff is the auto complete right um so we basically want to make a container that's
you know sort of of this and as you start typing and then so this is scrollable uh I think we want a div for for this so
is this the div that div that's the oh that's the selected item container uh this is a suggestion box oh so that's just
a div uh so what does it do there that's selected items um where do suggestion box get populated yeah so that happens
here so that's items that's the button Now that's navigation selection we want filtering uh right so suggestions box
yeah so that's this div right okay so what does it add to the div sorry go ahead no do it you're I think your questions
more interesting uh so let's do this inspect so that's the input that's the div oh interesting so it actually creates a
button for each one uh that's an interesting approach ah okay so it it literally is adding a button um with the label of
the button being the filtered item so that's what this is doing here uh and so then when you that's way that way they're
clickable so if you click on one uh then it adds the item to the unordered list so this is this thing is basically in a
sense sort of a custom formatted unordered list with allows duplicates I look yes it does allow duplicates we'll have
we'll we'll we we won't we'll take care um um and somewhere and we also want once they're added to the once the pill is
created for then it removes it from the list um that's interesting I wonder uh so let's let's go back to you and let's
let's start typing up some uh requirements or some some some jurs okay I'm good when you ASD uh right yes we overlap
with lunch um so this can go away I think I I think it can go away because I think we'll be more precise uh so the one
thing I want to write down before I forget is um how sure uh makes make sure autocomplete results don't return items
already selected want to do that on the back end side or you want well everything's everything's on the back end because
it's it's all HT it's all going to be HTM X um and uh which means anytime so basically when it refreshes it's going to
send the query but probably what it's also going to send is what's already been selected so that those can be filtered
out um but I think we should do that after uh we basically put the uh uh put the autocomplete container in a div if you
want to be more precise uh and sort of along with that um uh we don't we'll change the the par the the individual items
should be than then paragraph So I think put that on the next line here sense filter already selected result yeah so I
think we already put that down yep uh so when we send HTML from the back end do we create the HTML manually with text
blocks um yes or some other string concatenation I am still trying to figure out um a a component model for for HTM X in
the front end and back end and stuff like that but we're nowhere I I haven't I still haven't done enough yet I know I
want to do it um but I just haven't done enough yet yeah so for these things I find there's two issues with with time
Leaf I love time Leaf because it's natural templates um which means you can just preview it the downside is especially
for something like this it's literally one H HTML component right it's basically a div with a bunch of buttons in it um
and that's really awkward to to do in in time Leaf I mean you can do it but it's awkward from the sense of uh it's not
adding all that much um and uh you then have to deal with the fact that you won't get compile time errors if property
names are wrong or things like that um so we're we're going to continue to uh basically generate the HTML ourselves we I
don't think we've done much other HTML we did HTML for the search results but that was using time Leaf but I think for
these I think we're strings um so let's see so put autocomplete results in div container autocomplete results should be
buttons instead of paragraphs make sure autocomplete results don't return items already selected uh I think that's good
enough for now okay unless there's anything thought of yeah I was thinking we might need something in between here and
here I just don't know what it is so we got the paragraphs well I can't disagree with that because you haven't said you
haven't specified yeah yeah yeah um that that container that you were showing a few minutes ago like when we'll start
using that or are we just gonna use that as an example to write we're just using that as as basically working example
and we're going to sort of translate piece by piece because this the what I showed um reason why I picked it is is the
code is straightforward enough that I understood it um and there's a lot of stuff it's doing in JavaScript that we're
going to be doing on the back end or with HTM x uh elements got it okay so it's basically our our our guide my guide um
um yeah so let's okay so do we want to drop this select or we want to leave it there because it's useful kind of just to
see what all the themes are in the UI um I noticed it's been kind of Handy for us to to just down right this guy here
yeah um we could leave it for now until we yeah I I was just thinking it's like we we seem to to be when we're playing
around with testing it from the front end it's been useful to have what are all the possibilities so that we can know
what's there so we'll keep it around we know we know we'll get rid of it but we can keep it around for now all right so
um uh what we want to do is uh let's scroll up a bit on the bottom yeah so we've got our our HTM x uh got search results
of the div so I think let's um let's change that div because uh I don't know what we want to call it box do we just
break things by just changing that name manually yeah oh do we break things uh yeah because this here was yes we would
break that if if we change it but that's all right we're g we'll we'll update it once we figure out what we want I mean
so so what do we want to call this autocomplete box you said box that's because the other thing used box though right
yeah um so this is the container for all the autocomplete uh results so far matching matching of the query I could go
with either as or box I'm actually trying to figure out which two it feels like it's it's playing the role of a
component that is the box so let's let's call it box and we'll still do hyphenated yeah or Kebab case yep yeah Kebab
case yeah so copy that over actually is there anybody else using search hyphen results no okay yeah wanted to make sure
y so um let's in a way we were already putting container well but it's so uh I guess what I meant by that is is a
limited a fixed size uh or Max siiz actual so let's um are we writing our own CSS do we have have CSS um I guess we're
not doing any we don't have any CSS here all right so let's um let's write some CSS separate file or inline um let's
start in line and then we'll pull it out okay so we'll want a style equals here then um so the first thing we want is um
we want the height to be of a maximum size so we'll say uh Max Dash height nope we might want to use that but not not
yet yeah and um how many do we want to show like four four uh what's the vertical height unit uh not we could do 4M um
but there's another unit CSS units this's one for line height uh yeah LH let's try that okay um let's also put a border
around it so it makes it clear what what it is right yeah that stays in here right yeah so semicolon thank you I was
just about to ask Y and yeah so we want um we setting border to True uh no we got we want to say a bit more than that so
we're going to say solid uh uh and then we'll give it a a the color which is going to be the Octor or hash symbol um and
let's use what they use D4 so it's dark but it's not but it's like a dark gray or medium medium to um I think that's it
uh so when it starts out it'll be empty but yeah it's Max height not initial height right correct yeah so what what'll
happen is basically it'll grow until it can't until it gets to that height and then it and then it will not exceed that
height so as asks does uppercase L work um in CSS it it is not it might work but that's not the style so we won't do
that I could see the point though this does look like 41 I yeah yeah I get that but it's it's I'm not even it probably
would work but it is not standard so we'll just have to look with that yeah restart the server hey there SE James uh
there reason we're offering serers side HTML rendering because serers side HTML rendering is the best way to go in this
situation we don't have uh a we don't really have any state on the front end uh and this along with HTM X allows us uh
to drive exactly what we want to see from the back end because the back end has all the information all right start
typing see what happens hey all right so the box is uh let's do one that as more items yeah the Box wide we'll fix that
g has multiple C also has multiple the maximum yeah it's totally not pushing the uh uh and I and I know why um because
we need to fix our uh uh our our I wonder what the default overflow is um so can you let's do this with the with the
inspection uh so right click um yeah so want this so this is the autocomplete box uh this is a paragraph that has
exceeded it so it must be that um I would have thought the go here in this uh Auto there we go so now we got is we it
it's weird because I I I guess I I don't know what the default for for that so overflow basically says what do we do
when items inside the container exceed the size of the container um and I guess somewhere by default it's who cares uh
but now this gives us basically a a scroll um which is what we want and forl seems a bit LH seems a bit much a bit small
now well part of the problem is is is we've got too much space here yeah so we so the paragraphs are causing um extra
space we'll and we'll we'll fix that on the back end side um now we know that we need an overflow y Auto so we'll go
ahead I'll leave it back to you to go ahead and add well I was going to copy and paste but yep uh so you want overflow
dashy because we only care about the y direction it uh so isn't it more tricky to test routes since you're rendering
HTML contents um no why would it be more tricky in fact to a certain extent it's easier because the HTML that gets dis
that the browser displays is exactly what we're returning and so I can be very precise about what we want to show rather
than having to test does it return the right data and then have some JavaScript that I then have to test to make sure
does it return that Json data and and transform it correctly to HTML which is a waste um if you're doing machine to
machine apis sure use use uh uh HTTP endpoints um but if you're basically gonna gener eventually have HTML generated why
translate it to an intermediate process that then has to be translated again on the other side I I I just don't
understand that it's it's a it's a mistake that has been uh uh built upon over the past 10 years and it's just a huge
mistake um most applications don't need a single page application framework or even Library all right um let's uh before
we commit Let's uh make sure that let's change our paragraphs into into oh actually we're going to say that next all
right let's let's commit I take it back and did you excellent uh oh we wanted to change the width let's do that before
we do anything else that's what I was thinking okay um guess I might as well put it over height just straight up width
uh straight up width um let's do enough okay okay and we'll deal with the scroll bar issue later come I think you can
check off 23 and done JRA 23 done yep okay all right so let's make them buttons instead of paragraphs which means we
should probably uh do some prepare refactoring for for this because this is our backend gener code Generation Um so I
think we can close that one too and the repository as well so what we're going to want to do is um where the
autocomplete backend code is because that the front end is is fine for now what we want to do is we want to change those
P's to buttons um but I think what we should do is uh class because we could test through this but we want to basically
test line 34 uh and start changing that around and so it's annoying to have to go through this wider method gotcha sir
Shan extract this well I'll extract basically the the transformation of the list of which is basically from here to here
it extract well it's not extract it's Oh I thought you said extract sorry well extract the to a method yes but that's
not uh that's not what the code is doing the code is so what's the code doing yeah I didn't say button or paragraphs on
purpose right actually it'll be convert matching themes well no because it doesn't it's just converting oh just because
the parameters yeah for HTML and then we could change the right control shift L for forting no Control Alt L alt L there
we go a little bit better yeah no astd we're not going to call it stream collect and so on and so on and no just wanted
to quickly run the test but actually wait a second this is a MVC test this wouldn't have run this test would it uh well
we have tests against this method though right we've got our song theme Searcher tests so right that's true if it had
broken anything like if you go and change the P to a div you will you will break a an IO free at least one oh thought
there would have been more uh oh because that's the separator yeah okay yep yeah um so what we'd like to do is is
further move this out because we want this to to start uh transformation so we can make it static and then we can move
it to new class oh great wait a second did I need to actually I need to uh use automated refractor to make it static
yeah I think what you did was basically all that needed to change because it's all used in one place oh it's all used in
one place right right okay but it's always good to do the the refactoring rather than manually yeah um so yeah so let's
now move it to to a new what is move thought it was oh it's straight up F6 I was that yeah okay say we want the package
to be that's fine still in song theme Searcher yeah I mean sorry in. web yeah so you can do what I usually do here is is
I type song theme Searcher and then because I want the the package that it's in and then create a new class yeah so what
do we want to call the class that does you said HTML transformation Transformer and why is it complaining because the
class doesn't exist oh well duh uh escalate yep we're good right yep oh yeah it goes to main definitely great all right
uh you can run the test but that should should have been okay you can suggest names astd but if they have the word and
in it all right um let's commit because we did a all right uh and so now we can write method um so let's let's write a
uh uh uh characterization test and then we'll change it oh no is it uh Al enter create test right that'll create the
test clus uh sure you could do it that way well were you gonna you hesitated though so oh there I mean that that's fine
um there's just a different shortcut uh if you know that you want to go to to a test implementation which is the um tell
me uh control shift T control shift T ah right and then create it brings out the same dialogue it's the same dialogue
it's just a different way to get get to it yeah got it okay yeah um you okay with that name because we yes okay and this
would go in that package a characterization test like you said yeah so we want one that has multiple uh multiple entries
good yeah I'm clearly not creative today that doesn't matter it's more more it's more creative than than uh uh chat GPT
so bar I don't know just HTML yeah I think HTML is fine and then we want to assert that is equal to or is want to be we
want to be super precise yeah later on when we get to more complicated uh uh HTML then we might want to relax a bit um
but right now we can be pretty pretty precise and since it's a characterization test yeah you can just run it we can run
it yep so it'll fail and then we'll copy correctly yeah and of course it didn't so you'll just have to manually put in a
backs slash n i was wonder if I do it this way yeah then it escapes too see no just one backslash oh oh it's the string
right right right yeah you just hit Tab and hit Tab and then delete the next pass excellent okay so hello 145 asks a
question which is um you're on a Java spring boot Channel stream so the answer you're going to get is is Java spring
boot um uh ASP net is is also a great option um there is no right answer to this question it totally depends on why do
you want to learn back end at all so asking about what framework and what language you should use before you've
established why you want to learn it uh is the wrong way around what do you want want to do why you do want to learn it
then you can start figuring out what fits right so don't put the solution problem all right uh so let's do we want to do
a commit since we now have a a yeah even without I mean I I wouldn't use a text block here because it's so short um but
that's also typically the way I do it uh copying without the quotes um and then having it in and then having it a paste
inside of existing double quotes then intellig will escape things okay committed all right um so now um can we pull out
the list of into its own into sort of the setup part of that test great second option looks good yeah excellent yeah all
right that um do you all right so now we want to change it so that um instead of P's what did we say we want the button
yeah the BTN uh no no the full word the full word yeah so what I would do is I would use because you want to change all
four it's the full word button yep got it done um we'll probably want some other stuff but for now that's fine and we're
probably this might even push us to doing it as a text block because it's gonna start getting long um but let's do okay
oops oops yes so we just go manually fix those I presume okay so yeah go ahead I think I know where you're going with
this so um do we really care about formatting or does it just contain Halloween in this case yeah is that kind of where
you're going that's exactly where I was going so now so before this was useful because we had no other test that was
testing the HTML content itself now we have tests directly against the Transformer and so these are like I don't care
how you format this I just want to make sure that somewhere in there are are these themes so contains if I spelled it
right if you spelled it right yes and then get rid of yeah so now we should have one less test failing there it's is
contained significant uh you can still do contains and then basically comma separate it um got it so like this and I
keep forgetting about collabor yeah so suiga mentions collaborator based isolation I'm like I yeah I don't like that
name either um that I'm also trying to think of a better name and I'll have to think harder about that um are you
familiar with collaborator based isolation it's one of Shores no I don't know testing patterns so here what we're doing
is is we're sidest stepping the issue of we know that we want Halloween we want happy but this could break because if it
actually returned all three of those themes that test would pass ah so a collaborator based isolation does is is
basically um we now know how to convert to HTML and in a sense uh and so therefore we can use the same code that the um
oh the method uses and so then we can go back to be to an is equal to gotcha so use the HTML Transformer to convert in
the assert yes got it okay so back to and it's and it's something that that uh you want to do when we literally just did
what we did which is you pulled out the thing that does the conversion so you can test it more easily um and now that
it's tests right so is this H let's see it needs a a list yeah it needs that to be a list oh no it's not suggesting
convert it to a list really that's a bummer now repl with text block is not a solution that's a bum uh can you move
again huh I would have thought it would have done it I guess not all that excellent and let's go back and do the do it
to the other one and this is where I I would probably start um not maybe not quite cuz we two but if it was you know
like three four assertion we're we're almost at that point right oh wrong never mind that won't work no that won't work
fact it's even warning you that the is equal to is not a valid comparison it's like what what are you comparing anyway
it's almost too bad that it's not a compile error but of course you can always convert anything to a string so that's
sort of a problem excellent all right uh This separ it's is be I don't know what what was it collaboration yes hinter
Zimmer is a much better Zimmer that's that's our new name for we we'll tell James that's our new name for collaborative
based isolation he'll be happy about that um sorry what what were we doing here uh the commit comment um um Now using
collaboration based isolation or sure and we can say why we're doing that which is to be resilient against changes to
the okay uh want do you want to take another break we close enough to the end that we should just push on yeah I think
we're getting close enough to the end and um do we talk about end time um you you didn't tell me which end time it was
okay um probably like 1210 okay so basically 20 20 minutes or so yeah yep all right uh then let's continue so uh let's
let's let's add um let's just add one more CSS uh right thing although not to not to the we actually want to add to the
Transformer yeah so we want there um can we ask intell to convert this to a text block because that'll make this easier
replace with text block yes although I don't know why it indented it so much but whatever um you can probably unindent
if can you does that did nothing I don't know why I indented so far that's so weird let's manually unindent it and see
what Happ more yeah yeah but a reformat might push it out let's find out yeah yeah all right let's leave it I don't want
to fight fight with re re reformatting um so we class um so after after button so yeah want to say um class equals uh
and in quotes this is our auto complete I think that'll be fine uh autocomplete option autocomplete suggestion what do
you like basically something that says this is a thing that you can you can pick oh what was it called in the the sample
code because I thought I kind of liked what it was calling it was like box and then it was called suggestion button ah
so we could I think suggestion works okay um let's do that it's a little bit verose but we're we're not paying for for
the we're not paying by the bite so yep there you go uh yeah copy that down yeah to the other one all right uh Run's
gonna fail yep and we probably should have done a I forgot we want I wanted to do a prepare refactoring but that's fine
we can do it here ah um so what I want to do is is uh do a prepare ref factoring for what we're doing on the bottom any
guesses on what do what's the duplication the word button uh yes but there's more higher level um not that much higher
level basically well yeah this part no no so so oh because you're only changing the class part right so the the front is
very different than the back the open is very different than the close yeah right right right so this is for both yeah
estra is throwing throwing tdd game rules at me like yes we shouldn't do that but we're doing it anyway because we we
went too far with the assertion we could disable the test but we're professionals um so we're GNA anyway I should have
an option that would be like the advanced option in the tdd game it's like if you have earned enough experience points
or you have you know three or more commits than you're allowed to refactor on a on a on a red okay so how do you anyway
this extract the extract the whole string you're right variable uh I think we can be more precise about uh about this it
certainly button something button tag uh um sure uh although it's the to be precise it's the opening uh tag or it's a
tag opener tag opener well it's not a tag element start sure it's probably bet there's probably some more technical
terms we could use from the domain of HTML but that's good enough for now yes trust us we're concatenation yes so like
that yeah and then let's see if that passes H that still won't pass the test but it way yeah yeah all right so now we
can grab that wait a second um it's not a text block we got come that text block first right uh why it's just a space
and oh because it's going to convert the um the quotes into slash quotes oh oh I see uh well that's fine for now I maybe
we'll convert it to a text block but let's just get the test to pass and yeah yeah I didn't real I I didn't see the
double quotes there okay yeah let's block see now it did indent okay it's so confusing for some definition of okay like
yeah I don't know why it like I could I could see it if it indented it one indent from the yeah one indent but it's it
looks almost like this one's two I don't I don't I don't understand that um sometimes I'll put the opening triple quotes
on a new line and somehow that seems to make it indent less but I don't I'm not gonna fight the yeah I I don't think
that's any better no yeah okay so we get the class it to use a class but the class doesn't exist right and that's that
that'll be something we'll change in uh in the HTML file um but I don't think we have to I'm not even sure what what the
button should look like oh padding yeah there's not much formatting that we need there um but uh let's are we done with
our refactoring and we've got our test passing um then yeah I think we can go into the HTML and and add some CSS for for
that chat um oh there um oh was a question from Su James yeah uh I am actually writing an article I was I was writing an
article yesterday on exactly this topic because um I wrote in the article I get to ask this at least once a week um and
the the answer is a learning project uh and and the short answer of of what a learning project is is a project that you
that is in some way useful to you or someone close to you that you can get feedback on and then let the Project's needs
Define what you learn which is the opposite of how most people do it's like I I want to learn spring data jpa so let me
go write an application that uses it uh and that's really not uh as good as is saying I want an application that keeps
track of the books I've read and then maybe you don't need spring data jpa in fact most of the time you don't so
learning project is the short answer you will not get better by watching videos you will get familiar with stuff but you
will not get better uh and you will not get better by um doing leak code things unless you want to get better at
algorithms uh the way way you get better is by writing code that has constraints so a project that is realistic is the
go uh Tes I have not tried Swift I'm not going to be trying Swift anytime soon um it's a interesting language uh but
I've have not tried it at all I assume Mike you haven't done much with Swift no I know very little about that language
yeah all right so let's go um to the top HTML and uh in the head after line eight half uh let's put style NOP not script
right uh and just put the angle and let's define the uh what do we call it autocomplete suggestion I was hoping for it
it would autocomplete the auto yeah I was like oh come on it doesn't know it there's no way it knows yeah even Cody
couldn't probably wouldn't know um so the syntax is a not a colon but open curly brace oh and then new line uh so we
want to do is we want to turn the I think buttons come with some styling that we don't want so let's do um uh border
none and what else online I was thinking we could do start if we wanted to handle left to right languages but I think
that's out of scope so left is fine later I think that's all we need um we might need some padding but I'm uh yeah Swift
is like you wouldn't be do using Swift unless you're coding for pretty much like on iOS iPhone I mean I know some people
use the language for other stuff but uh it's got its problems from what I understand like it's it was supposed to be the
next generation or was it is the next Generation after sort of objective c um but I understand that there's some uh John
Reed who has a site quality coding.org he's he's my my goto person for for all iOS especially test driven iOS stuff it's
good guy yeah he's in our area he's in the Bay Area in yeah s San Jose which is kind of funny because like the last time
I saw him was in was when I was up in Portland oh really oh wow like we should get together cuz like we literally live
like half an hour or maybe 45 minutes yeah he's down at the bottom of the bay yeah yeah I've met him for dinner a few
times down there and for conferences obviously okay so I restarted it let me just make sure I did yep so now ah okay uh
that's not what I would have expected no interesting uh we probably have to do something with the display um of the
container uh H because you want them to just be a straight up and down list right I think we want in yeah I think we
want in go ahead what about looking at the uh the code example yeah that's what I'm looking at we want an inline block
you want it oh you already got it okay yeah so um let's test it out here so we don't have to take a longer round trip
yeah you can click there and what we want on the div um so you can go after the auto block and it's hyphenated inline
Dash yeah uh must have it at the wrong level um oh no that that's for the other thing sorry that's in the wrong place
that's not what we want I was thinking uh so what we want is on the suggestion box there must be a style I'm missing do
you want to share screen so who you're looking at uh um I would if there was anything to show but there's nothing oh I
see what they did no that's not it uh let's do it this way so let's do um because we want it on the div we want the div
uh grid and that probably will that probably will not be enough but let's hit it oh okay so I guess there's some
defaults for grid that is what we want excellent and if we click on one it'll interesting did I click on America I
didn't oh it's going off this search yeah window not the um right and so when you clicked on a button it executed
whatever was in here was basically executed the search the search because the button uh type we may not want button but
we'll leave it for for now um so let's go and change because now we know that that works uh so it's not there it's for
the div right yeah we probably want to pull the div style out now so let's let's do that I don't know if intellig will
offer to do that yeah I was wondering about that well if you click on style I wouldn't select oh well H okay yeah so you
want to grab quotes double yeah does shift will control shift W will un will will reduce the selection ah there we go
okay or or Shrink as they call it we want to put that up here in style what do you want to call the style uh just say x
until we figure that out and then paste and then we'll figure out what we want to call it so it's going to be here a I
think autocomplete box yeah one well one's called box is reason to not not no she can be consistent yeah um let's have
intellig uh put those on separate lines oh will it do that no oh that's a bummer really uh if we reformat it will do
that so if you just select the line and then do a reformat I just reformatted the whole file but okay might have
reformatt stuff we didn't want but as I say don't fight but you can basically reformat just a selection and that's how
you do that uh so now let's apply the style class sorry yeah yep all right so that should now that so I think there's a
lot tokes that llms can generative AI can can help us with a lot of this kind of thing um the problem is like all of
these generative ATI ATI AIS is what is it and what do we do wrong oh sorry you were still talking I was yes that's
right um so I I don't know I llms do stuff that doesn't exist and so that's where I have a have a problem and the
training data is is it's like we used to call these things like uh you know expert systems and other things that that
used rules to generate things and I feel like we could do a much better job of that um oh I know we did wrong we didn't
actually add anything to we did the refactoring we forgot to yeah so we we didn't forget we just did the refactoring and
refactor it appropriately uh display colon grid and I'm GNA have you have intellig sort those because I like them sorted
ah okay cool there we go excellent cool all right okay sorting um so if you select those I think under menu I'm about to
learn something new uh thought there was a way to sort pretty sure there's a way to sort just may not be on the menu
sort lines oh it's under edit edit menu sort lines down to three there it is y reverse lines that's interesting yeah so
you can join lines reverse lines sort lines there we go excellent I want to just do reverse just for Giggles okay cool
what else does it have it has short lines join which I knew about already reverse transpose transpose is interesting
yeah you know what that does uh it must be context sensitive so I don't know I don't actually know what it does in this
context didn't do anything I think it I think uh if you put your key on um like put the move the cursor one to the left
and then and then do the yeah and then do the transpose yeah so it transposes the characters I used to use that a lot
back in the emac days because it's a shortcut to do that because there would be times when I want exactly that and I
just anymore cool yeah the action search will help you find that which is how I found it that's true all right let's
commit because we're we're at time uh and we'll it control K on the wrong window here we go yeah yeah that won't work um
we basically got the grid I think we yeah we we have the um autocomplete suggestions that's it commit and push yeah um
yep that one's done so the one we didn't do was is now um selecting a suggestion push initiates a search right is that
what we want I don't think we do you want to initiate the search for each autocomplete added or do you want to initiate
the search the search yeah I think we're we were doing single selection oh okay and sure but if that seems like us doing
some work that's gonna be tossed let's figure that out next time because I don't want to yeah take your time at this
point right right right so we'll figure that out next time yeah um so yeah so so next time we'll we'll deal with some of
the uh sort of frontend navigating the list and selecting the list and selecting items um and then we'll also work on
making sure the autocomplete results don't return ones that we've already selected and next time is tomorrow and next
time is tomorrow so same time as today folks um uh 4:30 p.m UTC uh so we'll we'll see you then otherwise have a have a
great rest of your
