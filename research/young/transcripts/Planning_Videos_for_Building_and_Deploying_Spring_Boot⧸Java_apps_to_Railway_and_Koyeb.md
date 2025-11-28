# Planning Videos for Building and Deploying Spring Boot⧸Java apps to Railway and Koyeb

**Video URL:** https://www.youtube.com/watch?v=KqTZHgTFNZY

---

## Transcript

all right hello folks welcome to uh a solo stream uh today is not going to be my usual working on ensembl or something
like that uh what I want to do is put together a couple of videos based on uh some of the stuff I've been doing and
learning from uh deploying some apps doing some uh GitHub action build checks um maybe some native image stuff so sort
of putting all that together into um basically some good useful Baseline uh ways of uh building and deploying your apps
is sort of what I would consider a good start for an app that you're going to deploy um anywhere but specifically on on
to two Services one is Railway the other is coab these are platforms as a service so what sometimes referred to as a
pass uh Heroku is sort of the prototypical um example of that since they've been around the longest uh Heroku though has
gotten expensive um and certainly for sort of hobbyists like it's expensive but worth it if you have the need for it but
some of these um newer services like Railway and coab uh are much more suited for smaller apps that don't need the um
you know you get what you pay for so Heroku is certainly generally more reliable um but you pay for that uh they do have
a lot more services and things like that um but if you don't need all those if you don't need um some some of its
features Railway and coab are a couple of good examples of their still passes you don't have have to wire up networking
and load balancers and all that lowlevel stuff you get to work at a higher level um I certainly appreciate the the need
for some of you know you need when you need more control and then you want something like an AWS or Azure but um a lot
of times you don't especially if you're working on um which might consider hobby projects or basically non-critical
projects is really the way I think about it because there's lots of small projects some of which we might do is sort of
you know uh our own you know fill our own needs scratch our own itch as it were um but a lot of times there's I remember
building you know a handful of apps working in a company that were used only inside the company and they weren't Mission
critical they were you know they were basically tools that made it easier to do things um and kept track of things uh
but they were only used by the people working for the the company and so it was a lot lower sort of level of
requirements for you know no real scalability you know even though we might have had a thousand people accessing it
they're not all accessing it within the same second uh so those thousand people are Spread spread across days and weeks
um and so there's lots of times when we want a tool um you know where uh we don't need the level of scale reliability
and expense that that some of the other places uh offer we just need some way to get it to deploy it so everybody can
access it um if you're working for a really large company you probably have stuff internally that you could do do that
with but um lots of times you just want to say I want to make this available to the net or maybe it's something for your
company that's available to your end users um either way it's really about uh I want to get this thing deployed I don't
want to deal with with managing the sort of upkeep of that but there are some things that you want to do in order to
make that a smooth process and so uh what I'm going to be working on stream today is basically planning planning out uh
those videos and then separately I'm I'm going to record those videos and get those up onto YouTube um so let's see let
me bring up where is M and just so you know um feel free to interrupt with any questions I'm not recording this for I'm
I mean I'm recording this but I'm not recording this uh this isn't going to go into the uh into the video this is all
just prep work so feel free to ask questions as long as they're tangentially related to to Java spring boot or or test
driven development they're all a fair game code so um these are build and build and deply I always type deply like it's
reply but with a d uh and so there's two parts um there's building which there's not a lot there for these types of apps
um mainly there's uh sort actions and there's uh Native uh image and so related to that then is maybe you know Docker
the docker file so these are all kind of how do I build um then obviously then there's a deploy uh if you've got your
build stuff set up nicely um then the deploy is you push to get help uh so pretty much the the the the parts to know
about are sort of you know what's available on on Railway and what's what's available on coab a little bit about how
those Services work this so building and deploying to a pass that's what we're doing here uh let me this basically let's
call it two parts um specifying the jdk that you're going to use uh and then there's uh the gold command so if we take a
look at what that looks like uh where is my let's close that uh that's for later um what am I looking for oh yeah the
GitHub action like what am I looking there's there's probably one other part which is is basically when to run the
action um here in this build file I basically specified whenever you pushed anywhere since I generally only push to
trunk um or main or Master whatever you call it uh I don't since these are sort of my projects nobody else contributes
to them um but even if so I'm just still going to do everything uh and then there are the jobs and it's basically the
build and the build includes sort of the build and and uh and and and test and verify which is where it gets the name
from um so there specifying sort of what it uh and I basically have it set up for Java 21 but some of the things we'll
see is if you want you could do against what's called a matrix of different um jdks if you care about that but I'm
really trying to keep this simple Because unless you have a reason to be like if you're supplying a library then sure
you're going to want to run on a matrix of different jdks make sure you're compatible in some way uh but theide here is
this is a bespoke application right this is a custom application again whether it's a hobby project or something
internal to to a company uh you know which version of java you want and you likely want the latest one uh so you get all
sorts of good stuff with jdk 21 and come and with jk22 coming up is so I like to use The Cutting Edge not all the time
but I like to use some of the stuff that is considered preview so uh in case you're not familiar one of the things that
um Java has been doing when they move to a more frequent uh release cycle is they now sort of when they're thinking of
adding or changing something in the language or the jdk or the jdk they put it out as is either an incubator or then a
preview and sometimes it gets reviewed so it's not officially in the language so anything marked preview could disappear
to you know the next release um that rarely happens usually what happens is it gets modified or adjusted in some way
based on feedback uh and so I like to use the preview features because I like to then offer feedback um so Java 21 um
the preview feature one of them is is uh what's called an unnamed variable and I think they changed that recently
because in 22 that's going to be called some I'm not sure they Chang the names of some of these things the idea is
sometimes you want you have a variable that you want to ignore uh let's look at an go and do I have it open here yeah uh
and so this is in combination with a bunch of other preview stuff so here um we've got fancy stuff that is in recent
Java is we're switching on this event and then we're going to do something based on that event so this event uh is a
player account event and there are a bunch of implementations of that so there are these five different implementations
um so here we're using a whole bunch of stuff uh we're using um the sealed a sealed interface with permits uh so we have
defined at compile time which implementations exist which means this switch event notice there's no default call through
because we don't need one uh and in fact if I remove one the compiler is going to complain saying values so so this is
the the fancy switch statement with sort of a closed World um this works for enums as well uh and this is a record umet
what they call it I mean it's a record pattern um and the idea is so these events are record objects and this the
specific event has two pieces of information it has the payout and some other piece of information turns out we don't
need that information um which is the player outcome because for calculating this thing we only care about about the
amount hey there dudan and so because I don't care uh we can use this underscore um underscore has been dis allowed as
an actual variable name uh it used to be allowed before Java 9 and then Java 9 said nope don't do that I think it was a
warning at first and then became an error and now uh and they did that knowing that they were going to do something like
this so here this is sort of the shortest possible way to say there's a value here I don't care what it is I'm not going
to use it and you could just say ignored like that um and it's other the type player outcome but like I'm not using this
so this is why people why some people dislike job it's like oh that's over Bose why it's like well okay I can replace
that with this and now it's less for Bose and therefore uh Hey tkes going well so that's um that's one of the preview
features uh because that is has not been finalized yet um so instead of actually having put a variable and give it some
name when you're going to ignore it anyway this allows you to just completely get rid of that and here um player lost
game I don't care about the object itself at all because we don't do anything as a result so it's it's another way of
basically saying there's a value that I need to put here but I'm not going to use it don't bother me with it what's the
least number of characters I can type to tell you that it's there but I don't care about it and that's the underscore um
and so this is all under the the the 456 let's see uh 443 was the preview yes so 443 is the preview uh so in Java 21 if
you turn on enable preview then you can use this feature um and so these are unnamed patterns and variables so basically
the the unnamed this is well they do have a name it's just called underscore uh and then it is now finalized so in Java
in jk22 this has now been finalized but if you want to use it in jdk 21 you have to turn on the enable preview why I'm
mentioning this is um all about uh when you set up your jdk and you build um you might have to if if you want to deploy
with a preview feature that's you're totally allowed to do that but you'd have to do some uh you again have to sort of
turn on that that ability um so one thing about preview features uh is that you just have to be careful um that the next
release again sort of might take it away or change it in a way that you'll have to change your code um but it's not to
say that it's low quality not like it's Alpha level quality and and might break I mean that's always true but they put
preview stuff through the same general process of of QA and so on it's just that it's more um we think this is the way
it should work um but we want real people to use it in real Cod bases yeah dud I mean there's there's a lot of these
small features that are just sometimes times you know a little bit of syntactic sugar makes makes the the the cat
tastier um and so that's uh that and the record patterns um so the unnamed variables and patterns be will become an
actual release so you won't have it's not a preview feature anymore as of jk22 uh and by the way if you're not familiar
with the the Jeep site and you're like a Java developer they are not always easy to read but they're not to the level of
like the Java language specification which takes a while to figure out how to read um and so I think it's really useful
to look at them and see you know what are these features that are coming up so for example um the record patterns and
pattern matching for switch those are final right those were released in 21 so 21 was was really you know most folks
consider consider this one of the biggest releases some say of all time I don't think of all time um but I think it's
certainly one of the biggest releases since since Java Java 8 uh tkes asks about web assembly um I don't know uh web
assembly has been talked about as as as a compile Target for for things maybe there's value there um I know cotlin has a
way to to to to do that uh there are some tools that will Target that Java I I have to admit my bias is I've been burned
by that's kind of stuff before um and have ended up having to basically trash a whole bunch of code and and and redo
things so I don't I don't fully understand why people would um I I I just find like that kind of compiling to something
that runs inside browser I've yet to be convinced that that it's sort of worth it hey o uh yeah something something gw2
I one of the things that I like about sort of you know for better for worse JavaScript is it's JavaScript and it runs in
the browser and there are tools to develop it and edit it and and and natural language that that the browser speaks um
anyway so I don't know I I I I don't think we're there um and I I I I would personally want to have a compelling reason
to to to go that that way hey Chris Quant yeah cotland didn't didn't kill Java um and one thing I you know if you're
doing Android you're probably going to want to use cin but for everything else like yes there's there's still you know
probably the big things are nullability like that's something that cotlin has that in terms of you know no nulls unless
you're very explicit about it um Java you know will it ever get there I don't know it's hard to do uh there's some
efforts there's the J specify before think it's JS specify dodev yeah um and so these are there's some stuff around
static analysis uh but in terms of sort of getting better at being concise and less verbose you know step by step
release by uh D me ask does a jet in open jdk map to Something in the or so there's no difference between the Oracle jdk
and the open jdk um Oracle is just an you know is just another set of folks who are compiling what's generally the same
source code um so that you're not GNA so there's there's the standard which is the jdk so there are standards for um the
language specification and the jdk's specification and anything that is a Java basically jdk has to go through a
compatibility test and Oracle goes through that just like everybody else um and if you pass that you are compatible and
so there's nothing there's nothing specific to there's no language features that are specific to Oracle implementation
cuz Oracle else's and so while Oracle is kind of The Shepherd of the language um that's that's their main job yeah and
so you'll see a lot of you know a lot of these written by Brian getts who's who's one of the main Architects um if you
ever you know if you haven't seen a talk by him you should watch and Talks by him he's really good uh just you know
comes across as a as a as just a down toe but like explains the stuff and you know he gets asked I'm sure some of the
questions over and over again and and he just you know takes that in stride um so all these jeets go through a process
but once they're basically uh accepted uh and and delivered they're part of the language um so yeah uh Tes my country
zero cotland base St yeah there's there's I have not come across a lot of backend cotlin stuff there is I know there
people doing it I know there's people doing cotlin and spring boot which is really a nice combination um but I have not
seen the uptake in it since I first heard people doing that five six years ago so I don't think it's it's increasing all
that much in terms of backend development I think uh I think you know Java is is good enough and getting better um and
cotlin you know especially with virtual threads like some of the stuff that that cotlin has in terms of its it blink on
the name but there's some thread stuff that that concurrent SC stuff that basically acing kind of stuff and I I think
that that's just going to go away like I think the the whole reactive experiment and some of the Frameworks um like
spring I think virtual threads is going to take take care of 70% of the use cases that that filled um there's still
going to be some other cases around streaming data but I think a lot of the cases of I want to make sure I'm you know
I'm I'm responsive in not blocking uh you you generally don't almost don't have to worry about that anymore for a lot of
cases it's it's just there so anyway um that was a very long tangent into Jeeps I think it's useful for folks to to look
at it and read it and read about what's coming up you can um just go to openjdk dorg you can click on uh specific jdk
and see what's going to be in it so it's like hey what's going to be in jdk 22 that comes out in two months um so it it
gets released on on on March 19th we're currently in the we're just about hitting ramp down Phase 2 um so that means
pretty much the features are locked um so there's some stuff that is still in preview I'm bummed that um string
templates are still in preview because they're pretty cool um but we're getting another preview of that um structured
concurrency is in preview again it was in preview in 21 uh and I guess I just didn't get enough feedback so if you have
feedback give them feedback um My Hope Is that that one will be finalized in in jdk 23 uh scope values which is related
to the to the threading stuff is also in another preview uh this thing implic this is the new name implicitly declared
classes an instance main methods this is basically um meant for people who what they call onboarding on to Java how do
we get people like I remember teaching Java it's like you have to know here's your public class Main and you have to
write public static void main string array of arguments just remember that don't worry about what it means put your code
inside the main method um now you don't have to do that now you just basically write a main method that takes no
parameters and it and it can work without being inside of a class so that's kind of some of the main stuff that this is
aimed at is this on say would be nice if could just write test in Java and let AI generate code um you could uh you
still yeah you still have to write your tests in some language um jav is a perfectly fine language to write your tests
in uh I remain unconvinced that that's that that AI AKA machine learning and llms are are sufficient for that at this
point um but converting from java to cotland you can ask intellig to do that uh it'll it'll do a generally reasonable
job on on most of your code but um somebody still has to read and understand the code that's generated and and
troubleshoot it when when it doesn't work yes exactly jous like just type P psvm uh ignore all the CR write your code
here um now you don't have to do that uh and there's a few other things um like now you can just launch it directly you
don't even have to compile it uh so this is kind of the first step and and you know because there have been concerns
rightly so sort of from a market share point of view which you got to pay attention to um if you don't have have people
in University or coming out of University learning Java because they're learning another language that's easier to get
started in uh you're going to have fewer Java developers um so this is an attempt to issue oh tokes my take on desktop
Java well it is it's dead in the same way that desktop applications are dead lots of things that you used to have a
desktop application for uh you don't you are they are now web apps whether they should be I'm old I've been in this
business for for decades and I think there's a lot of crap um and it's not crap because people don't care it's crap
because it's very hard to write good responsive applications for the browser uh it would actually be easier to Target
Mac OS and windows as desktops but that's not what people buy um and the the problem with desktop apps is the update
problem uh and the security problem and other issues and so I wouldn't say that you know desktops are dead desktop apps
are dead or the Java desktop apps are dead they're just not as popular as they might have been at some point and I don't
know that they were ever really that popular I mean I worked on a team that created a desktop app back in 2003 um today
we wouldn't do it as a desktop app there would be no reason yes the UI was really nice um and we'd have to spend a lot
more work uh I don't know if it'd be more work but it would be different work uh to make it uh a web um it's one of
those you know uh I I get asked uh and maybe even two you passes it's like should I learn Java desktop it's like if you
want to build a desktop app you should learn it um but it's very unlikely you're going to find a job that app oh yeah
yes convert uh no let's just push a button and convert yeah VB do vb.net was very amenable to to sort of a conversion
because it sort of I don't know it I left I left most of my VB work behind around the VB6 time frame so the net stuff
was like this just looks like net with you know a bunch of Visual Basic syntax here and there but it's it really didn't
look like VB anymore oh and yes d d a minut unfortunately a lot of desktop apps apps are are web apps where we just ship
you the browser too and my experience with those is not great they are problematic um but I totally get it it's easier
especially if you also want to support being run in a browser that's that's easier to do crossplatform that way um than
than other ways and f z like have you not watched my stream before because I feel like I I I slam and and uh uh Spas all
the time for good reason I think in my experience nine times out of 10 you do not need an Spa you just need a good way
to generate HTML and a little bit of JavaScript sprinkled in um and at some point I'm going to be doing some HTM X on
stream uh but very much I think a lot of what's being done in in spas is because developers are bored and they want some
interesting um and fashion it is fashionable and has been fashionable for I don't know 10 years maybe to to do single
Plage applications ever since since angular came out uh but I I heavily am biased against single page applications
because I experience their basis because with a server side you know back end and just front end HTML where's your state
on the server with a single page application where your state client and server now you got to synchronize those now
you've got to distributed app um state is the biggest problem we've worse all right let me unwrap my my stack a bit uh
and get back to my main purpose uh which is building and deploying pass yeah oh yeah I'm I'm with you except I'm willing
to have a bit of JavaScript to make the UI a little bit nicer um even if it's just I'm leveraging uh somebody else who
wrote the JavaScript like HDMX uh because maybe I don't want to reload the entire page just to change one you know row
in a table but otherwise yeah I'm totally with you way easier to test way easier to work with um ends up being at least
in my experience faster uh the thing I hate the most is sitting there watching a page where they have these animated
things where it's like hey we're going to be loading some content here we're not ready yet because return instead you
could have just given front yeah eventually some of those absolutely you know I I would think that I'd want to see a lot
of that interactivity um in in the browser itself and not uh like it seems like to it feels like some of that effort has
stalled um but maybe that's just what it feels like because I know there's still some movement but uh Carson gr the the
author of HDMX I'm sure would would very much agree with that yeah Hotwire is is uh somewhat of the same idea um um it
certainly predates HTM X but the idea of of HTM x uh it's there's very much similarity and there's some some growing
number of tools to make it easy to do that with with spring Boot and I that let's say this quarter I won't say I
certainly won't say this month or next month but certainly this quarter uh so I was talking about enable preview when
you deploy um whether you want to do that or not that's totally up to you um I'm personally fine with it uh maybe if
it's not a hobby project if it's some internal tool maybe you don't want to do that um but one of the nice things is you
can specify whatever jdk you want so if you want to use jdk 2 you know the day comes out um especially in combination
with a Docker file you don't nobody yeah under fun zero it's it's true the the um the the testability of front-end code
because of the way it's written the way most people seem to write it um it definitely feels like testing takes takes a
back seat uh there are certainly people who very much care about designing and testing frontend code um but that does
not seem to be the thinking and so you don't design for testability it's not testable um people say well I can't test it
because it's you know display stuff it's like well if you have state and you're doing logic that um so what I wanted to
look up was uh Haven build enable preview so I think you'd have to specify that as a maven plug-in compiler um let's see
so here in my file I'm using Java 21 I am not using preview however in ensembl in uh it's file uh thought I had previe
maybe I'm not using preview features here either oh I know where I'm using it um here and so uh let's open up P yeah so
here um the shuf fire plug-in which runs the tests we've got enable preview and then uh the compiler with specifying 21
and enable preview so when we do a maven build um it's going to pay attention to these configuration settings as long as
these are set correctly then when you deploy it you're think uh oh you might have to enable preview when you run it do
you have to do embedded now I'm not sure have to try that so um so we definitely uh so I gota look I gota look at that
uh so mentions it's probably fine as long as it doesn't have business logic um yeah except what's business logic so I've
been burned by things that don't appear to be business logic uh but are things you can make mistakes about like
specifying the wrong name for something right it's basically a string that was misspelled and it doesn't match something
else you might not be writing the logic but some way or something is evaluating that logic and if it doesn't match with
something else uh so it's it's a little bit of a a a a tricky question is is this logic so um but still that doesn't
mean out yeah I agree under fun Zer I I it make it it makes it makes me sad um because I feel like there's so much
effort being written that is is actually worse you know it's it's a train it's heading off a cliff and maybe it's
already fallen off the cliff and there's just nothing you can do to nothing you can do to stop it except just say can we
not be that can we not do that can we try something else um but yeah I you know developers are going to be doing and
attracted to complexity uh I always say look for the complexity in the domain not on the technical side keep things
boring simple on the implementation side focus on the domain um I want to try this while I'm here uh so let's go ahead
and build this line so we're going to do a clean um verify I don't have to quite I could do package but I may as well do
yeah I guess I could have done a skip tests uh because I know they are test failures because we're in the middle of
developing something this is from our from my Ensemble uh so let's do a skip test folks don't do this at home don't skip
test because it fail I'm doing this on purpose I know what I'm doing I'm a professional okay so if we do a Java
blackjack no manifest no manifest H H oh CU I'm not they're not building what confused it might be that this this State
okay that looks odd because jar I haven't run I actually haven't built this and run it from the command line I'm not
going to play around with this project because I'm not sure what state it's in so let me go back to my format hero
project which is my simple project um and let's go into let's just go here and let's go ahead and create this as a as a
string what what's what's I got a unreachable that so uh put there so what's complaining level that's fine we're doing
nonsense anyway um so now we need to go into our pal file uh uh oh look thank you intell so when I told intell to do
that um I remember it used to just go and update its internal settings for the project but now it went in and said you'
re going to need to turn on the enable compile so I probably did that there uh I don't think it needed it here so if if
we uh if we run the application it work yeah that's fine uh but what I before Why didn't it do that did I not have the
spring boot Maven plugin so what was missing before is it built the jar but then what with because it was it's a spring
app the spring boot maving plugin comes along and repackages it so now if I do uh and that's not our Target uh unexpect
unexpectedly expected expected as expected um we need to run with enable that uh do I do that first let's try it here
without the okay so yeah so enable preview is what we want okay I was hoping there was a shorthand version i v but it's
all long long hand version that's fine okay so now we know working oh because I don't have the spring boot plugin this
is what happens when you never actually deploy an application so this this code is we've been working on for a few years
but it's mainly um for for learning stuff we don't actually deploy the app um and so therefore it's never actually been
Deployable that's kind of funny uh so that because we should at least make it Deployable so let's go and stick that as a
plugin up now um oops we do that now I expect to see a repackage happen yes there's the repackage all right awesome yeah
right if you don't want bug I mean this this this defined system administrators for decades we like the way the system
is operating it's working can you please not deploy anything new because then we work all right um so now I expect if I
jar um I expect this to fail because we're using preview features what's interesting is we won't run into the preview
interesting is it's not like it's checking there's not some so when you compile with a new with a newer version of the
Java compiler um when there's a sufficient change they change What's called the class file version which means if you
have something that's newer than the jvm you're trying to run it on so if you try to compile on jdk 21 and you try to
run it on like jdk11 that ain't going to work it's going to say it can't but here it's still the same version of the
class file and I haven't hit the code that um executes I haven't hit the code that's using the preview featur so
therefore it's it's running fine without the enabled preview so this wouldn't have helped me discover that anyway but
hey now it's compile uh buildable and Deployable um I'm G to grab this plugin because I do tests right so the tests are
now failing because the tests are running the test requires enable preview so I think we can fix that with that I don't
even need to package it I it all right so that looks good good all right um so enable preview uh so setting up Tom both
for the uh Maven compiler uh and for the maven not manen Maven Shu fire plugin uh and then uh it these are two dashes
but they're not the I know this is getting a little I don't know why I'm bothering doing this oh look On's popped up on
my other with there we go do we like the slab with the serfs or without with without with kind of like the width all
right um yeah that's actually all I want to say all right so uh that is for the enable preview um so our GitHub action
is this yaml file uh and this is kind of the minimal one you want and this goes into the GitHub workflows here is it
workflow or workflows close um GitHub actions so what this looks like in actions uh these are the workflow runs this is
the specific workflow but that's only workflow I've got uh and it tells you what the file is here and so if you click on
it will actually take you right to the file um when it just shows it to you it shows you to you the typical way but if
you edit it uh it actually goes into a slightly different editor where um it's got some stuff so if you you can add on
some other uh some other so what I think is is a little bit confusing is this file is a workflow file it's under actions
but it's a workflow each individual thing so one of these steps is an action so this is an action this is an action uh
and then this is an action so the workflow consists of you got checkout uh you got um actions they quality interesting
could could do like an auto format so there a bunch of things we I don't know if does sonar some other stuff there you
can put that in U but we're talking about sort of a minimal thing so um when you commit uh so when to run the on Section
push one else um but you can also specify branches uh so one of the things you can do is control uh what do I want
Branch I actually forgot what this is um help and for better for worse in my opinion way yaml um but this is the main
documentation so let's go ahead and add that that uh this is right so we can do on push oh I guess I could put that on a
single row let's format it that way that push turns out in yaml if you do it on the next line indented then it's
basically a parameter to the first one I don't like that but Fork uh the filters is what I was interested in Branch see
right so on push branches you can specify Main and then basically anything under releases not sure why you'd want to do
it when whatever it pull request and so what you can do is you can set up separate actions to run um separate really
separate you can have SE separate entirely separate workflows that run on different situations so you can run for
example lint analysis and sonar Cube on a pull request um but then when you push to master you're going to assume that
all that's done and then you can just run the the the tests um so that's sort of just what's possible uh but my example
is is much simpler than that again because is we're talking about uh a tool that that only has one one or very few
people working on it if you're working on it you're hopefully working on suble so that's one to run uh and then um the
build and test command um finding build um and what that looks like is action this is an step all right so that's that
file this uh this is something that you want to execute that could fail so this so what verify does is it is it
basically does uh compile test package does do does tests and then ver and then verify it doesn't do a package because
we don't want we don't need the artifact um verify just is an additional step on to after after test that runs any uh
non basically tests that are outside the standard Source main tests sometimes uh integration tests some folks put them
in a separate directory and so that's what what what those would be so like if you're running like selenium tests or
something like that so verify just make sure they're all they're all run um and so the the checkout basically just
checks out your your code uh this sets up Java with this version and this distribution um and we're using Maven so we
want Maven to cash and this is very nice because it'll figure out by default all the caching stuff so uh if you're
constantly rebuilding your project it won't take as long as as the first time because the first time unless dependencies
change so dependencies you see that here in our run let's changes actions yeah so you can see here it ran in 2 minutes
and 48 seconds um most of that time was downloading the dependencies that this project uses from there on it's cached
and so it only takes 28 to 25 to 30 seconds to actually load the cache check out the project load the cache and and run
the build so if we look at um this one we look at the specific log output we can part uh we're basically downloading I
should turn off the downloading I don't know that we need to see that parameter what does B mean again batch mode yeah
so you want to be in batch mode but I think we also want to turn off no TR I think we want to turn off transfer progress
it just fills up the logs um let's do that as well uh and I'm going to change the dasb to das batch mode because I like
the longer arguments so um let's do that and then uh let's go ahead and push that and we're only going to push that I
want this no I don't want to push that so say um let's go ahead commit and push and push and then we will see not here
not here not here uh we will see here in progress since the main stuff is cached we won't see the transfer progress
it'll just be for next time so this fine and so you'll notice uh here where is it no not here here yeah so this is the
cache key um but since this was the hit originally up front when it did the test um actually I might have done it before
that yeah so here's the cash restored uh so basically here's the cash it grabbed the cash cash was restored um this was
the key used for that uh and the cach was about 51 uh 51 yeah get up light mode versus dark mode it's funny that these
logs are in dark mode I kind of find that actually a little little hilarious uh although that's like terminal is one of
the only things that I that I stick to dark mode um just somehow terminals are are dark mode terminals were always dark
mode for me because I use Terminals and that's all they were um let's see so I think that's that uh and so that so
basically we see the caching um here uh and so since it cached it it's obviously much faster then it ran the tests and
that'll uh built and then ran the test that was successful I guess ran the test and then built the jar um and that was
successful and so then uh it was all available and so then what happens is a result and this is where we're going to now
get on to uh now that we're done with the building part so this is this is not necessary I mean you could not have this
and so that means when you if you just you know are like me and uh you just push to main or push the trunk or Master
whatever you want to call it uh then whatever system you have this hooked up with your GitHub whether it's Railway coab
or something else we'll pick that up and then then deploy it um but this is it's good to have this this is takes almost
no time right 20 25 maybe maybe longer depending on how long your tests run but hopefully they don't run too long um so
maybe a couple of minutes uh but that way you're making sure that what got pushed is actually at least passing your
tests um in my experience it's not it's it's you know even if it happens one times out of 50 where I oops I push
something that that I shouldn't have uh it's good good to have that back stop for me though the the errors usually
happen in in configuration like I've left off an environment variable uh at at the pass level and so um never that I
it's almost never that I have a failing test that I've pushed it's or something broken because and a test would have
caught or even just something broken usually it's I've messed up configuration all right and so then on Railway we look
at it we see um and if we caught it earlier we would have seen it building because it passed uh so we've got settings
where it is check Suites and so this is where it looks at the GitHub actions uh make sure that they completed
successfully and only then will'll go ahead and and do the deployment and so this deployment we can look at it uh here
we can look at the build logs um and so this is building using um and boy am I glad I turned off the the transfer
progress because that makes this log so much shorter so here um so one of the advantages of using a pass uh is that you
don't have to set up very much um I used to deploy onto Railway and rely on what what are called build packs which is
basically you give it the maven command to run it runs the maven command builds the jar all right so basically um so
there's actually this is uh this is actually pre-build so I'm um I don't want to call it continuous integration because
that's that's a process not a not a tool I'm just going um let's call it that and so this belongs actually to um there
are basically three different uh there's the Uber fat jar which is what you get when you do a maven package um there's a
Docker file where it will this is a Docker image that you can this is native image that can only run on whatever
platform you compiled it on um in a sense the native image I guess is sort of a subset of Docker file you can just
directly build a native image uh but from a deployment you so why did it like that before learn spelling um so that
might be useful if you are deploying to somewhere uh and you have a place to store your image um but really you could
just use the docker file uh and so sort of both of these um let the past build for you so I'm going to take both of
these here hey there uh C marrat uh what's my opinions for hyperskill I am not sure I is sounds familiar you'll have to
remind me what that is I think I might have an opinion but I want to make sure I'm talking about the right thing um so
we could build a native image this um but again we're talking about I want to deploy onto Railway or quab so I this so
both of these are passes their um Railway is a little bit I would say further along the cycle um so has uh production
ready database support expensive even aoku still um see yeah I guess I don't I have I haven't uh okay so it's the Jeet
brains Academy stuff um it probably good uh but that's just a total guess um I don't I don't have I guess I don't have
any opinions on on hypers skll because I haven't I haven't looked at it deeply it's probably something I should look at
intellig so uh C is mature uh just I don't know what the um here I wonder how long coab is going to have a free tier
because Railway went through that I see every one of these companies go through this free tier business um I think coab
does require a credit card uh but it's always dangerous as any kind of Provider of computation Services of which these
are uh for free it um so they have a free TI I have to are uh but you basically get um some minimal uh uh resources for
C virtual CPU RAM and dis first so this
is $5 a month um and you pay for any usage above pick really depends on what you need in addition to your application so it's likely um likely that you'll need a database you don't have to use one supplied by uh the past though like you could have your database deployed somewhere else um there are there are services that are just database only platforms um and that that that aren't from the big cloud providers uh you could use that in combination with your app you could not even bother to deploy it on a pass right you could deploy it onto a Raspberry Pi or you could apply it onto your local M machine um using something like you know anywhere from enro to any other tools that that provide access to your machine um but that's out of scope for for what we're talking about anyway so um then I think it's just a matter of so uh on Railway you basically create a new project so you create a new project and you choose um repo uh so do that um if you're not already hooked up it will require to go through the authorization process right so this gives permission for Railway and you'll do something similar with with coab to basically have access to your repository so it can actually project uh um one thing I want so I think I want to show app uh so deploy process for for no external database let's grab this and move that here and move that then one hey buer 64 thing that's interesting okay not sure what I'd use that for you more I guess you could deploy something elsewhere that connects resources interesting or is it manage I'm not sure what that's doing I'm I'm not a I'm not a terraform person so you'll have to tell me more there's a reason I use a pass I don't want to deal with with like real Cloud providers complicated all right so again the context of these videos this will probably be there'll probably be two videos um is you've got a project where it does not need the customization configuration and scalability and resources of something you typically deploy to a a traditional uh cloud provider so the minute I see terraform I'm like what's that for uh let's see so post Crest let's see uh so um trying to think of one of my apps access oh I see it's uh create a new Railway project get maybe that's useful I mean honestly this takes no effort and you do it once so unlike sort of redeploying things where you might change stuff I feels like now I got to learn terraform in order to do that that me like Railway already has templates so you could basically if you do something common like I'm always deploying this plus this in this way you can just deploy a template and and it does it for you so I am not I am I am not convinced that that this terraform Railway provider really does anything for me unless you are uh allergic to to web uis I I will admit the railway UI uh sort of in general feels a little bit under under engineered under thought out like there's some just like awkwardness but yeah so uh do we want to deploy it now could variables I'm not sure I even want to deploy it so let's back up um let's see my quiz down I don't think uses any database either so I will have to create some kind uh yeah I guess I could convert this project into storing stuff that um I mean I've already got the inmemory repository so I could convert I could take the final step and and uh and store that um this will work fine you'll basically and let's try this again so um what are I de playy that it okay good so it gave it another name fluffy crook which is great um and so pretty much once you once you hit uh depl now assuming everything works right no no build failures um then deploy so everything deployed fine now it's deployed uh so once it's built now available domain so now it's up and running and we um the details uh no the details just tells you about the see ah so I remember this the last time and I thought this was a little bit confusing is is um right now it's not available uh it's available internally um but we actually want to make it publicly available and look is spelled publicly the file an uh I totally get that typo you want to um we can uh generate a railway own those are the two we care about uh so we'll go ahead and have a generated not found ah there must have been a slight DeLay So now now it's up and go all right that's Tech um so that's it for for Railway uh let's go uh let's go turn off let's go delete this service otherwise we're going to be paying for it um there's a couple of things one is we can look at uh settings and we can set the service it we can do app sleeping that's still currently in beta um we can turn that on uh and that will basically turn it down to zero the service will still be there but if and if you hit it with some in input um it'll wake it um the one thing I found is that if the app accesses a database it feels like it seems like it's just always doing iio I have not been able to troubleshoot that yet to figure out what's going on is it the connection pool it feels like it's happening too frequently for the connection pool to be doing something so there's something going on where there actually is IO coming out of the application to the database but it's not actually doing work because so um so what we want to do is basically surface and now what it should do and this is the UI that that I'm like it should just take you back to the dashboard uh because it's here it's this empty project like there's no Services inside this project project so there's this relationship of project to services that might be a little confusing um here you can have the project without the service and you won't be charging anything because you only charge for running services but you may as well delete the project otherwise you're going have a whole bunch of them on this page um I should probably delete this one too I don't think this one has anything in it oh there no deploys for it uh because I removed that a while back um let me go ahead and gone truth um got yeah no I don't I don't think that's what's going on inside that would be terrible no it's it's something that um I need to run locally with like wire shark or something and figure out like what's it doing um because if it can't sleep an app that has a database that really sucks uh so what I'd like is like my ensembl app does not need to run 247 I'm paying for it to run 247 I can have it be less expensive by using less memory uh which I want to do with a native image cuz it does it doesn't even need 5002 um but uh but it' be nice if it it could then then I won't pay for it at all instead of just paying less uh all right so I think that's it for for the railway deploy so let's go ahead and look at coab uh let me run coab because one of the things I'm concerned about is doxing myself and providing and and showing my fine uh yes and I remember now what um what about what was confusing about has with what it calls an GitHub high quality chocolates I like high quality chocolates got to be high quality though and so here I've got the same app the format Hero app um what's interesting is this apparently is not Auto deploying because it was deployed 7 days ago um I just clearly uh Railway redeploy it recently app so it's got a single service it's pulling off of this Branch this is where it's deployed uh coab is I think uh they have two free regions um they used to have just one that was Frankfurt but I us though uh I don't want to add a domain yeah I so the UI are hard but I feel like neither Railway nor coab do a good job so like what I'm looking for here is where's the settings for when I upgrade when I push something new to GitHub you should grab it uh is that this cuz to me this looks like I'd be clicking and going to the repository but that's not what it does it actually goes the details of the app I find that confusing uh binary 64 asks what devops practices do you buy into I buy into devops as it was originally coined which is what netlix called you build you basically you code it do you build it do you run it um I don't 100 % buy into that in the sense that uh well I buy into it but there's there's there's some prerequisites for that I don't if if I were running a team I don't want them running kubernetes in the sense that that's not their responsibility when they say run it it means operate something but you have to have a proper mature uh operations platform if you're a startup sure uh in which case you're running everything and you're doing everything and you're managing everything um but if you uh have a team of any size and a company of any size you either Outsource that to some somebody like your cloud provider like a pass and there are larger ones than than these two um but otherwise uh you still want to have sres you still want to have folks who are you especially as you get you know but the sres should mostly be concerned with infrastructure I guess I'm more saying developers should not be aware that you're using kubernetes or not to deploy your applications now it'll depend also on the types of applications you're running but I find the widespread use and parent required knowledge of kubernetes to be offensive I think it is once again developers are attracted to complexity uh but it's it's for a lot of the apps they're deploying they need a pass and they already exist and I see over and over and over again companies redeveloping an internal pass cut it out you are not Netflix and so this the downside is is most compan are not Netflix they are not Uber they do not have 10,000 microservices nor should they um and so I see so much complexity uh pushed to developers developers should not should be tasked with operating things that are specific application um you can ship it and and kubernetes use cloud Foundry use you know use a a platform where they run the kubernetes so Cloud Foundry is a pass and it's a production level one that companies like Ford used to deploy their applications and it's very much like this pass so I think a lot of companies are trying to build their own pass it's not an eks it happens to use kubernetes but is completely opaque from a user you basically do a CF push just like you would do a get push here you do a CF push and it deploys it and so things that can go wrong there going to be two types of things that can go wrong the stuff around networking and storage and things like that that's your Sr team responsibility then there's there's a bug in the application that's your application team's responsibility uh and so there's still a clear dividing line um but the whole point of devops was to in a in response to S saying we don't want right this goes back to the earlier comment um stop changing the application because everything's working fine and and if you push more changes you're going to break production and it's like our job is to ship features so stop fighting me um and so there was this tension of SES don't want things to change and de developers only want things to change uh so we shifts a little a little bit of that responsibility saying okay you can ship stuff but you're for yeah I I I think yeah I'm sorry dud I and and I I I I understand your your your pain and it's like developers should not know that kubernetes is there they shouldn't know what it they shouldn't even know what a Helm template is they shouldn't know any of that stuff um not that they can't responsibility uh developers love complexity and we see kubernetes talked about lots of conferences so developers thinks that's important by ship it meaning they push a button to decide what gets pushed to production that's shipping I didn't say anything about about uh running like they don't run the hardware just like most companies don't run the hardware but unless they need to work with like again and this I'm talking about a midsize company that's got a bunch of teams that probably has 200 plus Engineers uh most of those developers kubernetes so they do they push it does continuous integration or more precisely it runs the build process runs the test process runs whatever quality uh checks you need it I don't have to know what kubernetes is to do that I was doing I was doing that before kubernetes existed and it was fine um and I see things going backwards with with kubernetes yes by ship it I mean you push the button to say this is this is ready to ship same way you'd produce a CD in the old days um and if that is just a push to to to master or merge with bastter or whatever it is you want to do um and you're running the the application right there's a clear and this is why devops is not a title it's not a group of of people it is the process it is developer working with Ops Ops does its job developers do their job but they're working together to continually deploy applications um again to go against what was happening and I still think it happens of your CIS admin saying stop shipping stuff we don't want to have to we we like things that are stable that's not the way businesses work or at least not the way they should work uh and so devops was a way to say let's work together to find ways where we can build new features without constantly breaking production um the idea that you throw throw something over the the the wall and it's up to to this administrations to figure out how to install it and run it it used to be like youd give them like a jar file or a tar file and they have to go install it on a machine and then they'd write scripts to do that um and that's what we're trying to get away wall all right so I was trying to figure out um how do I I guess that's settings uh choose your Builder um that's interesting why should I have to choose my out um so here this is interesting so here uh and I'm not quite sure I know Railway has support for Docker images I just haven't set it up where it would pull the docker image from somewhere else here I have it build a Docker image uh with a Docker file I want that to happen here too why do I have to choose the file let's open this up okay those are just overriding the settings so I guess if we select Docker file uh we want a web service we want Echo um and now I can deploy in Washington DC which is 100 millisecond closer in terms of latency so let's do that uh let's check the advanced stuff what we got here so we got environment variables got exposing the service I don't know why that's under Advance though okay I don't it's always interesting when when people put stuff under Advanced it's like what what do you actually mean by that so I don't consider these Advanced like you need some environment variables but whatever they're just extra um so we don't need anything there what I'm not seeing though is why changed so let's go to deployments did it try to deploy before no it didn't look I'm only using 122 Megs nothing yeah so I should probably explain build packs somewhere oh I I think I had it and I took it out because I'm not going to explain how to use build pack because I I no longer but I should explain it at uh so build packs are basically so ultimately all these services are deploying Docker images or let's let's say let's call them oci containers oci compatible containers um Docker image for short so they're all images that you can run with Docker um and so the question is is who defines how that image is built in structured so a build pack has everything you might need to deploy uh a language so for example for a spring boot app at runtime you need a jvm putting native image aside typically if you have a j file you're going to need a dangerous um and so build pack uh was sort of the easy way to do it because all you had to do is make sure that your jar file could be built and it would take care of providing a container image that already had the operating system and the jbm um but building that stuff is now easy like the docker file especially now with with and even multi-stage stuff is not new with the multi-stage docker file this is all you need um and the problem with build um is you don't have to image um and so this was a this was a this was a problem yeah they so I think when I first started doing passes I mean the Heroku came up with the idea of the build pack um or at least they certainly were user and when Heroku started Docker wasn't nearly as wide let's see Docker was what 2013 Heroku I think was older than that um so there was no container images uh or at least they weren't as Popin so build packs were way to have a package Deployable thing um uh and there wasn't anything else and so they created build packs now that Docker is is popular and it's easy to create a Docker image with the multi-stage builds I they're probably I think they're obsolete I I can't I've been trying to think of a reason ever since like somebody saidwell why don't should just use a Docker file um I want to use JK 21 when it's released and not 3 months later and in fact I'm not sure if Railway still has yet to deploy a build pack that supports Java 21 and it is now 4 months after it's been released um which is fine Java is certainly not their biggest target market but now if you have a Docker file who who the heck cares um just build a Docker file uh hey kuros uh I think coab uses firecracker micr VMS they support running Docker and the micro VM yeah and so these days Docker uh I don't know what Railway uses um but it's pretty much these days Docker images are are the thing and so what you want to ultimately have built is a Docker image and then the question is who builds it them or you it's more like who assembles it because um and so the docker file you know is is easy enough uh are people moving Docker to podman um I'm not actually running Docker I'm actually running orb deck so uh as long as you can you know read write and execute quote Docker containers which are basically oci right there's a standard for them um you could do what you know software uh you kubernetes and Docker files is the same yeah I don't I've built the kubernetes uh and it's doing way more than what Docker file does maybe you could compare it to Docker a path along the idea of I have multiple things I want to run and I want to yeah um I don't know much about podman I haven't I haven't used it I I basically switch to orb stack because uh it it seems to run better on on my Mac than than Docker does but it does everything I needed to do um to do I know the game done with Java Minecraft yes I have built Minecraft plugins and stuff back in the day when my son was born to Minecraft uh your follow on question um no it is not doing Minecraft development is is a painful tedious exercise that will make you hate Java so don't do that now I will say my experience is at least 6 years old so maybe it's gotten better uh but it was pretty awful um cuz it's a really old code base and now you're building stuff with apis and stuff on a on a really old code base and so maybe that's been cleaned up and improved um but boy I like I've been doing Java for 28 year 28 27 28 years and I struggled a lot because it was just terrible it was just terrible hey Lis gundu nice to see you um yeah I mean it it again maybe it's gotten better uh but I I I like got just enough done that my son was happy um but yeah was not was not fun all right so whoops um so I'm trying why why it's not autod deploying is it is it not Auto deploying because it tried and failed out see now I told it to be a Docker file oh did I not apply the changes oh shoot let me let's see if this work I have a feeling this might work because it's going to use it's going to ignore the docker file it's going to use the pom file it's going to build it with Maven so it detects that you have a pom file that's what the bill pack the code around their bill pack stuff does so it detects that you've got a pom file runs me even to build it um let's see so text your cradle does keep the right command um so I've got a palom file so let's see what happens point yeah orb stack should be wider known um so I'm glad I got one more person to look at it um uhoh I see red both clear there's some problem succeeded yeah I mean frankfurt's far for for electricity in packets but not that far I remember the last time I did this the the logs took a little bit of time um yes thank you there's an error uh but you're not going to tell me what it is are error there was an error we're just not is um so it's nice that at least like you know it left the old version up and running which is generally how they work they keep the old one running while they're building the new one then they deploy it and then they basically swap one well I may never see the log so let's go back to the service um so this is just a console on the instance that's working I don't want the instance that's working so let's go back to settings um let's change it to Docker file redeploy now logs succeeded so these logs are coming I logs all now so I had to force it to do a man I had to manually refresh the page that's a bit sketch uh so now the instance is healthy logs that's a little Annoying what if can I download them let's try and download them useful uh have I ever tried daku uh I've looked at it I've played with it but again it's like I don't want to I don't want to operate that at that level um so daku for or oroku I don't know how you're going to pronounce it uh is basically run your own Heroku um but then you're running it on you know maybe running it like on a digital ocean but I'd rather just I mean I could run the my Docker container on on there or I could just run a uh run it on a pass I mean I could see it if you're interested again sort of in a bit of a lower level um but that's sort of the but you know if I'm a team I I might want to be running that right again like I don't want the raw stuff that that you still have to do with like kubernetes I I don't want to deal with that it's not my job um I would like to know why I'm not getting my build logs though but at least the runtime is up and running it's healthy um so that is straightforward uh oh let me change the to Washington unfortunately I can't use the San Francisco's expensive I guess I should know I live here uh so let's change it to Washington is that going to cause a redeploy what's unfortunate and this is the downside of using a Docker file is if you redeploy it it has to rebuild the image and then deploy it as opposed to if you already had the image it could just immediately uh red basically just start the container so that's sort of the the slight downside I don't think it's much of a downside because your other option is you got to store the docker image somewhere and you got to pay for that and you got to pay for the it your sound the sound is not video not in sync locally it looks good problem and it could just be you well you won't have to suffer it much more Cu uh I got about 5 minutes before I got to go so let's see if this redeploy so let's see what else do I want to say about coab um I'll probably want to set up a new account so I can go through the process um so my mental model of of coab and and how it works is is not quite set yet so I need to sort of build that uh so I think that's going to be the a third video cuz I don't want to hold up the um so my goal for this stream was basically get sort of my plan for doing doing uh these as as videos that I'll uh upload onto YouTube so they'll be um focusing on the GitHub action showing what that's all about um setting that up creating that then there's the builds um uh I didn't cover the native image yet I think that's going to be a separate video too so mainly I'll be talking about let the past build it for you versus the build pack I'll talk about but I think video and then deploy that to railway um and then coab I think will be a separate video hey it's healthy can I see build logs maybe not I will have to file an issue as to why I can't see the build logs because I think important o no long a let's see they have no they're deploying a Docker image doing one thing I will say is generally the support from coab has been responsive uh Railway support has also been relatively responsive except for supporting Java 21 and build packs which they still don't support and have not and basically said use a Docker F which again I can understand but it happy um all right I will have the file an that cuz I really should see the logs I can see the runtime logs which is great logs are not I'm not sure why I'm not seeing the spring logs because I should be able to see so if I go to that app um but it's not showing me the runtime logs either these are not the logs these are just the events I wonder if it's having a problem with logs H uh yes tkes so coab has a free tier they have what are called Echo Eco Echo instances which are very tiny instances uh so let's see what are the what are the settings for the echo uh it's basically 0.1 of a virtual CPU so not a lot of CPU 52 Megs of RAM and 2 gigabytes of dis um that's free uh you can have one of those and it can only run in one of two places it can either run in Washington Frankfurt uh then there are the really cheap ones that you can you can run as many as you want you start paying for uh like the enano is um basically 0.22 cents for per hour so if we say uh 0.002 to 24 hours a day uh let's say 30 days a month it's basically $
150 uh $150 60 a month um the E micro the E small so you basically can you can pay for more but you basically so you get
the the the the echo one for free but you can only have one so it's great for sort of experimenting with but if you want
to really run something you're probably going to want to go up to the the standard level uh which is where now you're
starting to pay for right that's where the Nano starts um and then you can get more CPU if you need it so if you need a
little bit more CPU or a little bit more RAM you're probably probably talking at like the micro of the small level even
so like even the micro level uh or even let's say the small level 0.0144 so that's 10 bucks a month I mean if you've got
an app if it's a hobby probably you're not going to want to do that um but if it's maybe a tiny business or a tool you
use in your business or a tool that your team uses or something like that that you need deployed and you don't have
internal resources to deploy it onto um 10 bucks nothing so my estimated monthly cost is 268 uh oh cuz I didn't yeah so
if I select small then yeah look it calculates it for me um but Echo is nice because it's free or you can uh you don't
so I'm not quite sure exactly what the difference is um because you can have price I guess the echo ones are the ones
that start with an e is that right yeah so I'm not quite sure so there must be some other differences between Echo and
standard um than maybe you can't run the echo in certain regions ah so that's the other thing is okay so the echo um for
sure for economy uh can only run in a couple of different locations um standard can run anywhere that's the sense uh so
what's the average RAM usage of a spring boot app that's like saying what's the average RAM usage of any app there is
none it depends on the app um but you can you can get quite a lot done with with a half a gig of memory with a spring
boot app and you can absolutely use that's what the native image is uh use the grow VM um grow VM is sort of a misnomer
because it's not really a VM it basically is a compiler but anyway you can compile to a n native image to to use less
Ram yeah um so you can you can like my I mean not like my ensembl tool is is all that big um but you can you can run a
gig so so the free the Free level you don't get a lot of CPU so it's not going to run very fast um but you you'll have
enough RAM and uh yeah all right I think that's all I've got for today I think I've uh planned out my first couple of
videos um so I'll weekend can you make your app use constant memory though well you can if you're running if you're not
compiling to a native image if you're running the jbm you can just tell it you only have this much memory and only use
that much memory it may run out of memory but and might garbage collect more often but issue um but again it's there's
there's so many variables with how much memory application we use that it's impossible to to say without knowing about
the application all righty um That's all folks thanks for hanging out uh let's see my next scheduled stream at some
point this weekend I'll be doing some streams I'm not sure if it'll just be me or if it'll or if Mike and I will work on
the song themes app um as always if you're not part of the Discord you won't find out until the last minute uh one we're
going to uh stream next so join the Discord and not just join the Discord but also you will want to uh links so whoops
so there's a Rolls Channel and what you want to do is click on the coding stream alerts box and so then I basically I
don't ping everybody I just ping those who are interested in alerts uh and you'll get notified and usually I try to
announce sometimes it's not until half an hour before but I try to announce uh especially when I'm pairing streaming uh
at least a day day Advance all right thanks folks um thanks for hanging out thanks for the questions and discussion and
uh I will see you one
