# Creating Ensembler - Episode 1： ＂Let's Call it MobOrg＂ (Java, Spring, TDD, Hexagonal Architecture)

**Video URL:** https://www.youtube.com/watch?v=7Lg5ag13Gfw

---

## Transcript

thank you so let's create a new project we're going to use spring initializer so this project is uh I'm just gonna call
it mob org lack of a better term uh that should go here looks like moborg which is fine uh this is going to go in um
good old com.jitter Tad goboard moborg uh we'll use 16. um do I not specify the version of spring here or is that next I
guess that was next so let's go grab two point should we say the bleeding edge with a snapshot no I think we'll stick
with the get ahead Dot and it'll be fine yeah but I wanted to write a comment maybe so maybe I'll maybe I'll do an ad
and I'll just say pending uh because it's pretty easy to Amanda comment um I'm looking forward to trying spring native
that is going to be interesting um but uh that's experimental and does not support 2.5 yet so we'll skip that uh we
definitely want spring boot Dev tools so I I have been trying to revise my my like uh be more precise about where I
think it's okay to use lumbac and I think the one place I'm okay with using it is for defining uh for defining dtos yes
I do hate lombok um mainly when it tries to create Constructors or uh things like that in my domain um yeah I don't want
it but I think if I just want to use it for for easy to create dtos uh that's probably okay although I don't think I can
use records yet uh for dtos I forget if that's supported yet because it relies on Jackson the the Json processor to to
do that work and I don't I don't remember if it's stored if is it I mean I guess we could try I can always add it later
um so let's skip that uh we want the spring configuration processor um we will want time leaf will want that I'm not
going to start with that but once you add it it becomes annoying so I'm going to leave that out for now uh SQL will
definitely want spring data uh jpa um we'll probably want at some point to pull in the Flyway migration stuff so I'll
pull that in uh I'd be tempted to to do Juke I haven't done Juke uh in years and I'd love to to try it again but uh this
is this is not a a learning project this is a get well records weren't um released until Java 16 uh but I I have to
admit I've not been keeping up with with Jackson and like like I um will want at least initially no we're not gonna use
websockets or anything like that I O we do want validation uh we have to pull that stuff in separately now that used to
be included with uh with the web but now it's separate which was a surprise to me the other month uh Java mail sender I
probably want to but I'm not sure I want to use Java mail sender for that I probably want to use a provider so we'll
leave that out I can always add that later um Ops we definitely want spring boot actuator um I don't have any
observability testing uh I would like to play with test containers um eventually I want to try out the contract stuff
but not not this time around I'm already having have now reached my limit of new things for this project which is test
containers um I've played with reactive spring honestly this goes back to sort of what I was saying before about
scalability I feel like it's it's a solution in search of a problem for most people um so if you've got if you've got a
need for it I think it's really nice but if you don't really need it uh then then what the hell is the point um it just
makes things a little bit harder to work with um tram Stars this new project is my mob mob programming uh registration
tracking system because I system yeah I gotta have work with system at the end right uh so it's tracking uh since I'm
doing these mob programming sessions now and I'm doing multiple ones um every week trying to manage like who's in it
who's in the group have they gotten signed up with GitHub do they have access to the right Repository uh I don't think I
need anything else um look Microsoft azure uh yeah I don't think I need anything else uh would I'd like to install a
shell script formatter for what what plugins you have in mind oh yeah I'll take that um sure go ahead and install that
because today is install everything day apparently if you mean like oh like an orm I I don't unless you're talking about
something that's gonna download stuff so while it's downloading stuff foreign file this will be uh so manages um and we'
ll want to get or participants uh email address uh Anatomy access in my org we have a couple of microservices in
reactive but I guess it's justifiable only for for one of them also some of the services we have already rewrite to
non-reactive oh interesting yeah I mean if you need reactive it's great um if you have you know if you have a whole
pipeline you know and it's part of a pipeline of systems that supports back pressure and things like that and your
database is reactive as well or whatever you know basically the higher the whole pipeline is reactive then it's great I
I think it's it's really useful I just think it's not as widely applicable as as it seems like they're pushing it um
like every time I watch a talk on it I'm like okay you've explained what it is but you haven't said when to use it and
what to use it and and in my old age I'm getting really uh why Flyway instead of liquid base I've used Flyway before um
I remember I did an evaluation of Flyway versus liquid base but that was probably like six or seven years ago so I have
no idea if it's still applicable but I've used Flyway in my other projects and so it's what I know oh tram Stars oh am I
gonna put all my data in my by myself um so initially it will be all manual entry uh eventually the goal will be to do
things like you know uh integrate with calendars because that's always fun or adding uh collaborators to the repo um but
right now it's it'll start out all manual um again it's something I could I could totally do as as a questionnaire for
um you know basically using SurveyMonkey or or type form or something like that but that wouldn't give me uh things like
the the limiting of registration and also I want to basically have a dashboard view um you know so basically uh create a
new session uh see sessions and registration and how many registrations yeah exactly it's like okay cool and that's neat
and like the examples that I often see are these very basic sort of you know more like teaching here's how it works but
yeah I want to know like why um and there's all this effort which is great uh behind like the r2db stuff the reactive
database stuff which is great I think it's necessary um blocking is is something we eventually will will want to not
have to worry about but it's again one of those things where yeah maybe I don't know 10 of the systems five percent of
them need that kind of thing and the rest is just all right and other stuff that I'd like to integrate with uh uh so I
use a tool um when um when I'm running a mob I use a tool called mob time which is really nice uh time so it's a
collaborative timer uh and so what's nice is when you set it up uh it creates a timer you basically enter in the people
who are in the mob and it figures out the rotation and and sets a timer for for each person to have their time in the
mob and then rotate and um so it'd be nice to be able to I don't know if they have an API for this uh it is open source
I haven't I haven't I guess not okay um so not yet but uh uh even if it just I can push a button where it's basically a
copy and paste um list of people that I can just paste into mob time that's that's fine so I'll put integrate in quotes
with mob time oh yeah that's true could totally could okay when I hear about reactive the only foreign all right that's
a good one okay now I'm gonna yeah that's that's that's hilarious yeah anyways like there's a whole bunch of things I
could integrate with um but right now sort of my primary my primary goals yeah exactly looks like a Yol file um so
create a new session so that's uh that's absolutely necessary um so that's necessary uh that's necessary so that's
optional that's optional that's optional that's optional that's necessary uh that's necessary but I could probably wait
on that it's not like I have so many people clamoring for my sessions yeah hey there invisible programmer project sounds
interesting do I plan to to do uh go to go to meeting integration now I use zoom um I'm only going to integrate with
stuff I want this project will be open source um so you know people can do what they want with it uh but but I'm I'm
basically you know it's it's it's a side project that actually it's not a side project I think that's that's sort of an
unfair characterization this project is better than that um it's really I I need a tool to automate this stuff so I'm
writing it yes it'll be it'll be open source hey comedy foreign so yeah license uh Apache 2.0 I probably so do I need
the gdpr no if somebody wants to file a gdpr complaint against me I I really I it's been a while since I've looked
deeply at gdpr but I really it's one of those that should not be I mean I guess I can comply by having a checkbox saying
you agree to be contacted honestly I'm not um yeah I don't live in the EU so good luck good luck trying to trying to
come after me you're welcome to but but seriously like I I this is for for me for for for people who have have already
yeah never mind anyway this is one of those you know sort of related to scalability and performance things I'll worry
about that when I need um so I think in terms of actually order of yeah I mean these are already existing customers so I
already have a relationship with them I mean I I'll explore the gdpr stuff again because I probably will will need to
figure that out but I think right now saying a check box you agree to be contacted would be would be sufficient um so
this there's always the funny uh bootstrapping problem of a project like this which do we develop first um the dashboard
so I can create a session so that people can can register for it or create it have one already existing and then develop
the stuff yeah 100 agree I I would like to have that problem let's put it that way um let's go with with these two
because I think this this will this will this will be okay I do actually have um a surprising I'm always a uh pleasantly
surprised by the number of customers who I have who are not in the US um just think of like of my recent classes
probably half of the people are not in the US uh they have that are not probably half of those are in Canada um and the
rest yeah are in in Europe somewhere so um let's go uh create a story um hmm hold on I just need to configure something
because uh I have I have multiple personalities on GitHub I have my Ted Young um which is my more commercial uh username
but also have Jitter 10 and I want to put this under the Jitter Ted um so let's see Version Control GitHub go and get
repositories using SSH yes I don't know why that's not the default um but that's been annoying in the past is I've
forgotten to do that and then I'm stuck gonna have to go change the remote um hold on I'm going to do this off screen
because I'm not sure if it's going to ask for credentials or something um all right hold on I'm gonna go Secret uh uh
sure it already has access hmm I think it does not allow me to do what I want it to do I'm gonna have to talk to Jeff
rains about that um because it's by default picking the primary account uh username but I don't you can still clone with
with https that's still possible um but it's not but then you have to manage your https and credentials and stuff and
SSH is way better that's actually one of the configuration problems for um uh not problems but one of the um things that
people have to do when when they join the mob to use mob sh so they have to make sure that they're uh that they've
cloned it using SSH um not HTTP or they have a way to handle um all right then I'm gonna have to do this the
old-fashioned way um dude foreign that was not what I expected it to do okay uh let's just run these tests uh so I'm
going to fed up with that good clone and copy the link from GitHub into I may have broken it hold on let me don't do
what I just did all right uh invisible programmer uh MX keys like okay so uh I guess I should run the task um all right
let me go create the project why did that fit oh oh oh because it's got Flyway uh maybe I shouldn't have uh there's a
battery low warning on the the only thing I have running on battery I don't have anything running about it uh
everything's hardwired so yeah it was yours I'm like I don't have anything I used to have um my trackpad running uh
running on battery and then it would run down um that was fun when both my trackpad and my mouse batteries ran out and I
I had to wait until it got charged up and this happened during a training session that was fun um yeah I've hardwired
everything even though like my keyboard my keyboard is Bluetooth but it's always plugged in but my trackpad is hardwired
because I was having problems with with Bluetooth um anyway uh something here I'm not sure what's like on Mac but the
new git cross platform credentials manager has definitely made life easier on Windows yeah I don't I don't actually know
I don't know what credential management is on on the Mac anymore since I just but let's pull out um Flyway um foreign I
guess it was a good idea for me to run all right uh and I'm feeling like I don't even want to I should actually sort of
disable the database stuff until I need it because otherwise it's going um so let's let's group the database and um yeah
the best one you ever talk in your computer says is a huge update yeah I have learned my lesson I do not upgrade
anything uh in the hours or possibly even days leading up to to certainly to talks um but I do so much training that I
gotta update stuff at some point but I try to do it like right after my class is over for the week so I have a chance to
recover all right so my tests are passing so that's good um foreign I'm just going to have IntelliJ push it I'm not
going to worry about uh although I do want to add a license file let's create a new Repository um I think I have a good
ignore uh main will be the default branch um I already had do I already have a readme I have a help file I don't have a
reading I think I can add my own readme file all right and now let's go that all looks good and let's define our remote
probably going to complain because it's uh for commit and push to non-protective oh dang it the whole Main and master
thing um crap uh uh invisible program when there's no Global virus I have some Meetup talks and usually I have to use a
corporate laptop for a corporate laptop corporate ID decides when you get the updates oh uh composite I use my phone as
input device in such battery draining sessions once we better all learn from it yeah version PR except that um it's
gonna be messy if I have two branches I mean I guess I could go and delete the branch but I kind of want to abandon I
think I'm going to grab this license grab this uh yes it's text okay I'm just going to delete it and try it again oops
whoa that was not what I wanted uh manage remotes uh so let's go and remove that yes okay if this is a performing and
you we usually don't understand a lot of Americans have so much time to have issues like Mastermind yeah I I think it's
one of those you know this really isn't there are bigger problems agree totally agree all right so that is it's under
Ted Young but that's fine I'll move it later um I do need to add a readme but whatever I've got this project file all
right amazing how much time it takes when when we do this administrative stuff just thinking of uh of an acronym that
might be better than than mob org but mob org is fun I like it all right taking care of that stuff um that's all good
should I change so I've been using two space indents for quite some time um I'm wondering if I should change it to four
so the reason I I had two for the longest time is um to save sort of horizontal space but but certainly over the past
few years I've gone towards if you have that much indent where that makes a difference you've got other problems um so
I've actually been thinking about going to eight spaces but I feel like that might be be hard for people to deal with
but but I'm thinking about uh going so maybe I'll do that for this project uh tabs because I want to ins even though
that might be a a trolling comment because I actually want uh to insist how many spaces it is that's true there are
accessibility things um for now I'm I'm just gonna leave it because that's that's a that's a bit of a a rat hole that I
don't feel like going down okay I have a question about tddu spring where do I start writing tests from a controller oh
uh funny you should ask so we're actually gonna do that um by the way uh I teach exactly how we do that in my uh maker
maker design more testable uh class we actually spend a couple of days a couple of their half day sessions so we spend a
couple of those sessions just doing that uh test driving all the way and showing how to to split that out but as a as a
preview oh that's a good point eight spaces might be too much for for a PR but then you shouldn't be reviewing PRS you
um um but to uh to acadian's question to preview um this is how I think about writing tests uh uh so this comes from
hexagonal architecture and there's places where we need uh to create unit integration tests or what I call configuration
tests to see have I put the right controller annotation with the right post mapping or get mapping annotations and have
I done that properly in the spring configured correctly but then everything else is oops that's not I want an arrow then
everything else is a controller method uh and those are unit testable and so then basically is unit tested um even
though you're testing stuff that's in a controller class it's still a regular class so and I'll I'll do that in this
project uh transfers project managers marketing PR people have too much free time so they create problems like I don't
think it's I don't think it's a project manager marketing thing I think it's one of those cultural things where people
hopped on um something that they felt like they could fix uh uh in terms of you know especially in the US the relate the
problems in race relations and and things like that I think people hopped on it because they felt like it was it was a
um but it really is very you know theater-like it it really makes no real change and you ask people who might be
affected by it it's like you know what how about we just have the police stop shooting black people that um main master
I could care less I I'd like to to to take guns away from the police that's what I'd like to do so but you know changing
Master to Maine is way easier than than defunding the police yeah I mean recently we've we've had it just never ends I
mean clearly not not much has changed when when you see what's going on in here in in the US especially um you know cop
can't tell a gun from a taser I mean are you kidding me I thought it was a taser it's like really oh anyway I do my best
to do what I can um that's why you'll notice in in chat uh nightbot uh mentions that uh any subs anything that I make
off of of twitch or or related stuff um goes to uh the anti-police terror project uh as well as an organization called
the uh National Police accountability project so um I I donate to those because I think that at least they can do more
than than I I'd want my money to to go there so yeah exactly Simon gearing it somehow makes us feel a little bit better
when it really doesn't change anything so all right um let's get figure out what our first story is going to be so our
first story uh I guess I can take this out because money yeah you you know I I don't want to go down the road because
because I'll just get really really upset and and I I don't want to do that but where this country is in terms of of you
know because black lives matter um police need to be defunded and the gun situation here seems to be like anyway I have
feelings about that so I don't want to get into that there's always something happening right and that's the problem
there's always it seems like every week something happens and it's like oh maybe this time it'll change and it just
keeps happening and nothing changes and it keeps happening so all right but on to uh at least something that that we can
we can do here which is um let's create our dashboard so uh I think the first thing we want to see is um and so what I
want to see from each session is uh uh um session date time including time zone oh look we're gonna have to deal with
time zones isn't that gonna be fun are you misinterpreting markdown no no that's I don't think that's the correct but
markdown's not a standard so who the uh when I was in the US first time I was shocked when I saw the security date at
this project um is my mob organization project uh uh to allow me to to track people who register for my mob programming
sessions that I that I run randburg what id is better for beginner learning Java should I use eclipse or IntelliJ your
teacher has using notepad plus plus my condolences um so I will say that that uh if it's a choice between IntelliJ and
Eclipse I will be a hundred percent behind IntelliJ is it the easiest thing for a novice who's new to the language to
work with no it is definitely a professional tool um there are other tools that are more uh sort of novice Centric like
blue jay and some other ones I I don't know I haven't looked at those in years um but at least with IntelliJ you'll be
able to get some help uh from anywhere whether it's Reddit or stack Overflow or looking at the help pages and things
like that so um if it's something you're gonna work with uh take a stab at IntelliJ it's free the community edition's
free um and you can see if it works for you at least hopefully it'll be better than visible programmer uh maybe you
should put in a header into list except it wasn't a header header it was a it shouldn't be interpreting the the pound
sign um it should be interpreting pants on unless it's the first character in that line that's fine but if it's after an
indented list no but you know markdown with heck knows uh stomach hearing oh is there a note of time in Java you mean
jota time I mean where it came from where it started oh no worries ramborg rambog sorry uh uh Rambo yeah it you know it
is a professional tool it will take some learning um but if you set it up right it it can make things easier but if
you're just just learning then I actually think it's okay to be using notepad plus plus and a command line Java compiler
when I took when I was I used to teach intro Java classes and you start there because you want to get people to
understand what happens to the Java source files how do they turn into class files um that kind of thing I think is
actually important to understand but once you start creating projects with more than just a few files you're probably
going to want something a bit more uh a bit more sophisticated but it is it is a huge jump going from just a text editor
to to IntelliJ it's okay yes we're organizing mobs it's funny so mob programming uh there's some folks who who have
suggested renaming the renaming it to an ensemble programming which I'm generally in favor of of moving away from
something like mob um except from a search ability standpoint Ensemble programming is not searchable uh you gotta you
end up getting a lot of stuff that has to do with music ensembles or Jazz ensembles and things like that and so honestly
I I am fine with mob programming I'm not going to worry about the name um because it's very searchable and so for me as
a as a teacher searchability and findability is really important yes that's where yeah so Joda time was incorporated so
it used to be so it became a jsr uh a standard uh for Java the jsr 310 that was included as of java 8 so it's no longer
really a separate project although I do use Joe to money because I find it much easier than the Java money standard
which is awful if you've seen past streams you've seen how awful it is yeah invisible programmer I'm not gonna read the
whole thing um personally IntelliJ is a real development environment for Java vs code is a text editor and I'm gonna say
if you're serious about doing Java programming and you're doing vs code you're making a huge mistake I will not soft
pedal that you are making a huge mistake you are losing out on 15 automated refactorings that I use all new code with it
we talked about that actually early in the Stream I don't use it because I don't think it was the right it's the right
solution um but I should I should add this to flu yeah uh I'm not going to talk too much about git git is a version
control system so I recommend doing some reading on on on just generally what a version control system is and why you
want it git is a particular one that happens to be very popular for bizarre reasons it is one of the most programmer and
user unfriendly tools I've ever encountered my entire career and I have a long career I've written Version Control
Systems um and it did not have to be this horrible but here we are foreign yeah invisible programmer I I am I'm a big
shortcut nut um I am all about how can I not use my mouse in IntelliJ so I I've memorized most of the shortcuts that I
use uh that I use frequently and and I sort of feel personally defeated if I have to resort to using uh the mouse for
for something you can ask I'm not sure uh if if anybody will be able to help yeah good luck randburg and and feel yeah
invisible program there's the um uh key promoter tool I used to use that um but I found it was like it was telling me
with things that's like I already know this I already know this and so I don't use it anymore I do use the presentation
assistant so you can see you'll you'll see when I actually start coding uh you'll see the the the the the keystrokes
come up good try Simon gearing but thank you I was actually going to type Discord but and thank you for the the follow
folks who I haven't uh I don't generally like to call out people who just follow and who are quiet I don't like to call
out lurkers you're allowed to lurk it's totally fine uh invisible program is is uh uh yes the same is there any plugin
that I use regularly well the for for presentation stuff so let's let me write a little look here uh so at the bottom
you'll see uh the thing pop up for about four or five seconds that's a presentation assistant I have that on all the
time because I'm 90 of what I do is presentation in front of people when I'm coding it's actually kind of rare that I
actually code without somebody watching um and uh so that's always there so that's a plug-in I use um I actually do need
to write up I've been creating a cheat sheet for shortcuts um that I use in my course uh because I promised that to
folks who've attended my course and I've not fulfilled that promise yet so I feel bad about that so I'm putting that
together the other thing I'll put together is sort of all the plugins for IntelliJ that I find to be sort of when I
install IntelliJ on a new machine um but uh certainly presentation assistant is one of the ones that uh that I use um
honestly that's that's I don't have too many flu bits as we've talked about that before um uh and plant uml which is
great I love plant uml I have rainbow brackets just because um I had sonerlin turned on but sometimes it gets annoying
when I'm teaching and so I always forget to turn it back on so actually let me turn it uh I don't want to restart so we
won't do that uh I'm scruffed up um you're probably not going to get much help around here I certainly know nothing
about what you're asking about I'm a Java back-end developer so I'm probably not gonna be able to help you much but if
somebody else knows the answer um oh it's you know it's so funny uh when I was creating when I'm Cur when I was working
on the cheat sheet uh I'm like what keystrokes do I actually use and I'm like I don't remember what I use because it's
so ingrained in you know muscle memory um I have to sort of like take notes of like oh yeah don't forget uh command e
because there are key there are shortcuts that uh that I use all the time that I just don't even notice that um
sonarlint is is a it's a static code analyzer it may have have some security stuff but it's mainly just like uh this
could be final some some more stuff that than than just what IntelliJ offers um uh but it's mostly about static code
analysis just from regular static um I don't I don't know if they do if they have other tools that are for security uh
all right so if we're looking at existing sessions and I don't know why the tabs are indented like that or whatever um
sorry I was just got distracted by something uh so when I see a session name session date time number of people
registered um what else do I want okay and I guess details about the people who are registered uh participant details
and so that includes uh their GitHub username uh their email address foreign oh hey radio we are check marks yeah check
marks I don't know if I've used them foreign so and I'm going to work with a very basic uh very very very very unstyled
uh HTML output for this although I am tempted I am I am somewhat tempted to put a view front end on this and use an API
just because uh but I'm not going to do that I might add that but I'm not gonna do I think I can't even no not that
unstyled it'll it'll be it'll be black um it'll it'll it'll it'll be it'll be very unstyled you see even blue and yellow
is styled so it won't be like that because it's not a game only games all right so that's that story um I'll figure out
other stories such as uh create new session so I'm even thinking for the first story uh do I want so Craigslist yes even
that's that's some yeah 19 I mean I'll I'm gonna I'll eventually I'll pull and tailwind and do the styling with that but
not right now all right so what we now need to figure out is what is the first test we want to write um so the first
thing we want is when we hit the home page uh uh not the home page I won't have a home page just yet I will have a page
for me which is basically just dashboard um so well see so uh hey we can actually now write a test we know enough about
what we want to do that we can actually write a test isn't that amazing so we're going to create um and we're going to
do this hexagonal I'm going to use a hexagonal architecture so what we're going to be writing is a test uh actually
basically this kind of test we're going to rewriting a web UI adapter and we'll configure that we'll red test against it
actually the other way around all right the test against it and then configure it properly yeah like that all right so
our first I'm going to call it web configuration test because I'm really getting tired of using the term integration oh
did they ruin the shortcut key for so in general I really like the mac and in general I really like at least non-recent
Mack ey stuff I find some of the recent stuff to be bizarre um what I really do not like is the mac and the Mac UI never
since night you know ever since 1984 has never really been keyboard friendly it's always assumed that the mouse it's
very mouse-centric um and so whenever I can't use a shortcut key for something I'm always really annoyed it's like that
dialogue that showed up um there was if you hold down the option key it's supposed to underline the ones that you can
then press the shortcut to click it and there wasn't one for the check box so I had to tab over to it from an
accessibility standpoint that uh invisible program yeah there is no API so I may uh I may have to um there are two
options one is if I can at least make something easily copy and pasteable so I can copy and paste into mob time that's
fine but also mobtime is an open source project so I may uh open up an issue and I think it's a language I can write
some code in so I maybe will even contribute something foreign so this is going to be a web uh a webmbc test um oh the
W's not capitalized that's why uh we're going to Auto wire and uh oh I wonder if it wasn't excluded I'll check uh come
on import it thank you send keys and window handles yeah uh I mean I guess I could do something uh I'm not gonna go that
far uh transfer says my OCD is asking if you're gonna foreign do you really put private in on your mock MBC in your
tests I don't I guess I but I don't know it's a test uh okay so um we want a uh get request get to dashboard get of
dashboard all right so we want mock NBC we want to and then we expect God I hate static import stuff in tests so much uh
in this program it seems like completely extended I already have one endpoint yeah I I figure it would be fairly
straightforward to extend um I'm not I'm not too concerned about that uh Chad says yes you don't know why hey lexlers
yeah they're all visibility is is uh would be would be packaged and so basically any other class in that package would
be able to access it if they instantiate the test and my question would be who the heck is instantiating your test
besides your all right so we're doing tdd look at that uh and because we're doing tdd and my style of tdds to do
predictive tdd um we're gonna have an expectation around what we expect from this test so certainly we expect it to fail
and the question is is is how we expect it to fail in this case uh spring will do a 404. um so let us run all of our
tests uh so we expect this to fail with a 404 assuming everything else is configured correctly and look at that it fails
and fails for the right reason great all right so now we can go create a um this should not be in that package this and
then what we want to do is we want to create a whoops I'm going to create a new class create a new class this will be
our this will be an adapter and we want a get mapping so this is dashboard um uh dashboard so this will still fail
because we don't have a template for this but let's see if that's why it fails foreign development I don't like
fear-driven development that's way too much anxiety uh okay so this should have failed because it couldn't find the
template um correct it could not find it because it does not exist um we want it uh under resources templates foreign oh
look I'm already using now we're using uh Tailwind look at that okay so why does it feel like I'm missing okay so I
think if everything is set up correctly um this should so do commit dashboard endpoint we can see which files I added I
don't uh uh optimize Imports but don't do so got that that works um so we should be able to run the application I'm just
looking at the output here uh that's expected because its dashboard is the endpoint I created and hey look at that all
right I switch into four spaces yes I am going to switch the four spaces yes I'm gonna do that I will I promise uh
invisible program oh thanks for this tip I hate those codes yeah there so there's stuff in IntelliJ where you can sort
of configure globally that will apply to all projects there's things that I have not been able to figure out how to do
that with one of which is um these tools on the side I like my project and structure up on top so I can have that open
and I like my commit down here so that way I can have um the project open and my commit window open uh and I haven't
figured out how to make that as like open all projects this way um the other thing is uh uh the git commit stuff that I
haven't figured out how to say no you should be the defaults for all projects so I will probably have to ask for help on
that um there's a program why don't I set up because it's almost always Auto uh Auto um oh I know why uh there are times
when I import things that I haven't yet used and then if I optimize they get optimized away and so I don't want it to do
it that frequently so actually it turned off that feature because um like when I create a test file it pulls in the
search a uh assertions and I want that to go away and and get optimized away so doing that on Commit is is one I'd want
to do that hello binku all right so so let's see what's next um so we got that part work working uh so now we want to
see existing sessions uh and so what we want from an existing session we have that information um so we'll need to
create a dto oh I know what I wanted to do and I always forget to do this uh uh do I have a pojo being um Json the
problem is this one hasn't been updated in like three years and it uses Json and that's not what I want um based on your
tells no an helper no Java Bean to Json no not the other way around I want not pojo the Json but Json to pojo no why are
they all going the wrong way they used to be a plug-in but then it stopped working and so I've been looking all these
ones that take a pojo which by the way is just don't use that term anymore stop using pojo um that's what I want uh
generate Java and kotlin pojo files whatever I I have lost that battle uh a all right never mind not now all right so uh
so let's see so what do I want next what I want next is uh for it to iterate through sessions so I'm going to create if
anybody has a better word for for session because I feel like the word session is way overloaded in this industry uh let
me know um I could use event even event is over so uh but we'll go with special session for so one is for this to pull
into the model well it's not hodl total uh if it looks like I've been working on a remote meeting software there were
endless arguments about what exactly a words like that are like I can imagine oh my God yes yeah um should we go with
huddle I'm playing with going with huddle uh but we need to write a test first so let's go write a test uh we don't need
to write a configuration test for this because what we need to check is the content that is returned and we can check
that by directly uh uh calling that so we're going to create another test uh I'm almost hesitant to call it a dashboard
controller test but we'll start with that that's what I wanted to do there we go because then it Imports my I don't want
to exclude it from Auto Import but now I want to find out why is who's why is this being why who isn't foreign yeah but
it should have set it up so because by default it includes j in it but it's it it used to set up and maybe they stopped
doing that it used to set up the exclusion of junit 4. um but I wonder if I now have to um oh command plus oops I'm over
here there we go command plus does it uh oh interesting that test containers why why would test containers and the test
containers junit Jupiter which is junit why would it do that what is wrong with you people I'm sure there's a good
reason but I'm like that's so weird I I would assume if there's a specific G Unit Jupiter version artifact of test
containers why oh because it pulls in the regular test container so the regular test containers must have okay uh so I
guess I need to exclude that from um because that's getting really annoying uh because yeah it used to be that you'd
have to in the um uh starter test it used to be you had to exclude this but I haven't had to do that in a while this one
which ironically is the junit Jupiter one I forget how exclude works so exclusions exclusion junet okay thank you
IntelliJ for helping me on and it's now gone all right no now why is it complaining oh it thinks it's a Constructor no
it's not a Constructor I'm just not done yet uh uh what tests were we writing um all right so what we want to do here
what we're doing oh yeah we want to display sessions uh so the test we'd like to write is that um it puts some session
info into the model uh so given uh oh we're gonna call it huddle let's given one huddle uh results in huddle ways huddle
put into model our invisible programmer thanks for thanks for stopping by appreciate it all right so uh we'll create our
controller I keep wanting to type Blackjack controller because I type that so much okay and what we want to invoke is
dashboard view with a model and what we want to assert is that the model at least initially it contains an attribute for
huddles all right so this should fail because and it would help always doing this I'm always running the application
when I mean to run the tests and sometimes vice versa actually never vice versa it's always I mean to run the you need
to figure out a way to stop doing that all right so we want to run uh okay so that fails uh does it fail for the right
reason yes it fails for the right reason okay um so let's model add attribute huddles and um just thinking how how I'm
gonna want the the dto structure do I want something called huddles that has itself yeah I'll probably want something
like that so we want new huddles Game Dev says yes so we must do it uh this is going to be and in here uh well this is
good for now this will get the test to pass and then we'll worry why foreign I feel like it's something obvious that so
or as possible I'm confused well how else does one I feel like I I I don't know what's going on um because underneath I
mean I've used it before and I feel like I've all of a sudden not I don't know anything anymore like contract as a
record um I wonder if it's a problem because like there's nothing in the Constructor but otherwise you just knew it up
and so I just wonder if but wouldn't that cause a compile error like maybe you can't have an empty record but I I feel
like IntelliJ is just is drunk yes uh okay now I feel like I'm doing something stupid so it's basically saying it doesn'
t exist and now here we'll do oh did it put it in the damn you IntelliJ thank you now I know what's wrong and I blame
IntelliJ because it always no it has nothing to do with the record having something in it this is in the freaking test
directory because when when I asked intelligent it created it said oh of course you want to create the test directory no
I am in a freaking production class why the hell would I want to create this in the test directory and it does to this
to me like um I guess we've already given it a name so what the hell okay but seriously I I can understand if I was in
my test class and I think this is where maybe it's getting confused because I have a split pain and and maybe that's why
it's doing it but I can understand if I was creating a test class from a from a test creating a new class from a test
sure put it in the same place but over here I said create it and it created it and it yeah Alexa is yeah and that's why
I do point out in the class but maybe I should I should be like you know flashing a big sign saying watch out for this
problem because it does it happens all the freaking time yeah well back to a close thing no no no oh uh talking about
equality um yeah I forget the rules of equality for records it's probably what you would think it is it automatically
generates um an equals method for all the member variables um but otherwise but a record is just a class it's just
syntactic sugar for creating all the stuff for you oh all right I'm calm now that's so freaking frustrating and I filed
a bug against that I need to to so I can remember this moment where are honestly that's one thing that's really nice
about streaming this stuff uh is everything I do is recorded and so I can always provide a a video snippet of look uh
code compiles it should do what we want let's run our tests and they do excellent uh so now dashboard endpoint um oh and
we also um we also uh excluded to unit for which came in I love how easy it is to amend commits Endo function zero with
what age would you want to stop programming working doing workshops you mean at what point for me what what age would I
want to stop doing that uh I love doing it why would I want to stop yeah uh someone gearing you also have a timestamp
for the bug report for IntelliJ doing a dumb read the code generator namespace yeah I've uh which one was that uh hey
there um I'm gonna figure out how to mash us 92 uh why use MVC instead of rest and standard front end um because I don't
need the complexities of of a full front-end application right now eventually I might want to do that but right now if I
don't have to if I don't have to write front-end code I don't want to write front-end code I have written it I've done
lots of not lots of but enough front-end code that I could totally do it um but um it would be Overkill basically for
something that is that is pretty much mostly just looking at stuff and form-based filling out things uh a single page
application would be would all right next piece of functionality is uh so now that we have the huddles there um what is
going to be in there we let's define that uh and here so the the properties that we're going to have here a huddle is
going to have a name um I swear I can't look at like string name and think primitive Obsession anymore I have lost that
ability uh what else did we want we want the session name um okay now I gotta figure out which date and time do I want
to use uh I actually I won't need will I need an ID eventually I need an ID right now it's a name it'll be the name of
the session like mob programming um I'll add identifiers later uh into function most front and don't actually need react
angular they just use these for developer happiness yeah I find yeah lots of people use those large front end and they'
re not terribly large I mean I actually think Vue is nicely sized um or react isn't too bad either I think angular is
kind of large um but we use those when we shouldn't I remember when uh the bank I use uh for some of my accounts is
JPMorgan Chase and I remember hating them so much when they changed their their web Bank interface from a nice you know
perhaps a slightly dated styling but a real server-side generated HTML application and then they converted and now when
I visit the page I have to wait several seconds for it to finally populate the the page whereas before it would come up
and it would have all the information I needed and does it need angular no there's like no State there's no front-end
State and if you don't have front end State what are you doing it's I mean a bank application is like the most I do is
fill out some forms like I want to transfer money or pay a bill but that's a form why the heck do I need a full
front-end application that keeps taking many seconds to to do its job anyway so don't use it unless you uh hey there
idiocracy uh uh do I program it using a specific version of java in mind um I try to so it depends on my my audience for
my projects um I will try to Target the latest release the latest current release latest I guess not ladies and current
the latest release as opposed to the latest version uh in this case with 16. um because I I want to know the latest
stuff uh but when I'm doing consulting coaching training uh I'll stick with 11. um I do not tolerate companies that have
not upgraded to 11. uh if they want to take my class they're gonna have to upgrade to 11 on their machines um that used
to be a battle that has not been much of a battle over the past year um if you can't get the Java 11 you've got more
serious problems um I don't expect companies to upgrade to 16. right away but if you're not on 11 you have no hopes of
of getting anywhere else uh yeah so honestly I I picked the latest release unless there's a reason I need to be
compatible with anything there was an interesting uh tweet thread by uh Trisha gee and and um uh I'm sorry I'm blanking
on her name uh developer Advocates at jetbrains where they're asking like what would you what would you develop and I
can definitely see if you have to if you're in a larger organization you have to pay attention to sort of what's the
prevalent thing what's the deployment uh mechanisms um but I I try to stick with the latest because I want to use things
like records right now I can actually use records for real uh uh so why would I why would I hold myself back uh okay so
we got the the name of the session I'll have to add an ID later um what else do we want we want daytime oh yeah we think
about which date time do I want and it's been so long I don't right because that one is a daytime without a time zone so
we want uh so that has an offset from UTC so uh but I always forget the difference between offset daytime and Zone date
time foreign uh oh so it actually has the time zone instead of the offset um oh the Zone daytime has full time zone
rules time zones um yeah actually I want the time I want I want I want Zone day time because I might be planning things
in the future where uh if I'm planning something for after we switch from daylight savings time back to Standard Time
does that matter um well I'll use Zone daytime I don't know what I um uh uh anything zero why do people not upgrade from
java 8 to 11. um is it that hard to migrate apparently yes um because have you seen the craziness of corporate
Enterprise level applications in terms of how complex they are and the set of dependencies and getting that thing into
production it is a nightmare I've seen some some things that I'm glad I don't work at those companies um they have
dependencies on dependencies on things that are customized and have been used over time uh and they maybe were just able
to get it to eight um and have had great difficulty getting it to be able to deploy onto eight let alone 11. and they
just got tired and said well we'll wait a little while longer even though and Java 8 has been um in general it's not a
problem unless like it's usually not their code that's the province usually libraries that they depend on that maybe are
no longer maintained uh there are all sorts of reasons but they're really in my opinion they're just bad reasons they're
just excuses like you need to be able to upgrade um but usually it's a it's often a symptom of a larger problem around
their continuous uh they probably don't even have a continuous deployment system um in in a surprising number of cases
but I've I've seen Horrors and it does not surprise me that they cannot Get It Get It upgraded I know of a very large
that only recently have have started to yes code is code is code is not not an asset it is it is uh a liability so all
right uh what else do we need in our huddles why see now I'm on to IntelliJ you're not going to fool me this time why
are you for me once and and so on okay uh so for each huddle I should start renaming this stuff here uh so so for the
same name that can just be okay so we want um oh I didn't need the name for huddles uh uh huddles is the list of huddle
the Huddle I have each one of these has um I don't think I need anything from here other than as a container do I even
need this I could just store a list of huddle I thought it was gonna have something overall um but I'm gonna apply I'm
gonna apply yagni uh seven gearing time to leave and hunt and off to bed uh it was great to see you time gearing glad to
hear uh about your new job and I hope that continues to go well uh end of functor zero can use records as hibernate
entities I actually don't know um I don't know we'll find out when we get there I probably don't want to um because
you've got to put annotations on things and it's you can do that in in records but I feel like it's easier to to manage
with uh with just classes but um I think I'm gonna get rid of uh so let me do this let me take this back to what it was
and actually I'm just going to rename this to huddle uh uh let's go delete this um now uh we don't need that uh uh and
number registered so now we need to go back to our tests uh uh so what does it take takes a name and two okay so uh uh
oh given one huddle results in that so that's fine we can now do this a bit more precisely we can do model get attribute
puddles and what we'd like is this is to be a list now this will fail so we're saying uh has size of one so this will
fail because we're not even returning a list hey Class cast exception I bet you were never so excited to see a Class
cast exception like I am all right so this is going to be uh we'll pull this out into variable we'll call this a huddle
uh and then this is going to be list of huddle and that passes cool all right uh so now let's you and your stream of um
I don't know how well time Leaf works um so I'm gonna stick with list because uh yes lexlers I basically when I'm in
refactoring mode um then I'll start thinking about primitive Obsession uh uh and things like that right now I want to
get to the point where I can see the huddles um and then I'll and then I'll start uh that's a that's a great point of
the Grammy Game Dev uh I just don't know if streams how well streams are support although you'd think they would be we
can try it let's get what's new what we know working working uh and then we'll then we'll try it out uh what I want to
do uh is this going to uh um uh oh no that's not that's not the each syntax that's what it is we want huddle from
opponents that's what I want foreign that it's having problems with that I wonder if it can't handle records because
it's not because records do not um th and uh number registered what's a complaint about the th wait okay all right uh
tea body TR TD I'm concerned that it uh the company came down who why does a view need a Setter uh a view doesn't need a
Setter a view needs uh a getter um and it needs the objects the beans the it needs them to be Java beans and so they
need to have Getters uh to provide the standard way of retrieving properties off an object and Records do not do that so
I have a feeling time Leaf probably doesn't like records is my is my expectation yes naming convention which was
probably in hindsight uh it was the right decision at the time it had interesting repercussions which were in my opinion
should not have happened and I don't fault the Java means for that but um things that have Setters and Getters that
therefore define properties is uh uh part of the the Java being specification that um I think it was a fine idea at the
time and I think it's it's still a fine idea I think unfortunately what's happened is people have have taken what was
meant for tooling and put it into regular hand coding things which is why Setters and Getters are evil so um this is not
gonna work our tests may pass actually I wonder if the test will pass is time Leaf going to complain and blow up
honestly I'm a bit surprised it didn't maybe IntelliJ is not recognizing this correctly so let's run the application and
and see I I I I actually am surprised so um my guess is IntelliJ has not been updated to recognize so this error is
coming from IntelliJ saying I don't know what you're talking about I can't resolve huddle um it may just not have enough
information but it looks like it worked so cool number registered I love how like the the feel that has the shortest
piece of information basically a a number which will actually be a single digit number foreign yeah so the the
inspections that's that IntelliJ is doing are uh I bet that's a that's probably just a bug um it probably is although
I'm surprised at I would expect it to not understand name but I'm actually surprised that it doesn't understand huddle
because huddle I've defined here so that but it's playing it's complaining that I um I I would have expected it to to
maybe have an error on these but that it can't resolve that that is something else um seats to me sounds like so there's
a difference between seats available and seats taken uh uh so if you're gonna break a bit yeah and I know sometimes
IntelliJ will do this even for properly configured things and and sometimes it just seems like what time of day it is I
don't know yeah seat count doesn't help is that the seat taken or seat seat available I could have seat taken count but
why seats occupied but they're not occupied until you take them and you don't you don't occupy your seat until you're
actually in class maybe it's so hard I'm fine with number registered I don't mind the the length of uh yeah if we steal
all the seats then nobody can sit all right um so that is working surprisingly um and look we learned something we
learned that uh time Leaf apparently supports records okay so then uh let's do commit um dashboard displays huddles holy
cow the stream's almost over what time is it oh my gosh it's almost four o'clock uh let's see what else we can get done
before I end um although I can go a little longer than my plan time um what I want to do next let's go to our that uh so
we probably want to is there anything else we want to add to the session sorry huddle um they've got name daytime number
of people registered we've got that and so now we have participants so let's go and so that will be uh how much do I
want to assert here in this test I don't think I want to assert there's probably going to be some stuff that this that
I'll modify in this test for like well how did that huddle get in there but for now that's fine so let's go to um a list
of participants um yes no yes what do I want right okay so let's go ahead and create this as another record and you keep
insisting on the test directory why why uh so what we want for this is um uh uh get get hub foreign and Discord user
name now his username user uppercase n or is I don't know I'll leave it uh the government game data so I wrote a game
for a game jam and now I'm planning to publish it on Steam and I put together a loose schedule I'm currently refactoring
the post Jam code because it's a Jam game and it got messy many of my stream viewers are bewildered because they've seen
many games develop but never ever factored I bet they're confused yeah it kind of feels like it is username isn't it
okay um and now this new to group do I actually need I told it to leave in same Source route and it's considering same
Source route so apparently leave and say same Source um they stay new to them up they stay new to my um basically is
this the first uh once they've participated in a mob they're no longer new but I need to see that because I need to uh
do do slightly different things if they've never been part of the mob so for example if you the grumpy Game Dev were to
be in a mob you would be new to my mob huddles um and I'd need to to do some special stuff exactly unlike fight club
though we do we do talk about mobbing all right and this is gonna fail uh not compile uh so that's that and then we're
gonna just say a list of new participants that's going to get ugly fast so let's pull this out to participants and then
technically this is participants size now here we can do a new participant and what do we need here we need a full name
the grumpy Game Dev and this is the advantage of using full name instead of the freaking separate first and last names
sorry pet peeve of mine that so many systems are created despite the fact that that we should know better around how
people refer to themselves and stop asking for first and last name uh GitHub username I don't know I will get that
information at some point but I don't know what it is offhand um do we have a driver and Navigator uh uh or just driver
no we have a typist and a navigator although I'm trying to figure out another name for a navigator I was thinking
director um but I'm not Comfort somebody else suggested the word typist and I like it much better than driver because
drivers are still making decisions and I want to make really clear that typists are not uh hey if you're willing to tell
me what your GitHub username is then uh let's see email I'm not gonna say email I'm not going to docs you uh grumpy Game
Dev I am open to other names um because Navigator sort of loses its I'll think about that I'm not so sure about that I
like the idea of of the hands though I was thinking of calling typist a robot but I don't know well well we'll we'll
have to brainstorm on that a bit more okay um so now that we've got this this is um see Actually I don't even need this
what am I doing the this dashboard view is not going to show the participants on this screen well hmm so the question is
do I want to just display the list of huddles and then I click into them and see the details on a huddle or do I want to
see all the all the details for all the huddles um I think this should be the summary and then uh I should have a
separate endpoint for the details on a specific huddle yeah all right well I'm glad I figured that out now instead of
writing a whole bunch of code for that um so this is really huddle summary then that View these are views I have not
been naming them as such um I think it would be more clear if I do okay um still called huddles we still have the same
information so that hasn't changed and this is three okay so that means we'll have a different endpoint um so dashboard
shows the summaries and then we'll have a dashboard will be um this will be the last thing we do we'll leave ourselves
with a failing test let me make sure the tests pass I don't I would like to run it why okay this is intellij's fault for
not reading my mind it knew I wanted to run the tests why so let's do a commit um I'm not going to add participant yet
uh what did we change here oh we just renamed stuff yeah all right so then we'll um create a failing test we'll leave
with a failing test and then that'll be it for for today's stream so we want a new endpoint so that's going uh this is
going to be get of huddle detail endpoint returns 200 okay so I'm not going to be super form got uh puddle and expect
status is okay foreign so this will most certainly fail with a 404 and it does um and we'll probably have to do a bit a
bit more testing here because we're going to have to come up with IDs and things like that so we'll do that next time um
so let's make sure we take notes on so at that point we'll probably introduce an identifier for huddle um no we won't
need identifiers yet for participants but we'll need it need those not too far in the distant future um sort of into
your eye uh uh once we have IDs for huddles so huddles or aggregates in domain your own design terms a huddle will be an
Aggregate and aggregate of participants um so they'll have IDs will then be able to create a huddle repository to store
our huddles um we'll need to create a service uh once we get to creating a new huddle we'll probably need to create a
service there um but probably I can get away without it until then so I think that's that's that's good enough for now
uh even though it's a failing test all right here rock thanks for thanks for hanging out um so we'll do a raid uh in a
bit once I I'll do a push so that way if anybody wants to look at that code they can certainly do so thank you Vector
Loaf
