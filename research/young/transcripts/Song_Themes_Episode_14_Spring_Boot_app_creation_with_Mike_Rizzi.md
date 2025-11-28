# ＂Song Themes＂ Episode 14： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=ud-zS5ch1eU

---

## Transcript

he all right hello folks good morning on this Thursday it's cold where I am I don't know about where you are Mike it
night welcome oh audio problems tell you something so while Mike's getting his audio back um uh I'll talk about what's
what's on plan for today um but I'll also mention as I often do uh I have a Discord so um we've got uh lots of folks
talking about the stuff that we stream about um Mike is on the Discord as well uh and we talk about design and Java code
and intellig and testing and architecture and all that good stuff so uh join uh we also have a book club so we're
starting our next book on Sunday uh it's going to be the programmer's brain and it's never too late to join so go ahead
and check it out uh and find us find us there all right how's your audio I think I'm working now all right great I keep
forgetting that once with streamyard if I use the mute on my headset it stays muted no matter what and I can't unmute it
and I have to reset the headset it's only a streamyard thing I don't know why but yeah probably a it's probably a
browser thing because streamyard just uses whatever the browser whatever the browser does that's the that's the downside
of of browser based uh streaming tools um but it is what it is all right so um it's off day off day off Au oh off off
said off I'm like what oh you were asking about the weather oh yeah before I lost my mute yeah it was 38 degrees this
morning when I went out to get coffee yeah and there's never ice on the windshield in Oakland California there was ice
on the windshield yeah yeah I was looking at this at the at the weather it's like oh it's not raining but oh it's G to
be cold because I I'm GNA go out in my run later and I'm like oh is it gonna get warm enough even like by noon I might I
might have to actually put on uh even even when it's in the low 50s or even high 40s I'll go out with with a t-shirt um
but uh if it doesn't get out of the if it doesn't at least it's sunny so that'll that'll that'll help but otherwise I
might have to actually wear wear another layer which I almost never do so all right uh so yes it is off authentication
day um and authorization because it's both uh and so I'm gonna have to figure out what uh what what service we want to
use and how we want to do so let's let's talk about just where we authenticate from from from a um we'll just leave it
at that uh so let's let's look at at jir and see where we're at okay let me get my screen out of the way bring up jer.
txt yeah and I think I'm not sure if I wrote this after we finished yesterday or if we wrote it during the stream
yesterday authentication for database admin role um and we'll use a third party delegation of some sort I think the ones
we were talking about yesterday what was it Kai and super base yeah Kai and super super base so I was looking at at at
Kai but um I actually found uh uh Thomas Shuli I think that's how you pronounce his last name um who actually is dropped
into the stream here and there uh he's he's pretty pretty active in the spring community and he actually has um an HDMX
super based spring boot starter um so I thought we would see if that works well for us so um so super base uh which
comments and I've seen people talk about this uh it's so funny it's like there are all these different services that
provide all these pieces um and it's really kind of interesting that uh you know if you look at the big cloud providers
you know your aws's and azures and and I guess Google Cloud um I say that because like I I just don't trust anything
Google produces these days uh you know they have you know as part of the the dozens and dozens of services that they
have they ALS one of those is is authentication authorization it's interesting that the more pass oriented platforms of
service ones don't offer that so uh even I I don't even think Heroku does which is sort of the you know OG pass uh I
don't know maybe maybe it doesn't maybe I never looked at it but um it seems like that's something that that they should
offer sort of out of the box because it's already handling the delivery of your app why not also have authentication on
the other hand it's it's it's also like you know would be the benefit to to them I'm not sure but it would certainly be
a benefit to to to some to to sort of apps like us is make it easier to integrate but that's where sort of um you know
do you put the off directly in the app or do you have sort of a frontend Gateway that does some of the off for you uh so
there are a bunch of different ways to do it and um so for my ensembl app I actually just use GitHub a lot since since
by definition any body who's going to be using it has to have a GitHub account otherwise they can't actually join The
Ensemble uh so that works well for me but for for this app we want something more General and more generally applicable
and um so kind and there are a few others there's um I've done some stuff with Fusion off uh who who are who are great
folks um and I've done stuff with um off zero back in the day when they were still independent before they got bought
out by OCTA uh and superbase is interesting because it combines the off stuff with the database stuff and so this is
where he's like you can get your database from your pass and you can also get your database directly from a database
vendor uh so there's neon um and neon supports that has the database is what gives coab their database so so and so it's
just the industry is really interesting and then superbase has off plus plus database and so it's like well you know
maybe maybe we CH choose superbase for the database I don't know I mean I I kind of find it easier to have the database
where the the application is deployed because then it's easy to grab the um the database credentials and things like
that so so I think um we'll probably just stick with the off stuff since we actually don't need database now anyway and
then we can maybe figure out so that's kind of the the high level summary of what we're considering um and I was playing
with with kinda um what maybe and maybe I shouldn't be surprised and so one thing I I I always feel like as a spring
boot backend developer who goes on to the web to find products and services in this area is I feel like a second class
citizen because everything is aimed at are you a react developer are you a front-end JavaScript developer here you go B
of the Box you know boom you're done and uh and even backends like you know uh like go is more popular than Java in
terms of its its sort of first class support um and so kinda does have an SDK for Java but it's not uh it doesn't appear
to be a spring boot starter so you have to you can use spring boot um either that or I don't understand the docs and so
I am you know as you know I I am constantly frustrated by docs that don't take the point of view of of an actual user
like Doc writing is hard and you should hire somebody to do a good job because then you will get customers and for
whatever reason uh like I've done work for for for clients and and written documentation for them and um like it's worth
it because if somebody comes to your site and it's like I don't know how to integrate this they're going to move on to
to the 10 other choices that they have yeah so anyway that was a a very long intro to uh I think superbase might be the
easiest on ramp since but we just won't use the database part of it and we just won't yeah I mean we don't it's not like
you're forced to um right they both have you know signific sign significant uh ceiling for us before we have to pay for
anything like right um I forget what super base is but it's pretty it's pretty DAR High uh it was like 50,000 or
something yeah 50,000 monthly active users I think Kai was 10,000 but like either way like that's orders of magnitude
more than than we have any reason to uh expect anytime yeah um yeah so the only issue with with super base is if you
have like lots of lots of projects they limit you to to sort of two active projects and they'll just pause pause the
ones that uh that are not getting any access I one thing I find interesting and and uh is in a lot of these things like
yes they have a good a pretty nice Free level um but it feels like the The Next Step Up you know is
now $25 a month and which is you know yes the Free level is pretty high but there are some some limitations of you know like number of projects for for super base where it's like I want three but 25 is still actually more money than I'm making and it would be nice if there was like a a $
110 level um so one of the and so one of the nice things about um the O stuff is most of it is going to be so spring
boot security with spring boot um once you've Def and we'll see this as as as once we sort of get started once we
establish which path so what generally in in the security basically say here are the routes and here's who can access
them and once you establish that what's nice is you is you really isolate which security implementation you're using and
so uh it' be interesting and we might even do it um or I might do it offline uh if we use superbase if we swap out
superbase for something else what does that look like and it should be pretty much isolated to just config uh so pretty
much like one or two files um and so that'll be nice because if if we decide you know switch to kinda or something just
to switch to something else just to try it out uh it'll it'll be straightforward yeah good isolation is always good
maybe not always but usually good that's almost always good um yeah so uh let's so the superbase starter that we're
going to use is from um here I'll I'll throw comments so I I expected to to use kindai but then this morning I was
looking around I'm like uh I'm not sure about that and so sort of last minute this was the decision um think in private
in case that's easier there it goes and so uh Thomas shuy I think it's pronounced that way um at some point Thomas will
me uh it's s c h u h l y is that the HDMX spring boot person you were mentioning earlier yeah uh there's a y at the end
and it's Thomas t as must be shely because it's it's you yeah converting those those those German uml outs to into
English characters is always fun I remember back in the early 90s I was writing uh a Search tool that would search
German and English I heard had down in terms of parsing the different parts of a word prefix suffix Roots interesting
conversion between B's and P's and stuff like that as the word gets things added to it um and I had to learn how to how
to basically parse German words which are generally much much longer uh and pull the different pieces out so we could we
could parse it and index it and that was that was that was actually fun that sounds cool actually yeah all right um so
to get started you're gonna have to sign up for super base okay so presume I will do that off screen yeah um let's see
start your project probably because sign Ines so you'll have to sign up yeah or you can start for free that'll probably
now oh I said I can do GitHub yeah I always go back and forth but for stuff like this I just use I use GitHub to it's
just as good as anything else yeah it's one one one one fewer one less manager on the outside chance I just searched My
Vault to see if I had super base but I don't yeah I know I'm the same way it's like have I ever signed up for this
because um you know I'll sign up for all sorts of stuff like this and then you know months later forget about it and a
year goes by and it's like oh did I sign up for this oh look I it okay one thing that's really annoying is is I'll get
i'll get emails saying hey we've updated our blah blah blah and I'm like what are you again like because you know I
haven't you know got an email from them in three months and and I must have signed up for some service and it's like hey
we have a new version and it has these very specific detail features I'm like but what are you again and I always feel
like if if you're gonna you know if it's going to be a while since you sent me an email is sure hey cattle um that's
cool yeah I I did a bunch of stuff with with um I learned a lot in in my my Linguistics course that I took it at uh
Queens College back in the day um learned about and that that informed me about all the stuff about morphemes and and
and stuff that change as you uh cycle through the different parts of speech and things like that so sounds like fun all
right you got an org I got an org and you got the and you and and you get the or based on your GitHub username yeah I
just um and I did not uh one thing I noticed is like I did not see a way to change um the organization name which was
kind of frustrating maybe there is a way to change it oh there is I I just didn't look at it um yeah there song themes
um well this is organization so I would I would leave it unless you want to change it to your personal name yeah I'm
okay with um one thing that I and I tweeted about this yesterday one thing that annoyed me about um and superbase has
the same problem is uh if you go to the account preferences on the left so you can save that before you go off SC screen
and got a preferences there the one thing is is like I and and I I feel like lots of folks I see it less these days but
lots of folks copy Apple's horrible UI of let's put some light gray against and some darker gray and some various Shades
of Gray that are not very significant and so like if you look at the account page which you pulled off screen yeah sorry
it's got my email I oh okay um uh you can go back to the to the Oregon because you can can still see it can't H or never
mind that's fine it's not moving oh oh I see got it yeah so um maybe bump up the the zoom just a tad oh yeah of course
yeah how's that uh and so this is this is another thing like these these dashboards clearly like there's some dashboards
where where they're now like oh you might not want the critical stuff to to appear on screen so we're gonna sort of you
know uh hash it out or or Greek it out and and and hide it for you until you click a button to to show it um and
actually used to have a a a browser plugin that would that would automatically do that so that on stream I wouldn't
access acly docks myself um but if you look at the the left side like the projects organizations account and
documentation those are headers those do not look like headers they look like just dim options yeah that's what I was I
was clicking on this exactly exactly go to organization that's terrible it's terrible um and yes and and I complain and
I had this problem when I was at Apple we were working on our internal cloud system and they did similar stuff and the
text was small and I said first of all I can't read this second of all and you know I didn't want to say this too loud
but but you guys are violating uh the law because this is inaccessible right and you must make this tool accessible and
I had to fight like I had to fight much harder than I thought I would have had to to say can you make this like increase
the contrast so one thing that developers in their 20s don't understand is that uh contrast is very important to us
older folk um and apple does this all over the place and it's horrible it's it's this poor contrast thing so this
contrast from this to this is and this is especially bad because the links don't have any other indication uh that
they're links and so like if you're going to do those as headers like the one thing you could do is what I do is make
them small caps and so then it looks like it might be a header um but this is this is this is just terrible anyway that
um rants aside uh so let's um let's see so what do we need to do um what's next um so I think we need to create a new
project soin Within base yeah so if you click on all projects there on the left upper left you mean the one that's
clickable the actual one that's clickable yes not projects but all projects right new project uh yeah so new project new
organization button did you notice that uh yes interesting yeah so you can set up multiple organizations I guess um and
so here we would we would have song themes um I would suggest uh Cel or Keb the name yeah all lowercase Kebab case
because one of the things I I'm never sure about it's like how spaces and capitalization are going to be handled um what
do we call this one is it yeah it is song theme it's the same Kebab case okay cool um I mean it's possible that that
name is irrelevant from a from a and that will get some kind of ID um but we can always rename the project later so it's
so it's not a big deal yeah yeah absolutely Astra this is why diverse teams are so important I agree them it does no
good if you have a diverse team and you ignore the people who have different opinions that's why yeah um so you're gonna
need a password for the database um I mean it's gonna hide the password so you don't have to worry about about that but
you might want to generate it off screen go off screen if you want and this is for postgress yeah this is for postgress
it's weird like why why they would not generate their own password for this I don't understand well there is a generate
button here or link that's so dim I could I didn't see it like again the contrast is terrible my my password Vault has a
generation thing I'm just going to generate and um I am sure I am 100% sure if they ran this page through the uh the web
accessibility guideline standard it would fail um which is technically illegal just saying uh and something I I I I was
mentioning earlier is both superbase and Kinder um for the name have first and last names as separate fields and that
drives me crazy because my middle initial is there it's important and other people have even worse situations because
they have like two or three middle middle names or surnames that have two two you know two space separated things um and
it's just terrible you're saying I can paste it in oh sorry keep going yeah you should be able to just paste it in okay
and so I just tell folks like stop parsing full names you don't need first name and last name is separate Fields there's
no law that says you need to do that I am begging you I'm begging you stop doing that have a field for full name if you
need to have a uh something so you can call refer to me more casually than my full name then ask for first name or ask
for nickname um but you are are insulting people who have names where the middle initial or middle name is important and
I think it it should needs to stop and I feel like today's rant day yeah yeah oh that's good there is that um is that
famous blog from posting from oh yeah the false names about names yeah Ian I know somebody whose first name is a single
letter yeah just the letter V yeah and they wanted it to be their full name but back then California wouldn't let you
not have a surname now you can have a a noname so your name one letter yeah um and do did you ever meet uh three yes uh
no I never met three but I know okay yeah of yeah so so his he he had some fun fun times getting his name name changed
so his name was was for those who don't know uh he was well known in the in the sort of early XP Community um in the Bay
Area and it was his name was was basically three capital I so three Roman num three um so yeah pretty much the the he
pretty much isn't he P the person that pretty much invented the concept of chartering yes he was definitely that's
that's how I met him through uh through some some chartering work with anley n yeah and there are all sorts of issues
with with capitalization and how and spacing and punctuation I had I had I had a site that wouldn't let me put a dot
after my middle initial and I'm like are you kidding me in in a in a name field you're not allowing me to put a dot what
about a dash is that okay what about all people with hyphen I mean it's just stop trying to parse and and and do stuff
with names that is the most personal thing you could you could have and it is therefore the most infuriating and
insulting thing you could do is mess names um all right uh good afternoon lundo uh Al I haven't been ignoring your your
your messages um well we'll we'll talk about that stuff in in a bit I want to just get us I want to get us pass my
ranting sorry uh I think that's all we need here um I don't know what the next page does so it might be good to um is
there a next page oh I press create uh you press create but I'm not sure what happens next so I might do got API key and
secret but you have to reveal it yeah so luckily it appears they have hidden the stuff that needs to stay secret uh the
stuff that is public is visible so I think we're okay um bring in it back then uh at some point you'll have to reveal
those two pieces um I'll do that off uh but for now I think it's I think that's fine so what who uh laughing at so um oh
what's that that's cool so um all I did was um I I you know all tabbed between this window and intellig and it moved
away from the uh that's interesting it did it did a page reload yeah that's interesting yeah oh here it is oh I see so
when we finish creating it jumped down to this part of the page but when I did it all it also took away the but also
took away the it did the reveal the the reveal stuff um I assume there's a way to get that back I know so that's that's
really that's really conf confusing um I'm gonna go back and see if it jumps no interesting only did it when it oh you
have to click view so so the basically it's under the view API settings um which you can do that won't reveal anything
um so that's I guess it's kind think well I could see their perspective on it though I'm gonna do it again like if I
switch here and then come back now it didn't jump interesting no I no it was basically on some timer where it basically
maybe it was doing some background processing or something um UI um let's see so what do we so let's see what we need
now for authentication so if we click um just looking at the authentication settings page if there's anything sensitive
there um so that looks fine there's nothing they're just offet you can click it but they're just settings for like you
allow you new allow allow new users to sign up um we might want to actually turn that off right until we make it yeah
available to anyone else um and what I don't see manually that's what I'm because what we'd like to do is is obviously
add you as an admin see I don't see how to do that uh unless that's under they have the same sort of annoying uh left
sidebar icon thing where it's basically I don't know what these are and so you have to Mouse over each one to figure out
what it is that that you want to do uh ah so the so the authent so the one with the that looks like some weird padlock
not like any padlock I've ever seen um this one the one that says authentication it's supposed to look like a padlock
that doesn't look like a padlock to me that looks like some combination padlock or like icons are supposed to be the
simplified abstracted most abstracted version of the concept all right I'll stop um so really is this is what happens
when when I when I start using a new service so uh if you go to that page it's going to be empty there are no users and
then the upper right we can add a user so that's how we'll do it okay um all right but let's uh so let's yeah so let's
add a user um let's see if I I'll do it oh cre and you'll have to do it off screen because it's going to ask you for us
uh email password yeah and do you think six minimum password is good enough or I think it okay just oh great my one
password just good because I'm basically going through your what you're going through uh on my it weird and that's
interesting so that doesn't be appear to be a way once you've user to change their display name oh interesting maybe
that's only something that they can do I don't know I mean that's fine but that's interesting so is there how do I even
add a display name because it's not even in the ad us yeah it's not I don't know I don't know huh not gonna worry about
that yeah so I've got that created back um so what we want is back to the API settings I guess I shouldn't be worried
about my email address because oh yeah I mean it's probably not that hard to find given it's my actual name well and I'm
using my real name here so it's certainly guessable so is that's users uh where the API settings go sorry L as's comment
oh there it is wow this is okay so what we want to get to is um uh so let's let's go ahead and add um uh add the spring
boot starter uh for the the from Thomas um let's add that to our our pal file so what you want to add uh unfortunately
he doesn't provide the maven version so I'll have to tell you what that is did you pull because I upgraded our spring
boot uh last night no I did not so do so do an do a I think it's a what is it just pull uh control T I like shortcuts
and merge even though there merge well I did do a bunch of typing in jer. txt oh right okay did we lose it no because it
would have merged it and I didn't modify that so um so that should be fine um P so yeah so let's go uh uh and let's
stick it up um yeah let's stick it uh a uh line 70 half uh so add another dependency block so do uh open angle bracket
dependency yep so the artifact ID um that's going to be that uh HTM x- super base- spring-boot D starter if you scroll
down you'll see that in the initial setup section of the read me the read me in here yeah so just scroll down so grab
after the colon there and the dependencies ah so from HTM X to to to to start first one got it yeah yeah that'll go
artifact ID yep and then the group ID uh is going to be the the tly and then uh we're going to want to add a new line 73
and a half which will be 0.3.2 because that's actually the latest it uh and so you'll need to go into uh or just wait
and Maven we'll get updated okay so that's all good like it's doing it yeah not found uh at the bottom here no it's
lying um at least I think it's lying uh if you open up um where's your Maven toolbar um it used to be on the right but
I'm not up that's weird uh so do open up the actions yeah and then just type there uh oops sorry that was that was the
popup do it again uh we want the one Below ad Maven projects that's just Maven with the m there but not the blue m not
the blue M the dark M the dark M yeah that's weird why did that why did it go away I know that is weird is there like a
pin that I'm missing I don't know not seeing a pin maybe it was accidentally removed and now it's added back um so if
you open up that tree and then open up the dependencies tree um yeah it's there yeah so that status message was just out
of date got it cool all right properties is that system. properties no uh do you not have an yeah you have an
application it's up uh right above test in the in the window oh there it is okay yeah I was looking the wrong hey it's
desan welcome Java grunt hey desan um all right oh where you going we'll be your background for your packing I'm a
skiing all right um so what we want oh Copper Mountain yeah yeah nice uh so what we want and uh we'll probably do some
of we'll need to do some of this off screen um and we have to make sure uh not commit this um oh right uh the better way
might be to do it uh as an environment variable um actually I think what we'll do is we'll just leave it empty and just
get everything hooked up uh and then figure out how we want to um do this stuff at a later point because this this uh
the the credentials we won't want we'll want to have locally but we'll want to put them as um environment variables on
the the path that we're so me and let's copy the whole section there uh under under that yeah here you can just click
the copy button yeah we won't need all of it but um it's just easier to copy it that way and try and select and copy and
let's let's see how smart intellig is let's see if intellig converts that yaml uh into uh into properties I hate yaml
and I try to avoid yaml as long as I can so let's switch back to intell um so let's get to a couple of new lines and
then paste nope it didn't that's too um sort of but it's not it's it it it does the other way around which which is
which is nice if you're yaml it'll take property file formats and and if you paste it into a yaml file it'll convert it
to yaml but apparently it doesn't do it the other way um that's fine we can do this manually so let's um uh let's change
line five um that's going to basically be our our prefix um so uh change the colon to a DOT and then uh and what we're
going to do is basically copy that and just prefix it on all the other lines actually wait a second I was going to say
do you want to do the multi carat yeah I was just about to uh Alt J so Alt J works if you're searching but in this case
you want to create multiple carrots and the way you do key okay so double tap the control key and then do the down arrow
is that the control key that's um what is what is it then on uh I haven't customized my keyboard mapping so it's what's
it called I'll just look it up from the actions question down yeah um I guess huh but they I guess that's that's what
that's what it's I guess maybe on the Mac it's different so yeah it's control and then control down and then you can
just keep you keep doing control down I am doing it but it's not moving it uh if you move the cursor after it then you
can add more so hit Escape okay and then control and then control down a few times here we paste control control down
that one's be carrot uh and now you can escape um and we can get rid of 14 through 16 because stuff uh and then let's
grab the project is uh I think I think he had a a link to that who did on the read me um oh and the read me ah I see
that project ID got it yeah so uh no no sorry go down right above where we copied pasted he has a link there yeah so
grab that but you want to just take the project part of it because the the domain name is going to be different for you
and that's where you'll go from here so that's that's the URL you're going to go to on superbase to get the settings or
you can just click on API on terrible it's API docks is it proba it's under it's under settings so the gear API and so
what we want um what did we come here for I thought it was Project URL we wanted project uh we wanted ID do you think
this project URL is the project ID no uh uh what is the project ID that must be the prefix yeah so it's basically if you
see in the URL okay the dip whatever yeah so it's basically the the the the prefix it's also the prefix to the URL so
you see in the project URL section the URL it starts with that and so everything everything yeah there's no separate
entry for project ID interesting which I guess that would go here yeah yeah and we don't need line five true um we can
actually copy and paste the anonymous key because that can be public so that was back on on that page button and uh and
so what I would do is comment that line duplicate it and comment it out because eventually we'll want it to look like
that so what that means is um with the the dollar curly it means pick it up from some other place uh either uh specif
specify on the command line or from an environment variable um but we're going to just put it in directly so get rid of
everything after the colon uh and in fact um all those colons should actually be equals so here you can do a select the
colon J and you said equals and just put yeah um now secr I got to do offline right yeah we're not going to put that in
now because uh because we're going to want to handle later um so what page did we actually have a controller endpoint
for the UI for the bulk import UI I don't think we did I think we just one I'm not even sure yeah actually see what we
have well that's the that's the the welcome page that's um but no under under our our in in remember this would be an
inbound adapter all right uh so I think that controller is is only um for uh searching uh scroll up so we've got the
theme search yeah because there's a button and it does a get controller because it's confusing to call it just song
themes when it's really a specific thing um we're not moving it shift F6 shift the other F6 yeah the other F6 one of the
other f6s um song theme Searcher is that what you were saying yeah I think it should just be song themed Searcher or
search controller and get rid of controller or search controller I'm up for for getting rid of a controller what about
you works for me all right let's do it let's break the mold get rid of that Hungarian and yeah we should probably rename
the test as well yeah hey there a hand so high is that it yeah cattle we're gonna we're gonna figure out how to do that
because eventually that will be an environment variable on the the pass as well so we won't want it and we certainly
don't yeah um rame the variables yeah yeah me too commit yep hey there zerox Mr Colonel a summary of what a virtual
thread is and its benefits um virtual threads are are are huge huge huge um basically means that uh you will never you
will basically not run out of threads but the Bas the the basic idea is instead of worrying about threads blocking and
sitting there and doing nothing and they're a precious resource um because typically you can only depending on the
operating system and Hardware you could probably only create on the order of thousands maybe um and so each one you know
so if you have a high uh if you have a system that's needing to to do a lot of things simultaneously like handle a lot
of people searching for songs um you would not want to have one thread per user because if you've got 10,000 users 9,000
of them are going to be very unhappy if you can only have a thousand threads and so before virtual threads what you
would do is you'd have a pool of threads and when you hit a point where you have to block because you're waiting for Io
SO waiting for the database to respond waiting for connection to respond waiting for some read some of the file um right
basic if you don't have what you need in memory to do the work you not got to go fetch it from somewhere and that takes
a long time relative to to the thread to the computer right a second for us is not a long time but you know that's a
thousand milliseconds that's a terribly long time uh to a computer and so um so it used to be you and this is where the
Frameworks and and underpinnings would provide pools and and it's like okay you're blocked I'm going to take the thread
away from you and run some other code and now you're blocked I'm going to take the thre away from you and and use it to
run some other block of code until it blocks and then I'm going to take it right and so there's just all this you know
shifting around of of these these threads because they're precious resources well virtual threads basically says stop
doing that we'll do that for you in a sense and so now threads are cheap um for a while they were called fibers that's
why it was Project Loom uh but now they're just virtual threads um and for me it's always funny because in the very very
very very early days of java that's how how it worked uh what we're called Green threads and um and so now we're sort of
back to that which I think is kind of you know come full circle and so now it means you don't have the framework nor you
have to figure out how to hold on to and share these precious resources you don't pull threads anymore you just create
them when you need them um and let uh the underpinnings of of java figure out how to how to do that uh and virtual
threads are absolutely production ready um yes there like anything new uh there's always going to be some edge cases
where you might run into some problems um for the most part though you probably it uh hold on I come actually come back
to that one um yeah so when when Oracle and Java and open jdk say that virtual threads is out of preview and even when
it was in preview it was still sort of production ready you just had to worry about the API changing it is it is
production ready people are using it in production and you should be using it in production and this is why um if you
run like open rewrite spring migration script it will turn on the virtual threads for you because it is production ready
use it use it use it use it absolutely 100% yeah the Jeep Cafe uh love love watching his his stuff um yeah absolutely
use it um take advantage of it uh stop worrying about pre being a precious resource don't use thread pools anymore you
don't need it um yeah it's really I mean I I I can't it's one of those super super powerful hidden things um but it's
it's it's a a breakthrough lambdas and and I I am very thankful because as I was mentioning before like the alternative
is you have to you have to figure out async a we so a lot of languages do async a weight in order to protect these
resources saying okay I'm gonna go async and then I'm gonna wait I'm gonna block against other thing and and you don't
have to do that we don't have to do that in Java so in terms of the secrets yes so uh there is you can set if you use
Dev tools you can set um a config uh a special config in your home directory under do config spring boot um I do that uh
and we might do that uh as well um because it means that you don't have to uh it means basically the property is there
and is automatically read in development um and so that's that's probably what we'll do uh yeah um just catching up on
other questions yeah private Keys never end up in GitHub rebos that never happens I just realized I was on mute top of
hour should we um take a break catch up on yes chat yeah so let's take a break and when we come back from the break uh
we'll set up a we'll have to set up a controller endpoint just to basically sample one um just so we can get or I guess
we could protect the theme surch but we we'll figure that when we come back from the break so we're going to take a a
break yeah seven uh how long seven yeah okay all right we'll take a seven minute break and we'll see you when we come
back great all right so while um waiting for uh Mike to get back uh just a couple of announcements uh you've been seeing
the link to the Discord uh come come through so go ahead and join if you're not already a member of Discord got lots of
great folks uh asking questions about Java spring boot testing um lots of resources shared when new releases of Java or
intellig come out we we talk about those um and as I've mentioned before uh we've got a book club um so it's never too
late to join but we are starting uh we'll have our first session on Sunday so a few days away those of you who are in
the book club read the chapters don't wait till the last minute like like like me um uh so it's free to join uh but you
got to be in the Discord to uh to get access um and the way the book club works is we pick a book and we read it uh we
read a chapter or two and then we spend a couple hours on Sunday uh working through it and talking about it and sharing
our questions and confusions and aha moments and experiences and things like that so uh the book club we meet on Zoom
from 10:00 a.m. to noon Pacific time which is uh 6:00 to 8:00 p.m. YouTube DC and uh the next book that we're uh going
to be working through is the programmers Bane brain I would say Bane I don't know why uh the program is brain and it's
really um it's something that is is uh the whole idea of learning and so on is really something that that I've been
studying for for six or seven years now I've got some talks on how people learn and why it's important to understand
that uh and this book is is written by someone who's done research in the area uh so it's going to be uh very different
from your typical technical kind of thing so I I know I'm right uh rock and roll let's go back here yeah I'll post a
link to to to the there it is do we ever get back to Al W about the no I was gonna I was gonna get back to that uh
questions now you're one step ahead of me I'm just scrolling back in yeah uh so w was talking about um do a cucumber um
and yes this is not as rare as it should be um mock mock a bunch of behaviors and it's even worse at the sort of
cucumber level because you've been working sort of further out outside and my recommendation is is find ways to get rid
of these tests um you might have to keep them around uh but you what you want to focus on is is how can I start testing
closer to where the behavior is actually implemented and by closer I mean you have the the object that has that behavior
and you want to write tests directly against it as opposed to the objects here and then there's another object here and
another object here and if that's what you're testing against that's testing at a distance and you want to test as close
as possible um and so typically this is what I what I see happening is you mock some dependencies and then what are you
testing are you testing that you mock them correctly um so what I try to avoid is is is avoid mocking all together and
use different kinds of test doubles um and so uh if you um will probably be doing that that here once we get past the
authentication when we start to get to to database stuff um you'll see that that we're going to use what I think are
better techniques for um testing with external services and also on solo stream where I'm working on ensembl uh you see
a lot of a lot of that where dependencies are are either stubbed out um or they're they're faked uh and we basically
don't don't use mocks and we test as close to the can um so my recommendation is is if you've got these tests that's
great uh but what you want to do is use them as a foundation for then building uh and writing tests that are much closer
to the behavior which means you may have to refactor the code uh one of the the main recommendations I give when I come
in so I do I do technical coaching when I come into a team is we need to split this code because it's doing both IO and
business logic and you want those two to be separate um and this is why I like testable architectures like hexagonal and
and clean because they really guide you to do that that separation yeah because otherwise you end up testing your DUI
setup makito right and and to me makito is is a test smell uh and a code smell because it means you're doing things that
you really don't need to do if your code is designed to separate the io from from right all right let's get back to uh
so oh so I I want to talk about the the commit um run test thing so one of the things I found is is that uh intell when
you tell it to run tests it runs them after the commit but before the push which at least is something uh because I was
doing that yesterday and I had that turned on uh and I'm like oh it ran before the push because it actually failed um
I'm like okay that that's better than running it after the push but I'd like it to run before the commit so um so let's
see yeah so what uh do you want to close the the notification there on the lower right yeah um so unsurprisingly we we
will have because I don't think we finished our our setup of of this so let's take a so um it's funny I saw who was I
watching video now I can't remember who who it was I know who it is I'm I'm just I'm for some reason I'm blanking on his
his name oh it's gonna Josh long my gosh I don't know why like I guess I don't don't mention his name a lot out loud and
so his name his name escaped me so I was watching him him do some stuff uh this some experimental thing with test jars
and he goes into the context LS and says we don't need this this is a useless test it's actually not a useless test it's
actually a very important test for this exact reason which is it is the Baseline make sure that I've got stuff
configured correctly um if you add on other tests then yes it might become redundant but uh if you've got no other
spring boot comprehensive does my application start this is actually the test you want the context loads which is why
it's named that way it's like can we get the application context all configured and loaded and wired up uh so I think
it's a good sort of Baseline test um even though it looks like it does nothing it's actually really important because
it's tagged with an at Spring boot test so the at Spring boot test does all of the the initialization and these are
terrible tests to write in general but for this specific purpose it's perfect um which basically tells us we've got some
configuration to deal with uh so let's go look at what we're missing so let's scroll down in this devastatingly large
stack Trace as it's what happens when these things fail uh let's keep going maybe make the window bigger uh actually
right there so um we've got a web security uh couldn't create a web security configuration uh let's see if there's more
we're gonna so when I'm scanning through these what I'm looking for is those where we see the caused by because we're
looking for caused by which is caused by which is caused by and we're looking for what is the actual thing that we're
we're so this one is caused by could not postprocess uh and that's caused by error creating Bean with that uh because it
can't find that by uh and that's because there's no MBC Handler mapping thinking yeah so it's having trouble creating
the health end point which is going keep going yeah keep going I wonder it's if it's if um so I wonder if if uh Thomas's
uh starter actually requires the database settings even though we're not going to use the database uh what I'm guessing
is that it actually still requires those to be set up um look it so let's go let's go add those properties from here in
his his setup uh no let's just go add them to the application properties we know what I file where' it go oh there it is
like you said on the top top file uh so let's drop down to the end let's go to line 12 and do superbase dot uh and
database so yeah super base. host uh I mean I guess we can go grab the host from from the uh from the super base
settings so that uh database yep so copy the host and then next line is going to be database uh let's just I wonder if
that's enough uh well let's let's set name as well although he doesn't have that in his thing let's let's set name I
don't know what the name what what what super base defaulted to oh looks like defaulted the progress postgress so let's
copy that basically we want to get all the super base. database stuff set up all yeah oh it probably it my guess is is
those don't need to be specified probably because um it's basically your project name with prefix with postgress so
could probably figure it out um uh and I think we can leave the port out because that's probably the default and the
other one we're missing is yeah so for that um we can just uh use the the syntax he has in the read value right see this
the curly the thing yeah uh so let's let's run the the again that's promising uh ah so it looks like um and I didn't see
him document this so we'll have to do some suggestions to improve the read me so it's looking for Flyway we don't have
Flyway W um so this is kind of unfortunate that uh he's forcing us to use both the um basically use all the database
support um that's kind of a bummer uh I don't see any that um so that might be that might be a poll request uh so then
what we want to do is let's go file let me get the what is the exact uh is it what am I adding um so let's go let's
close this file and I think we actually have a commented out above so let's let's turn on the postgress dependency so
let's uncomment out um and then let's add in um uh within postgress or a separate dependency uh separate dependency um
actually this we can uh we can have intellig put in for US ah sweet so if you scroll up to the top of the dependencies
you see where it says edit starters oh click on that oh sweet and uh if you open up or search dat uh or you could search
there how do you know it's in there because it's got a check mark because it's got a check mark oh you know what it
could be uh it could be that and I see see that now in the air Message the Flyway is is can initialized because um the
driver failed and maybe that's because we didn't have the postgress driver so let's cancel out and let's try it again as
then rerun the test as then rerun the test yes okay because we just dependenc uh I wonder if we'll require jdbc all
right let's look at what failed now uh so Flyway so still couldn't connect to the datbase let's scroll down scrolling
let's keep going it's funny the same error message uh oh wrong password uh we haven't set up post crpes yet have we well
superbase is so that's the database part of superbase is it's a post press database um but because the password is wrong
Flyway couldn't do anything uh I didn't realize we had Flyway turned on so let's search for Flyway and actually let's in
which one the the Flyway so uh is that what you meant yeah I was gonna say just delete back um so if we don't have
Flyway then let's try it again let's run it again I've not had the right Focus let me go back go oh I know what happened
my wireless mouse probably ran out of battery luckily yeah so cattle mentions uh I prefer liquid based to Flyway they're
both good they're both quality um matter of of whatever you prefer uh I have more experience with chest I think nope huh
control shift F10 didn't work that's working I used the mouse in that case versus keyboard all right we have success uh
so it must have been that we had Flyway in there um and then Flyway needs to connect to the database but since we didn't
have a real database password uh it was trying to set up the data source so okay that makes sense yeah let's do let's do
a commit now that we working and this is sort of the downside right of of um what's what's the word bundling um you you
sometimes can't it's sort of all or All or Nothing uh so the downside of a bundle is you have to take the whole bundle
and the same applies to to library versus Frameworks Frameworks you're taking on the whole framework whether you like it
or not maybe there Parts you don't like too bad uh on the other hand assembling libraries yourself and gluing them
together means that you're doing work that maybe everybody's doing a million times and that's how Frameworks get born
and that's how drop wizard got got born um I was a big drop wizard pan fan back in the day before I boot good enough or
um sure you free feel free to suggest a different I don't have anything better which is why and and it's one of those
like I don't feel like I need to to use my brain to to think of anything better because it's yeah it's good enough cool
all right so now we uh We've successfully added the dependency um uh we do we have we have Dev tools in the pom file yes
we do I see it right there um so what Dev tools allows us to do is uh and I posted the the link in the chat so um this
is something that I I forget who mentioned it in chat earlier uh you can create a config file in your home directory um
so that way it's not in the repository but it will still be read by the spring boot application when we run it and only
when you're running it locally so it won't pull it won't try to pull in the config file uh when you run it in production
production will set the environment variables um so what you'll want to do and you'll do this offscreen uh is um create
that that config file and you'll want to paste the an non key or whatever they called it that so this would be at the
root for song themes in other words the same folder that has so why don't you uh so bring bring up the docs that that I
have up up on screen so the spring boot Dev tools Doc it's in chat as well where is it in chat ah there it is found it
should be near your top yeah actually when you select it when you're displaying it it actually highlights it in the
comment oh chat so it's easy to find that's cool that's here yeah so if you create a file called spring-boot ddev tools.
properties if you create that file in your uh in a subdirectory under your home um since you're running Windows it would
be whatever your home directory is user home or whatever um so if you create a doc config directory and then underneath
that a slash a spring boot directory and then you create a properties directory in there uh a properties file in there
go right so that's your home directory and so if you create a DOT config under that let me make sure there's not nope
been long since I've done this on Windows command let's see if that's the right syntax it is wh right I guess you could
bring up if you had a a the Ws or whatever you could use that you don't have to use the Windows command prompt yeah no
I'm already here um and then yeah let's make the spring Dash boot directory into that for some reason spring didn't look
spelled look like it was spelled was all right now this will be and now create that properties file yeah this out do off
well keep it on screen for now until we until you paste the thing because you want to make sure we get the the format of
the file correct yeah let y I think we'll need the Anan key and the JWT those key no interesting okay why is it not
finding what are you trying to do I'm trying to get into the folder through Windows Explorer and then use subblime to to
create the file and open it um oh it's literally GNA have like one line in it so can use VI if you have to yeah well I
don't know if VI exists in my prompt do you have a prompt I get it what are we going to call this file again um what it
says yeah do you have the windows Linux thing set up on your machine I'm not sure I do the one what um there was one
that was popular back in the day I don't know if it still exists anymore um well no there's officially supported Linux
the windows uh Linux oh really that I do not know oh posix no no no it's called wsl2 is all I know about it but I
haven't used okay uh windows in years I'll check okay so I got the file Sublime so I'm ready when you are so WSL is the
windows sub uh subsystem for Linux but basically gives you a full Linux environment on your windows I believe it
requires Windows Pro which I have so then you should I would highly highly recommend that that you get that because then
you can stop having to use command yeah yeah yeah I'll look at that later yep okay so so we want in here is basically
the same property name uh that we're going to pull from um so we're going to so you can you can go back to the intellig
so we can find the property in the applications properties file application properties file the other one yep uh so we
want to do um so it's going to pull from the environment variable um I don't know if it's going to parse it correctly uh
so can yeah we can do that so copy uh line six everything inside the curlies equals now off screen um and then I'm just
looking to see if we need anything else uh and we don't need this uh if you want to may as well do that one as well so
copy that that one in that'll be obviously a separate line offscreen do that stuff so that in here I just realized I can
go my I've got like 40 lines in my uh config and and something that I need that that I want to do um because I know
Deshawn does this on on his on his setup is um I'd like to have it all this stuff in my one password in my password
Vault and have it just reveal it in the um environment transparently um but I haven't I haven't looked at how to do that
do interesting the database password so I've already got the JWT uh secret now on super base it's saying the password
you provided so here's a UI challenge I you you generated it right well what's interesting is look it doesn't oh you
gotta you can't there's no scroll bar ter yeah it's terrible okay so that one I will pull from my like changing the
contrast and making the contrast low just to indicate UI hey invisible programmer yes uh so uh you're watching on Twitch
um and so it's always becomes a video on demand on Twitch uh but also you can see it on YouTube uh since we simal cast
to to both and so it's available there uh and yes today there's a lot of struggling fumbling around you probably will
defitely want to watch it at least to times speed with also your finger on the fast forward button to skip past stuff
yeah okay file made and we're all right so um and saved Let's uh let's see so how can the trick is is how do we how can
we verify that this works um I guess we can protect protect our site so let's uh let's let's go ahead and in um whoops
what where is it I was just looking for is so let's go back into our application properties file and let's add um uh
some more dopu doget uh and this is going to be um let's just use slash so we'll allow slash um not sure if that needs
to be in double quotes but we can put it in sure and then uh so that will that's basically telling superbase or telling
the authentication stuff hey this is public uh and so you don't need to be authenticated at all let's add another row so
you can row um let's see so how in a properties file do we enter multiple that separated by commas curly answer I think
it's comma separated so let's try that um so I uh delete that line put a comma uh and let's do um the the URL that you
have at the bottom there on search all right and public uh let's create now uh another entry uh so super base. rolls you
sure I am sure it's not okay I know it's not autocomp completing but that's what the docs say uh these yeah I'm not sure
why since these are configured um it may not autocomplete those although like I'm not surprised that if we when we do
admin that that won't autocomplete but I'm a little surprised rolls wasn't uh wasn't autocom completable but anyway
super super base. rolls. admin and this stuff is way easier to config I guess in in in in yaml but doget and so what
this is saying is for those who have the role of admin they are allowed to do get requests against this endpoint um
actually why don't we take the theme search and move it down to here mean this whole line no no just the URL oh I see
what you're saying like this yeah and then get rid of the comma yep fine I think I think that's application oh uh before
we do that actually we need to go back into superbase and and set up some some links so the way ooth works is we Bas is
underneath it's going to basically do uh a request for the login page to superbase and then superbase once it confirms
who you are it will do a redirect back to our our page and we have to tell it what URLs are allowed so authentication um
unless it's under something else um what are we looking for specifically what we're looking for is there are uh so there
there needs to be um we need to tell superbase which links it's allowed to to redirect back to because we want to
redirect back to our site once we finish logging in because it's going to then give us the token um but we need to tell
superbase what URL that is so that people don't you know do all sorts of nasty stuff is authentication uh I'm not seeing
it that's passwords so what we're looking for is URLs they have a search capability in this I don't see one oh there's a
search button command yeah what what was the search keyword you like so where is this site URL specified oh project what
no now somewhere we need to be able to enter and this is usually straightforward and I'm not sure why it's so obscure um
basically so with other ooth provider it's very easy you basically say here's the URL uh here or here are the multiple
URLs that that you're allowed to go back to is this it oh that looks like it where is that um well I actually went to it
I'm going to go I'm going to roll back so I had done a search uh the control K it brought me to this help page oh it's
under authentication not under settings wow that's confusing so then I clicked on this allow list and that brings us
here and then I clicked this and it B us there yeah so they basically have authentication stuff split into two parts
which is very confusing um where's the parent oh configuration so if you click on the padlock on the left that's where
we are gotcha yeah um and so what we want is URL configuration which is where we are and our site URL uh we want that to
be uh um and so I think we need to add a redirect URL so click on ADD URL there be I think we can just add the same
thing oh what the local yeah when we actually deploy it'll it'll we'll need to add the URL of where we're deploying to
should we do both now or since we're no because I don't I don't know where we're we're going to deploy it to or what its
URL is just yet I don't know if you've hooked up your custom domain to it yet I forget I think you did yeah yeah I did
see but we can it so tkes asks uh why are we using superbase and not my database we're not using superbase for database
even though that's part of the name uh we're using authentication um okay now I think we're ready to to run our app
locally and see so you selected the config but you didn't run thank you which is a really interesting UI issue because I
see that happen all all the time oh we renamed our application so you probably need to open up the the project oh shoot
um right click open up the project window startup what did we change we renamed that from from the standard out of the
box song themes application oh you can just click the the Run Green Run Arrow there on the left y right uh so it's
trying to connect to the database file um Let's uh let's comment out the postgress oh that's for test coner so we'll
leave that sorry do we have postgress somewhere else um yeah so let's comment that one out yeah and and flyways
somewhere around did we take that out I forget we deleted it okay good okay uh let's try running bummer so I'm actually
surprised that the password is wrong because I thought we specified that in the yeah the file in the config file um I'm
gonna look at it just to double yeah you did it's the let me just look at my Vault yeah super base admin password that
matches do you think um the properties file needs a new line an empty line after that empty lines don't matter okay or
or lack of empty lines don't matter or lack okay so it can parse without got it yeah um does it need to to pick it up
well no we're restarting the server so yeah it should be picking it up automatically um uh uh let's see do we specify oh
that's in the P that's in database so what you could do temporarily is offscreen put the password directly in here right
uh and then close the tab um because maybe it's not reading it okay I'm going in the correct way then does it need good
now help me remember not to open screen back F10 H H well so it's not a problem with it picking it up the environment
variable um oh I wonder do we maybe we had the host wrong what did we put in for the h wait so let's uh since we know
it's not the uh let's um revert your your application properties so you don't have the password in there yep let me know
when that's done reverted uh did we grab the we did copy the host right that is the the host so um yeah so I thought
maybe we left it over uh from what he had in the read me but no I'm pretty sure now remember we copied um I mean we can
double check the settings yeah that's I was thinking the other thing we can do is we database H should we check the
settings first yeah let's double check the settings so that that would be database yeah database uh not database but
under settings down here yeah so confusing and it's under database so that's the whole URI and and we copy the host we
copy the database name the port is the standard Port we copy the user and you have the password oh the user wait a
second uh yeah we did yeah um do we need to specify the port no the port that's the standard Port so you wouldn't have
to set it unless it's different from the standard but 5432 is postgress is standard okay database is and it didn't say
it couldn't connect it said it it said the password was wrong um good point so we no it's like I was like oh did I not
but we could reset the password well let's do this so um at the top where it says connection string on the superbase
site if you that mode session mode okay I guess other options are there uh transaction mode that's fine that's just
pooling okay copy that so copy that and then go into intellig uh open up the database tool window so under Tools do you
not have should I don't know where they hide that on if we bring up the actions and do database yeah that's what I was
doing uh it'll be sessions the blue one maybe or Explorer no you want you want you want one with the you want the there
should be a database with the database icon but where the database icon is gray oh oh I got a spell database right that
helps yeah that's the one first one first one got it it's so weird I don't know like I guess it hides the tool Windows
if you've never used them and now it's visible but is it not but it's not it's uh and then act and then that's just
active to Windows all right whatever um so if you if uh if you go to the plus there and we want to add a new uh data
postgress yep and um if you uh just paste it in paste the thing that you copied into the URL and your password you're
gonna have to drag that off screen and punch in your password and then when you hit okay or connect bottom uh so
download the driver because I gotta close this uh no you don't have to close it oh it wouldn't let me click download no
no but you wouldn't you don't click there there's there's an entry on the dialogue got it dialogue should I do this uh
oh you can do it that yeah so what that does is is yep is the the ID itself needs the drivers to talk to the database
and it doesn't ship with them so it has to download them should I open that window back up um if you've added the
password you shouldn't have to you should just now be able to uh try and connect uh you can hit re you can refresh it
something unusual has occurred uhhuh all right so this looks like it's a super based problem that uh I don't know what
to do unless there's some characters endofunctor zero mentioned this maybe there's some characters in your password that
are not allowed did you have special characters in it yeah the only only one oh actually yeah only one which is what
Bang Yeah that might not be good I can I can go back and reset yeah so let's uh let so why don't you go ahead and and
change the the database password I think you have uh yeah it's there but you have to click uh below scroll down down the
right there's a um wasn't there a reset password I thought it was yeah it was right below parameters right there there
it is I'll do this off screen I don't know what it's gonna look like right away oh I just put it in there okay well I
could just let it generate yeah I could just let it generate and then just copy it yeah Vault click reset and then I
have to put it in this so you might I you want to turn my screen off you haven't already yep is the end of the you why
okay I think you can bring me back and then I just do now I did it through screen uh here and actually it's you can do
it and it's hidden it's interesting so when you open this up see it's the hidden password so right I could have done
that on screen um so now we just do refresh and see if we're pathetic yep well we got that something inusual though um
um well I am stumped cuz let me see if I can connect to my super base so I connected successfully so there's something
not quite right on on your end um do you want to bring up the the yeah I had it off screen uh oh interesting overrides
above one second let me um I'm gonna scroll horizontally in this window here the has interesting it doesn't have a when
you paste the URL and and it has the password it automatically removes it from the URL and puts it in the proper places
um I see but I would I would double check the password because it worked for me so you might want to copy and paste the
password again I did but oh so you're saying from resetting or from it from The Vault because I reset it well from
whatever you reset it to yeah okay let me do that screen again apply okay because here I'll show you what what you what
you should see here we go oh okay don't know what happened but possibly well my buffer I thought I had it in my buffer
maybe I didn't yeah all right well then that was the problem so uh now that we verifi that we can connect with that
password go ahead yes wow how did that interesting so when I did paste in bang it's like what that's clearly not right
but it's like that was the same paste I did seconds ago into huh that's odd okay so it's the properties file is uh
changed and saved okay so now we'll start restart the server now let's restart the F10 me um so in the um yeah config
file it's just this text uhuh right because the other it's saying the dollar sign curly is saying hey go over there and
get it right well you can do the same thing we did before com duplicate that line comment that out temporarily paste off
off screen uh okay will you I'll remove you than this is like the hardest stuff whenever I I set up a new service this
is always the the most annoying hard stuff uh especially doing on on stream because um one of the things I I do is uh um
I'm ready I basically inject the value from the properties file into something that's displayed at startup so I can see
did it actually pull in the right thing because oftentimes like I copy and paste wrong or I mistype the thing um and uh
but I but that's not something you can do on stream because you literally that's s what you don't want to display um but
injecting that value you can use the at Value to inject that into uh into the startup and then you can actually look at
what is the actual property for that um so I just you can put my screen back on it's safe to put it back yeah oh there
we go complete initialization yeah so Uh something's something's not right in the way the config is set up set but we
can we can resolve that offline yeah that makes sense um let's just make sure not to I mean you can always reset the
password right I mean this is not right I'm not terribly concerned about this password being revealed because uh once
we're once we're done with the stream you'll you can go you could go reset it very quickly um all right uh so now off is
running we can now uh and again this is sort of the I think um I probably would not use this starter because it seems to
require you to connect at the database and I don't want that um and maybe there's there's some pull requests we can do
to work with Thomas to say I actually don't want to use super base's database in there I don't want to have to configure
it uh but anyway um let's now go to your app from a browser so we should be able to assuming we configured things
correctly we should be able to hit the rout and see the welcome message and we do uh and so now if you go to the slash
whatever uh what we want the Local Host right I'd love to press the cap lock key just map it to something else like I do
hey perfect so it took us to unauthenticated which is what uh what the default is somewhere we have the default where if
you're unauthenticated it hits you it it puts you over to unauthenticated um what's weird we didn't test root then no we
did we saw the coming soon no but that was not Local Host that was song thematic oh oh oh okay I thought so typed uh
same thing for rout so the too many redirects uh is is a problem because we didn't tag unauthenticated as something
that's public and that should actually be public so let's go add that um so let's go back to base no so this is going to
be in your application properties but that's means you're gonna yeah have to do the offline um I'm going to push it way
down like out of view and we can look at the top fine share my screen again um now we don't have a login page uh you
might have pushed down stuff so where're you might have pushed down stuff we need though so let me take you off the
stuff that had the the super base public get that stuff we need visible yeah where did that go um there no it isn't wait
where'd it go exactly it on second I'm gonna pull out the password I'm GNA put it in that little no pad thing over here
and you can share my screen again I'm just so this is the whole file uh well we lost all those entries our well at some
point we lost so that's probably why it's not working let me do local history but I think you might have again that
there's the go ah so uh jenith brings up a a good suggestion um you can put the password in the yl file because um yeah
we can either do profiles but if we do you if there's both an application yaml and an application properties properties
will take precedence but it them we just have to make sure we don't commit that okay I brought this back in I still have
the password off screen but you can so why don't you um create should we do should we do this first two things inflate
you think the ammo yeah well I'm actually thinking about changing your your uh your local config to uh to construct it
differently um I do not have password on so so these are the two lines that we're missing right uh let's add a couple of
more to the get so put a comma after the end of the get line yep uh and we want the basically what we have up there on
page yeah and yeah let's restart that okay I got to put the password back in so you um so don't put the password back in
go into your uh config file your off offscreen config file oh that one right yeah um and instead of the uppercase
version because actually that's actually the environment variable and for some reason it's not picking it up so what we
can do is we can set the property directly so if you use the lowercase superbase do JWT secret making sure the S is
uppercase and you put that in your properties in your local properties file that should work oh wait a second Super
based secret or superbase database password I'm sorry the database password and the JWT secret which we'll need also
need but basically make both look like what they look like in the application properties in terms of the the case so
lower case lowercase superbase dot. database. password yeah okay done and then the JW so now let's see do I have that
one I could just type it by hand super base. jwc do Secret and still equals and still equals yes okay saved okay so
what'll happen is the um so spring has a a priority order for what overrides what and the dev tools global settings
config file overrides everything so it it will always replace whatever might have been defined before um it should
override it uh so let's go ahead and run the app and see what happens hopefully it'll still start up if not then we can
fall back to the other way all right y cool uh so let's go let's let's see what happens now so let's go to the rout
which we should be allowed to see Noe H um maybe it has to do with with the way the multiple properties are set up uh we
could sort of take those two entries and put them in the the yaml yaml file okay uh so basically cut lines 15 and 16 and
then let's create a new file at the same level is the application properties so just right click on application
properties and say new uh and it'll just be a file and application. yl or yml whatever either one is fine like that yep
uh do a paste and let's see what happens no it didn't do it okay uh so let's uh no I I I would have expected it to
convert it but I guess it didn't um so let's let's copy and paste from the read me because I don't correctly so if you
scroll down there's that um I think that's actually wrong I think it needs to be indented one more because it's missing
the super base so go to the top of the file do super base colon ah and then paste yeah uh and so let's for the get let's
add another row uh so instead of six six um we can leave the post it doesn't matter uh and then uh let's add the theme
search uh six and a half uh actually no we don't want that one public so let's go and uh under so indent one and I it's
rolls colen yep and then indent uh and then admin and then admin colon and then in restart did start successfully it did
okay so now we'll try root uhuh there we go all right so it must be something that um it's not processing prop a
properties file correctly uh that seems like a either we're not doing we're not doing it correctly either we're not
doing it correctly for multiple values or and which is likely the case because I don't do many multiple I think oh I
remember have to do you have to specify it as an array uh which is kind of annoying so the animal is actually easier for
this so we'll just leave it so that was probably our mistake in the properties file um all right and so now if we go to
slash uh themes yeah it should now redirect us to unauthenticated um but the the too many redirects is problem cuz it it
shouldn't be redirecting anything here in console that's helping uh so hold hold on you're scrolling um oh I see what's
happening so it's redirecting to a page that doesn't exist and therefore it redirect it's probably trying to redirect to
some other page uh redirect yeah so I think I led us down a bad road so that's totally my fault um I didn't realize that
and I should have rather read me more carefully uh it looks like this is not just um so it says usage with which the
HDMX this library is heavily optimized for HDMX it's actually completely only useful for hmx because he doesn't have any
documentation for how one would um do this off without using HTM X so uh that's is that that bad because we were
planning on using HTM X weren't we well but he's using it for for all authentication um which I wasn't planning on doing
because that means you are uh tied to HDMX you're you yeah you're you're 100% tied to that um interesting so that's my
fault uh but we're at time so I think we should call it for today um and what I'll do is I'll do a little bit more
research on uh using super base more more directly as an ooth provider um because then we can then we can leverage just
Spring Security and use its configuration so I I don't think this is a good fit for us because I'm not honestly crazy
about like it's offloading too much to the configuration file and I actually prefer uh programmatic configuration um
that's just my preference not saying this is good or bad just my preference uh but I think the deal killer is the HDMX
well the hmx and And the fact I mean and yeah that's that's that's that's um I mean it does say htx sub based starter so
but I didn't I thought we could still leverage its authentication but apparently not so um all right it's all good Lear
we learned something y yep we learned stuff any questions left in the chat we haven't I so uh but we learned a little
bit more about how to set up your uh config so that'll that'll serve us well going forward because you'll probably just
keep that um and then we'll be able to pull those properties in uh into whatever setup we decide all right um That's all
folks for today uh sometimes you you don't make as much progress as you'd like but you still learn stuff uh so thanks
for joining us and um how many story points was today I can't remember a thousand thousand thousand points today all
right so thanks for thanks for hanging out um I will probably do a solo stream later today uh we haven't yet scheduled
our next pairing stream but we'll do that we'll do that soon and so we will see you next time thanks for joining us m
