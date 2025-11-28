# Modernizing Spring Boot apps with DaShaun Carter

**Video URL:** https://www.youtube.com/watch?v=_E04EJaN95I

---

## Transcript

I'm G to stream it to kick and all right so we're live um this is the first time I'm using streamyard uh on this end so
hope you all will forgive any uh any problems that we encounter hey there deshaan welcome thanks for thanks for uh doing
this thanks for putting up with um with with all sorts of changes at the last minute so thanks lot we got this this is
fun I'm I'm very much looking forward to this I've been looking forward to this uh I hit the button uh inside a
streamyard that said uh stream gear channels so I hit the button so we'll see if if that works and this is I was
impressed I've never seen that before um so yeah I'm all the way around impressed so far already we just started um so
plan was uh I basically have two two apps that I figured we'd go through the upgrade one hopefully will be somewhat more
straightforward um a smaller app uh but still on 2.7 um let me go ahead and in two days that will be out of support
actually isn't it already out of support technically I think it's 11:24 so that's oh okay so they they they give you
like a two- day overlap between the the 32 release and then2 comes out yeah tomorrow tomorrow tomorrow yeah so one day
overlap right I'm I'm gonna go double check check my stats and go to spring.io projects spring boot support 2.7 and to
support 1124 all right so so just in time 3.2 all right uh and I'm going to set up little there we go okay so that's
also another cool feature that um streamyard really one of the limiting factors was like the layouts at first so I don't
remember when they changed it and gave you a little bit of flexibility on creating your layouts um but like when they
did that I was like oh is great yeah yeah I was like oh good CU because um I didn't I didn't spring for the higher end
no pun intended I didn't spring for the higher end uh streamyard so the resolution is at 720 and I'm usually
broadcasting at 1080 was y that's what it was so I did spring for that um and it was for the 1080 and that's why yeah if
I if I I have to decide if I want to want to do that because I'm usually going through OBS which is great if if it's
just me because then I have Ry really nice OBS layout and I've got the the chat and I've got the music in the background
and I've got the various different scenes that I can switch to um and I don't pay anybody anything yeah uh but uh bring
guests on board um I've done some pair streaming so uh earlier this year did some did a lot of pair streaming with with
James Shore um but it took a while to get that configuration set up properly because we were also pairing on screens and
things like that yeah um and I didn't want to put you through that extra like hurdle that's the thing I I don't have uh
yeah I don't have agendas really um I like bringing people on and I do it like randomly like oh hey like we're we're
having a conversation chat like do you want to come on and just be on and then we give them a link and all they need is
their browser if they've got a webcam mic they're good so there's no real setup on their side and that experience has
been great yeah and I don't you know I think have been paying for this the pro bucket um for a year or coming up on a
year I think it was January maybe uh but I really didn't start getting the value until just recently yeah where you know
streaming more and doing more stuff so yeah yeah definitely being able to bring bring folks ad hoc on on screen and and
uh not having that that hurdle of of any kind of setup is definitely definitely worth it so um let me go to the code for
this and I'm gonna zoom in even more so that way folks can can really read it and I'm watching the chat and now I don't
I don't maybe know your audience as well and oh hey we awesome hey what what no we no no dark mode uh for for this
stream nice try though I was waiting uh what what what what's the setup here uh no no no dark mode here um I'll I'll
I'll I'll refund your uh yeah so light mode is modern it's back light mode is back yeah like and that's the thing too at
conferences like depending on the room and the light like that's a serious decision you know like whether if you can
make that adjustment that's a big deal yeah yeah absolutely yeah I I know learning from having presented like it depends
on the room but usually like actually dark slides tend to to be better um but if they've got a really Pro setup and
actually sometimes the the light light theme is better and so it's it's Hit or Miss but when I'm when I'm streaming and
it's and it's later um uh than I then then I'm much more more willing to to switch to dark mode because I know folks are
sitting with a iPad in their bed or whatever yeah uh thank you so much for letting me know about my audio I I bumped it
up a little bit so hopefully that yeah let us yeah I haven't one thing that streamyard does not do is give me any sense
of audio signal for anybody which is something that I do get uh nicely with with OBS so if any of the audio is is not
good also let let me know absolutely if if like fonts or or other things are not readable because I'm having to bump up
my screen like by by it looks on my side yeah this is this is 150% so like 50% larger because uh because because 720
yeah um click on that hide button down at the bottom too of the screen yeah I guess I can do that there we go oops and
it it did some weird things before but now it's okay so what this little app is um this was uh one of those apps I
created because anytime I was doing some some date or time formatting I always like had to go to the documentation the
documentation is not that readable like one of the things that I'm really big on is as some of you in the audience know
is I'm big on examples and so um what I wanted was a little tool that would help me create the format strings for for
the the daytime formatter and uh and so what I want is something where it's like I could say well what does it look like
if I've got a two-year a two digit year and uh the long numericals for that one so what it does is it shows you so here'
s the pattern and you can basically just copy and paste it and eventually I would add a little copy copy link and then
it shows you some examples like here's what it would look like if the months are are short uh and here's what it looks
like if if the months are long and then and then basically some other dates and then you can play around it's like ah I
want the four-digit year EX looks better um but let's let's use a short numerical and see what that looks like and so
the idea is you could sort of play with this and and sort of configure it and then get it to to to what you like um so
it it's a pretty you know it's it does stuff um and this is actually in Spring 2.6 judgment here so this is Judgment
here at all um and and I was looking at like oh wow it's really that old I haven't I haven't touched this in in in quite
some time so I thought this would actually be um this would be a a good starter because it's not doing any database
stuff it's not doing any security stuff but it is doing some stuff um and and that'll be good to start the other
application that will that will probably take quite a bit more time is my ensembl application yep um and this one is is
going to be uh fun fun fun is the word fun is definitely the word uh so this one's on the latest 2.7 because I've been
I've been keeping that fairly up to date right um but it's on Java 17 although the uh yeah the hard things are probably
already taken care of if you're already on Java 17 yeah so that's be easier than we expect well the Java part will be
easy what the and I and I think we discussed this at some other point um the security is going to be fun and the
database I assume this but we'll see so there so this one is a full you know it's got database it's got OA uh against
GitHub for for security um and uh oh perfect so there's there's all sorts of all sorts of good stuff um the nice thing
is is of course since this is me is all these apps are tested hey Simon welcome that is so cool like so you're you're
able to see here in the comments you're you're seeing comments from from my stream as well and I'm Overjoyed that's
awesome Robotech hello Simon hello we're glad that you're here Happy Thanksgiving very beautiful uh so we so we l
mentions uh let me find that so we l mentions I assume he's referring to the date formatter um I remember reading
something about Y versus U and every time I look at it I'm like oh okay and then I forget about it so I think there's
something about Y versus U in terms of the year but this right and yes tomorrow is is Thanksgiving here in the US so
thanks wishes so so where what should we do where should we get started so what I normally do uh in my role like this is
a big part of me like when I see that 2.6.4 uh I want people to be on the layest and greatest you know the 3.2 is coming
out tomorrow uh so uh Simon knows it I I want you to go to the um open rewrite docs uh so docs. openen rewrite org and
then go to there's a recipe catalog on the left uh recipe catalog H go to Java there's a bunch of recipes in here for
all sorts of different languages and then on the right go to Spring and then we're g to do spring boot 3.x now one of
the cool things I want point out is like yeah this is uh very very new I got the I got the note yesterday from Tim to
beat yep I saw that note pushed that I'm like wow like thank you so much how cool is it that when that release comes if
you're paying attention you can have automation that goes and upgrades all the version upgrade all the Palms right the
spring Cloud meme uh so we're going to not go to 3.2 we're going to go to 3.1 and then 3.2 will next day so do the maven
spring boot up go down a little bit Maven to Spring boot 3.1 that's just the properties that'll just do the properties
but the other recipe will do everything so scroll down a little bit it says migrate to Spring boot 3.1 ah I see up one
more probably work I just changed my local Alias for that uh but if you scroll down uh are you using Maven or Gradle I'm
using Maven I am I am a gr I am a Gradle hater I'm a Gradle hater I I don't hate Gradle I think Gradle got its uh its
use cases and I understand uh but I'm also a maven fan and I'll tell you the number one reason why because of the schema
because I can take a maven project and I can make adjustments to it and know what the results going to be because of the
schema exactly exactly that's why I mean hate perhaps is a too strong I I have been traumatized by uh very very large
and complex Gradle code in in the project build file because it's just code and I've seen some Horrors and so I've been
I've been I've been traumatized by it which is which is why I I understand its need and yes there there's uh so one
application when when I was working at Apple we were working on an internal Cloud build build system and so they needed
they needed cradle you want to put iTunes you know deploy that thing and build that thing you're you're gonna need
credle uh but um yeah I'm like you I'm I'm I'm a fan of like tell me if it's right or wrong because there's an XML
schema and yes XML isn't isn't perfect and there's there's all sorts of issues with with that and it can be a bit
verbose um and plugins may not be as easy to write as as we'd like but um but like in the case of like an upgrade uh so
exactly just take that like gradles gives you that ability to customize yeah but it doesn't give you a consistency when
I go from Team to team project to project everybody can kind of do their own thing and that's part of it's strength so
when I work with teams that are upgrading with Gradle one of the things we and one of the patterns that we do is we
remove all the unnecessary stuff from the Gradle file and then we run the upgrade then we run the recipe and then we put
it back in like that's literally the pattern that we're doing y but we don't have to do that all we have to do right
here is copy that that shell copy that command line and you can run it right inside of your project you can run that
command line and let it go to work it knows how to upgrade from Spring boot 2.6 toing I noticed so so one thing that
that I just realized is it's going to try to run Maven but I use the maven wrapper yep so change that I've I've switched
I've switched all my projects to use the maven rapper because um especially when I'm doing teaching or coaching it's so
much easier for for them to to just use the maven rapper yep in instead of trying to install and upgrade of course with
SDK man that stuff is relatively straightforward but then if they don't have SDK man installed then they got to do that
St SDK man and now you're reminding me to go look do my SDK update and see if there's a new version of java that I'm
looking forward to I'm looking forward to Liar new uh 2.0.1 plus 15 is one to have plus 15 crack support oh so that's
what I'm looking for and I don't think it's been updated yet all right so let's see what it did here wow so did quite a
few CH no not not a lot a lot let's see so change the Palm so it knows how to upgrade from 26 to 27 it's going to do
them in order so it's a nested recipe and knows how to do them in order and to change your date formatter so the date
format changes uh you can see that it picked up on those and it says oh okay we've made some changes here uh in your
test and in the controller so this is annoying to me oh so yeah yeah yep um I actually I don't you know there's enough
magic in Spring where it's like I I want the at autowired on my Construction to to tell the reader when they when they
when they're looking at it that this is the one that even if it's the default one that spring can figure out oh I I know
that this is the one is gonna uh it's gonna call but I actually like autowired um even if it's already yeah the nice
thing is you don't have to take these right yeah so we're it's not doing any commits we can go back and we can look at
the diff and we can see exactly what's happened uh and I will say that there are some dependencies that this will add to
your palm right and I normally just take out like the glassfish one we'll probably see but yeah it's so it's nice that
um I use junit 5 but I used junit 4 for so long that um my force of habit of creating my tests as being public and my
test methods is being public When J unit 5 came out you didn't need to do that anymore uh so it's nice that that the
test should not be public yeah Simon points out Simon uh is awesome I hope you guys get to meet someday he says the ree
compeition is also available yes yeah so so I actually used um way back I actually have a video of me doing some of the
open rewrite stuff to upgrade a a spring boot 1.5 project to Spring boot 2. whatever at the time yeah uh so I have a an
old video that perhaps I should take down but but basically uh it works I've been using open rewrite for for a while and
following it and um it's there's some really nice stuff you can do if you if you really get get into it yeah so thanks
for pointing that out Simon so the you know this recipe hopefully this works and and your test pass and everything works
and we're good to go uh and again feedback from the community uh somewhere between 15% like if you've got you know your
Enterprise org startup org and you're trying to stay current when they first learn about open reite and I first show
them this particular recipe um and it's you know I've been doing this for about a year right since spring Bo 3 came out
and about 15% is on the low end 15% of their portfolio was able to upgrade automatically using this recipe and the high
end was 70% of their you know so they were just able to go click the button and go and 70% their stuff is upgraded
normally when we do the upgrade we show like hey here's the other we didn't just get to the latest and greatest which is
like your security right oh now I get patches right it's not it's not that you get all the benefits that go along with
the upgrade and we show them like your performance and latency and all that other stuff so now your your application
should be ready to go and now I would say run your tests yeah it's got to finish downloading everything right because I
don't think I've had 315 on this machine before there we go fantastic so I I do this this exercise so often that I kind
of you know the first thing that that tells me that 315 is available is the recipe right right that's the thing that's
oh like oh yeah oh 31.5 came out today and there it is now it's doing all the good indexing so that command that you
just ran I have that set up as an alias because I do it so much like just as part of my normal day-to-day MH I'm I kind
of struggle with where that responsibility lies like for me it's a nice enough tool that I can just do and have it
automated locally but I think there's a lot of like platform teams that want developers to run run this and then this
and then this and then this and run all these things right before you send it to our Pipeline and and I'm kind of I
think it can't be one or the other I think it has to be both is my where I've landed like maybe I don't want to do a get
commit every time to get all the validation I want to be able to run it locally but if I missed and if I didn't run that
sneak or uh the upgrade then I want my platform to catch it like Don't Let It Go without having all the the bells and
whistles so the responsibility like yep I've seen it both ways but I think that it should be in both places all right we
got all tests passing and we got 315 awesome fantastic so let's see um let's see what the changes it made yeah so yeah
so this is this is the one so I took out my autowired but I'm going to put it back because I like my autowired you're
you're allowed four oh that's interesting okay because uh it used to be you had to specify the value because it wouldn't
have the information at runtime yep um now you don't a yeah there's a spring benefit there's a spring upgrade I was like
hey yeah you don't need that well I think it's it's related to to version of java I forget which version you it used to
be if you turned on debug during compilation then it would put the symbols in the runtime and it would be accessible
through reflection um at some point I forget when that became probably with Java 17 is my guess I possibly I don't go
deep on the jvm but I know that spring boot 3 uh rebased with Java 17 right so but I'm pretty sure that was available be
because I have I have prob it might have even been 11 I I want to say but anyway it's nice that it that it noticed that
because that's no longer needed so that's cool and did the same thing here of course y so cool else public from your
test yeah so took out public in the class name and public for here um and that's pretty much all it did is totally fine
you know I have I have my my teammates whispering in my ears about don't use public unless you need to use public like
leave it leave it not public until you need it to be public yeah I mean for test it sort of doesn't matter because no
you're not nobody you don't have code calling your test so it's really more of a hey we don't need it it clutters things
up so let's let's reduce the visual the visual noise yeah but absolutely for code default to to to not public public
absolutely that's something I've learned over the years and we got more tests getting rid of public one of these days I
I want I'll I'll run the this specific recipe that the J unit five five stuff on some other projects because um I've got
a lot of Publix that we can get rid of hey it saves what one two three four five six it say seven seven characters per
per per line uh um so that's all all more tests fantastic and good old Arc unit test and tests and the version and let's
see so it added that's the one the jaxby runtime right um do I need that I forget what I I remember when when I first
upgraded something to that that was added but I forget what that's used by you take it out and run your test file that's
that's the that's the best thing right so the other thing that I find myself saying a lot is like the more mature your
tests are the easier this process is going to be everybody's like Oh how we how do we know if it's going to work like
how do we know if this upgrade is going to work in production well how do you make any change and know this is going to
work in production right if you don't have tests if you don't have tests you're gonna have to do it manually and then
you're G to be nervous about making any changes and this is how Legacy code becomes Legacy code um it's it's that it's
that lack of confidence that really hurts your ability to to keep the code sort of fresh and and new and and and uh
there's a term that Eric Evans in mainen design uses called Supple I love that idea of like Supple code that's just
easily changeable but it's comfortable to work in and if you're scared to make a change um and basically your suggestion
to like well comment it out and try it out is very much a tdd mindset a very experimental mindset yeah all right guess
we don't fantastic hey everybody's showing up this is so good like I said I've been as streaming a lot more lately and
it's been fun having the community uh I enjoy like I said and I always say and I I've always enjoyed having you like as
my cooworker uh on the stream so that's just what I'm trying to do a lot of times I'm not you know chatting or I'm even
cleaning up my messy office like just to have somebody there uh it's nice and I I remember a handful of times where I
was like what do you think about this and you'd give me a 2 and a half minute thought and I was like thank you thank you
so much so I I'm trying to do that same thing that I got from you like just I want to be there as uh help somebody else
sometimes we're going to learn something we're going to show something cool but just to be present and yeah in the same
kind of mindset like Hey we're remote you know I don't have somebody you know down the hall I'm not passive stuff and
that's what I liked that's what I like doing I like always having some live streams on and uh live coding is my favorite
thing yeah I love it I can I can do it passively and that's what I'm trying to do so yeah I'm glad to see everybody here
showing up yeah so Simon yeah I love Arc unit I've been using Arc unit forever um so my arc unit test uh is basically in
this is Nish this is actually can be cleaned up I'm not going to do that now but basically this can now be like much
much simpler because there's um although I find the terminology that AR unit uses for some of the predefined
architectures to be a little bit it hurts hurts me as a as a very pedantic person um because they call it uh onion and
onion and hexagonal are not the same thing they're very similar uh but they're not but anyway this what this what this
test does is basically ensures that I don't have um dependencies in in in the wrong direction and that uh hexagonal can
be looked at as a layered system so basically this this test just en forces that so I don't even though I teach this
stuff you never know when you make a mistake and and you want your test to catch stuff right that's the whole point of
having them so yeah I love Arc unit fantastic all right so success success are we feeling good like we feel like we did
it I it it all looks good that's wonderful so let's go ahead and actually commit it so I'm going to ask a question um I
noticed that you have the ver version versions oh uh I want I want a better way to to do this in some kind of automated
thing but I haven't figured out um like there are two different kinds of versions like this one is like I bumped just
because I've made a significant change even though it's not a significant functional change so maybe really doesn't
deserve a new version but I I manually do it when when I make when I make a a a functional change um but for my more
like my ensembl app I actually really wanted to do a new version every time I deploy and I've played around with some
things and I haven't and I wasn't satisfied and I haven't looked at it in a while um but it'd be really nice to to every
time it actually gets push to GitHub and then successfully run all a tests and then successfully and then basically then
deployed um like if fails a test on on the GitHub action then I'd want it to to not not bump up that version uh so that'
s the long long answer um I I'm going to go look I have in the past I used um the GitHub Shaw was version that's all
that I cared about like hey this is what it is uh but it's hard to like track than like changes and do change logs and
all that kind of stuff made it really hard so as as a you know startup mode and just like get go forward get to
production it worked y for a while yeah uh and then as I started learning more uh I'm going to another one of my GitHub
repositories I have this initializer Plus+ you know I talk about having this pattern up I want to be able to do it
locally and have it on my platform right the the the conventions around like versioning um I'm going look it up I don't
remember what it's called exactly but I have this plug-in for Maven that only it it creates the version so I said my
version to zero that's what's in the P file and then it uses this plugin to determine the version based on the GitHub
tag so if there's a tag there it it gets that tagged version 0.0.2 if it's not a tag I can say that it's 0.0.2 snapshot
I can say like hey it's close to or it's dirty like hey it hasn't been committed so I have this like consistent way of
versioning and then my version is always managed by the GitHub tag so it's just consistent I don't have the manual um
process of editing the Palm file I don't I'm not a real big fan of the maven convention for releases yeah I haven't done
a lot of releases with Maven and every time I look because I want to take a look at it I'm like oh never mind yeah I
think it was like three commits show up in your repository each time you do a release yep prepare for releas yeah
prepare for next for yeah yeah yeah yeah so tokes welcome back yes we're doing some some Java today I was doing python
yesterday uh and uh yeah we're today we're doing Java in Spring we're upgrading we're making sure that everybody's on
the latest and greatest and tomorrow's Thanksgiving and there's going to be some new releases so on Friday I'm gonna
ping Ted and I'm gonna say hey like have you ran the recipe again like let's let's get it up to latest and greatest
that's one of the metrics that I try to get people to think about is like hey when 3.2 comes out how long is it going to
take you to get your app production yep uh I don't have a mechanism that says oh yeah there's new release go and run the
recipe but when I do a commit right I want to make sure that you're on the latest and greatest yep so just like what I'm
doing with that command line uh as as I'm doing changes the goal would be to have some automation that's going and
checking you know when there's a release or have some event like hey yeah a new spring boot version comes out like go
and fire it off across all yeah that's that's possible I'm just not there yet y yep so should we uh 315 I assume works
with 21 right it does yeah so should we upgrade to as well upgrade before you do that how about do this run your tests
do it from the command line see how long your tests 17 throw a time in front of that command don't do that a lot so what
do I do just say time yep time space then do test I don't usually run it from the command test I'm I'm I'm so out of
pract whoops I and I misspelled Maven that's on me go so just you know it's a it's a not real yeah scientific but hey
this one it took 1827 seconds now upgrade the Java thing yeah so I saw I saw this uh in I saw this commit and I saw I
think it was even you Simon who was was uh posting about this and um I I have to say I'm I'm like just thrilled that
Loom is is is finally here and that spring will be able to to take advantage of it and uh we can stop talking about
reactive uh I don't know I think reactive has has its place but but I think it's it's going to be vastly reduced uh in
in in sort of the use cases that it that it needs to cover yeah all right uh is there I assume should I run the open
rewrite to upgrade the 21 I don't um I don't think it's going to do much I actually I don't know if it if there I think
if you uh let me think here uh from experience I think if you switch to Java 21 and then you rerun that same command I
think it'll upgrade your pal to Java 21 but I'm not sure I'd like to see that so if you SDK use Java which which Java
are you using right now uh uh I I at 21 21101 automatically yeah so It upgraded it It upgraded it to uh it upgrad spring
it didn't upgrade the the the Java um was it supposed to uh no I don't think so um and now you're making me think
because I've been doing these demos and I'm wondering if if I even went back and changed the Springs Java version to 21
when I was doing this I don't think I have been doing that so yeah let's see if there is a recipe for version let's see
upgrade migrate to Java 21 this is in that's seven to eight uh there's a recipe I'll throw it comments here's the recipe
that I found change Maven Java version property values to 21 so there's a that this one so here's the migrate to Java 21
yep that's one we want and then if you scroll down it'll show you all the recipes that are included in there let's go
grab that yep let's rub it let's so 1827 was what we had before but we were using Java 21 but we didn't upgrade the
maven version so let's just see if this joining and we're doing the we're doing the recipe because we want it you know I
want these things to be automated yeah maybe that yeah we could have just yeah yeah so Carl we could have just changed
the number but I was curious what what else the um what else the recipe might do yeah so it looks like it looks like
that's what it just did it's like all right let's just change the upgrade so let's see yep that's all it did that's uh
um Gibs about the one hour a day of tutoring training like just do it like every rep is my answer you want to get better
at anything do more of it okay what happened failed uh I didn't refresh the me change this intellig should have
refreshed that it did but it didn't change that okay go oh interesting uh it didn't update argu it yeah so that's why um
I'm going to I okay I'm going to take some I think we should take note of this and and and uh have them add that to the
upgrade to 21 um not sure what what where it would fit but this is because uh Arc unit uh didn't add 21 support until
like 1.0 but is latest I think it's 1.01 let's go take a look ar um so there's a similar issue with lambach right
lambach well of course yes um even it didn't support even Java 17 until like 18.5 or something like that and you know
you you find these things that you run into but the coolest thing is that we were and I get goosebumps because I get
excited about this stuff the coolest thing is like we were talking about it and I'd ran into it enough where I'm like
hey and I I just I hadn't opened up the issue but I was talking about it on Spring Office hours and Tim to be was there
he's like oh yeah we got that it's already there y I saw that y okay yeah those guys those guys are great so it looks
like they change the that so I'm gonna take a note of this um and yeah like my mindset uh is when I run into this
especially if I'm building my career or you know my Enterprise on top of Open Source software um one of the cultures one
of the those kind of patterns that I see is the people that are willing to open up an issue when they find it whether
they have a a fix a PR for it or not the people that are willing to open up an issue when they find an issue are doing
better yes they are figuring out where figuring out how how to describe how to write better how to communicate better
they're moving forward faster uh so this is one of those patterns that yeah I want to I want to model and I want to show
so I'm and oh they changed upgrades of dependencies yeah so so I don't know if they have a recipe for for Arc unit
upgrade um maybe not but that's that's what's needed here because actually there were there were a bunch of changes uh
and you know that's the kind of thing this is yeah my head this is kind of the thing that's simple enough where I could
go write that recipe and I could contribute something back so I'm like oh maybe yeah so what did they what did they
change for for that um got release the yeah so 10 changed a bunch of um I'm not sure I want to spend time trying to
figure that out no oh so here analyze classes did it just change the I wonder package let's see no I do not see a recipe
for it and then this is the thing right like oh well there's no recipe and we're stuck and the thing that I I'd say it's
like okay scoot on continue on you know get the benefit of what you've got you don't have to upgrade this now if you've
got time sweet but I'll bet you there's a bunch of other stuff that you can upgrade in the meantime yeah so let's yes
yeah let's let's If This Were Me on my own I would I would go go push forth but uh I think this is offline from what we
want so let's go and let's go and Java version 21 let's roll back fun but that's cool that that uh uh we found some that
that open rewrite can can that you or I can can help uh open rewrite get a recipe for argu upgrade because I'm not I'm
sure I'm not the only one at least Simon and I are are are using Arc unit yeah well Arc unit is and ARG really Spring
moduli right exact I was just about to say it's it's a it's a core piece of that so so so for me right that that makes
perfect sense to go and do that out but yeah this is the the same advice I don't want people to get stuck on the one
upgrade uh where oh hey okay I can't get to Java 20 but you got to Java 17 you got to springb 3.1.5 you're getting tons
of value exactly let's go on to the next one let's see what else we can move up because there is performance benefits
there is other benefits you're getting um even though you're not yeah I mean just if you know if this was a Java 11
project or or yeah Java 8 or even a Java well maybe not Java six but eight so I can I I without naming names uh I have
worked you know in the last year worked with companies that are still using Java 5 uh and I've got on that computer
that's right there I've got uh web logic running uh andic one of those you know not with the open rewrite but there's
another project that we might look at in a little bit uh the spring boot migrator that can take your ejb your je uh
applications that are running on something like web spere web logic and it can actually migrate them and convert them
over to a spring boot so tests are passing oh really you're running as a spring boot App instead of needing the
middleware like web logic or web spere oh that's cool isn't it amazing like mind blown that's that's that is incredible
yeah and I I will I will say the joke uh that honestly what we put out um we're we're kind of better at upgrading je
apps over to Spring boot than we are at staying on with our recipes for spring boot just spring boot but we're working
on it and wonderful so Carl mentions the display dependency updates Fantastic look at all that stuff is downloading oh
my gosh um do you ever deal with what is this oh that's cool that's oh that's nice um so I use I use uh I use caffeine
for for caching because caffeine is is is is a nice little cash cash mechanism so it looks like there's an update there
um and I use this uh so one thing you may not have noticed is uh when I was running format hero one of the one of the
cool things I added it was one of those oh let's try let's let's try this out is this identifier when when I'm using the
deployed version um it's one of those things where if we're collaborating on on our datetime formats Y which is kind of
a ridiculous thing but but the idea is uh so it generates these human readable IDs that are that are unique um so I can
say hey Deshawn go to go to format hero. and use the ID average Stingray 56 and instead of some you know really long uid
that's impossible to read That's so that's what that's what this does oh I feel like I've got something else from k k
kler I feel like I've got something else from that in my stuff somewhere but let me write that down real quick cuz I
like that so yeah so this is definitely useful to run I think as as part of so thanks for mentioning that Carl um as
part of you know the recipes are only going to look at the stuff they're going to look for yeah but you may have have
other things so if there was a arch unit recipe that you know you would run them in order like hey I want to do these
and you can kind of like stack them right and as you find the the patterns in your repositories you you're gonna know
like oh yeah I gotta add this one to my list remove duplicates remove class fish Etc Y Cool all right so I think we can
declare the easy one format hero done we did it uh and did I push it I pushed it so it's actually probably deployed let'
s out so so tell me I'll have to go find where it's deployed where do your thing where do you deploy things so I have I
have three different places I deploy things um uh one of them is I still have some stuff on Heroku that I want to
migrate off because it's getting a little expensive um uh and Railway is where I have my ensembl tool Railway where I
have um did it deploy format hero should not have done that so I pointed so I was trying out this new one I think was
maybe even mentioned in one of one of your streams or somebody's stream mentioned uh KOB um as a oh yeah yeah that was a
Thomas yes Thomas right yeah um and that one it's very much you know these are all platforms of service right I don't
want to deal with like AWS and even and Azure is too expensive for for for a little guy like me um I don't have Cloud
money I have raspberry money uh what's that I have raspberry pie money yeah and um so realway is nice uh this platform
is a service and it and right now it does everything that I needed from Heroku including you know hosting a postgress
database and and things like that it just works really well um and so kab is is very similar although it's a little bit
behind the database stuff is not quite there uh and so I was trying it out and I basically had deployed format hero to
it um let's go I'm over here taking notes like I'm it's not being recorded but is being recorded we're hanging out like
one of the things one of the other patterns that I've like to adopt it's like I like to record these conversations so I
don't have to take a bunch of notes I record it get a transcript from it and then I've got it and keep it and I can dump
that into one of my llms large language model I can ask I can ask my own context questions he have ever talked about
railway yep yeah that's something I want to do because I've got um have 600 hours of streaming video yeah and I'm like
where the hell did I do X I know I did this change of this where did I do it and it's all now the stuff is fast enough I
can do I can do it locally I can I can get it transcribed locally so we're doing that so now being able to to dump into
an llm where I can say hey where where did this happen that that'll be nice yeah just having that so uh Josh long and I
uh last week we worked with dwan Lightfoot uh who is lab every day on YouTube and danan is a developer Advocate over at
AWS he made this YouTube analysis assistant for his YouTube videos and what he what it does is it goes and grabs the
transcript from his YouTube video gives him a description gives him a summary of it gives him the SEO tags that he
should put on his YouTube video yep and now it also generates a thumbnail using get generates an AI thumbnail where he
doesn't have to do anything you just point to the URL to the YouTube video and it gives you everything that you just
copy in and edit paste and of course we're going to automate that part too where it updates the video in your you know
using the API in your YouTube so boom get this uh cool I I need the I need the thumbnail generation because that's the
that's the part I actually really part that I never did and I never even spent time even though you know Dan Vos you
know got all this like yeah you got to do the thumbnails and this is part of his thing I never spent any time on it last
week when I was first taking D's project first bin I grabbed a video that I that had been out for 4 days mhm I had 24
views and I I have my normal like I'm going to share the video on these plac had 24 views in 4 days um I I ran it
through his analysis tool and got all the stuff I edited the same video I just put the description the summary the SEO
tags and the uh and the thumbnail and now it's at whatever 300 views four days later like overnight it had 200 views you
know 10x whatever we were doing so I was like okay proof done like I'm doing it and then I showed that toos little AB
test there yeah yep and then Josh is like yeah we got to do it like it it just works so great but it originally it was
well the other piece that it does is like it says from the transcript you can ask it like what's the best 30 second clip
for like a short or a Tik Tok and it gives you a 30 second clip that you can be like yeah this part where you talked
about this grab that because it's a joke and joke is funny like right right it's just it's it's great so we're having a
lot of fun with that making this whole job easier for the videos and all that kind of stuff so yeah yeah because I've I'
ve got a lot yeah so I've got like hundreds of hours I um so I've been using I been using descript for for a long time
and they recently have bumped up the the the AI stuff that that they've added and so now I can dump it in and it does
most of of what you describe like it'll generate um it'll generate a blog post it'll generate uh a YouTube summary
including the timestamps for all the different chapters um and I I did it for I I uploaded a recent stream uh and the
timestamps IT generated were like oh what happened here because there was like a big big gap between the chapters and I
started looking at it and um I realized oh this is where I I I was challenged by my uh viewers they they redeemed the
right code without a test and so I went off and and and wrote um uh basically an implementation of storing information
instead of in a database the easy way I did it the hard way by storing it as Json in a file and that was without tests
and as you might be able to predict it went horribly wrong like it was it was it I ended the stream and it was it just
wasn't working um I think I eventually got it to work and I'll have to look at the next stream but it was one of those
like oh that's why there was this big gap because because I went off the rails that's really really neat um I also used
descript that's what I used in the past um but again like the the extra time uh I was looking for like hey I'm done
click the button and do all the things right uh with descript from what I understand I still had to download the video
upload it what I like about dript is I can remove all the ums and a yes that plus I can also on the export I can have
the the voices so I I got the speaker name so yeah as I've done many many of the the spring off hours it now knows who
Dan is and who desan is I don't have to tell it who this is it's just like oh yeah that's Dan so that's been wonderful
yeah yeah so I I run a book club and so every every week uh we were on Zoom for two hours we're currently reading um uh
learning domain driven design and um it's great so basically we record it and uh descript generates the transcript and
the subtitles um things like that and you can give it a glossery of like here are the common things that I terms that I
use like dto and intellig and things that it would normally not not get get correct uh and so it corrects those and and
um and I've been playing around with the hey can you summarize the book discussion and it comes up with some sometimes
it gets a little off uh it's like that's not quite what we did but um but it's been it's been really nice for especially
for people who can't make every every session to be able to to catch up and and not have to watch the two hours of of
discussion yeah yeah you can go and you know hit the the fast mode uh but you can also you can just share the transcript
yeah so I I share the transcript I share the and the subtitles are there and I publish using I paid more for that you
can I published the the two-hour thing using descript the descript has its own it synchronizes the transcript with the
video as as the video is playing um so that that's that's really publish to YouTube from no since uh it publishes to
descript own oh got own service um and so that means a lot of the the rendering work that or whatever work it has to do
is is not happening on my computer so basically I just tell it do the thing and and it creates an unlisted link so
because for the we have our discussions where we don't where we're like if you're part of the book club you can you can
find out but if you're not We're not gonna we're not going to put it up on on YouTube very cool so um yeah so we
deployed and and this is all still working and uh this is up on Railway fantastic and I love you take stuff for
production yeah an important part all ensembl so for those of you who uh are not familiar with this tool so I so with
the video that I've been up that I uploaded yesterday um to YouTube I I've been up been well behind in uploading my
streams since I don't normally stream to YouTube I normally stream just to Twitch and then I basically want to do some
very very light editing before I pushed up on YouTube it it does mean that I don't uh that it takes me a while so I just
uploaded episode five of me developing ensembl which was uh like two and a half years ago so it'll be a while before I
get get up to date so right that's the kind of that's kind of the uh how do you simplify that right the thing that I'm
learning uh across the board it's not just in this developer at it like the people that are automating the boring stuff
y are the people that are able to do more of the important stuff so and there's a trade-off right like how much time do
you want to spend automating this thing how much is it really going to save you well like you're two and a half years
behind yeah right so how much value is there uh if you had you know spent a 100 hours on on the automation how much time
is there and I know that it's hard right and that's one of the things that's kind of kept me at arms length from
streaming more often it's like there's a lot of work work and people don't understand how much work that is but the
thing you just mentioned is like the idea of on Twitch is where I'll do my live stream and then I can edit it and then
deliver an an edited version to YouTube descript could make that really really easy you could cut out the the sloppy
parts and from the transcript you boop boop boop you could ask the a like what are the boring Parts which parts should I
cut out and go there's a there's a ton of opportunity here to take some of these tools and I I put all of this AI stuff
I'm I'm in my head it's just the new spreadsheet yeah it's going to be so common these models are going to be so common
that it's just the new spreadsheet you know uh what is the uh I forget the one tricky thing from Excel anyways like yeah
just the models Which models do you have you have access to it and go and it's not even we're not even going to think
about it yeah what's what's slowing me down is is I don't even do like I yes I load it into the script because it makes
it uh easy to do everything I need but I I don't even like for the streams there are some streams like I'll do some some
pretty fine editing um but these I just need to to get them up and actually the thing that takes the longest time is
just rendering an upload um and that is like yeah I could automate it but I'm only going to render and upload one at a
time so so so automating isn't the problem it's with the actual so I'm glad you mentioned um uh the automated thumbnail
generation because that's the thing that actually I need to automate because uh especially like I was looking at like
okay I did these other thumbnails um so I did these thumbnails and I'm like where the heck did I do those thumbnails
what application did I use to create them because I wanted a consistent look and I realized oh I remember which tool it
was oh that's painful because what what I had to do is I basically took you know took a snapshot from from the stream
and then took that and then overlaid it with things and it's like that's too much work um and so if I could automate
that uh show you some of the output go to and so what I did is I basically went into canva yeah uh and I just in canva
and if I could I could do it one step further of just saying here's the video it's Desa on YouTube and I just want to
show you I did it for a couple of them I haven't gone through and automated all of them uh but if you go to uh yeah
scroll down past live streams you can see uh which ones were like that one and it and it generated it purely from the
transcript of the show now this one over here the this third one the YouTube analysis assistant I took the the head
shots of me Josh and danan and I said here's me here's Josh here's danan here's the transcript and that's what it came
up with oh neat I was very very pleased I'm gonna give that a shot because if I can because I I'm generating the
transcripts anyway because I like to to use the script to generate it because like I said it it it knows my glossery in
language better than YouTube does um and so I'll already have the transcripts and so if I can just say here generate a
transcript for that one of the um early on that's cool uh back when I was on mixer uh one of the one of the guys that I
watched and I watched him code it he was coding this thing for the transcripts where it was pulling out words like
kubernetes in intellig and and he was building this yeah this bucket of the words being spoken you know from the audio
right here's how all the different ways I say kubernetes katees t right idea like and he was building up this gloss so
that when he uploaded his transcript or his video it knew how to pull those things out so he showed me some of these
things I was like and that was one of my favorite streams to watch as he was developing this and every stream you know
new technology comes in you do it you pull those words you feed it back and then it transes and it has the ability to
pull out those words but he had a nice little automation around that like what were the new words that came in this show
right that it didn't do right and he's like boop boop boop and then he refet it and then it worked I was like just nice
very very cool stuff yeah but I'm just scratching the surface I don't know yeah yeah so if I can automate the the
thumbnails um then then I'll then it's just a matter then it's just a matter of of of rendering letting my computer
render and so and that's now all done through chat gbt right or yeah the open AI has that but you don't have to use open
AI right what we're doing is we're making it so you can run those models locally so you don't have to go user service a
lot of the models are are public yeah yeah I know we're I know we're on a bit of a tangent it's totally fine um and
while we're on this tangent uh have you seen um the uh so um I don't have but basically you you can use this you can uh
you know create a UI say that you know here's my UI and here's a button and it says you know uh then you can basically
all right go ahead uh oh I don't have my API key in here so it may not let me do it yeah so you basically send this to
uh it'll it'll send it it'll B take a snapshot send it to to uh chat gptv um and then generate basically HTML Tailwind
UI for it um I have this running somewhere I have to figure out which tab I'm in it might actually be on my laptop
awesome but uh uh it's it's fun to try out and it's actually really nice because then you can say well make this larger
make this background green and you can start commenting on it and and building it up um and so so the author Steve Ruiz
has a bunch of samples of this on uh on social media um Steve Ru is R you Iz awesome yeah good stuff and so this is the
kind of stuff that like I always thought of of you know this idea of of exoskeleton right you know allows us to jump
higher faster SA safer I'd like to see more safer in this kind of stuff but you know jump higher and faster but it's
still we're directing it and and we're just more powerful because we're getting getting all this assistant because like
you know yes I could I write the the HTML for this um could I go into Chad GPT and describe it yes I could but it's
actually really hard to describe uh in a sense you're describing an why would you describe an image so that it can
basically like just give it the image here's what I want it to look like go generate the the the HTML um and that'll be
really nice uh to to incorporate into the you know the workflow because because you know I could do this but like it's
like you're saying it's like it's time that that kitty looked over the so let me uh let me second oh wow it's already
filled up okay what was filled up uh I just want to check that before I put it on stream that it was okay to put it on
stream so getting back to to ensembl so ensembl is a tool that I created um because one of the things I do with my
community uh with people who've um purchase my various courses uh is we run a weekly Ensemble basically group
programming uh anywhere up to five people are participating and um we're all connected in zoom and we basically work on
an an application and are just constantly adding features using tdd doing lots of ref factoring so really it's it's one
of the best ways to learn is to do and get immediate feedback from someone like me to say hey let's let's try this let's
try that but also we everybody learns from everybody else and so um I think ensembling or what's sometimes called mob
programming is is my favorite way as as an educator to to get people to really do deliberate practice deliberate
practice is required to get better but it it's not enough to just practice you get need to get that feedback so that you
know you're not learning the wrong thing yep um so anyway I needed a tool that would do things like well there's a
capacity of five because more than five people it it it starts to to to break down in terms of people's attention and
and and things like that and so I wanted a tool to to help me create those and schedule those and also create a uh
integrate with other services like create a zoom um Zoom meeting for me because speaking of automation it's like all the
stuff that I had to do manual I had to go into Zoom create a meeting I had to make sure I get the date and time right
and and put all the stuff in and then I would have to send that Zoom link to people so that they could actually connect
uh and then uh I you know people would say oh I can't make it and so they'd have to tell me that they dropped out and so
I'd have to say hey now and it was right is wasn't a lot of work but it was just a lot of tedious tedious things so I
created an application um that that basically did this for me I did not so I watched you develop this I didn't realize
that this was something that your community got as part of your your training and yeah gooseb that's amazing yeah and so
um right now I'm only I'm only doing it once a week but sometimes I'll do multiple ones and we have sort of different
different you know sort of like a Multiverse we we always start from from the application we built in in the course
which is basically a blackjack casino game um and we we build on now it's multiplayer and now you can place bets and now
well in this Multiverse we did persistence in this Multiverse we didn't and so we're gonna actually do event sourcing
for for uh starting this Friday um and so that's going to be really interesting uh because I haven't I haven't really
done a lot with with event sourcing but anyway so that's what this tool is um and all and and allows me to uh and the
most recent features I added over the past couple of months was this ability to have uh what we call Spectators um where
you're not in the rotation so you don't get a chance at the keyboard or or what's called navigating or or directing uh
but there are PE but you you actually get quite a lot out of just observing just just just watching um and so uh again
it was one of those things where it's like for a long time I would be say hey we're filled up but if you want to
spectate send me a direct message and I'll send you the link and you know it's like nope and and so actually the uh the
episodes where I added this are actually still on Twitch eventually they'll they'll get over to YouTube but they're on
Twitch and um you know and so so tded it and but but it's on 2.7 that's amazing so so let's see if we can upgrade it so
let's let's go for it this a great project and so this since we use there's a lot of time a lot of effort in this
project so it's not true yeah and so one of the things I've got of course is um uh lots of great tests uh and so so I
use postgress um so early on in the project before test containers was a thing yep um I used H2 right because that's
what you did that's what you did uh because uh but then you know the pain and I'm using Flyway for for my uh database
migrations and the pain of keeping two different schema definitions H2 and postgis in sync was not fun and then when um
when I was able to start using Docker and then test containers made that made that much easier uh it was it was just
like this is so tests the tree right so things are working yep all the tests are passing and there's some database tests
in here yet the whole thing ran in in just a few seconds which is just the the the The Wonder of of of test containers
and automating that has been such a wonderful thing awesome so you did upgrade a test container yeah so basic once test
uh I've got a test fantastic that uses has a couple repositories and and uses uh yeah use test containers fantastic it
just works all right let's keep going so here's the thing where I always default to running that that same same upgrade
spring boot 3 recipe that's just my my normal uh it's probably not going to do a whole lot for us here it'll upgrade
some things it'll upgrade the maven pal and the version it might find some properties uh that need to be upgraded and
it'll probably throw in that glassfish uh Jack be that may or may not Beed but that's kind of where I start right let's
let's start let's see what what works what doesn't and then we'll we'll dig in because there are some other things that
we might want to uh dig into but so I wonder if will it clud the security five six ones uh it'll do some but no okay
okay that is so there's three buckets of things that are the hardest to upgrade uh that we run into like at at scale the
things that we run into where people get stuck and and they're like well what do we do uh the first bucket is the
internal libraries and rappers this is the one that we run into the most often where hey I put a a wrapper around the
spring boot parent pal you know it's my enterprise. org's parent pal and everybody must use this and that just
oftentimes it doesn't provide a lot of value but it does become a big blocker for trying to stay upgraded because like
tomorrow spring boot 3.2 is going to come out on Thursday or tomorrow yeah tomorrow spring boot 3.2 if you got a parent
Palm you know in your org you've got to then upgrade the parent pal and then you've got to go and upgrade everybody you
can't you can't upgrade so let's just say it wasn't 3 out2 let's say it was a cve right that was being fixed right um
your parent Palm process becomes the blocker yes thank you for the calendar. spring.io uh the parent pal becomes the the
bottleneck for all those upgrades and when I talk about how long does it take to go from hey it was released to its in
production that just adds another block that isn't providing a lot of value uh and I understand where it came from and
oh I want you to use these dependencies and you have to use our internal library but we can handle those in different
ways like recipes or you know I use these spring shell projects that like hey make sure that you've got our certificate
make sure that you've got our you know yeah whatever it is defined and I make that a a shell that you can run or a
recipe that you can run locally I also run it in my pipeline but not as a parent bom there's other ways to fix it that
are easier to manage and and less of a a problem that's the first bucket the second one is Spring Security right and
what what happens is people are looking for the one to one uh like oh hey this I'm looking for another web security
filter chain property just like this and there there's not it's been simplified and I don't I don't know it I'm not
going to know all the answers but I know that's where there's going to be a lot of problems uh and then the last one is
data hibernate hibernate upgrades those are the three buckets that we run into the most all the other buckets that we've
ran into have been resolved by the the people that are submitting new recipes all the time over to right and yeah
they're not problems anymore but those are the three buckets that are consistent yeah luckily I'm um I'm expecting the
spring data since I'm actually using spring data jdbc because I'm a I'm a big fan of of of uh Aggregates and just spring
database was designed specifically for the type of applications I do which is domain driven Aggregates um it's I I don't
I don't need dirty checking and and all that other stuff so so it's it's uh when that came out I basically switched
switched over to it um and that's been just great Carl added the whole like defining bombs uh to get your dependencies
as a and I that's something that I totally need to put on my list of you know options yeah thank you for that reminder
that's a good one yeah yeah bombs are are something that it's like I know enough Maven to be dangerous um but but sort
of it's been a while since I've had to to work on projects myself in a in a sort of larger environment where a lot of
that stuff um or some of that stuff like the parent Pals you were mentioning come into play so yeah so Simon asks about
you that's actually um uh I have I've played around with it on and off for many many years um and for some reason in my
head that's something that I associate with you really yeah maybe maybe I don't know if you did it on stream or
something but for some reason my head I put you in that bucket see here's where I'd love to ask my personal chat GPT hey
did I ever talk about J um uh I did use it for a project in 2016 2015 so that that shows you how how how long it's it's
been uh and and I've kept track of it and I've I've wanted it to use it here and there um and so uh one of the nice
things about sort of an architecture is with with sort of DVD and Aggregates is like each thing can can can actually you
can use polyglot persistence right so I can say hey for this stuff I'm going to use you know spring data JBC postgress
um and then for this stuff I'm going to use uh Juke and and maybe some other database or maybe also postgress uh and so
sort of that that freedom to to do that um while I probably wouldn't do that unless I had a really good reason in like a
real you know uh corporate uh project it's the advantage of these these projects is I can do whatever the heck I want
yeah um to add on to that thread that idea of I can have different persistent tiers uh we mentioned spring moduli this
idea in what's in my head and what I'm doing is I'm taking some of these microservice patterns where I had you know
gateways and securities and user service and product Service uh as a microservice architecture and I'm trying to pull
that back warm the kind of a rules practices is when you have a microservice it has its own data store you don't have
the the multiple Services relying on the same schema because then it's hard to update like how do you do that so in my
experimenting I'm trying to do this like hey I've got the user service is going to live in postgres and the product
service is going to live in my SQL and the every other service is going to live in reddis and like put those together
but it's still being deployed as one application and having all those different persisten years okay uh I don't remember
what it's called like the the guy the better mouse trap he has like and it hits this and it does the thing what are
those things called rub goldber Goldberg machine y uh I in this spring modulith project I'm I'm developing like a Ru
gold uh everything gets persisted to eight different things all through events so I sometimes think of it as of it as as
Frankenstein's monster because it's a whole bunch of different s that's one big walking unit that functional but it
doesn't look pretty yeah um but actually that might be fine yeah I mean that's that's the things um pretty big on on
modulith over microservices just because I've seen so much pain and suffering that teams are are dealing with because
they have have too many microservices and and a lack of understanding of what what the whole purpose is and and um and
if you create your application in a modular way then yes you can have this information this service and all its data is
is you know doesn't have to be in separate separate Deployable units um and that makes refactoring which of course I'm a
big fan of you can see it on my hat um makes it so much easier and when I was working at in early earlier in this
Century um Google has a monor repo and so it made things so much easier uh now they had tools and built up but I think
that that there's there's lots of lots of advantages to that but yeah you don't have to have one you know it's like oh I
you know we only can use this database and in this database and and we want to you know and one of the things that
actually we're talking about in our book club uh Greg young has no relationship has uh of of cqrs Fame has a talk that
we were looking at from 2014 about polyglot persistence like look if you need a graph database use a graph database don'
t try to put that in in in SQL because in a relational table based thing because it doesn't fit y um we've all made that
mistake we've all done really nasty things that we're not proud of because all we had access to was Oracle or or that's
all we knew and we didn't we didn't you know you know back in the in in the late 90s early 2000s like yeah all we had
was Oracle there there were no other database there was no such thing as a graph data or at least not you know there
were object databases those were big and we saw how well those turned out um uh but yeah now we have a plethora of of
databases and and not that you want to use them just because oh we've never used this one let's go use it right but now
you have you can say is this something that is appropriate for relational schema or is this something that that maybe
requires a different different kind of thing and you can use those from one Deployable artifact and and it's great yeah
I oh Echo strike sorry just just want to call out Echo strike resubscribed on on on Twitch thank you so much Echo strike
nice to see you here yeah uh yeah this is great I I like to um just re-evaluate my assumptions I think that's a practice
that everybody needs to do like hey now that you know I used I used to say like every year like have a have a party um I
talk about like the maturity dashboard like if you took all your projects and you said hey are you on the latest version
of screen boot uh does it h are Test passing does it you know has got coverage uh does it have pipelines is it being
deployed to uh Railway instead of uh Heroku like have we done all these things that we call mature and every year you
know my my Approach used to be every year you upgrade that maturity model cuz I yeah now those other things those are
given now this is the new a right right that we're shooting for but now that Java is coming out every six months yeah
and spring boot's coming out every my new mindset is every six months right re-evaluate your portfolio yeah and reassess
what what what's good yeah because maybe and one and one of the things I like is um and this comes from my extreme
programming background is is um if it's painful do it more often because it turns out that then it becomes easier and so
if you're trying to upgrade from 8 to 21 that's a lot of work but if you were upgrading along the way yes the 8 to9
transition was really painful and difficult but once you got past that once you got to to 11 um then going to to to to
you know take the interim ones 12 13 14 15 16 17 um and then you know I'm look there's some stuff in 22 that I'm that
I'm looking forward to uh which 21 is is middle age 21's been out for over two months 21's 212 is right around the
corner you can get the advanced ones on on 22 and start trying it out and but that's things like and you know with tools
like this open rewrite you can uh and there's another one called error prone that does some some similar kind of stuff
um and uh if you do it more often and just you know it's like oh it's really hard it takes us so long to deploy well
like then deploy more often uh and it takes us too long to do and and so um I think that's the hardest thing the hardest
shift uh is is to get there but once you're you're on that faster faster release frequency and faster deployment and a
lot of it of course if you've got good tests and fast tests then it makes a whole all the rest of it rest of it much
easier say if it's painful do it more often the way I say it in my house is do the hard things until they're easy yeah
so very similar I like that yeah and and and sort of part of it more often is breaking things down into smaller steps
and this is for me a fundamental mindset of of things like testen development is break it down into the smallest pieces
because small steps are easier than large steps but breaking it down to small steps is hard so it's easier once you
figured out what those steps are but it's often can be very difficult to figure out what is the next smallest step to to
do yeah and that's a skill that yeah you have to practice too yeah and as it's totally a learnable skill and um whether
you do tdd or not breaking stuff down into small little tiny steps of behavior modification uh are are a great are great
way to go whether you do test first or test later fantastic yeah sometimes uh complaining doesn't doesn't always work um
that's a that's a separate skill that's that's actually really hard is is how do you influence your your business folks
to say look we need to spend some a little bit more time not take three weeks off and and do nothing but refactoring but
hey how about we spend 10% of our time 20% of our time doing these refactorings and adding tests and upgrading these
things that that business you can get your stuff sooner um and I think that's uh that's a struggle yeah and that's a it'
s a culture signal like yeah there are definitely ORS Mercedes put out their open- Source I don't know if they call that
a Manifesto but just their their policy on open source and how they're giving all of their software Engineers time to
contribute and learn open source Technologies like that's a part of their policy I I read it I was impressed by it and
you know if your company's if a company has something like that like that's definitely like a magnet that's going to
pull in a little bit closer as a developer so yeah but navigating the the company stuff that's some I'm still working on
all right so let's run it run it and happens just Alias Maven to Maven W should probably write it Alias for that um so I
I make an alias that's I call it spring cubed that's upgrade it to run that recipe upgrade it to Spring boot 3 uh and it
does it looks for the dot in VNW um but I believe that there is also a recipe that'll upgrade your Maven rappers version
Oh I should probably do that too yeah because this one's older yeah I mean it's it's it's there's so many things I could
I could improve at the command line but I find myself um just not at the command line as much as I used to I find myself
uh uh just doing so much in in intellig like um you know 25 years ago it was emac was where I lived and and and these
days it's intelligent ideas where I live and and I do almost everything from within it so it's really interesting I use
um dur D EnV that uh I use that a lot uh the one thing that we've been talking about lately is to keep your secrets keep
them yes key you don't have secr on your on your local so then when I go into the Ensemble directory uh before I pull up
uh intell and or idea dot uh I'm in that directory and my durm sets up my in my environment so I can set up things like
hey here's my my credentials here's my my key as an environment variable and then what I do is or one of the other
things I could do is I could have these these plugins ran I could run these recipes like before you start intj like you
go into this directory immediately as part of durm like run these scripts and have it upgrade the things so that's just
something that makes yeah I I still roll my my keys in the in the uh in my local machines config directory so it's not
so it's basically spring boot config but it's you know basically in till SL config and that way it never gets
accidentally pushed in and never shows up anywhere um but I saw your stream on on that I like oh I should I should try
that out because that actually uh might might make it easier especially as I move AC move across machines yeah and on on
streams it's nice my my worry of credentials getting put in so for a long time I was in that mode of I just didn't want
to have credentials on my computer and you as you're traveling more and all that kind of stuff and especially more that
you stream so now I'm updating all of those VC files and they can those can even be committed so Josh and I are sharing
the same VRC file if you're on a team absolutely yeah yeah we both have our own secret bucket right but his access he's
accessing his keys I'm accessing mine and we have the same outcomes so that makes it real nice so it looks like thank
you guys so much for we've got a build failure all right let's see says could not parse as Java illegal AR exception so
it is saying web security web security config okay huh well we knew we were going to get into some some security
security stuff so let's see uh that's a jav see what's going on oh wait it didn't do anything else it just stopped it
just completely stopped so it was uh this recipe produced an error please report to the recipe author co wait a minute
this is um this is Behavior yeah this is definitely not uh oh and another turn the mic volume up I will do that uh
normally I just got to talk into the mic it's a one of those I tried to keep it not on camera I just got talking to the
mic uh so yeah this is um interesting because what I expect I expect it to be able to get through everything so we ran
our tests before and test all passed mhm yeah the I mean the application's clearly working because it's deployed in
production uh so wonder what it got hung up on let's see so does it even tell us what line could not par as Java h yeah
I mean this this I mean as you know security configurations go this is not terribly complex um but I do do some unique
things so uh basically I have um an access denied Handler um I have a a user authorities mapper because I map uh I do
some mapping of basically you log into Ensemble using GitHub uh I don't use pet I don't I don't I don't want to write
authentication and there's no need for it people actually have to ask who are part of the group have to have access to
GitHub anyway uh so using GitHub ooth kills a multiple birds with with a single Stone um uh so yeah it's not not
terribly like that's it actually fits on the screen um yeah so so first thing is like we want to make sure we capture
this note um second thing is is I want to just try re rerunning it um that's yeah just try rerunning it because I have
had where the recipe didn't download everything it needed to download and rerun worked um Robotech thanks for being here
and icon thanks for hanging out with us uh my Marathon went great I survived I'm I'm recovered now uh so I'm now I'm
ready to look for the for the next one and uh yeah it is the day before excited yeah so so echor strike this this API
has has changed uh the security stuff has changed although it is they still tend to be this fluent chain API which um
that's why I have the format or on off because otherwise intelligent will try to reformat it from my nicely laid out
things so I don't I I don't I don't think it's it's terrible uh it it can get um it can get a bit bit overwhelming but I
think I think it's okay uh yes uh I I I should use a different metaphor than than killing stones yeah so so tip for
those of you who who do this kind of thing and you don't want your formatters to automatically reformat uh intellig will
respect these tags so when you when you you know I'll often hit hit the shortcut key to just reformat code uh almost
without thinking uh in fact I have it done upon commit and so it'll it'll it'll ignore this this segment of code so so
that it won't try and push stuff together that should be together I think I saw you do this you have like a post commit
tag or commit well so intellig so again I do all my stuff in intell so intell has a bunch of things where you can say uh
optimize Imports uh here I don't have root format code on on here um but you can do a whole bunch of things check your
to-dos so I'll often uh when I'm working with with others I'll actually reformat code uh sometimes rearrange code and
then check to-dos like we have a a rule where um you cannot push um uh so sometimes we have a pre commit check sometimes
we just have a a uh we'll do it here um like no Todd's allowed like they should be temporary and they should never never
enter uh the the mainstream but in this case I have because intellig is great at formatting code I'll have it just
reformat things yeah so same same problem okay well that's uh that's interesting and unfortunate yeah that's too bad so
let's go up to the log and let's see which recipes it was trying to run and so it doesn't say so we didn't even it says
running recipes so we didn't even get there and then it said I mean it's like yeah it doesn't tell us so it's using the
visitor pattern and it's going in it says Hey I was visiting this and I couldn't parse it could not parse it as Java so
we can we can um Carl says which so Carl says which version of jdk am I running on 121 and 101 uh um maybe you should
try Java 17 could try 17 I doesn't hurt but let's keep track of this I want to just write down this error could not
parse as Java and config just take some notes I I do I want to open up issues uh and if we can create well yeah I forget
what what version is in yeah Project's in 17 okay yeah maybe that's it yeah do experiments and and since this one didn't
work uh we we can take time and I can show you another tool that I share with folks and see how that works one thing we
could also try is running a a smaller recipe yeah because this recipe is a a recipe of recipes exactly and so we could
we could just run run some others and just see see what's going on there and by the way hi lexers I don't know if I said
said hi when you said morning so welcome I think we've said hello to hello yes uh so so s mentions um uh Loren's uh
stuff about security I have his I have his I actually have all the editions of his book and and I need to go through
them because there's some stuff that I have in my project where it uh is this clui all right so that is interesting
thanks to to Carl's recommendation of trying uh 17 that's uh is this repo public yes it is okay it is Public public and
open source fantastic so all right yeah so it made a whole bunch of changes all right um so now now the fun part yeah we
can go look let's let's run the errors yes so the MVC matchers so this is the security uh the whole security
configuration that that changed um where instead of using the the old web security config that extended something and
override now you basically just have uh uh security filter change filter chain um so it can't what methods are on here
so so this is unsurprising folks I yeah if if nobody else I expected the the security stuff to to to not transition
right so let's take a look and so now what I do is I say let's go to our uh release notes I look at the spring boot
migration guide kind of as a ay where to start spring boot migration guide there a spring boot 3 migration guide and
there's a Spring Security section right there yep migration guide preparing for six for matchers do we change anything
yeah matchers uh I wonder if it's a if it's the migration to 5.8 that we need yeah so yeah I think I saw request
mentions yeah request instead of yeah because I think they they they because I know the the old in the olden days it was
ant matcher um and then NVC matcher reduce some some issues with some potential problem security issues uh but I'm
losing the not seeing the specific guide for that y so let's see use here we go I'll put the link here so for directions
on how to upgrade this visit the getting Spring Security section I link uh grab matcher and NBC matcher to request
matcher so it looks like it's a straight change yeah ah here we go use as as advertised use the new request matchers uh
so we're going change so that's interesting why looks like so yeah so that seems like carat that's seems like open
rewrite uh recipe yeah could have done that yeah especially since it's a onetoone not like parameters changed order or
meaning change or something like that so yeah but it was sounds like you're taking notes on that so for MC matcher and
for ant matcher and ant match I was with somebody yesterday where they were doing the upgrade and their ant reest uh H
can't access test roll uh oh was that a it um wait I'm confused what where is it at post test I'm going to do I'm going
saying uh so let's look at our test container dependency which version are we on uh you know another another big thing
is let's take uh uh the one we got from Carl the maven dependency updates yeah but actually now that you mentioned the
um test containers so let me see so what did it what did it do so far so it upgrade the and container no here look here
you got a you got a new exclude also did you see that right there we have that's probably not needed anymore you
probably not this exclude jit jit yeah so this was done because I uh uh I did this at some point because test containers
will pull in both junit 4 and junit 5 okay uh I don't know if it still does that um but yeah we're definitely on an old
old test container version to dependency yeah do this do the do the maven versions display dependency updates that we
got yeah and let's see what else we got like I could have run with a dash ntp but that's fine uh so let's see uh I just
start the test container one two I know test containers itself is oh it's 1193 okay I was confused by the by the J unit
so 1193 literally just came out this is so cool like that so and you know like these these little takeaways uh as we're
doing this um just that alone the the display dependency updates that's something that you know I I'm not a big fan of
like reports per se like just like hey you got something wrong I'm more a fan of like I found something wrong I know how
to fix it right right yeah I'm sure um because I run uh depend I let dependabot uh access my GitHub repost and it's been
complaining for a long time about about various things and um yeah yeah let's see if that fixed it uh so let's do a
rebuild yeah that's the I'm I'm perplexed by the error because it's it it said something and intell didn't see it and so
it was a little odd so is your intellig using Java 17 compiled so that must have been it um it must have been the the my
guess is is probably because the exclusion that you noticed probably caused some some problem and confusion um so I'm
glad I don't have to exclude anymore uh and we think we don't need this we think we don't need that but we can run a
tests I'm just am well I'm amazed test that are passing I'm amazed that all the tests pass I gotta say now one thing is
is that I don't have tests um because it's it's a a something I need to research more I and and this is where I need to
go and reference um the the spring security stuff is is testing code that is uh that has Spring Security is been the
bane of my existence and I basically um just disabled all those tests because so give me the example like so um yeah so
got been um Carl saying you cannot exclude junit junit from test containers because internally they use something of jit
4 yeah I was able to exclude the engine because clearly that worked before um but they must have changed something since
1.18 uh Andor some interaction with with spring boot who knows um I may have to go look at that again because one of the
things is when you're writing a test um intell will will if it sees junit for somewhere on on your class path it's going
to suggest that as as something to test uh yeah so basically I'm trying to to test stuff through through the the
endpoint um so for example can I can I get the page and uh I've just gone through all sorts of stuff using with mock
user and because I have this custom um authorities mapper in in the mix uh I I could just I I I could just never get it
to work and I I have to revisit it because I I especially now that my security is updated and maybe there's there's some
some newer stuff that or at least that when I ask questions they won't be annoyed it's like it's like oh that's old
stuff we don't think about that anymore you know because and not annoyed in the sense of I'm I'm asking something bad
but it's a lot easier to answer question questions from their side on newer stuff than on than on stuff that's two years
old so like that that Suite of tests that I normally would do is like hey I've got um three roles uh you know whatever
user admin other uh and then I try I want to test to make sure that they are able to see and not see the things that I
would expect so I had like a regular test that was just for security that was just it would stand up and I was using my
default was I was doing um Mach MVC test uh and that's how I was doing I think that's we using maybe uh but that's that'
s how it was validating yeah hey giv this roll giv this access set it up this way and go and then I was doing it with
and without a so I had like these different blends of things that I would set up uh for that test but yeah getting it
once you get it once you get that pattern in place yeah and this is the other thing with security like once you figure
out hey this is how we do security and this is kind of where how we do it like there's not 20 different patterns for how
you're accessing things right uh typically so once you figure out that pattern then you copy that pattern and you go
apply to the rest of your repositories your other projects yeah yeah and so that's that's I remember and I'm I'm and
this again it's like I'm sure I have the video of me struggling with this and which video did I struggle with web
security and I'm also sure because it was so frustrating and and not fun to watch that I did a lot of the the struggling
off offline um and this where a tool like uh uh Z MAAC based tool called rewind where it basically monitors and records
everything you're doing um and then you can search that so so in the sense that it's a the same kind of thing but it's
it's monitoring only only what you're doing so I'm sure that if I had that running it would I'd be able to find when was
I struggling with everything you're doing how like the screen uh the screen uh web camera if you let it um and and audio
uh and originally it was only for M uh M1 M2 processors they now either have made available or are making available uh
an Intel version so I haven't been able to use it much because my the machine we're on now my iMac is is is an Intel
based machine um so I couldn't couldn't use it on that uh but it's really nice it's like hey when was I browsing for for
so and so um and so it's really really hand so on my on my laptop which is an M M2 Max yeah it can it totally does that
Carl put up the uh test containers issue ah yes so let me take a look at that shouldn't require J for library on runtime
class path oh this has been open for a long see I expect test containers doesn't require junit 4 as you can see the
Legacy dependency has been excluded in my case I'm Crea oh yeah so I think this was the oh yeah okay container I don't
know uh let's go to your your test container uh where you're using your test containers in your tests I just want to see
how it's set up this is probably the old style because because I've got the the Dynamic Property Source yeah so we can
we can upgrades yeah uh where we're using um I forget what it's called the so what is it the the service service
connector connector yeah service connector makes it so we don't need all of those uh properties we don't have to
redefine all those properties we just get them so let's uh so let's run these tests but like right now let's do let's do
commit right now we're good we we have upgraded we're on 3.1.5 we're using up so fairly painless we did have to roll
back to Java 17 in order to run the recipe yes so that was good that was a good call yep thank you to try that thank you
Carl and how how great is it that we have a this and uh okay so committed that um let's uh can I run this locally so
here's another feature right um one of the other capabilities that you get with spring boot 3 I think it came out in
3.1.2 was that um that test class so when I was you know yeah out in the world doing my stuff uh I I didn't really enjoy
the docker compose but although Docker compos is nice it was like hey here's a Docker compos you can run it locally like
do that get clone run like with Docker compose so with spring boot I think the docker compose support came out with
spring boot 3 where if there's a Docker compose it'll start it up for you and make everything available so you can at
least have a working local version right then later they added this service connector and they added this new pattern
with your test class you could have a test application class that runs your main your spring boot application class
right but it also passes in this test container context that has your defined test containers running so instead of
running your main class you run this test class and you get all your test containers and then you don't need your Docker
compose right yes I was just reading about that where um feels like still seems like a slightly influx um but basically
uh um if you want to run your your application locally yeah but you want to use test containers what exactly what you're
describing and it's like you just do this and I'm like yeah because right now what I have to do I mean it's not a it's
not a huge bird and I don't have a Docker composed but um intell does have uh a way to run yep as a run configuration I
can just run postris yep and and uh so when you do that does it run it as a Docker container yes awesome and so what you
can do is um it will like again it's like I never have to leave intellig which is that's kind of the go which is my my
dream right you know yeah once once it pulls in email then which is always the joke right it's like you know uh all all
development environments expand until they they can handle email that was the joke on emac and so please jet brains do
not add email to intell um but you can see all the containers and images and things like that and and look at the
process from from within intell that's amazing um yeah we talk about this get clone run is the lifestyle that we want to
be in right so you can just check it out and boom uh then yeah not even depending on your IDE just be able to yeah go
and run it so it is getting better I love that you brought up like I don't want to leave my IDE either like uh one of
the things that I I used from you in the past was used to have the little uh intelligate plug-in that had the chat so I
could just be looking at my IDE and I had my little chat and now that I'm I'm streaming again today uh kick uh I have to
stream over rtmp I think it's the protocol so I don't get the chat integrated with streamyard but I could could if I go
back to using your plugin I could do it there so I could still see and share all the stuff yeah so yeah the advantage of
the new 3.1 setup is that it auto starts stops the containers if not explicitly configured otherwise with that setup you
still needed to Define it as a pre-action though yeah yep yeah yeah so and this is this is sort of the you know the
stuff I'm I'm gonna have to spend a little time on it's like what are all the goodies that I get since since 2.7 so many
goodies and you know got a great you know short story for you to go watch who would that be Dan Vega's got one he he's
got all the new features and springis 31 3.2 and they're easy to consume uh I I would start there with Dan definitely I'
ll do that and then yeah and then as you go like uh I have another question for you though that you don't like to leave
your IDE do you use Dev tools yes locally okay yeah yeah um although I have have uh I have so there's some interesting
stuff that happens when you when you have Dev tools I think I actually pulled it out of Embler because it was causing
some weird um I don't remember the specific issues uh but it was just like it wasn't providing value anymore um and so
and it was interfering I forget what it was interfering with might have been I'm curious live reload wasn't working
properly I forget what it was um but I I yeah tools yeah I want to find out right the this is something that I wasn't
using I was comfortable I I would always have my terminal open and I was just doing you know the maven start run or
Maven clean test in my terminal uh and now I find myself shifting to using more of the IDE I'll tell you a secret um I
have been trying to like you know limit how much time I spend on I could be down here for 24 hours yeah but now I've got
this iPad Pro over here and like when I don't want to get like all the way into the code I run this iPad Pro and I do a
remote and I use the code tunnel vs codes tunnel so just like for little things especially when I'm doing python like I
don't want to mess up my my ID with python plugins right so uh vs code yeah install all the plugins cuz I don't use it
that often but it's been a nice like hours of battery uh it's enough to like open up all my stuff I can have all my
projects open I can go in and look but it's just my iPad and it's been it's been really nice and I've been spending a
lot more time on that lately yeah I just I just live in intellig and so using anything else is is is my my fingers don't
like it because they know all the all the magic shortcuts do you do the emac bindings then no no no I I I haven't been
an emex user for real in in quite some time I use and since I do a lot of training and and and education I I try not to
stray too much from sort of the out-of thebox experience um wonderful so I I you know I'll add on a few shortcuts for
things uh that that don't come out of the box but pretty much I'm I'm pretty much out out of the box kind of kind of set
up I want to ask more about your training sorry if that's off topic but like the as you're training so you're also kind
of recommending like Hey we're going to use intellig and your people are getting trained on and tell here's the shortcut
here's how we do this and the the carrot select and all that kind of stuff that's cool yeah yeah and that's that's
something that that um so the way the way we do the The Ensemble the M programming and there are different ways people
do it sometimes people will have hey everybody uh connect to this VM that's running on some Cloud machine um or
everybody connect to my machine uh that has its benefits like that means nobody else has to set up anything the downside
is is you're it's sort of like you're doing this in in somebody else's room in somebody else's uh uh house and it's like
then when you go back home and you try to do it it's like oh everything's different and so what's nice and lexler uh is
is actually part of this group and um nice is you're using your own machine because we use zoom and basically we swap
screen sharing uh and uh so that way when you learn stuff and for me as the facilitator it's like wait are you on
Windows or Mac because I have to give you different shortcuts um but but uh uh other people help out and so we're not
just you know so so what we're really learning is is not just like how do we implement this and and architect this and
Design This and and and code this and write tests for this but it's also um how to how to use intell in ways that a lot
of people don't know like I've I've been using intellig for for 20 plus years as long as it it's existed and there's
stuff in there that um one of the presentations I did at kcdc was here is an hour of me refactoring this code using
stuff you probably have never tried or seen um and and it's just fun like there's there's nothing like being able to you
know do a few automated refactorings and significantly change your design and knowing that that for the most part it's
going to work that's awesome a thanks lexers yeah and because you're you're you you know you're doing it using real code
and getting feedback in the moment right to me that's the ideal learning environment so when you change drivers you're
changing screens yep uh there's a commit and then we're just grabbing the updates and doing that okay yeah so there's a
tool called mob sh um which is a wonderful Tool uh it basically does all the hard work of creating a brand specifically
for the work in progress that you're doing as as a mob um and you just say mob start pull it gets all the latest stuff
on your machine and then mob next pushes it up for the next person and we can we can rotate in 20 seconds wow yeah so
everybody has that installed everybody has that installed yeah so there so you know to to get into to my Ensemble and by
the way you are are totally welcome to to join uh you can start out just as a spectator um you're totally welcome to
join let me know and um we have a timer that that's set up and I in fact I part of ensembl the next feature I'm going to
write is a timer to build into to ensembl uh because we use another tool called called mob time but um but it means I
have to do something manually right I have to take the people who are in the course in my Embler I mean I have to copy
and paste them but I copy and paste them into a randomizer first to randomize the order and then I copy and paste that
into the uh Mob timer and it's like why am I doing that um and so uh we set time for you know three to five minutes per
P per person and then then we rotate and the screen share it's like it's just really smooth works works really well um
I'm gonna give you another tidbit and with streamyard you can do the thing so I don't know if you're paying for Zoom I'm
paying for for Zoom anyway because I do all my my training through Zoom so it's not an additional additional thing yeah
like my I normally do one-on-one Zoom uh so I'm not paying for that uh but I do just I use streamyard I send a link I
create a a recording studio send a link to that recording studio and I can bring in my people there yeah yeah what my my
dream is to be able to have a tool where I as the facilitator can see everybody's screen at the same time and I know
there's some tools that kind of do that because as a trainer what I want to do is I want to do code along with me yep so
I demonstrate something and then I'm able to look at is everybody doing it yeah um if anybody knows of a tool that does
that really well please let me know because that that's my dream and it's totally possible and I'm sure I could write it
using pull it together with um yeah but I've got enough side projects yeah so yeah all all fun stuff that one that's one
right for for your core of what you're doing that makes a lot of sense there's probably a lot of value there and yeah so
Simon mentioned a value ad like why choose me over the others right yeah because because um I've got you know one course
that that I'm way behind UNF finishing my apologies to those folks who are who are there um but of course we're getting
hopefully getting a lot of value out of the the ensembles but a refactoring with TJ course and there's um Hines kabitz
does does an intellig Wizardry course and he's so I've learned a lot of stuff from him but really you know getting out
there that there's just so much more power to this tool um I mean that's one of the things I I why I do a lot of
streaming so I want to show like this is you know this is why I'm sticking with Java is because all these tools are so
so powerful and it keeps on right Java keeps on getting better right so we're yes you know we all we did was upgrade
today but now we have another opportunity to go in and make it even better make it even easier improve right delete code
right right no bugs delete it we can make it better uh how far does intellig code with me get you or technically
speaking uh yes so yeah so so Simon asks about code with me um I tried out code with me a bunch of times and the I was
really disappointed because I figured oh like I've been using Tools in fact some of the early videos you can see me
using a tool called flu bits um there's another one called code together a bunch of these tools that try to you're
editing on your ID but it's synchronizing with another vs code has Live code built in so it's works better um uh and so
I tried uh code with me I figured all right it's coming from jet brains themselves but the problem is the way they the
architecture that they use is this sort of client server model which means you have you don't have all the power of the
refactorings as the client that you do as as the host and for me that's just that's a deal killer right okay that's a
deal killer um if you're doing something where you're pairing and you want to pair on one screen so you don't want to
swap back and forth which repairing I think is actually nicer is tupal tupal is awesome I've used we used uh James sh
and I when we were streaming tupal is just in like it's a it's it's an amazing piece of technology and and it really uh
it just yep uh and yes so um I saw you using that believe yeah so you can see down here that's that's what I'm using the
presentation assist assistant and so it shows what's nice about the presentation assistant is wait what are we seeing so
if you if you watch down here oh wait at the bottom comment uh take Carl's comment off the screen I can't see it oh
sorry I realized that it's hiding the important stuff there we go you can see as I selection and that's presentation
site um all your plugins got to find it your bill site in a long time it looks is so AB shifter is my number one one
recent over the past year favorite um if you ever do split screen development which if you watch my stream I'm almost
always doing split screen tests on the left code on the right uh it makes switching back and forth and moving things
it's just so easy so easy intellig can do it but then there are no real shortcuts for a lot of the things so it
basically adds a bunch of shortcuts and presentation assistant um custom postfix postfix is underused go ahead and check
that out um plant uml of course and and a few others so uh yeah I'm learning so much today love that stuff um and where
is it uh I don't think it's so if you're really into testing infinite test we basically run all your tests every time
code changes that may or may not work well for you but you use it it's it's when I'm in a certain mode well no nion cat
progress bar you know I used to have that installed but but but um it it got a little annoying but uh if you have not
installed the the nion cat progress bar plugin install for a little bit have a little fun at least once once this is
great yeah I've seen other people do the like anytime code changes tests run uh is that something that VSS code has a
plugin for too maybe I I think I've seen that pattern with vs code users more often for some reason um yeah I don't I
don't know about vs code uh and I know that uh so Carl asked something about um latest version I'm pretty sure there's
there's some change around that that was introduced recently um it's been one of those things that I feel like I'm a
little bit behind usually I'm pretty much at the at the Leading Edge but but uh there been so much going on with new
versions versions of java new versions of intellig new versions of spring and and other stuff going on that that's like
I need to catch up I need to spend a little time like you know and and and this is what I always reiterate to people it'
s like it looks like I'm really good at this somehow naturally and it is so not the case it's like I spent hours when
nobody else is watching sometimes when other people are watching I'm just playing around I'm just experimenting and you
know that's how we get to use our tools better right the again going back to like these tools are supposed to help us
and uh if you don't take the time to learn the shortcuts and experiment and try out the refactorings and and look at
like every time in you know anything is released anywhere there's there's almost always some kind of change log of
here's what's new and go through and read that like people spend a lot of times in some cases quite a lot of time
writing those things and so I think it's it's it's great for us to say what's new it may not I may not be something I
need um or in six months you may say was there that new thing and then you you sort of are at least aware that it that
it's there and you can go go search and find it yeah if we automate all the the boring stuff then we can do the cool do
stuff I'm seeing this dependency your sulky ulid I was like what what is that yeah so I just went and grabbed a peek and
I'm like man see I'm just I'm I'm gleaning all of this cool stuffff this is is awesome ah so yeah keep on keep on
learning what's new yeah right wouldn't it be nice if there was some place where we could go and somebody just told us
about all the new cool things that were coming out all the time that'd be great it's it's there it's there you got to
read it though so nobody's gonna read it for you that's the problem I like to so like I talked to this or I think I
talked to you about this this just idea of like you know Carl like the calendar calendar as spring out a there's always
something and when I look back there's only two weeks in 2023 where there wasn't something new coming from this right
right wouldn't it be nice if there was just like a and this is my you know I think I'll get there eventually but it's
going to take a lot of learning before I'm comfortable of like hey we got a new version of string boot like what are
some of the changes and just a little quick little video that says hey here's some of the changes oh we got a new
version of spring batch like what are the changes like a yeah read me the change logs right like something that you
could consume in the background yeah and something you could find like oh yeah give me give me the the short version
quick version this this week's new stuff in spring this week's new stuff in Java yeah yeah do it as do it as a podcast
might as well like that that's that's the goal I'll get there eventually yeah it's going to take a it's going to take a
lot of work yeah I mean there's a lot of and yeah because there's a lot of stuff that that's and it's one thing to be be
aware of it it's another to be like what is this good for right that's the harder part like like how is this GNA help me
the hard thing for me is like if I go from like 3.1.4 of spring boot to 3.1.5 right like what what changed you know top
of my head I think it's just dependency versions are the only thing that changed but like there's no cves like hey I
could do that short version like hey guess what you can upgrade to this like no stress no worries I can go and look at
the Reason notes I could do that but there's a lot of releases the other the more difficult thing is like what if I'm
coming from 2.7 right like now what's changed and you'd almost have to like review that much yeah every time like all
right so if you're coming from 3.1.4 great news nothing nothing's going on here's what's been you're all good you're
safer than you were you're up you're coming from 3.0 like how far do you go back if you're coming from 3.0 like hey
here's what's different if you're coming from 2.7 now as of tomorrow I don't have to worry about 2.7 right so that's the
other nice thing here right and this is also when you hear the spring team talk about like why they can't support 2.3
any longer right because that's a lot to to keep in yeah so so now it's three versions right that's like hey here's the
new the last and the one before that so n minus two that's not too much to handle yeah uh so it's just like what does
that format look like I've I've noodle over and I've tried several times on taking just one and offline and recording
like I'm in embarrassed a little bit but then also like some of these projects I've not ever touched yeah yeah but if
like on November 16th right there's multiple projects there like if I were to do that like that's a fun day of work
where I would touch all of those projects you'd have to have your little hello world example but if it was something
like real or there was a bug or something like hey here's what's been fixed but just having that hello world example if
I could get to the point where I had a hello world for all 60 of the spring projects yep I would be I would I'd be
loving life yeah so that's that's the goal maybe we'll see that in 2024 but that's the goal and yeah this is just I I
love my job I love what we're doing sprot 3.2 comes out tomorrow y this has been a blast Ted I'm glad that we got to I I
I honestly thought we were going to be digging in and running into a lot more problems than we yeah I thought so too I
mean I'll I'm gonna I'm gonna actually run the application well let's run it locally we have time let's see I can let's
see if I still got another 30 minutes I can hang out um let's run postris running I think it was what's TCR mode oh TCR
so I assume dud is referring to uh test and and commit or revert and so it's a specific way of doing test driven
development so the idea is you write the test it should fail you write some code and it should pass if it doesn't pass
you revert so instead of trying to to continue building on the code that hasn't worked yet it basically sort of forces
you to take a step back and and and start over um um and it's what was the book code complete is that is that where I
got that that from it was code complete I don't remember who the Steve something code complete is old wow that's very
old yeah yeah he said like the idea of throwing away code like being comfortable throwing away code and starting over I
think that's where I got that concept and I still kind of like believe it's the hardest like the the hardest thing to do
is you paint yourself in a corner to throw it away and try again yeah it's it you know we as humans have have this loss
aversion we are we time and time again we're we're like we get invested in it and and staying detached from it and just
saying I don't you know so what I recommend to folks is is you find yourself in a corner go back to the last working
commit take a break and come back and you will you will be so much better off and I'd like to follow my advice as well
that would be nice but if you can follow my advice and then then you'll be better off I all this that's a that's
honestly I don't know that I've ever I'm sure I've ran across it but I don't know that I've ever like really thought
about it one of the other things that I I'm trying to understand always is like how to get to production faster how to
deliver code faster better better code faster right so all these different patterns for how people work uh it intrigues
me and I like learning and I like practicing uh I was I was doing XP back in you know 99 200000 I've done all the
different flavors and all the different bells and whistles and everything but different teams have different needs and
different modes that they operate in U and and a lot of it depends on you know the business culture and the process on
how things are are working um but you talked about the mob timer and I talk about like the we did like it's not mob but
three people in a pod uh but we're all working on different parts of the same application and we were just doing it one
Milestone at a time as kind of dependencies like hey there's somebody doing the the UI and we doing the API and we doing
the database and like all right now let's tackle this piece and we had a Pomodoro Timer and we were just like heads down
boom we we had each other's computers yes were open up to each other so 880 on the front end was connected to my 54 63
or whatever on the back end and somebody else is kind of like yeah managing the API yeah things are working running the
tests and even though it sounds awkward for the way that we were delivering things at that time it was it was exciting
and it was fun and we all were contributing at the same time but we were still talking to each other like oh right you
know what we went down this paast and we change and we were able to change quickly yes yes and pivot like as we needed
to get goosebumps being able to work that way is is is you know and and now today as as ensembles like I I would really
never want to work any other way yeah it's just so you know besides being productive and spreading information and and
learning from each other it's just fun I mean we are social beings and being able to like truly collaborate and and just
have have fun like we get work done but like it's to me it's so much more fun than than sitting in front of a machine by
myself struggling against something or even just you know getting stuff done it's just I've been then doing that in a
group um is so so much nicer uh and yeah so I like the uh yeah the the mob idea the mob timer right Simon I'm I'm
looking at you like wouldn't it be fun to just like hey let's just build something yeah and do like a a five minute
timer and just have like you know s like Hey we're going to do it all right and have it automatically switched oh Simon
screen do the mod at sh and Boop and now we're here and now let's just let's go like what's a good way I like that yeah
fast feedback yeah Simon so um so as I as I suspected all the tests pass but it looks like we've got a problem so um so
what happens is is uh it recognized me because I've logged in on this browser using GitHub before so we're running it
locally running locally we're trying the new version running locally and we're running into problems so it looked up my
username Ted Young found me um assigned me these roles so admin is admin and member everybody gets a user Ro but if
you're not a member you won't see any the you won't it'll be useless to you if you're a member you'll see which ones you
can join if you're an admin then you can see the admin screen um and so apparently it uh it threw an exception somewhere
um and says I'm authenticated but not authorized and it seems to have uh different roles than were assigned by the by
the authorities mapper O2 user and scope read user okay all right interesting so let's go to the GitHub granted
authorities mapper those looking up found assigning roles and the way that we're doing that is we're putting these
rolles in that set right so the roles that were in the database right are being now just assigned to this right user
right so we return basically a collection of granted authorities for user and we saw that it was assigning them so we
know it got here we know it returned those collection of granted authorities is what's getting returned now we got to go
look at how are we handling that collection of granted um let's go look at where was it trying to get to so this is
going to be one of web there are times when I want to work alone too when I'm struggling when I don't want people to see
you know the mistakes and the struggles yes but the fun thing is and I'll say this even about Ted some of the my
favorite streams are when you were struggl when you were frustrated because of the way that you thought out loud and the
way you've got to the solution that's where I learned a bunch yeah so I try it's it's it's hard but um I'm trying to
work more in public whether I'm going to be successful or not yeah yeah I've see you've been streaming a a lot which is
great great trying to do more I need to to get get so uh so this is after after the login yep sequence um here you go
the user Authority above security confict granted authorities mapper yeah so that that'll get the implementation um
that'll get my GitHub that's um tramar thanks for asking I'm on Twitch as Java Grunt and I'm on Kick as Java Grunt and I
so yeah I'm here deson Stop on by I'm trying to trying to stream a little bit every page so would have already
recognized that I was logged in so it wouldn't have shown so so let's turn off this exception handling because basically
this is hiding whatever is is going on underneath go oops wait what just happened yeah what window forbidden 403 you
don't have PR so now it's immediately falling through seeing because what we expect is that you're already logged in
right M I'm gonna see if I can log out um which is an overlooked a lot of times the ability to log out can I can I
please have new session can I please have new authentication so I expected it to now at this point ask you to log back
in ask me to log back in and it's having having TR so okay so interesting it's actually having homepage all so I should
be able to see the homepage because I don't I don't it it doesn't do any authentication until I click a button to go
somewhere else so has permit all changed is there something no this is I mean I can't imagine that this is not something
that I I would recall and I'm going to go back to my uh the same link I sent authorization um can we look back at your
web okay uh but spring handling if trailing slash is changed um that did change the trailing slash thing but you're at
root so that change I wonder I wonder if that's it uh Slash cuz I the star star here but I don't ah so the putsy might
might be uh let's um let's try that yeah I I definitely I don't think that this is the case though the training flash
well it if not then we'll find out but it is suspicious that I can't hit the the homepage so let's see um what am I
think okay let's actually run go look at this Teamwork Makes the Dream Work man right that one that one was subtle
because it wasn't because for all the others I have the star star yep but for the root I did not yep um so see this and
this folks this is the benefit of streaming you get all sorts of helpful people in the in in the audience and you don't
have to solve it on your own well I was already up here uh I was reaching out to my friends because I got I got the
slack I don't have all the answers I got slack I was gonna be like hey have you guys seen this so this is this is
something that um is clearly easy to overlook uh would likely if I had proper testing you going through security would
have been found um but I don't and so that's and you know and this is reality right there there are always going to be
areas unless you are lucky enough to be in a situation where you have code tdd from the start you're going to have
portions of your code that are just under tested fact of life um and so the more you add to other places it means that
you can narrow down when you do run into problem it's likely going to be into those areas that are under tested um but
at least if it's 10% of your code or 20% of your code instead of 90% of your code you're going to be you're G to be much
better off so um this is something that uh would be great for the recipe to fix and it's probably a little bit more
invasive but if it's going to do the fix that it should have done before which is MVC matches to request matchers that
should be part of part of this another good C for a recipe this cuz yeah this is just but yeah the thing that you know
if I'm if I'm trying to help somebody upgrade their Spring Security the thing that I want is I want to have that test
Suite that says through for these different roles like what is the login like at a minute like have a have that yep that
would catch this right yeah was so let's sign in with GitHub and oh a template parse using forbidden oh that's
interesting so this is in our member register temp so um we got a timely rendering problem which again is another area
that is is under tested uh and so unsurprising to me at least that that this failed um so it looks like when it was
trying to uh go to the member registration page um there's some something that didn't parse correctly with time leaf
spring six which is it's underneath spring boot three I'm gonna step for one second go look uh let's go minimize that so
actually I'm going to do a commit of that fix uh fix mat or root path to star that um right so now we can close that and
we'll close that and let's go I'm glad my gr GitHub granted authorities mapper is all working fine because I was a
little concerned about that uh so let's go dashboard so no there it is so let's see uh this used to work because is
empty is property because it a oh but it's it should be empty not is that's interesting this was allowed before so
something must have changed I have a question let's that Maven dependency updates and sure let's see if there was a a
Time Leaf well It upgraded the time Leaf I'm I'm I'm gonna try one little experiment and then we'll go ahead and do that
I'm GNA see if if the putsy is two for two this um because that is empty was was allowed before but it is a bit
suspicious because not quite a property and it's not quite a method name and it might have been I was getting away with
something I shouldn't have been doing I love more constraints because that mistakes so so we still got let me turn off
the wrapping love deep stack traces so we still got a parse exception uh looks like there might be another place I have
that line them that's good it it it went past the right voila py is two for two look at this so apparently it shouldn't
be uh dot is empty which makes sense from a Java Bean property standpoint it should either be empty and therefore it's
treated as a property or it should be the method called is empty and why I got away with that before um something's
changed in the in the spring expression language parser uh but um now now we're working so now I should be able to
create test Ensemble put a fake link here and that's um so fun trick that I do is I have uh Cloud flare if you're
familiar with Cloud flare I use cloud flare yeah you can do like page redirects based on domains yes so you could
generate a zoom link for whatever and then you could automatically go to cloudflare and redirect it to the zoom link so
you could have like a friendly URL for the zoom link and then have it redirect to your Zoom link URL whatever it is that
yeah the reason I'm typing this in here because if I leave it blank um it will actually automatically go out using the
zoom API and go ahead and create a meeting got it automatically and then that link becomes part of the meeting and then
people people can access it but I put one in it says oh you know what you're talking about and by putting this in I'm
not having I'm basically preventing it from going out through the integration fantastic very so then I have to go and
delete a meeting later I saw you had s grid as one of your dependencies that's definitely a part of everything yeah send
Grid it's just it just works I haven't uh I haven't I I I probably will switch it at some point point but um but hey
look at that folks we did it it works fantas kind of as I expected there were problems in areas that were don't have
automated test against them um but with with the help of our our wonderful audience audience we made it through it's all
working and and not unreasonable amount of time yeah and one of the other things that would show is like hey yeah like
here's all the other values now you're on a currently you know stable version like the released version so as of you
know tomorrow you are current right you're exactly still get support and so you know I'll have I have a little more sort
of manual testing that I'll do but um this will I'm G to basically you know probably not today uh but next time I stream
I'll I'll push it to production but this is great um so I would like to have another one of these uh and let's just take
it to springb 3.2 yeah sometime and and we'll spend some time then uh cleaning up the Cru that's that is you know like
we saw the the test container stuff we can clean that up and and that would be that' be good to do yeah fantastic this
is great uh when are we going to stream next I'm going to stream not on a schedule but a lot thank you yeah so um if you
follow me on on Twitch uh you'll at least be notified when I go live um but uh if you're not already in my Discord
banner so if you go there you can find out about about uh my stuff um but if Discord and the information is there um I
basically will post in the announcements uh when um with some amount of notice usually a day or two in advance sometimes
more usually like a minute or two like hey guys I'm about to go live yeah I mean you know some yeah and sometimes I'll
be like oh hey I'm I'm feeling good so let me let me go let me go live and so you'll you you'll get one of those notices
and so um so make sure you follow desan follow me uh in I know Des Sean I I I have the notifications turned on to
YouTube so I do know when you go live awesome um and so uh yeah so we'll we we'll do more of these because this is this
has been fun I gotta get back into your Discord um Mr Shadow sorry you joined late uh but Bly we've we've upgraded a
couple of applications from from Spring boot 2.6 and 2.7 to 3.1.5 and and all and but so much other stuff was was talked
about besides that um but it's up on YouTube um since we simoc casted to to YouTube uh so you can just catch the the
rerun there and and it was fun and it worked like mission accomplished for sure and it was fun for I learned I got a
bunch of notes uh and I you know I'll definitely go back and look at the transcript yeah uh yeah I got tons of stuff uh
I want to say Carl thank you so much Foie thank you so much Simon as always like the the the group effort was definitely
uh one yeah sa saved lots of time for us so thanks yeah yeah so oh and somebody said please push those changes yes I'll
push those changes because ensembl is is open source um Embler fantastic and yeah so I'll push I'll push the changes to
um once I'm once I'm prepared to to to support it I don't want to do it before the actual Ensemble on Friday just in
case I've miss something when it when it goes production but after we have our Ensemble on Friday I'll I'll push these
changes so you normally do those on Fridays yes um I would love and invite for as a spectator I will send I will send
you send you an invite offline um I I don't use branches tram Stars you know that I'm I'm trunk-based development so it'
s always it's always push to Main uh and so if I push the main it's going to deploy it um so I'm not not quite ready
ready to do that I might do some more testing later if if I up to it on my on my tags uh approach where I can say only
deploy it if it gets a tag so I can do like you know hey run the test cool and then I can go apply the tag yeah so you
can that it's just a little another step so you can still keep your stuff in GitHub yes and that's actually something I
need to do be better at because there's times when like the situation I want people to be able to see the code but I
actually don't want to push to production just yet yeah so uh find the name of that plugin there's um jayver it hasn't
been updated while yes yes that was the one I looked at a while back and I'll have to look at I'll have to look at it
again that's the one I like I use that and then because I do a lot of like native image stuff I also use uh the OS Maven
plugin so I can get like the operating system and architecture right that I'm deploying to because I like to do arm64
and x86 yep builds so yeah Tad this is amazing well desan thanks so much this is this has been fun for me as well and
and I'm upgraded it feels so good to be upgraded yes yeah let's do it again thanks again thanks everybody this is a
blast uh yeah and I'm looking forward to the next time y all right thanks folks and for those of you who are celebrating
have a good Thanksgiving uh for those of you who are not celebrating have a good rest of your week and we'll see you
next time bye
