# Creating Ensembler - Episode 2： ＂Huddle Details＂ (Java, Spring, TDD, Hexagonal Architecture)

**Video URL:** https://www.youtube.com/watch?v=jiWU5YuP74c

---

## Transcript

foreign hello folks and uh welcome to uh the stream uh so hopefully uh over the next week I'll be streaming some more uh
some more than unusual because I'm not teaching this week I am preparing as I am always For an upcoming class but I'll
have enough time to to stream I hope and um uh what I'll be working on today is uh a project I recently started which is
something to help me manage um so what this tool is is basically a way to coordinate so I'm starting to run multiple
weekly sessions and uh they have different folks who can join so I need to manage that figure out who's going to which
um I have a size cap so I can only have so Simon gearing me no watch out for the Wiley Coyote I see you um so uh okay
it's I guess it's not surprising surprising I guess I hadn't really thought about how many moving Parts there are to to
running multiple mob programming sessions so I've got to know sort of who's who's who signed up cap that that limit uh
cat that do it cap the size limit the size um uh no if they've been there before so I know if I need to hook them up and
sort of as part of that do I need to hook them up to the GitHub repository we're using um do I need to provide them with
other information uh ultimately hooking up to all the apis so that I don't even have to do manually the GitHub we have a
mob timer so I need to populate that with the people who are in the mob um yeah so so a whole bunch of different things
uh uh and I've been doing it manually and it's just kind of annoying mainly the communication like uh you know letting
people know here's the zoom link for this session uh here's the repo we're using Etc et cetera so it's a bit like
hurting sheep of this program is yeah it's not the the hurting is less of a problem it's more just letting them know
that that they've been hurted so uh but my goal is sort of mvp-like is like the minimum I want is just some way to track
uh who's in what uh and I've been using Discord is the main means of communication but I don't want to um sort of I just
restarted my machine and so IntelliJ is not up so let's open up IntelliJ yep all right there we go here we are welcome
to the project uh oh let me update the stream has started so uh I'm probably going to go to around five so what's that
two two hours in a bit um so that's that's we'll see how far we can get hey outernet welcome to the coding stream uh I'
ll probably do uh I've been doing some music stuff although not as frequently as I'd like uh due to some health issues
uh but I have recently been collecting foot controller pedals for some reason um foreign I got the exonic airstep and
the Behringer foot controllers coming at some point so once I get the baron gel I'll I'll do a stream with with both new
foot controllers and then finally make a decision and return the others so that look out for that soon ish because
that's it was supposed to be delivered yesterday and now it's like well it's now at least it's in Stockton which is
close by but who knows when it'll actually be be at my door so anyway um uh let's see so supposedly I had a failing test
to remind where I was uh uh uh info so let's close that let's close that uh so let's see so mineral requirements are I
need people to be able to register calendars GitHub mobile time zoom was there anything else I think that was it uh so
for me to be able to create a dashboard so if when I create a new huddle um the things that it needs are basically uh so
date time I already mentioned that down here daytime duration and topic so right now I've been running 90 minute um mob
sessions which have really been we're like 100 minutes 105 minutes uh which is fine um but I'm I'm thinking about
offering different different lengths hey the grumpy Game Dev welcome welcome uh so I'm thinking about uh offering longer
ones so that we can uh sort of get more done and sort of lower the overhead of getting initially started so that's uh
that's a possibility and also I'm thinking of having multiple but they feel like three hours due to cringy silence I
don't think we've had a session with cringy silence maybe I've had cringy silence on my stream here but not I don't
think we've had that in the mobs um yeah so think about uh so right now I've been using mainly just to get people used
to mob programming and and practice a little bit of tdd and making sure that we know the process and refactoring things
like that uh but this project itself I've uh thought might be interesting because it's more realistic than the blackjack
game not that that's not realistic but this one is more realistic uh and off and doing that during about programming
session because you know that way I get you all to work for me I don't know yes the metanus uh would would yes mob
program the mob programming oh dear okay um so I I have a failing test and I think that test uh was done on purpose to
remind me where I so I think that's what we want to do right because we have dashboard uh and so dashboard has a list of
huddle summaries this we had the Huddle summary view uh and now we want huddle that shows the detail for a specific
instance of a uh of a huddle so fails as expected so um oh in today's mob programming session was really interesting uh
and I have to sort of extract it because uh so I have uh sort of two two policies for um when I'm doing tdd one is that
uh never trust a test that hasn't failed and the other is predict if it's going to fail how it's going to fail before
running um today uh a prediction was wrong and we looked into it uh and it was very useful because the test was failing
but failing for the wrong reason so we fixed it um and then we had it fail for the right reason and that was important
because if it failed for the wrong reason we fixed what we thought we were fixing or implemented what we thought we were
implementing it would have been fine the test would have passed but then if it later failed for some reason it would
have failed in a way that somebody might be confused as to what the heck is going on so I thought that was really good
uh Grandpa game does says I was thinking about this thing an idea to consider is to make a Discord adapter yes uh did I
not have that in my no but yes that was definitely something I thought about so thank you uh Simon Gary from up is
programming the app to organize the mob as a self-organizing all right so this test fails let's create an endpoint so
this is the Huddle endpoint uh eventually oops uh so this is huddle huddle detail View detail all right uh this should
fail because there is no HTML file representing the Huddle detail it's getting way too meta getting a new it's too early
for me to drink though yeah anyway um so this should fail because the template uh where are my templates template
template template there's my dashboard um so what did I want to see on the foreign details oh I guess actually I should
fix that and let's see what do we want to display so that's um so name date time oh and I guess now since I said I
wanted that why won't you line up uh duration duration and topic all right so uh that's what we want I'm just going to
copy that into here uh and so this is the detail page so I'm not yeah I'm not going to display this as a table this is
just going to be a detail I'm not sure we'll figure that out um what's up uh what do I want this to look like I guess
just yeah so let's do um let's just put them in a P tag for now so name uh and then we'll put a span uh is it name or
topic not sure I'm gonna have to think about that so this is gonna be um th text and I'll want something in there I'm
not size so put this in a p whoops put this on a p and I'm going to do similar stuff for daytime duration uh good old
americanism no April before 2021 yeah uh Hey viable Clan member uh the th Tech stuff is part of the time Leaf and we'll
see how that looks when I finally figure out what variable I want um topic that's gonna be Blackjack and foreign size
405. huddle Dot oh I should just do it with object this is all going to be huddle and I always forget how to do that
syntax which is why I have a cookbook foreign yeah well I'm an American so um we like our dates this way as wacky as
that is uh so that'll be named that'll be uh start uh that'll be duration topic and size yeah if I was doing something
where it would require sort of sorting or something then I might um uh put it in different date formats but this view is
for me so I'm the customer so I want that date format for the registration screen that I would think about doing
something yeah so we totally love to be awkward um I mean to a certain extent like this is how we I talk about dates we
say April 24th 2021 so it replicates that but yeah it really from a sort of logical sense it makes no sense I I totally
agree it's okay uh so I need to use the Syntax for time leaf and I forget what that is yes time is date time time zones
time is what is my what does my computer clock say my computer clock says 3 P.M It's 301 pm um okay so I need to look up
uh time leaf what version are they on oh do I have 3012 uh Docs um model attributes know what to call it uh oh it's um
yeah that's syntax but that's for input foreign well maybe I can but I'm not going to try that out now I'll go with Old
Reliable uh so we'll just say huddle.name okay uh so I'm here if you want to do it properly ISO on the server and
localization on the browser yeah I don't want to do a bunch of work I would like to to um eventually provide links for
calendar invites and that kind of thing um let me make a note of that but that's so world time buddy is is the site I
like to use links for cuddles and our because I already have sort of link with calendars although uh both theirs and
nine um oh uh at least for for the date on my computer it doesn't have either format it actually says although you can
only see part of it up here it says Saturday April uh 24. so I don't even have the digit version the numeric version of
the dates because I don't care about the year I I know what what year it is so I all right yeah this is one of those
things where where all the date time stuff could could completely overwhelm the rest of the functionality which is why
that's all right so uh so let's go back here um uh I don't think I need these Styles all right so that should fix the
test no oh because it's trying to evaluate the expression yeah okay that duh so let's comment that out for a second now
2020. that's true it's what day 400 of March March 400 and something 2020 yeah all right so test pass um that goes in
why why is IntelliJ suggesting to put it in the test directory the file in which I created it from is not in the test
directory foreign I have to check on the status of that bug because that's really annoying uh so create a new one of
these or we're creating a new one yeah sure and then and then I will add that attribute under cuddle to be puddle detail
View all right so that will get us closer um oh did we say did we find out that we can use records yes we can use
records how Hallelujah and so what we want is a string for the name foreign hey transtars you would suggest use a Cliffs
if I don't want to have that bug um nice troll attempt uh Simon yeah it should default to um the same directory as as
where um like the context of I'm creating I don't know why it does that uh that's why I filed a bug because it should
not do that it should be related to the the file in which you invoke the action that's relative to where it should be
because that's usually what I do uh so string name um this is gonna just be string uh start because this is a dto so we
can just do string string string duration string topic that looks cool yeah records uh I'll be Clan member I was
configuring my eslint rules for ID length and so is ID length uh like the name of some identity some variable or other
um oh duh I basically created a Constructor uh so let's see so what do we want here um we want name uh 04 24 20 21 10
a.m PPT that's gonna be fun to generate uh duration 90 minutes and size is four okay um um although at some point we'll
need some identifier to specify the Huddle uh I think so this provides us with the view but we need to be able to link
the views uh uh tram stars because uh the view is a dto and um maybe at some point um uh uh like really I don't so I
don't want to provide a local date time to basically the time Leaf template uh because I want it to be just a string and
I'll figure out on on the server at some point um I would provide a date and then have the browser change that but right
now that's complexity I don't want so oh and I dang it did I disable flu bits uh now why would this certificate not be
trusted it's issued by let's encrypt I have not seen that before but I will accept it uh all right uh that might work I
make no guarantees no warranties uh the grumpy Game Dev depends on the issuer but let's encrypt is a top level trusted
thing so I'm surprised that that it had that problem I wonder if that's a bug because I am using uh uh the Early Access
of the next release of IntelliJ so um alevolent uh dice uh why don't I invent my HTML I haven't fully finished it and so
I haven't formatted it um I tend not to indent the body um because that means like the majority of the files indented
for for no real purpose I I don't have a a strong style for for that what do I want to do next um so implemented uh View
impression test and implemented passes and Page exists with basic content all right um so I've got the basic endpoints
it's returning just basic views uh let's just oop right I probably should create a home page and that's my huddle
beautiful I know um okay so those are working of course as expected uh do I want to provide a link from those to that um
for that I'm going to need to start diving into some domain work so let's do that I don't need flu bits to tell me for
this notifications and no pop-up thank you okay um so initially what I want is I'm fine with sort of manually entering
the information so what information do I want I guess do I want to create a session next so I can sort of see existing
huddles over the last really all faked uh I can view the details uh oh yeah I need to see the participants so I'm not
quite done with that um some uh some domain objects for this so we're going to have let's see so what classes do we want
we and that's probably good enough for the detail that we're showing now uh so we'll have a huddle Repository when I
feel like I'm missing something foreign and so I could push down from uh from my controller to force it to create um a
service so let's go do that so I've and actually I'm going to turn off the split right okay so now now I need to drop
back down into this test okay so what I want to do here is I want to have um basically a oops and that goes in here uh
seriously what if there's a problem with my so I need to go look at my templates for a second class so that's fine but
why is it not putting I feel like that should be on the next line all right remain okay and then what I want uh is that
create a Constructor for that I won't do anything else uh this will end up being Auto wired so spring is not happy with
it but I don't care about spring right now um so this shouldn't change anything this should still run all the tests if I
do I wanna uh I keep thinking I want like a different shortcut uh for specifically running the test I think I might have
to create that but not right now um and that's not what I wanted either I all right well I expected all the spring-based
tests to fail uh so that's fine um I guess let's fix that there's no reason why I can't fix that so let's go into uh and
we'll provide a bean uh for so um okay I thought I told flu bits to be quiet but apparently it's not listening I don't
want to change those settings okay what's the difference between flu bits and fluids notifications okay I don't know
what the difference is between those two but clearly one is not the other um okay so what I want is to have uh a method
on the service for finding all active huddles or that's actually a good question what do I want to happen foreign that'
ll be an interesting question to basically push down what I'm well I want to push down what I'm currently faking in here
with uh information retrieved from our service so let's do that so this is going to be instead of huddle summary view
passing in literals uh we're going to say huddle summary View from uh puddles so let's get that no not rename uh all
right let's create a local variable for that that's going to be huddle no puddle hey we don't have a huddle object we
should go create one of those uh but that's actually going to be go and create that that goes in our domain um now that
we have that oh it's a record um can you not have a static method on a record I'm really new to records hmm that would
be kind of a bummer but I uh what do I want to do here because I don't I haven't used records uh in this way before so
yeah I mean basically it's a class I'm what I'm trying to think about is like it's not the way I want to do it so I can
have a static method that okay so why didn't it let me create it is because now it should let me fix it right no why are
you not letting me fix it it's fine I'll initialize it there you happy oh so the fact that it wasn't initialized it was
preventing me from doing what I wanted to do that was annoying all right so let's take a step back uh let's go back
delete that go back here and now now it has me create method so that was interesting the fact that I declared it but I
didn't actually assign it prevented it from understanding what I all right all right let's go create that method uh yes
I'm aware that it's null so what um what do we want to call this uh not sure if I should put a find in front hmm
normally I would but I wonder how that looks um we're trying to get a test to pass right there should be a failing test
whoops would help if I so we currently have some tests failing yes yes the one we're really concerned about because we'
re now trying to move that statically the static literal the literal stuff that I had in the controller I'm trying to
now push it into the domain so I can finally start creating some of that stuff so that's that's the current failing test
um so let's uh say list of um huddle uh transfers what's your opinion on sending domain object from controller to
service main object from controller to service uh so for me if if it's a domain object I wouldn't be wanting to for it
to be valid if some of its properties are some of its information is null um but if I'm sending a dto that's some kind
of search I guess it depends what what are you sending from the controller to the service for is it a search query or is
it create this thing but not all the data is available it kind of depends uh some personally keep fine for methods that
accept search criteria yeah that kind of makes sense like I kind of like uh active huddles uh let's say you want to edit
entity in database um if you're editing an entity why would some attributes be null I mean unless they're nullable in
which case I probably question why they're nullable foreign for now what we want is um private string name private what
was it uh is it zone or offset date time all right every time I look at it forget the difference uh daytime with an
offset versus Zone date time which has so this has an hour uh an hour minute offset versus this which has the item okay
that's what I want uh if you could only edit two then I would have a a dto that only had fields for those things that
are editable and then that would be what's passed into the service and in the service would would merge the two would
apply that those edits to if that makes sense uh so this is start date time and private and um now I wouldn't be passing
the dto directly to the service uh I'd be pulling out the pieces that are that you were editing but if it could be a lot
what would I do in that case um yeah it's hard for me to say what a yeah so I wouldn't pass the dto to the to the
service because that would cross the boundary um but I'm fine with like here's the two Fields I want to edit uh please
update these two fields um but if it started to be more than just a couple then I'd want some kind of domain-specific
parameter object so I'd a huddle edit object or something like that that's that's in the domain or I might just have um
yeah it depends on sort of how how much could be editable how big the things are um and how much you'd how much is
editable versus not editable because another option is you um yeah one way or another you're gonna either have a bunch
of parameters or you're gonna have a parameter object that represents it uh uh and yeah it's more it is a bit of a
mapping issue as well and like summing aside it's like it's it's unclear to me where the responsibilities need to be
split um if it's really just data editing and there are no rules about it they're probably going to be some rules about
it does everybody you know is everybody able to edit the same thing you need to validate the things the fields that
you're editing who does that validation um and that's where sort of having uh types for all the things you're editing
makes that a bit easier um but yeah there's several ways I might do it I'd probably just start off with parameters and
once that got too much then then I'd see where I'd want to sort what do I want to call this this is basically register
registry registered regist registered number registered I feel like we I was we were naming this I don't remember what
we came up with did we come up with something else somewhere uh it was in the huddle um where we create it with the name
and its foreign so here that means name and Zone date time of of oh it can just be now for now uh uh and then number
registered starts at zero so that's fine okay so then our huddles foreign like I'm writing too much without a test here
I need a product owner I am the product owner um I guess it's okay and then I'll then once I finish sort of doing the
the Deep uh the Deep dive then I'll sort of start thinking about what I want from from the service so that's fine um can
chat be well I mean chat certainly can contribute ideas as they always do that's where huddle came from from the oh no
okay um so this is testing that I got a summary view so actually I think that's sufficient because I've got that which
is where I was what am I thinking of uh converts to huddles this is then and so this is uh huddles stream map um no my
return value is wrong that's why uh uh okay so do I want to convert yeah so either this is a list of that's what I want
so this and then let's rename that to views and then this let's change the return type to that okay now that's better I
was like why am I returning a single instance when I want yeah I don't know if I yet want a mapping test but I probably
will at some point so we're going to map um from so this is where like I like the method name from when it's static but
when it's used in a mapper uh when it's using a stream map collect didn't they add was that in Java 16 or was that in
later one where there's a um huddle summary View to view oh if I want that to clarify this one yes okay I wasn't sure
about that uh champ says do you guys use did you uh so the other mapping libraries I've looked at for Java um I like not
maps Google map struct uh is because um ooh spring extensions uh is because you could set the default such that it
wouldn't map anything unless you explicitly said you wanted to map these fields because one of the things I'm I I'm
concerned about using automated mappers is unintentionally revealing information from your from your domain model
foreign maybe I'll try that out it's been a while since I've looked at it but when I was looking at the different ones
this is the one that I thought was was the most straightforward well straightforward not that any of them are really
straightforward but um anyway so this is what I this is one foreign so let's return new huddle summary View and now
we're just transforming so does that take takes the names from the Huddle you just say name uh huddle string and then
huddle uh public time no not get now what is the problem here the old name may be final um sure see this is what I
dislike about um this thing and I I gotta figure out what the setting is to turn it off is because it's not always up to
date and I'll figure it out when I compile when I try to run my tests then I'll know something's wrong but like it's not
compiling enough uh for it to for update hey look the test passed uh looking forward to the next version of automaper
for net takes advantage of the new net.net 5 compilation time code generator stuff so no runtime that'll be good uh this
is hey we all it is still on a mapper I have no no no uh no horse in that race all right so all a test pass let's just
run it nothing should have changed all that was just sort of pushing stuff down into the except that we now have an
actual date time isn't that a lovely display of this of the date time though but you know hey it's correct uh and that's
dashboard and this is huddle uh which is still showing fake stuff so that's not ISO 8601 I have no idea what this what
the standard is that it it thinks it's using for tostring um oh yeah okay so that's that okay so we have converted uh
the dashboard View so we grab the active huddles we convert them to views put it in a model and that's what we get in
our huddle service we're still faking uh the huddles um we should probably push that somewhere I hate tuneless Channel
nice to see you yes and the the meaning will start uh hey Connie Shmoney yes I am using time leaf sorry it was hard to
read your name because for some reason it's showing up as like a really dark purple against black uh in uh the standard
chat window and so sorry about that but yes I'm using time leaf um all right so what's next uh let's do commit um pushed
uh actually oops created for meetings you should use a local date foreign um I thought Zone again this is this is it's
been a while since I've looked at at these I thought Zone date time would won't when I convert the local date time
convert it to a local date time it'll take that into account uh so it uses um it uses a Zone offset uh uses it and a
time zone with a Zone offset so is that right thing I don't know let's see how how far away do I have to worry about
that um so we just changed the daylight savings time we won't change until what November I think I'm okay with figuring
that out later yeah so um I think I think I'll I'll uh I'm gonna kick the can down the road and basically say do I need
to worry about this when we switch back to foreign all right so um all our tests are passing we just did a commit uh so
the next um what do we want to test around this right now it's just a bit of there's no no Behavior yet here so there's
not much to test at this point um huddle service do I want to create a repository at this point so I can start storing
some of this so I can create an in-memory one and um oh huddle should have an adult should have an ID yeah huddle needs
an ID now what kind of ID do we want to give uh what's the difference between instant and local data oh all right I'll
take a look at that um uh uh yeah so I could either create the repository and fill the data with stuff during startup or
I could go and and create the create title functionality I think either way I'll need an ID but I can probably go with a
with a long for that but I'll defer that um so what's the behavior I want I don't think I need to do completely outside
in for this because I know the information I need um it is basically the name right now I think capacity saw capacity
will be our sort of maximum capacity will be global so that'll be um that'll be managed by huddle so huddle being the
aggregate participants oh it's gonna need we're going to need participants at some point but not when I create them uh
foreign oh dear lord okay I will definitely look at this later uh Okay so the behavior I want is we want to be able to
create a new huddle given its name I don't think I need the duration right yeah I will take the time to read it it's not
um I won't read it now hey it's my water uh description I'm not sure what what what you're asking I can interpret that
in at least three ways I wanted to tell me what what um I'm actually kind of struggling with name like what do I call
these things right now it's been mob programming session number one number two number three number four uh oh
description I actually have uh some other stuff I have topic for that um so I don't need something called description uh
I'm even having a hard time coming up with name so I do have topic because I've um sort of multiple streams of what we'd
be working on in the mob uh so that would be the topic either blackjack or actually this application um but I'm
wondering what name it will be like what how do I call these things I guess I'll find out once once I start using it
what what this is for um do I want an auto increment number no I don't think I want that yeah what's interesting is
there other and that actually prompted me uh it's it's my water um there is probably something related to uh for huddles
um besides the participants there's also uh goals of the huddle uh so we have what we call missions that we do and we
try to get get those missions complete or at least get moving towards completing the mission so that'll that'll be
useful for details of the huddle um okay so what's the test I'm gonna write here so for service what we're saying um
that reminds me that's another bug I need to fix so uh this dialogue which you get with uh go to task navigate go to
test for some reason it goes right to it instead of giving me the choice to create yet another one and I don't know if
that's a setting I've unintentionally changed or if that's a regression in the behavior I actually should go and load up
when that was working in IntelliJ but it's very annoying because I like to have multiple tests uh and so navigate go to
test I want to hmm hey information rocket um I don't know when it comes to IntelliJ I've been using it for so long that
that I notice when behaviors have shifted and so therefore I'm fine with blaming IntelliJ but it could be me I I could
have said something uh but I have to remember to investigate that okay uh so what do I want from the service um do I
want to create another method or do I want to use this one so I want to create a huddle and then when I ask for all
huddles it should return that one oh you noticed that problem with the Early Access I've noticed that though even in the
production uh the release ones um this isn't a new problem this has been actually bugging me for for months now and I
keep forgetting to to investigate um so I'm I'm glad somebody's confirmed uh additional experience for that so maybe
maybe it actually is not me all right so let's go huddle service tests um let's call this huddle service create uh
tramstar you can make inner class Oh you mean sort of nested test classes I and so so I had I had someone ask me in I
had somebody ask me in a training course about inner classes uh I just don't use them a lot and maybe it's just me um
hard they're hard for me to sort of find and then sort of uh maybe from test it's fine but but inner classes in
production code unless it's truly like inner and you don't really see it from the outside it feels like it just I don't
know something about it that I'm just not comfortable with and it could be I just don't know how to use them well for
tests I the whole point of me splitting out the tests into multiple classes is I want to see easily that um that there's
multiple of them and that it's a bit easier to find uh uh also I tend to like from a sort of change management
standpoint I don't want like one file to be changing a lot I'd rather split it out but again uh no definitely not you
and my team every time with Chris intelligent go glad it's not just me and yeah and now that I've written a Post-It note
I will absolutely research it and if there's I think I did look to see if there was already a bug in the bug database in
the utrack um I don't think I came across it uh but but good good to have that confirmed all right so the test that we
want is create uh is no I don't think I need to start with zero crate huddle is found is uh foreign you're struggling
with times and can't find a solution oh no what do you what oh thank you for hitting that Discord tram Stars appreciate
that uh okay so if we create a huddle so we're gonna basically get a service so a huddle service and we're saying if we
do huddle service create puddle is that redundant doesn't quite feel redundant because it's not a service I'll say
create huddle I don't care what it is so I'll just use now won't do anything and what can we assert what we're going to
assert is that when I go ask the Huddle service I'm going to say that is has oh there are lots of things I care about
time um that uh for now I'm not going to there's definitely a lot of stuff I'd validate um around the creation of a
huddle instance where yes the in fact I probably want a minimum time in the future if I'm creating one and I'm and I'm
creating one for like in five minutes well I guess I could it's like oh no I forgot to create one but that would kind of
be weird but certainly yes in in the future um and not too far in the future uh uh so at least that for some definition
uh it's kind of if I add a task I set a time in hours and minutes like 0.50 but I want the time in minutes oh off Hannah
I'm not sure I'd have to I'd have to look at that yeah times I've I used to do so much stuff with time and time zones
and things like that when I was working on a insurance billing product six years so yeah all right so this test should
fail because right now we're not returning uh so that'll fail foreign so we could return an empty list but that will be
the same result that it would fail um hey happy puppy tail uh do I use at nullable um I don't use a lot of those
annotations um mainly because I want to avoid nulls altogether so I don't want anything nullable I would push any of
nulls that I'd have all the way out to the edge uh but I don't I don't use it a lot I use it sometimes when when do I
use it I haven't used it in a while but I have used it in the past it's it's fine um it's it's useful if I'm working
with code a code base I can't change a lot yeah I certainly don't don't want I don't think I want any nulls in the um so
what I want to do here to fix this test do I want to push this further or do I want to sort of fake it at this level so
I could in the service store the list but we know that violates the statelessness of a service um so let's go ahead and
and and push into is that taking too big of a jump do I feel okay with that big of a jump yeah I think I'm fine with
that so let's go create uh final Repository uh that's an interface you didn't just put this in the test IntelliJ foreign
try again buddy I'm on to your tricks okay oh I'm a bit of a Maniac of of trying to use the keyboard as much as possible
uh so create huddle service new huddle service uh uh oh um for now I'm just gonna say no and here you know as well boy
that's going to break a bunch of stuff um so now that that's there uh what do I want to do here is huddle Repository
save um actually I should create a new huddle new and then Repository okay and so now now I need an implementation uh
Harry Potter tail do I use one of those fancy split Ergo keyboards no I don't I've I've tried to use them in the past I
am just um too lazy to relearn how to type I never really learned how to type well and I've occasionally gone on efforts
to improve my typing um and those are have been short-lived so I just use my um my uh what the heck's the name of this
one I forgotten what it is oh the kikron yeah so this is the kikron K8 Wireless which I really like uh the only problem
is is that the wiring for the power uh is 180 degrees off of what it should be so foreign oh look I forgot that I had a
keyboard I guess I can take out the still getting used to it part I should edit that oh oh I gotta go edit that okay
yeah the biggest the biggest problem is is as uh for a while I was switching back and forth between a MacBook Pro
keyboard and this keyboard MacBook Pro keyboard if you know it has a a function key in the lower left this has a
function key in a completely different place um but now I just don't use the function key much anymore but all right so
we've probably got a bunch of tests failing right uh let's just run the service create test um I guess that at least be
not null so let's go back and uh in our huddle service create test we'll create new in memory so now that'll fail
differently right because we're not actually saving anything now why did flute bits open up um yeah no functor zero yeah
so this is uh the reason I'm using huddle is because um this is for scheduling mob programming sessions problem is the
word session is so incredibly overloaded uh that I wanted a different term and uh the grumpy Game Dev the other day came
up with the term huddle and I really like that because it's very not ambiguous and not overloaded at all so but it does
mean that somebody new would uh talk to the repository and find all we'll implement it will return empty list for now uh
so we won't get null but we'll get oh you edited for me thank you uh yep thank you appreciate that perfect yeah I'm not
sure what else I'd want to say at this point so thanks okay so uh this fails because it's not actually storing anything
in the in-memory repository so let's go do that for now I'm just going to have a list um at some point when I need to
assign IDs and look up my IDs I'll convert this to a map so this is storing huddle huddles arraylist and now uh save
will basically uh huddles add huddle that should still fail because we're not returning anything and now we'll return
list copy of puddles I know copying it is probably a bit Overkill but let's let's be defensive yeah just thinking I
might change the schedule of a so it feels like schedule's actually not enough I need to create one and then I might
change its schedule because to me schedule is also sort of a bit of an overloaded term um were you asking because of the
the terms all right um let's let's run all the tests so the other tests will fail because we have nulls for our
Repository so we'll go fix those all right so we have an in-memory huddle Repository created huddle is returned for all
huddles yeah no I that that's what I figured you were going at um I agree I don't I don't like create um probably being
over over thoughtful at what would the button be would it be Creator schedule I guess schedule as a verb in that way and
then it would be a reschedule yeah actually that's probably that's probably fine so sure I am actually let's let's
change this so we're going to call this um do that I'll rename this to schedule do we have create anywhere else thank
you end of Hunter zero appreciate that uh Connie Shmoney have I used angular in the past yes in the distant past I use
no but I've used angular one um I don't like it I much prefer if I'm going to do something for me I I am not I am not a
JavaScript developer I I can get by but that's not that's my my main um area of expertise so vue.js works really well
for me because it's like it's it does what I need uh when I need something that sophisticated uh have your puppy tail
because um I like to name my tests if I'm testing sort of a specific aspect of a class like sort of from a feature
standpoint um I want to put that in the name of my test to make it clear all these tests have to do with scheduling
versus finding versus uh that kind of thing because otherwise you end up with with test classes that are really big uh
uh and plus it also gives me a sense of if I've got a lot of those like a huddle service something tasks and I've got
like eight of those then my service might be doing too much I know a lot of a lot of my um actually I don't know if it's
a lot anymore but some of my my uh training and coaching clients uh companies especially large companies like some large
Financial firms uh some large how to describe them a very large Financial firm that you probably have in your wallet
yeah I can say that um anyway they use angular a lot and they always wanted me to say hey can you teach you know spring
Boot and angular it's like nope I can do the spring boot part and I can do the job apart I'm not going to help you with
the angular part I have no interest in uh let's do a commit since we've got all our test passing let me just make sure I
can barely do CSS yeah I'm happy to do spring Boot and view that's fine I I have multiple projects using View uh first I
gotta get my my uh uh refactoring to testable code class recorded and then I'll work on on my you tram Stars yeah so I
don't I don't know what I'm gonna give that class again because I'm currently um creating a self-paced video version of
it um but if there's enough demand I'll I'll be holding another one probably not uh uh service can now schedule great
and find hey BK the awesome uh is the class free uh no um I I do have varying levels of pricing for it there's a lot of
free stuff out there some of it is worth about that price some of it is better than free um but that one that one's not
but I do I do I am so I don't want to go too far down that road um but I have a belief whether it's true or not that
when you pay for something you you invest more of yourself in it um but I've certainly uh drastically drop pricing for
people if uh for based on purchasing power so there's what's called purchasing power parity also for students um and I'm
looking at other ways to to make it more affordable for folks oh join a Discord and or sign up for the mail list and let
me know what you're thinking uh because I'm much more interested in people learning how to code better and test better
um than making money off of it per se or at least making money off of individuals I make I make enough of my money off
of Corporations thank you all right so let's see what's next um so schedule how does return for all yeah there's a lot
of stuff going on my Discord um book study group we're currently reading um currently doing my programming sessions
right now it's only I think it's just a study group oh did we create a link for that uh so besides that uh the mod
programming sessions that I'm I'm working on this application for those right now they're limited to people who've
attended the class uh but at some point uh uh next couple months I'll be opening um as part of a uh a not-free service
um but not not expensive uh and those those are um 90 minutes or possibly we'll do some longer ones a couple of times a
week and we do mod programming practice our tdd practice our refactoring uh and I'm facilitating all uh Hey Kenny's
progress jukebox um well I certainly don't make any money off of twitch or at least any money I make off of twitch is
immediately donated to organizations I make my money by by selling training to corporations who can pay me what I'm
worth yeah I don't I don't I don't make money off of software development anymore it's uh yeah if you wanna if you want
to edit that that command you can you can totally throw the word free in there somewhere uh okay so we've got a single
one um how we propagated that throughout let's let's move up the stack let's go to our dashboard controller uh so here
we've got null let's go and this should Now fail because by default great BK the awesome hope to see you there uh that
did not fail um that's unexpected so that means I'm still Faking It right oh because I'm using active huddles um let's
for now change that and I'll worry about active huddles later in fact good uh and in that case because it's null so oh
that one's null because we've configured it to be null so we'll go fix that foreign so we should still though have a
failing test yeah that's that's the one are we not doing no anymore on this let's see okay good so this one's failing
because we didn't put anything in the Repository so we'll save a new huddle whoa not what I want that zone date time no
okay a little bit of love mod love for for our mod here tram Stars who's going above and beyond uh okay so now we're
back at passing tests let's go um do a commit so I could pay the big bucks yeah don't tell the tram stars that uh all
right so let's uh so basically um uh Now using using in all right so let's take a step back and think about what do I
want next what's the minimum that I need in order to make this thing usable so we can create one we can find them um
should we now create does the reposit I forget what I did with the repository it just adds it to the list right okay so
we can see all of them so now I think let's create a form so I can actually schedule one from the uh into function zero
says would you call the class that represents the read dto resource if it was for Json API we'd still name I would not
name it view if I was returning it as what would eventually be convert the con converted uh so if it's an ATB based API
and that's what I was returning I would not call it a view I would call it um if I couldn't think of anything else I'd
call it dto generally I like request and response so it'd probably be uh uh huddle response or something like that or
huddle View not about huddle view but it'll be it would be have a response in there because it's it's the response to an
API call if I had something that was more specific to the API itself I would use that but I wouldn't necessarily use
View uh I might use dto if I couldn't come up but I tend to use request and response for for apis uh to help me track
sort of visit something coming in or is this something going out foreign so let's pop back up all the way to um the
dashboard to create a huddle sorry schedule a huddle uh let's go into our still don't know why it's not liking that it's
like sometimes it works sometimes so display the huddles and then after we'll basically um create a button create a form
and then inside that create a button uh that says uh schedule new huddle um so this is going to be uh action not um
schedule not thrilled with that name but I can't come with anything better and this is and um what we want with this is
going to be uh um do I want to deal I don't want to deal with parsing and I've dealt with this let's go see how I solved
that problem before so in our web adapter we had date formatting did you crash hard yes you did buy flu bits bye all
right uh so we're gonna grab this oh heck I'll just copy the whole file right now I'll pull out the other stuff uh and
then the important thing is in our resources templates uh deposit uh right yeah no pointing session um so I want uh
input type is I don't want to go down that that rabbit hole and that truly is a rabbit hole where it feels like you're
on psychedelics um thank you uh yeah type equals date and then I'll have and we don't need that and we don't need that
uh so there's gonna be a local early dates what let's see I take it in and I convert it uh I'll worry about time zone
stuff later okay oops now what is it complain about here oh foreign we're going to form the form is going to take two
pieces of information in right now uh so we need to write a test that if we uh submit that information that it it it
okay so now we want um create schedule new huddle results in cuddle Repository all right so we'll create that and that
and so when we do dashboard controller schedule huddle I guess technically I should have created a an integration test
for this being a post endpoint uh so I'm just going to return redirect actually I'm not gonna return anything useful so
let's put that on hold and now let's step back out to our web configuration test and we want posts to schedule huddle
endpoint uh uh redirects so we'll perform a post to schedule and expect status to be is 300 redirection okay so this
will fail when we run this and basically it was uh you know expected redirection but we got 404. oh I think I didn't put
post mapping so yes that's fine right because that's why I was writing that test okay so I'll do Post mapping to
schedule now I expected to fail because it's not redirecting so we won't get a 404 but yeah basically it's complaining
about the template so close enough uh what do I use to host my apps Heroku I love love Heroku I don't understand why
anybody if they have the choice would use and try to Cobble together uh five different surfaces on AWS when they can
just deploy to Heroku I get it if you want to have specific services or or things like that but um Heroku is just too
easy all right I don't know see you later I'm not gonna be going for too much longer all right so now let's redirect
redirect uh we're gonna redirect to Nowhere basically um so that our integration test passes then we'll drop down into
our controller test that's where we'll figure out where we want to redirect to uh which I presume will be dashboard and
does in fact let's run all the tests uh we'll still have the fail test that I basically put aside but everything else
should pass okay good so we finished the post test now we can go to this test and pick up where we left off um so we're
gonna hold on to the return of and the first thing we're going to is equal to and then we're gonna um assert that the
find all and um yeah basically we're gonna pass in something here but we don't have that yet so there's no way this test
can can pass we'll fix this and then we'll work on that so let's get this to to fail as we expect all right let's go fix
the redirect dashboard I always think of the meatloaf song whenever I write dashboard all right so that's as expected
and what we need to create here is basically a new um so that class will go in our adapter and uh oh we can use records
here because right now we're not going to do any validation uh although we can we're not going to use any Bean
validation and even if we do that will so let's call this a record and what we expect this oh the naming conventions are
going to be weird does that work how did it work the other way will it be able to figure out the properties if they're
not it must be able to figure it out we'll be able to write to them but that's why IntelliJ is complaining okay so I
think the reason why IntelliJ is complaining about uh uh this stuff being read is because IntelliJ is looking for
getters um but it doesn't understand that time leaf and or spring understands records and does not need Getters and
Setters because records do not generate names with Getters and Setters with get and set it just has them as the name of
so I wonder would it now understand it no all right that's an experiment for um all right so we've got the date and we
want uh and let's put what does this look like foreign oh uh I don't think that's what I wanted I just realized what I
was doing oh and I guess it's showing on the wrong screen whoops I just realized I am creating the which maybe is not a
bad idea actually maybe that's not so bad basically I'm creating the um the fields and the button although uh I think I
have need to format that um assuming that on the home on the dashboard page you're going to want to be able to just
immediately create a new huddle uh I guess that's fine for now but eventually I'd have I think I wanted that button to
go to a page where you'd create the new huddle but this is fine foreign and I can definitely tell my brain is is uh one
thing I want to do here was display none all right so foreign sure hey spister yes so that'll be date and then oh whoops
wrong field that's going to be something else that's the date this thfield is okay I have no idea if that's going to
work uh that button is unstyled that's a problem I don't want to do too much to fix it yeah let's do that why does that
not look like a all right calendar oh I'm gonna have to add time oh that's gonna be all right well I'll worry about that
later uh okay so we got our front end um with at least the right idea of name and date time on the schedule huddle form
schedule huddle form is a record that looks right our dashboard controller test uses that uh this test should still fail
because we're not using that information hey swifter uh you remember just enough Java from high school just to confuse
yourself oh no we get two failures um two failures why are we getting two failures template dashboard hmm that's
interesting uh uh I probably should not be using a everybody tell element input time yes there's an input date and
there's the time there's also the date time local uh all right let's fall back and use and basically create a class oh
what am I doing let's have IntelliJ do the work for me why am I the IDE works for me I don't work for it drinking it it'
s over I don't know that uh so what we want is actually Getters oh but these are final these shouldn't be final that was
that's the basic now everybody should be happy is well IntelliJ still not happy but that's never been very happy there
but so the issue is record is records um are basically immutable uh uh and we that doesn't work well with with time Leaf
which expects to take an object that it can call sets on to fill uh but it's still complaining why are really did I
maybe do something else wrong why do I feel like I'm doing I'm leaving something out there's an annotation that I always
forget if I need or not uh which is the um hmm the subathon is going to end sabathon is all right let's take a closer
look at what's going on so it's complaining that there is no Bean name available as request request attribute template
Dash all right let's go back to so it's saying that it can't find name oh it's not dollar it's star why didn't you oh
there's a twitch streamer did a still aha so now it's complaining about uh uh oh right of course duh because I didn't
put one into the page um do I want to do that now sure let's go so in the dashboard View in addition to adding that we
want to add although I guess we could do this as a foreign no I don't want to change signature yes now we've got back to
our one failing test that we want to fix uh oh we're almost at the end of time we'll go a little bit longer uh and then
all right so we've got the form the form is populated the right time uh we have the post endpoint right now the post
endpoint doesn't do anything which is why this so what we want to do is when we give it so we're going to say that's not
going to work because it's expecting an actual date that's where we're going to use the date formatting foreign browser
schedule get date time okay and it doesn't like that because uh what but we want a Zone date time I wonder if I should
change it to local date time for ease of use and then uh let's see if I can just change this oh this is gonna have to be
changed anyway because uh this was assuming that the time doesn't matter but actually um and this will require me to
look into uh time is time is relevant yes that uh developer.mezilla foreign HTML elements input so there's date and then
there is daytime local what I'm sorry how is this easily that's easy um this Firefox not support that would be ironic uh
some browsers May resort to text only wait does fire does Firefox seriously oh Firefox doesn't support well I guess
Safari doesn't either so oh well uh no support the input type is recognized but no no date specific control this one has
a bug but basically it has no support all right well that's good to know I mean I can understand I.E not supporting it
uh Edge supports it because Chrome supports it but that's unfortunate oh well all right at least I know so then I'm
gonna have to use uh I mean it's easy to type but I'm kind of disappointed it doesn't and what is Safari's problem it's
got let's see apparently date the uis for date daytime local and time I wonder what that looks like but I'm not going to
worry about that all right so sir this is beyond your skill level so you had some beers I am so surprised you had some
beers and download Chrome and problem solve no I'm actually really disappointed that see this is actually the one I'd
want like this is this is kind of what I'd want I don't want I mean it's fine but yeah yeah no spester you don't ever
have any any fancy beers um all right so we'll have to split that out um I also need two parts from uh separate time
field so this ain't gonna work um all right so that works um clearly this is not going to work when I actually start
running it from the with a proper date from the UI but I'll figure that out later uh uh MD bootstrap I was at the
material design picker uh you know the time picker I'm actually less it's not a huge deal um as long as the it's just
unfortunate that it doesn't have the combined date time uh uh uh picker but I'm fine with it being separate fields so
that means my schedule huddle form I mean actually it sort of makes it a little easier so my schedule huddle form uh uh
so let's go and delete all this so it's gonna need date and then time separately and I'm wondering should I do am I okay
because I basically sidestep that when records worked for viewing do I wanna I wanna go down that road because I'd be
fine using lombok here because this is basically a dto uh hey there cook poo all right um uh so this is date um what are
we expecting again from the browser browser is YY mmdd uh YY mm d 33 yes the 33rd of November of April yes uh what is it
the time format I'm a s what is the time format is there a space before the AM PM I like guava I don't like grapefruit
uh so the question is what is this how hmm foreign the value of the time input is always in 24 hour format that includes
leading so that's fine uh step uh oh that's interesting you can include a list of values that might be useful because I
usually when I schedule my huddles my mob programming sessions I don't do them usually there's a couple of predetermined
times that might be let's see so step attribute granularity um all right so basically it's going to all right so that's
fine um that would be oh daytime is wrong right I just changed it and I didn't change it in the HTML page so let's go do
that so this is not daytime this is date and then separately time and this type is time and this is time and this is
date okay now that should work and then we'll go rate somebody excellent yes I know that you do uh uh do I wanna PR no
I'm not gonna do that okay but but thanks thanks for trying all right that brings us to the end of
