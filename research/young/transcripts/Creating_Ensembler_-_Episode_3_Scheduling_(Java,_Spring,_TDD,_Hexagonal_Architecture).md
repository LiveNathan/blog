# Creating Ensembler - Episode 3： ＂Scheduling＂ (Java, Spring, TDD, Hexagonal Architecture)

**Video URL:** https://www.youtube.com/watch?v=1vmu-AMRKl0

---

## Transcript

so this project is uh for me um I've been running I've run now four of these mob programming sessions and there's just a
lot of sort of details that I have to track uh so I'm trying to reduce that manual work by creating an application to
let me uh to offload that manual work it's all doing uh oh we're doing it all test run of course and uh Java spring all
the all The Usual Suspects um and also with sort of an MVP in mind in other words I want to get something up and running
and deployed that I can start using as soon as possible even if it doesn't do everything so there's lots of things that
it could do so I've got a whole bunch of thoughts here um but basically uh the things I really need are um just the
ability to have people self-register so I don't have to constantly poke at people hey are you coming hey are you
registered uh as well uh then manage that uh so that's that's what we're working on uh is a good question so let's run
all our tests because that's what we should do and by the way you can follow along uh let me start flu bits so that way
you can let's open up that window where is flu bits there it is so the source code for this is open foreign so that's
the GitHub Source repo for this project it's Apache licensed um and if you want to uh follow along the code while I'm
working on it without having to wait for me to push something um did a lot did all the tests pass all the tests passed
there aren't a lot of tests still got a ways to go but let's take a look and see where we are um I think the last thing
we were working on was creating uh scheduling a new huddle so um probably want to start creating like a ubiquitous no I
don't want to open that file uh let's create a new file uh so we've got uh huddle this is the mob programming event
itself to replace session which is uh um uh so whoops hey Kenny cuddling time yes let's cuddle our our projects that's a
good one Kenny what are you doing here not doing music not today well I did get my my new midi foot controllers which I
will uh possibly try um all right so that's created let's go back to where we where the heck are we where the heck are
we um right uh scheduling a new session I brought over some code from other project for date formatting uh we got on our
dashboard um I didn't originally intend this it turned out that I sort of put this here of not thinking that this is
where it would go um so let's run the application to see what the page looks like so run right I keep forgetting I
should I should create a home page how about let's do that uh I keep forgetting to do that so let's go do that um let's
go grab I'm gonna go grab the one from Blackjack my Blackjack game because it's a very simple home page and that goes
into static and then we'll just rename some things org um yeah I won't use the coloring that I use and uh we'll just use
a link to get to really really simple page that way I have something mob orb no org man nice typing today all right
let's really did you did you lose this again there we go there we go all right so now I'll click here there we go okay
so we got our dashboard there are no events uh no no scheduled huddles um why are there no outlines oh right because I'm
using I'm using Tailwind which basically completely um that's do that uh I don't want to get too tied um let's
temporarily turn that off and see what happens okay so at least uh at least the stuff is easier to see so name it's not
even figured out what what the name is um because lately it's just been uh on a new the the uh an ordone ordinal number
of of which session I am running so I guess this is technically number five uh uh and then the date let's see this week
is going to be uh um April 30th so for 30 2021 not 2020 anymore uh and that's nine am right so oh that's right okay so
now huh uh do I want the Zone date time foreign I feel like 90 of this project will just so it represents so Zone day
time is what I'm currently thinking I'm using uh it holds so so that is one I want to use okay so that means I need to
convert um the browser date time combine those into a zoned date time which also needs to be okay so we can go ahead and
stop the application because that's about all to um foreign so this is this test that if there's a right so now I need
to actually schedule it so we've got the service that does the right thing now we need the front right so this is this
is where we left off I need to leave better notes about where I leave off next time and oh hey look it's got almost the
right time uh so that's 0900 am that's what I wanted to check I wanted to check what actually gets returned when we do a
post from that form so the dashboard HTML submits to uh so this should be a th action uh that action equals that um all
right so actually I need to see what um foreign play so schedule Hubble form um and so in the form got just named a time
so that matches uh and yeah all right so let's let's run this and see what the browser does so let's go back here and go
back foreign number five which is on April 30th 2021 I forget that I know that that it was going to return it in 24 hour
time format so what I need to do is I need to convert from uh uh okay so now that I know what I what input I'm getting I
can now write some tests for the conversion so that's going to be in the date time so that's the browser uh and I guess
I did have a to-do of what I oh Ted okay uh so time format for browsers or the browsers input type equals time tag is uh
hour so we need a public static final uh uh no what am I doing this this needs to right okay so that they don't need a
separate whoa oh that was weird okay so that's hhmm right so from browser date and time raw date raw time we'll use the
uh um so I want a Zone date time from can I do from uh do I want oh I want something that returns a Zone that returns
Zone date time but that's um oh I want of instance uh instant that's what I want okay so for instant uh and this is
local date time local date time okay and then so the instant that I want is the local date time with uh uh a Zone offset
how do I figure this this is the kind of stuff you do like once you once every project and then you keep going back and
forth whether I want to store this as a Zone date time or as an offset date time and this is what America now that's the
Zone ID so then I'm confused why it needs ugh foreign uh this is the one I'm trying to call local date time foreign oh
because it's not of instant it's just of uh and that is because I want to return so probably should have written a test
um so we're going to test that um browser formatted date and time are converted to Zone and then we're calling date time
formatting format from browser date and time and we want to assert that that zone ignoring I don't think we should I
think it's just is equal to of 2021 04 30 hour is zero nine minutes zero second zero no Nanos and a Zone ID should be
America uh oh that's interesting it got confused uh so the question is is that the right Zone ID foreign Cisco alias
yeah America this one's going to be wrong too so uh so the question is is how is that going I mean that looks right it's
got the nine and if I did this in um November when we have daylight savings time this will fail but uh at least I'll see
what it prints out and so it does print out minus eight so that's correct all right so that's that's actually what I
want all right so let's go back to the dashboard controller so it takes this information and I don't need to print this
out anymore and now here the date time can now be converted via the date time formatting um if you like the schedule
huddle form should should do this work well let's make let's put it here and then we'll push it into that so this is
going to take the schedule huddle form uh get date and uh and then the other thing we want to do is when we display this
stuff it would be nice if it showed it in a slightly friendlier format but actually for now this will be fine so let's
go and close that and refresh this so mob number five o four Thirty 2021 090 am schedule and there we go that's what we
want I mean not in terms of the display but that's the output we want uh cool all right what I should do fine did you
something about the private Constructor yes thank you very much I let's clean up the output I'd like a nicer display for
the date time formatter foreign so do time uh and so the pattern is going to be month to year hour minute minute uh
that's weird in this code I had a static final for the date time formatter for converting for parsing it but I didn't
have one for why am I I don't know all right uh I want do I want Am Pm I think I want AM PM like that uh so the format
is date time we want to be called from the dash the who does the summary View does the conversion uh of the name it's
just doing a two string so we're uh date time formatting and that should do it so I mean I could write a test for this
but it's so easily visually inspected that that I'm fine I'm not writing a test for it uh other than it's annoying to
have to type in some data to get it to show up whoa too many pattern letters uh they formatted date time formatted as
mdy date as months okay here uh so we'll grab this and so our Zone date time and then we'll assert that when we am like
that uh that will we already know cause yeah it is a single a and that's why I'm I'm writing a test because I know that'
s what it should be uh I don't want to run the application I thanks thanks kishu yeah I I was thinking it was like oh
it's like the M's and the D's like you have as many as you need space for um but clearly not I misread the documentation
uh let's run these tests so I expect this to fail because of that let's go fix that it should just be 1A um that was not
expected oh I forgot to change the other test back after I broke it there we go okay uh added date time formatting for
dashboard display yes thank you all right um I don't oh I hit enter and not space and so basically canceled the Mac
still confuses me in terms of what is what is what button is going to be clicked when I hit Space versus what button is
going to be clicked when I hit enter foreign and then when I hit one of the shortcut keys if it if if it goes into here
then it's treated as a pi symbol which is not uh okay she says love to see uh set up spring up with tests yes I am very
much a test driven even when doing spring that's how I teach stuff that's how I do it um we haven't gotten into too much
depth around the spring specific tests um and I tend not to use a lot of makito I'm glad you're a test fan all right so
what's next in terms of features we've got the ability to create uh sorry schedule a couple of huddles trying to use the
correct language so so mob number five is on April 30th 2021 I should probably pre-fill that at some point and then um
also this should get Focus look at that beautiful uh and then mob number six is uh 0501 2021 at 10 am excellent all
right so that's working well which is not surprising because I have tests for that um so we've got schedule a new huddle
uh see huddles and how many registrations for the existing huddles uh um the Huddle list to the huddle huddle I don't
know that I want to do that just yet oh no actually I need to do that because now I need to start fleshing out the the
domain a bit so in our domain we've got a huddle um so when we create when do I want to I don't want to get into I don't
want to get into identifiers too much so I'm going to um uh should I should I use records I'm I'm a um well this is my
domain so that's fine and not sure I feel how I feel about using records in this way I mean it saves me uh of typing but
I do have to put this creation method just to make it a little bit more convenient yeah I think it's okay all right so
foreign Strikes Again by putting the file in the there we go uh uh and I'll need a getter and Setter for that the only
place you will find Getters and Setters in my domains are for identifiers that's fine currently the repository will be
responsible for assigning the ID how the spring data version will work in the back of my head is is should I be using
uuids here I really dislike uids um they're too long and when you try to make them shorter then there's other issues uh
so let's not do that uh oh but we are gonna have to do a find by ID and so the question is do I need to write a test for
this Carefree Sparrow what are you doing here welcome but yeah coding coding not there's Kenny from Kenny's prog rock
jukebox misread sorry no music today or actually not sorry because if there were that would be worse Maybe um everybody
if you're not following Cafe uh so do I want to assign an ID and write tests for that or do I feel confident that this
is really straightforward my coding streams are a different kind of torture but yes my music streams are definitely
although more in the you asked for a torture because people kept asking me um what I do in Tawny so for that in my
in-memory memory yeah I'm just going to copy and copy and paste heck the whole thing is going to be the same uh all
right so this is gonna have to convert from a list to a map uh all right let's let's just do it I really should be
writing tests for um such boilerplate code that I don't really feel they need to do that so our ID is going to be a
huddle ID uh that's our sequence save this just becomes a put uh foreign and that's uh huddle ID of a little ID of and
then we put that okay and this is huddles values uh so all my tests should continue to run and pass unless I've broken
something what did I break foreign oh so I wonder if schedule a huddle is um oh that's my bad uh okay I wasn't running
all the tests before that's why I'm like why didn't I see that fail before okay so now um now this one is failing
because I wasn't running all the tests bad me uh and so for this test we can't just post to schedule uh without having
basically a mock and so here's one of the few places I'll use a mock uh not the mock NBC but a mock for um what is it
going to be for the Huddle service uh why are you still doing that foreign service that's the problem um not the right
thing to do I don't want it to execute any of the content I just want to see that I yeah Still's got to return the
template so if I want to do schedule I'm going to have to post valid information which is a little bit annoying but
that's fine so uh that's gonna be it's not a re is it a request attribute uh so the paramas I need are the the date the
name test date uh oh 4 30 2021 and then one more param for time all right so that should that should fix why what am I
missing why couldn't you parse that oh because I had the date format wrong oh just thinking like this whole web
configuration test doesn't really care what it does with the data um and so it's sort of a shame that I have to populate
it and basically simulate a correct form submission for that but I'll do that for now um all right we're back to all
Test passing what the heck was I doing before before I did that um we're now storing oh yeah we're storing IDs so that
uh So currently this one's fake so let's go make this realistic now so huddle should now have an ID and we should
actually uh get the detailed view for for that ID but for this level of tests I don't need to look at the return
information um because because basically this getting the Cur the getting the detail view which is a string based
representation of the the domain object that's the responsibility of my huddle service uh okay questions what
information do I get here so this is a get mapping um let's start here so this this is where these tests get a little uh
I don't want to I don't want to test for a 404. I want zero to actually be a valid thing but that means I have to have
uh the service know how to to do that so so that would be a service so what do I want here for the fine test uh foreign
for the find at least is fairly pass through it's pretty much going to delegate to the Repository um and how much do I
want let's see so there's going to be a find by ID so that means we'll have to return an optional so it'll be an empty
so we'll create um do I not have my shortcut for that darn it foreign so huddle service assert that the Huddle service
and this takes a okay so let's fix that oh hey ambery how's it going so create this this returns an optional and right
now we'll basically return null which will be fun uh so we expect this to be empty I love a search a uh because I can
assert that an optional is empty um this will fail because it's actually going to return null so uh let's run foreign
empty that'll get its pass and then of course we'll need to write uh foreign so here we'll do pretty much this but here
we're going to assert is not empty is sufficient so this will fail because we haven't added anything foreign this should
still fail because uh even though we put one in there um technically we and then the huddle find by ID should be the
saved this will fail because uh we're not finding anything in our huddle service so it'll return an empty okay so fails
is expected I'll go here uh and now we basically just delegate to our Repository oh we don't have a find by ID method
there or should it be a long this is where I'm still a little fuzzy on what this strict border for uh domain objects are
especially for IDs server it's a domain service so it should speak in the language of the domain but somehow I don't
know it doesn't quite feel right so let's go let's go implement it uh so now this will fail we're testing indirectly but
that's kind that's fine and so now we can basically of the nullable why am I writing this from scratch I've written this
before pretty sure that's what it is so huddles get huddle ID that should work tada okay let's do commit um uh let's not
push until I run all all the tests because I may have broken nope I didn't Jamie what am I missing uh so I propagated up
finding these huddles by their ID um now in the dashboard controller change it so that um uh but let's start one level
lower let's start in the dashboard controller test this is schedule foreign yeah we want the huddle detail view all
right feels like it should go perhaps in a separate test class but we'll leave it here um View uh foreign view of an
existing huddle is returned um go create the repository we'll wrap the service and inject that create the controller uh
and in here we'll grab no not from there we'll grab from here that so now when we call Dash uh huddle detail View we're
going to need an extra parameter uh I don't care what that returns hey there love me love me senpai 101. welcome yes you
are seeing Java and spring and we're as much as possible doing test driven development on this so welcome uh uh so we'll
need a model model equals um and what we want to assert cert uh actually we want to assert equals for I forget the name
of the thing that what am I expecting on the page uh uh huddle detail it's just called huddle uh oh uh all right I have
to do the other that's the wrong kind of test that's not uh so from the model oops from the model we're going to get an
attribute the huddle and that uh not to cast it and so then on the Huddle we'll assert that the Huddle name uh I jumped
to the wrong file somehow uh so we're gonna assert that the name on that good enough but it should fail because um the
wrong name is going to be in there because I have hard-coded stuff in there excellent fails as expected uh so now though
now we're going to have to have the method um take the um I always get confused because spring names things slightly
differently than what they are called in sort of rfcs and other things so I sometimes get confused about the names uh so
what we want to do is we want to not only get the model but the ID the ID so we'll do uh would be explicit about it an
uppercase lung yeah let's do that so long zero of value um oh I don't need to box it here yeah I do so let's go here um
but you see that it it unboxed it but then got rid of it uh funnel ID and then we have uh path variable see that name
just never makes any sense to me like I get it it's part of the path whatever all right so this will still fail just
because I added the parameter I'm still and now I've got two failures right I expected the web one to fail because now
it's totally off um because I'm not passing a parameter but that's fine I'm not testing at that level just yet so this
one is failing as expected uh so now we want to do is call the service find by ID uh uh huddle ID oops huddle not Hittle
huddle ID of huddle ID um now I don't currently have any tests that's what do I want to do if it's not found they should
just return a 404 so I'll need to write a test for that let me not forget to write a test for that I'll write a
placeholder test uh detailed view of non-existent puddle returns all right I'll leave that I was tempted to put a fail
in there but I don't want I don't already I already have enough method enough tests failing so let's go back to our
controller um which will of course explode if it can't find it um and huddle detail view we can now get this huddle
detail View oh I don't have a conversion hmm I don't have a trans translator of domain to view here uh I guess I'll just
do it manually so what does it take it takes the name so we'll get that from the huddle uh huddle um foreign duration
topic and size oh I may as well just do it the right way here I already I have the code here there we go all right so
this should now pass and it does so that's good um that's fine I want to actually get rid foreign let's just suppress it
all over so what is that constant conditions yeah that's fine all right so that test passes which means we can the
detail view of a huddle by its ID foreign so now if we run all the tests we'll still have the outermost uh at webmbc
test failing because it's not using a parameter uh and so it's probably getting yeah 404. all right so let's fix that
one so that's in our web configuration test now this will still fail with a 404 no actually this will fail with the null
pointer exception because we're not checking to see if it was found in in the repository or not let's see if we're right
well that's interesting it passed hey there I am Chets um because the find by ID would do a fi what do I return if it's
uh I just handed off to there and it returns but why did why why didn't I get a null pointer exception because of
nullable says um if if we find something then then that's what that's inside the optional if not then the optional is
empty and then the get uh should have right oh okay so it wouldn't be an old pointer it would have been I would have
expected a no such element exception foreign did one really get thrown and it just oh hey let's get thank you for the
hydrate foreign well let's write this other test because I'm suspicious of that so uh I mean unless no that's fine uh
and then we're going to do and we're gonna assert that the model we won't even get that far if so I have to fix that
post fix so according to what we've seen this foreign so this passes because this is throwing an exception Let's uh pull
this out and just make sure because I don't I'm so now this fails of the nose Okay so this is or working the way I think
it this is the Huddle detail endpoint why there's an order of tests yes it's an order of tests because what's happening
is is this one um so do I want to Mark the in-memory Repository is that mockable no that's in the domain I can't mock
that uh I can mock the Huddle service because or do I just want to do a dirty's context actually if I get this test to
fail that's actually a problem because I don't want it to fail because I just want this to test whether I've configured
it correctly um these are these are these are such a pain well let's say I mock the Huddle service so it should still
fail within yeah so it's still fail that way um foreign that's interesting okay so there was another optional coming uh
really what I need is a dummy huddle because I don't care about its contents but it's just so let's let's make this one
actually let's make it that so this tells us that it will return uh this one when we ask for that one and we ask for 13.
that should do the right thing it does uh let's just make sure if I change this this should fail with no such element
exception and it does okay good so for me this is one of the few places I'll use um makito and it's and it's mock stuff
uh uh it's a little it's a little dangerous because I'm relying on a lie and the LIE is that um what it does with this
13 is always going to be transformed into a find by ID so I am assuming I'm I'm nailing down behavior that this endpoint
method in the controller is gonna call uh huddle service find by ID if it does its job by any other mechanism I will
have to um which isn't great because at this level I don't actually care what it does that I've configured it so it
understands that that huddle endpoint exists and takes a path parameter of a number um but for now this is the best I
can do all right so let's run all the tests and they'll pass so let's do a commit um added a huddle ID as path to level
two so we fixed the flakiness so now we're sure that this test is doing the right thing um what is the next and are we
happy with the the test at the next level in which is a dashboard controller test this one fails as expected so we've
got it succeeds we've got it failing then um oh well actually what we'd like you to do is not actually throw no such
element exception that's what we want to fix um what we'd like it to do is is return a 404. uh that do I throw an
exception and have uh an advice thingy or or am I where do I be very explicit uh a response entity then I can control
that and I can test that directly that's all right so um what's up yeah so I want to write a test uh we're no longer
going to return string we're going to return what are we going uh I could return response entity or I could can I return
a redirect foreign I mean I don't actually want to redirect so what am I doing so I had redirected my head for some
reason uh well let's try it so let's um with that is that what I use here though on the web NPC I've been doing so much
with the apis I'm like getting always getting confused uh I was I was I was that's what I was thinking of and I and I
for some reason wrote the redirect uh so that's what I want um foreign but will that allow me to return an error I don't
think that's what I want so the yeah that's not what I want either do I have to do the wow I have forgotten how to do
this foreign with an exception but is there no other I mean that should I just do it that way is that looking for
something that so I can throw an exception and then have an exception handle that basically translates that exception
into a response entity I mean it's still an exception but uh at least I don't have to create learn something new every
day so we'll still return a string um do we have a test we haven't finished we we haven't created a failing test let's
go create the failing test so what I'll do is in this failing test uh we don't want it to fail in this way anymore we
actually want to detect um a yeah that's good enough I can poke around in it if I want to but okay so now we're
asserting that when we try to do get a view detail page on uh an item that does not exist that's the exception we want
and then if we want we can examine um which would be extracting uh what is it um status and that's equal to http status
not uh not not found okay so we're doing is we're saying that it's this exception and if we extract out get status it
should be that um it will not be this yet that's how it so let's switch back to running these tests correct so it fails
in that way what we want to say is uh get or else uh oh except we can't do that because the so um we'll have to do good
old-fashioned throw new response status exception uh that takes not just pay status not well what do you know that
worked now a little ugly uh this will have will refactor and move this into the Huddle detail View thing uh let's do
that now so this is from yes I got it thank you uh then we'll and then we'll so that shouldn't have broken anything uh
let's now run all the tasks I don't all right so that all works um now I can provide links from the uh a dashboard I can
provide a link directly to the detail on one of those uh let's actually do uh commit so return for for not found for a
tunnel detail View or huddle from okay um so let's go to our dashboard template all the huddles for each one we're just
displaying the text uh but what we'd like is um and I know I'm using a table it's a table it is a table not using table
because it's something else but it's a table and now this is going to be uh this is to uh yeah huddle and is my
expression which is huddle so now in the view I need to head add huddle ID and the href needs to have an app okay uh
title detail View we now need an ID and this gets huddle ID um foreign the Huddle detail View to have an ID that ID will
become part of the URL that will be selectable all right so now this I could could write a test for this but it would be
really super annoying and I'd have to write basically an HTML test to see if it generates the right HTML all right so
now so our dashboard's empty that's fine we'll add that one or 4 30 20 21 9 0 am oh I didn't add ID to the Huddle
summary View Le get ID thank you all right Let's uh just trying to think if writing a test would have been would have
would have I mean this is this is something that that doesn't change um I just wish there was a um could I have written
a controller test no because this is a template could I have written a webmbc test yeah that might be worth it I don't
necessarily have to check to see the specific content but that it just doesn't fail completely like it just did that
might be useful all right so let's and look at that we've got a link does it take us to right place it does if we click
on it what happens we see it all right so that was all working um so we can create we can schedule huddles we can see
multiple of them uh I don't have a good way of going back to it wants me to switch tabs uh I can go and create a new one
and oh 501 2021 uh 10 whoops ten am now we've got two this one's at 10 am the dates and times are correct um now of
course it doesn't persist it that is a problem I mean it's not an uh but I am actually getting on the hungry side uh it'
s getting close to dinner time for me so I can implement I don't know if I'm gonna go for another 30 minutes um so let's
see so what have I done I've added uh uh so the dashboard page now shows all of the huddles that were scheduled um we
can look at the detail view of each one uh they're identified by their identifier um probably need to write some more
tests for the repository but it's really straightforward we can find all we can find one by its ID um I don't want to
persist it into the database just yet because I'm not sure how exactly I want to associate participants which are the
people who would attend um so a bit more to work out in the domain what else let's let's go check out our project so
that's done uh so we can see existing huddles um duration that's just information I need to add into the huddle uh name
versus topic is something I'm still but this is done foreign I need to see participant details so oh yeah goals um I
don't like the way IntelliJ is formatting this stuff but whatever so this is done well actually no that's not done uh I
don't have any of that stuff uh this I think right now I don't think I need anything else I can schedule a new one do I
need to edit one I mean there'll be some stuff that'll be nice to have like sort of postpone or something like that um
oh I just realized I'm gonna need for the participants to be I'm gonna need to be able to see for a participant which if
any but I think in terms of scheduling from my end that's all I need and so now what I need is to display the potential
um which is going to require me to have uh some identity per person so not user maybe user because that's what everybody
uses uh but I'll need to have a uthentication and so with authentication I'll have I guess a user and if they
participate in a mob they become a participant foreign so let's let me create another document which will be um just to
do's to be next so the next thing I need to do is uh participants just um do I want to do register uh what would they
see as soon as they and the language around participant and foreign I just hate the word user but I guess that's what
everybody uses so no pun intended um uh so some sub scenarios on that is um currently I don't want them to register for
more although that's also going to be kind of so what would prevent them from registering um so I can't register for a
huddle they've already registered with uh I mean there's sort of the onboarding process um do I want that onboarding
process to happen when they register foreign GitHub instructions for installing mob sh are um Etc so we'll assume that
that they've so this is uh only show huddles so on my dashboard I want to be able to see all huddles but for a
registration standpoint should only be able to show future ones hey girls um Oh you mean besides user could it be
developer yeah so I'm trying to figure out what the language is so participant is somebody who belongs to who has
participated or will participate in a huddle um I mean I'm not terribly opposed to User it's fine it represents somebody
who I um I mean I could call them developer there's also a part of me though that's like I'm going to be integrating
with some Authentication ID open I you know open ID or oauth kind of thing uh and so calling them user is probably fine
um in the in the Huddle though they are represents someone who has registered system provided to GitHub username Etc so
I guess I'm going to be authorized authorizing I'm going to be authenticating via GitHub because I need that information
anyway so there we go um yeah so there'll be a user or so yeah I mean it might just be a one-to-one thing I'll have a
user which will be sort of just the core of of sort of the information I get back from authenticating via GitHub um and
things like name name email address and whatever I get from GitHub uh everything else no actually I need to know more
for a user I'll need to know obviously you know name email stuff I already have in uh here under participants so I got
name uh email GitHub if they have a disc Discord username um I do need to know if they're new to um and that's sort of a
one-way flag it's sort of a latch once once they're no longer new although it might be that maybe you know that gets
changed or something like that um and so that's about that's really about the user so the question is is what is the
difference between user and participant um I don't know I'm gonna have to play that by ear I I might do a little little
design walkthrough next time using some some CRC cards or something like that that might help uh but I think I'll have
to I might have even though I usually don't do sort of things that that I know a lot about like how am I gonna do the
authentication I haven't done GitHub in a while but I know how that's going to go uh and I usually want to explore
things I know less about in terms of how the system is going to work but I think that might inform at least the
information I get from GitHub will inform the rest of this um and do I need something separate per like so do I need
user and participant to be two separate things or are they I don't know I don't know yet like is there anything that
that would be specific to the Mob programming yeah so my language on on ubiquitous my language on user versus
participant um foreign yeah I don't know I don't want to think about that anymore because my brain uh Chris yeah
especially when rolls yeah rolls I mean it may get to some point where I've got users in the system am I a user right I'
m the um convener for lack of a better word I hadn't thought about that I guess I'm a user and there is a role um but
there are only two uh the manager me and but could I delegate some of that and could a user be both I mean I guess by
definition I'm a participant but I don't need to manage myself I'm only needing to manage people who attend yeah I mean
there's all sorts of questions um yeah so user is the thing that will be authenticated through GitHub uh in terms of
authorization I think it will I think initially it'll be just straightforward it'll be either administrator which is me
or participant and so I guess that's a role foreign um so yeah yeah definitely don't want to be copying information it
will certainly be some relationship um I'm fairly confident that uh I can always refactor my way and fix any problems
but but not running into them in the first place if I can avoid it uh so I might I might do sort of some lightweight CRC
card running through some scenarios to see if if that works um but yeah I appreciate appreciate the the thoughts because
there's this is what makes some of these systems complex is is this stuff and I'm trying I'm really trying not to make
it too complex because I'm not trying to build this build anything too sophisticated uh but I will need github-based
Authentication yeah I mean eventually this is gonna and I'm trying I'm really trying to keep it simple because I just I
need something that works I probably will not get it done for this week's mob uh but for next week's for my future mobs
I want to have this be usable so like I don't even need like I'm only gonna promote this to people who I already know so
I technically don't even need much in the way of Authentication um but I'm still gonna need some representation of them
in the system whether I authenticate through GitHub or whether authenticate I don't think that I don't think that
actually simplifies anything unfortunately there's still gonna have to be something in the system they're going to have
some way of knowing who they are yeah yeah all right well I think I think we're in good shape um for next time uh and I
hope to be streaming most days cause I'm not teaching and I've got time so um that's it for today uh let me push the
last thing what did we just do um oh yeah so we now can uh and uh links now take us from summary View uh go to that is
pushed um and that's it for today uh thanks folks for for hanging out and and giving me some some good thoughts all
right thanks everyone for hanging out uh I appreciate I appreciate it and I will see you next time bye
