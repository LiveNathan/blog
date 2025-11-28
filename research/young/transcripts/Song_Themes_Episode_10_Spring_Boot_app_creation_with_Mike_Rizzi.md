# ＂Song Themes＂ Episode 10： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=xGcLTlRl0s8

---

## Transcript

okay all right hello folks happy Saturday yeah so uh we're gonna be streaming for a couple of hours as usual we're going
to be test driving uh implementation of Mike song themes app anything you want to say say mik before we dig in no I
think just dig in all right so uh let's see so where where did we leave off let me add that probably should run all
tests if we left ourselves a breadcrumb yes let's do that I think we didn't but we'll find out it's always good to run
all tests when you start a session anyway true I just noticed you're on Spring boot 320 probably want to upgrade that to
321 not that it's urgent but always good to stay up to date meaning do it live or do it offline another time uh we can
do it offline or maybe if we have a few minutes at the end we'll do it okay it should literally be just change the zero
to a one and everything should just be fine what was the number again three uh 321 let's see see what is uh what's the
calendar look like calendar ring iio let's see when is 32 322 comes out in a couple of weeks so yeah probably good to be
up to date on that you said 32 or 322 uh 3.2.2 comes out on the 18th gotcha um so yeah so we'll want to keep up to date
um so no no no breadcrumb tests so let's uh we got this thing where we left off yeah right so we wanted to add more song
attributes Searcher code and so uh some of us mainly suiga and myself uh had had played around with different ways of
doing that um that indexing uh so I thought I'd uh oh thought I'd mention that we tried a few different ways and it it
turns out that um either a for Loop uh basically a nested for Loop or a nested 4 each is actually the most readable um
oh most readable code yeah so uh let's see for those of you who um that's the experiment you had yeah uh oh that that
might have been it yeah I didn't I don't think I ended up putting desan uh so let me see if I can so this this is the
fun part about um if you join the discard uh we have dedicated Channel to um basically talk about stuff that we do on
stream and um the uh I'm GNA copy and paste this and then I'm gonna put it on my screen so let me see where' that go
Searcher when you say copy and paste I'm G to paste in my local thing and I just basically just so I can I can show
folks um me screens so we see here is uh this is basically the same the same thing so um given a stream of of songs what
we want to do is we want to in a sense the the operations that we're doing because each song has multiple themes we need
to in a sense denormalize the data so instead of one copy of the song with its multiple themes we basically copy the
song multiple times one per theme so we end up with song theme song theme song theme um and that's what uh so that was
one of the things we looked that was sort of doing a flat map but it turned out that um it's it's just easier to to do a
compute if absent so we did uh a different thing um but the comput if absent uh so if we switch to your your view again
so I'm gonna switch back your screen let me move out so yeah so in the original uh or in the current version uh if you
scroll down a bit we have the the getter default but actually what we want so on line 27 we've got get our default and
then we have to add the song and then we have to make sure to put it back in the map um compute if absent uh basically
does that in sort sort of one operation so uh I'm G to switch back to to my screen now um and so uh the compute if
absent um we basically say uh if there isn't already a list there um suig use set but basically it's it's same thing uh
we create basically a new placeholder for that theme and then uh but either way we then add a song and so this turns out
to be the actually the I think the most readable the other alternative which which I came up with um actually I didn't
come up with it uh with quite a bit of prompting chat GPT came up with it um chat GPT came up with some very inefficient
or very confusing ways to do things uh and so I had to push it to say no no can you come up with something simpler uh
and so it came up with this nested for Loop U which is basically for each song for each theme in the themes compute a
fatson and then add it and so that so these two are basically equivalent this one is using nested four Loops uh and this
one is basically using a a four each uh I don't so as so I was saying in in the discourse like I'm not sure which is
more readable the first one seems more readable because we've seen at least I've seen four Loops all my life for most of
my life um whereas the four each is a little bit different but they're uh essentially the same um and so uh and you were
saying the first one's less efficient um you saying the one that chap GPT came up with was well it's so it turns out the
one we did and anything doing with streams um and and chat GPT came out with with a bunch bunch of different
Alternatives were were quite are pretty inefficient now of course we're never getting to the scale where that matters
and so it's so for me it's much more about what is the most readable turns out I think this is this this for Loop is
much more readable uh and it turns out to also be probably the most efficient um at least at this level you could always
make things more efficient and so on but I think this is because it's not creating temporary iterators and it's not
creating a lot it's not creating a lot of temporary stuff which is what streams uh sometimes end up doing especially
when you're doing some of the flat mapping and and and grouping that that uh are some Alternatives so anyway if you want
if you want we had quite a bit of discussion around this uh so um as usual if you want to know uh how to join those
discussions you can always uh if you're not already there join join the Discord so just ted. Discord if you're not
already there um and again we have a a channel dedicated to talking about stuff that that we've done on stream so that
was that was the experiment that I wanted to do and and uh and so uh so there we go so should we Implement that one
there more the more readable one yeah so I think uh doing um we could do the nest for each it's basically the same thing
under underneath uh whichever one you prefer um but I think either one of those is going to be better than than than
than what we currently have yeah I agree with you the first one let's go with the first one again probably because I've
Decades of for Loops y yeah um it'd be interesting what um some of the newer developers is more readable to them who
have a different Paradigm of what they you know how their career Arc went right you know like did they never did for and
they went straight to 4 each and streamed and not M you know could be interesting well it's it's funny though it's like
streams have been around since since Java 8 Java 8 is what 2014 I think um long time ago like there are likely very many
developers who started programming in Java after streams existed yet my experience with work with such developers is
they don't use streams and it it's it's just a sad State of Affairs that that that that's the case it's like learn learn
streams they've been around for for for very long time uh they aren't necessarily the most efficient but we're not
always about efficiency right we're always we're we're often about readability um and even though here we you know we
ended up with something that uh I I think it's it's a shame not not not to learn it one thing that so agree one thing
that I think was really interesting about and this has been my experience with interacting with with tools like uh like
chat GPT is you really have to to know what it how to evaluate what it's what is giving you um because I was you know
like saying here this is what I currently have can you make it more efficient uh can you make it easier to read but you
still have to evaluate it and you still have to test it to make sure it's it's still working properly because there's no
certainly no guarantee uh there's nothing inherent in these tools that will give you code that that's working um and I
and I I really caution folks when they use tools like this that you have to know what it what it's doing um you have to
understand what it's generating and you have to understand what you're asking for at a higher at sort of the next level
up of of architecture or abstraction uh because you could certainly ask it questions and it'll give you answers but in
no way does it say this is the right solution for your problem and one of the things I've seen happen then uh is people
Implement very complex things that are completely that that work but are just the wrong solution because they're novices
and didn't have any way to evaluate uh what was an appropriate solution um and that's where I think these tools can be
sort of dangerous in the sense of leading you down a road that is that is not when you should go down uh and you end up
with sort of complexity built on complexity built on complexity when hey FNAF welcome doing great uh so you said
something some Architects say that four is a code smell in Java four Loops I I think whoever um should take a look at
this code and say and tell me and tell me that it's that's not fine like there are cases where uh streams are a much
better solution but I wonder if that architect is thinking of an index for Loop where you're doing you know in I equals
zero semicolon you know even even that has its uses um I I think so true I react very badly to to generalize overarching
statements like this is bad like four Loops are bad like sometimes they are the best way to to to do things um so I I I
I I I that's why I try not to make blanket statements um other than you you know like even tdd like you should not
always do tdd you should do it when when it's appropriate um but I find uh like there like here here is you know here
was a case where really the streams ended up being much more complex we actually came up with again if you look at the
Discord you can see the solution um uh I'll I'll actually copy uh I'll cop here I'll copy uh what what chat GPT
suggested for um basically that was that was pure streams this so this is a pure stream implementation this is terrible
from a readability standpoint this is terrible like I'm sorry compare this stream implementation with this lovely for
five line for Loop which is really just three lines of clo code and two closing braces this is terrible from a
readability standpoint it does the job um but it's just like trying to figure out this is actually doing uh is is not
straightforward um it happens to use a map entry uh suiga created a pair class that that did something similar that was
slightly more readable um but still it's like this flat map and then a collect with using a two map and there's other
ways to do it that that's not quite this this complex but it ends up just streams don't have the power to to do what
what we want to do in a way that that's that's straightforward um so uh so what uh so I'll give uh chat GPT the benefit
of of saying it also came up with with this implementation so this one um so this longer one is basically I said hey can
you do this using the collectors to map and so it said okay I'll do collectors to map um and so I in this case I kind of
let it down the road of I was just curious what how it would generate it uh but originally when I said can you use
streams and and grouping by this is what it generated but even this I think I still think this which is you know
technically just as many lines of code as as the four Loops uh it's still it's still much more comp loops and you sort
of have to figure out well what is this flat map doing and then what are you actually grouping by uh and all this this
kind of stuff so um streams are are are not always the readability all right I know that was a bit of a a tangent but
but I thought it was some really interesting uh experiments that's cool so should we uh let's get back to your screen
and so do you want to change the implementation to the for Loop um would that be our first task sure if you want to do
that or just do it offline we can do it offline um focus on more let's uh yeah let's let's maybe maybe do it offline um
because uh I want to get to adding adding feat me too okay all right GNA Matt add more attributes to our right currently
small record but we want to drive it by tests I presume is what you're going to say yes so I think the the last thing we
did was we we pretty much um encapsulated all the setup so that uh in preparation for this step right that was that was
the last thing we did um and so now if we look at uh um basically where we actually instantiate this record in our tests
uh it's pretty much just in our Factory um is uh and so this is this is interesting it's like you know what tests would
we want to write that would push us to add these attributes um and so for that we probably want to what uh or sort of
really the the probably the service layer which is you know how how we interact with our with our application um what do
we want to do there so maybe let's look at our song Service uh tests for what are we doing um in terms of of adding you
my brain just fell out what was the F12 all that just to see the three names of okay yeah I mean there's only there only
the three we we want we want the added uh added songs so we're just basically there on line 41 on the top um uh so we're
basically saying to the factory that one that one really it's 45 where we're actually adding the song right if we wanted
to to drive this by test and here's a case where like I don't have a strong feeling that we necessarily needed to drive
it by test because the other two pieces of data that we want to add to the song the release title in the artist I think
it's three actually uh was it three release type yeah ah okay we talked about possibly grouping those into another right
but that's more of a when we really need it kind of thing yeah um and so really the question is probably more at the it
would I think any test would be more about how do we want to view the UI um because even right now all we display are
the the titles when we do a search by theme right uh so do we want to start there and say what do we want there and so
that would be at the level of our adapter and so that would be our test and so here we don't even say much about what uh
what the content of the results are we just say that that we get some search results um and so we we have to decide sort
of where do where do we want to start with this um where we may want to start is again since since our sort of larger
goal is to create a UI to add songs um maybe we want to start there that if we add a song with the these pieces of
information uh then they're all saved and that might be the best place to start then so you might start literally at the
UI layer not subcutaneously um I I think I think we can still do subcutaneous but uh at some point we're gonna want want
to implement that UI yeah no it's for sure and then I have and then it's to me it's this one would be well both of these
will need Authentication right um well yeah so when do when do we want to add that because uh like like we had mentioned
last time um it doesn't matter until we have persistence right and right now we're not persisting but once we do right
once we do we'll need authentication um so I think that that is pretty much dependent on on persistence because if it's
not persisted who cares and who cares what coupled and for me certainly adding songs via UI is for me this one's
probably more useful being able to bulk load a a lot at once but we do have to build the single song for you know I
could always bulkload one song contribute but that could be interesting conversation all in itself is should we build
this you know adding one song via UI versus doing a bulk load first and that may be a can we kick down the road until we
until we do the attributes um yeah I mean that'll that'll come up pretty quickly uh I mean that'll probably be the next
thing we think about but we can certainly say for now now uh let's not let's not worry about it although we are
designing the use case for single entry uh single song entry because it's not um we're not handing it a file we're
handing it basically individual attributes yeah so um so I think we need to actually decide that now do do do you want
the the first way for you to enter song bels to be bya via comma separated file or is it UI well it's not entirely just
what I is either way until we do persistence it doesn't matter so much because we're just gonna well if it's adding by
song via the UI without persistence then I would um maybe want to go to the bulkload because we have to keep reloading
you know every time we restart um but adding a song via the UI feels a little bit simpler though the bulkload is mostly
just a a loop through adding a song and then parsing from a file so well a strong opinion I'm just thinking out loud
here I mean I think either way either like I think persistence is is is the the next thing we want to do um after we do
something that we can enter songs from the UI so the question is is which do you want to persist do you want to persist
a single song at a time or do you want to persist uh having loaded uh CSV does that question make sense no it makes
sense it's just to me it's very much a coin toss um once we have persistence though I would definitely prefer the bulk
load um so maybe bulo is the way to go um then that's gonna uh shift things a bit um because then we need to figure out
what uh what is that what is the format of of the CSV if it's going to shift significantly I'm okay with going with DUI
it's not mind because if we're adding it first as then yeah well you're the customer so you flip the coin I'm not going
to make the decision developer yeah let's go with bu load all right yeah so what does that shift in your mind really so
that means we need to uh uh figure out what is what is the flow of the UI so we can figure out from an outside in
perspective what um what are we actually providing to to the application what are we what application hey James welcome
that's interesting howdy uh tkes did we do performance improvements no I use out of the boox intellig I don't I don't
work on projects large enough where I have to performance um so uh so we want to look we providing a file that we're
that we're taking from your machine is that what where how it starts off yeah it would probably be like that um so we
have to have like a file picker from the website unless you wanted to do a back end bulkload that doesn't have a UI
that's just you know like a CLI kind of thing so that's so you bring up a really interesting yeah I know I'm like I'm
thinking lot here um so I'm I'm working with with someone who uh who has they where they what they're building is has
some very similar aspects to this in that users don't really edit the data they mostly are searching and viewing the
information um information is is bulk loaded by the person who's running service and they're generally doing that in
terms of loading the information in production but that's not necessary they could have something running on their
machine command line or or or otherwise that still writes to the database in in the cloud because that's where the
system is running but the thing that's actually loading that data doesn't actually have to run as part of the
application um so the advantage of that is you have a few there are a couple advantages one is that's the only way you
bulkload data in and so there's no worries about authentication and things like that um in fact since you're not
deploying that aspect you don't have it's it's much much easier to to develop um the downside is is that you are making
the assumption that only you can do that uh which means if you ever want to open it up to contributors now you have to
go and Implement uh whatever you know because you basically didn't implement the stuff in production um but those are
you know but depending on on the kind of service that might be totally totally fine I think eventually I would like to
open it up for contributors to not just contribute one song at a time and tediously have to go through but to be able to
bulkload right um either way we're gonna have to do authentication if go that route right um but if we could get farther
along without authentication yeah May does it it may make that our lives a little bit easier yeah I think we're I mean I
think you know like we said as soon as we have store persistence in the database we're but the authentication stuff is
not for for basic authentication it's it's not really that heart uh in the sense of it's very well known we I know how
to do it uh so it's it's not something we have to research and Spring Security at its very basic provides generally easy
ways to do it as long as we're delegating the authentic the authentication and authorization to somebody else um but
getting back to to the to the file upload there there actually one two maybe three different ways to do this um one way
is file picker and we pick um an Excel spreadsheet and then we decode the Excel spreadsheet directly uh the second way
is still a file picker but we say no it's only you're uploading a CSV which means from Excel you you save it as or
export it as a CSV uh the Third Way is don't bother with file upload at all provide just a big text box where you copy
and paste the CSV right now turns out when I was implementing kid money manager and I and the first thing I had to do
was import the data from the spreadsheet I chose that route because I'm like I don't do this very often um and I don't
have to do a file upload right yeah it's a cover which isn't hard but it's like basically I didn't need to provide such
a beautiful way of of importing files because I did it so so rarely um in fact I did it twice and that was kind of it
because once I had the lat data loaded I didn't need to load the data anymore it was now it was now loaded right so um
and I could see it getting more complicated at some point when it's opened up to other people than me like hey you're
you know it doesn't match the right format or or even like here's what I'm about to import here's what I think it looks
like yeah you know like sort of split it out in the columns visually yes and have it go is that what you're thinking you
know right and you say submit right and and there's all sorts of well you called this column title but internally we
call it song titles that which title did you mean um did you mean song title or release title and then basically
matching up the columns right and as you're saying like you you could get pretty um friendly and and right easy to use
but that's a lot of work uh that may or may not be worth it but it's it's certainly you know what is our minimum minimal
lovable app um and and the the easiest to get going is is probably just pasting it into a edit box a text area yeah text
area yeah heye hey swegi you missed the part where we're talking about the theh the indexing stuff so you'll have to
watch the the replay um so it sounds like uh we probably want to go that way so where what we get from uh the what we
get from basically the post right posting the form is a bunch of lines of text that are CSV um does that sound right and
then yeah in a in a very specific format so we can be very much like it must be this this is what we expect um and we
can always loosen that up later but for now since you're the only one uploading that or copy and pasting uh you can you
can do whatever is convenient for you yeah and it doesn't even need to have a header row that says right this is artist
this is song title right we can just say it's this order period right um yeah that so um then uh maybe let's sketch out
here what what would what would that look like what would the CSV look like especially in light of the fact that you can
have one to many themes right uh hey James uh yes so the the Blackjack Ensemble blue is what uh we've been working on it
as an ensemble for for about three years uh and it's all it was the very very core original code was not test driven uh
although did have tests as part of a course I teach on refactoring to testable code um but everything we do driven uh
that's a big topic I'm going to hold off on that um and maybe we'll we'll talk about that later if not uh uh I'll make
sure to talk about that on stream because I have opinions opinions no but it's not it's not a short answer and I don't
want to Sidetrack us too much yeah it's a great question yeah so what um so what do you envision the the CSV looking
like so looking at my into I don't know why I'm moving out of um release type's going to be an interesting the themes
plural yes so then that's going to be interesting is in should this I don't know about should I'm gonna take away the
word should should have could have as it's the way if you've ever exported um or and as many as you got it'll take it
right um or so this is the the question that I'm starting to think about out loud is do we do it that way or have some
way of subdividing themes yeah I'm just going to pick this just for Giggles um but something I don't know semicolon
things that aren't likely to be in a in an album title I mean in the theme comma is not likely either but we'll just do
semis for now or do we have a column with them all spoed together with some separator well since themes will never have
commas in them I assume imagine um really yeah so right now they've all been one word okay but they might be two could
be yeah there actually let me go take a look I mean like you had New Year's yeah New Year is two words and that has it
may or may not have a a a apostrophe yeah I'm not worried about apostrophes I'm worried about commas commas yeah I'm
trying to think I don't think well I don't have the ones I only have the spreadsheet hyphens I think that's an
interesting one let me go see if I have it easily spot here this friend of mine gave me a bunch oh my God in 1988 she
gave me these lists um I'm looking for any there was something that was sentence not jumping out at me like all night
that's two words but it's not really a sentence yeah so so again the only restriction I'm think about is would you ever
have a comma and I can't think think of a theme a comma um and if it does we would we could adjust at that point um so
I'm thinking that uh sort of the the one of the better CSV formats is everything sort of in each column has double
quotes around it so each column you have double quote contents the column double quote commas outside the the the quotes
and so that um that gets that gets you all the benefits of uh you can put commas inside double quotes and it doesn't
interfere with with the parsing right um and you can then do things like for your themes you could treat that as one
column by putting double quotes around the entire set of themes uh and it helps with having spaces and other characters
that might get might might be otherwise problematic right so you're thinking like this right now on the other hand what
I'd be optimizing for is what's the easiest thing for you to export from your existing spreadsheet and then adapt to
whatever that is I frankly um it's very easy to take and this one's Excel it could be Google Sheets of course um for me
it's very easy to convert like right now it's multicolumn so for me me right now it's literally be one I think up to
five um but I can very easily you know have those columns collapse down to one so I don't think sure and and that's fine
um I believe that computers should should work for us and not the other way around right right right uh we don't we
should we should not work for machines machines work for I mean even though it's easy like yes it's literally one
formula in expel in Excel that you just basically copy and paste but that's work and you got to check it and I'm gonna
I'm gonna I'm gonna Devil's Advocate you a little bit not on the philosophy the philosophy I totally agree with is I
feel like I failed in that spreadsheet by starting out and having multiple columns the reason it's a fail is if I search
for let's just say Halloween and um werewolf mhm okay well now I have to search multiple columns I have to do a columns
it's a little bit trickier to use the spreadsheet is what I'm trying to say with that design right sure but um but if it
if that design got changed to being one column with all the themes comma separated my life with the spread sheet would
be made easier sure and if and if that was and if you're you're if you're going to do that anyway then I'd say yeah okay
fine then we'll use we'll use that format because you're GNA end up with that format anyway yeah I'm piing up whether I
want and so so so I agree like yes you know it makes the usability of the spreadsheet as it exists if there are separate
columns it makes that worse uh and and putting it into a single column can make it better although this is where I'd be
like writing a little function uh that would do that work for me across multiple columns but well and I just realized
the downside of of combining those columns into one in the spreadsheet is that um right now here I'll let me just make
it so that it I can bring it over into view so right now hey you be quiet no no no what are you doing um hide go away
Dropbox so here the nice thing about each column is I can quickly look at what they all are so now I'm kind of going
back and forth like well maybe it is useful to have them like you said you would probably write a a macro to uh yeah to
deal with it if I were if I was still using the spreadsheet still using the spreadsheet but the idea of this is to get
rid of the spreadsheet yeah so where were you headed with your design thought was besides just pulling it in as I've got
it was there another angle on that uh no basically like I want you know and uh like sui says I'm channeling my my in G
paw although I I very much believe that before GAA has expressed it is that there's far too many applications where you
work for the application and the application doesn't work for you right and I think that is I think that's just a very
sad State of Affairs I think it's it's unfortunate that um that we have to change the way we do things instead of the
computers changing the way they do things and I recognize expensive but like that's that was that was the vision of
computers make our lives easier and all they do is make our lives harder so given that I'm thinking not changing this
structure of the spreadsheet just uh having to decide here on the top you got me cornered in the conference room i' got
to make a decision on the product owner that's right and it's not a it's not an it's not an irreversible decision
exactly that's kind of where I was going with was we just gota we gotta choose we got to choose Direction because we're
we're stopped on the side of the road yep so the current one is option D then if I don't change the spreadsheet right uh
Swede asked that if there's any significance to the order of themes and my assumption is no no yeah it's wor I yep uh I
think the only difference between B and D is D follows the double quoting pattern that we want to use right uh then and
there we go okay so what we can do is uh we can start writing a test um so why don't we take uh a realistic example for
our the option that we chose okay um and we'll we'll basically have that kick off our test sounds good let some how
about songs I'm getting tired of Christmas Halloween and yeah new holidays are over let's let's I got Angel okay Angels
oh I don't have album titles though oh I do for they're all comp ones that have titles let me move up find something
titles ah there's a lot of ones with titles for songs related to fatherhood daddy um here this is only got a single
theme though that's fine gotta start somewhere yeah and and a single theme would be the and a single thing would a
single theme would be the the this the yeah the the yeah and then this one would be empty because we're talking release
title release type and be so suige brings up a good point uh about are we sure that if you exported that row it would
appear in that way um I'm like 99% sure uh me too but perhaps we want to actually export so basically copy that row into
a new spreadsheet and then export it and then make sure it looks exactly like that well export in Excel it's basically a
save as yeah save as because export generates a PDF yeah uh do they have an X actually they do have some additional oh
interesting so they have you can either do save as which is what I would do but I just learned something is that you can
actually pick under export change file type and then CSV is there yeah though wouldn't that actually change your file to
be that and you not old one but it says it's under export though that's confusing for change file type then I'm assuming
it means save as with a new file type but I'm not going to do that experiment on this one I would do it on a raw on a
well you're gonna create a new file anyway so it doesn't matter yeah you just want to copy the the one the one the one
um and I know we said no header rows but if your spreadsheet has header rows then we should assume that that's what we'
re going to get again we want to make this so you don't have to do any change right make this as simpler as simple for
for you the user as possible so you have to do the least amount of work on your own so I've got three header rows just
to make things more complicated then whatever you've got we should handle okay so in that case let me I'm gonna I'm
gonna have a have have I'm gonna Advocate I'm gonna advocate for for the user there you go even if you're not because
I'm gonna I'm gonna say we want to make this as easy as possible for Mike Rizzy here we go okay and I have contributed
but we're just going to ignore I have other columns right you got to remember this I'm gonna have to export and dump so
that's great because right if we're saying right now we want to ignore those columns then we actually need the headers
um to help us ignore those columns because again I don't want you to have to go and and create a new spreadsheet where
you're manually removing columns uh just so you can export the thing just so you can import into song themes got it okay
so that means I have to fix these columns uh titles which I no we will adapt to no I understand but song title so this
one artist SLB I mean artist is fine we will internally it as artist you're going to BR be me we will not force the user
to have to go and change column names but we don't we're not going to make it available I want to make Mike rizzy's life
easier that's my goal but I feel what I'm trying to say is I haven't settled on these column names so if I go and change
them to do knowing me then the app will adapt okay the computer will adapt to to you and not the other way around I mean
look I you know I I'm I'm I'm being a bit fous like and it's it's more for for for anyone who's watching than for you is
is I wish more developers thought in that way of I will adapt to whatever you give me even if it's a little bit more
work on my part because I will then make my users life easier so if you want to do some work to to to sort of clean up
the spreadsheet in order to import it um whatever whatever you want but uh I I think it's important to for for folks who
are watching like to think about how do I make this easier and it and if it takes me like half an hour more isn't that
worth it um given schedule pressure and things like that I understand it's not always possible but um a little you know
developer is having more empathy for for users is is always thing um toward that end yes where did this go second I did
theh export oh there it is where' it in that's what it does interesting so it doesn't it doesn't um yeah I could drag it
into why did that come up Carbonite setup Jesus just pull this in here it's it's interesting to see what it does okay so
it looks add a straight text so it's interesting it doesn't put um quotes around column titles there is probably a
setting that does that or at least I would expect there to be a setting uh from my recollection it's been a while since
I've exported but from my recollection there's a way to to do that so rather than I actually would like to move forward
with a simpler approach for now and still keep the the customer in mind is let's just do it with no headers for now out
of the gate and just with a simple example and build up to the header thing because I feel like it's a bit of a tangent
at least from my mind because I want to I don't want to be trying to figure this out live like how to get Excel to put
out quotes and all stuff okay just I don't want to spend everybody's time butting with Excel and going this needs you
know how do I get it to export um such that it much pretty much just there's probably options yeah I mean uh and suige
brings up a point that that I was going to make which is we don't necessarily have to process those header rows we can
just ignore them we can just ignore the first what was it two lines three lines three yeah three so that's easy enough
to do okay um but but I'm also fine with with saying since you're copying and pasting it into the text box that you
could delete it yourself uh in order to simplify our our work uh and simplify our our tests a bit so I'm fine with that
yeah and I'm totally in agreement with the the GPA approach you've got as well um and I think that should be the end
game for sure like we want to make it so that you know we look at the headers we can ignore columns we don't know what
they are so if somebody's submitting so for example I have a whole bunch of more columns than than these right we got
whether it's radio friendly you got a note section which we haven't talked about actually think we talked about a bunch
of additional coms we just are right are we really at the hour already um yeah we're just we're just about are at the
hour so why don't we uh why don't we take our break and then we'll launch into our first uh our first break woohoo so of
course you know that's that's the thing about breaks is while you're on break you keep thinking yes which is why I love
breaks yeah it's like they really are important and I was realizing that if we're doing Pac and a a text box that the
whole header row thing is kind of a mood Point yeah that's what I was saying before is like if we're gonna paste it you
could just delete the first three lines and or not even delete just select all or just select what you want yeah yeah
yeah same same thing yeah so yeah cool let's rock and roll uh let's see um we were talking about going from controller
down yeah except I I I noticed that you have basically an empty column for release type yeah did you want an example
that has something no I actually think that's that's useful to know um I actually realized that we probably want to just
use uh the ones with the actual names of the columns rather than than a real example because I don't uh we could do that
later but I think actually it'll be easier for us from a test standpoint if we use something like uh what you have
actually in row in option D so yeah so where we're going to uh start the test is um at the the service layer because
that's the first place where we go from um getting it from our our controller is form submission it'll be in some form
object and we'll basically have just one Big Blob of text uh and what we want to do is uh yeah let's start a new test so
ad songs uh bulk or bulk ad songs using C using CSV format something like that y so we're gonna right so we're going to
assume that the controller just passing text yeah yeah pretty much it's going to be uh right now it's going to be easy
because it's one line um but we'll have to handle multiple lines um and we'll just assume it's one long string and then
we'll split it to parse it into multiple lines and then we'll parse each line so we're going to do um this one first
yeah I would say actually with with only one theme uh and then we'll we'll expand it to have multiple idea actually we
could just start by assigning that to a string can we yeah that's our our string you can you can say uh you know just
row equals equals uh but you will need to actually Escape that so uh grab the whole thing yeah no yeah that's not gonna
work because you whoa what happened uh you copy and paste problem oh I see yeah to old school okay so cut that to the
clipboard now put a double an empty basically an empty string past and now paste it it'll put in the slash yes right
right right because intellig is help is helpful and smart sweet um all right so we now want to have uh a new so what are
going to do uh we're going to expect that when we add this song it's basically saved in the repository so let's
repository it's a variation on this yeah I forget if we have one that basically doesn't take anything I can't remember
either um so what's well I gu yeah it's complaining what is the sequence control space uh no sorry control space on the
other one left yeah because I want to see if it auto completes any other options I guess not um we can go look at song
repository itself because I don't remember what it has uh takes a list well that's the oh interesting so we don't so we
don't have one that basically starts out empty um how about we create oh create another one so let's do let's do it the
the good old uh tdd way uh well refactoring way so let's write what we want so we can say uh new array list is the
create um and then let's extract right side of that that whole statement so from song repository. create through the end
yep and let's extract that to a method and we'll call it create empty oh there it is create empty yep and then we can
move that repository I always good the other F6 um yep and that's it right escalate you know turn it from private into
public get rid of the attribute uh and just since we're not we're not consistently using the annotations you can drop
the not null there on the bottom line 21 oh right somebody had asked about that in the last stream that we had yeah so
it's I I use it sometimes like maybe in test code um because it gets generated uh when you actually extract the method
you can tell intell J don't bother with the annotations uh at some point I'm probably going to decide that I want to
really start nailing down those annotations in preparation for uh some upcoming stuff and uh with with nullability and
things like that but for us we're we're not that um all right so we've got an empty repository we've got our our row um
let's go ahead and uh as part of our so that's all the setup we need uh oh we need sorry we need the song service so
let's create yeah and now we can call song service um what do we want to call this import ad bulk ad CSV ad add CSV I
don't know um I tend to like methods to be start with a verb when possible so add bulk then or add bulk songs or is it
implicit because it's a song Service uh I mean we could just say add thongs and that it happens to be oh plural and it
happens just just to be text string although I feel like there's an implicit um conversion happening which is why kind
of like CSV in there uh bulk either CSV or import to to get the idea that that there is some transformation so I'd say
import songs oh I see you think there's value in saying CSV or is that a bit too detaily I guess if we had multiple ways
differentiate yeah at this point I don't I don't feel the need to to down yeah yeah I'm with you and then takes a row
right or not a row it takes a string uh it takes a string yes yeah we'll change method uh fala asks why not use some CS
rerer we probably will we're not there yet yeah um create this in the service right yes okay it what do I want to call
this not row CSV Hungarian a and that might be it or so that's we get the setup we get the execute so then the action
the assert would be well we're not returning anything so right and that's why we're checking the repository right so
let's see the simplest thing that would work is we gotta query the song repository yeah uh and we basically expect it so
the the the minimalists expectation if we ask for all the songs is that there's one yeah that it's or even more minimal
is not one I think one is yep cool this is going to fail let me switch to um where is it shift 10 the other alt shift
F10 there we go uh just IO free I presume at this point yeah yeah all right uh so tram Stars brings up an interesting
point of where do we basically do the parsing of the CSV is that right application or is that adapter adapter well
interesting uh I wasn't saying the answer was adapter saying I was saying in unison the same thing you were saying yeah
and so um one could argue both ways one could say uh the the you know convert in external presentation external
representation into domain objects uh one could say that that's the job of the adapter um on the other hand uh it
requires coordination with the domain anyway so even if we had um for example we got an email address uh uh where does
that you know it would still require some kind of factory or some kind of uh or the object or the domain object itself
to uh be given a string and and and you get an email object um the other thing that come you know that that I think um
would we want to do this work adapter right so if I want to keep going if we want to have a CLI I probably want to do
the same thing and I might point it at a file and it would read the file and then call call this method yeah so the
adapter would just do file and then calling the domain well the application the application yeah yeah so it this is this
is an area that that I don't I wouldn't necessarily like if somebody suggested no let's put it in in the adapter uh I
wouldn't I wouldn't actually have a problem with that um because we could push it into the application when the Second
Use case arises where now we need example yeah and if and and and this is where where for me it it does get a little bit
fuzzy is uh even if I'm doing even if we're importing CSV you know we've got a rest API that supports that we've got our
UI and we've got a CLI and maybe even stuff comes in from something else um does that mean it belongs in the application
not necessarily it could just be that there's a shared parsing Library that's used by by all adapters um for me because
this method doesn't mention IO and it is very close it is basically parsing information um I I these days I kind of say
let's put in the application see how see how that feels uh whether it belongs in song servers or some Factory method to
to do the parsing is is is is again it's sort of it's sort of fuzzy um let's see tramar says my opinion CSV is same as
API terminal anything external if you change domain you also change external stuff I mean that's true in in general
right even if you know if if we change what gets passed in anything if we say hey we're now adding more attributes to
song well we do have to basically do changes up and down the uh the the set of layers um and so this is kind of my
feeling it's like this seems like a good place to put it um maybe it's wrong uh we'll find out later but again because
it's there's no IO here uh it would be easy to move around uh and I think it it's it's sort of tempting to try and
figure out what's the perfect place for it I know I get CAU up in that but I think because it's going to be easy to move
around uh I'm not gonna worry too sense hey this Noob uh do I have a preference on template engines uh when it comes to
Java applications with spring boot time Leaf I think is the only choice I know there are other ones uh JSP for sure not
um there are other ones but one of the things I like about time Leaf is you're basically creating HTML files so I can
preview them in a browser uh there are some other template engines that are more also up todate um that don't do that
and I personally think that uh being able to preview and design your HTML Pages without having to run it through the
server to see what it looks attribute and yep today's perfect might be the wrong place tomorrow um when we have more
information we can always mooving around y uh so did our did we run our test I we may have done it I've totally
forgotten so we did a while ago and it failed but that's because it was returning let's run it let's run it again sure
if you if you forget you can always run it again fast yeah um I use the shortcut key all the time and I'm often uh
perhaps surprise isn't the wrong word but but I'm um like this is such a a handy shortcut I don't I don't it's it's one
I really can't live without so control shift enter or um on on Mac it's command shift enter is basically complete
everything so it generally does a good job it doesn't always do it perfectly especially is when when you're inside of a
multi-level parenthesis expression uh but basically no matter where your cursor is it will jump to the end of the line
close the parenthesis if that helps uh and put a semicolon at the handy see uh okay so what's the quickest way for us to
make this pass are we just uh add a song hardcoded repository so now do we feel like we step add or yeah you have
something in mind so no I don't but I just just I just I was so so finish your thought oh um no I was thinking out loud
and so that's why I was pausing because my I wasn't coming up with another approach I mean the song right now is a title
and a theme um where were we you want here song service where are you there you are song and just make the title just I
don't know the whole the whole string coming in from CSV which is not so helpful but it would get us to pass is that as
helpful a step as hard coding a song I'm not sure that's why I'm thinking out loud yeah so so suige brings up sort of
what I was thinking of is is oh change the assertion is if we do want to take a bigger step we would have to create a
more precise assertion um so we we would want to say something like uh we expect that um the song that's in the song
repository matches matches our our string uh and so I I kind of feel like we could do the well just you know add a new
song and just maybe leave all the attributes empty or something like that um but let's let's just make let's let's take
a bigger step because because I think think we're going to need to drop down a level pretty quickly that's true pretty
much right away because we're going to have to and there are sort of two two directions that we're going to have to go
which is um the the CSV parsing and the adding of additional attributes uh so let's let's change our assertion to be
more precise and what did you have in mind well I think we can do it contain yeah it's still all songs okay and that
contains exactly and I think you can figure out what what we want to assert and you're saying I want to make sure we're
probably want to use the song Factory by right so were you saying just take the entire row and put that in no no here we
here we want here we want to actually okay right so we're we're making this a a much sui use bigger which which has a
nice aspect to it um I tally tend to call this a more precise but it is a a deeper assertion is that what you mean yep
okay right because that's what we'd expect right given that row of CSV given that we're only pulling out right now two
two of those pieces attributes right right this expect and even that's not going to work because we're not parsing yeah
clearly that's not going to work because it's going to say there are no there's repository yep now we have a different
so now what we can do is we can sketch well what would if we had a magic method that given that string like right and
then what would it return getting that singular something like that yep and so what we're what we're doing here is we're
trying to figure out okay what is this next level of of object gonna going to look like what is the basically what is
the the best API for us to use here um and now this will guide our our next set of tests uh against whatever this uh
song be I'm sorry I was thinking about something else what were you saying so now we we we we have an idea of what our
API for our our CSV song parser so we can comment this out disable our test uh and and drop down a level to start
testing against a new class which would be oh I see yeah yeah gotcha okay so right and then we're going to create a new
class CSV parser and then might from there build the test have it auto create the test yep okay so that' be in the
domain or application think right I yeah I think it's an application um I could be I could be convinced either way um
but because it's more of a interacting with the outside world aspect I'm going to say it go goes to application so you
said CSV parser nope no controll uh all what is it control oh yep control shift T oh interesting one yep and it will
automatically does it know to put it because yeah so if you go if you go this way it knows what to do as opposed to
creating a class from the test where you always have to force it to go into the to go back yeah Source directory and
let's put the test at the thanks so I I talked about this on my stream the other day um there's no need to drag the
editor tab to that tiny little space on top uh what you can do is when you drag it note note the background changes so
drag it to the bottom but don't let go keep going keep going so note that that the editor window is a much bigger Target
for your mouse and there's therefore it's easier to drag to note that the entire pane is is marked in blue which means
it won't further split the pan if you move up just a tad note that it now indicates if you drop it we're going to split
this pane into two got it um so when you drag it to the top it's much easier to drag it to above the the the splitter so
drag it above the splitter above the splitter keep going up up there you go now it's going to split you don't want that
so keep dragging up now stop right so it's a much bigger Target than trying to hit the tab bar got it so if you're not
using like the tab shifter plugin for the keystroke when you're dragging it dragging stuff around I always recommend
it's much easier to hit a bigger Target um in in ux we call this Fitz law uh it's easier to hit a bigger Target than a
smaller Target was it called tab shifter plugin yeah so the problem with tab shifter plugin is if you don't code much
you'd you have now an additional three or four keystrokes to remember so um uh I'm giving you basically a weight that
you don't have to hit a small Target you can hit a big Target that was cool and it's funny it's one of those things that
once you see it it's clear what intell J is trying to tell you but unless you look for for it you won't notice why is
you may not even notice that it's changing the background to Blue right and if you drag it more to the way see I still
did it the old school y habits take time all right so let's um now that we know what uh what our API is going to be um
let's go and and and write a test and we're basically because we're dropping a level we're still going to be able to
grab uh basically this test but we're going to be eliminating a bunch of the intermediaries right so we're pretty much
going to grab the row and the assertion and a lot of the in a lot of the in between stuff is going to disappear but you
can copy the whole thing and then we can just delete that's kind of what I was thinking yeah yeah um no I'll insert y j
five that's one um let's call it pants let's paste it and then we'll go back and uh figure out what what we're saying
here so basically we can delete second instead of that we're going to say well what was that what was that sketch that
we had from from our service ah we said just magic method so we'll have to come up with but we now know what what it
looks like yeah it's something that that takes a string um and it'll be uh so we'll need so we're going to call this
method on our parser static or uh instantiated uh so that's a really good question um it would be very tempting to say
just parse this for me and give me stuff and create a static method um in General that becomes hard to sort of pass
around as a a dependency that you want to that you want to give right so ultimately you might want to provide some kind
of strategy pattern where it's like hey use this pars or this parser um and so this will be basically an instance method
which which is row which is row we don't need import yeah that line you can delete because we're not talking to song
service anymore right uh and that we're going to want to assign like you had in in the sketch yeah goodby Sketch whoa
really do know what a whist is no did it there we go took a second uh and now we want to assert against that list the
assertion turns out to be exactly the same same yeah uh but you don't need the all songs because it is yeah probably
time to name this before we go and create it I think we can name yes so I have a name in mind I'm curious if if if you
have one um I probably would have done something I mean it's my initial reaction is that's what I was think just that
yeah okay works for me I was like well it's called a parser the class so it's like but yeah so it it turns out um we
might uh end up with some some more specifically named methods but at this level uh that's that's totally a fine name um
so I think uh yeah let's go ahead and create it and then we can name then we can I think finally name our test okay make
sure you finish you uh you're in the middle ofation so finish that on the bottom yep those are all legit right y yeah y
okay yep yeah want to get you to the to the null part so all right so here you know what I would do I would go look at
the other tests we pulled from and they just modify the name but yeah let's go look at that what did that say well add
songs using CSV so this would be parse songs in CSV yeah so i' probably say song since there one I might say from as
opposed to in yeah I didn't like in I thought I was pausing I was like what else good enough that's that's totally fine
okay cool run it and fail so how's it gonna fail oh good question um let's see the parser exists the string exists the
parser is going to return null songs will be no so they assert that right will be fine it'll I guess the assert that
will throw a no poter exception when I tries to dreference it to look at so it turns out um since we're just handing it
songs uh the first thing that Asser a generally does with assertion is check to see that the argument is is not null if
it is null it doesn't throw a null pointer exception it basically fails and says well I was expecting this to not be
null um so that's what what what it'll yeah yep got it whereas if we were in the test here and we did we called you know
dot something right if we said like dot then we get then we get a n poin right because in order to to pass the parameter
in they would immediately throw a null pointer exception yeah got it yeah make cool yeah so suiga mentions you can if if
you don't want to drag and drop you can always rightclick uh and it'll bring that in the menu where you could move to
opposite group um I I find that harder unless you use that a lot and you know exactly where in the menu it is because
that's a pretty darn long menu uh and you have to remember in some cases that uh it's split and move down or split and
move right or move to opposite group so um that's one of those cases where I'm not sure the menu is any faster than
dragging and dropping all right so let's let's make it fail for for a better reason yeah you can always do the action
just say op you know op group and and do it from there oh really there's a bunch of Ops uh Oppo you still got a yeah
then it's why is open showing up I don't know because because yeah yeah yeah that's probably probably some machine
learning gone wrong okay let's um we want let's make it fail for for a different reason uh so list yeah probably could
just say mop and see what happens I could say what mop I wonder if M MOG would work better but now we're now we're
really we're really off track yeah um did you see the result yeah so now so now it fails for for a good reason so now
let's uh yeah suiga MOG isn't any better actually so I try I tried that all right so let's make this um let's make this
this pass uh so we could return a hardcode of value I don't see much of a point in that um so let's um let's actually
try to try to parse it so here's where we now can have a make uh do we want to parse this ourselves or do we want to use
a library well the fact when I started typing this it's pretty clear there's some libraries here or maybe not oh CSV
Escape no maybe not I would certainly like to try a library so there rolling this I mean I wonder is there didn't
somebody say there was one yeah so uh there are a lot of choices um as you might expect there's ones that have been
around forever like Apache Commons has a CSV parser um there are other ones that have different purposes there are ones
that are meant to be super fast uh uh the one that uh let me go back and find it I'm not sure if FNL was was uh um
referring to the open CSV library but that's that's that's an option um is that a bit of Overkill at this early stage or
is it so this is the trade-off right um yeah I mean I feel like if we weren't using the double quoted format then I
might just write it from scratch right you could just do a a string split on a comma uh and you're done but because we
do want double quoted which means we want to be careful about embedded commas it's not so simple uh so way back when
when I wrote um my parser for kid money manager I actually used I didn't use a CSV Library I basically leveraged uh
guava has a splitter class and so I had it split across commas um which worked fine for me because I didn't I wasn't
worried about embedded commas uh but um we are or at least should be and I don't want to write a CSV parser from scratch
yeah me neither so um without doing a ton of research is there one we could just grab for now and then yes so uh there
is a couple choices the uh CSV reader one yeah that one yeah it's funny it's still on on them that's published in
November so it's not like it's a that's sitting yes yeah so so for something I mean it's funny it's like for something
like CSV recency is probably not something I'd be terribly concerned about like if it was in the past three years that
would probably be fine even if it was a little more you know three or four years it would be fine because it's not like
that stuff changes um for other kinds of libraries you want to be careful uh especially if if there's any anything that
could ever be um have a have a c a cve for for security stuff um but for this I I I'd be fine with that so let's uh the
the even quicker start up there under developer documentation so there quick start but then there's even quicker start
uh that's probably kind of what we oh that that might be too quick because we don't want it to read it directly from the
file so here uh can you zoom in the the browser it's a little small for me oh yes of course forgot about um still
reading a file I mean yeah we may have to look at the docs to see uh so scroll up a bit so reading that so we probably
want the uh RFC 4180 parser because that's in general what we want from a well-formed CSV file uh but we don't want it
to read from a file right second that's just their example is using a file right right I'm sure it it can I'm sure it
has the ability to to to read from other things we just need to figure out what that is um so the CSV reader um I mean
we could always uh so let's let's look at the um let's look at the reading into an array of strings there under yeah
yeah so that's what what I was thinking of since it since all the method seem to require a reader interface
implementation we could always uh uh pass that in that that will that will be just fine um yeah let's do that so let's
let's pull in this Library okay what's the best way to do that um the best way to do that maven um just search for
artifact on the page yep there we file that's weird let me double click go and let's um I generally put this stuff uh
yeah so we can put as so I put it above the ones that are marked test few that would be right here uh that yes and sui
mentions the 5.9 is apparently the latest yeah uh so we want to do is change that I hate documentation that doesn't keep
that stuff up to date it's not terribly hard and it makes for a experience um can you uh hover over the orange what is
it complaining about is there a transitive dependency oh because it's based on yeah and so this is always the problem
with a is built on old stuff like Apache collections um is there's uh cves there but I don't think we have to worry
about that so do we ignore it or leave it so fine all right uh so let's go back to our parer and we want to do PSV uh
was it let's go back to difference between the two documentation you wanted to go to U quick start right oh actually you
know what um the CSV parser is what we want because that doesn't deal with reader at all it actually deals with strings
oh yes and it does the hard part of seeing if you're inside of a double quote or not which is really the key thing that
we we care about um and so songs that will give us unfortunately that will give us a string array is what it is uh and
these are basically the um oh on the columns yeah what should we uh I might just say columns because is hey there uh
what are we writing we're working on on an app uh where we can search for songs by themes that assign all right um and
now we do uh so exception uh oh why is it throwing an IO IO huh why would it throw an exception does that um it's
terrible does this have documentation or no well I'm looking at the source code it that's terrible that's terrible
that's very I mean one of the things is it tell it it at least tells me uh how old this library is if they think it's a
good idea to throw an IO IO um do we surround it with TR catch catch oh yeah swegi I didn't I didn't nightbot all right
so and what we want to do is we don't want to throw an exception um uh for now let's just list and uh so what we want to
do is uh inside the tri block after we grab the columns uh we can now go ahead and columns and so what is it columns
zero for our title uh no one oh you're right one then we would have had a failing test if if I got that wrong that's
true uh and let it grow uh and whatever whatever column the theme is in uh that would be four right 0 one two three yeah
that looks right yep we well song requires theme to be a list so you need to do a list right I forget does ARG work at
this no yeah I don't need to select it I just do it return um well we need to return a list of the songs you want to
make a local variable with the list of songs no we can just y the technically 21 right now we don't need reached right
oh it already the compil told me exactly y all right let's run it okay prediction um if we've interpreted the
documentation correctly this will F is there more documentation than that one page hey that worked cool uh usually so
usually I would actually write some more exploratory tests but since we're we're using just I mean it's this is where I
struggle with with libraries like this it's like should we just copy and paste that method into our code because that's
the only thing we're using um so that's something that I that later yeah so tramar said uh something and then said no
was completely wrong yeah so so this sered two purposes of of actually getting stuff implemented but also like if we got
it wrong like if for example it was returning multiple lines and each entry in that array was actually a row uh we would
have found that out um because our test was was specific enough so yeah so it sort of served two purposes it was precise
enough that if we didn't interpret the documentation correctly um that it would have uh been obvious so um let's commit
so you were saying yeah we could do um good enough uh I don't think we implemented it I think we uh we can now we can we
CSV uh so where's the CSV data from this is going to be something that is to be uh basically uploaded by by a user to
bulk the ideas instead of data entry of one by one we wanted the ability uh to take data that we already have in a
spreadsheet uh and bulk import it into the application uh we probably will use text blocks for for anything that's
multi-line in fact we might even use text blocks for the single line to get away from the annoying escaping um right but
that tends to add a new line and that's why it's a little bit harder uh line um so we're at 3 o'clock our time how are
we feeling feeling pretty good I could probably do another half hour just looking okay Commandments I have for the rest
of the day okay um do you want to take a quick break or push on I think I can keep going all right yeah so there was
that one I'm GNA get rid of the Palms where was it was in the service one where was it I thought I saw a single line oh
it's probably the color of this no we're only calling it from within test we had the sketch in our in our song C oh
right right right so it's just a sketch yeah I um if you go to the there we go yeah so now we know what that looks like
um so do we have enough implemented in our uh CVS song parser for us to be able to import songs based on the test that
level at the service level at the service level so at the service test this is the disabled one right so do we have
enough implementation and I think we do I think we can undisable it uh and then call the method we created well I mean
import songs will call the class we created right right right basically use the sketch we had but now call it the thing
that would now yeah exactly so says if if we only ever need to bulk import one song we're done yeah exactly you could
just take the next line uncomment it and then use the the the method that's been magically point tab not enter right it
took me a long time to get used to like which one is which tab will overwrite what you have enter will append what you
have yeah yeah and then we could just uh we got put in the repository right now we gotta put in the repository y so
actually we would we could just call it ad song right because we wanted to do right oh this is songs uh we could do song
we have Mone too much for uh I why did it autocomplete like that that was weird uh that's what I expected is it yeah so
now we uh you can do if you start typing s and hit enter and now song and it'll probably suggest a way to yep and that
should do it cool so now we've pass yeah I think it prediction yeah I think it'll pass I think the ODS are pretty sweet
so uh let's delete that blank line on 37 and commit is it now multis song No but now it's actually at at the okay all
right uh let's now implement the test where we can Implement where we can add bulk import um multiple rows so this says
add songs plural you should probably fix this name to make it singular or do we expand this I thought we did that this
to be well so actually I think uh you want to go down a layer uh I actually want us to uh use this opportunity to start
changing uh to start adding the attributes for song ah because we're not fully using all the data we have there on the
input row uh because we could go down multiple input but but that that feels really straightforward I could predict that
that will just be straightforward what's not straightforward is is adding the attributes and that's what we want to do
anyway P push in that direction yeah um would we redo this we have a new test or use this one and force that's failing
to start I I think this is where uh uh first of all we we are only importing one song so yeah okay um this is where we
change our assertion now we want all those attributes it oh I already got that one you already got that yeah and do we
want end yeah i' I'd probably just take that row uh uh it might even be in your clipboard without the the slashes oh
right would be in control shift V jir right uh oh yeah you could just copy it from there Y and then pretty much paste
Factory where what song uh what are you there um was it song Factory a test you mean this song Factory here got it yeah
yeah because then it'll Force us to yeah yep arst song title start theme one yeah and once we get to figure out how to
add multiple themes that will be sort of the next level yeah Mak sense still returns a song definitely a string for the
artist I think all the names are great because the strings you you pasted in were already good names for what we want to
call these things yeah now release type eventually we might want to think about making that an yeah and do we just force
it so we could structure meaning like this yeah uh but title right this point we call it song Tit so now we got a little
bit of a two terms for the same thing from an oquit so here it's called title right that's because and and when we
change when we incorporate release title that's probably when we want to rename that record component right uh and that
theme one has to be a list of right so should I um for now I'm thinking about changing this immediately to title is that
what you want it to be in the future well we got Title Here for create song I was going to parallelism right but which
direction are we heading are we going backward forwards yeah yeah yeah because the way the the order of oper sort of the
next steps I see is um propagate song title to the song record right and then propagate that to the other Factory
methods and then we can start adding the other components my now funny enough I think uh I think this will pass well are
we even using this well we are it oh yeah it'll pass because we're only checking two of the attributes right well we're
only creating a song with two because uh and it the assertion is kind of misleading right it looks like you're using all
the things we're not all right um so let's uh let's do that rename on okay there must be there must be some history as
to why shift F6 is rename and F6 is move because you do renames way more often than moves right but and rename and move
to me aren't siblings yeah yeah so oh well all right um let's run all the test just be sure okay did you run the test
yeah I was just one second I was trying to find something alt shift place so you're saying when all test io3 uh I
actually didn't but actually I'm glad you did because we haven't run those in a while yeah well we ran them when we
started the stream yeah which is while shift F10 cool no they definitely did renaming first because I remember it used
to be a plugin called renamer before intellig was a thing it was a plugin um all right so let's uh let's so let's go
back to our song Factory and there so what order do you want these in basically the order you have them yeah I don't see
any reason not to other than yeah I think it's important to have theme at the end yeah we might as well stick with this
order all right then let's do it so are you seeing something like as long as I had cap loocks not on I think caps lock
should never be the default uh yeah artist song title release title release type um oh did I override song I guess I did
yeah you again so why oh I need a space is what I need is new Constructor or change the existing one that's an excellent
question it depends on how much what did the change so the only the only place that we actually call new because it's
only going to change the Constructor I believe is maybe one place in our production stuff uh and literally uh this
Factory can you scroll up a bit we have another static Factory method there right yeah so let's translate um 16 to be in
terms of uh the one on 19 so basically delegate instead of a new let's delegate it oh there's not going to be any I
don't think there's an automated refactoring for that yeah I was wondering if it was well we could by doing an extract
it's not worth it so just say create song no no just say create song Oh great because they're same this would then be oh
this one already this one has the multiple things I'm sorry then let's let's not do that now so we'll we'll later um so
I think let's let's change the let's do a commit can I fix this name first theme one at this point it's not a theme one
well oh wait a second it is it's a it is a theme it is a it is the first of of I'd leave it I think yeah yeah you're
right um let's we're not compiling that's fine but I want to do a commit before we do a refactor I see because in case
we have to back up we don't want to have to un try to undo it yeah so this is a a I usually say something like a a
factor I like the literation of Factor uh I'm not sure about Mike but I'm I'm pretty much a Java head doing jav been
doing Java for 27 years I was big in C++ for a couple decades and then C and then uh started dabbling in Java which you
could probably tell that I'm not a javae head but I think it's super cool and I'm enjoying it all right let's do that
risky refactor so this is a part I wasn't sure what you mean by that what are you thinking I'm thinking change the
existing Constructor red no that's what we want and that's what you want one two three what is the difference between
the first and the second string string actually that might not be the one we want that's the one we want what the
difference H the difference is the second one puts artist first the first one ah puts the right so you need to need to
navigate through it to see like the type is not sufficient which is the whole problem with using types yes primitive
Obsession yes got it yeah okay yeah wider so got artist uh oh it mucked Up songle mued Up song title interesting default
value is song title uh can you move the dialog can you move the dialogue up because I want to so uh yeah so let's change
that to song title then release title is fine uh the second song title should be released tip boy I don't know why it
did that really mang set up uh and then we got themes yeah okay so it was close but no cigar yeah or okay I kind of
think it's I'm not sure so let's continue because and this is why we did that checkpoint because this is a bit of an odd
uh change so I expected um I expected callers to call the Constructor to to be now not compilable like 16 so that I
expected uh let's go look at what it did to record to the song record artist song title release title release type that
looks fine yeah uh and so is the only I expect to be one other compiler error so let's let's try to run the free tests
mainly because I wanted to compile I always do run tests as a way to do compile right so I expect at least a couple of
compile unsurprising okay all three are in song Searcher yeah oh they're on the same line yeah it's basically because
there's three errors on that one line right right so that's it uh we probably could have done this with the change
signature um but let's just let's just fix these by putting uh just empty quotes there yeah or you could put in sort of
default that so if you select the the word and then type a double quote it will quotes nice which is which is Handy
although sometimes it's annoying but in handy uh so F off I ask how to fix primitive Obsession in this case uh I yeah so
let's see now this one's interesting song with theme basically I think we might have even been calling this where are we
calling this from I think we're calling it from the startup so we added this prefix of song it's like whenever you even
checking this oh this is uh right this was when we were first doing doing some tests uh and so B thing so that was that
so this is basically for for tests right because that's the only place that's called is in that test right yes let me
double check again yeah yeah that one test because it's weird to the song with theme plus right and I wonder if if maybe
we wna we'll want to move that into the either use the song Factory or maybe move it to the song but this it's fine for
now our main goal right now is get stuff to compile so let's fix the other compile errors same thing right uh no here I
would I would put empty strings because otherwise we're in danger of matching what's in the tech what's in the test in
in an we'd probably have end up fixing it but it it it would be false falsifying it you know what's interesting that's
happening there is did I do the paste I did not oh I did wow just automatic so now we should oh know there's still some
there's still now yeah this is the problem with compiler eras you compile you fix them and you try and compile again you
find uh oh so here um since these are used by tests where we don't care about those other things uh let's just turn
those into Strings that just say irrelevant you know relevant artist that wrong so we do want the actual title that's
passed in though all right now at this point well it's not the right time to re factor that name oh you could have yep
so now here this is the song Searcher so this is basically just test data uh that gets put in when we start up the
system uh so here I think we can just do the same thing surround it with with double quotes So for those of you uh in
chat I posted a link to uh my talk on primitive Obsession and how you fix it so it's a good good video to watch uh one
of my favorite topics but we'll be doing that in in in song in the song themes app because uh certainly for some things
we're going to want to have some Behavior around them uh and if nothing else stop having string string string string
string yeah all right do it compile yet but I haven't tried it let's find out not seeing blood in the gutter is one of
my colleagues used to say about compile erors now we broke the whole world uh did we uh we might have swapped some some
places in our song Factory and put things in the wrong order that could be check uh let's let's find the one Let's find
let's track it from one ah okay so this is what intellig was warning us about so on line uh 72 there um and again this
is this is the problem with with uh uh with untyped or string you know basically untyped stuff um so let's let's fix
that because it's thing so you're saying is that um this should be song title yeah and it converted it it it converted
it because of the order of the parameters uh so we probably we probably took a a step too big got it um we should have
put it put the new stuff all the way at the end get everything to work and then put stuff in the right order right why
is this one not so we can probably just do a global search and replace for song colon colon release type but why is this
one failing this one's let go let's go to it I'm sure it's the same reason I was like right a but where is the Coen Coen
that's what seeing Uh Oh Our Song Searcher is wrong right song titles by theme we're not that yeah ah here that's why I
want you to do a global yeah Global search and replace for that which I forget the shortcut for that is that's under
finded and then uh finding files replacing files control shift F okay uh control shift R because title just let her rip
let's do it be brave and let's run our tests see which ones are still broken not two so this one I expected to fail
because we're not uh oh right we have we're not going to parse it so that's one uh and that one is basically dependent
on uh that one's dependent on the the broken CSV parsing this one yeah so this is what I this is what I expected after
all the the the the fix UPS we are not parsing all the columns right because we just adding those columns yeah so we're
back to finally adding the feature that we're were adding right and this is probably a good place to stop to leave us a
breadcrumb for next time no good point but we can commit and we're certainly a good way towards getting all the
attributes so song now has all the all the attributes that we want uh and we just parsing all right time flew by two and
a half hours yes yes and it's interesting like it it took us a while to figure out like what what do we want to do what
were the next steps and and so on and and that's that's a fact of life typing is not the bottleneck yep for sure did we
get all the questions that came in yeah I think so oh awesome um oh suiga mentions in addition to the to the double
quote there's other stuff that will sort of Auto surround um to be quite honest I've turned most of that off because it
seemed to to want to do that at the most inopportune times so I end up turning that off but it's there you know what
it's called in the um options menu uh it might be called Auto surround or surround it's it's under smart keys on yeah ah
I'm not going to undo it I just was wondering which one it was yeah and also for anybody watching yeah so there's a
bunch of things under here under the smart keys where it'll Auto uh insert the pair it'll Auto insert a pair quote um
it'll do a bunch of things for you uh I I've turned some of those off because I actually end up being smarter than than
intell but they're good they're they're usually doing the right thing yeah and then there's a there is a separate
surround uh a whole separate set of surround functionality that you can do um that's up here right yes yeah so it's uh
surround with which I guess is control LT for you so if you code hey and uh just click any just click where T and this
is where you can surround it with the if if else try catch stuff like that and I have I have some custom ones that I've
that I've created as well that you know for when I'm constantly when I'm constantly surrounding stuff with list of uh
you can do that with with the with the custom surround with yeah it's a live template yeah live templates yeah yeah so
live templates they're they're basically two kinds there's the I type A and it expands like a macro kind of thing and
then there's other ones where it's takes whatever's selected as as input into the live template and so it's um sorry
were you INR me to do something I was just browsing yeah so if you if you look at uh the um if you look at those
templates with right like this one yeah and so what it does is it takes if you look at the the template you can see the
dollar selection dollar um and that's what where what it it grabs from what's currently selected and then sticks it in
into the template cool and then if you want to make your own you just add another the plus sign sweet all right I think
that's all it's good for me yeah I think we're gonna be a little bit sparse next week yeah maybe one day maybe not yeah
so we'll play it by ear as always if you want to know when uh when I'm going to go live Solo or we're going to pair with
with Mike or someone else um Discord is the best way to stay informed uh so just go to ted. Discord if you're not
already on the Discord uh if you are um make sure and you want to know when when I go live to stream make sure you go
into the there's a special Channel and it is called rols and I'm going to show you what that looks like this okay so uh
if you're in this Channel and you want to be notified uh when I uh because I try not to Ping everyone um so if I do if I
send a message to at everyone it pings everybody uh and I try not to do that um sometimes I'll do it if I think it's
important to the whole Community um but I don't like to Ping everyone when I'm going live so if you want to be pinged
when I go live just click the little alert button under coding stream alerts um if you want to know when I do other
stuff you can click on those but pretty much the coding stream alert is what's going to happen more often than the other
stuff so once you're in the Discord go to rolls and then pick what pick which one you want uh and you'll be notified
assuming you have your notifications set up in the right way which I will leave to your discretion to part all right uh
and so as Mike said uh the pairing will probably be a bit sparse um but I'll be doing some solo streams next week uh so
and as always uh join us on the Discord for also discussion about stuff um other than that uh I think that's it all
right see you next time see you next time
