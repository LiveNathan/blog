# Spring Boot： Upgrade, Native, and more with DaShaun Carter

**Video URL:** https://www.youtube.com/watch?v=cobLUktQbuY

---

## Transcript

all right hello folks uh those of you watching on YouTube Hello with a little delay and twitch perhaps with a little
less delay but hello folks uh I'm here with my good buddy Deshawn hey thanks for having me I'm I'm happy to be here I've
been looking forward to this the last one was so much fun and yeah yeah and it it seems like timing is right I've been
watching your shows it's fun I like having you on in the background yeah and lately I've been uh pairing with with a
friend of mine on a on a new app and so um I I sprung for the full or at least the next level up in in streamyard so I
can get the higher resolution and other stuff so now I'm eager to invite other other people on board but uh you're
always a favorite that's one of the the features of streamyard compared to what we might have done with OBS yeah with
streamyard just oh would you like like to come on and talk about what you're working on here's the link let me send it
to you and then they can just literally jump in the show if they've got a browser yeah there's there's stuff I miss from
OBS I'm a bit of a control freak but I'm trying to to not get too uh wrapped around that stuff like oh why can't I do
this why can't I push these things here and yeah other other things I have to to do differently but um but yeah it's
great for sort of uh bringing folks on without that person having to know that that that that Paradigm of I want to have
all the control and I do things a little bit different and I'm used to doing it this way but 90% of the stuff is done
the way you want it like what's the what's the value of this this 10% of I really wish I could do this versus the I can
pick up and I can start a show and I can invite people and I get all these other things good there is a tradeoff there
there's Jonas yes welcome there welcome and there's a trade-off there and I see people make that tradeoff towards the
the 10% is really important versus they're going to spend more time on working on that 10% than having 90% of the things
done and moving forward on the other things that they need to do there's I've seen that trade-off and that battle in
many many different ways uh on this software Journey yeah what what I'm swegi yeah what I'm hoping for is that they open
up some kind of API to make it possible to do some to do the things that I can do it's one it's it's funny it's like
there's things I can do just really trivially in O OBS like I want to add an image I want to add this thing I want to
add content over here that that I Define yeah so that uh that's what that's what I'm missing so hopefully they'll they'
ll get there like and I got really surprised with the layout editing the layout I was pleasantly surprised I wasn't
expecting it I was like oh okay that's okay uh but then they gave us the ability to to manage our layouts yeah um the
one thing that I think I'm missing is like the overlay like have an ability to to Overlay some HTML uh or web page like
that's the one thing that I I feel like I'm missing the most but everything else I'm I'm pretty good with yeah I'd like
have a little more control over some of the uh camera stuff um and being able to pull in like chat uh and I know that
they're limited by twitch that they can't support uh like I can comment and it'll go out to to both YouTube and twitch
guess it's only going to go out to YouTube because twitch doesn't support that's that and it's like okay yep can I
figure that out and well all right I guess I'll deal with that yeah so it's those those it's it's it's some of those
things where um I I miss them but but yeah the trade-off for for for being able to bring bring folks on yeah the multi
platform thing yeah yeah the multi streaming is the other thing like I can't from OBS unless I use another service like
a restream I can't my computer does not have the the bandwidth to to multistream in a way that uh basically that would
work reliably so yeah to handle the chat like this morning I realized that uh I'm pretty good about like hey somebody
does a chat and if I'm streaming multiple platforms I got to put it up on the screen so they can see that you know Jonas
is high yeah uh but my son my 10-year-old son was in here and he created some uh startup images and he's taking an
interest in it but then monitoring the chat and he was like oh so and so says this and he just pop it up I was like oh
so I didn't have to monitor the chat he's bring those messages up and yeah he was my that's your he's your producer
proder that's exactly what he was doing he didn't know what that meant but that's exactly what he was doing yeah hey
asid made it all right as's one one one of my big fans um well let's get let's get started so uh I put together a little
fell workspace um to keep track of what would I what do I need desa's help on um and so here's our list so uh we're
gonna do this and Des Sean's gonna help me because a lot of this stuff I don't know much about um at least when it gets
down to the implementation level theoretically conceptually sure uh some of it like the upgrad should be straightforward
but there's some related stuff so should we do metrics first yeah that metrics let's put it and working on so again I
don't know the uh dependencies so over in my screen I'm going to start doc.io and I'm going to create I'm just hitting
the dependencies and I'm looking for the Prometheus uh dependency and I think that's all that I need um I think that's
all that I need is if I go and I explore it oops we got a we both prefer Maven over Gradle yes uh it is called the
micrometer registry Prometheus and I can the group name is io. micrometer and the artifact ID is micrometer D registry
registry yep and then io. micrometer micrometer D registry D Prometheus group is IO micrometer iio do micrometer yep
okay updating yes there we go and that's it that's it so now if we start this application what that is doing uh you have
the actuator in you have the actor I do I do uh let me check what my uh what do I have exposed I've got Health info
metrics wonderful that's all we need all right uh yeah I think that's all we need uh we might um let me peek it might be
separate for the prome registry uh let me go just quick peek here um I did this oops fail to start C what did it not
like about running what does it say here yeah it ran uh I'm going to add one more um endend point to your uh line 21
there Health metrics I'm Prometheus what do we think why did this is host network mode um well let's make sure it's not
us uh let's comment out our Prometheus oh I didn't well I ran it before we haded the Prometheus uh oh but do we think
the dependency itself is a problem I think it should be but let's just make sure I don't think so either let's go back
just to be sure one of the things that I'm trying to do also is live inside of my IDE a little bit IDE huh all right
right so this is my default here I'm I'm fine with restarting stuff like I'm fine with like going um Docker you're you'
re acting funny let me go shut you down and start back up that looks fine I wonder what I expect I wonder I wonder
wonder which would be really bad so I don't use Docker I use orb stack okay I wonder well the database is getting
started uh let's stop it manually and restart I wonder if orb stack is something how incompatible has made itself
incompatible in some way what I I found myself saying this morning is I typically learn more when things don't go right
yeah it's no fun when when stuff goes right so yeah I get I'm comfortable when things are broken that's what things are
broken most of the time look at this uh I didn't get to read it all but yeah I love that you're upgrading yeah adding it
yes let's go like this is great oh good your calendar pop up this job great um yeah so and and of course I have you know
orb stack said hey let's upgrade this morning um so of course yeah what could possibly go wrong upgrade what could
possibly go wrong I do same thing so let's see these are in use uh running that's interesting that's interesting that
it's aware that ensembl is the thing that's talked to the database how did it know that so one of those things that I
worked on this week was I was pulling in a new library I wasn't sure that that new library worked I deliver all of my my
projects to uh raspberry pies so I build the native images and I pulled in a new library that I hadn't used before and
when things didn't work in the native image things didn't work but my tests were passing right my unit tests were all
passing so I was like how come this isn't working and I my default response you know my gut was like oh I wonder if that
library is using reflection or something or proxies and it's not compatible with aot processing it can't it doesn't have
the metad I needed for GR VM so what I did was I I made an integration test that builds my project run all the unit
tests and then if I want I can run this integration test that actually generates a native image so I can run my tests
against it but I'm using test containers right so I got stuck on how do I get this native image to load up this test
container for redus how do I how do I make that happen how do I feed the property I can't use a service connector
because it's in an image it's image to image so I'm not like feeding something out into my unit test how did I get how
could I get this aot native image to talk to my test containers how do I give it the right properties and how do I get
them to to see each other in the same network uh and you know I got stuck and I was like oh I don't know Jonas was there
I said hey here's what we're trying to do we knew kind of what we wanted to do but we didn't know the the language we
didn't know what methods we need to call or what we need to do so I reached out to Ole uh from test containers and you
know it it was maybe like 15 minutes I might have taken a break and I sent him a message 20 minutes later after I sent
him a message he sends me a repository he's like hey I know exactly what you're doing here's what you need to do so then
I I separated out my jbm test test the my normal unit tests I put those into an abstract class I extended them for the
jvm and then I took the exact same class and I extended that same abstract to use it with the native image yep but I got
it so that builds a native image uses the same test container the exact same way give a different port for rest assured
to know which port to use but it's connecting the exact same way and everything's passing so at that point I knew that
my my native image is going to work the same way as my jvm image and the problem was somewhere else and it was with my
reddis configs uh when I got to production but it was cool that The Ensemble knowing that hey here's the post uh the way
I set it up as I defined a new network and here's the network that we're going to use for this test so use that same
network when you deploy that native image so you can see that there's a redic instance there and you can just call it by
its name you give it an alias and you can call it Reedus so that that issue what I just saw with the ensembl seeing that
postr was running I saw that same thing see if or anything orb stack no nothing least known let's see um so is this repo
can I get to this repo uh you can yes uh let me give you the I'll play I'll put it here in chat so everybody can see it
because it's GitHub on someware fantastic so what I'm GNA do is I'm gonna go and I'll pull down the same thing and we'll
see do I get the same behavior this is kind of a default right yeah I was I was gonna I was gonna see if I can downgrade
um my orb stack uh because I don't know if I want to spend too much time sitting in the debugger into if if I wasn't
streaming I might spend an hour doing that but I'm not gonna but yeah we'll see here I'm gonna do I use a GitHub client
I'm G do GH repo clone Ted on so where does it get inspect response from here inspected inspected has size of one and
I'm pulling up I have Docker running not orbac so I'm just going to pull it up and see if I can make it run I'm going
try to stay inside of my has that oh that's interesting so the PS response ID it got was the oh so when it did a Docker
PS it got this short ID yep which is a prefix for the full ID which is why it didn't find if didn't find it in the in
the map because itn't doesn't match I think that's a bug somewhere I don't know if that's a bug in the expectation of uh
default not supposed to provide a full ID I'm on so how did it get well like you know from C I can give it the short or
the long right the API should allow me to do both yeah so wa ran run compose stream filter run compose so that start up
the compose and then it got the running responses that is interesting yes if you don't know evaluate expression evaluate
expression like it's funny like because I do tdd most of the time the only time I'm sitting in the debugger is when
doing this when I'm trying to figure out spring or or some other library or framework I don't do it on my own I rarely
do it on my own code um and so sometimes I get out of practice uh but um the debugger in intellig is so incredibly Rich
uh that it's really worth times learning it if you're not already already familiar with it yes so F says I only debug
other um yeah so it looks like when it calls whatever mine's not coming up either canot Dr CI inspect response I'm I'm
getting the same error huh so now that's weird yeah okay well that's good because then I won't bother with with FL FL in
with with orb stack yeah so this this you know raises the I'm pulling down images I can see that down uh is this a
problem with uh the dock compose plugin it's weird though because this was working four so okay I wonder what I wonder
what's changed um okay let's let me do what what version of java am I running James uh I'm running 211 I don't know
which one so I am my runtime is sdk2 which is weird uh I don't see how that would have anything to do with it yeah I'm
on I'm using the live Erica uh 2101 um but I'm getting the same results I was just kind of looking like hey what what
things can we eliminate yeah so like if I do a Docker PS I get this container so the so I guess the question is so I
don't know how much long I want to spend on that but um why is it still up so it's so so what it looks like is happening
is it runs the dock compos dock compos successfully completes and now it's trying to find the specific container ID so
that it can connect to it or do whatever it needs to to do okay um but this PS response where is that coming from
because that idea is wrong that's what uh so where's that coming from that's iterating through the running PS responses
which comes from here what is that and it went through inspected so what do that's so weird because it should be just
taking the IDS it gets mapping it and i' use a list of strings and then it runs that inspect command oh so it gets the
list from one API and feeds it into to another oh okay wonder wonder if that thing here I I think I'm not g to try and
troubleshoot this much more I think let's work around it so I can always just let it run um uh can always start at the
docker composed manually def fall back to that um so let's let's just do that then um have to change the docker compose
where is do comp false where is it so online9 I'm just G to remove the dependency okay that should start although since
the database isn't running I expect it this is me my predictions I expect it to fail because the container is not
running and oh did it not repport even so are you passing how are you passing the username and password to your app is
from application properties uh yes so there's an application properties uh the local um where is that here okay so the
local is for winning running local uh otherwise it uses the railway profile which then gets it from the environment
variables okay so these get it from here um all right so now it's failing because the container is not running so let's
uh although it says it's running how' that get running wait it says it's running H did talker talker PS mine's not
running spring so uh starting and this time it says okay Local Host 5432 is not there it's not running so now I'm going
to do up all right I should have done up with a dashd right so now Docker composes up that oh I I'm Local Host 5432
refused why is it not up yet there we go so I had to I had to bring up the container directly I'm not sure uh maybe the
composed setup for maybe the composed setup is different I'm not sure but I'm able to wondering why yes we like I like
light mode sorry when I stand up I get a different profile yes the local profile should be default but maybe I didn't
set that up right uh yeah it's it use it should use default so how come when I stand up with Docker compose yeah if I
start with Docker compose it doesn't work I had to run the the container directly got it okay um I'm not sure what
compos is doing differently than my other setup um I think I know probably uh I think I have 5432 is that not when I
stand it up I get a oh okay so this should be 5432 on both sides something like that because when I stand it up I it it
knows that that's the port it's running on but exposes a different port let's try that so let's uh ask you James uh the
app is deployed in production but it's a private app so you wouldn't really be able to see much um I can I can I can
show it off a little bit later still says what am I doing oh I got to restart my do so let me yeah let me restart let me
stop let me run Docker compose yeah now it should work no we can't do that bug let's let's that oh but this is grid oh
you probably won't be able to run it run it because it's going to pick up some properties that are private to me yep
there you go um so at least I'm connecting to post but yeah as long as you get to the connected to pokerus then then we
know that that right that's where you need to be so let's try that so cool so now I think that that changed to line five
I think that might be the one so does that fix it that didn't fix it for me it didn't fix um I wonder if uh restart I
did restart restart your post so because when I do Docker PS I should see 0.0.0.0 port 5 432 gets forwarded to the post
Grace containers Port 5432 oh I may not have the compose bin because orb stack doesn't have that issue see compose yeah
it says I can let's out yeah it's there int seems to be having trouble connecting to it interesting maybe because it's
not in local that and Y Docker Dash compose and Docker compose are two different things this is not I don't know who to
blame for that um all right let's see so that's up let's see if this can connect to the to that so when I changed that
port in my Docker compose yeah that that worked fantastic I always forget about about this yes um every like every
single time well hey hey we we checked the box it wasn't on our agenda but we still check the box so um so Docker compos
setup correctly uh but there's something wrong with the docker composed spring boot thingy I don't know what to call it
the plug-in yeah interesting yes yes I've seen that yeah and yes what fun all right well what are we doing hey like
that's the thing like we can go Meander down different ways we started yeah it was funny because when I was thinking
when I was sort of planning this stream it's like are we gonna have enough to fill two hours and if it takes half an
hour to get the application started yes I can um all right so we want all right let me do this let me stop that
appliation is running and let me we were concerned that the changes that we made might have caused it to not work but
now it's working yeah so let me do a commit on the compose and we can now close that and it's now in our pal file uh so
we're going to leave this commented out we're going to add back in that's what we wanted to start with was our eths with
all right now uh the database is still up so now if I run should start connect fantastic and you claim that we should be
able to Host is Itor actuator yeah actuator slash metric should be there metric are there there's some and then I
believe try a Prometheus yep see exra info uh maybe it's just that metrics let me go look I have this other example does
it add stuff to that y it might just be adding it in there um but startup so has application started time yeah do we see
so I don't see any of the values there no these are just the names do we have to I think we have to separately request
the values is that the way it works try actuator metrics Prometheus I don't remember what it is what is Theo please
remember is it I just don't I just don't use the met I I don't remember so let me just go and stand up this other
project metrics I got to do all my credentials again sorry ingest that's for ingest that's din trce want so it should be
Prometheus uh but I wonder if require something else it's supposed to be actuator for metheus yeah okay why work is it
showing thank you that uh so maybe we have to give it the the metric name otherwise it just gives us the names uh that's
what it looks like so this is templated did we uncomment did we put the Prometheus registry back in yes yes it's back in
there um but it is maybe Maven didn't pick it up let me restart just to be sure because I added it but I'm not sure
sometimes may even Falls a bit behind yeah you added the property did you put the the dependency in I add the property
and I turn I think I turned yes and here's this dependency okay and this is the right one we what we're looking at yeah
all right so let's run it I'm peeking at another project oh it's got uncommitted changes so that's database all right
let's try it again yeah that's ah now it's there there we go so I I think uh intellig was slow at at at recognizing that
uh it had changed okay so good cat double checking that there we go there we go and now let's look for that start up so
thank you not B jgas at all for recommendation um yeah so let's see what are we looking for we're looking for startup I
think start up there's started um I think there's a startup time connection usage time does it start up to wordss start
taking to start the application uh you just had it oh something it's application start time process start time 1.73 2
seconds oh process start time there you go I think that's sure ah so start time of the so that's the start time of the
process that's when it's started process start time in second seconds so two lines down from that yeah so this is
basically the documentation for this gauge so this is this is is this this is confusing because this is the start time
of the process since the Unix e epic so that's just telling us when it started not how long it took to to get started
and that doesn't make match well I'm sure it is the time since since you since 1970 uh because it's E9 oh oh okay yep
that's not the one we want yeah that's start time that's time ah time taken to start the application there you go that's
the one and I think that's the one you're actually pointing at before uh 3.44 all right let's see if we can make that
better so 3.44 so is that is that that must be a templated is that a templated no it's not templated okay all right so
the way that Prometheus Works uh in systems past it was like Hey I'm going to take these metrics and I'm going to I'm
going to send Telemetry so if I if I'm overloaded I'm sending traffic right right uh and Prometheus was like maybe that'
s not the best way yeah how about let's let's just capture it right hold on to it and then somebody can ask and then
somebody else can go and grab it so they put all these metrics on this endpoint this Prometheus formatted endpoint which
that's kind of a a standard way of doing it and yeah you can get some really interesting things here so now we have
these metrics being exposed but it's still valuable like I don't have to have a times year database scraping this just
yet right it's still valuable to right here where it's at I can go into production I can see how long things took if I'm
comparing startup time I can get that so I'm going to do a commit and say added yeah James I know that like I do that
thing too uh he's watching it's bedtime and he's putting a stream on in the background to just try to learn things
passively I've I've done that for years I've done that for years so I I get it uh but right now it's like like it's
daytime for us so like how do we how do we make that adjustment for like who's in light who's in dark uh it's two
different things but yeah I understand I know your pain I feel your pain uh okay so so now we got an endpoint so we got
an endpoint um committed the box that checks that box hey we we did something let me go check it out get the do yes ad
metric start up completed love it um the next one we list is great now we'll upgrade it and then see if there's a
difference now there's two things here right we are going to upgrade dis reot 3.2.1 but I think we're running on Java 17
still yes and we'll want to upgrade we want to upgrade that as well and why do we want to upgrade because Java 21 is
better Java 21 is so so uh I an ensemble and this morning um we used uh switch with pattern matching and pattern
declaration variables and we're about to use record patterns and sealed and permits and and all that stuff together is
just so nice when you need it how amazing right yeah so of course we want to be like thank you Java team let's let's do
that yeah maybe let's do that first yeah let's do that first sure um and I say that because that one's easier it is yeah
but also if you're if you're not on job be that'll be yes that'll be an interesting Apples to Apples comparison as it
were so oh yeah that too uh but like I've been doing this for a while this upgrade thing for a while and what I find is
doing it one at a time do the Java upgrade first you're going to get benefit from that even if you can't upgrade to
Spring boot the the new version spring boot you can just upgrade your Java version and you're going to improvements
supposed to do it all by sure okay so uh let stop the application let me just run my quick should James I'm glad you're
here awesome yeah that's great we're feeling good all right so um test pass do we want to like start it up and see yeah
so now let let's start long database is still up so let's go ahead and right it spits out all right a startup time there
uh in the logs but having on that metric end point is kind of nice so saw flash was like 2.9 we're already getting
improvements like we just did you know there's lots of other stuff but like yeah I mean not the most scientific you know
was it a was it a you know already warmed up whatever and so on but like yeah we're starting it up and and hitting it so
it's nice like it just we expected something different even if it went the other way right to 3.24 yeah still we're
upgraded we're on the latest version y 17 is like ancient I know it's it's like you just think you think you know 17 is
is like what three years ago well with Java coming out with a new version every six months so it's for Java 21 is middle
age it just came out in September but it's been out for over three months Java 22 is incubating Java 22 is Early Access
Java 22 is going to be GA in less than two months yeah I want actually less than three months three month well three
March March something so it was September 18th yeah so three months yeah yeah so here we are like JV middle delays like
if you're still using jobs that's ancient one thing I know some some organizations have have scheduled as sort of
quarter you know quarterly updates it's like wow if you're doing quarterly updates that means you're doing one update
possibly halfway to the next release so maybe you should go faster that that is a a big concern if you're doing
quarterly up quarterly updates of what because Java doesn't come out the same day as stream boot Right yuntu comes out
on 10 and 4 right in October and April Java's coming out September March Stream boots coming out November May right
right so updates you're missing out yeah yeah and I just yeah I think J5 is the equivalent of Windows 3.1 not even
Windows XP oh but let me just say oh my gosh that's forever you're you're not the only one like I I was surprised just
like you that there are still workloads running Java 1.5 in production I'm just as surprised as you are you may as well
Cobalt as far as I'm concerned at that level yeah I mean it's working right it's it's running it didn't fall over it
didn't stop working but just feels like a testament to yeah well exactly risk is like okay we've got a really severe cve
what do we do yeah but yeah I you know so let's just assume there are some percentage of orgs that are still running
Java 5 okay I'm willing to bet that there is a much larger percentage of orgs whatever size org you want to pick there's
a much larger percentage of ORS that have no idea what's running in production they don't have a app inventory they
running all over until yeah yeah I don't know generics aren't enough for me I need I I really like the Lambda and stuff
and streams from from java 8 um but now like with I feel like 17 adds some stuff but it doesn't it feels like 21 is
where I really feel the improvements like along the way I've been you know I for my own stuff I generally keep keep up
to date but it really feels like 21 stuff is start to really come together around like pattern matching and and some
other things I'm I'm trying to keep my stuff upgrad so I don't get into all of the the Java features as much as I'd like
I'm practicing uh I care about giving things to production and right now I care a lot about security if I'm going to
expose you know hundreds of raspberry pies and stuff to the to the world I like to feel a little bit protected yeah yeah
I have a little bit of confidence that I'm not you know yeah bet in the farm kind of thing I want to let me patch I'm
going to try to patch things as much as I can as often as I can just to yeah oh yeah if you're if you're still coding
like you're on Java 7 you're just missing out just missing out and it's a shame but you know but you're still on a
modern jvm with with all the runtime like everybody gonna find Value yeah I mean you know folks always think about you
know the language itself but that runtime is one of the most incredible pieces of Technology and and you and you and the
way you get magic benefit by just running a different jvm is just incredible that's it just up so upgrade Java first you
can still program against the Java 7 API but upgrade Java first you can write like it was Java one that's fine yes you
can all right uh we are now on so we can we can check this easy yeah and we we saw some improvement we measured it we
saw some improvement yeah now here we go and now I get to use did you turn this into an alias yet turn what into an
alias the upgrade oh no I didn't okay I didn't I just don't do it as much as you do um but I I don't want it I don't
want it to be in Alias I want something else to take care of that automatically I don't want to have to worry about that
I think Alias there still seems like that could if uh certainly you can add to intellig you can add commands that you
trigger tools that you trigger so that might be one option yeah um it's easy enough to to do I'll tell you um I like
tools like Concourse and cartographer that are just um not triggered I can I can actually like pull and I can take
Advent like if I see that spring boot 3.2.1 gets released I can go and say oh here's a new release let me go make sure
that all of these repositories are upgraded let me run that command on all the repositories that I know of make sure
that they're still all on the latest so slightly different than like it depend upon right right but like let me just go
and do things yeah get that needs s asks uh Alias for which command uh basically for for this monster of a command now
is 32 inclusive of 321 it's yep so this is the open rewrite which is a framework yeah there's a lot more there's a lot
more to it um there for uh so what is so all the like and you can tell you can look at the recipe list one of the things
that that um is really interesting about open rewrite is you have these little recipes like let's update you know the
just the dependency part let's update the parent project let's update plugins let's migrate and then those can consist
of you know sub recipes all the way down until you get to to individual things one thing that uh I wanted to do is um
sort of run the reverse recipe of of removing the autowired because I know it did that as part of the upgrade we ran
last time and I actually like The autowired annotation on my Constructors and it removed it yeah so um there is a way to
to disable individual pieces of the overall recipe I'm not going to do that but but it is possible to do that yep and
you can glue recipes together and you can reorder them uh it's going to add the Jack's B glassfish implementation and
yeah that's one I always find myself deleting um but that's okay like the value I get these recipes way outweighs that
extra little bit of uh let me go and undo these things but the vision that I have for me and for you is I want I want
this taken care of yeah at a different level I don't want to put it on the developer I want it to be handled at a
different level yeah so so gets dependabot we'll upgrade the dependencies but it won't run what you really want which is
an open rewrite script like because upgrading dependencies is great if the dependency is backwards or at least is it not
a breaking release yeah um but what you really want is what we're doing which is hey there's some slight changes some
things got deprecated some things got renamed some things got removed and and replaced with other things it was much
more substantial when we went from 27 to to 31 with the security changes and things like that um but yeah you want you
want sort of a dependabot a rewrite aot kind of thing yep so that would be ideal we should go write one well it it
exists the of open rewrite uh has a company a SAS company that they they have not just for like the upgrades but also
for like cves and patching and like oh here's how this exposed you're actually using it here we're going to make it so
that that method can't get called right like the loog think like yeah yeah we're going to we're going to hide that here'
s the here's the recipe that fixes that cve right and they do that at scale so yeah it's there and there a lot of in
between yep there's a lot of things in between uh but yeah that's kind of the future it's like we were talking just a
minute ago about running Java 1.5 wouldn't how cool would that be that we both wrote things and took things to
production in Java 1.5 or or even older wouldn't it be cool to know that those things were being upgraded and that man
that would just feel cool like to know that all that software that I wrote in the 9s in the in the alts early 2000s yeah
that all that was now just running on Java 21 wouldn't that be something that we didn't have to go back and and do these
migrations not just every six months but every time a new Java version came out every time a new spring boot came out
every time operating system you know like how many things are we going to tie ourselves to that we have to go back and
be doing patches wouldn't it be nice the future of software wouldn't it be nice if we could get to ruction develop our
software in a way that it could take upgrades easily and just yeah let it run yeah they should they should be low low
ceremony yeah so so demo 26 um up an upgrade like that from java X to Jakarta that's exactly what you want to use open
rewrite uh recipes for is because it'll do that for you because that is you're not going to want to do that manually
even though even though Pro uh even though intell actually has some ways to do that transition for you automatically in
your project yeah that's one of those words like I don't even want to open up the project like just do it yeah like I
got I think the one time that I was paying attention like I open up intellig and it's like hey um you're you're default
you're using Java 21 and this is still Java 8 should we upgrade these for you yes click okay you're all right uh this is
it so yeah we're going to do it and we'll run the test button after we do this so let's see what it does we're we're
upgrading and this has a a bunch of recipes that are kind of together makeup that we know how to upgrade to Spring boot
3.2 the latest I ran it this morning and I was by running this I have it set up as an alias spring cube is what I I I
run and it just upgrades my project to the latest version of spring boot and and it was this morning that I found out
that oh spring 3.2.1 is that released and I was I saw that by the diff in my pom.xml nice so it's doing its analysis it'
s a it's Java programs the recipes are are made in yes Java I actually when it first came out I actually looked at that
writing at writing some so yeah it's yeah it's totally and that's and that's what's really nice about this there's also
another project called arrone that does some similar things but um these are all like if you have your company your own
framework like you want to I remember when I was working at Apple we had our own internal Frameworks and when we'd
upgrade them sometimes it would be work on the part of our users to adopt it and so had I think we had something that
was not nearly as smart as this that was mostly text based kind of changing stuff so it was error prone um no pun
intended uh but if we had had something like this um then this is ideal like you you have your own internal Frameworks
write a recipe that upgrades it and then just give it to your to your users that right so I have one particular moment
in excuse me in my career where I wanted to upgrade one of those internal libraries but I had no idea how far and wide
it was being used it was for a public partner exposed API and I I wouldn't even know where to start but I had something
that was going to save our company money and save us resources and save us time but it required a breaking change and I
had no idea I couldn't like see yeah hey do this thing because I was going to break people right and I had no idea how
to get that delivered so instead of doing it I had to like do like a a not as awesome upgrade a not as cool way of doing
it and I had to like sit on that and in that pain of knowing I could have saved a bunch of future headaches but I had no
way of delivering that right easily right and it was hard enough getting those Partners to validate and consume our API
you know as we're giving out credentials like uh you had to run like a a soft launch and run it against a a test
environment and validate and which should for you or I it would take a 15 minute or 30 minute stream to go and talk
about it and hey well I expect this to happen and then we read the docs and then it'd be five right but some of these
customers it was taking like six months to like call our API respond with this you know respond with the 204 or 201 give
URL that we can hit but it was taking a long time so I couldn't have imagined how long it would take if I didn't have
something like open rewrite but now yeah if I could say yeah there's a breaking change in this new version run this
command yep and it'll fix all the places where you're using our library it'll fix it to how you're using the new library
the right way y yeah that's the future of soft and that's and that's and that's to me what exactly what you should do
it's like to put the burden on the framework or the library like you know what your change is and yeah yes it might not
be the easiest most straightforward translation from your old API to your new API but you're going to know it the best
and then yes it might be more work to handle all the situations how people are using it so that it gets to the new API
correctly um but then you save so like The Leverage that that has you know of over any size company is is incredible
that's the future that I want to be a part of out of memory exception oh Jonas we can figure that out yeah I would if if
if not they're really responsive to problem reports and such um so Jonas if you're trying to run these particular ones
this upgrade spring boot 32 uh I will definitely help you out we can pair you know how to get a hold of my calendar uh
and I know the folks over at open reite we can call them and maybe we can get them on the horn and we'll work through it
so power of community Fe or not we will we will get you taken care of hey do attitude welcome all right so um one thing
that it did which is good uh I wonder if I had accidentally deleted this before but it basically excludes the junit from
test containers because it still pulls in junit 4 is that still necessary I I know that in the past it has been but I
want to say it's not not necessary anymore let's take it out and see what happens uh so let's do this I'm going to look
at this little project here I don't think that that's necessary anymore and it's adding Jack be back yeah we definitely
don't so one thing I definitely want to do is create uh a way to run the commands with minus a couple of recipes that I
know I don't need so um other than that was just a version number upgrade let's see what did it do to what did it do to
my property files hey it turned on Virtual threads as it should I was waiting for that it should so let's see it so put
it in application properties and it added to my test wait a second oh it adds to my test application properties ah okay
I'll accept that that's cool um so let me let me do something so uh let me Force may sure and what I want to do is I
want to see if that test containers thing is needed so let me go so I I'm looking at another project and I don't have
have that exclusion and my thing so where it comes where it used to come up is let's this um so if I created a oops I
created a test method yeah so this is what it is so it doesn't know do I want a junit4 j unit 5 test because they're
both in the class path and the J unit 4 is being picked up I think still by test containers got it so if we so we can um
we can verify that by going to our pal and where is test remove refresh since it seems to be slow there you go and let's
go back to our test so now if we an insert test now it knows it's junit 5 there you go so that's still still needed um I
think I've been tracking there's there is an issue file against that I'm sure it's not straightforward all right so let
me tkes uh interesting uh undo I wonder so with the exclusion um well let's let's make sure that I haven't broken things
by tests I am using test containers sort of in its older style did I run it I well let's see well let's take a look
because I'm I'm going to use the spring boot parent Palm to uh doing it this way is requiring the junit 4 to be on the
class path okay um I have a feeling if we converted this to the to the new style because this this is the old style of
of setting up test containers that we wouldn't need that um so thanks for for mentioning that that's ige because uh we
would have noticed that so let's go and exclusion uh so this is putting junit four back on the class path yeah so we'll
have both which is okay it's not hurt anything it's going to affect us when we're editing and adding tests uh but this
is going to work we expect yeah once intellig decides it sync there we go yep that did it okay then let's what I want to
do is then because I've got oops not that I've got here somewhere yeah update test container usage so I'm going to add
now all right um otherwise all the test pass now so tested one thing what's when that Happ the uh there's an issue uh
open since 2018 generic container run from Jupiter test shouldn't require junit 4 library on the Run class that issue is
still open yeah and I I know that I've read the refresh and now our application start time is just about the same 29 2.9
39 okay we'll take it actually technically it's 30 some odd milliseconds faster but uh we'll call that certainly not
slower there you go so there we go 2.9 39 there he said 2939 2939 yeah okay we'll take it so now we're there it looks
like the junit 4 is still a requirement to run those test could well we're going to commit since should I mean we've
just been making progress we're checking all sorts of boxes here look at that trail award we are flying let's go and
look at this that and done uh so attitude upgrading versions to me is so confusing to not cause any breaking changes
well this is where having good tests really helps abolutely but also of course like we've been looking at good tools I
don't know if there's such tools it wouldn't surprise me that in theet world if you want to buy some tests you want to
buy some tools to make you a little bit more confident somebody's selling that somewhere somebody's selling that
somewhere so Stars uh Railway does support Java 21 last I checked um because they're using the Heroku build packs no
they're using the Nyx packs um actually now I'm not sure if if Railway uses 21 I'm pretty sure they do uh coab just last
week or actually may have been even this week finally upgraded uh so that you can deploy Java 21 to their platform so I
know they work um and you always have an option of running a native image build a native image that gets rid of the jvm
and gives you a native image that you can run just about anywhere y maybe we'll get into that uh I want to find out
which build packs that Railway is using yeah so they they used to use build packs but some um uh oh it could be that
they don't support it yet um and and so it's really interesting it's like you know platform as a service uh is great in
terms of doing a lot of work for you um relying though on their build system to build your artifact means you can
simplify your end of things a little bit a little bit um but you do run the risk that they're be like J 21 was released
in September yes and it wasn't until early December that coib supported it and so you have to decide it do do you like
waiting or do you like having things under your control how much money that now I know a little bit of insights uh
around some flavors of the bill packs and what was happening uh there were some Upstream other changes were in place
they had to make some other changes that were kind of like hey other contracts that they had to do in order to move
forward and those took a lot of energy but my understanding for for the build pack ecosystem is when Java 22 comes out
it's going to be should be straightforward adopted faster know days not weeks yeah for those build packs to be caught up
yeah but it's funny it's like even days it's like I don't want to wait days I who does yeah who does because uh uh what
was it um like even Gradle like if you're using Gradle and you're using cotlin in your Gradle you had to wait um there
were some workarounds that they finally had but it's like I don't I don't want I want I get it we get so impatient yeah
so pass vers well pass vers success I think is a wrong comparison you probably mean pass versus what they sometimes call
I which is infrastructure as a service so AWS and all and and those are providing you in the infrastructure but you're
you're on your own for for cobbling all that stuff together uh but it's likely going to be cheaper if you know how to
use it correctly because um you can optimize things but there's yeah there's a cost cheaper some ways like because that
thing yes there there's the operational cost but then there's the the costs of what what the maintenance and the
maintenance the documents and all the so for me it's it's mistakes I am terrified of making a mistake and getting a a
you know $5,000 a monthly bill um or just Mak a mistake with security because I didn't do something right and I didn't
to cook up private Network correctly and expose something and and if you have people who are dedicated to doing that
because your organization is large enough it pro you know and you run run all the numbers it might make a lot of sense
um but uh I'd much rather you know especially for for smaller apps or even if I was running a company it's like let's
start with a pass see how far we can go yeah when we start needing things and we start looking at our costs and it
starts getting a bit expensive because passes can be a bit pricey they can be a bit pricey but the newer ones like
Railway and Coya their pricing models are really nice much better than heroku's so yeah numb lot of options and make
sure you include developers in those numbers because they cost money too and you know one of the things I like saying is
I don't have Cloud money I've got Raspberry Pi money so I'm trying to do these things on Raspberry pies there's a lot of
Open Source a lot of the paths you know offerings are built on top of Open Source projects yeah right and you know I've
got more that I've got money so so I'm going to go ahead and spend some time on these things and and I'm going to learn
along the way yeah but yeah I I lean into this platform approach I've got a bunch of these different domains I'm a
domain hoarder I've got boot apps running all over the place but if I'm doing as a platform you know build packs are a
big part of what I do if I'm do as a platform I can run all update all and I can get everything up to date or if I'm
really smart I can keep track of what's been deployed with which version like hey keep metadata repository of what's
been deployed with Java 21 so that when Java 22 comes out and it's available I can fire off that event that says go
upgrade into Java 22 yep yeah and I I I guess uh I don't want to deal with that I don't want so great that you're that
you're playing around with it but like I I'm bottle recycling money it's like I've got five bucks I can spend a month so
I'm I'm fine spend five bucks a month on on my apps and C is even is even cheaper uh with with the way they're
structured um so hold on one sec yep yeah so it's it's funny it's like you know we always talk about scaling and things
like that and like especially for our personal stuff like you don't you don't necessarily need that kind of scaling
maybe you're lucky or unlucky you get Hacker News attacked DDOS but uh yeah how many requests per second can you handle
Raspberry Pi I know depends but some estimate like yeah it depends on what I'm doing the fun thing is is with the
Raspberry Pi and with the native images uh that I'm deploying and I use K native serving to Auto scale uh so I can I can
move my resources around so if I get a Thundering Herd uh on my Hello World app I can scale up that hello world app on
these different devices and then the Hello World app is doing its thing and it's processing now it's going to move some
things over it's going to do some batch processing the hello world gets to scale down and the the batch workers get to
scale up so yeah uh I've got a lot of raspberry pies so my like total throughput uh request yeah I I I couldn't even
give a ballpark but on my on my uh yeah when I do on my laptop um I think I could I could run that test that's a good
thing I'm gonna I'm gonna put take a note to do that like how many requests per second can I handle on uh K native
deploying these native images uh for just like a Gatling is what I'm going to use like I've been using J meter for such
a long time but now all cool kids are using Gatling so I'm going to oh okay all right but yeah so for me what what I'm
more interested in is um is is latency rather than sort of and see his the new down uh like I don't care how many per
second I want I want my one request to come back really fast because you know the number of users like of my ensembl is
you know maybe 15 um but like I don't want to have to wait another half second for the page so exactly maybe on the
first one uh can really handle l native images yes because it can deploy and all these ones as far as I know they're
going to let you deploy Docker in fact uh ones like fly.io don't even mention Java uh so it's this like we don't even
rate an entry on here Java's not here um but Docker is so so it's fine all right so we to do which means you know so
Railway which has first class support for go ahead and run Maven and build an artifact and then and then run it perfect
for a spring boot um ones like fly iio if you want to try them out you're going to use Docker but then why not use a
native image and and there oh I was going to show uh ensembl so let me show ensembl H so hold on let me make sure I'm
not gonna show anything sensitive I know pink Emma she's been on my streams and and and every once in a while I'll show
a secret or two and she's like free tokens get them get there's there's um uh I don't have it active anymore because I I
haven't been doing much stuff with use Secrets um but there is a tool that for some uis that don't hide the API keys and
things like that uh the extension will actually hide it hide it for you when you turn it on that's really this so this
is the the the UI is is redbear basic minimum does just what I needed to do um so with this Tool uh it's basically about
managing events you can sort of think about it that way um but has some some built-in things like um shows me how many
participants if anybody declined so they had signed up and it's like no I can't make it um just me that uh I can click
into here but it's going to show some details that I'd rather not show and then all the way at the bottom which I it
shows all the ensembles uh through time um you can create a new one and so what it'll AO this is this is sort of the key
part is uh you just give it a date and time it will go out to zoom using the zoom API go and create a meeting at the
right length with the right parameters with all the right stuff uh and then um and then that's that's it and then when
it's over I can I can upload a recording and it it provides that link to those who have have signed up so uh it and uh
let me see yeah I'll show I'll show that other thing later um actually let me try something switch to that so this is
this is the member view so if you are able to if if you paid me money in certain ways uh you can you can join these
ensembles and so what we see here is um the date and time and then the participants right now uh this one actually these
happened in the past uh even though it says upcoming uh that's I got to fix that uh and then I have this feature that I
recently added called Spectators because I was getting so many people who was like I want to to join but but I don't
really want to join I just want to watch and see what it's like um so I have a special thing for that uh and um you can
sort of flip back and forth if you have per right now there's one level of permission next week I'm going to be
streaming about enhancing The Spectator capability because some of the things that I wanted to be able to do uh you
can't and anyway so there's a bunch of features I want to add about around that um but yeah and it's it's us is a tiny
little postgress database not very large but still postgress works really well and uh and so after the recording link
you'll see this when one is coming up you'll see the invite uh and yeah so it's it's you know I talk a lot about like
you want to learn build an app that you actually could use y because you're gonna find things that Spacey you understand
yeah and that helps you and that you'll be motivated to to to use it and you'll be able to provide if nothing else your
your own feedback perfect close that and I finally added a a favicon um yes which was like why did because like why I
thought I added one some time back and I don't know it must have disappeared or I never did it and so things like that
like yeah because otherwise it has an ugly like default icon it's like so that's that's fixed up let keep going all
right um uh yeah I don't know much about cus I will admit my ignorance to to Cous I don't know what the surus when I
hear Sur all I think of is uh scale up from zero scale down to zero scale up fast scale down all the way to zero that's
that's what I think of cous yeah I guess I I think of cous as more like serous functions but maybe a misconception
similar like I think about like because when I first started playing with like serverless stuff it was basically here
write 10 lines of code in this you know AWS UI and and and push a button and now it's available you don't have to do
anything um with with containers or anything like that so to me it's it's I guess serverless for me translates the sort
of container list like I just want to write a little function um but yes you want you know y to have the ability to to
scale up and scale down to zero quickly is is certainly valuable and the technology has come so far that you can right
because part of that scale up part is you don't want it to take five seconds or 30 seconds to yeah come up right so part
of that that corner of the technology is it's gotten so fast and so Advanced that you can have a spring MVC web app to
red and post scale up in 0.4 seconds right right right so there's different options for that uh AWS Lambda is one uh but
James you've heard me say before get your MVP to work on your laptop first and to do that on your laptop you use I don't
want a monthly bill either right so I use Cana of serving yeah and I use I use coab and you can get a a 512 megabyte
thing which is more than enough especially if you're running running native to to to do anything you likely do maybe not
everything but you know certain certainly enough dark mode for Embler yeah I should probably have at some point when I
when I upgrade the UI um dark mode man uh from this from the beginning of the stream I I wan to um I I I I I want one of
the things for for 2024 is is is I want to hire a UI designer to improve the UI because like I could do it but God it's
it's so painful can I tell you a secret go ahead you want to know who my UI designer is who voden have you played with
ven I have I philosophical problem with with that I want to hear I mainly it's it's I've been burned before by trying to
do everything in Java um okay and I like uh so way back in in when I was working for a company called guidewire we were
internally evaluating what our next step was in terms of um front end uh and we were looking at at GWT and we love the
we love the fact that hey we could write our front end GWT we did uh so I ran a Proto uh was me and and somebody else we
were I think was somebody else might have even been just me I forget um but we were sort of doing is this gonna is you
know Fe feasibility uh so we were looking at is this is this even gonna g to work and to create stuff was great but then
when we wanted to interact with other JavaScript yep it was so so painful so Crossing that that Bridge basically from
you know Java calling JavaScript and JavaScript calling Java um I basically said no this isn't gonna like this is not
going to work let's just let's just learn JavaScript use JavaScript on the front end do it you know with JavaScript and
HTML um and so yeah so that's I I think there's if you're working inside a company um and you need to get tools deployed
B is great love it love love the idea of that um but for me I I don't I don't I I like a little bit more control so I
come from I don't even build front ends I I'm building the the Enterprise grade hello world right. Json right like
everything is kind of uh spring boot Centric so really the UI that I've made is uh what you just showed is like a
million times better than anything I've ever developed until I use voden like so I like if I want to make something
pretty and presentable and and be like hey I I'm full stack right that's where I go because it takes me zero time but I
don't put any effort into thinking about the front ends I'm my my mind is definitely thinking about how the backend
systems are going to talk to each other yeah and and honestly I haven't played with voden in a while so I don't know
what it's what its performance is like um but I'm I'm very much of of in in the camp of I want the browser to do its job
which is render HTML and I want the back end to do its job which is generate HTML um and anything I need to bridge the
two to make the UI a bit more interactive without having to hit the server I'm going to start with something like HTM X
um and and a little bit of a bit of JavaScript um you just because because the thing I don't know about and I'd be
really curious and I'd have to spend some time with voden is what is the test what does it look like to test yep like I
can write tests against my back end that's generating HTML and I can if I wanted to I could run HTML unit to see that it
generates the right stuff um and and related so I don't know what the testing yeah what that looks like for for voton so
that would that would be interesting this is this is what I want to do with you uh so sometime after the new year uh I
want to go down this path uh I got a project in my head that uses voden that I want to do uh and it's something I think
you'll enjoy too uh and I want to do it and I just want to start it with waten and then we can talk about all those
things from the start because there were some really cool interactive things uh Dan Vega and I did a a workshop over the
last couple years we were doing these workshops and we used I did the front end I I built this voden front end uh voden
gives you kind of a backend crud interface uh out of the gate but I basically I rip that out we have these new um
declarative HT P clients MH so I basically I rip out the crud I plug in this declarative HTTP client that's just
consuming the crud rest API that we generate in the workshop right so you get this like nice cool thing but it also has
this cool like one of the default uh uis is like this chat interface like hello and you you type and you response you
get a little chat window that says oh that worked or like just a little feedback window but it's all in Java right you
and I right now are both kind of uh we're at the helm we're doing all the things so when I can first of all they have
like an interface that I can go and plug and drop in different templates and I can drop in different components they got
a beautiful component library but then there's also an ecosystem of components around bottom that just make it really
easy to go yeah so but I have a project in my head I would love that like Hey we're starting from scratch because where
I kind of run into problems is like what's the first test that I'm supposed to write is it that the context loads is
that supposed to be the first one okay now which one right which one after that what's the what's the one right after
that yeah yeah yeah uh so that would be fun for me so I'm making a note here after the new year uh I want to sit down
and just start like let's get a let's get a Hello World you know Click app and let's write a test yeah around bot yeah
I'd love to i' love I'd love to have an excuse to to to to try it out more because I I feel like my opinion are about
four four years out of date so um so as is it possible to do front end with without JavaScript but presumably uh what
you mean is with just HTML and CSS and yes uh I mean the ensembl UI like the the look of it I'm okay with it's and this
is where it's like it's a bit more like UI is so many things and so it's it's almost a bit more ux like what what do you
want to see what's in useful information how do you want to you know sort of architect how how how things look and
that's where uh I'll want uh someone to to help me with that um because I I I I use Tailwind I know enough to to to get
by um you know may not be the most aesthetically pleasing thing but it's more you know how do I want to structure this
this information so that UI the only JavaScript that's that's there is to translate the DAT and times to your what the
browser says your local time zone is because I feed coming out from the API it's not even an API what I feed into the
HTML is UTC uh because what you want is you want the browser to to do the translation um theoretically I could have the
server do it uh but having the browser do it was was a little bit easier I'll probably migrate to to the other one um
although if you if you look if you run the performance you can actually see that JavaScript execute and so I'm trying to
beef up the the uh the page the page load time because that R matters again for like this apps like I need come on let's
move it you're not doing that much um so when I and HDMX would make that even better because then it doesn't have to
reload the whole page ah yeah so I come from a time uh I know I'm dating myself but there was a time where JavaScript is
a little it would work in one browser it wouldn't work in another and we were we were battling like oh well which which
browser do we support like we're going to support this one just get it to work on this one because we didn't have a team
that that could do all the different browsers that were changing all the time yeah so yeah the the the dark days were
were definitely dark and and and I was there during those dark days and it took me I I might still not be over that
trauma um you know where it's now okay to to do you know to do JavaScript and um and I need to sort of beef some of that
up because one of the apps I want to get back to for next year is is turn my uh my my tdd game my tdd game yeah uh into
an online version um so I've got the back end for that I've got the front end in View and I want to see what I want to
do it in HDMX and maybe even use uh view components that be um so that's that's that's what I'm going to do there so
that that uh that will be that'll be a modernization project as well because that one is also old uh it's actually two
or three years old now so but you can do web apps without any JavaScript whatsoever do it all in the back end and it's
funny I was talking I was talking to someone and they wanted me to do uh a boot camp where start out with you know for
mainly non-coders to to get them up to speed so you start out with you know your JavaScript HTML and then do spring boot
uh and then they wanted to react and I said I'm fine with those first two modules I am not with you on that last one uh
a you know I don't know enough to be able to teach it and B I don't want to know enough to teach it because I think I
think it's way overused yeah yes exactly tdd game online uh with with HTM X I think it's totally there's no reason why I
can't can't do that there's nothing there's not so much State and complexity on the front end uh that it needs to be a a
full single page application so I moved my mic my mic used to be up here and everybody was like oh you're you're quiet
cuz it's got a weird thing and then I moved it and now I have my headphones turned up so I have them Monitor and I can
hear my stomach it's down it's down below and I can hear my stomach in my headphones and I'm like I hope that everybody'
s not hearing that because my stomach has just been the whole time so I'm like wondering is it is it worth having the
mic down here so that everybody can hear my stomach well you sound good and I haven't heard any rumbling so wonderful
you're all you're all good works best with ie4 yes the good old days of works best with ie oh pixie report just just Ed
herself for themsel a little bit Yeah so I mean there's a bunch of monitors I don't know if the so tc39 is the standards
committee for for Java well technically equiscript um and I know there's some new date stuff I don't know if it's out or
I haven't followed in in in a while but yeah it would be nice if I could say without without having to write any
JavaScript here's the date and maybe this is already possible I don't know I haven't I haven't looked at that stuff in
probably since I wrote this for for Embler which is now almost two years ago so maybe maybe that's changed I should look
into that um but yeah it would be nice if I could say Here's the the UTC do whatever you need to do you're you're the
browser you know this stuff do it yourself um like time zones time dates all of this stuff is super D super duper
difficult yeah and one of the things um having been in this world of updating and having servers and having Rasberry
prise uh and doing things like Pudo app update Pudo app upgrade uh for a long time if you had yeah ran Linux you
remember this package called TZ data TZ data is time zone data and how come it's being upgraded like what could possibly
be upgraded every other day for the entire year like how many countries are being brought in switching time zones like
what kind of funny math are they doing that I'm getting a new time zone data package like weekly what is even happening
yeah but I say TZ data everybody knows hey I'm going to check it up oh TZ data like it just yeah yeah and for those of
you who look closely at your Java release notes you see we're updating TZ data to whatever we're dat to whatever it's
like oh we've got a patch release we're updating TZ data it's like the main reason we're releasing it yeah crazy um what
should we do next what's the next on the list uh well test container usage is next but I kind of feel like native image
should be okay let's go there let's do that because I have no idea what I'm doing with this so so let's let's talk about
the native image stuff so we we've kind of mentioned it a little bit one of the things that came along with spring
framework 6 and spring boot 3 we had to rebase to Java 17 why um mainly we wanted to be able to use some of the newer
features that were available and what we what we what the spring team was trying to do is support more advanced modern
usages mhm with Java so they said hey you've got to get up to job 17 but promise you it's worth it because you're going
to get do all those cool all these cool things and one of the cool thing that I care about the most was these aot native
images so what what we're going to do is we're going to give ourselves uh this ability we're going to say hey grw VM go
go and look at this bite code and optimize it and if I'm not if I'm not able to reach part of that code just throw it
away if I'm if I pull in a dependency for junit 4 but I'm not using junit 4 just throw it away right because that
dependency is coming in as a test scope and it's not going to be in the native image it's not going to be there right so
it takes a little bit of time the grvm piece is analyzing that b code it takes a little bit time so even on a fast
computer it's going to take a minute or so right but at the end and it's going to give you this mostly statically linked
native binary uh it depends on if you're using muscle or not but statically linked native binary so if we're on Mac it'
ll be for Darwin if you're on M2 it'll be for arm64 the trade-off there's a couple of them there's the the compile time
MH but then there's the fact that that that output can't be used across all of the other places of where you in Java B
code is right one once run anywhere right that you had a jvm any operating system anywhere bite code jvm you're good and
because Java does that Backward Compatible thing like this was amazing and maybe that has something to do with the
longevity of java but now we want to do more with less we only have a 512 megabyte free tier we want to be able to get
more than one app or at least one app on that 512 megabytes so grvm to the rescue spring team making it easy to the
rescue but we get it out of the box we don't have to do a whole lot we have to add our grvm dependency uh so we can get
the grvm metadata MH so that if there is a project that we're using that might have um reflection or proxy usage we can
tell gr VM say hey like this class right here in this Library actually uses uh reflection and I want you to be aware
that here's where it's used so make sure you do the extra work but I'm letting you know now because you might not see
that at compile time right right yeah especially reflection that kind of stuff you will not see it compile time so the
metadata repository exposes that to the grvm so the grvm can make sure that it it takes that into uh account when it's
building that native image because you don't have those abilities we're doing all this ahead of time compilation at
compile time we're doing all that analysis we can't do the other trade-off another trade-off is Dynamic Property
changing Dynamic class math changing we don't have that right there is no such thing right and there's you know some
people look at it as that's actually more secure right if you were the log for J thing right not too long ago if that
was a native image you didn't care right right you that wasn't exposed because it was thrown away that code that you
weren't using unless you were making that a part of your test and then right you shame on you anyways uh but here we are
we can basically add this one step uh in the parent palm of string boot you have a a native profile and it knows what to
to do from there all right so all we have to do is add that grvm dependency and the way I cheat I go to start. spring.io
and I in a generic project I click Maven I go to the ad dependencies support yep and I click Maven on the top left I can
just so you can copy paste oh I didn't I didn't click Maven yep click default there you go and then explore and now I
can explore yeah yeah dependency uh so it's this one yep is it just a plugin just right just that and that's going to
that's going to access all the uh the metadata Repository and give us all the things that we need in order to do this
native image build so now because we're using spren boot 3.2 we've already done the upgrade we already seen all the
performance rout we can go even further by doing a native image so instead of doing spring boot run or spring boot go
run uh we can now do there it do yeah we excuse me we can run a native build so I'm not sure how to do it we're just
turning on the native profile and doing a spring boot build image uh I I don't have to build an image I can do I can
build the native uh output without putting into an O container so from the terminal I'd be doing spring mvnw Das P
capital P native because that's the profile okay yeah that's the profile and then native colon compile there we go so
now we've said hey we want to do this native compile so now oh we have to have a gr VM jvm ah so we have do that yeah I
don't think it'll be able to do that or it doesn't have to be grm you can also use the Liber Nick version I'll just so
let's grab yep gr vmce grce yes so the gr C the gr jvm it's a jvm built with Java so it's open jdk it's it's doing all
the other things but it's built with Java but then on top of that it has this ability to go in and scan and do all the
analysis on your Java but also on other languages but they built it with Java this is coming out of Oracle labs and
their work they had this project for a while it's been out for it's been out for a while uh but early on I watched a
video of one of their brilliant Engineers on the jbm they had this like sub straight project like yeah this this is the
minimum part of the jvm that you would need and you were able to like build just against you know use just some part of
the Java libraries against this substrate but I remember watching that video I found it on YouTube when I was like oh
that definitely led into this grvm because what grvm is doing after it does all of its analysis it grabs the bits it
grabs that substrate of the jvm it needs a little bit of garbage collection it needs a little bit bit of the thread
management but it handles all that now the cool thing with spring boot it's it's also doing that analysis on the spring
boot jar so it's analyzing or I mean the Tomcat jar it's analyzing all of Tomcat and doing all the Tomcat down and it's
putting all of that so you have your your app your bits of Tomcat and the little bit of the jvm that you needed and it's
all squished down in this tiny little statically linked binary it has all the things including the garbage collection
inst doing the virtual thread support M it's going to have its own virtual threads boy look at my CPU pinning my CPUs oh
this part was it's us it all Yes uh when I first was doing this my my stream would blur out and be like oh yeah sorry
we're we're doing too much stuff glitch glitch glitch so yeah just that like that little uh that little feedback thing
of I can stream and I can do a native compile today that's like a that's how far like we're doing this in just right two
years I've only been in this role for two years and two days and happy anniversary yeah thanks and we've come a long way
and it's great yeah I can I I can tell my video is jerky oh it is so my yeah my webcam video is a little jerky so that's
unsurprising while we're while we're waiting for that uh tram star had a DDD question um so I want to return a list of
country code to the UI but in our domain it's a value object is it fine to return a list of VO to front end uh has to be
another context aggregate route so the key thing that that I have had reinforced for me lately in in the DDD realm is
that Aggregates are only needed if you're doing changes to state if you're changing stuff if you're reading you don't
need an Aggregate and in fact the aggregate can be annoying um so for something that is like country codes if you just
want to display all the country codes it doesn't belong really to an aggregate it is separate it is basically hey here's
a table in my database of all country codes um and so you may not even need to pull those into value objects because
value objects would be where you're going to use it in the domain I might pull it directly from a repository and maybe
even turn it to Strings um especially if there's no ideas I would assume though there's probably going to be some key
because you're prob it depends on how you're localizing things but if I were to do it I'd probably use the iso two
character or perhaps three character country code as the key that comes back sent by the API um to associate that with
the actual country code because I might actually localize the country codes the actually country displays but if it's
just the country codes that you're displaying to the UI um just return those directly from the database almost I mean
you you know you may do some mapping in between but um that's something that's been really really sort of refined in my
head and clarified is is you know in domain driven design there are these things that are Aggregates but it's all about
protecting from uh and making when you do changes making that consistently you know you don't have to go to cqrs
separate your read and write things but in a sense you you are already uh so hopefully that that answers your your
question tram stars and hey G all is done all right fantastic seems to be done so now in your target directory you
should have a probably called ensembl uh target. Embler uh and that's an executable there it is yep so now fun is let's
run it all right the properties that we had that we gave it at compile time are the properties that it's going to have
right it's going to take in those properties so let's see if it starts okay a MC Handler mapping introspector request
Transformer okay I've not run into this before let MEC Handler mapping introspector request uh well I got a little clue
down first presumably that would mean so if I if we change the setting to that do we have to re generate the okay yes
that's a bummer uh so let's put that in I guess in our let close this here properties thr that here now fun fun little
trivia thing is I'm a big fan of arm 64 Raspberry Pi Apple silicon I have an amp Amper machine when I was waiting for
that Amper machine to come from China uh I was really excited because it had 96 cores and I was convinced that my native
image builds were going to be blazing fast but alas they were not the Windows machine that I have in the closet there
the little gaming computer that I bought a year ago is still the fastest native compile that I have and our friend Josh
long has the new new latest and greatest M3 right laptop with all the bells and whistles uhhuh and that Windows machine
is still faster it's they're not doing the same for same right the windows Mach x86 that doing 164 so it's not same same
but like when I'm doing demos if I'm trying to show stuff off uh I like doing demos with the Windows machine because the
native builds are seconds much faster 30 seconds right 30 seconds 30 can great fantastic we are uh that's a good
question we'll look at we'll look at the size once regenerates it yeah so here's the cool thing is the size of that
executable remember it's including the app right and tomcat and the jvm all of that is in that executable when you're
delivering the container the size of the image so there's two things here there's the size of the image mhm right that
executable uh you're not you're probably not passing around that binary executable a lot of places unless it's a CI but
even then it's it's still tiny yeah because what we were doing in the past like spring shell the CLI it was you running
Java and you were loading the runtime to do that well now that's another place where I find a ton of value in these
native images it's now I have the spring spring shell project I can compile those cool little shell tools into native
and and I'm I'm doing it with Java and it's awesome but I'm delivering these native you know you don't need to go to to
to start using goang to create nice little command law utilities yeah like so I don't I don't have all the information
but I believe it when I hear others say like right now it's kind of the Java 21 with spring 6 and spring 3 the most
important release ever is Java 21 of of java this is the biggest Milestone that we've ever had and again language things
aside right everybody kind of you know especially for those of us that have come along the journey the big thing is I've
been around long enough to hear a bunch of the the language Wars and oh no you got to use goang or no you got to use no
or no of course you're doing AI you got to use Python like right right where there's like these default if you're doing
this then you must be using this language but now we're in the spot where there's been so much effort and emphasis and
work put into our ecosystem that personally I don't have to switch languages yeah for anything like there's yeah I did
uh you know I was really proud in like uh 2021 uh my first few weeks on a new job I was delivering open source PRS in a
bunch of languages in C and go in Ruby and Python and Java I was and I was I was fine with it it took me a lot of time
but I could figure it out enough to get a PR get something fix to work and I was delivering I was doing a lot of it on
stream actually and uh nice but I was I was fine with it I was having fun but now I with the raspberry pies you know a
lot of those fun little starter projects were all done in Python right uh and now all of those little fun little
projects I like I'm not doing python not in this home lab not for me not for what I'm doing so I'm converting all these
other one-off projects and these one-off languages and Frameworks I'm just bringing all back to Spring in Java and I can
deliver his native images and I can do everything I want with these devices and I can stay in my same language my
comfort zone yeah I'm still getting outside of my comfort zone because I'm having to do things and and analyze these
other languages and put but I'm also having fun using chat gbt to tell me what is this thing doing and then I just turn
around and I I write it in Spring yeah to come back yeah it's not come back it's it's it's people recognizing that that
but yeah I I you know uh I've been using Jaa for you know since since pre1 and so I'm um i' I've been quite relieved
that uh that it's been going so well especially over the past couple of years and and with Java 21 and all the the
thoughtful additions to the language and now the the you know the jvm itself and now with the the grow you know native
image support um yeah I can stop having to say oh I maybe I should write this is because I can write and go if I need to
but I'd rather not so you're looking at the the size of the image the 123 Megs that includes Java right so the jar was
the jar itself was 59 and so it it's not surprising that this is going to be but not terribly like it's not like it's
gigabytes uhuh now if you built the containers if you built the containers with the jvm you would deliver that jar would
be one layer so that 59 Megs you'd have your operating system but it'd be the same operating system uh let's just say
Alpine right you would either have the jar and the Java layer right with your operating system or you have the ensem and
the operating system so when you look at that 123 Megs versus 59 Megs there's a whole another layer that's Java 59 Megs
You' got a lot bigger than it's a lot bigger than yeah it's a lot bigger than the additional 70 Megs or so yeah and that
let's see goes into account like when we take that out and we pass that around our our friends those native images at
least for developers in my head your development team is all using native images on their laptop and it's scaling to Z
because they don't need it running 247 yeah I'm deploying to raspberry pies and the native images are great there um but
yeah there's some places where the J is better but I think for development typically those native images are kind of the
default and that's the better way to go ah okay so this is not surprising because um that key is only supplied uh uh
when I run locally when I run uh with Dev tools because it picks it up from the config directory all the way up in my
base um so so I could probably mvrc is what I have defaulted to so I get those in my shell and I can just pass those in
yeah so that's something I I if I'm going to do Native images um I don't think I'm gonna push is I'm gonna have to
figure out a better way to do those environment variables that are sensitive um so you'll have to come back and and show
me how to how you do that yeah and I've been showing that off um where in our you're familiar with dur MD EnV that uses
the VRC files basically when I switch I've seen it but I but I'm not familiar enough with it to when I switch between
different projects different directories I've got a VRC file and that VRC file just says hey here's the environment
variables that you need but I don't want passwords and secrets sitting on my disc right so the pattern that I've been
sharing that I do is in that VRC file I say hey log into my secret store whether it's one password or I use bit Warden I
say make sure you're logged in to there and then for this application go and grab the the login go and grab the S grid
API key and put it in this environment so it's not on my disc it's still in the environment if you get into a shell you
still get it but the way that I have my computer set up because anytime you open a new shell you've got to type in the
credentials that my my big long password in order to get to my credentials so you can't just land on my computer and get
access to get what you need yeah and it's not on dis anywhere yeah I'm gonna add that to my list let list I have that
yeah we have to we don't have to dig too far but now the native image piece this it's nice if we had it um that startup
time uh is faster the memory footprint is GNA and that's that's actually more important to me than than the startup time
because like you're were saying it's like if I can squeeze it into a smaller VM I pay less yeah yeah and yeah and when
we're dealing with 512 megabytes which for a lot of languages that's that's plenty and now Java and spring and
Enterprise grade production ready spring it's plenty yeah it wasn't that way that long ago but now it is yeah yeah I
mean ensembl I think runs in a it's runs in a 512m space anyway but it's not a big application so yeah um so we're going
to check out browser report the Duram stuff I can show that um oh do you want to see the auto versioning stuff yeah if
you have time I mean I know we're running up against your schedu time but if You' got time running up against time um
you push that off if issues nice so tram Stars I'm assuming that since we can deploy a Docker image we don't have to
write our own Docker file we just need to create our own image that could be retrieved from somewhere um and you can put
for free up on GitHub because I looked into this in their container registry you can uh there's some limitations around
how much bandwidth and some other stuff um but if you're not every day you can pull I think I there is an image size
limit but I think like the probably the the network usage is going to be the the more important thing but I think if for
something like this as long as you're not deploying every day or multiple times a week you're probably fine yeah um I I
still deploy I have all mine going to my public repo uh on Docker uh and I just have a little name convention so I know
what's what yep and yeah and it works yeah but the rule is Jam stores don't write your own Docker file don't friends
don't let friends use Docker file because that's what that's what I've heard from desan he says he says don't don't let
anybody write Docker files like just generate the image and then put it somewhere um but that does mean you have to
generate the imission and put it somewhere yeah so um I can show you I have time I can show you how I use jayver okay um
yeah so so let's go back to your project all right um and oh I showed you my initializer Plus+ and you you submitted a
PR for it yes uh I don't know if you're running that locally uh but in there I've got some I got some cool things uh it'
s not magic uh what I do is let me pull up this other project um I add an extension I'm G to try to find a project that
I can talk to real quick I add an extensions. XML inside of my mvn directory H and I'm going to just copy and paste this
over into Discord so that formatting and I'm going to try to keep the formatting oops I saw earlier today I and I wanted
to say something but I was I was not in a position to do so you're you using the three back ticks instead of the the
triple double quotes and I like no it's the triple double quotes uh so here's my here's an example it's actually I think
the 1.7.1 but I put this into my DOT extensions so so just a separate file yep a separate file inside mvn inside just
not inside the rapper yeah okay so let's do that new XML there's two there because I again I'm doing arm 64 native and
x86 native so uh for the jate ver is the only one that you need and this is It's it hasn't been touched in a long time
but it still works it still does what I need and I'm going to add this I'm going to make a little change uh I'm going to
give you the cont and this is J.C config same uh in the exact same folder okay so this config file basically is telling
jger how to find the version number and you've got I think those are all of them that you can you can say hey grab the
last version or do the next version or whichever tag I'm closest to so that if I'm on a branch somewhere it'll still
give me like a valid Branch I can get it based on the tag so I can do these really interesting things because like in
your palom file you've got a version right and when you're doing a release you do get you got to change that version
somehow you have to have something around it if I remember I change it manually and that's about my my process yeah so
with with what we have right here if you do a uh clean package if you've got tags it's going to yeah just do a uh mvn
clean package and Master um I can just run this from the ID what you want me to do you want me to do a package package
let's just do that and what it's going to do at start it's gonna say hey where am I where am I in G I saw it flash
something and it's going to give you a version based on Z yep because you don't have a tag tag yep inside your
repository now the cool thing is is like you know if we're pushing and we're doing other things in our cicd I don't want
to forget that tag and sometimes I've got other conventions around it but by using this pattern by using this plugin
when I tag something that means something and when I tag it that's the version it doesn't matter what version I have in
my pom file it's the tag right and I'm doing more things off of that tag in other systems right when I'm reading and
analyzing and doing all the stuff when I'm trying to connect the dots between all the systems I don't want to have to
like check out a repository and then read the tag read the version from that pal file it's much easier if I can say get
tags I can see what versions are where so now is what's it what's it using the version for is it using the version for
anything besides the the name of the artifact it replaces it yep so it replaces that version so now you're project so
replaces this so yep at build time it replaces this version yep so I actually my convention is I replace that and I make
it version zero because it's going to get replaced M so just so everybody knows when they come in here that's not where
you do your version and now if I did a get tag okay V 0.0.1 let's go do that right and this will just be local right um
package and so that means when I when I go to my actuator info it should show up there yes okay so that's one of the
other nice things is that's that's my main yeah that's that's one of my main use cases is is that's what that's what I
want because um that's how I know I make sure oops Yeah that and that's the fun part like when we're showing this off I'
m like hey what version excuse me what version is running uh I can show that oh I'm running two different versions and I
can do the canary I can send 20% of my traffic to version one and I can send 80% of my traff version 1.1 and I can show
it and I can do really cool things and I can tie it together with that info and having the multiple deployments so that
work I didn't I didn't see it yeah it I mean it certainly generated the right version and so yeah I should change this
if I'm going to do that this is this is my pattern and that it's old it hasn't had updates in years but it still it ain'
t broke yep and I've been using it for that long and yeah I'm not running into any edge cases really um except for
snapshots on Circle C for some reason the way that Circle C's build process checks out things it makes jayger feel like
it's on a snapshot so it label things wrong so I don't do dirty flags and I don't do snapshot you can have it say hey
this is not a commit or this is dirty you've made a change to this build and it's not committed anywhere or you do a
snapshot where it's not on a tag and you can have it tell you those things in your builds right but I just have it go to
the next one so the way that I I can still get commit to main MH but I don't build the images until I say all my tests
are working I do a get tag V 0.010 and then right I can even be messing around and have that local it's when I'm ready
to Let's Take This in production get push origin tag B 0.010 and then it's sending that back up to my GitHub to my my
project and then GitHub actions and Circle C trigger yeah and that's that's the next step so that's that's stuff where
where I want to um get sort of a preview environment up and running running so that I like I saw your agenda I don't do
a preview environment so I have these different clusters and like right now I've been doing things on the cluster that's
on my laptop and that becomes my preview environment because I just build the image I throw it up to a Docker and then I
can have it running on my on my juice box and and I'm still working on it right I'm not ready to take it to production
where I might have a production but I didn't set up my tenants that way mhm so like if I make a change to what version I
want deployed right in a production cluster and on my laptop I didn't I didn't separate those two so by you bring
bringing that up I'm like oh how how am I going to tackle this yeah because I don't need a preview environment but what
I what I what I would but it would be nice to have um but sort of more so there sort of I think there's sort of two
steps to to that is one is um I only want it push to production and I guess if if I tag it correctly because what I
might want to do is is I've been you know all the commits we've done today are local I haven't pushed it up because if I
push it it goes to production and I don't I'm I'm concerned about Railways Java 21 support or lack thereof so I don't
want to push production but I do want to push it to GitHub so it's off my machine yep um so what I what I want to set up
is at least an initial like unless it's tagged with a full release or something like that don't you can run all the
tests but don't don't and all have to set up something Railway to make sure to watch out for for that yeah um but it' be
nice to be able to um with one step sort of push it to to GitHub and say I want to just make sure this works okay off my
machine let me check that on coab because it's free and then I'll shut it down uh and then it's like okay so okay or
maybe I do want a preview because I want people to look at the new UI and and try that out um well the other thing that
I I mentioned before we started was that generate the native image run all your tests against the native image you could
do that against a regular jvm image right but that pattern of my integration test maybe I don't run those here because
it takes two minutes to build that native image but maybe in my pipeline or my GitHub action I run my unit test and then
I run the integration test right whether it's got a tag or not just run the integration test and build the image run all
of those tests and make sure that it's doing what it's supposed to do right and I'll get i'll get a green on my action
right my get up action will say yeah everything's working and then maybe I decide I'm ready to go to production I do the
get push B tag so in my actions um I'm going to just point you to a URL uh I have those Circle CI and GitHub actions
where I show you how to filter don't do this unless it's got this tag spe tag right and that's what all want to do yeah
yeah cool but yeah this is hopefully this is valuable hopefully this is fun this this was awesome look at all the the
stuff we got done like that's great it feels good all right I want to do it again so do I we got we got stuff to do I
enjoy this I'll say it again I really enjoy hanging out and and I I know that I like to talk and ramble but hey you know
this is I I I to me one of the best parts about streaming with somebody else is we get to to to chat about stuff and
talk about stuff and and you know ramble or rant whatever that's that's the best part it's good so I am hoping that um
after a little bit of a break yeah that I really want to do uh a boten you know let's like go from the start and let's
just talk about it I'll tell you why I like it and we'll see if we can connect the do on some tests and y yeah and we
we'll have some fun I'm looking forward to that already all right well have a great vacation have a great time and and
in vacation and come back refreshed um I will try and all y all out there uh I'll be streaming some stuff next week solo
um hopefully some more stuff with with Mike on his song themes but I've got some features for Embler to work on um and I
might have to back off the the Java 21 change if raway doesn't support it we'll see if I can figure that out excited to
see how that plays out uh and hey Mike's there um hey Mike I've enjoyed watching Mike yeah at least this week I know
I've dropped in a few times you guys working on stuff this week yeah and so we'll we'll we'll so lots more streaming
folks um and uh that's it have a great rest of your day and thanks for thanks for helping out desan appreciate it all
right all right bye folks
