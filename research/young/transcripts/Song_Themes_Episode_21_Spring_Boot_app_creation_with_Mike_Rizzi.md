# ＂Song Themes＂ Episode 21： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=2VAsQpflZqM

---

## Transcript

all right hello folks welcome to a Tuesday pairing stream and good morning at least here on the West Coast in the US uh
good evening I guess in in Europe how you doing Mike doing well doing well and you doing all right so what have we got
on the agenda today yeah let's see bring up oh sure I guess at the highest level we're still working on adding songs via
bulkload of tsv right and last time we we made some nice improvements to uh actually propagating the errors to the front
end as opposed to just throwing an exception right and I guess the middle level thing was we're handling incorrect
number of columns pasted right and once we finish that we're gonna work on skip over unused columns yes and we'll need a
her a row for that hey there stupendous fellow welcome great name stupendous name I meant to say it's a stupendous name
let's see hey Cyn hey cine so uh looks like we were going to put the import string back in the Box upon yeah I think I
think we do that because that would really we talked about that last time it be be nice if if if it fails we kind of see
what we put in um so let's let's start by running uh running our tests I want to run all of shape so far so good y right
we're happening all good I'm going to switch io3 so let's see so uh when uh you actually have the code at the bottom
that we want to look at so view so we can ignore the the null because that should just never happen uh so if it fails so
if it success then we redirect just to to the root at some point we'll probably want to redirect to somewhere else but
that's good enough for now um but if it fails then uh we add the failure messages but we uh lose because that
information is not sent back uh and the page and we're basically doing a redirect so the page I think we can just add
another flash itself I was wondering about that yeah send follow asked what yes we are using jira yep and it's called j.
text and yes it is a joke and we laugh every time that way we can say we're working on jir 58 yeah yep and it's a it's a
much more efficient year doesn't take up much disc space doesn't much cognitive money um so yeah so I think what we need
to do is um so one thing that happens sort of for us which uh was talking about this on on I think it was Twitter
whatever they call Twitter these days I refuse to call it it's current name um there's a mapping of the form that gets
sent in from the front front end uh maybe pop top nope I forget what it's called so I'm just gonna go HTML and then see
what we get so you're doing a find in files you oh no no I did not mean to do that I meant to yes and it's the got be
the one not not that many choices uh so let's look yeah so if we look at the form we see the text area its ID there on
line 15 is tsv songs that gets mapped to the input string on line 27 at the bottom because it match spring will will
basically try to match that name it's a bit concerning always to me to to rely on the parameter name because you might
unintentionally refactor that uh and say I don't like tsv songs maybe I want tsv um and so what we probably want to do
is uh actually annotate that variable um so that way we can have sort of a a what's the word I can't think of the word
like um um defensive programming technique to yeah there was another word I was I was thinking of it's an it'll it'll
come to me at some point probably in the shower or something uh so what we want to do is put an annotation this one
would be um at request Prem yeah and then that takes the parameter of a string which is the name uh that basically the
stable name that won't change oh I see so you're saying if we change this name we can change we yeah so we need to put
in request param we need to put uh an annotated parameter there sorry just a parameter and that's the string called tsv
song so that way that's stable ah and it will use that in variable name the variable name yeah so now we can rename the
variable to X if we wanted to and it wouldn't it wouldn't matter we could rename it to X Twitter yes we could do that or
just xit t t r e r which is pronounce as you think it should be um I haven't heard that one that was really good yeah
that's that's that's one of my favorites uh so now that we've done that um now we can be more more clear about what the
parameter is and then we can stuff it back in uh using the ad flash attributes that we have uh at the end of this method
so test first uh I guess sure why not we're text and we've got song import adds failure messages for failed import so
you think would this would be a new I guess we could do it two days we could have it be a new assert an additional
assert on this or a completely new tech test um I feel like this is behavior about the failure message uh so sorry this
the behavior about the failed import and that failure message is is one aspect of it um so I think ah I think no
actually I think adding it here is fine okay because uh we can change the test method but basically like we expect the
right things to happen upon failed import we expect failure messages to be there uh and we expect that the tsv songs is
what was originally put there if we wanted to go that far um so what so this this brings up a good question uh that I'm
often asked about sort of testing at different layers different levels sendis fall I'll get to your question a second um
and uh I'm more comfortable having kind of these mult multiple asserts even though they're asserting different
properties uh at this level because it feels like the further away you know sort of the further you get to the edge or
the no sorry the closer you get to the edge the further away from the center uh sort of you're you're you're testing
multiple things you're you're looking at it this is you know the the subcutaneous test of what what do we want it how do
we want this form to behave and so we want to then assert on the behavior of the in a sense the entire the entire page
the entire result right um because we don't need you know as we see in this test if you bring the whole test into view
we don't actually test the content of the failure messages right we just say that there are and we check that there are
two uh but we don't check the exact content because we have tests for that we have tests that are closer in that that
are better defined uh that test more variations but at this level we don't need to test that we just need to see really
what are the things that go wrong we forget to stuff in the model or in the flash attributes redirect attributes right
so here we're mostly just did we did we get the um malformed the two tsv two malformed songs right in the right so uh
stend follows uh question um um for HTTP apis um I generally would name idto as request and response uh as as you
mentioned um but I also name them uh also depending on their roles so this is not a a a rest AP quote rest API unquote
um this is this is actually a web UI so here uh we're not using a dto yet um um we do have some view objects so we have
some dto that that are that are view objects and I actually have an article about some of this that I uh that I actually
need to update because it was sort of Unfinished um so put that article there welcome so um let's add on to the test
okay let's see we're checking the redirect here we're checking that we got definitely well yeah I guess we could start
backwards so assert that um and what do we want to call the Maybe original original bulk songs um I mean I might I guess
we could what were you gonna say I was gonna say uh how do we think about this this is um is like a putback original
text area content that's kind of what it is know yeah content that could be a longer name but I'm okay um so let's
create this one local to I guess contains exactly well it's not contain I mean you could actually do contains uh I think
or do we want just to be empty In The Same Spirit of the has to sorry Mouse well so for the failure messages we have
tests on that right that exactly what the messages are here for the text area we have no such tests so I'd like to to do
something like let's start out with is equal to to the original malform songs I don't know um if there'll be some line
trimming or whes space trimming that that will affect that but we can always fix that once we see uh in in a sense this
is this is are we close enough um you know putting aside putting aside whites yeah redirect attributes get flash
attributes content well this I think we know what that is that's that's the tsv songs that's the uh the request
parameter name right because that's what we want to put it back as ah okay right right right so that has to match the
name of the input ID and it's unhappy why so you gotta cast it oh cast it because it's just an object from point of view
hey there vean uh well when when Mike and I are pairing nobody gets to choose dark mode so don't feel don't feel like
you actually reminded me to turn that off during per mode when I'm solo I'll I'll I'll do dark mode but not when we're
pairing really I didn't know you you did Dark mode at all uh I have a a twitch Redemption where if you have enough test
test passing points you get to to redeem and there's some folks like like weat L and some other ones who have uh quite
like many thousands of of points and so they they they redeem those for like a period wow yeah yeah I mean YouTube stuff
like that it has nowhere near the kind of viewer interaction types of things that uh that's s it does which whatever
that's why that's why I prefer twitch all right so what's our expectation here well if we didn't set the flash attribute
at all I'm expecting some sort of error I don't know exactly what get flash attributes returns but we could find out if
it does an exception or something yeah I think might just be an empty string it'll either be yeah I I expect either an
well since it's a since it returns a map then it's going to be a null because get fles attributes returns a map of
string to just unknown and since that's just a regular map the contract is then null if it's not in there so that's my
expectation okay well let's run no yeah yeah so was no y all right let's make it not read you could do control D ah I
was debating whether to copy and paste or from scratch um but you're right we have a test that will tell us if we copi
and paste it does that feel right feels pretty good loud good to me's go you're gonna delete that extra space right
which one oh yeah sorry that's the problem with 150% Zoom is it's hard to keep it all on the screen and see yeah the the
fuzziness of of your layout yep okay so we expect this will either pass or be off by some some line white space but hey
sweet look at that nice I passed all right so uh should we run it and see yeah let's let's run it to see if it actually
works even though yeah anything goes wrong here it's it's in the HTML let's see I think I have it yep and H did you run
the app I thought I did I may have just forgotten to press I've never done that before 10 yeah and that's and that's why
the the the the shortcut um which is really inconvenient on on on the PC uh to bring up the Run menu because it it
basically runs runs the one you select as opposed to just making that the one the active one I always forget what the do
I have it handy the Run oh yeah alt shift F10 it's like so not like it is not in it is not intuitive at all not even
remotely like there's there's no relation between and of course that's the purpose of function keys is not to have that
okay I should probably do this off screen that's the one thing I did not do was yeah dble double tap of control will
work too I just never like double Taps um but I'm on a Mac and so it's just uh something R I have to look at one my
fingers on it's uh is it control control option r on the Mac easier you're logging in through kind yeah I totally spaced
on getting my password B set up and ready before we started streaming I think I need to add it to my checklist let me go
check my checklist I was gonna say uh no I don't have it on there that's why I didn't do it and that is bring up
password Vault I love checklist they are so boss okay now we're back we got song importer yeah so D there there's
control control which is run anything uh then shift shift which is search everywhere um those are if you're if you're
don't know the more precise shortcuts those are great uh I don't there's something about the double tapping I just I
just don't like but and then there's there's option option at least on on the Mac which stuff all right so let's uh
let's paste some some bad stuff in just grab something from my thing which is incomplete how about this not enough
columns all right okay fire off import oh no oh didn't work number of columns was two I wonder if we have to put it in
the session oh interesting that flash uh attributes are not well this attribute made it over um oh wait a second no do
you think the request pram is not well let's see so um what's the order of events that happen so we do a post to here we
set the redirect attributes we do a redirect to where we redirect to song import so that does a get request on the song
import uh import uh it'll be one of it'll be the get mapped method for that should be able to control click on that I
bet oh here yeah and we want the the icons the same that's weird why doesn't it tell us because there are two different
kinds of requests doesn't tell us which one is which jump to the second are the icons different no they're yeah so uh
that's that means improving do we have two song Imports yes we do because one is the get mapped so I assume if you
select the first one that's the first one in in the in the order in the file I'm GNA go back down again and do it again
yeah so so the first one go to the get yeah so there are popups I've seen where intell will show you will prefix it with
get and posts I don't know why in that one it didn't make a note of that you think it was a setting that no that's that'
s totally not something that you I I've never seen a configuration declaration for the uh for redirect type which is not
great um ah so uh what we need to do additionally I believe and let's do it as a spike and then we'll we'll test drive
it so um let's uh what we need to to do is because the get mapping Returns the page um the flashh attributes survive why
does the I it may be because it doesn't connect it with the survived right when we went back yeah the browser but I
think because it's a model um I'm not sure so yeah so let's let's try this uh oh wait a second do oh do we need to do is
it a Time Leaf issue where it needs oh of course srly thing of course um yeah we're sort of uh well let's see would that
matter I wonder how it I guess it has to so it would be something in here possibly yeah we need to make this a th field
that's why right as I said I figur it'd be something in in our HTML if if it didn't work yeah so uh yes so let's change
the text area um let's drop the ID and name really yeah because what we're going to do is we're going to replace it with
uh th colon um oh actually we could just do do a th uh a th value that would be fine so sorry revert revert the change
um yeah and so add-on uh you can put it after right after the text area open we'll do a th colon yeah and that's going
to equal uh the Dollar open curly closed curries and then in there is going to be tsv songs um is there a reason to keep
I mean we're keeping the name the same is it more than for consistency sake but because well this specific name must
match what we add to the field attributes here uh add to the flash attributes yes but what I'm asking is does this name
now still need to be called tsv songs to match this um like would they so the so the ID must uh must match the incoming
request pram right um and the th field when this page gets generated pulls from the model which is what we're adding to
the flash attributes so they could be different I don't know why you do that why would you why so so they don't have to
be the same same but but by convention I make them the same right right right I think my thought was this original text
area content does that make it a little bit more self-explanatory from a maintenance standpoint that's where I was okay
yeah I mean I I would I would be surprised if I encountered code like this where the field was different from the ID got
it um let's try it again okay restart I was a little bit complete w so let's look at the stack Trace what yeah yeah so
let's get to the start of Trace all right back up uh so I had a problem template oh sorry because you typed th field uh
and I meant for you to type th value ah yeah you said field but um I was wondering why it changed I should you okay
let's just rerun it yep wait till it's fully up this time okay bring this puppy back on screen okay where we've got our
our data our bad data here uh let's let's try this in the in the method uh what are you thinking uh we need to add a
parameter to the it's um who uh what does anybody call uh this method from our tests because if so we're going to need
to change signature we got one test um so let's go ahead and do a change signature forget that one by heart F6 yeah no
wonder I don't forgot that one yeah contr F6 okay what do we want to add uh we model which one spring yes model an okay
name uh model's the best name the best name awesome uh anything else uh let's have as the default model there it is yeah
rip so are you thinking we'll pull from here so um in the in there um they're meeing the song import yeah uh so at this
point the flash attributes um I'm gonna say let's let's run in in and even though I don't normally do this this is more
to understand how the framework's interacting uh let's set a breakpoint on line 26 and then we'll take a look at the
model and so let's run it uh in debug bug and we're up okay let me get the window back whoa what changed I don't know
just hit reload interesting okay I like how it says zero classes reloaded it's like all right it just wanted to talk to
us it was feeling lonely okay so we're at the again uh you want the model so the model is empty um because I think the
redirect attributes are not held in the model they're held in a SE in in a separate thing called a flashmap uh and so
what we want is uh let's stop the application and change model to um I wonder if it's because we don't have the oh that
should be okay uh let's change that to redirect attributes what's it going to do with the uh oh it's still gonna is red
attribute still derived from concurrent model or is that going to break 20 on the test uh that's going to break the the
because they're not compatible and that's fine we'll we'll just pass in um null for that got it we could pass in a valid
object now so we're g to rerun via the debugger to see what the uh yeah content is yep ages yes we know so weird why it
does that when it's zero this is always so frustrating because like the docs are not helpful here they just descri the
the reference docs describe how to do it and a lot of the examples that you find are basically doing what we're doing
with the failure messages but not with um not with input um I'm going to say let's not push on uh I don't think that's
good use of of our pairing time yeah so let's let's defer this um let's undo the changes we made for uh for this and we'
ll we'll uh I'll research this offline actually the unclick J but just um or should we look at each of them make sure
we're not GNA uh I think we um I actually think we want to keep the the change we made to add the the the flash
attribute because I still think that's the right thing um but for the um the parameter to the to the get mapping we want
to undo that yeah so let's above run all just to make sure we moving uh yeah so let's just look at what the commit so
what was a change there uh I fine okay and that's the request PRM yeah I think that's still fine by the way you can stay
in in this and there's the left right arrow that takes you through each file oh right uh that's fine you can probably
optimize one I do that I need do that from over here right yeah was this one importer test I don't remember I think so
yeah yeah now it control shift oh actually that one I don't know by heart Control Alt yep run all tests yes make sure we
didn't bust anything probably should do running the app as well test uh because now we're that what is that fail before
did we not run all the tests when we added the request PM I don't recall we're doing IO free yeah yeah uh so we need to
fix that so let's um let's test so uh after the post what we want to do is um aopt pram so right at at the end of 31
songs um and here we'll actually have to give it so it's a it's a name value pair so it's basically what the contents uh
we can just add an empty string as the second parameter oh that so that'll have an error but it'll still do a redirect
and so that's all we care about I believe let's try it because I think all all outcomes of app what interesting did it
lose the know okay that goes that was weird did you refres just do a refresh I wonder if I think I did behavior all
right let's move on well that was unsatisfying yeah I mean we could you know I could do a little bit more research um I
I have there are a few things that we can try and I have a feeling we' we'd figure it out but it would probably take
another five 10 minutes and I don't think that's yeah jump to jir 59 yeah so let's uh um commit uh original enough ah
you paused that means you want to change something I could tell um yeah I was just looking at at uh at an example and
and I think there's one thing that we can try um but I'll try it offline it might be literally one thing um so we could
do that or we could go and Skip Skip to um so jro 59 is is a refactoring we 62 well this be a fun change of change of
pace I think what do you think yeah let's do something a little more feury instead of is what you are toggling insert
mode yeah I was I thought I had it but I didn't have it right there we go I think I got it right now yeah off by one no
modes yeah no mod it was I saw some discussion in the chat about modes and and whether the double double tap is a mode
um it's like no modes insert if you're if you're a Vim user you're all about modes um I'm an emac user which is all
about not being in modes philosophy uh all right so what do we want to do here um this is where uh it's our um our
inputs The Columns to the basically match against the column headers as opposed to assuming a right so how do we do this
in a baby step way well one one baby step way is to be just backwards compatible um to use the current columns that we
that we expect but instead of using positional uh so basically treat is a a refactoring right an implementation uh and
so instead of positional do a lookup in in the heter rows but we will need to change some Behavior um because right now
the only rows that we skip are blank ones uh we will now need to skip header rows so what what's our specification for
how for knowing me I currently have looks like three rows as the header but the one that has the head names is the third
one it doesn't have to have the title you know one and two but I know you like to keep it friendly for the users um so
can we assume the row that has artist in it in the First Column is our header row oh that's an interesting idea because
if you leave out that that's a required column so if you leave that out and somehow you just paste you just copied you
know from from column two it wouldn't be valid anyway right so we could say that that the header row is the one that
contains artist and so we one is artist well too generic like would be better to call it like artist SL band name
something that's I mean I guess it would nah I was what I was think well we could always I mean we could always encode
later in a config or something what are the possible header names for that column um but I think right now we can be
what you know be more yag like what do what do you have right now yeah yeah okay so if we were so I think to be
backwards fully backwards compatible when what we want is to implement skipping that's not just blank rows but basically
uh skip past the header empty um gets a little tricky because what what we' want is let's say you copied you know from
from Row one uh column one to you know all the way out to the row you know 10 of column whatever the last theme column
is um 10 contributor yeah so if you did that to 10 we'd have to skip past the first three rows and the only way we'd
know that is if uh like how do we tell the column one is part of the header versus just it doesn't have enough columns
all right because we're checking too right because the first row has one column second row has effectively zero columns
well actually does that second row come across as a bunch of but somewhere we do a trim but I'm not sure if we do that
for detecting blank look so I'm not sure I see a good way to make it back fully backwards compatible like we could do
something like well if it doesn't have enough columns let's continue scanning until we find one that has artist in it
and then we'll know we we're in a header row uh otherwise we'd have to restart and say no there was no header row let's
rescan everything um and then the first row is basically an error uh and that just feels like a lot of work a lot of
work for for not a whole lot of benefit yeah I think just either I delete these two rows from the spreadsheet or for now
since we're doing copy and paste that because you know the the row one and row two thing are totally trigger and
eventually we could once we say now we require a header row um then we can skip past the the first two two rows and
basically ignore everything until we hit the header row right but for now we can say um it's a header row if uh unless
we just want to skip right to we require a header row so let's see what's the advantage of requiring a header row out of
the gate I guess for backwards compatibility it means a it would break back yeah so so if we say we require a header row
that's no longer backwards compatible yeah whereas if we detect whether there's a header row um I mean basically the the
real question is what do we want do we want to always require a header row like you know when when the thing is fully up
and running do you want to require a header row I of feel like we have to I think so too I think it's a good idea so
then it's not really backwards compatible I don't think we can then I don't think we can do this as a refactor I think
it's too much right too much work for for not enough benefit so to basically change all of our tests uh row so V asks do
Maxs allow Windows snapping I don't believe Max have that built in I that well we kind of have a sentinel column which
is the first column we're basically saying it has to have the word artist in it um but I think it's too difficult to uh
I mean we could basically say if the first row is not a header I mean we have to look at sort of what the behavior we
want is I think we decided we we want a header row so we're going to get there anyway so we may as well go there now
yeah so we can make that as a tiny change that basically the first row must column so I'm trying to remember which tests
are so what I what I would say is since we're doing uh a behavior change we want to think about it out outside in and
then sort of propagate the changes down um so let's start at the song importer because that's where the text at the uh
importer test level or MVC test level well MVC is only for new endpoints we're not changing any of the end points so it'
s at the import level yeah yeah so I can qu these guys if you wanted you could name it song import or subcutaneous test
but that might be a read I almost made a joke saying you're getting under my skin Ted but I didn't make that joke no you
didn't I didn't hear that uh so the first one uh we don't care about it's basically just that's just testing for the
template um that's the one we care about uh so let's make it let's make it fail in in the in the expected way so we'll
have to make that yeah I don't think there's there's no unfortunately there's no nothing that will convert that into a
muline string because it would actually change the string itself ah so it's three yep in Java is that right yeah okay
and then delete the there uh no control shift J to join those yeah I know I was I was I knew it was J but I was trying
to remember which one it was I sheet that one I know because it's the Windows um let's run this I I I think this is will
will not change anything because we skip over blank row let's just make sure that that's the case but we can yeah all
right uh and now we can um break it now we can break it so we're going to put in the header row yep will this work
actually we wanted nine don't we so let me see if I got nine one two earlier I think it was these two that were hidden
is that give this two no what did we done artist song title release title release type skipped notes so you had notes
there yeah we it oh we just skipped over it yeah so do we really have nine we had more than two well basically we we we
ignored everything after the ninth column so here you have 10 columns but we ignored column 10 um and we skipped over
notes right okay so I just want to make sure I got the right headers y so would this actually let's see what this does
actually those are tab characters yeah do a multi select is that what you about to say yeah yeah uh Alt right yep yep
okay so now it should so you got radio clean in in there is the headers um but we don't currently expect that that's one
of the ones we're not expecting right yeah right my count was off uh get rid of the T right let me go back and hide that
one from now soon you won't have to do that yeah I know that'll be great it's clearly causing a lot of cognitive
friction so yes I'm glad we're tackling this yeah I mean it's it's it's all you know it's it's not it it's like which
ones did we originally skip right which ones did we hide which ones did we show but then skipped anyway it's yeah it's
terrible yeah so now it band this I think there's a Control Band too a band that's control something Control Plus I
think as long as you don't have a band that has uh uh the pound sign or the hash mark in it um I ran into a bug on an
application that uh take basically sort of bookmarks your current page um so it takes the title uh and basically turns
it into a markdown thing so it takes the title and then puts the the link uh but it seems to be confused about the hash
sign because one of the titles that I was copying had had the uh language name fshp in it oh and the same thing happened
for C and how are those written with the with the with the pound sign the hash mark and basically treated that as like
oh I'm gonna ignore everything after it and it just really it did not handle that at all which was very s very
surprising to me because like what why are you looking at that as the in in the title um and I'm not sure if it's the
the the I'm not sure where the problem is because it's basically copying it from the browser into another app so I'm not
sure if it's the extension that's broken or something in the API to to the app yeah yeah I don't know it's like as in
the in the title like that's just HTML the hashmark is is allowed um whether it should be is question hey there tokes
welcome while we're on a tangent uh I almost never use Link lists and stacks and cues depending on what the algorithm
needs I know that's not necessarily helpful but it is definitely a it depends um but I almost never I can't think of a
reason to use a linked list so a I can't think of a reason why you'd ever write one um and B I can't think of a
situation where where what's that other than in school well or or an interview for a developer position where they're
just being lazy um and I can't think of a reason to actually instantiate one in my code I think I did it once and it's
like what am I doing it uh all right so what do we expect to happen here it should come back with a size of two I agree
okay let's find out so two not one y indeed y yeah so tkes that is the common reason why people say linked list and I
say prove it prove to me that whatever you're doing is actually faster with a link list than with other data structures
and it's rarely the case that your actual runtime performance is going to be faster with a link list uh unless you have
a very unique way of of dealing with your data um but a lot of the times uh you you really it yeah again this is one of
those situations where it's like I've been writing Java for for 28 years and I can't think of more than one or two
instances I've ever used link list uh and so there might be a better data structure but it's again one of those use the
the simplest most straightforward ones until you have a good reason not to uh because absolutely you might be giving up
a lot of performance like are you doing mostly wrs and are you doing mostly sort of random inserts into all over the
place uh that would be a very unique situation or you're constantly inserting in the middle of a list um those are
pretty rare and so again I'd want you to prove it with show me the benchmarks because it's likely that that stuff that's
happening completely in memory is being dwarfed by other issues that is that is almost always what I see um there is
this is one of my favorite rants is uh yeah I mean like these kinds of structures are super fast but you have to know
what they're for um and the the problem is is that in school so those of you without us drilled into us and nailed um
you know Big O performance and so on and performance is is rarely up for 95% of the use cases of what you're typically
dos are elsewhere uh and maybe just chose the wrong the wrong algorithm but it's rarely The Collection class so choose
the right collection class uh but otherwise run your run your performance you know do profiling see where the problem
actually is um intellig has a wonderful profiler built in uh gives you your flame graphs and and and things like that
and those are those are great so before you try to optimize things first of all just get the code to work right this is
the order of operations right make it work um and then maybe make it fast but only after you've proven with bench with
actual real world benchmarks that it's actually rant uh we're a little over the hour mark do we want to take a break
since we've got a failing test yeah maybe just a quick five minute one okay so we'll take a break and then when we come
back we'll fix the test or at least attempt to fix the test hopefully we'll we'll do that one so we'll see you in five
up yeah you want to you want to fix the bottleneck um if you really need to drop down to assembler uh I don't know I
think you're working on atypical applications um most information system business-oriented applications are not likely
going to need that but hey you never know I haven't written assembler in Far so uh just a reminder um uh in in our
Discord uh besides having great conversations about all sorts of stuff including conversations like this uh we also have
a weekly book club um we are reading the programmer's brain uh we just got into chapter three so like I always say it's
never too late to join um you can catch up you can find uh transcripts and and recordings of previous uh book clubs so
every Sunday at 10:00 a.m. Pacific 6: p.m. UTC we get together uh usually 10 or 15 of us and talk about what we find in
the book and related things that relate to to what we're doing and it's really uh good discussion good way to to learn
uh and uh in this case learn about learning so join us uh just head over to to the Discord if you're not already there
and uh you can join us on Sunday for for our next session all right and we're back okay so now we got a failing test but
we want it to skip the header row so we don't want to change the assert right correct right because there really is only
one song right um so let's go to uh to our handle there and let's flip that to the bottom yeah close some of the other
distraction so we would drive farther into the service yeah I mean we could you know make this test pass uh by just uh
trimming the first line from tsv songs but that's probably not not a good it it was certainly pass but does it pass we
end up sorry doesn't really help us refactor towards the yeah yeah okay let's drive deeper so let's yeah so let's go
here um so now here we probably want uh to to sort of hop back to our tests so look at what's calling that and well
because this one is from uh right more of an end to end yeah this one will break yeah so what we're doing is we're sort
of taking the the outer the outer layer uh writing test against that that those fail um and then we'll want to actually
disable them while we work on our inner tests but for now we we'd like um uh let's disable this test and say reenable
sorry let's say let's yeah so let's say when is that a hyphenated word I do hyphenated yeah okay otherwise it's yeah
weird yeah reent yeah handled okay and let's do the same to this one this one being this one yes I'm gonna be lazy uh
well let's make the test fail uh correctly because right now passes oh yeah good point found songs has size one oh
protest right there's only one of that thing yes yes got it okay let's run this is that all so expect this one might
still pass because it's treating the first one as a song uh which is interesting um well we never said you can't have an
artist called artist and a song title called song title yeah and it's you know maybe someday there will be somebody
who's done has their stage name is just artist I mean I know there is the artist formerly known as but I don't think
there's anyone called just artist which is why earlier uh this morning I was saying maybe we should rename it artist you
know or band name because then it's harder for somebody to it reduces the the surface area of a collision between right
right the header so what do we think about this this test do we want to just leave it and say it's uh we're gonna have
to we're gonna have to break it its well we have to break something in order to insert to add the behavior is this the
right place to break it this one's testing against service this is so this is an endtoend test this is really just
checking have we broken anything that we didn't didn't realize so I'm inclined to just leave it okay um that we have
closer end tests that test precisely what is parsed this is really just saying have we hooked and this was more about
did we wire all our components together correctly and that's why we called it our our endtoend test so I I think it's
fine to leave it doesn't happen to fail um but we want to have the header in there so that uh we know that that doesn't
hurt anything as it were yeah so then we'll go deeper and find right which there are many surprisingly so let's um sorry
let's let's back up a second I want to just see where we were here um right so here uh what are the tests that we have
two that's what we get intellig to do to have a plugin that says if the class name ends in test go into window yeah yeah
uh can we bring the full method into view yeah okay oh all of them or no no that the method that you're in bringing into
view that's this one no where the wherever the carrot is that one oh right right right that one yeah header I think it's
still in the buffer yep um wait a second oh yeah we yeah that's gonna be a problem so we got to fix that it really is
yeah yeah first this is the downside using generic data it's come back to hurt us totally us should we just convert into
real yeah let's just grab some some real data we okay that's a two song so what I would what I would say is um what's
the other before you do this what is the other test that's testing import songs it's it okay so that one's a a Mal form
so we'll have to fix that one up as well but okay so let's um because what I was going to suggest is we might want to
start encapsulating the the the song setup um or at least the song text into a factory uh to make it easier uh to then
to then change it we're certainly going to need that when we get down to the next to the next level um so let's let's
fix this one up and then we might want to extract a a factory okay so I do we really do we need think it should have
something in every column yeah this this should be valid data okay well some don't have fields for their empty columns
remember some are required and some are right um I would say a mixture of of both grab yeah let see if those two seem
good yeah mixture now I forget well we'll find out what past will do I think it's going to do that yeah so we'll have to
can you do yeah I tab interesting for selecting a tab you're gonna just need to to use the arrow keys yeah no I was in
the wrong place okay so now actually this is the heter row isn't it uh it is now yeah yeah it might actually is it
exactly the header row no looks like it I said that's missing it's missing these oh this is why you wanted the factory
yeah you're GNA have to copy paste manually copy paste okay I mean you could get fancy with copy and then you can copy
the whole thing and replace the the tabs with commas and surround them by quotes um I'm not sure you want to do do that
process no if you're fluent with multi multi karat it single single oh it's a note and column oh wait a second oh we're
skipping it so that's fine so theme one would be this theme two would does create song not have VAR args complaining oh
because it needs to be list of yeah so you need to surround the Hawaii Halloween and vampires with a list right Noe of
course I couldn't think thinking you didn't install the list of uh no I still need manually you're probably missing a a
whatever the keystroke is to figure P artist song title release title string uh we don't we don't have a factory method
for this one we have the song title and then themes we don't have one that takes right we have one just for one yeah so
we're almost at the point where we'd want to introduce a builder uh but we'll we'll not do that right now um should I
put this back as a and make it no let's go change the factor let's just duplicate uh that last one and add uh yeah and
then you can drop the list in the course cool that takes care of one now the second band yeah vegan I'm I'm not sure
about that um I I I I like keeping the this the inputs to be actual strings in the the test code itself or or in the
test code somewhere I mean we're going to do a builder or we'll do a factory I don't know that we need a I I feel like a
builder for the inputs um I don't I don't like sort of concatenating strings and things like that and then that's extra
code that is is sort of making certain assumptions yeah I me we'll end up having to pull some of the literals out um but
I'm not sure we need to go to to to a builder if we wanted to sort of fuzz the inputs then then it's more like a
property test and then we might want some some kind of thing that that generates random strings but I think situation so
in theory this should just work oops sorry the wrong go okay letting a rip but we could have mistyped something there
could be something junk happened yep I think it might be a oh no we don't have a uh can you make the ah test a bit so
the issue is it's taking single yeah because you included uh as a theme but that's supposed to be an ignored column
that's a notes column I think let me just double check I notes uh I think I think we're getting bit by the whole hiding
columns yeah yeah um so we're just gonna have to suck it up and get through it and then once we have header columns our
life will be better right well let's um so something's wrong with this oh but if I dragged if I copied uh let's go look
at the previous code no we didn't yeah that was a skipped one and I think you can just delete one of the tabs there yeah
I think that will do it and one there point vegan is is like and I was wondering it's like why is single in notes and
not release type yeah I don't think we've I have standardized on oh right release type is not what you think it is it's
not format it's not it's not format different right format is 7 inch right LP CD right right whatever yeah it's a con
you just pointed out that it's a confusing name thank you you bous language what's your you bous what are your
definitions for these things right so that passed okay so that passed let's yeah so now we can we can break this so we'
re sort of drilling in on our uh from our outside in Direction so let's break this by adding the header row and what are
you doing up there you're here well song factor is technically but point taken um I was trying to find the test that
there we go now does this one have record wrong correct uh should still work what I might do is go back to the
spreadsheet and copy the hetero and paste it in here and just see what the difference is yeah yeah so if my hypothesis
was true right they're the same yep okay cool let's paste that into our our test that we want to break should we retest
this one to make sure this one still it if you'd S I expected to I expect it shouldn't yeah it shouldn't make a
difference because we're not checking the columns and it ignores everything after the ninth column so it has too many
columns is not a problem right and it's looking for the song protest yeah so now we expect this to fail songs do we test
for three songs we don't well we do indirectly by saying we're expected so it's gonna it's gonna say that that there was
a song expected a song found that was not expected which is the artist right it contains exactly in any order y yeah let
me fix this and this is why contains would not be the right thing to test here we actually want contains order so if we
scroll down it should say following elements were unexpected which yep hello swie all right uh so let's disable this one
and then we can drop down a layer a layer correct uh indeed that's the layer we want yes basically the song parser F2 so
there's two pars multiple songs what's the second one is that something we we actually want to get rid of uh the so
what's the difference between that it so this one just checks for successful result right the other one checks for
successful result and the correct song so it feels like that that's no longer needed maybe we needed that as uh uh think
when yeah I think it a stepping stone to doing uh resulting success implementation yeah so you're thinking dump this one
I'm thinking of dumping agree so what tests in here do we have that are checking multiples well actually it doesn't
matter uh they're all going to require a multi-line string top they don't currently all require multi-line strings but
they're about two there well so this parse and maybe we should put this in a nested this is testing the pars uh directly
so this one is not going to be a multi-line testing which parts is this or are we uh no this is oh right we're not
testing par song sorry okay so yes so this has to be this is going to have to be there's yeah half dozen of them and so
what we could do um is uh have a method that that's called uh create songs with header and then instead of just directly
assigning it call that method and then we insert the header and so we can do that in a a backwards compatible Way by
doing that anything and then uh have the have our have our Factory method then add the header and that all the tests
will break unless we want to because I don't think we can right this goes back to the sort of the backwards
compatibility thing I don't think we can do this in a Backward Compatible way right we're GNA break all the tests at
once because we can fix all the tests at once by basically skipping the first line that's the first step um and then we
can start writing tests that including does that make sense yeah so you're saying create a um sort of a setup Factory
method here yeah so if you extract the string right just this just the the string part into a yeah and header uh and
then now now take the string and and push uh introduce oh oh control so can I pause you for a second can you bring that
menu back up I home so go to the uh extract introduce those are all Control Alt they're all Control Alt yeah so the four
main things you're likely going five actually right variable constant field parameter method all the extract introduces
our Control Alt with a letter that pretty much makes sense other than maybe method you might not think of but right V
for variables C for constant f for field P for parameter M for method so Control Alt is all your extract introduced
stuff right no I knew that I actually blanked on the P part not the control Al part yeah and I was like it I was I was
mainly pointing it out not just for you but but for everyone that that um all those are related and if you just can
remember on the Mac it's it's uh command option on on the windows it's it's Control Alt it's kind of cool when you think
about it because it's this you know sort of side menu yeah exactly and everything under there yeah except for this one
the function yeah but who I mean I I that one I rarely use so that one I don't care about it's it's one ones you're
going to use commonly like it's funny is like the order of this menu I'd probably push method the meth section to the
top to the top yeah yeah or at least maybe under parameter yeah agreed so hey there elw asks about is result a good name
isn't a to generic uh it is a generic class so this is um in our parse we created this result type that returns um
either the success with its value uh or one or more failure messages and so this is actually part of the result pattern
which is much more common in net I don't see it as much in the Java World um even though I think it's very useful uh and
this idea of the results um was a I forget if I originally encountered it but it uh if you look up Railway oriented
programming not railroad programming but Railway oriented programming um it's a very functional style of where you can
basically do a bunch of operations combined them together and you basically get success because you've mapped everything
through correctly or you get failures and then you get uh your final failure messages not have to deal with exceptions
um it's not to say never use exceptions but in this case we expect failures right we expect input to be bad right that's
not an exceptional case that's not like oh we lost connection to our database or our file uh you know couldn't couldn't
be read um and so want those so that's what the result class is so it's it it generic um and our implementation is
really simplistic uh we'll we'll get more complex over time uh because you can get pretty little uh you get pretty
interesting uh if you really push the functional aside hey there JT um so we are doing what's called test driven
development as you can see on my hat tdd um and so what you want to do is uh you break the test first um and then you
want to fix the code but because we're we're testing in levels and layers right so we have um tests at the outermost
layer where the text comes in from you know from a form submission uh so we have a test at that layer uh but then that
layer pretty much just delegates to the next layer which is the application layer that doesn't do very much more other
than some other stuff and then it finally delegates to the actual code that's doing it right so you've got two um layers
of Delegation and we can't fix the outside test until we actually fix the innermost so what we do is the the way I do it
is uh make the test fail at the outermost level then disable it and then have a make sure you have a rule that that you
don't have disabled test for very long um then go to the next level or layer uh have a failing test disable that since
you can't fix it yet then at the innermost level which is where we are now testing directly against the thing that's
doing the parsing of the of the songs then we have we're going to create that test in fail and then we can finally fix
the code once that test passes then we pop back out to each layer and turn the test back on and it should succeed if not
then we've done something wrong because somewhere in between the layers um and so we sort of do this you know outside in
and then back inside out uh uh to do things yeah more chats or we going back into the code uh let's go back watching the
chat yeah I think so we've got yeah so let's uh so let's that do that introduce parameter right that's what we're gonna
do that's what we're going to do no no no on the method inside the method itself because you want to introduce the
string as a parameter and you don't have to select anything just do introduce parameter ah whoa and this is tsv songs
whoa uh I don't know what you did me neither undo oh it's asking for the name yeah sorry I thought I was asking for the
enter so now's asking to if you want to replace this other one with that uh no I cancel yeah because it's a uh it's a
similarity um between the parameter we're sending in and it suggested a duplication that's not really a duplicate uh so
let's use this new um tests let just look at the that no no no yep do the same thing there long lines yeah y uh this one
will have to come back to but this this uh and and yeah we'll have to come back to the failure ones but let's focus on
the success ones uh that one which one the one that yeah skip empty in blank rows no you already passed it go back the
one on uh 86 we want to do that as well because it's still successful it's okay um before we move on to much further so
so far most of the ones we replacing were single single line strings this one's a multi-line let's run our test to make
sure that we haven't broken anything with the with any of these yet yeah this multi-line has me um concern that was
quick well they should be quick I mean right now I wouldn't expect it to fail because it's pretty much you pass it the
string and it's returning what you pass it right so let's do the same thing y for yeah oh I see what's happening it's
reformatting on its own yeah because you're you're indenting the the the opening triple double quote um and so it moves
things around but if you see the the alignment of the strings is based on where the closing triple quote is not where
the opening is and that's why intell is highlighting um that's where the the it Java will treat the start of the line
which is correct got it I don't know why I didn't dense it's weird a character is in from a from method call but that's
that's what it does it's probably a setting in configuration somewhere I have to look for that that song control shift
sorry Control Alt L will reformat let's see what it does with it no it doesn't actually so you could do it again and see
what row sure let's see what happens yeah so what it does it it mucked up all of ourt oh we don't want that yeah that's
good enough undo right yeah level oh hey buy coffee mug I love your avatar um go back to the top uh do we handle all of
them is there no no further tests I did that one that's it okay uh let's do a uh a commit we actually just run test one
cheap right so this was pretty much um preparing uh know breaking them in a consistent way header y all it you could
probably grab 14 and and and put that in is 14 legit uh that's something I'm concerned about let me go grab it from here
because that's 14's a comment yeah I would probably delete the comment at to what do you doing you said you wanted me to
put the header do we turn this into a multi-line and add it no no we want to put that in the in the factory method
because we want all methods now to include the header that was the the point of extracting this right right it yeah yeah
right because we want to require the header row above all inputs right and we've got that now we expect pretty much all
all the tests that are calling this are not going to fail so that's gonna be what like five five of them six of see F12
so we get one two three four five six seven tests yeah but some of those are failure failure motion oh right and that we
did not modify those yeah yeah rip yep five and they'll all fail in the way that we expected which was it didn't expect
the header row which is currently just processing as another song yeah so they're all going to be basically off by one
errors although not the typical off by one error okay all right uh so let's do the simplest thing that could possibly
fix this which will probably then break also the failure mode fine so stream uh swegi what what are we missing the
commit contain two disabled tests were there other problems that we yeah so they didn't they were they weren't fail they
were just ignored and it treats which I think is great it treats problematic so what we can do is uh stream has a a a
great um method called skip so we can do a one so now those should pass but the other those should pass but our our
failure ones will will likely fail oh failed expected size two but was one right because it's now skipping one that that
should be right because we didn't have the header so that looks header is so here um yeah let's let's put in the header
and then put in better uh malform songs yeah let's where's the header you just call the create right are we oh we're in
a different test oh we are in a different test all right then then let's just copy paste it uh well we could promote it
to to a factory method uh so let's let's undo this and then go back we can did it yeah I'm undone uh yeah so let's
promote our Factory method so the the two steps are make it static and then move it to new new class got it and the move
will change the the scope to public at that movement uh it'll open it probably to package access because it basically
escalates it to just enough to be class I'm trying my darn just not to use oodles uh I'm I'm fine with with Factory so
TS song Factory song Factory yeah why do I feel like we already have a tsv song Factory somewhere I don't know we have a
song Factory but we don't have a t song Factory right now it wants fully qualified name is there a way right so what I
usually do is um uh type another test class ah so like song Factory and then hit enter no song let it let it auto
complete the whole thing and then hit enter there go and then I then I back up and and replace it that yeah got it to
escalate visibility yep or accessibility depending yes I couldn't see your face on that it was covered by my screen but
now we want this to go to main no this only for tests test yep no take me a second uh we're good otherwise right yep
cool all right and so now we can use it from our song importer one we've already got the PRS there so you don't need to
type a AR again oh good point oh that's left over from yeah really um probably because we're in a different layer oh I
see yeah yeah yeah yeah here yeah got it so vegan a you you probably won't run into in reality you probably won't run
into any problems but if you drop the do then somebody could collide with you with their libraries although since most
libraries follow that they won't they won't Collide but they did the reverse domain name on purpose because by
definition it unique uh it's been 28 years and it hasn't yet so I don't believe that statement I'm going to disagree
with you on that there are lots of people who use package names that are disconnected from a domain name uh and that's
their prerogative you can do whatever you want limitations but that hasn't been a cause for problems uh in my long
experience all right um so how about we fix up the the contents of that test right actually that's not true medic coffee
mug that's for a DNS lookup but that is not the name of the RC's but I believe there are other things around characters
and and so on that you you can have in certain domains that would not be valid Java code but you start getting into
extended character sets and stuff like that where off actually I title thanks Mighty coff I appreciate keep we so we're
expecting two failure messages because both of those will fail um we will now actually still get two failures because
the first one will parse as uh will parse correctly oh this this test was failing before because there's only getting
one now it should now it should pass because we're adding the header row so this this one should pass again okay uh I
think we still have go ahead yeah but we still want to clean clean up the other ones that have artist yes so is that
here no it's a hetero I think that's it for this test class so now we can go back to our tsv test go to the top yeah
let's go through yeah don't care is probably okay yeah I think that's fine they're not close to because it's not the
same right there's one yeah actually I can from where was it it was in song import a test thought it was yeah there it
is three one and we want to make sure we call the yeah we're be and that one we already changed yep and that one all
right let's run them so failing well of course I know I was curious so let's go let's go to that test and see uh returns
failure result for a row with columns h oh because we're doing calling par song that's why so actually we don't want to
add the header row ah so let's revert that yep okay uh can we change the name of this test yes say par par single song
it yep well single wasn't spelled song uh prob why wouldn't it be hardcoded we we're expecting an explicit error message
where there should be two columns so what else what else would we do what are you thinking yeah so let's let's change
the the contents to be more realistic you might have that in your buffer probably do but too late actually I'm probably
gonna make a are yep big mess what's the buffer this is where control this is where control W is is your friend so you
can make sure not to accidentally do a quote and now you can just clean up the back slash n at the end as well
interesting uh not in this test the test is very explicitly saying I am giving you a song with with two columns so
columns yes that's my favorite constant is is make it harder to read indeed so when I ran we had a failure uh right
because we changed the contents of failure excellent so uh now if we pop back out to our um song importer test and
reenable the since we're now just skipping it it pass is this one IO free yeah it is yeah yeah yep and uh we can pop
back out to the other disabled test which was startup no no service right right yes uh we are planning to actually parse
uh so the current task we're working on the current story we're working on is we want to handle um columns better uh and
so we want to do matching of columns to the header row so we want to require the header row um and so the first step was
basically always having a header Row in our tests that's valid uh and then we'll start writing some tests that start
manipulating that uh asks we currently use DB unit to write unit test for repository layer what do I think um I would
say what are you actually testing uh if you're using for example spring data's repository um are you writing custom
queries and things like that in which case maybe although I prefer to just use data jpa test and and test things
directly so it's hard for me to answer that question without seeing seeing examples of your of the tests you're writing
which is a a great thing to um ask in the Discord questions like that uh because then you can share uh put fragments and
things like that but in general I don't I haven't used dbunit directly in a in a long time because pretty much trust my
omm to the to do the right thing all right um so uh we're now skipping the first line and we propagated all those things
out so yeah commit I don't really like that the wording of um yeah if you're wrri if you're writing jpql to queries um I
always look first at can you use derived queries right the method names to structure those but if you've got complex
enough queries uh again not sure why you'd use dbunit and not just directly test against the Repository that it
retrieves the right things so I always see dbunit as a a lower level thing and and that's why I just don't use it at
least if I'm in the spring framework um like want to just call the method and and expect that you get an object that has
the right data because it's doing the translation of of stuff for you and dbunit seems just overhead that that's not
needed but again I haven't used dbunit in in many years so I don't know uh not it okay commit message uh might be
important to say that we currently ignore ah but not for so what's our next want so ultimately right now we're just
skipping the header row we want to start text we're already testing for number of expecting do we want to start off
constraining the order in other words at first have it be this is the order of columns and then later on deal with we
don't care what the order is as long as the the header row column um I need an example of what you're thinking so maybe
oh maybe write a write a test yeah I'm trying to think of how to now we're artificially creating this header row that
has this is what if we change the order is that like sort of a second level functionality first level is we expect the
headers to be there in this order with these names well it's not the we don't act the whole I think isn't the whole idea
we don't care about the order we just want to match right yeah match columns so so what's what what's our first step in
that direction gotcha yeah I was thinking about baby step as like doing it partially but now I'm H that's what I'm
saying I'm not sure what what you mean by partially which is why yeah I okay which is why I don't think I have a test
okay yeah if you can't write a test then then it's not it's not clear enough for us right right right can you delete
line 13 that's gonna annoy me 13 it h uh somebody coffee mug yes and I posted a link to the source code um and we perver
j. text because it means we can not leave our editor and we're not assigning things we're not uh having contributions
and comments so there's no need for for uh anything yeah speaking of what would be the simplest Next Step um so we could
uh do something where um I don't know if it's second header but uh so there there's sort of two directions I see I I can
see this going one is still correct um but we've swapped columns uh another direction is do a better job of skipping
columns which is kind of where we were heading because I think it's it was less about order and more about oh we keep
not hiding the right columns and so we have need so I think if we had a header that had the columns that you're
currently hiding we should be able to skip those because that's really what we want so I thing it may not be the
smallest step um but uh that's all got to start somewhere something columns well it's not skip we're not skipping the
header column we're skipping that column entirely when we're parsing the rows 62 right I'm not sure I'm not sure what
you mean by that by what you um skip columns with an unexpected header that's what I was trying to say if that's clear
in other words if there's a column that's currently hidden it's going to come in right I'm not sure what you mean by
unexpected oh um that doesn't match our current expected columns which is do we have those defined well yes within this
method well but that's more columns than we actually parse so it's not that they're un so expected feels like a
confusing term to me because right now we're expecting notes but we don't do anything with it right so it's more like
that's why I liked unused which is what I didn't which is what you originally wrote in the Jura ah right so line 62 says
skip over unused columns ah which is why I was wondering why you were repeating that in line 64 thing yeah I was going
like step one step two yeah so so now we basically just you know draw draw the rest of the owl as as it were so we've
done 63 um although we're not looking at at the Sentinel at all right um I maybe that's maybe that's not yeah I'm not
sure just I'll leave it down here for only um only parse want yeah let's draw the rest of the F and Owl first draw some
circles and an oval FNL I do not know that reference but so let's um uh so we need to Define what those columns are so
what are the columns uh that that are valid that we want and those are defined in the song um in our song object right
those are the ones that that matter because that's right right now we're looking at those one two three themes so we can
put that in in a list of what are of what are um of the of the expected actual but we need to know what the column
header right gonna put this here for a second then get the column representation of them from Z Factory what do you
think um comma each for the or just do it more like 68 without the string part I think I think comma separate is fine
yeah so we don't want contributor and we don't want notes so these are the columns that we do want right so artist song
title release title release type and then one through four seams yep one second I have to pause for yep so my opinion is
this will matter more because uh we're we're going to be generating a lot of code that's going to be pretty bad um I'm
going to have to do a lot of cleanup that's all I'll say what did I miss oh I was just commenting on Mighty coffee mugs
about morale it'll be more important to know how to refactor even more so yeah so we can delete this now we list yep I
think we can drop that because we're going to require that those columns exist so that might be we don't even do we have
to even require artist being the first column we don't anymore do we no we're we we basically are currently at the
assumption that the First Co the first row must be the header row and that there's only one header row yeah so um just a
a time check we're currently at uh at noon sure could I probably have energy for another 30 um okay but I could end
sooner if you want to yeah let's let's let's go for about another 15 minutes okay sounds good I am actually hungry so I
was like how much do I ignore being um I think we want to change our instead of having enough columns does it have these
headers does that make sense in other words here we've got one two three four five six seven eight so we've got eight
column headers exist so this is a change in our minimal expectation of require nine columns uh we're now saying that um
must have these eight columns so it's not uh so that might be the F the the intermediate step before we actually parse
it now the header could have is it must columns um because we're ignoring all yes we can say any other columns are yeah
all right so let's write a test for that at the parser level yeah so we can out so we probably want start with the par
song method um which is going to be interesting because it won't have access to the header so that might not be a good
place to start but we can look at it oh yeah so right now what it does is uh the um number of columns the number right
yeah I think we'll have to start from outwards uh outwards or inward well we're at the innermost call in oh right par
calls par yeah um oh this is going to be interesting so we could start here we could start at the outer layer uh but
either way I think the interesting method because what this requires is is row because otherwise it won't know how to
how to do the mapping oh right um we could uh and this this is this is more of a a design issue um we could when we
create the row and then uh but that feels like a design choice that I'm not sure about right so currently we have a we
don't have a Constructor so wherever we're constructing it so if you look for Constructor all right so we're just you
know we can look at how song surface actually does it right it's always creating a new parser every time we call it
import songs and so right could peel off the header row and pass that in that just feels feels wrong it feels like the
service is making a decision that's really not its to make oh you were saying having this method peel off the heter row
from tsv songs right then pass it into tsp yeah I agree that's yeah all right so let's so I think we need to start sort
of uh we don't have to but I think probably starting at parse song itself um part sign there it uh we have I mean we
have a choice we could do an outside in have a test against the parse that has uh different columns it fails we disable
it and then song what do you think uh not able to have an opinion I got up at 5 this morning yeah so well then maybe
this is a good place to stop um yeah so let's uh let's leave ourselves some some good breadcrumbs for next time um so
let's uh let's go back to jira and make sure that that makes sense for us so I think the next test we write is one that
passes in just those eight columns because that would currently ignore uh to only include those those eight columns so
you're saying sorry what was the test again columns and that will fail and that will nine maybe CH maybe change the word
uses yeah that's better yeah and that would be at the that would be at the par Song level um or at the or well we didn't
decide so we didn't decide right don't know where that is yet y to do decide whether to test at par for all right yeah
Mighty coffee M I'm not sure it doesn't feel like it's the job of uh service layer to peel that off I agree that's
that's sort of my thinking is is is kind of like the parser here's the schema for year to parsing but it we created and
then we throw it away and so doesn't necessarily have to be included there um but we'll see we may end up with that but
I don't I don't know that we'll go that way right off the bat yep yeah I mean even with the the short we only took one
short break um yeah uh typically you'd want to take take more frequent breaks yeah and some longer breaks at this point
so and not be sleep deprived well that helps yes yeah all right and then um Thursday uh it is a hard stop day yep that
one is two hours yep cool all right so uh thanks for hanging out folks appreciate it as always um make sure uh if you
haven't already uh subscribed and followed on the various platforms you do so as well as joining the Discord join the
Discord if you're not already there otherwise uh um I'll probably be doing a solo stream tomorrow uh and then Mike will
be back with us on Thursday same starting time as we did today 9:30 a.m. Pacific uh which is 5:30 pm UTC and we'll see
you bye
