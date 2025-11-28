# ＂Song Themes＂ Episode 16： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=Jxqqc4HqT1o

---

## Transcript

all right hello folks and welcome to another pairing stream with with Mike Rizzy hey Mike how's it going good how are
you doing I'm doing well uh so I um I found out that we were at least I was because I was the one pronouncing it uh the
the name of the tool we're using for authentication it's not kinda or Ki or anything it's as if you pronounce it without
the e it's kind um and I only found that out because I was like how do you pronounce it they must have something on
their site that says how to pronounce it and it's somewhere in their about box uh and it says it's pronounced like the
word kind I'm like oh okay why I why don't you make that more obvious because that is not an obvious pronunciation based
on how it's spelled I wonder if it's is it a US company maybe no they're they're Australian but even so yeah because I
was wondering if there was like a Scandinavian word that's kind of like that that's pronounced kind yeah I know it's
yeah no okay no no no and they said uhh they're not planning on whatever um were people complaining is that why they
were I don't I don't I'm assuming they got some some people reacting otherwise why would you say that and I I had posted
a comment on on madon about that and uh somebody said what because they thought I was talking about Kindle oh um and I
was like no no no nothing to do with Kindle it's it's kind uh and I was saying like look if your if your name is going
to be a non-obvious pronunciation you kind of want to make that clear like that is your company product name so you
should probably make that clear and I think that that's true for people as well like um it took me a long time to figure
out how Emily Bates pronounces her last name uh it wasn't until like I I was like how does she pronounce her name how
does she pronounce her name because it wasn't anywhere like obvious until like I saw a talk and she introduced herself
and I like oh okay now I know how to pronounce it um like my name it's there's not really many ways you could pronounce
Ted Young so uh I don't I don't have to do that but for for anyone where it's like a not obvious name like why not have
a little video saying hi this is how you pronounce my name it's I was just thinking about the name kind and we were
talking about Kindle well I guess it's the Le though it doesn't really work the joke doesn't work yeah get the out of
Kindle all right um so last time we we ended on a on a high note with with actually getting the authentication working
um so that was good um so let's pick it up from there let's figure out let's let's check J and see where we are I think
I know what what we have to do next but we can check that cool yeah I haven't looked since we were last on wow must have
because it's moving to the left party that's just like note stuff yeah that's just note stuff don't think we yeah so
yeah actually we haven't um written much in jira on this regard uh well I think it's it's I think it's right there the
next one which is UI for bulk import so I think uh I think we can check off authentication authorization um or at least
the the hard part we'll probably still have some configuration to do um so protect um the I guess the admin end points
hey as good evening to you just what how would we describe what we got done um uh Oho um sweet uh yeah and what we can
do is um once we protect the right endpoint then we can uh deploy it to production so maybe add on to after 56 uh deploy
to production and update uh the kind configurations so that the URL call back is all set up the redirect call back or
whatever they call it set up they can find kind configurations for redirect yeah whatever the URLs are that specify
right I do like to accidentally press that uh caps lock key can you I mean do you have do you have a tool to reprogram
that key like I know you can do that on the Mac with some controls probably can I haven't actually thought of that I
mean it's only lately I think it's because I've got it oriented at this slight angle because of the dual monitors what I
like about it is I don't I I I oh you can actually use it for something I can actually use it for something exactly it's
like who the heck you who like unless you happen to be doing a lot of caps lock stuff it's really not not you know not
much use for is uh caps loog basically emulating all four meta Keys pressed down at the same time is great for for
Global hotkeys okay all right so let's work on uh so let's let's let's work on jro 56 let's get our our security config
set up properly or set up appropriately not properly it's not like it's improperly set up cool so let's go to um uh the
security config file this one yes uh what zoom level are you at feels like it's a bit small to me uh control shift a
zoom 110 can we try 125 yeah I could have sworn we were running higher yeah that's better thank you yeah you bet all
right uh so what we want is is um instead of authorize any request where where uh on line 16 there what we want to do is
we want to authorize only for uh the authorization requests um so let's say in instead of uh actually combine 15 and 16
because we're going to do a little bit of different formatting probably want the control thinking no the other one no
too late you got to do it again you gotta undo first and then do it go there you go uh so put the the dot before the any
line um and instead of any request what we're going to do is replace uh and basically put the closing par on the all one
all the way at the end put that on a new line as well because we're going to replace the entire line 16 now okay um so
we're gon to replace that whole line with with request matchers no no too much yeah I know it was it jumped more than I
wanted to oh yeah okay there we go yeah so we want do request matchers y uh and what that takes is basically a variable
list of arguments uh pretty much strings is what we'll use um so we're going to say uh string with with Slash in it oh
say the word string with flashing it no no double quote slash double backslash that one yes got it um for so basically
that's the root for now that's the one that just says like coming soon so that one will permit all so say DOT permit all
yep and then on a new line we'll do request matches um uh actually do you want theme search open to anyone I guess so so
that one should prob point I mean just the search the get request right it kind of looks does it actually have to see
what it looks like like how clunky is it like is it sure we could temporarily do it and then if I don't like the way it
looks we can keep it hidden till we build that UI a little bit looking a little bit better um so then let's uh put that
on the one before it so let's erase what you got there or actually doesn't matter just hop up a line put a comma and
then do uh Slash and then just hit that for autocomplete yep okay it's nice that intellig detects your your get mappings
right and this is something that that uh is part of this their spring framework support um so now uh did we actually
Define an endpoint think did I don't think we did so um because I think we just had the two the the sort of the homepage
controller which is just the slash and then I had the the song theme Searcher I think just had um uh the the controller
just the song theme controller just had the theme search where song theme controller uh it's the Searcher actually up in
the adapter in web ah this one that used to be called right yeah uh yeah so that just has the get mapping for that I
don't think there's anything else in there in fact otherwise intellig probably would have suggested it um okay so then
what uh what endpoint do we want that to be and this is for the bul entry right right um I was just thinking SL bulk but
we could do bulk hyphen entry future you know right now we're just going to do a simple one which is just an you know an
edit box you can dump in um if we had future ones that are like you know file picker would we want a different endpoint
for each of those or just one and then just the implementation from the UI I think I think you just want one yeah so in
that case just I do either bulk or bulk entry what other um terminologies could just say uh song entry or import oh
import that's better how about um how about song import okay so let's punch that up there on line 17 and and uh one
thing we haven't set up is sort of a uh a translation of authentication to roles um I'm not quite sure how kind
configuration Works in that regard um so uh I think we we actually don't care right because we don't we're not
differentiating between differentation roles yeah so we can just say then uh after after that just say authenticated
yeah it yeah that should be here so that's an an intelligate thing to to basically it'll jump you to where that's uh
where that's implemented if it was right which this one's not cool um so what this will say is yeah so what this will do
is for Slash and for slash theme search you don't have to be authenticated um the other thing we probably want to do is
we've got some static files that we don't want uh or maybe we don't yet I don't think we actually have any static files
um well when we get to those we'll set those up because we'll want those to be per permit all right for things like
graphics and spgs and icons and stuff like that so all right um that that's it actually that's all we need cool do we
want to create the endpoint next or what's yeah so I think now um now we start uh outside in create our test for an
endpoint uh figure out what so it'll be very much like the the MVC test you've got for song themes okay oh actually
might just want toop should name it sorry you might just want as you're not using intellig astd what intellig I'm
disappointed as uh Hey Jonas um we're gonna go for at least a couple of hours uh so maybe two and a half depending on
our mood yeah and welcome all right uh you were saying something about renaming something oh no I was going to say let's
create the production class first because then the automated class thing will be better but since we're just going to
copy this test class yeah my original thought doesn't mean anything anymore yeah you can also go go the other way uh you
can create the test class and say jump to non jump to the implementation uh although I don't know if it'll it but it
won't create it yeah it won't create it right yeah yeah that's why I was GNA go that rout all right so let's um I don't
know what do you think some things import you want to make it exactly like the endpoint name which is song import which
feels better I tend to try I tend to like shorter yeah as much as possible I'm with you on that one okay all right done
get this down here let me close a l of these windows okay so uh we'll just change that it's the song endpoint well we
won't need any of the query parameters because this so we don't need oh I would love to say I didn't have coffee but I
did was six hours ago though or longer that was an early coffee um yeah 7 a.m. uh all right so let's run this test uh
just on its own do we want the two get two song import I guess I always I always struggle with with this particular name
is it like is it a get request to this is or is it a get request from this or is it just a get against like the what
about um well it's specifically performing a get important if you do this is is it to or against so that's why that's
what we had get to let's let's not bike shed this let's just let's just leave it keeping it consistent unless you have
unless unless somebody has a much better name that's yeah compelling we'll just leave it um so let's run uh so so
generally what I like to do is um for these kinds of tests is run this test class on its own okay yeah control shift F10
is your yeah and we expect this to be a 404 because there is none although we might get a problem before that with the
issue uh ignore going yeah so we get so we've gotten a 302 um because security is on uh and that page explicitly is
protected against authentication um and so this is this is a case where this stuff starts to get a little bit more uh
complicated which is uh which we have a couple of choices of of what we can do here um one is uh we can use what's
called a mock user um where uh so the problem is we've got in the ma I just want to make sure understand the issue so
here we're saying Hey song import endpoint must be authenticated but we we haven't got a system yet for authenticating
so we do oh we have a Sy for authenticating but I mean and that's why we see the redirected URL as being as being a kind
so then what's the failure so we're getting a 302 redirection instead of a instead of either a 200 or what we'd like to
see first is a 404 right right so we'd like to see a 40 for because we don't have a controller with a get mapping for
that endpoint right but even before it's kind of interesting yeah it's even before spring tries to see if there's a get
mapping for it uh because if it revealed a 404 for what should have been a secure endpoint that would be leaking
information so it basically says security takes priority you're you can't hit this end point because we've defined it as
being authenticated authenticated right so we're going to take you through the authentication that so how would we have
the test this is the mock user you're talking about yes so what we want to do is we want to tell the test Runner hey
Pretend We're we're authenticated as as this user got it um so what we want to do is uh go to the top of the class and
put an an name uh and say at with mock user oh we could we could probably do Anonymous user uh because I think anonymous
anonymous users are weird Anonymous users are authenticated but they actually don't have any authorities let's let's
first try the anonymous user see what happens so instead of with mock oh no pams uh yeah it doesn't need any prams I
don't think it does I haven't before let's see Anonymous this annotation is added to a test to emulate running with an
anonymous user security context will contain an anonymous authentication token um are you reading this I'm just reading
the the docs yeah uh it's just so weird um this idea of of being authenticated as Anonymous it it to me it's freaky it's
it's just it's just wrong but I I understand why it might have been done but yeah well it failed did it fail the right
way no it still has a yeah it still has a 302 so enough uh so let's let's uh I would have thought so it could be that
have so let's just do do uh with mock user okay uh and in there the string sort of doesn't matter that will just become
the username yeah looks like it made it farther let's see yes 404 that's what we want for far yes uh all right great so
now we can make the test pass so now that the test fails the way we wanted it to we can go ahead and uh that is it worth
no I just create just create a new class yeah we're gon we're still going to keep working on not using the word
controller if we can importer song importer sure that's awesome what an cool so let's annotate it with uh an at
controller at the top and then we can put a an at get ma get mapping for the method now the get mapping goes on the
method right uh so some people like redirect and view uh we're just going to return a string and what we call this one
just song import well song import was sort of the the name that of the end point so I tend to have them closely aligned
yeah sense what is going on with my fingers I don't know uh so kosan asks can you explain the difference controller and
rest controller yes so this is something that I remember was very confusing to me in the early days of learning spring
um controller is a web controller so what happens with the at controller is that it means that the return value from a
method so like this get mapped method is not going to be data that's going to be sent to the caller it's going to be the
name of what's called a view uh and if you're using something like Tim Leaf which is likely if you're using at
controller you're probably going to be using time Leaf um it Returns the name of a Time Leaf template which is typically
whatever name you give it plus HTML in the appropriate directory so um so the return value of a of a method whether it's
a get mapped method or post method with at controller is intended for using with with regular web apps not you know not
not any kind of API just where the server is generating the UI at rest controller what it does is it says oh whatever
value you're returning from these methods I am going to return to the caller possibly in fact by default converting it
to Json um so if you're writing apis for your likely overly complex front ends but I have no opinion on that um then uh
you're probably going to want at rest controller and so that means the return values from any of your methods are going
to be uh converted to Json by default and then just returned so if you're writing restful quote restful apis you're
going to use rest controller if you're writing web a web uis um using some kind of view template technology like time
Leaf then you're going to want controller time leaf and HTM X as well I presume uh well time Leaf is the server side
generated stuff HTM X is to make the interactivity on the on the front end uh a bit a bit nicer um I don't think we are
going to use HTM X anytime soon um more likely on the on The View uh search side than than the entry side yes so since
this is a web app we're going to have a get that's going to return the page that says says here please type your stuff
in or copy and paste or whatever and then one of those buttons will initiate a post request which will then submit uh
the data and it all right um so since this method says it's going to return a string we've got to return something um so
we can just return an empty string you you could return something that would that would be a more interesting error um
that's that's totally fine uh either way time Leaf is GNA complain I can't find a template with this name right so let's
run a test with our new failed failure so somewhere in there it's going to it's going to say uh hey I couldn't find uh
error resolving template template might not exist template for sure doesn't exist um so let's uh let's let's return the
be I I want to name this um I tend to name it just the name of the the endpoint so song import even though and you don't
need the HTML because it auto welcome all right and now let's uh oh sorry I'm getting ahead of you runaway driver no no
you're you're totally fine um you were exactly doing the right thing um what I was going to do is look at one of the
exist do we care about the ex yeah let's grab the um let's take the one that has no page it would be nice if they had a
copy paste in one keystroke I wonder if they do uh so they do it's it's F5 right which is which is normally copy we're
in the right place everything else okay uh yeah let's change the header when you say header you mean H1 tag uh and for
now just stick in um what should we use I guess a text since this is a multi-line thing I guess and we can tell it how
many rows and columns we want because we'll want it to be uh so text area so we'll we'll give it an ID later um so we'll
just say uh rows equal yeah equals just equals okay I wasn't sure I need to do the times Le thing um say yeah 20 sounds
good I'm just picking a number and then and then columns or actually it's call CS calls because apparently bites are
costly in the early days I don't know uh we can do something like a 100 oh 100 oh it's number of but it's yeah uh you
too early for an ID yeah we don't I mean I guess we could assign an ID but we'll we'll do that later okay um and we can
sort of preview this all right uh there a shortcut for preview yeah if you if you move if you hover over in the upper
right of the of that oh right yeah let me I or should I do it within I tend to do it within intell for this kind of
stuff because I don't need the full power of of chrome it's pretty Chrome what exactly so I'm gonna I'm gonna close that
and then let's do it does interesting is it because there's no ID that in there that's oh maybe maybe swegi is saying
maybe this is not good enough oh does it not like the self closing maybe uh let's try it again but that's weird iess all
right that is weird but so I guess not all HTML tags are self closing there is some you have to I guess so um the
standard uh there's a warning apparently yeah um yeah I don't know going to worry about that uh so uh oh aderan um asked
about is the project somewhere on on GitHub uh yes yes but you're not going to find much in the way of Aggregates this
is a very small this is a very tiny project see but do we want to you want me to grab the URL for the um what is it
warning about now on area let me just get this in to chat I guess you can post I got I got it oh you already did oops
then delete oh right it doesn't like mine because I can't chat yeah URLs okay cool well not not on the YouTube side and
and uh it's weird it's like um there's no way in the YouTube chat to like sort of give permission to people uh that's
where YouTube sort of chat stuff is really well well behind Twitches um but can you hover over the the text area on the
top I'm just has uh Missing Associated label oh okay yeah because it's it's going to end up being inside of a form let's
actually wrap it in a form while we're here because the text area on its own isn't yes so what intellig is doing uh is
if you'll notice the url url wasn't just to the file it was actually to intellig itself that's serving up the files and
has some code that it injects in order to to do what's called a live reload so that's the live reload support so when
you save the file it will re it will uh update the thing um so that's why that that happened and I guess because we
didn't close the text area it assumed everything after that was part of the text area or something uh which was the
injecting so uh all right um that's good enough for now um at some point we'll add the um the form tags and a button
we're can add a button now if we want uh so after the uh just say submit oh uh then close the tag and just say uh but
not autoc close because we want to give it all right text on the button uh and then we could just you could import yep
you got something better you about to say something that's cool a compile error down here no that's saying the test
failed oh right that's test passed all right great woohoo so now we can get rid of our MVC test and move to test a one
that doesn't exist yet right or uh right right so you can go to the there song importer this one so production
controller yeah and you can there it's alt shift T you could also do create test but alt what was it yeah alt shift T
really um no sorry control shift T yeah it's like sometimes the on the Mac the command uh key is an alt and sometimes
the command is a control and I I'm sorry I don't have all the bottom I was just seeing what we did before for the other
yeah this test is going to be way simpler way different yeah um we just actually want to see that it that it returns
song import as as a name because we're not uh we're not populating any models we're not prefilling anything this is just
uh an empty form um yeah so it's going to be relatively straightforward so we we just want um song import back uh so
create the song importer call the string uh you'll want to VAR that up because we need the I I was still working on the
backspace there um now I usually call it something like either view name or page name or something like that technically
it's the view name okay um and that's our action so yeah yeah uh and then we want to assert that that's equal to song
import which of course we'll pass but we'll want to we first there we go was weird unusually so for for for whatever
reason and I I understand why because there are a lot of autocompletion possibilities inside of assert that um I never
wait for int to suggest the the name when I'm inside of the assert that because it takes too long got it so if you were
waiting for it to auto complete and it took a while happening wait a second we want a failing test first well we want
the we'll we'll make the test be correct and we'll force it to fail by changing our it there I'm GNA use some of the
techniques from uh uh from the book club on like some uh memory techniques see if they work for getting better at the
keyboard shortcuts uh so let's change um the code to just to be just change it to something else or just something
doesn't matter yeah uh so let's switch to running uh back to running our IO free tests and so this is this should fail
pass sweet yeah the postfix is nicer because then you can autocomplete and then type aast and then it'll surround it
with assert that and jump you right to to the other thing yeah so that would be like this um yeah oh but it's a custom
one that that suiga created ah okay and I think it's somewhere in the Discord yeah I'll find it make a mental note not a
mental note make a real note as okay okay right so that's it for this one um now we want to go back to our MVC test
because now to post mapping pinpoint I don't really like that name but well it's not not a get it's a post to mapping
end it's a endpoint all right astred have a good night night astred yeah we started much later in the day today didn't
we yes I pre-apologize to to my European users European viewers yeah um so I would opposed to to mapping endpoint as
opposed to the song import endpoint uh and what we wanted to do is when we do a post to Our Song import uh we wanted to
redirect so what I would say here is is post to song import endpoint redirects right would you include the word
redirects I'd like to make it clear that I'm that I'm that I'm posting to an endpoint yeah okay that's but that's just
me cool good right right and you want to Auto Import that oh yeah without that choice so do Alt Enter so do Alt pick
whoa yeah so what I what I end up doing is uh uh basically excluding a bunch of the um uh is the uh the one in the mock
MBC request Builders which is not at all obvious and so so what I end up doing is uh certainly taking the ones in so if
you hit the right arrow from here me it's off screen but I'll hit it yeah uh and see see it's giving you a whole bunch
of choices of of what part of the tree of of things that it could possibly import do we want to eliminate and exclude um
you pretty much don't want anything from com GitHub Docker Java so you can exclude all the way from there second one
from the bottom yeah so if you hit enter what it'll do is it'll add it to this exclude from Auto Import so we'll never
now ask you to Auto Import from that again you can always manually do it but it won't automatically automatically do it
and so over time if you constantly tell it no I don't want this no I don't want this no I'll never want to Auto Import
from this soon you'll get to the the point of only offering you choices that that actually make sense um any of these we
should get rid of yeah so the last one we want to get rid of you're never going to use that and um I tend to uh exclude
the web one so now you should be back down you should be down to like two choices um and now you can just choose the
first one because now it's now at this point it's obvious in a sense of do I want am I in a test or am I in production
code and I'll want one or the right here I'm not sure what I'm gonna put in oh we asking a question uh he was just
pointing that he has a the templates in a on up on GitHub IGI so where were we um oh Syntax for post uh it's the same
thing for get well mostly for what we're gonna initially do it's the same thing it takes a URL or maybe technically a
URI uh and the same thing for the and expect uh and so here we want above why is it not know it oh there we go um and
then is 3xx redirection that's about saying I need to cast to a request Imports did we actually import the right thing
no we didn't uh get rid of all these no no no get rid of just the one with the post because ah so did we act did we
accidentally exclude the wrong thing I was wondering about that because I didn't remember the name being that oh we must
have we must have accidentally excluded all right let's go back to your settings we must Import that these guys general
or is it more yeah so that's so if you click in there you can probably or maybe it does it in order um this this ISS
Java yeah why do it Escape Can You Escape because yeah that way yeah okay so um think was in this pile Oh we
accidentally yeah that last one is is wrong um so just delete that yeah I think we we did a too low level y oh okay
great perfect but it just did it without asking which one we wanted um probably because it knew the context we can
double check it should be Mach MVC request Builders so that's correct yeah okay cool now we run all um or you said for
these you like to just run the class for these I just run the class yep so we expect this to fail because there is no
post end point right um forbidden let's let's scroll all the way up yeah I'm wondering if it uhuh uhhuh yep okay uh so
you see the session attribute stuff and there's this mention of the csrf token this was causing me a like I was in a
different situation I was with HDMX doing a post and that's a totally separate problem um so uh we actually need to say
so are you familiar with csrf no okay so uh csrf stands for cross- site request forgery um and so it's protecting
against is uh a post coming from somewhere that didn't Supply the form so if we didn't have CSF csrf protection somebody
could steal stuff and and do a post on your behalf without you knowing about it right uh and so what what um the
security in combination with with time Leaf does for you is it'll actually inject uh a token as a hidden element and so
when the form gets submitted that comes along for the ride and so it checks it checks that that the tokens match since
our test is not doing that at all we need to add to our test hey can you stick in a csrf um so right before the closing
the last PR on line 31 oh 31 uh say dowi yep and then just say csrf open close which will be a static method which I
can't stand but this is where we are really interesting Yeah so basically what that method does is it supplies uh some
configuration customization uh for you um I just really hate static methods so like that one and the status and post
like all these methods are static methods and I just hate them because they're not discoverable yeah but that's what
Vach MPC provide so that's what we got to use um so I generally format it so let the dot width is on a new line oh just
to make it it clear um but it should still at least now fail correctly as we expected yeah uh 405 there we go so this is
a 405 not a 404 because there is a get mapped method for this endpoint uh but there's no post so it is not a 404 it's
it's it's found uh but um it's the method method doesn't match method not allowed is 405 this is this this is why like I
actually have like my ensembl tests where I've already solved these problems um I I you reference them I have to
reference them because I don't write these very often and so therefore as we know about our cognitive architecture use
it or lose it so I always lose it um I don't I don't know what the latest is I know there's newer stuff like there's the
rest client as opposed to the template uh there's a I think there's a test rest client and I think and there was the web
client but that was the reactive and I basically treat reactive is dead um I I have not looked to see what what's new
here uh it would be nice if if it was better but I I I have I actually haven't looked I should list uh hey there alw um
so go ahead and ask your question we'll get to it uh but you didn't finish your question so I can't answer until you
finish your question but go ahead and I I see it I see you so finish typing it we were so exciting while we stopped
typing like was I was I was waiting with baited breath for the rest of the question all right um so this fails for the
right reason um and uh so let's make it at least pass for the right reason so here we'll we'll again do a public um and
so here I I typically say well what this is a response to a post and so I always make this be more like you know process
or parse or or uh handle song that so I didn't like parse because parse might be delegated by this method um that's fair
that was just my initial thought process now as a response to the to the post we'll eventually redirect um which is what
the test is asking for and we'll eventually redirect back to the song import page or maybe some post song import page
that says hey we've imported this or something like that um but we'll figure that out later for now uh we just need to
make sure we've got the post and now to tell it that we want to redirect we basically return a slash so spring MVC
interprets that and says oh I need to redirect where do I redirect it to in this case slash eventually it'll be a
different name but pass yep it does all passed all right great cool um we haven't done a commit in a little while so
let's do a commit wow it has been a while yeah yeah uh and then it's probably a good time for a break oh yeah um good
enough it all right great time all right so we're going to take a a break give our uh minds and bodies and eyes AR rest
uh and we'll be at we'll be back how long do want for a break I'm good with five okay let me set my timer where' my
timer cool uh so as you can see from the banner um and I mentioned in chat uh next Tuesday I'm going to be guesting on
um the agile lunch and learn and so I'll be talking about uh my tdd game um and you can click on the link so it's bitly
td- game- lunch uh and then you can register uh and get an invite for that um and we'll be talking about predictive test
driven development basically what we're doing here on stream right predicting how it will fail precisely how it will
fail uh we'll talk about that talk about the game um about uh why I created the game what the game's about uh and there
will also be a special offer at the end where if you're interested in purchasing the game uh you'll get uh a discount so
uh make sure to join us for that and uh it'll be recorded so in case you can't make it live uh it's at 10:00 a.m. uh
Pacific Time 6 PM uh UTC um uh but if you can't make it it'll be record record and and and be thing uh so adaran asks is
it just about tdd and agile be talking about scrum as well scrum is not well I I don't think I want to go down that road
uh no we will not be talking about scr I'll leave it I'll leave it at right uh wrong screen sorry about that I did wna
uh I did want to give a shout out to um yeah it was adaran the control enter driven development yes alt Alt Enter yeah
or command enter or option enter I guess I I call it dot driven development because it's basically that's what you do
you hit the dot and you see what what um oh right because it's running the uh actually why is that failing yeah that's
what I'm thinking myself I'm like fail let's take a look see there's anything up above no themes we haven't run all in a
while have we did we uh oh this is the get request I'm sorry okay I'm like why is it expecting successful um right so
now because we were and so this is the the it's good that we ran all the tests we should run all the test occasionally
um uh this is because this test was written before we added the security now we need to go back and add the with with
mock user and that this one yep may as well add it to the whole test you so this annotation can go on specific test
methods but um this one it'll it would apply to any other test that we might add yeah uh at least for now um now this
one because it's just authenticated I wonder uh so wait a second wait a second this one shouldn't fa because this is one
that's not that's right so can we double check our config because right because I thought we put this up in in right
forid all uh let's does it yeah so let's let's let's let's add the with Anonymous user instead of with mock user because
as I said there's there's this weird even when you're not authenticated authentication it's a compiler no it's a mind
which test is this get to search endpoint returns 200 three or two but got redirection we expected successful so we
expected a 200 but we're getting a redirection because it's it still thinks it needs to authenticate um I don't know
does this apply for search criteria as well uh that's not so anything that's after the query string is is not part of
not part okay what h sh uh I'm gonna have to do a little bit more research on this because this is not going to be um
obvious uh this there's so there's something when when the Spring Security moved from NBC matchers to uh request
matchers there was some slight Edge case incompatibility with with something that that I'm not understanding so um
rather than uh waste time on that now uh let's um what's Natural Born coder saying uh that's something else ah okay um
that what do you think do you want to disable the test or do you want to no um leave it because it's only when we run a
all uh wait when we had with mock user did that not work or did we not try it with that I now it passed okay so there's
something wrong with my understanding of permit all with request matchers and it's not uh it's not an obvious solution
so we'll leave it we'll leave it at that um yeah it looks like there's some uh uh can you scroll up a bit on the top
pane yeah okay so that that all looks right um there's something wrong with my understanding of permit all because that
should work without being logged in from our tests so something something missing in our in our tests uh configuration
do you think it's a test related I I I don't want to waste time on on this right now yeah because I think this because
whenever I whenever I get into Spring Security stuff it's always like I spend two hours trying to figure out what's
actually going on got it um so we got it working with the fake user even though that yeah so that's that's that's all we
care about for for this test possible um that it's not actually using the config class uh because the config class um
right so that's that's probably what we need to do uh but for now we we'll do that later and we we I want to uh not get
get uh rat hold into into Spring Security stuff um but that's likely the the thing is when we run tests uh it does not
pull in all of the configuration it pulls in some configuration uh but not all of it and so we'd so since is no security
configuration but security is included but therefore it's on the class path that gets configured um but not using our
configuration so it gets default configuration which means every everything is protected uh so uh so let's let's move on
okay back to jir or you have something specific in mind uh well where are we X deep uh so let's so basically we're now
um we're now on 59 right because we can't deploy to production till we solve what's on with the oh we could we could if
we wanted to um I don't know if we want to do that now we could totally do that because the issue that we ran into is is
is right if disappeared oops sorry about that my browser refreshed uh yeah so let's think about our UI so we've got our
template which has basically a big text area uh it has a button um can we view it again did the button show up I don't
remember seeing the button yeah you're right I don't remember seeing it either oh there it is let's uh let's let's put
um let's put the button inside of um let put the text let's put the text area inside of a div and if you just hit uh
contrl s control s really oh for Save yeah so that causes the the refresh the browser to refresh right right um all
right so we got the the text area we've got the button um so what do we want we want basically when you post um we want
that string pretty much we'll just take it in get works for me so um this is where uh uh so let's let's go write a test
against um so we can close the preview of that tests uh so our song importer test we'll request so we'll need a new test
where um um so what should it do what should it do and how will we know it did it so when we do a post what's going to
come in to our our post request uh basically to our post mapped endpoint is basically going to be a string right um so
uh let's let's open up the song top um there it is so my recommendation and I recommend this to anyone who's using
intellig don't manually scan for tabs because we are we are not good at at scanning for for tabs um especially once you
get more than like two uh I always recommend uh either commande for the the or whatever control e for the most recent
one most recently open things um or get to know the specific shortcut that goes to class names um uh and then just type
the class name nope no that's files that's files you want just control n control n yeah that's close yeah um because
then you could just type SI and you and so sometimes if you if you if you are switching back and forth maybe you can you
you can like what we remember is sort of locations of things but then tabs move around as you add and and enclose them
and that's why we're constantly scanning you know which one is which one where where is what I'm looking for uh and and
I and if you watch people who are doing this um you'll see that that actually takes much longer than going right to here
typing SI and and boom you're you're there it seems like it might take longer uh but the the the variance of searching
the tabs uh is much higher than the very well-known I know if I do this keystroke SI enter uh it's going to take me
there with without any work I also find that it that it doesn't um the the cognitive load of searching starts dumping
stuff out of your head and so you're searching searching you found it and it's like what was I doing sort of like you
walk here uh yeah so command e enter um there's an even better one if you're switching back and forth between uh two two
files is is control tab um control tab so command e brings up the dialogue but Waits you for you to select something
control tab as soon as you let go of control tab it it takes you right there so control tab still brings up the thing
but if you just want where I was before control tab is great for for forth It's like this is this is really getting to
like super optimizing like I want one fewer press uh probably not sui that's actually where where where I was going and
I wanted I just wanted to get our uh song importer open on the top so that we could discover that we're connection so um
from the point of view of our test what we want to test is that when we call the Post method right our handle song
import and we send it a big string which is basically our tab separated values right uh what we want is we want did that
get passed along to our application so we can go ahead and look at well what method is it going to call in our
application do we have anything in the application yet I don't think so sure we do the whole parsing stuff oh the
service song service right import songs right that's our uh from a hexagonal architecture point of view that is our Port
that is our uh point of entry into our application so it takes a string uh although it does say the parameter CSV that
done so uh oh I guess where's where's your control key keyboard layouts are weird like one thing I I I dislike about the
the laptop keyboards is the function keys and and the FN key on on Mac laptop is in the lower left um on my desktop
keyboard that's where my control key is and I hardly ever use FN and I'm always using control and so I find it really
annoying that the FN key is there this is on MacBooks yeah yeah um all right so this is our entry point this is our our
our P Port of Call as it were um and so what we want is we want to say if the string gets ped into here how we know that
that worked uh is pretty much what suiga says like we should then be able to see this song in our repository so this is
where we're doing um uh an adapter wiring test we're we're checking that the adapter the inbound adapter is wired up to
our service uh and so what we need since it doesn't necessarily return any information because it's essentially a
creation command um we have to in a sense look for for for well what happens when when we call import songs with with a
bunch of things well we know exactly what happens uh it gets parsed um each song gets added and the results are in the
repository so we should be able to write a test where we call song uh the the the song importer call the Post method
directly with a string and we should see repository and we'll find out pretty quickly that there's no possible way it
could currently work the way the the controller class is implemented because it's missing the connection to our
application layer here right so right now this has no connection with anything and therefore what what we're about to do
will not possibly work but that's all right we'll we'll test drive that so let's uh finish see whoops not there I did
not mean to do that Z there we go so natural boor quarter what I use um on the Mac is uh command option o that takes you
to any symbol um because generally I actually don't find myself searching much to a specific thing I might search
globally um otherwise I'll use uh command F12 to give me the whole list and then I can start narrowing down the search
uh but I'm almost always like I don't find myself doing that a lot I'm almost always following call paths where then I'm
just doing a a interesting uh uh okay find the right I'll just put now now I'm I go with causes put yeah something like
that yeah I would I would drop the word one I don't think the number makes any difference here I think what's important
is that uh uh a song import puts a puts song in Repository yeah yeah I love it less words I always this um now we don't
care about the view uh we will but not yet uh so for import yep and now when we try to write the assert we'll be like
wait what how do we assert we don't have access to to anything right um so the first step will be well we need to wire
up our song importer to our surface so let's um let's go do that so let's uh create a song service on line uh we could
ask the song service possibly uh to to search so if we go down to line 27 if we start thinking about what we service
search by we could search by theme but that's kind of awkward so what we really want is we want access to the repository
so what we'll need to to do is uh create a repository and pass that into the song service and this is where these
application Level tests um start to grow a little bit in in terms of their setup because you're we we need some
sometimes we need fakes or or even sort of uh there are dependencies that the service often requires all these other
things in order to for it to do its job um and we have to supply those and here we're basically tapping into uh or sort
of listening or or going to be exploring hey repository you should have this stuff in it so we're not going to be it we
could assert again search by theme but since that's really awkward um we should just assert against the repository we
don't have access to the repository uh then we're GNA have to get access to the repository gotcha would we give access
to it or we we we will create it inate I see got it so before we create the song service and song service takes a
repository as a parameter we need to go ahead and create the repository and we'll want to hold on to that because that's
what we're going to query new uh I believe the Constructor is factory right create so uh these methods are are not
available outside the package and we they really should both be public create empty I presume yes do you have a
preference on that one I figure brevity is uh I'm fine with that yeah yeah so I I I go back and um I find I end up going
to a to uh Factory and a and a and a test Builder rather than than putting that stuff in uh in in the production code I
don't mind that it's there I just find that I often need more configuration uh and I found and and I I just don't like
all that extra code so so so the difference between James Shore and myself is in and me in in some of this area is he
likes to put lots of stuff in in single classes I like more in smaller classes uh so I find create null ends up growing
with all the variations and then all the stuff that's behind that is actually in that class uh so uh it's absolutely
hexagonal um um I wouldn't call the services I wouldn't have we don't really uh have all those I mean I guess you could
call that because right now it's fairly fairly straightforward right with time will be more complicated than that yeah
not much more yeah yeah yeah so when I when when I heard about Kent Beck's lumpers versus Splitters I'm like oh that's
why I'm I'm sort of constantly like why why do I not like that because they're two two different kinds of people well
it's probably more but in terms of that there there's too uh would say it's bad practice to just overload the create
method um I find a create method that doesn't take anything to not be intention revealing so I I I prefer to have
explicitly named uh creat empty rather anything yeah I think the other way or another way well one way I think of it is
um when I'm the caller if it reads more like a sentence I find that a little bit cleaner versus creating it's like oh
what am I passing to it right and now have to think about it what it is I'm passing to it versus the intentional
revealing aspect of the name right basically lets me not have to parse what's in the parin yeah like does that mean it
does something differently or not yeah yeah yeah exactly same thing I want it to be create to take a parameter maybe if
if that if that's meaningful and if there's ever going to be where there's some kind of default then I want to be
explicit about that and given that maybe this one create empty like should we but there's no overload for create so true
all right yeah so uh we fixed that let's go back to our test put in a repository yep uh let's delete line 30 because we
we don't want that and that's going to muck things up all right okay so that's all still set up yes and so now we want
to pass importer it's not built for that yet okay right so now we'll need to fix that Constructor and you can go ahead
and assign a variable a field uh if you do Alt Enter on song y yep now it's uh a red UND underline that's not a compile
error that's a that's a uh intelligent warning us that it can't autowire we don't care we're not we're not there yet
we're we're we're running with all test doubles and and we're not using Springs so we don't care about that just yet um
but let's uh yeah so that's fine um now let's let's go back to our test I'm gonna close the project window and so here
um now we can do an Repository uh we need to call our method on the songs and um sure all right so now if we run our IO
free tests uh this test should fail because empty is it alt shift F10 yeah that's the one that brings the Picker up yeah
that one I never memorize because it's so different on on the okay um oh what did we do did we break another test one
well let's not pass in repository or the create empty the song empty uh oh but it requires a service so we can just um
ah um didn't song service have a a default con default Constructor can't we service yes yeah whether that's correct or
not is uh in in a sense this is this is doing the uh more like the create null because it's creating the stuff um we
would never want that to be used in production that how would you go about fixing that what were your thoughts um so
what I would do is uh put the cursor on line 14 and hit Al uh hit Alt Enter on the top line 14 top of line 14 the top
pane oh top window got it and then Alt Enter uh replace Constructor with Factory method null um I don't like the way it
did that uh let's um it made this private and then it replaced the calling what's the part that you don't like uh I don'
t I don't I don't like that Constructor um I want I want what the Constructor is doing basically in the method that we
just created so let's 16 half sorry not 28 and a half 25 uh 24 and a half okay uh and you'll have to declare that
variable um although we could probably just put it right in uh you know what never mind delete line 25 um just say
inside the the parentheses for 25 just yeah let's run our tests see if see if anything okay just the one that we
expected okay yeah that's possible we didn't we we didn't set the constructors to be changed so it might not have uh
that that might have helped but that's fine um so now we can get rid of that private Constructor because we're no longer
using it all right so now we can go back to our test uh and now we saw that test fail for the right reason the one we
were just writing um and so now we can switch back to song top uh and now of course this still can't possibly work
because we haven't given the post method anything to work with so uh let's create uh so let's do a handle song import
let's hand in uh at the bottom in the test let's drive the change from our test um so let's create a string that
actually is a valid tab separated uh song so let's grab that from somewhere probably grab it from another test I could
just copy the whole line because true all right and then let's pass that into handles song import that'll Force us to
create uh a parameter yep um let's run our test to see if we've broken anything by doing that oh broken anything more
because we're still mainly mainly so so one thing that I do is I don't do a separate compile step I just always try to
run my tests and if it fails to compile then then I'll see that um so in this case it was more about did we break
anything from a compile point of view gotcha okay yeah I don't I don't understand why here the checks in the mail as
they say um all right so now uh now that at least there's a possibility for us to get this to pass right so our test has
all the elements it needs it sets up the repository connects it and wires it up to the service um and it actually passes
in a valid string uh and now we'd like it to work so it should just be one line of code yeah service yep yep run the
test run the tests good work woohoo sweet yeah so what I what I I I I just love this process where it's like we just add
one line of code you know we did some prepare work of passing stuff in um then boom and everything just works so now
commit so we've successfully at least done the um I think we have just about everything uh we'll need one last piece
which is um modify the HTML file to to match although we might not even that um once you do the commit then we'll we'll
try it out that okay well I think it's more than that I think the controller wired yeah I mean we've we've written the
code like we we spent a lot of time writing tests and then the code is just it just is not a lot and works so we
basically have song importer Imports song via post from from the uh HTML page is that what you said yep one of these
days I will do that once it gets cheap enough I I really I've got 700 hours of of video uh that I could I could train AI
on um I'd love to do that but not there yet four test failed yes so what we haven't quite finished um is the uh we've
done the application layer test double IO free stuff um but we've now broken uh spring so now we got to fix
straightforward it's basically all it's it's all spring tests because it can't load the application context because that
little red under wavy underscore uh in our uh importer it wasn't happy because it had no way of figuring out where it's
going to get that from right so let's tack on uh above 13 so 12 and a half let's do at autowired even though I know
that's totally optional uh I like to put it in because I don't I don't like I don't like that much magic um so no pns um
so now what we need to do is go into our uh configuration so where we're doing our Bean configurations probably in our
startup see you're searching again yeah you're right see how long that takes you y you know you're totally right that
was lame uh it's not lame it's just it's just AIT it's a habit yeah it's totally a habit yeah yeah so um let's just add
another Bean above and this one will create the um song service so we'll return a song service yep so we can just pass
in a new song repository uh right now um our song repository is an inmemory song Repository right um I don't think we
can call song repository like that because we don't have a Constructor yeah create yes I mean we could pre-fill it like
we we're doing above but but this is fine um and I have a feeling that that song Searcher is actually no long longer
valid find yeah we'll find we'll find out F10 oh okay so I expected I expected that um because we uh we are now um uh so
we're now we're now expecting a string to come in but in in this test the post is basically not sending anything and so
um the the string actually is null M and that's fine that's that's basically an unhappy scenario that we should uh uh
validate through tests okay where would we write that test so we want to write that test uh this one as as basically an
an iof free test and um what we want is uh new Test new test template what would we call this one um null and we could
be more specific we could say uh uh no missing missing uh uh songs missing songs yeah or missing text or y so a lot of
cloning here well we don't need the repository right so we don't need access to it so we could probably just use um the
more convenient uh so we need song service because that has to get injected into the song importer um but we can
basically copy line 13 yeah because we don't really care about since we're not checking the repository what we're going
to do is we're going to basically going to say when we call this method it should it just throw an exception well it
shouldn't throw an exception what should it do um that's a good question so this is at the controller endpoint uh at
some point we'll probably want uh to put in some although this would normally not happen through the web UI um because
the idea is the web UI would not because there's no way the web UI could pass in anything other than I mean unless the
unless the HTML page is misconfigured uh for now it should just red it should just redirect to to to the same page and
later on we'll we'll we'll handle we'll do some handling for model that actually might be uh although that gets a little
tricky with the with the redirects and the Flash attributes uh let's just let's just say the redirect redirects us back
to the the song Imports page so that's we when we call this but with empty uh specifically with with null so maybe
missing text is yeah uh we could say null or null or missing text um but maybe this is just null text because you said
the only way this would happen is if we don't have the figured if if if the page is correct it would hand in an empty
string which we already handled yeah um so it's really specifically it could not find any string anywhere in in the form
that was submitted by the post right okay so I think let's drop the word missing and text uh so we want to do is we want
to grab the return value of handle song import because we want to hang on to to uh and I would call this redirect
redirect otherwise you get a mess on the front end redirect equal to or yeah okay new line so if we look at what it
currently returns we if you jump to import right we see redirects to slash we don't want that we want redirect to uh
Slash song whoa if you want to do that don't paste yeah I've been bit by that once before yep run it so we expect this
to fail because it's going to redirect us to slash always that's fine so let's run tests okay oh yes of I should have
expected that but I didn't um so now we need to put in a guard Clause uh that if that if tsv songs is n else just do a
straight guard clause and then we'll put it make turn it into a require or would you just do the require right away um
no I write it and then I then I refactor it okay so there are other ways to do it but but um for example we could
actually annotate tsv songs where we can set a default for it being an empty string um but I kind of like this better
because it's a little bit more uh it's on what did I do wrong that's fine oh there we go okay yeah it doesn't add the
other one till you hit enter right you probably want to copy what you have in your test because that's what we yeah so
now it should pass and then we'll yeah okay all right um there's not going to be a good refactoring which is why I
didn't up front because this isn't throwing an exception it's doing a direct um what we can do is we can do a mapping
because really what this is it's a it's a mapping of input to where we redirect to uh so we can actually um if we wanted
to we could convert this into uh an if else we could convert it into even a switch statement um uh basically a switch
expression I personally think it's okay right now because we don't know where this is going to go and what else it's
going to do so I would probably just leave it okay I'm good with that um so let's run all of our tests to see that
problem all right night all right all of our tests passed commit uh so basically we wired uh wired up the song importer
with Service uh and fix problem with and handle y application bring a window over in a second okay um what's going on me
a second here we go this one I can use did and we want to go to our new song import page the session time retained sorry
what were you saying I was just thinking out loud sort of what like why were we re authenticating you authenticated the
last time and so how long you you're authenticated for right I have to look at the kind configuration stuff I presume I
guess I don't know if I don't know what what options are available so all right so um look at that later then so let's
uh let's paste something in interesting that little huh okay let's grab from the test correctly or you thinking go from
um I was thinking take it take it from your spreadsheet from the spreadsheet okay let's see which Let's test it for real
right now which columns we were looking for artist song title release title not format we were doing release typ did we
not did we oh I mean I guess you could hide it but uh well if you hide it doesn't come copy right column you mean from
the original design yeah oh there's like a ton of columns so there's a lot of columns we're skipping what other columns
are we skipping uh let's see because I only see D and I mean there may be stuff off to the right but we already said
anything after themes we ignore but why did right okay why why didn't we why didn't we skip because I think our document
was saying let's go with the ones that were the most important this one we didn't we didn't need so not this one the
format so we probably wna make that easier on you the user no uh but but for now we can we can hide it since we're not
going to go change it yeah interesting that's twice um what's wrong here ah there we go okay what do you think just one
line oh did somebody do did did beautiful South do a cover of Don't Fear the Reaper yes I'm not familiar with that cover
I'll yes interesting how it's got that little tab thing there for the first line uh we should fix that yeah should we do
import well no we got to fix that that that extra space so so that must be being inserted because of the way the
template uh tag page yeah uh so you want to put the closing tag right after the opening tag because basically anything
that's in between the two tags is is it's gonna put it there right yeah restart yeah you can restart is that restart
says run uh it is a success that's not what it should have slash so what do we see in the in our console output oh we
didn't send a post oh so this is a mistake on the on the HTML um we did not do a post to the right thing and by default
it does a get ah so uh let's modify our form tag because our form tag doesn't go to the right place so let's let's
configure it properly and this is this is stuff like um I've had discussions with folks where it's like oh you should
have had a test for that it's like yeah we could write a test for this but once we write it it's not going to change
very much um and it's easy to manually inspect so uh so I I think we should we we can just do it equals uh and this is
going to be the endpoint that it gets submitted to so it's so we already see it as one of the options the song import
post and then we want another one which is Method and that we want post a little disappointed intellig since we selected
the post endpoint why why it didn't fill in the method equals post for us uh I think that's all we need um we really
should attach a name to the text area even though we're currently not using it um so let's do ID equals um what did we
actually call the the variable name inside of our uh inside of importer uh we call it tsv song so let's thing no songs
yep and uh do name equals and value and uh at some point we'll change this to to use time Le but for this for now this
is fine what is it still complaining about the text area do we not have a label is that why yeah let's create a label so
if you let it do that yep uh and you can move the text area to new line and then just write something in the label it's
like uh paste your songs here or something in between no no no oh oh I that's a label yeah because uh we didn't put a a
a it interesting do we not have access to to slash can you try to do a request to just slash that's weird yeah we did
yeah put the slash there explicitly no it's all good uh let's look at the the console what did it what did it say uh so
let's scroll up a bit so we're looking for uh so we did the get so scroll down because you're too far right so we see
the get here um we then see uh text HTML that comes in and it does the get uh that looks fine understand it's unclear to
me who who that 403 where that 403 came from we'd have to do it again yeah should we have had um Network yeah we clear
clear it out in there I hate that icon because it it it does not mean trash stuff yeah it's it should it should be a
garbage can not a not a not payload post was not allowed uh you can close the yeah yeah so um mean but that shouldn't be
a problem test oh did we not we did add it to to authenticated do you think this is connected to the other no but that
was a yeah um possibly it's a csrf problem again that is not uh that's not being dumped to our console um so let's uh
let's disable csrf and see if that fixes it and if that fixes it then we can then we we know what's going on okay code
or uh so no it's here in config um so uh basically after line 14 so 14 and a dot um I forget the modern way to disable
it it csrf yeah that one and uh you want open pen csrf and then close pen and then disable and that's it so let's try it
again um what I suspect is that because time Leaf isn't processing the form because the form wasn't decorated with any
time Leaf uh annotations that it didn't stick in the the csrf token um we can examine the the the HTML when we try it
again yeah you were trying to refresh it was basically a post yeah yeah um so if we look at if we do uh sorry if you do
it uh click on elements the top tab ah there it is uh form yeah so there's no crsf csrf token in there because time Leaf
wasn't processing the form at all so it left it untouched um so I suspect that's that's what the problem is so let's
paste it and say disable us should I keep going down headers so the content type is form all encoded that's the host
that's the origin we're not we're same origin so that's fine um and the payload was was fine Source yeah so that's fine
it's you're all encoded um I'm puzzled by by this uh can we go back to the to the headers start from the top or yeah
let's start from the top okay so we're posting to song import uh I happening yeah I don't know H so this is probably a
good place for us to stop anyway time uh so I'll I'll I'll look it into this offline um and see what see what's going on
because I'm sure it's a simple solution it was not the Cs csrf token uh which surprises me um is there uh what's what's
in the console there um oh yeah was there up there's a lot aha okay so amcat is amcat Tomcat yeah Tom yeah that's the
Tomcat Handler it it uh it cuts it off to fit the number of characters um oh look wait yeah so I don't know why though
that caused a 403 that's what I'm puzzled about because oh I know what it what it was what it's doing okay so because
through an exception it's going to redirect to a slash error uh I'm confused why the browser didn't say that response
yeah so of course there's no response uh can we go back to the headers and we want to look at the response okay yeah I
don't understand why we're not seeing what we should be seeing is a redirect to slash error and then slash error is
actually not allowed so I'm confused by why we're not seeing those requests yeah because there's not much because the
other stuff is is some is just Chrome config and we'll turn up and we'll enable the error page to be shown uh so let's
add to request matchers on line 17 uh add a add a comma and then let's put in slash error right okay so you what you did
was you uh reposted the same thing which is why we got the error but that's what was happening is is uh during the post
it threw an it threw an exception um and it tried to basically produce the error page uh but it tried to produce it as
response to a post and so it's a really weird it's a really odd situation that's why we didn't see her redirect because
didn't actually redirect um what it instead does is it Returns the content of the post and that's why the refresh causes
it to post again because it never actually redirected so produced a page that we weren't allowed to see but it didn't
change the url because it didn't do a redirect uh and that's why that was that was a little harder to track down wow
okay yeah all right well that's good and we're missing a column yes SoBe maybe we did include that column well we'll
have to say that for for next time next time this will be a good getting all right so That's all folks um we're almost
there uh obviously error error handling we haven't built into our controller um we can decide whether we want to do that
next but we certainly know that we need proper uh uh proper input um so next time we'll we'll pick it up from here uh
and uh we'll also add the csrf stuff uh then we'll sort of make sure that that we can sort of do a round trip of of add
some songs and be able to find them right be just about there yeah yeah all right folks thanks a lot uh we will see you
next time um so be sure to uh join the Discord um that's how you can find out in advance when we're uh going to stream
either as a pair or if it's just me solo doing my ensembl or stuff um as a reminder next Tuesday 10: a.m Pacific uh 6 PM
UTC I'll be on the agile lunch and learn uh talking about my tdd game as well as uh predictive test room development
what we've been doing here all day or at least all afternoon and uh it is not too late uh to join the book club we have
just started we've just finished chapter one of the programmer's brain and so we're going to be discussing uh chapter
two uh and maybe chapter three we'll see how far we get but it's not too late to join join the Discord find the book
club Channel um as I like to say it's never too late to join you can always get something out of it even if you're
coming in halfway or three quarters way through the book anything else I'm missing I think that's it all right sounds
good we'll see you next time
