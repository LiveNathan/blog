# ＂Song Themes＂ Episode 12： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=e6cmP1zNqJk

---

## Transcript

oh all right hello folks welcome to episode 12 of working on Mike song themes app how you doing Mike good good good
morning morning and good afternoon for everybody or evening for or evening wherever you are it's funny whenever I do the
math because I always post like when it's PST and and when it's UTC for some reason I always end up with uh adding 900
am and then 9 even though it's eight hours ahead and then I end up with with with 6m instead of 5m and I don't know why
and I do that a lot and I don't know why I do that but n n plus n is is 18 but that's not the right time well software
Engineers like fence post errors well it's weird because it it only happens uh with like a 9:00 a.m. start when it's any
other time like if it's a 1 p.m start I don't have that problem but I always somehow add nine to nine I always add eight
to any other value so one of the one of those strange border cases yeah yeah the brain is a funny thing um so last time
uh we started working on bulk import of multiple songs right um should I share your screen sure sure I can see where we'
re at let's add to Stage turns out tsv is a thing I know you were calling it by that acronym and I was looking at some
other tool I don't know what it was and it was like do you want to imput you know C oh no was an export that's what it
was it was an export of a uh radio play with software that uh the radio station I work volunteer at um as I wanted to
get a list of everything I played in the last year and it was like do you want tsv do you want CSV do you want Excel do
you want I'm like oh okay cool it really is a thing it really is a thing not that I didn't believe you but it was just
new to me yeah yeah so that's some one of the things I actually do with the radio thing is I make list of favorite songs
of 2023 but also things that are new to be in 2023 could be decades old right it could be um I like making multiple
lists something something about radio people that like making lists some people y sorry some people are just list makers
yeah yeah it's true yeah so let's see where do we leave off adding songs load well let's do the usual of let's yeah okay
we got a breaking uh test yeah and that's failing for the right reason what is the right reason let's see yeah we're
just getting one song right yeah in fact um we could we could so one of the things that that I tend to do uh is start
with the least restrictive assertion that will fail because sometimes it's easier to understand like this one it takes a
little bit of time to like look at the error message and it's like what's the problem oh it's only one of them is is of
the two that we want is in there whereas if we just said assert that songs has size of one or sorry two in this case it
would have been a lot more obvious that that it failed in that way right um but you so what what we can do is um and
something I just I just thought of and I'm not sure why I don't do that we could actually do multiple assertions so we
could before the contains exactly because you can chain the assertion so you don't have to write a separate assert that
oh really yeah so just yes so it will blow up on the on the first thing that fails because it's it's uh it executes it
in that order so you can say has size two sweet um and uh what you can do is if if it's unclear well why are we
expecting two um we can put a description before the has size um if you do a DOT as above that and then you can say uh
expecting two songs what about this and so now if you it will basically show the the text error message in addition to
the one oh and it still does the does it will still yes it will still show the the the actual so you don't have to
manually dis display that yeah ah got it it shows the actual but it doesn't actually fire this assert because it blew
before that right because it blew up before yeah got it and I guess one other thing to make it a little bit more
self-explanatory is we could do um right but it doesn't help with the blowup no the description is helpful certainly
yeah yeah the as description yeah nice so that that's um and so then once we get it to two songs if it's in the wrong
order for some reason then at least we know there are two and it's just in the wrong order right so does this or the
wrong content right does this as display only for the next so so the way it works is it's it is the description that
will happen when we blow up and so if we want a different description when it blows up on the contains exactly we can
put in another as and say song songs You Know song expected something like that yeah so the as will then supersede once
it gets past the first assertion right so if you want to see that change the has size to one so to get it past that
point and then we can see that it should display unexpected song content yep that's cool well it's now officially a good
day quick all right so we've got a failing test that's failing for the right reason um let's see if we can make a pass
yeah so let's see what did we so code so how are we doing it right now list oh we're only doing it for one song right
sorry I'm just taking some notes sure yeah yeah so we're basically ignoring um we're yeah we're basically ignoring
anything after the the first 10 columns we're ignoring everything after the first eight columns or nine columns or
whatever right is it in considering this all one big row pretty much at this point yeah because we're only parsing on
tabs we're only splitting sorry we're only uh splitting on tabs we're not splitting on new lines um H we probably would
just want to lines as as well and then uh and then Loop through right so split on new lines first so we we might yeah so
we we probably want to do a prepare refactoring because right now the code from from 11 through 18 is to parse a single
song right uh so I think we can we can just do that without without having to disable the test I think we're we're
professional enough we can we can refactor with one failing test yeah so that's uh oh I used the wrong Control Alt uh
parse song yeah I was B to say parse one song or a song I think I think song is sufficient yeah no I think so too that's
but that's why I paused my brain was options oh so we can we can run yeah we can run the test it should still fail in
the same way yeah yep yeah awesome cool um and so now uh we can do another split uh well we can do um I forget does does
string have I know file has dot lines oh actually before we do that we still have some refactoring to do so this is now
a song go yeah no Collision there okay and then sorry you're gonna I was gonna say um so string has a specific method to
do exactly what we want which is do lines uh so we can do tsv songs. lines and that will give us a stream line do a VAR
um no we're gonna we're gonna we're um uh I kind of want to do this as a as a prepare I'm not sure if it's worth it uh I
was going to say let's let's do first or find first oh returns optional that's going to be painful all right let's not
do that I was going to say let's do a fine first and it it basically still only parses the first one more more compare
like but I think we can jump right to it uh so what we want to do is is pretty much a map so we want to use the the par
song method to to to do to do a map so we do a map yeah and uh what we're going to do is um inside the yeah yeah that's
good inside that uh let's create a Lambda of just s s arrow and then um that'll be our string and so we can say uh
parong method y and uh we can let it turn it into a method handle I just for forgot is it going to be this colon colon
par song is that what it's gonna do so let say Control Alt T is that right no uh no just hit Alt Enter oh I'll enter
right right right yeah yeah okay so it is that was right yeah it was right I think you didn't hit enter no now you got
to be on the orange part in the par song ah this par okay yeah that makes sense um and then after the map uh we can just
do list uh and then return that and get rid method you can just say return oh return ah okay does do return yeah find
out yeah sweet all howy um you say hi to Tes yes I I I did you did okay very rude IES you know that's my realid name
Rude Boy no kidding so uh I think this will pass if not we'll get more information pass oh wrong so that's a tough one
do visually um oh wait are these actually the let's see so uh oh it's missing Joy it's missing Joy one two three four is
that right is the input right so let's see we turn on let's see how do we turn on um being able to see tab characters
that's settings right uh I usually just go to go to is I think you can say something like something yeah active editor
show Whit space is the first one ah now actually this is interesting do I hit enter or can I do like an arrow to make it
I don't know I usually just click this one with the mouse oh really I'm gonna hit happens I don't I don't do ah just
hitting enter did it okay good to know so I didn't even have to hit the mouse sweet okay so now we can see it so it's
still gonna be so we get one two three four five six seven eight nine oh you can't really see these small wrong I'm
gonna do something give me a second um that might be a little bit V visually easier to deal with than that well I was
gonna say instead of us inspecting it let's write another test yeah so let's grab line 50 and put it it uh and put it in
on basically a copy of line so we can grab um the one with four so we yeah so that one has four themes I would say
duplicate that first one does control D only work for a line doesn't work for Whole M that works for whatever selected
so so if I do yeah so select the whole test oh I have to literally select the whole test right so it's either the
current line if nothing is selected it will do the current line if you have anything selected it will duplicate whatever
is selected sweet so if I do this and then hit control D yeah it duplicated the whole thing sweet then we should
probably move this working one part another song I mean this is a temporary test this is temp well it might not be
temporary it might expose some some issue right I guess let's just name it crudely like that for now whoa overload you
must have hit the wrong key yeah okay so we want to grab the Joey okay I wonder if it's I wonder if it's a multi-line
issue I wonder if it's uh a whit space issue of some sort no it's actually just not picking up the theme right oh you
renamed the variable so got to fix 51 yeah yeah but I wasn't sure how far we're going to go what you were thinking of
doing so your thought was to okay put in I was just being mechanical driver at that point I wasn't thinking so that's I
I was actually just thinking out loud um let's just run this test we expect it to fail but I'm curious how what the
actual parsing is just this test yeah okay the rare time we run a s Le test I know on this date at 9:21 pafic time so
let's see what the what the actual was um so the actual artist song title release title at least type empty um huh but
but when we ran all of them so let's run run all the tests so fail oh I ran latest not yes oh my bad hey Sia we're we're
building uh an application called the song themes app and uh right now what we're doing is we're working on the parsing
uh since we import bulk import songs in a tab delimited format we're basically uh test actual oh wait I think can we
look at the test sure multiple song test can you scroll down is our actual correct I mean are wrong oh dang I see what
we did you probably did a we probably did a copy paste paste that's or duplicate um I'm like because like that that the
actual is actually right okay let's rerun yeah dang who still failed just well let's look at the the uh scroll down a
bit to the other part uh there's a parsing problem with the song title yeah a wonderful uh once again our our expected
Is Wrong the song is What a Wonderful World but your expectation is wrong yep that was definitely a copy paste error
yeah because I noticed this was farther to the right yeah yeah yeah that's what I noticed as well yeah this is this is
where um I think that sorry keep going I was gonna say something about how about you go uh I was just gonna say like it
would be nice if a search a could be a little bit more actually wait no can you can you do the click to see difference
there's that button there the link there at the bottom oh yeah I forgot about that yeah so that that's that would have
made our life easier yeah all right I forgot that was there I was actually like oh I wish it was there and there so
youna say something yeah I was gonna say that's the disadvantage of trying to deal with this to me ugly tab delimited
string I I know that's what our input is but it does make well so we can turn it from the invisible tab characters and
use the the Escape T that we've been using elsewhere um and that might make it in one sense it makes it a little bit
harder to read but it makes it much more clear where the tabs are yeah it's true but all right let's let's run it and
then we can delete that that temporary test because we now expect it to pass yeah yeah Okay cool so we can delete that
test yep yep awesome since we had that learning about it difficult to read and uh seems like a good time to do to do a
replace yeah you can just do a total total search and replace in the file yeah nope wrong shortcut I thought it was in
Sublime what is search and replace in control R control R yeah okay so we want to replace H does the tab if I hand type
in the tab character will that go in no it's gonna move yeah it's gon I need to select one interesting I'm double can't
double click on whites space yeah that makes sense because it's right yeah replace all yeah you're braver than me I was
like sh IA true yep still pass all right let's commit hey so we got that Test passing but are we really done with
multiple songs um well let's go back out a a level and see what our uh Service Test looks like um I don't think we had I
think we we so we decided that there was kind of no point in writing a multiple right uh line one at this level because
it was pretty much passing it directly down so um I mean I think we're we're done if you wanted to change this test and
change line 53 to be multiple rows i' um just does it get us anything oh to make sure um just just that it's now
actually uh importing multiple songs at at this level I mean it doesn't it doesn't get into anything in terms of driving
any code uh but it does um sort of match the typical what typically we'd want this uh the import songs to do is there
any is there an automated way to make this a multi-line or you just got to manually do it I don't know you'd have to hit
Alt Enter and find out ah good idea put into declaration and assignment N I don't think doesn't look like it okay so oh
interesting um I wonder if it if you if you do that no I was gonna say if you do what you just did okay and then uh what
is it suggesting is it just suggesting removing the the two double quotes if you go up to the no no what on the on the
orang Oh you mean this one yeah that orange okay yes okay it's just gonna say remove does it offer anything else no okay
all right so yeah just just manually do it so it's three yeah ah now it's thinking well it it basically autocom
completed the closing triple just gonna be oh man commer 256 you're I I I feel you as as my son would of I I I I totally
get that um I I I wish I I I wish I had a good answer other than uh than some cliche of of hanging there or something
like that because I'm telling you I mean there this is you know this is why I'm I'm I'm independent and probably
unemployable because I can't I can't corporations I know that's maybe not what you're looking for but at least you're
not you're not no you're not alone so yeah uh let's and let's um let's update our our assertion yeah I'm going to copy
we got to make sure I don't make a mess of it I just added the number two yes to everything everything yeah even the
theme uh even the theme is now theme 12 okay yeah I didn't want to I wanted to keep it simple few weeks ago I learned
that the customer mine is still using visual age still using small talk that's impressive I worked for a company around
that time frame that was doing production Small Talk working at Telco Le Pascal yeah well T Telco is one of those I I
did some work for Telco way back when it's out oh it didn't index one out ADV um that is surprising um but good yep
that's what we're looking for is what went wrong so probably what let's let's see so uh let's go take a look at at
import service run on window server talking to db2 I've done some db2 stuff not on main frame so my latest client still
had DB has db2 as main frame yeah when I worked for the insurance software company db2 was one of the ones we supported
um though to be honest I don't think we ever actually maybe we had one customer uh but IBM was paying us to to to
maintain that um I don't know and I think we at some point stopped stopped doing it because a lot of our customers they
were pretty much either Oracle or Microsoft SQL Server so what's going on here we create the parser we parse songs and
then for song and so we're getting the out of bounds though in the parser itself so yeah so let's take a look at that oh
we have a ah so this is uh an edge case because what is that 10 there for um that line 17 that is uh how many columns we
want to parse right and you just mentioned that look at how many cols we have here one well no I was going to say
perhaps we should we should make that code more self-evidence yes that too uh so let's let's let's change that 10 and
let's make it a constant unless you have a better idea but um constant is the first thing I so I'll command alt uh C oh
right right right C for parse it's a good start are we still are we doing screaming caps yes even though some folks have
argued you don't need that anymore because the ide's color things like it's idiomatic it's been around for as long as
Java's been around I'm not changing it yeah certain things I will I will push against and change uh but but there are
other things things I I will not I mean the that one it it actually is screaming important um so yeah screaming cast's
one of my favorites yeah yeah all the names for these things like snake case and Kebab case and things like that are
amazing yeah there's a lot of old Tech that was that was good these days we we it's optimize for for cost um so yeah so
let's let's write a failing test because because um I'm guessing what the problem is and we should write a test to to
prove that I'm guessing it's because it's actually trying to parse that third row that's my guess third row this yeah
which is basically empty and when you say write a failing test even though we have a failing test do you mean a failing
test closer yeah a failing test that's that's closer yeah got it so we'll go back to tab separated close this puppy
what's interesting though is if we had here parsing multiple songs we had the same thing why is that one um oh we're
testing something different though no but it's it was failing during passing and the other one is go back to the song
service test I think it's number of columns of data one maybe you're right three four five nine right but we're only
processing nine so that shouldn't be a problem because it's Max yeah basically it's it's what what that does is it says
after the after that many columns treat the last column is the rest of the line and so we basically are saying that um
so it's but it's failing on on column one see index one for out of bounds for length one so there's one column that was
able to parse from whatever line it's processing that line number is out of date because we uh we inserted some code so
if you want to rerun the tests yeah I'm pretty sure it was Yeah so here's here's an um we could uh uh we could write
some more tests or we could do like a a system out print or we could follow in to the debugger to figure out exactly
what's going on um I tend to avoid debuggers and and and print statements uh but it might be the most efficient at this
point just to see think of how to write how I'm okay with that I just was trying to give it a few more yeah because I
don't cuse cuse um what we can do is we could do the same thing we could basically copy 53 to 56 on the top uh and feed
that directly into um our our closer see so I know there's some comments in in the chat but um but we're we're deep
inside debugging this so we'll get to those comments so don't worry I think there's only one multi yeah so it'll be this
test right and I'm now and rerun right yeah no the asserts the well the asserts will fail it'll certainly get past the
has size of two um and the rest of it will obviously fail but the question will be will this actually complete the
parsing or will we see the same array index out of out of bounds point yeah okay so it's so there's something about this
data setup that is is causing a problem which is great and this is why um I know somebody asked about why not use the
buggers is because I always want tests that recreate the problem because then we have a test hope and then assuming we
fixed the problem we now have a test that is exercising that specific problem and so there's something different about
this data that is causing the problem that um uh that are sort of more realistic data is not having a problem with so
let's um let's duplicate let's put this in a test of its own because this is clearly a different at the tit level at the
titel right yeah yeah yeah I guess I could have duplic did the whole test yeah that's what I thought you were fine and
then restore this back yeah healthiness and I think we only care about how size of two I don't think we care about
content just yet because right now we won't get that far anyway yeah whoops that seem about right uh yes okay okay great
we got got a failing test uh so just want to catch up in in in chat a little bit sure so lonox ask are you learning
spring for the first time spring I would say I'm I had some previous experience but definitely on the thin side yeah I
mean Mike doesn't code every day like I do so uh so that's you know that's why it looks like I that's why it looks like
I'm navigating a bit more only because I do this every single yeah uh so com 256 um yeah so um what I would say is is
that yeah I mean as things get more complex as we build more and more layers as we build larger and larger systems I
think in a lot of cases some of those layers are are completely unnecessary I feel like um in some cases slightly the
RSE but like having developers have to understand kubernetes in detail uh seems like a ridiculous waste of of time um
but I totally get like it's if if you're interested in sort of the uh the microprocessor I mean I grew up coding 6502
assembly um and 80 286 assembly which was not fun um I totally get that like as as abstractions have have built up you
sort of lose touch with what's what's going on underneath and um business applications and things like that are no long
they're never going to go back uh but there are embedded systems and so um you know so if you if you dislike
abstractions there's certainly uh places in the industry not as much um but there are places where you will still
program and code against microprocessors right there is all the stuff that's in that first layer uh and so I would I
would say you know have you looked at that have you looked at um embedded systems um or uh just device drivers yeah
device drivers all the stuff that that is that that lowest level of abstraction there's still people out to code that
that's not that's still not done by Magic the micro code I mean I don't know who's there probably aren't that many
people in the world that do that but somebody somebody does yeah but I mean there's there's lots of stuff um like iot
right iot is huge right internet of things you know putting putting all the smarts at the edge of the systems that that
stuff is you know a lot of it is still done in you know some of it's done probably in higher level languages but um
you're you're you're coding in the small because you're coding you know even if it higher level language you're still
coding at the device as opposed to um on some virtual machine uh container in a virtual machine on a on a rack in some
big data center yeah you can still see the metal air quot see the metal yeah so hopefully that helps a little bit uh
let's say I have a shop domain domain H the domain has address which can either be online or physical uh use interface
address as physical yeah um I mean I would I would yeah I would say that that um probably just don't want to want to use
inheritance so there you could um but if they're if they're not substitutable because what does it mean to ship um then
then you'd have to to do something else I think we probably need to to to to dive into more details and so if you're not
already a member of of my Discord um that's a great question to ask in in the Discord uh because um that's the kind of
thing where where we can look at code uh and provide some feedback on on on concrete code because it's easy to talk in
the abstract and still kind of not thing uh so so cattle says the whole devops thing is Shifting responsibilities
infrastructure yeah and I think that is not what was intended by the devops movement the idea was that there still are
Ops people CIS admins sres or whatever you want to call them who provide higher level abstractions so that developers
can run their apps in sort of the the 90% case like operate their apps in the 90% case deploy them on their own without
having to get system admins in involved right it used to be and and it's still true in lots of places like hey sis admin
can you install this new software um and they go run a script or something um and so larger firms should be providing
platforms that raise the level of abstraction not lower it uh and I think it's it's it's simply that PE that developers
like fashion developers like shiny new things and developers like complexity um and management is incapable of reigning
those folks in the fact is is that that hurts the business but as G says uh software is so wildly profitable on a per
developer basis that we can write cra code and crappy systems and still make trillions of dollars and until that changes
um there's no incentive to to improve this stuff I think wasn't part of the devops thing also related to um having less
of a a separation of throwing things over the wall as far as sort of ownership in the in in the positive use of the term
right not in the pejorative use of the term right right yeah I was supposed to you know we were supposed to to because
the old days the CIS admins would fight any change and would make it really hard and you'd have to have all sorts of
quality Gates before you could be allowed to to install the software on on the live system um because CIS admins don't
want change because that means risk and things failing uh and devs want to get their stuff out and so it's that you know
they're they're at odds and so the whole devops idea is let's actually work together to to to fulfill both sides um
Netflix's you know the idea of you build it you run it did not mean that developers should also become sis admins that
was not the intent at all um but if you're a developer who's writing applications and you were dealing with figuring out
how to configure stuff for somewhere it's broken and that's that's all I'll say about that it's just broken broken so
lots of conversation chat I don't think uh we can keep up so um wow look at all that yeah was like oh wow there are lots
of messages so uh as I mentioned join the Discord like you know these kinds of discussions right um lots lots of folks
to to hang out out with uh and and talk about these things um and yeah I mean unless you're unless you want to go back
in time to when things were simpler which unfortunately is not really possible um there's always going to be stuff like
even you know even the the the 8086 processor nobody very few people knew what was going on underneath that and and and
these days you just can't know the processors themselves are are too utterly complex um to to to truly understand like
uh it used to be you could sort of predict how many cycles this thing would this code would take and now that's just
impossible and you just have to say that's that's the way it so thanks weet law all right so um we found that this
failed right uh yes so I was failing here yeah um so what do we want to do at this point do we want to say okay we need
to hop into the debugger or is uh there something else do it's failing on column oh wait escaped that I don't know was
the original test that way let's go back over here yeah okay so that's the problem there actually are no tabs in our in
our input how did that happen uh I don't know at some point added but that's good because this is this is a test case um
where what if the rows don't have enough data and that's exactly what's going on here in a sense there is only one
column and that's why it's failing on on the second one it's failing on trying to get the second column so so if you so
if you uh replace that thing and then if you hit if if you hit the left arrow and then hit delete ah okay and then
escape to get out of multi karat pass yes we l we absolutely are parsing tsv data using back SLT why what else would we
do I'm I'm not being factious like what else why would I what else should we do anything it works great why why use
anything more complicated um so now the the other test is failing because it has the same problem yeah that's not how
you parse that's it is there is there another way to parse tsv that I'm unaware of it's tab now if you're going to say
that well there could be tabs in the actual data I'm going to say that no we have the requirement that there's not um no
we we decided that it was better to use one line of code to do a split than to bring in an entire Library so I'm GNA
100% disagree with you here we we're custom we're we're customizing this exactly fit for use and we're test driving it
so it exactly covers what we we need so I'm going to totally disagree with that and you can watch past episodes we're
not going to relitigate that argument all right um so our test should now be passing because we actually have columns in
our data they were they all passed yeah all right uh let's oh sorry what were we gonna say I was thinking this needs a
better name uh well now we know what the problem is um and these are the the the sad cases that we we need to cover
which is basically what if there aren't enough columns what do we do so we should probably um modify this test to uh oh
sorry no dark mode uh when I'm pairing sorry about that I should turn that that request off that and why are you not
working there we go I swear the twitch the twitch UI is is the stream manager UI is just seems to getting worse and they
fired a whole bunch of people so I don't anticipate it getting better anytime soon oh ouch um so the magic index I mean
at some point you got to translate column numerically oriented columns to uh the actual content and we know what that
format is it's it's a format that that we've defined and that we are literally test testing um so you're G to have um
you're G to have magic numbers or what seem seems like magic numbers I mean is that uh who was it that said it uh uh
liox oh um yeah I guess I don't know if we we did talk about it earlier that the there's at some point we're looking at
here's what the spreadsheet looks like at the moment right um go away drop box um and the idea was at some point to
start checking on column names right to not be so magic numbery but it's a different magic number it's a literal string
um but it isn't as as obtuse as 012345 um but we're starting with the simpler case for now and we'll slowly grow it as
we need it yeah and you know admittedly we could have just jumped directly to let's let's use the Excel spreadsheet
import libraries um and and do it that way so uh so let's write some some failing tests so let's turn that test into
basically um and sorry not failing tests but sort of uh unhappy case tests because we've we've done all the happy cases
I think we were we were basically done with our happy cases and now we have some unhappy cases and do we want to um
modify this one which was used temporarily and just re yeah so let's so let's modify that one to be our our first uh
unhappy case of of not enough not enough columns and what actually let's figure out the assert is then will name the
test unless you have a name at the top of your head um handles rows with not enough columns for whatever we mean by
handle out okay and you want to just drop one drop um I would say let's let's drop them all and just have one column
that is a simpler looking test that's for sure and I don't even think it needs to be multi-line I think it's basically
just a row with with one column with the tab or without simple um well we know we're not going to expect that uh and we
can see how it fails we have to think about like what what right we're now back at in in tdd what do we want it to do in
and and what basically how is how is it going to handle this we can run it just to see um 22 yeah so that's that's kind
of what we expected uh yeah liox we we may get there um but because we're working with with a fairly fixed thing uh you
know this bespoke app we we get to to make things simpler by not having to read the headers and then match things up but
we could certainly do that and like right now it's I'm going to be the only customer imported data right um but when it
gets to the point which is you have to look look at the earlier recordings but when we get to the point where we start
opening it up to let other people contribute then at that point we'll probably have to think about making a little bit
more robust or not and then we just see what kind of failure modes we're getting from people that are submitting and
then go okay we'll solve that one we won't Sol so so it's pretty much a yagy we're not writing more code than we than we
absolutely need for a minimum lovable app yeah um so what do we what do we well we want to let the ultimately let formed
so this is always the interesting case of of any kind of processing any kind of input from the outside world when um
when the outside world could give you bad data uh there's sort of the the two typical options which is the throw an
exception or change the result type where you could return um either a successful par result or a failure message and
that's the result mechanism that net uses a lot uh or the either more functional kind of kind of thing or the way go
does it which is always return an error code that you always have to check which I think I understand why they did that
I don't like that either um but in this case uh unexpected that we would get bad data um I would I would say we go with
with the result uh mechanism which is which is sort of optional like in the sense that it returns either either here's
the parse song or information about why we couldn't parse it so um that's interesting I would have thought exception but
rather than talking about whether to do exception or not I have a question more about how would that be Implement you're
proposing be implemented will we do it as an object that includes a list of songs and a result text of some sort so sort
of like rolling our own optional basically yeah yeah although this is It's we're we're at the parse individual Song
level so we only so we we uh in in a sense we're going to create um an either or a maybe or a pair uh which will either
have if it's successful it will have the song and we can get it out of the song out of that object like we do un
optional um or if it's failed then we can get the failure information which would be some kind of text message saying uh
we're in enough columns here's what we found oh I see what you're saying so you're saying it's not at this level it's
going to be at this level right not paring song the par which will affect the cerates as well so it will no longer be
list of song either um because we need to to gather yeah interesting I've not done that technique so I'm game to give it
a roll yeah and and I think it's a really good alternative to to exceptions because here um you you would end up with
with a similar result because if you threw an exception we actually are throwing an exception right we're not throwing
it the the uh the runtime is throwing it we could catch that um and the question is then where would we catch it would
we wrap it around the entire iners of par song um because we wouldn't want to do it at a higher level because we'd lose
information so we'd want to do it in inside of the parong method because that's where we know what was the input and
which one of these columns failed um and so we could catch the exception and then generate the the thing and then well
then what would we return we can't return a song so we'd have to throw another exception right basically catch the yeah
so we'd catch the exception par song translate it into a different exception throw that let parong plural or the parse
method then throw another exception which we'd have to catch in our application uh and then basically translate and and
figure out oh there's an exception and extract the message and that's just Messier um would you have to do the second
level in other words uh parong you catch the runtime exception repackage it into a we'll just call it a domain level
exception and then not TR then parse parse just doesn't even catch it just let it keep going up bubbling up yeah so it
depends on do you want do you want it to stop processing completely as soon as it hits any kind of error so if the first
row has an error do you want to just stop there and say I can't continue or do you want to process all the data and say
which rows I couldn't import and so it sort of depends on your expectations about bad data so if you've got a thousand
rows and it fails on number five you have no idea if six is good and so you throw an exception for five and stop you fix
it and now it fails on six and so you go fix that and then it fails on 34 and then it fails on that whereas if it could
have continued processing it could say hey there's a problem with 5 6 34 88 and you know 994 so it depends on what you
want if you if you think as soon as we hit corruption means there's no point in continuing then I would say yeah then
there's no point then you just throw an exception right here in par song uh and and basically blow up the entire thing
and do nothing with pars it just it'll it'll get blown away wow I like the idea of getting specific it it just also
seems more complexity for such a small we're just getting started kind of app versus just blowing up and going okay
start over I'm not saying there a reason not to do the either or thing yeah but I'm just the I mean you could always
start that way and then make it more sophisticated with time I guess what I'm try say yeah we could absolutely do that
if you if you is the customer say look it's unlikely I've got any errors and if I do there's only going to be a couple
and I'm fine with with just failing as soon as I hit it um we can go that way and basically then say in that case it
makes sense to just throw an exception in par song so so figure out if there's the right number of columns if not throw
an exception um and that's probably good enough if we wanted to try the um the I'm going to call it the optional
approach call it the either approach you're gonna give it a name yeah because that's that's that's what's commonly used
in other uh more functional languages gotcha so if we're going to go to the either approach we could still use that and
then still behave as if hey we got the first error we're done or is that GNA make it more complicated well uh no it's
it's Bas it's it's it's pretty much do we throw an exception in par song or do we turn a different type where you have
to check that something went wrong that's that's the difference because if we're if we're basically going to um you know
you know then then what happens if par song returns an either where it says it was unsuccessful uh then what do we do
from the parse method to indicate that there was a failure right one second my my son has a question for you yeah
actually let's oh we at break time anyway yeah we're at break time anyway so let's take let's take a break and we'll
come back and and and see what we decide to to do sounds good it'll take a five minute break and we'll be back and uh
continue from there Talk Amongst yourselves all right oh looks like I've got sun shining in it's been rainy here I
forgot that that we actually have Sun uh so just a reminder um of a couple of things one is uh the book club uh we
finished our previous book learning domain driven design and we're starting our next book um voting has closed for that
but uh we still haven't picked a book because basically we have to have sort of a runoff um but if you're interested in
the book club join the Discord like with lots of things if you want to chat more about this stuff talk with other folks
uh who are interested in in design and tdd and architecture and things like that uh join the Discord um the book club we
meet on Sunday mornings 10: a.m. Pacific spefic time which is currently until Daylight Saving Time ends is currently uh
6 pm. UTC uh and we spend two hours on Zoom talking about um whatever book we've selected a chapter or two and uh we'll
um I'll be announcing which book we're actually going to read uh and then we'll we'll start up again with with the new
book so that's that and let's get back code all right so I think we left off deciding either to use either or throw an
exception right I was kind of leaning toward it either just because I've not done that and it'd be a fun to do a
different technique um though I do think you know first failure we can just say sorry badly formed so as much as I'd be
interested in in doing either here as well um I think we can we can yagy it and say well we don't really need it so
let's just do the right thing uh or the minimal thing not the current situation for the current yeah yeah that's true
I've been calling it either but really it's more a a result thing so yeah but um we're just going to throw an exception
yeah you're right because because the either stuff there especially in Java Java's not not quite got the power uh and uh
result would be more than more than sufficient but we're we're going to go even the cheaper route of just going with um
uh throw an exception and you said result is the structure that c is using yeah uh yeah so net has has the result
pattern yeah it's kind of a a shame that I don't mean yeah it's a whole it's a whole interesting area of of ever
handling like checked exception is it's interesting to look at it from sort of a type standpoint it's like actually
every method has two return types the one that is stated in the signature and the one that is unstated so yeah that's
that's an interesting way yeah I'll def I'll defer to your your knowledge of that stuff we uh all right so then our
expectation so what's our yeah is it um what we want is assert there are a couple ways that we can do by like this yeah
first one second uh it doesn't matter and then we give it a a Lambda um so the thing that's going to fail is actually if
you just inline songs there want oh it doesn't want to do it because it's stuff and you need to turn that into a Lambda
so it's not going to take a parameter so you just put empty here like that you say empty PS uh so instead of the s that
you have just put gotcha let me get rid of this so there there's sort of so so what's interesting about a search is is
always that it has lots and lots of sugar there's lots of different way there's often two if not several different ways
to do the same thing um so here we can say assert that thrown by and you give it the code and then you say uh is exactly
instance of uh so you can delete 53 yeah and then at the end of 54 we're going to do um is exactly instance of and then
we give it uh a reference to an exception class what do we want to call that exception um can't for now for now we can
say legal argument exception as a placeholder uh and then we we can replace it with a more domain specific one so the
other way we could phrase this is uh assert that illegal argument exception is thrown by um let's write that one just so
we can compare contrast yeah is it uh it's assert that all one word assert that illegal yep that first one yep and then
the same and then dot is thrown by and then your your Lambda we got to practice using welcome yeah so um I think in this
case if we were going to leave it as a legal argument exception the second one I think is is nicer yeah um but since we'
re probably going to change the actual type uh uh the first one is probably uh going to be more flexible yeah okay dump
the second one yeah so let's dump let's dump the second one and there is also assert that Throne assert that exception
of type uh so we can I actually covered this in my search a talk where I spent an hour like going through all these
variations um so you can say assert that exception of type and here we can say illegal argument ception is thrown by so
it's basically like which one do you want first um I kind of like the second one better yeah yeah I think the second one
is is if you say it out loud kind of feels more like what how you talking about yeah yeah okay cool we just went through
three different ways of doing this y as I said if there's there's nothing but but variations of ways to do things with
the Serge uh and endofunctor zero if you're asking are all these different variations of assert that part of the
standard API these are all part of the assertj library so uh so that exception of type IL legal argument exception is
thrown by that code um I think this will fail because it's currently throwing an array index out of bounds but uh let's
find out at least it will fail in a way that is closer to yeah so now it got an exception which is we expected but it
didn't get the right one so we need to now do that so would we change the assert to array index out of bounds or go to
our custom assert in other words go to green and yeah so if we were doing TCR or something like that I would say yes
let's start out with what we know it does get that the pass and then change our expectation um but since we're using
predictable uh tdd we predicted that this is what would happen so in a sense that's a passing uh that's that's a success
and so now we can move to the next step of of making it throw the exception that we want okay so what would we like to
call this um well oh sorry first we want to get this test to pass oh we need we need to actually catch the problem
before uh going the yeah uh so we asks is there a practical benefit to what are you asking about the variety of
assertions or something else okay so let's um let's make the test pass I think what we can do is we we can we can
basically have a guard clause which is um verify that the number of number yeah there's there's benefit I mean to be
quite honest um search a is all about having different ways of phrasing things depending on what you prefer uh and so
Some people prefer assert that thrown by and some people prefer assert that exception of type um sometimes they put out
stuff and it's like no I like it better this way and so there's a lot of sometimes I think almost too much syntactic
sugar uh the downside is having a lots of choice is not always a good thing so it can be confusing with with all the
possibilities um but that is the nature of a search and I I actually like it um yeah so what is our expectation didn't
we decide 10 well 10 was the maximum we wanted ma but we but we ex so how many do we 10 do we just care about a minimum
care so I think our implication was as long as we get at least nine columns we're good and then we ignore everything
after the ninth column yeah this is GNA be interesting as we change what we're importing but I guess yeah is so it's a
guard Clause so less than nine well we're going to throw an exception if it's greater if it if it's if it's a guard
Clause then we're going to say if the length is greater than nine uh oh sorry you're right less than nine you're right
yeah okay yep yep and that's a magic number which we'll deal with in a bit Yeah you can do thrr and then let it rest oh
cool then you can do I I AE H make sure you get the right one that's the wrong one ah yeah they both have the same thing
so I usually do i a disambiguate yep just a message yeah ill ARG I like that ill ARG usually if you type I that's that's
more than enough to get it to to disig grate but yes ill ARG is is also and it's funnier yeah so we run the it let's see
there's only one column so split good have you seen something I'm not uh no I was just gonna answer we if it's greater
than nine we're fine we only we only look at the first nine columns and so if there's 10 or 12 we don't care um because
it's certainly possible you could import data that has more than that um and we just ignore anything after the ninth
column so yeah so that's cool um refactor yeah so let's development what do we want to call this constant um minimum
number of so my my preference here would be to not bother making a constant out of the number but to hide the number
alog together behind a named guard Clause like this uh since we we can actually extract the whole thing the whole if oh
so the way I tend to do it is is basically um oh require or something require we could say require nine columns if we
come come up with a more abstract way of phrasing that we can go we can figure that out but this is at least exactly
what it does it made it static again oh that's weird I I've noticed sometimes uh int or not like intellig had a bad
habit at some point of a bug where it would constantly flip on the checkbox for making stuff static um and so that and
the problem is is that once you check that box it's on until you uncheck it ah so uh why don't we undo it and then and
then re-extract so we can sort of reset that setting so if we do extract it's gonna go straight uh so what you want to
do is do twice then do it a second time yep oh yeah and this is and this is why um I actually think in any kind of
pairing or group situation having the dialogue always pop up is I think much more clear so but that's where that setting
is so you can uncheck refactor ah the name require at least nine yeah if that happens then would you put just sort of
keep the guard separate um I would actually put the I would actually remove the space from 20 because it's a guard for
for that thing that's that's the way I would do it I feel like that's part of that block I like that that better yep as
so should so that was just a refactor so it still pass right which it did um and now uh and now we can go ahead and and
Ratchet up what do we want the be um I don't think that's enough information though um I think that's fine you think
it's fine yeah I mean that's what we're expecting um and what we'll want to then do is is add more information to the
actual exception message so it tells us uh what the actual data was so that we if we get it we know which which row um
it was on and what what the problem was with that row so I create this guy is this is domain are we testing the
application layer did we not create a domain yet I forget what what packages we' got let's go see no we have domain got
domain pars is in application oh the parser is applic actually that's so that's an interesting thing is like should the
parser be in the application um I think we decided that it was in the application and not the adapter uh although I
still in my head I would I would go back and forth um so let's put the app put the exception in the same place where
where it's going to be thrown from back but let's make sure to put it in the main and not the test directory yeah I had
flipped it the first time yeah go and so we want to uh make sure that's an exception on do you just no we want to
runtime otherwise it'll be checked and we don't right so now it'll fail if we run y right we want to add information
yeah so I think what I'd want is um we'd like some more information at least what row was it on and here's where
actually where we're throwing it doesn't have that information so we'll have to figure out what to do uh but we could
start with a simpler case of okay you didn't have at least nine how many did you have and right so what we can do is we
can add on to after is thrown by we can add on another uh uh assertion right because we shouldn't be changing the code
first right same here or a new exception no no it's part of that because we're basically saying this is going to throw
message and then we can give it the want which in this case is one right um is that what you're thinking something
something like that yeah uh and and also um do we do we want to dis do we want it to display the actual full row data we
actually don't we don't necessarily need need that if we have the row number but it might be might be useful well we do
this first and then add number the Run number have to come in from the yeah okay so now this will fail okay okay uh so
ASD mentions should we mention how many we expected um and maybe that's that's actually also useful even though we know
it's it's nine now it may not be nine in the future right uh or even if the code says it's nine the exception is going
to be in some log somewhere we would like that information can we do plus here of plus um we're probably gonna want to
convert that to string template but plus is uh so I'm gonna I'm gonna point out that you immediately jump to an
assumption of what the problem was and we do that all the time uh and so let's look at the actual ex what the compiler
is complaining about oh right right right right so what I suggest is going to the the the exception class uh and do uh I
forget what the keystroke is it's there yep that's it this all good yep okay that's it now you can go back ah now we're
clear right this one's not being used at the moment just fine y so now it should pass I got the space there after it did
M so now um who was it that suggested asid asid yeah let's do next which was let's go back let's go back to our test
test and say number of one it was maximum right maximum well at nine how was that for a format not sure I like the comma
but I don't feel the need for the colon there because that data is not gonna that's that's part of our our message so oh
I see I was thinking of uh I mean we could pull that out if we'll see the duplication right I don't know all right let's
watch it expected so you're yeah and you'll want the comma andace space and now if we see if this passes we're now green
again we can now say that I don't have a a strong feeling about it like I'm I'm fine with with what it is yeah I guess
when we get to the point where we change the number of columns and we get bit by it we could go that approach yeah I
mean there's there's two things that the compiler uh and that even tests don't care about um is the nine in the word
nine in the method name and that nine in the in the text string right um and so the question is is would would we change
that without changing those as well um I I I could probably be convinced to extract the the nine to to a constant and
then replace replace the the string and the the number with that that constant so this yeah so weat L jokes but I've
seen this I've seen people do this like yes that was so much more helpful yes you've you you've totally documented the
number very well thank you very much but I've seen that and I'm like no I've totally seen yeah um so let's uh will
intellig suggest to convert that string concatenation stuff to using the string templates possibly not because you might
not have enable preview on uh because that's the string template stuff is a preview feature so we might not have that
available um so that's fine uh but do a reformat because that lack of space around the Plus at the end is oh is bugging
me yeah it should have catch all right um anything else we want this message to say I think that's uh the only other
thing oh the row would be do we want to display um oh the content of the column columns so this guard Clause doesn't
have that information uh although it could sort of concatenate The Columns that it got I don't know how useful that
would be um and I don't know about you but what I'd be really interested in is like what row was that whatow that seems
more important than the so here's where uh uh we're gonna have to get a little messy because our song has no idea what
Ro is working on right the only thing that knows that is is here um and even here we don't actually know it because we'
re yagy well I think if we're gonna say we're not going to display the row number then we need to say here here's the
data that we got in this row um as perhaps as ugly as that is if we just if you imported you know 100 rows and it said
oh not enough columns I I don't know about you but I'd be pretty annoyed I'm like uh how do I know which one it is at
least if it tells you some of the data that it got then you could at least search for it um so I think I think it should
uh at least uh I think it should display the what it did find is there a would this all be encapsulated within the the
message or is there a uh this is derived from what runtime exception is there another there's no other place to put this
information that's okay there's not a standard spot standard spot is is this message yeah yeah okay contains or song
number of columns it doesn't know what a row is at this point well it knows it is a row um so so I I'm this well it
turns out we well we're actually not reading this from a file uh this is going to be copy and copy and paste from the
spreadsheet this is how we got to the tab to Limited Format because when you copy to the clipboard from Excel at least
on Windows I actually don't know what it does on on the Mac I'm it does the same thing but that's probably not a good
assumption uh but at least on Windows when you copy and paste that's what it looks like it's T limited so we actually
aren't dealing with files yet yeah we decided to punt on files because I'm the only customer and it's simple so now was
that gonna well I guess we'll find out I I suspect that it's going to be something different than that but we'll adjust
that that's kind of what I was thinking we'll use the the characterization test method of this is close enough what does
it actually do and then we'll we'll fix our test to match so right now the test is going to fail period because we have
no row contains fail and so then let's I feel like we start um here's where I just copy and paste yeah you mean all the
way up to here or not include the arst uh no all that and then really oh just to get a pause just to get just to get a
pass and then we'll we'll replace it thing yeah let's see I I expect it it will produce straight brackets uh around the
content because that's how it does a two string on arrays serves whoa that's interesting oh right yeah so actually we l
was right see see I don't I don't use a raise very much you're but but you were way closer whe than than I was in the
sense that it dumped the actual uh internal uh reference information uh so we actually want to do is um I'm sure there's
a method on arrays to do this so if we call raise yeah Dot T want yes so for Simplicity St throw the square brackets
around it on the test or yeah because that's what we're that's what we're going to want um and we might want to update
the test to basically have two columns yes be a little bit more descript sort it little more meat plus little something
a little bit more that will tell us what what happens when when there when there's many so what do you think have this
fail and then we'll characterize from there um I think we can change the one to a two uh and then we can let it fail and
we should expect it to be artist comma song title oh change we change no leave that because I expected but I expected to
fail on that aspect of it on that not on the y do you think we should um instead of having generic artists generic song
Charle we should have actual songs act artist and song titles I think this is test data so I actually think it's it's
nice to have um generic kind of kind of things sounds good I mean it almost doesn't even matter it could be just you
know the words one and two it doesn't really matter right all right um we happy with the message um I kind of would like
the word rows here but well it's not rows it's columns oh right right right columns so I and I think that's I think
that's pretty obvious from the fact that it said number of columns is two should have at least nine nine yeah you're
right I that uh so you're using you're phrasing this in the present tense which is not it and I'm not saying that was
necessarily bad I'm just noticing that else where else you saying there's tense issues or is that it uh that's it um
contains can go sort of either way uh and i' I'd use the word must here instead of should Ah that's a very pedantic
thing no no I was I was having a discussion I was part of a discussion where we were talking about that it's like should
means there are possibilities where you don't right but in general you should whereas must is like no if you don't then
it's a failure and that's really what the situation is here yeah to me that's not pedantic I totally agree yeah yeah I
guess that makes me a pedant um so let's run our test because we've now broken uh our test and then we yeah okay yeah I
agree with L I think this is one of the things that um I know I probably don't even do enough myself uh but this is to
me where I find um both doing tdd as well as doing these very fine grained uh isolated tests what some might call unit
tests but I think it's more than that it's it's testing against the object that has the behavior it makes it much easier
to manipulate the input so you can get the precise exception uh or whatever fail um which is much harder to do as you
move to other objects that call other objects and that finally call this this kind of thing so uh I I like I like I
failures um do we want to clean up the formatting in that require on the bottom oh yeah uh if I remember the reformating
let me tell check see if I got notes on it feel like it's control shift L but I'm not does nope so it's going to be the
same set of keys that uh the control alt is usually a a common common thing is it l so it's Control Alt L yeah oh okay
so that's was so I tend to to put sort of phrases together on on a single line so you got number of columns was with its
content and then I would put must have at least and then minimum columns on the same row basically combin 36 so you want
to do control shift J oh yeah undo yeah that makes sense yeah I was cool yeah we little things we're missing a period at
the end of the string I don't know about that I think a period the end of the string is a sentence versus a bullet item
which doesn't have a yeah so it's like an it's it's it's interesting like is this error message uh a sentence or is it
it you know just a blob of information that that has no end I don't know I could be convinced either way yeah where did
that test is so um what about the zero case we sort of had the one and the two case is this going to handle the we've
got a row that's just blank and is a blank row an rows sure um no rows will work because when it does lines it's
basically going to be none and it won't iterate through anything um we should probably still write a test for that but I
think we're probably gonna already handle that uh but what do what do we want to do for blank rows do we want to to skip
them I'm leaning towards skipping them I don't think it should throw the whole thing out so we want to test for skip
blank rows what do you think Skip blank rows or Rose what are you thinking by adding the word song there to
differentiate it from well there's no other row so yeah I don't think it's necessary I mean I could see that if you were
thinking ahead about um we're also going to have header rows and we're going to have to process those um but if again I
think yag will so yeah it okay so we just steal this one and we want to steal valid rows we're skipping blank steal oh I
wouldn't go that far we don't care about the contents we just care the number of rows ah I see gotcha so let's yeah is
that sufficient uh actually I think if we're going to do that um then we need to be more precise say do we need to do we
care about whether the blank rows in the middle of two existing rows do we need to have another test for the blank row
being first or the blank row being last um well one we let to test I don't know that we need that but let's let's get
this one to at least work because this one will not work right this one will columns columns so this will fail because
of the Guard Clause we just wrote now I want to know what's in unexpected should we add this no no no well this that
should have failed right that's what I'm saying just trying and debug what failed about it um I mean you could add those
assertions I'm not sure that's going to that's much well it has to if what if it considers this a row well no then if we
considered this a two where was it you were thinking it was going to fail so I was figuring that when it split it into
lines it would have three lines and then uh the second line that it processes so not there but when it when it does the
map um and it does lines and maybe this is a misunderstanding of of what lines does sot lines should uh is it getting
rid of the own oh there it is okay right because I would have assumed lines would have said I'm going to break on a new
line and so there are three rows there are three lines and so um the third line the second line would basically be an
empty string and when it tries to do a split uh it would basically have no columns and that's certainly less than nine
so that was my expectation uh I find that hard to read Q it's still pretty hard to read I imagine uh if you hit the
three dots on dialogue uh you can say adjust font size and you can make it better a line is either a sequence of zero or
more characters followed by a line Terminator so I would have expected line 62 two in the test to be a blank line and
with that and because that's zero or more characters followed by a line Terminator right so what happens if we try to
parse a that not sure if we did because I would have uh we tested sort of with with one column with two columns we didn'
t test with an empty string so let's let's uh let's disable this test even though it passes I'm um I'm confused by
passing make a new test uh yeah let's put it above the one that was uh testing for the exception one row now the other
one Skips a blank grow so this one's going to be just starting with an empty row or yeah we're just going to give it an
empty string the rest is of the test is so you can copy the the test but what we want is an empty string what happens
when we try to do a parse of an empty string so I don't think that copy paste was useful yeah but we want the rest of
the test because it's going to be very sorry I'm not grocking copy 57 through 62 got it 62 uhhuh oh sorry 61 okay and
paste that into the test above got it and then uh on 52 just put in an empty string ah and I expect number I don't I
don't know what does what does split do uh does it return zero if it finds if for an empty string what what does what
does split actually string test yeah the the docs don't say did did we run the test no i r let's let's run the test oh
it just ran all us uh doesn't tell us what it does when the empty so it says if the expression does not match any part
of the input so if there's no tab then the resulting array element which if it had one element columns would be an array
of one and it would be an empty string and so why is that not blowing up because we saying if the length is less than
nine it should blow up can you stick the uh a single character on the in the 51 like that yeah so this should fail
because it's going to say number of columns was one must have at least nine D okay so that's failing in the in in empty
does it return the Min does it return that uh message that so is is split on an on an empty let's write another let's
let's write a test of uh uh uh let's write 49 in the test or in in the test so that dosit Yeah and then uh as a string a
back slash T and uh yeah let's use uh what did we have 10 and so then outside of that um so that returns an array so we
want to say has size one because that's kind of the way I read it and let's run that test or run run passed can we
change that H size of one to has size of zero just see that it actually fails in that way because oh right want to make
sure that iter's yeah being string well string with a slash oh no method oh we're calling the parse method which method
uh that was my wrong assumption that's why we're calling the wrong method okay let's call parong so let's delete 49 and
50 on the top so my understanding of split is correct if it's an empty string it will return a single column that is
empty uh this should be par song uh uh which is private we should really make that public I know that violates all sorts
of things but I'm I'm okay with that uh and now we expect this to fail in in the way that we saw it before which is
number of columns is one must have at least nine and the row contains basically empty bracket yeah okay um let's yeah
let's passes hey swegi welcome howy all right okay so we know that an empty row we've handled that it does the right
thing um so now what I suspect is that lines is either is is ignoring blank lines is the only thing I can I can figure
because we know that if it actually passed that empty row of 70 of line 72 in the test we have seen that par song fail
but what we're seeing here uh and we can write again a sort of a little validation test above above line 70 we can do an
assert that um no no inside the test we're just it's just be temporary we're just validating oh let's enable the test
actually it's not enabled uh let's make sure that it's actually passing because I wonder if we else aha okay I think
what happened was you must have uh we somehow switched we somehow switched to running a single test and we actually
didn't we're not running this test okay good so this in Hallelujah um so uh let's let's now uh now we can finally kind
of fix it let's let's do a a commit um so that we we we haven't done a commit in a while yeah it's been a one changed so
I thought we changed your settings so that it did that it pop didn't pop that up as a popup but I put it in the editor
tab it does sound familiar that oh it's under advanced settings all that just grab that for my own edification are you
writing an article that's going to include all these that it's a good idea actually um show diff that one we we um made
it multiple made the song service test multiple that's not the interesting one think so I don't know if you if you
notice that for diffs it shows uh in the gutter when where there's where you can find the added files near the scroll
bar location all the way on the right so in the right gutter you can see the green oh the green so that shows you uh
greens are changes so that rightmost gutter is basically showing you the entire file and showing you the scroll bar
right sort of where that is in relation so if you scroll down to the green you start added so I think it was pretty much
all data import data have we called it import we haven't what have we been calling it paring that works for me all this
is this is that like uh I really think that setting is wrong like because it's basically committed right so if you do uh
if you open up the commit window all the stuff has been committed correct believe so yeah so the test failed because it
ran the test after the commit even though and I haven't I I have that on my list to to file an issue I think that's
wrong I think it's like if you're going to say uh don't com like if you're gonna say run tests to me the whole point of
that as being part of the commit dialogue is like run the test first and if they don't pass don't commit otherwise
what's it um all right so we've got uh got a failing test it I say and I sorry I say that because uh it's past our sort
of scheduled time slot and so right it is getting yeah if I wasn't dealing with the because this would be a good place
to stop yeah I think you're right um yeah if I wasn't dealing with a little bit of a non-streaming related crisis I
would probably keep going for half hour yeah um is this a good enough breadcrumb I think it's an excellent breadcrumb
because it's basically skip blank Rose doesn't work uh and it doesn't work as expected like it before we thought it was
passing and it actually wasn't right me to put anything into our jira yeah so jir yes suiga you're right it when it does
the code analysis warnings that stops the commit um I never I never had that turned on before so I don't know if that
behavior has changed but it seems bizarre to me that in the commit tool you say run test and it runs it after it that
makes no I I don't know is it is it a bug and I'm the only one who's noticed it which seems odd but it I I don't so I
don't know if that's intentional Behavior or not but if it is it's wrong it's weird yeah so that's why I have it as an
issue to file so I'll actually do that today um so I think we're we can say we're done with process multiple songs if we
consider that sort of happy case um and now we're on to negative cases uh of skip empty rows um are there any other
negative cases I don't know don't know uh and then then next after that I guess we'll work on the the header rows 55
yeah we did because that was basically part of our negative cases yeah I think that's good and then so next time we'll
we'll handle the empty rows we'll handle if we think of any other negative cases we'll handle that uh we'll skip the
header rows and then we could probably move to the UI finally we could skip skip the header rows oh that's that's true
if we want to go right to the right to the um to the UI next then then absolutely skip the header we could skip skipping
the header um all right cool the time always goes so fast yeah yeah it's it's kind of kind of amazing yeah all right
folks thanks for thanks for hanging out thanks for all the participation great to to see you folks um I don't we we
don't yet have a specific plan date and time but of Discord to ted. deev Discord um you get a link uh to to the Discord
if you're not already a member um that's where you'll get the most notice of upcoming streams either pairing with Mike
or solo streams by myself uh book club we uh the voting the polls have closed I haven't looked at it yet today that'll
be my job today um and then uh once we finalize a book um or books a little bit of foreshadowing uh then um then we'll
announce it and we'll get set up and the the book clubs uh will will start again with with with uh our next books so
join the Discord lots of great places to have discussions about everything from tdd and testing and domain driven design
and architecture and Java and all that good stuff so so join us uh and uh click on the alerts buttons in the rolls
Channel if you want to be notified specifically of when uh streams are planned I try to as soon as they get they get
planned I try to put it there um if they sort of ad hoc streams which is usually just me uh I try to give at least some
amount of notice more than you'd get if you were just following or subscribing on Twitch and YouTube so that's it thanks
everyone thanks saided that was fun yeah it was fun I'll see see you all next time by
