# Writing the Spring Boot, HTMX, WebSocket, etc. Tutorial

**Video URL:** https://www.youtube.com/watch?v=uU1TJQRaonA

---

## Transcript

no oh no n d n all right hello folks welcome to um won't be a boring stream for me but it might be for you uh been
trying to crank out this um this article tutorial actually uh and it's been a bit of a struggle because I keep getting
distracted um so I thought let me use uh Ed the live streaming to to help to help me Focus since that's worked in the
past so uh so what I'm working on is um I've been doing a bunch of playing around with with HTM X um making some
mistakes that maybe other people don't make but that I made uh and also increase my understanding of how it works and
how to use it and so this is basically a tutorial uh that pulls together all that information into uh an article that is
hopefully useful for for other folks so let's get to it uh let's click over here and let me check on that okay I'm also
using a new technique for um playing video video playing audio uh a little music in the background so let me know if it'
s obtrusive Ive annoying or uh otherwise if it's okay all right so had um made a mistake in one of my usages or a couple
usages where when you're specifying how the information is going to be swapped in the Dom basically I've got an element
and I want to swap it with something else so I have a button I want to swap it with a different button or maybe I want
to swap the button out completely um and so there are various ways to swap and for someone who's JavaScript browser
background right where you've written a bunch of this stuff and maybe you're using uh I don't know if you'd pick this up
if you're purely using a framework or library but certainly if you were writing sort of raw JavaScript uh a lot of these
swapping um types would be second nature uh these are part of the JavaScript browser API um with what's called uh up so
there's an API called insert adjacent HTML um and you basically call it on a Dom element so maybe you've got uh a
reference to a div and you want to replace it in some way or replace it it's internals um and so it takes these
different position strings so these are strings um and uh it accepts one of these four values so there's so these match
right before begin after begin before end and after end these match HTM X's um basically these four the delete I don't
know if that's any kind of standard um inner HTML and Adder HTML are actually properties of do Dom elements so these are
parameters sent to the insert adjacent HTML um or insert or insert adjacent uh element whatever you want um but the
other inner HTML and outer HTML uh uh are properties and delete is a method so we can see here in HTML is a property um
and I don't know if they call it they call it remove so I posted an issue because I thought like the fact that this
inner HTML and outer HTML are case sensitive is potentially problematic was certainly confusing to me Not only would it
not work if you didn't have all four of these letters upper case what's worse is you wouldn't get notification that
that's a problem so I'm fine if they want this right case sensitive um I would you know basically suggested that that
should be documented um because if you call let's say the the underlying JavaScript method for insert adjacent HTML and
you don't use one of these you will get a syntax error exception if it's not one values HDMX does not do anything if
it's not if it doesn't match any of these it basically just ignores it um or and uses some default which I think is is a
mistake um because if I specify inter HTML but don't capitalize it correctly I will not know until I see incorrect
Behavior hey there astred nice to see you uh so anyway that's just a uh something that um is you know really have to
think about and this sort of a general thing is like you have to think about who's your audience um and if your audience
is folks who are not JavaScript developers then you have to be then first of all it's extra hard if you are a JavaScript
developer because this stuff is innate um and you might not even think about capitalizing inner HTML in any different
way but if you come from other languages where it's common to capitalize it differently like I do in Java um and you're
not having any kind of strictness uh where you're basically warning or in the console um then that leads to a very
frustrating experience um and I've had uh folks disagree with me saying well it it needs to be precise it's like well I'
m fine with that um but if you're going to say that it must be this and cannot be capitalized differently and that's not
documented here and there's an assumption that one knows that capitalization is important um that that's a mistake
that's an assumption and in documentation you want to reduce assumptions potentially hopefully Elimina all right so
that's what I've I've learned recently sort of where does where does this come from where did these things come from so
these two are the properties of Doms uh Dom elements uh these come from the insert adjacent HTML this is just they
decided delete why not remove I don't know uh and then there's there's none so it's it's kind of you know it's one of
those is if you're going to claim consistency well that's why we're using after begin and before begin spelled that way
uh an inner HTML and outer HTML capitalize that way then delete is inconsistent um and I I know it it may seem like I'm
being pedantic but you have to be pedantic in documentation because you can't make assumptions uh and if you start
mixing things up like well you know these are properties so you have to know that these are parameters to a method so
you have to know that and this one has nothing to do with anything other than it does a remove so it calls a remove uh
element I'm fine with that being what they decided uh but then then it requires a little bit of extra documentation so I
hope to achieve at least that in my um in the article I'm writing or tutorial so let's go to that update uh let's see oh
I got a merge situation out uh so we'll that and we'll grab okay so I basically had split up uh into the notes uh and
the article so actually let well okay and what's the reference the reference is this now that's a reference for the
other ones there okay so always the hard part of of of these articles is sort of starting them um but I it latest so
what I was doing is I was map um so I decided when I was uh what I wanted this tutorial to be is eventually build build
something non-trivial um not overly complex but something that would demonstrate uh all of the things that that I want
to show and so um eventually uh I'll the tutorial will end up having uh a tic little tic tac toe game so something where
it's live updates um multiplayer um with built-in chat uh things like that so basically targeting different elements and
and having the that yeah I use that too I basically say can you can you write me sort of the the subheadings for for for
an article because it does overcome that that like blank uh page syndrome and yes I definitely don't like what it does
so it's a lot easier to edit than than uh write from scratch I may I may do that um so that's my overall goal even
though I haven't fully finished the code for this I I I now know how I would do it um so what I want to start with are
uh the the sort of the basics of of HDMX and sort of what it what it purpos is um I wonder what chat GPT would say since
since HTM X doesn't uh didn't really exists a lot I don't know if if chat gpt's training data includes much of it it see
verose like in the realm of web development and data retrieval I mean seriously uh I mean I could probably adjust it and
have it write it more um the other thing that that this that this helps uh with is um sort of seeing where where I want
to elaborate see see I don't want like bullet points like I don't want that but that's all right it gives sort of
Direction yes in the in the realm is is a great uh is great for an mission with here e uh updates to state m for yeah um
um that's why I said this might might be boring I'll I'll I'll make sure to say out loud if if I need need some thanks
for so I think I want to try and avoid because it's very tempting for me to go into a whole uh discussion of of hyper
media and the benefits and I think think I want to avoid that because I think the HTM X site um has has quite uh
basically handles that really really well they've got all the good essays uh so I'm not I'm just going to refer to those
um somewhere he does mention this idea of islands of interactivity that interesting he's using islands of interactivity
here in a way that's different uh and I was sort of conceiving it so from for wonder if that's the first reference so um
Fernando uh talks about isin of interactivity is the name given to interactive components component um for yeah I mean
that's talking more about components which is a separate separate thing that then static HTML new interaction of a page
um yeah so I think the intent of islands of where I don't know the ways using it is as a self-contained component that
knows how to do something and then uh get the updated date from the server but the way um Carson writes writes it in his
article is more about uh where there's actually frontend interaction before it finally pushes something to the back end
so this idea of drag and drop so there's interaction that's happening on the front end uh and it is until you sort of
drop it so there's interaction this there's uh animation and and interactiv happening and it's held on the front end
until you basically let go and drop it and then that gets communicated to the back end so you could say that's that's a
and you could further say that's a component that you'd like to reuse but that's um that gets into what a component is
but uh so there's going to be some things and this is where HTM X by itself is insufficient uh you probably want
something like Alpine or other sort of very light framework works that do uh things that are purely purely front end for
the user um so there's there's things where it's like uh I'm G to edit this thing so you click a button and and now you
edit it and you hit submit I still think of that as sort of an an island of interactivity but but I don't want to sort
of diffuse the term so it's basically just um interactions with the state on on the server I'm not sure I don't I don't
want to go too deep into that because I want to let folks read the the specific essays on the HTM X site and I want to
focus pretty much on like I don't want to spend a lot of time on on on this introduction I want to get right into here's
here's here's it s yeah I'm just not going to use the term islands of interactivity because I I I I think that that's a
a a rat hole I don't want to get hole so let's see so can new long time Leaf so spring MPC plus time Leaf gives us um
server side generated web JavaScript um let's see so I can get rid of chat stuff sh um for okay uh do I want I think I
want outline the next section then I think is uh where we'll start to attributes so the question is do I do I create uh
yeah I think I'll create an example without HTM to um how to do it with uh h about who decides what the button says so
if we use the example that I it um so where the button talk B Cycles the state of the server through three different
states uh you could certainly Implement that regular spring MBC time Leaf click a button reloads the page um I don't do
I do I want to go down the road of who decides what the button should say is think so I think I think it it gets a
little bit into hyper media but I think that's I think that's useful um because it testability let's say we have a
simple application that what that object is yeah uh but it Cycles it through three states um States um that's in the no
where is it State change actions that's in the oh that's in the state change controller yeah timer um yeah there there's
sort of two two aspects to HTM X and I actually think uh I mean they're both they're both useful and you get away with
just updating some State on a part of a page um but I think what's really powerful is is the hyper media and that takes
it level and I think that the testability is is then is then much easier hey suige so I'm having trouble maybe I'll come
up with a different example but for now I'm going to use the example of of a timer that has three different states done
but if somebody has an idea for other uh multi-state back so the idea is there's a button um like uh and I'll just
sketch that out so is buttons um different three states if we just want to do that so if it's sort of a an elapsed timer
I'd like another example because timer feels like it needs to be more live uh and like my Ensemble timer and um well I'
ll see if I can come up with a different example oh it's going to bug me for a different timer um h uh if you want to
explore me doing some videos with some ideas that you have the best way to do that is uh join my there and you can join
the Discord link um so one thing that might be a bit more compelling is sort of a time tracker then I don't have to have
sort of this where do I see the timer running uh kind of kind of for yeah I like that better so a task timer has has
sort of three states uh it's active so you start it you stop it uh I guess it only has two states but then there's sort
of an additional be yeah sort of like a a stopwatch but for for a task so there's so there's um like uh lots of these
tasks timers uh and you say I'm working on this task you start it and then maybe you pause it and then you resume it uh
and then you basically say okay this done and so the three states would be uh we need to completed um well is that
really the state of the task uh sure because I created a task but I haven't started it yet I've started at it's very
much like a timer but it it gets away a bit from from having to see that that timer um and then I can later let get away
from my original project but this uh uh this might be good too hey there gaar not quite sure what plan okay so I think
that's that's what what like that so if we have these three buttons um it means that they they can't so buttons to uh to
complete a task that hasn't started paed so we want the buttons to reflect the task so it can be in uh one of where
could the so the decision logic could be in the JavaScript uh but if we're talking about places I guess three places
well let's enumerate them that's case 3.1 um okay it is th switch that that's much harder to search um okay uh so one
place we could do the decision- making in the time Le template um uh so in the controller can return one pages option is
there a third option that's leaf fragments but that's still the same page um or I could do what I do in an on uh so this
current state of the task which be the the text of the button uh point yeah that's pretty much what I was doing for for
step three suiga is basically what I do in ensembl as I have a list um and then each thing has an attribute uh whether
it's enabled or not or visible well if it's there it's visible uh what I um uh which controller is that that's in the
register that's a registration form um oh right that's in the uh Ensemble view Ensemble summary view right so we have is
uh a status and it has some display links but in terms H here it is so basically I do have the uh the endpoint it hits
when you click on post so sort of pre predefined what what a button would look like um and the end basically the text
and the got uh eventually I probably want to create examples of each one of these but not not now um and for the first
version of this article I'm not going to include those one uh so that would require us in like HTML like for um so
problem number two is that you through uh so there's no logic in the front in the in the template pages um yeah I don't
know if there are any other downsides but templates for I'm going to need to to provide examples here um because there's
no way that that's examples uh um so that's a good question I uh the audience that I'm aiming at are those who are uh
are spring boot Java developers um who are at least somewhat familiar with time Leaf um and I'm I think I'm laying out
the reason uh so these are the options without using HTM x uh and folks might not be aware of all these options um it
might be uh they might be familiar with time leaf and say well the the if and switch are good but may not understand
what the downsides are um so these are the possibilities without HTM x uh and now now I'm going to bring in um why HTM X
might be might be better in this case hey there Durham for is um e so uh what all right I think now we're at the point
where I've got to write these examples hoping to push that off a bit more but I think I've got to write them uh then we
can dive into um basically how does HTM X work that gets us into uh Target and project um and so let's go and create a
new uh page um yeah if you don't know what time Leaf is uh I'm gonna have to just say go read um I think though the
example Les are straightforward enough that uh it won't require a deep understanding of time Leaf um but I do not want
to explain what what time Leaf is because otherwise I will never finish this thing uh I have an entire cookbook on on
Time leaf that remains unfinished for that reason um let's see so what do I what page do I want copy uh let's copy this
page this is the targeting demo yeah so let's copy this example for this sides um that uh this is uh time so we make the
get request to get the page and then we have a post request to state mapping and so this get mapping is something um
thing same endpoint here uh and here redirect to that so um so leave the ID in stuff and we'll take that out from XML
and so that's the button we get rid this this now becomes a submit form action like I guess I don't need the background
of green okay oh man that that that that hits um the only advice I have is is just it there's always going to be folks
who judge whether they actually know more or not um and there will likely be folks more um I mean you know why am I
writing this uh there are clearly people who know more about this than I do uh who've actually already written a book on
this uh so women has has has written a book called modern front ends with with um uh time leaf and and HTM X so why am I
writing this um I feel I have a different way of of explaining it uh in a way that sort of tracks with with how I
learned it it not I think what what can help is writing it as this is what worked for me and this is how I learned it
and this is how I understand it um and not from some you know this is the way to do it uh this is the right way you know
the only right way to do it because there are many right ways to do things um and so again sort of come at it from this
is how I see the world and this is how I about and so you know clean testable maintainable code is great uh and the more
people that talk about their experiences and viewpoints on it um the better um I'll say this even though I is there's a
difference between knowing it and doing it um but just like we have lots and lots of different books on the same topic
and articles on the same topic and music right why why write more music there's already music that does everything it's
like yes but you have and that means it's not uh that means it's it might be useful so for example one of I um I
definitely appreciate the work that's gone into a book like that um this book by uh well these days I'll I'll pronounce
his name correctly uh whim whim de Blau I think um and so uh but there's stuff about it that that doesn't work for me
doesn't mean it's wrong doesn't mean it's bad um doesn't mean it's not worth reading and and and worth purchasing I
think it is um but I found this book and his previous book uh to almost jump into quickly so it didn't quite work for me
it took me a lot more effort to understand it and that's just me right it's not every book not every article not every
blog post is going to work for everyone but the idea is that maybe you know for the million people you know the one
that's already out there works for 80% of them but maybe the one you'll write will hit those other 20% or maybe just 10%
uh and so new people will gain some appreciation or understanding of what you're talking about um that they didn't
previously have and didn't find with PE writing so that's that's the way I look at it there's also the um right in Anger
uh not necessarily be be angry or or be you know in any way sort of nasty but sometimes if you see like oh that was
really you know I have strong feelings about that uh then you can use that also yourself yeah a lot of us struggle with
this stuff um helped what is it complaining about here oh that was just highlighted okay uh so um what we want this
example is the one where time Le decides um put uh the question is what does the button do does it hit a different end
Embler so in the templates where there's the input this is submit okay so I do hit a different end point let's go that
way oops I've got too many windows open let's close one don't need that one okay what is that pink I don't understand
that uh so do I want a different end point for each button or do I want so an ensemble I do a different endpoint uh yeah
let's do a different endpoint for each one with your Java grunt how you doing desan all right astd have a good night uh
uh so this one be uh this it's going to be start and so then this is uh and these are definitely not restful URLs but
I'm not going to worry about that there's only so much I can do here uh so let's duplicate these a few times so we got
start um pause well I know a lot about staying focused that's why I'm streaming because when I'm streaming focused
that's that's that's why I started streaming is like um it enabled so uh so this is so start start different endpoint
pause pause um complete what does that look um I'd like all those to appear not that way can I do that I don't want to I
don't want to go overboard so one of the things that and I was mentioning uh when J Blah's book um it's nice that
there's a lot of uh and he uses Tailwind CSS as well it's nice that there's a lot of formatting there but sometimes that
can get in the way of wait what are we actually looking at here um and so as a novice especially if you're not familiar
with Tailwind um you can be sort of overwhelmed with and it's not just a Tailwind thing you can be overwhelmed with the
HTML structure of the page uh and it's sort of kind of obscure what are we actually trying to learn here so I don't want
to put too much sort of unnecessary um what they call extraneous uh to use a cognitive load Theory term um but I'm going
to give it a try uh and so this would be a class equals then uh can I do a flex gap uh and I don't want grid calls for
perfect so we've got four different buttons um each one has a different endpoint um and so now what we want to do is we
want to add uh the th if because we don't want to show all the buttons this is the the whole point is that not all the
buttons make sense so if these here um oh heck I may as well introduce it uh so it's going to be private state uh let's
go ahead and create that we're create H I don't want to add a Constructor parameter I want to create the the you um I
don't want to create it in a separate oh so this is going to be an start started completed now we get to figure out and
this is why this is this always feels a bit complex uh and now I think I I I know what I want to do so when I when I
pull this Co code into the article itself I want to actually get rid of all the formatting so there'll be the sort of
the one with formatting layout CSS basically uh and that'll be in the repo but even this amount of format and layout
obscures what's really going on um I and I have a project on the backlog so there there's a bunch of tools that are for
sort of writing these blog articles uh where it can pull the code in from a repo um but not the and can actually pull
sort of fragments of code and so you mark up your code uh what I actually wanted to do is basically drop all the the
extraneous formatting because when you're reading the blog one of the problems is and even if you're reading this in a
book like all of this stuff is irrelevant to the main thrust of of the article right because this just make it look nice
but this is actually irrelevant to understanding what I'm trying to explain but it takes up a lot of space and it takes
up a lot of space and you can use other CSS so you're not using Tailwind that can make it a little bit easier U but it's
still clutter and it's still really irrelevant information um so one thing I could do is have the nice version that's
tailwind and and and the one the article is just without Tailwind using just defaults um and maybe maybe I want to and
I'll have to do that manually because I'm not about to write the tool that does that because that's a separate project
and I don't need more projects out if I take out the Tailwind then this this will become easier to see okay so uh and
again this is one of those things where it annoys me um I don't know if it annoys everybody and maybe some people like
to see that but I like to to to see just the absolute minimum that still explain um Okay so we've got our different here
this is going to be uh start and so this is um start timer task uh task timer uh so start Task timer pause Tex task task
timer and resume okay so this this is pause this is all task timer stuff so I that start pause start um now I'm
wondering if I want to redo the do some fancy multi karat work uh so I'll take this word uh no we'll take again that out
put it here then fix all these okay yeah I think I like that better now I got to make the same change over here timer
like great now we need to uh put in the model um we'll do an attribute uh be let's be clear about that that's just say
um might have to do a little bit more and pull out the task timer into something that uh has methods on it that um so
our task so we'll create a task uh ask task it be timer new task timer and this is Task to started pause please okay so
this we can move make interner class timer and then we can take task timer and we can move that uh to its own thing
maybe yeah oh yeah it can be final okay fine I'll make it final even though it's really weird Okay um so now I've got
all can I guess we could run it um let's add this to the our index page and let's run it so all four buttons should be
there um uh although we're not displaying the state anywhere let's display the state somewhere otherwise it's going to
be um wrong happen oh that's why I was complaining because it doesn't go there well why didn't you say so that's so
weird we it's like it didn't it didn't tell me that this was an error it just painted it again there we go so waiting to
start by pause it it's now paused if I resume it it's now started uh although I never technically started it and then I
can complete the task um there are obviously no constraints on are you allowed to switch states that would OB that would
I could certainly Implement that but that would obscure issue um perfect however now what we want is we'd like to not
show all of the buttons we can go ahead and stop this um so the start button should only show up uh I actually don't
need this this if uh State equals so it only shows start if we're in that is the start not is the state not waiting to
start oh what is uh that's not right hey there Johnny 5G uh yes for this specific example this is exactly what I want uh
because uh I'm basically showing here's how you would do it without HDMX um but you still want the buttons to be
displayed based on state from the server um so here I'm using the the thf uh to decide and then that um uh and then that
will because it's a PO a form post will cause the page to reload then I'll get to the example uh with h doing this with
HDMX that then does not reload the page but I'm basically writing an example of to sort of make the HTM X solution uh
sort of make sense for people who who only know time leaf and what am I doing wrong with the state equals worries I you
know I as a reminder I never mind questions while I'm doing this Stu even though I I'm trying I'm in sort of writing
mode uh I'm more than happy to answer questions that for uh I guess it does need to be equals string right for hey there
National born c um well it's already a string in the template and I'm already showing what that state is and swear every
time I do this it's always like the the expression right CU When I add it it basically does string I believe that's
what's showing up because then it becomes a string I mean I could be more clear just inspect yeah so the current state
is this string thf for sanal ah feel so stupid getting this hung up on just this thing well let's add in the next one
just so I can move forward so this one is pH if uh so you can only pause if we are currently for okay that seems to work
now because now I can pause and I can't pause anymore because we're paused I can resume which does nothing right now uh
but it does change the state and so now I can okay I don't before uh um but actually that might have been correct
natural born cter so probably it might so it it looks like it was put in the map as an enum but when it when we did a th
text that's when it called it to string and that's why so I should have closely all right so that's that's what's going
on okay great so now we're now we're past were the do I want to convert it to an all right so um the start button can
show up when we're waiting to start the pause button is only active when we're started the resume button should only be
paused because if it's waiting to start it you can't complete you have to have task um if you started it then you can
complete it if you paused it you started so that's our that's our state machine look so here we have only the start
button shows up on waiting to start we start it and now we can either pause or complete we can pause we can either
resume or complete uh and then we can complete the want well that was quite a bit more work um but now we got uh now we
got our time controller next uh is number two which is we can template yeah it it it almost always is it um would have
felt shorter if I hadn't up all right so number two is we want to have different templates uh so let's go do that um so
let's go ahead and create a of uh start what the that was weird so the current state in this case we'll always be
waiting to start um so we here and the only thing we show is if um something like that and now we need a copy of this
controller we'll call this time these templates um so now here we decide show uh and hey we can use a switch statement
in fact we could use a switch expression which would be completely state yes please create the branches for me thank
something that will return something that will return something and that will return Expressions SO waiting to start
will return one this is paused and this is be um so started pause or complete and then we'll copy this from started to
paused and the difference is this is resume this is resum otherwise it's the same this is the pause template this is
always paused uh so we got started we got waiting to start started paused and now completed forms um I guess I maybe
want a new task I so so let's try that one so that's a different index for div look woh ah change no well that's
interesting it's saying I can't controllers that that's an AM how is mapping understand oh I missed one okay it is
complete yes I agree it is ambiguous I one so I I hadn't updated the post mapping here for this complete method uh and
so it was confused because I had already mapped that endpoint into the other controller that error message was was could
have been a little better um yeah I think what would have been nicer is if the error message said uh cannot map this URL
to this method because this URL is already mapped to this other method so that's why I was struggling to read that
because error messages are that I must have missed that when I did the the multi carat auto complete that'd be fun to
redirect to some someplace else all right so let's go back to one start pause resume pause wrong fast timer controller
template oh wrong and in tell you weren't you thanks so if we start and we pop pause we resume and we complete task
great I don't have Ta on this page that's not uh all right what does that look enough all right so that takes care of
two template um but basically just a loop buttons so let's go back to uh more like this one uh so instead um that was a
mistake I made last time but not going through all of them uh so be model timer all right and so we can close these
templates we can copy this one to be um descriptors and so here we get rid of the if and we get rid of all the other
buttons all the other forms um still have the current state here and here this action will be replaced and this text
will be replaced so hey there Trill frags um what I'm actually writing uh so I am writing an HT MX and and spring boot
uh guide um there are other guides on on the web uh so I will certainly not finish it today um but make sure you uh join
my Discord if you're not already there and I'll I'll announce it when that's ready um there's also a good book um uh on
HDMX and modern front ends that goes that's going to go certainly goes way deeper than I'll be going in in this tutorial
uh so that's this book modern front ends with HTM x uh and that's a book um that's available on lean Pub uh I'll throw
the link there whoops wrong button uh so that's the link to the Discord so you want to join that and so whim wh whim has
a bunch of um in addition to his book he also has a X on his blog just finding that so this will also have the link to
uh to his book yeah so that's that's something that um there's some good essays on the HTM x.org site that I recommend
reading uh that talk exactly about um let's see what do I want to close I uh so if you go to the essays there's a bunch
of things about um especially like hyper media apis versus data apis so this is basically are you doing uh like what
does rest actually mean most people use it as a very much like an RPC um so there's really good enough time to read yeah
so there's some good stuff here to read uh I'll be touching on that because one of the things that I think HDMX gives
you is not just being able to you know maybe replace some logic in your time Leaf template with something on the server
but it really sort of changes your point of view of sort of RPC versus true rest and so you end up basically um not
building apis because most apis even though they they may be called rest tend to be um very much RPC like uh or RPC
Andor cred likee which are very similar if you haven't read read these essays I recommend reading it there's also a book
that's free if you want to read it online um I forget where the link is that all right so um we now have this got action
so I want want that yeah yeah time leaf takes a bit of getting getting used to um but for me the the HDMX stuff
basically avoids a lot of the JavaScript write yeah yeah so it's and it's a so it's a it's a it's an architectural
decision to make um do you want like basically who's manipulating the HTML to change it um if you're returning Json over
API then you have to write JavaScript to transform that data uh and so that's what that article on on the HTM X site is
is talking about apis so it's like you get data what do you do uh you have to transform it whereas if you get HTML then
you just goes but I think our industry has gotten returning uh always returning Json and then leaving off to more and
more complex JavaScript to to transform it all right so model has button descriptors so what we want here um th each uh
where we got the buttons and then for each one our action text is label what this is going to do is it's going to Loop
through all the buttons that we're going to add uh and so these are this is data that we're we're going to be putting
into the model and we're going to have two pieces of data we're going to have the URL basically what endpoint are we
going to post to um and then what is the text of the button that say so let's do that uh we got the correct thing so we
still add our state attribute just so we can display the current state um What We additionally want to do is then uh add
attribute um buttons and we're going to create some new button thingies and you just imported something I didn't want
you to import didn't you did you're just going to keep importing that aren't record uh so we want our button to have two
things in it it has a string for the label so the first one is somewhere um but this actually needs to of now you don't
want to import oh uh so let's see so this will depend on now uh so start pause resume and have I been saying complete
task yes and the URLs are going to be uh Okay so we've got our new HTML page um let's add index descriptors all right so
let's take a that so this should work it's going to show all the buttons um but at least we'll have the state change and
then once we get that that working we can uh make it so it only shows the backwards isn't it oh it is backwards all
right oopsie by all right let's try that again there we go uh oh I didn't do the div to make up I'll fix that in a
second so we're currently waiting to start if we start the state changed um we can now basically pause resume pause
resume completed task uh so now we need to make it so that uh you the buttons only show what you're doing so let's do
first add back the surrounding div oh I have the each on the wrong thing that's why I'm like I thought I did that the
thing we want to repeat is the go it uh how do we want to do this um I'm going to be a little redundant because I want
Clarity over abstractions so uh we'll grab this one similar and we'll put that here but instead of returning this uh we
will we'll say um list of equals and so for waiting to start what only start um thought I had dot yet when it's started
you complete if it's paused you can resume or complete and if it's nothing and I'd like this to be a list consistent uh
and now we can say model add attribute the buttons and we can just say so I think that's all right look just thinking
about testability uh but that's a thing so let's reload this right so we're waiting to start we can only start now that
we're started we can pause and complete so we can pause now we're paused we can resume and complete we can resume and
now we can complete it so those are the three options where you can solve the same problem using uh basically your
sprink MVC controller and your uh time Leaf templates um of these three if I didn't have any other choice um I think
this last option is the nicest um because it has no logic in the time Leaf template and you still have to and you only
need to work with a single template uh where it can get a little bit iffy is if you want each button to be displayed
slightly differently then you have to push more things into what is your your sort of button definition now um I I I
want to capitalize HTM X um but that's not what they call themselves like like the library is HTM x lowercase so that's
what we will me um for yeah I love Yeah markdown is great for for uh so this is my basically the my blog um and so my
blog basically uses markdown plus some additional sort of plug-in like things um I actually use log seek for for my note
taking uh because I found it to be sort of the right balance of what I need without giving me too much and it's want so
so it's that yeah um so it's open source uh the only thing that that you might pay for is they have currently in beta
testing uh a cloud synchronization that's separate from whatever uh but since I'm all on Mac I use iCloud um which
mostly Works iCloud still has some frustrating problems where it won't always sync uh and I sometimes have to kill the
process that's supposed to syn and then it starts again and then it just works um but it's open source uh it's still has
some rough edges um but they keep making um kind of depends on uh sort of sort of two issues one is it's not locality of
behavior but it's sort of locality of of information um if you use a Time Leaf template it means you've got uh
controller code that Returns the name of the template but it really depends on on the type of information you're going
to be um finally get into our HDMX example and I've been doing this now for three hours is that true oh my God and I
haven't even um all right so uh let's write our example which will kind of be like this one except even one so this will
do uh yeah okay um I don't know if it's if it's easy per se it's certainly there um you have to set up a a context uh
and then you have to execute give it the template and then give it the context which is similar to what spring is
providing through its model um so it's certainly doable you won't find a lot of help uh but there is a there is a way to
do it um but you won't find a lot of help if if it doesn't like I I actually looked at it because I was doing it for
another project um but it was not straightforward uh because all the documentation that and all the information you find
on the web is all oriented around using time leavea with some kind of framework like spring or or or others um but the
interfaces are there because it it's it's meant to be a template engine uh and then wiring it up requires some glue code
which is what they provide um so the short answer is yes um the longer answer is it may want because one of the things
that I wanted to do was for testing the rendered HTML although this is a slightly different use case uh I didn't want to
go through through spring because why do I need spring or not go through the entire even the mock MBC part of spring I
just want it's like can you execute this method and give me the rendered HTML so I can assert against that more directly
so slightly different different use case but yeah uh if you look at the time Leaf docs probably yeah so here it talks
about how to configure and use and build the the template engine resolver uh and then here it talks about the provide
and then how to execute the template engine so essentially you execute the template engine you say process uh you give
it um so unfortunately you're giving it the name of the view which is why it requires a resolver so it's a little bit
more more work than just like here's the template text string um here's the context and then give me the output uh it's
a little straightforward uh guess you could write your own resolver because a resolver is an interface straightforward
all right so I've got uh my HDMX options let's go ahead and controller um uh let's actually start putting these in
packages how about that so let's put timer uh and then let's put the rest of timer yes I know go ahead I'll I'll get it
I'll get it one two and what did I break all good uh I'm going to take a quick break and then when I come back we'll
work on the HDMX one um and I probably won't go for much longer because it's already been a few all right so now what we
need to do is we need to pull in X um tempted to pull in the web jar version things um nine10 y that is exactly the
point of this article tutorial that that I'm writing um I argue that uh why return Json that is just going to get
rendered as HTML why not let the server render the HTML why not that's the way web apps have worked since time began or
at least since the web began um all this complexity of front-end applications I think is uh uh largely unnecessary
complexity so in general I think it's HTML um so uh because then you have the flexibility on the client to animate stuff
based on the Json you can animate stuff based on the HTML as well not sure Json I mean it's unclear what you're saying
by animate uh but if you're talking about using CSS transitions to animate things HTML is fine if you are doing
something where um you're doing something much more complex from a user interface standpoint uh then you might want to
write some JavaScript sure um and yeah you should certainly shouldn't be parsing HTML uh so I agree with that you you if
you're if you find yourself writing JavaScript that's parsing the H HTML that's getting returned uh you need to rethink
uh one of the decisions you made was wrong either the parsing part and requiring that uh and so maybe HTML is not the
right form for that but the intent is not to replace all communication with the server with with returning HTML HTML is
what you want to return if you're going to basically present exactly that with no changes to the browser and therefore
to the user but you may not need to do that so uh you'd have to give me a concrete example of what you're stuff because
for example um if we go to this oh what did I do wrong oh right I did this thing again now what oh okay turns out you
can't have two controllers with the same class name even if they're in different packages because the default uh
internal Bean name uh that spring uses is just the name of the class which is generally fine um but right so uh I bring
this example up to show what you can do but um in terms of what what's being displayed here all of the HTML um that's
making up what this timer looks like is not being done on the front end all uh that I'm getting all that this page is
doing is basically listening for websocket uh incoming websocket messages and the contents of that websocket message are
HTML that represent the exact state of the timer and so sort of again rethinking the idea that the front end has to do
everything now you may not want to do it may not be terribly efficient um so it depends on what you're doing but this is
I think a a page we see that this stuff uh just so um sure if your clocks need to run with Precision that is smaller
than the latency between the server and the client um I don't think the browse is going to work well for you either uh
because latency is what a couple hundred milliseconds so if you need that level of precision then sure do that on on on
the browser um but if you need to synchronize that across multiple machines you're not going to have a choice because
you how else would you synchronize it you're going to have to communicate that uh and so yes you could do things like um
coordinate with you know uh ntp and and coordinate with with each other and do peer-to-peer and so on and again yes if
again like nothing is the answer to everything um but what are you doing that requires second uh if response takes three
seconds to receive um the time will still be on time uh it just won't update as frequently because it's getting the
countdown information from the server the server and so this is a fundamental aspect of hyper media of something using
something like HTM X is that the server is the single source of Truth so um if for some reason there's some latency or
maybe uh you've got some some slow proxies along the way or something that's causing that much latency um then yes you'
re going to get a very jittery timer uh and you might have to then rethink what what what you're doing but the timer
will always be up to date as of the last uh message that it got but if your latency is three seconds for everything then
what well then I'm not sure what else you're going to do I mean again it all depends on what your application is going
to do so you're you're basically like you know this is a um you may not realize you're using a a a technique of of
argument that basically takes every response I I provide and throws a speed bump in front of it and that's I think the
wrong way to think about it um I think you need to think about is what are you trying to do what is your problem and
does something like this solve that and not every solution so again you're using the term animation and I'm not clear
what what that means for a drop- down animation um that's likely going to be running solely on the client right so uh
transitions um those kinds of animations that don't require new data yeah absolutely that runs in the browser the point
is is that the thing that generated the HTML and the CSS comes server so HTM X by itself it's just JavaScript right so
it's not doing anything magical um and so you may find in addition to HTM X if you want certain UI animations and
Aesthetics and and accordians and things like that that's not data that's not state right that is how am I present ing
that State uh and that you can use something like Alpine to to do that um but in terms of what is the current state
where does it get that state what are my server all right so we've got our HTM X is next um no because HTM X targets
reloads so it does not reload the whole page uh so that's exactly what's happening here um the only thing that's getting
reloaded on this page is uh the div that contains the timer right so basically this everything else remains anything
else you have going on on the page remains um so it basically it does a fetch or a get request and replaces the contents
of this div with whatever came back from the the server so that's the benefit of HTM X over uh purely server side um and
r on the browser to reload the entire page is that you don't have to reload the whole page so HDMX is doing things that
you probably would would do anyway if you wanted to say I want to just have this portion of the page change without
affecting anything page all right so what we want here is want none so what this is saying is when this div loads um it
will will trigger a get request to get the current state contents means oh hey there so Tech welcome dinner yeah I'm
gonna need to break for for for the day by I'm doing some HTM X and spring stuff um okay so we got our current state um
this will be targeted so we're not going to have the template uh uh this um yeah let's target actually let's spam we'll
set the ID to um and then what we want is div um here so for that we're going to do uh request uh oh but that's on the
button so we do here actually we don't need any of that here because that'll get loaded upon uh the initial load so all
we have to say is ID equals against uh HTM X options task timer State there's a different endpoint from the thing that's
going to load up this page in the first place yeah so we're about to see what what what happens on on the server side so
so the goal of of this um is when this loads it's going to immediately do a get request uh and that get request is then
going to go to the server and the server is going to respond with two pieces of information basically two HTML elements
uh one is going to replace the span here and another is going to replace the button div here to provide uh the actual
buttons so it's going to return the HTML that will content um I don't need anything else do I at it am I really selling
it I don't think I've sold it yet um so what we need from our controller uh is let's let's get rid of this for now this
down here so we want um this page this endpoint to to return this page which is test timer option hmx and that's all it
returns um we don't even need to put the model date because we'll get that separately now we need the get mapping that's
going to return uh the con the the basically the current state uh and the buttons so let's do a get mapping and our
endpoint is this now this one is going to be different um because I don't want to use a template uh so this is uh no not
request body response body so what response body does is it says instead of returning the name of a string so what we'll
say is return um and we'll return a of we'll do multi-line strings because HTML hey there H um you can ask go ahead
answer uh so that's the span and then inside the span we want the current state and so what we're going to do is put a
percent s uh and then we'll close the span and then we will say state does so that's uh this endpoint let's go add this
to our index all right and let's take a look uh we can well actually I'll leave that open okay so what happened was and
you may have seen a little flash of of text change um is uh as soon as the page load this changed this span here um
because it was triggered by uh this div here saying that it should upon load do a get request and what we sent back was
we spent sent back a span ID in fact we can look at this if Network and so what we see here is returned and so then HDMX
basically flopped it in replacing what before uh let's see so using the VM option Java log and config for logging
purposes um uh what are you using a framework are you using a library what do you what what kind of application are you
writing because that would depend on the framework or library is using for your application in general I don't like
passing VM options um because those are often hard to configure uh so I either do environment variables that get read in
at at startup time um but it totally depends on on what application of so if you you're using spring boot uh you want to
use the application properties to specify all your login configuration in fact you want that to have all of your
configuration uh because the nice thing about that is then you can have different profiles and and it can look at also
environment variables and things like that um so different Frameworks will will sort of configure things so it's it's
it's less about the web API it's more about what is the context in which your code is running and so Frameworks will
often do a lot of things for you configuration is one of the main things that the Frameworks um provide um and spring
has one of the most complicated although for for good reason uh ways of of configuring yeah so if you're using something
like um you know javalin as your web routing and server support uh then your configuration would be very different it
might even be completely up to you um but in general I don't like to put configuration stuff on on command line
execution because very easy for that to get munged or dropped or you deploy it to a different server and now that isn't
there um it's a little bit better if you're stacking everything inside a Docker file then you define that but it's very
easy for that stuff to get lost um and then all of a sudden stuff isn't isn't working right so I much prefer to have it
a bit more visible in in a config file uh somewhere or in an environment variable if you want it to change across
different different environments um so let's see can we do some throttling what would that look like page so it notice
the current state here and now it changed right so the throttling basically pretends it's a very slow uh uh interaction
and so that's where um we can see that uh the page loads doesn't have the current state until it fetches in now if that'
s a problem if you know you're going to be on a on a slow connection then what you can do is when you first render the
template put in the current state so you don't have to wait load but normally it's going to look like it um so that's
just the timer State we still need the buttons so let's go and buttons so what we want is so so what this um what this
what this tells HTM X on the receiving end is hey look for the thing that has this ID which is over here and replace its
inner HTML with whatever this this is and this gets to be the current state now turns out this element type is
irrelevant work and we can inspect it and show that it's still a span because it it needed something to carry it needed
an element to carry the information over but then it threw away the actual outer parts uh the element Parts because it's
just replacing the inner HTML and so I actually tend to call it a swap container to sort of show that that this element
because it can be confusing it's like hey I returned to span why is it showing up as as a p or is a div because HTM X is
not paying attention to this part it's only paying attention to what in between um all right so in addition to returning
that we also want to so the ID is going to be our button div right so it needs to match this swap uh then iner HTML and
by the way this case matters HTML uh and then what we want are the buttons um so here we're responsible because I'm
returning raw HTML uh I'm responsible for rendering that one grab this one and technically it's the form container
container windows why it's tabing as off uh and so here we don't want a th action we're not because we're not processing
this through timely so it's just a regular action um and it options and that's it so this will only show the the form
button um but we get to decide what this that and there we go there's our start button and our start button looks like a
start button is a start start button it's got the form it's got everything um it's got the action in a sense hardcoded
but it's only hard-coded from the server the client has no idea like if we decide we don't want this button we want some
other kind of thing then uh the client doesn't care it just renders it and so what we want is basically uh one of these
for each possibility so start pause complete and then we do a similar thing to what we did for the model has the options
is now we decide how to render this um but we get get to test this easily because it pretty much we have code that says
based on the timer State what HTML do we render and then we just render buttons and I got to go change the security
stuff because we CH we move stuff around in terms of actually why was that a 403 I that was unexpected um let's go look
at our security config should be a permit all uh oh it must have been an error page that's why so we uh we want the
forward I forget how we do this uh so it must have been an error I'll have to figure that out in a second that why there
we again I feel like this should be the not oh did I not say that those were posts no those are oh because it's trying
to do a form ah okay and this is the other difference um we don't want these to be forms because we don't want the page
to fully reload what we want is actually to use HX post so let's fix that uh let me make sure the security thing fixed
the error page so still not sure what I was trying to to do maybe I was trying to go to some other page but anyway I
know what the irrelevant right so we don't want the same old buttons that we've had before um what we irrelevant uh
instead what we want is an endpoint um and that endpoint is that and then we can get rid of the form and get rid of the
form and bit return Tas timer state body in fact all these are response bodies which really is I'd like this one to be
not response body but this uh there may be a better way to do that but I don't hand redirects we basically return
happens all right so we've got our network um we're getting a 403 why are we getting a so why are we still getting a
time we need authentication is on the websocket otherwise any request should permit all right that's the right way to do
it right do we need to permit all first and then authenticated but how did the other stuff work security stuff Spring
Security stuff drives me crazy okay that's what I thought we can't configure the request matches after we've done any
requests that totally makes sense and that's what I um but then I don't understand why working it's not a csrf issue is
it it crsf because I'm doing a post but I'm no longer using a form um so one of the nice things time Leaf does for you
and this the downside of using of generating the HTML yourself um is that uh if you run it through the time Leaf
template and it sees a form with a post it will stick in a crsf token for you uh since we are not doing that I wish it
gave some other error message than 403 Forbidden when you don't have a crsr csrf token s all right so now it's working
and so now what we can note is that the page is not reloading anymore so when I click resume the only thing that changes
are those things that were highlighted the page itself did not reload so I can uh pause resume and then complete task um
and it's only uh these buttons that changed and this this span that changed um the rest of loaded um the last step is
now we only want to show the buttons that we want to show uh but I'm going to stop here hope you all learned something
but if nothing else uh this made me uh make really good product so I think uh um one of the hard things about writing
this stuff is is the examples and so now I have really solid set of introduction hi there uh if you're going to ask
something or or make uh a chat comment um foref for English here otherwise I saying um all right so next time so
probably this weekend I'll be streaming um more on this um basically more on me just writing this article uh so the next
step is um I want I want to write a test for this to test drive this because that's why I actually prefer going this way
as opposed to going through the time Leaf templates um but I think I think I'll probably also uh create an example that
uses time Leaf templates for for these buttons but the main thing that that changes is instead of having these buttons
inside of a form that we submit the whole page you YouTube's algorithm it's interesting and so the the two benefits of
this are um it makes this page a lot simpler because all of the things that are varying according to State uh I can
change on the the back end and also most importantly is it doesn't reload the whole page and so it's not obvious on this
page because there's not much else on the page but if there was a lot of other stuff on the page you would see that it
wouldn't get rendered uh and that if there's other state on the page you wouldn't lose it uh and so uh was mentioned
earlier you wouldn't lose any other listeners that that um I haven't gotten to that part so right now I'm just always
returning all the buttons but that's not what that's not the final Behavior I want uh the um the behavior that I have
for the is so here the only options that are shown uh are the ones that are available uh and that's that's what I'll end
up with uh and so I'll basically have four different ways of doing the same thing so you can compare and contrast uh the
different the different mechanisms so I just haven't gotten to um programmatically changing the stuff and that will I'll
time all right um thanks all folks for for hanging out with me um while I struggle with with writing this stuff and
coming up with the good examples um I I could do swap delete but uh I may as well just reload the the whole thing um
because if I delete it then I want to add the button back right so when you're swapping between pause and resume um
somewhere you've got to add the button you deleted back and so it's just as fast to just say throw away what you had
before and show these buttons just throw away what you had before and now show these buttons there's almost I don't
think there's any perceptible difference because it's all Dom manipulation that the browsers are optimized for and I
think conceptually it's a lot easier to just say here's the new state here's the new state instead of just saying well
delete this but add this unless it's not there and that's just too complicated um so I think uh Delete the the swap
delete might be useful in cases where you actually are deleting something so if you've got a row of of you know contacts
and you delete one of them then yeah yeah why what's the benefit right so the for me the one of the the benefits of this
is I don't have to write more complex stuff than I need to I basically say 100% this is what is going to get pushed to
the browser and that's what they're going to see um starting to play around with visibility I I I'm not sure what the
benefit of that is and it just makes the code more complicated so I'm very much in favor of simple brute force and let
the browser and the rest of the world optimize it because if I'm going to get all complicated with you know different
visibility and and hidden and and and um yeah that's what I'm doing I'm swapping the container so the entire contents of
the of the div go so this goes away and I get buttons yeah I mean there's always a lot of ways to do everything and and
I'm optimizing for what is the easiest to understand what's the easiest to test uh and um for this kind of stuff I'm I'm
not at all worried about try out optimize performance or optimize how much data is being sent across because this is
bytes um and this is Dom stuff that the browser is is excellent at so I'm going to optimize for my my understandability
uh or the code understandability uh and and testability yeah because otherwise I'm you're you're writing a front-end
framework and I don't want to do that and that's the whole point is to get away from that um and I think there's a
certain there's a certain way of thinking about like uh like stop optimizing code like I have to laugh because you know
some of it is like when you're using a front-end framework or even not and you're just writing a lot of JavaScript I
mean you know there's so many websites out there where it's downloading a megabyte of code code like I'm sorry a
megabyte of code and yeah okay it's not a trivial app but it's not that complicated that's a megabyte of code and I'm
like what are you doing um so I'm I'm happy to to send across a few extra bytes uh each time with some request because
it's less than megabyte uh if your container contains an input field that has unsaved data in it um yeah if yeah no
different again no different than if you wrote JavaScript to swap out um input Fields because you got some new Json
again there's there's just no difference you got to do the right thing so if you hit um if you have data in an input
field and the the way it gets swapped out is because you did a post and it sent back data then I'm hoping you send the
data across with the post um but again there's it's just running JavaScript and so if you do the wrong thing you're G to
do the wrong thing there's nothing going to protect you against that yeah and if you do a post the server gets it uh and
it will post it back that's what it does um or it could leave it alone I mean it depends on what you're doing like
that's the advantage is if you've got you know five input Fields um and you want to do do a post well then don't send
back something that would get rid of those input Fields just you know if if it's if it's interesting to or useful for
the user to reuse those fields with the content that they already have then don't replace them you don't you don't have
to replace them it doesn't uh you know so it all depends on what are you targeting with with with your ID so here I'm
targeting um basically the actually this input right this this div right here but you can return a bunch of different
elements that Target different things all all place so there so state is a funny word there is user interface state but
the state that we're talking about where there's a single source of Truth is application state which is held on the
server so things like you know if I'm filling out uh an address form I probably wouldn't do this with HTM X but let's
say you're filling out an address form um and I dropped down California because I selected California it can now
populate um perhaps the zip codes that are California so the gooey state is the current state maybe state was a bad word
um let's say I selected zip code first right so I type that in so now there's UI state of the ZIP code that's UI state I
haven't submitted it yet to the server um or if I have a drop down of you know is this being shipped uh you know with
one C you know carrier or another um and that affected something else on on the UI well that's UI state but until I
actually tell the server tell the application I want you to process this it's still it stayed on the browser so browsers
have state but it's local State and the idea of hyper media uh and hados is that the server state drives what you see on
on the UI but there still going to be gooey state right what you know what form is is is shown and things like that but
what you get away from is the is synchronizing application State and that's where you get really complex front-end
applications that I think are overkill for most for many use cases um is the synchronization of application State that's
where you get in where where I just see an overwhelming amount of complexity and bugs uh on on applications is because
at some point you have to take the information that's in your browser and send it somewhere otherwise what are you doing
yeah there's certain types of applications that completely run in the browser and don't talk to any server well that's a
different kind of app there's completely a set of apps um where where you do need much more complex State manipulation
on the browser so for example canva or Miro right these are very complex front-end applications uh in the olden days
they would have been desktop applications and it's not until you hit save or maybe as you manipulate things it's saving
all the time but the rendering and and the current state there's a lot of synchronization of state and that's where
things get complex but many many apps don't need that level of State application State uh synchronization end and State
Management is is the source of so many bugs because now you're out of date and who's right is the client right or is the
server right and how do you know and what if you missed a message um transmitting from the client to to the server and
you just went on your Merry way and then at some point you had to synchronize it and there are mechanisms to do it but
they are more complex and so if you need that complexity then use it but a lot of times I see it's like you got a basic
information business app here you don't angular yes why not if your latency is slow and it's a simple sum then maybe you
do that on the client side but the minute you have other calculations like what about shipping what about tax does ta
does shipping affect tax is it inclusive or exclusive does it depend on where it's being shipped to does it depend on
where it's being shipped to and where it was purchased now you get into domain business rules and then you do not want
to calculate that on the client so if it's a simple sum of a couple of elements sure if if because you want an immediate
response you do it on on the browser but once you get to anything more complex you want the server to do it because a
calculations and it's very easy to not realize you've crossed the line from a simple sum of a few numbers to now
reimplementing those rules on the front end and now you have code to keep in sync between the front end and the back end
and that's where you get into trouble because now you've got the front end calculating things one way you submit it and
then you look at your invoice and it's like wait a second that's not what I saw on my screen and you do not want that
and if your latency is is is very long where you might say well hey what about uh getting good response times like well
then fix that problem because you don't want to put the same code that calculates the same thing implemented in in even
if it's they're both front end and back end in JavaScript they're in different parts of that the front end is is great
for for manipulating things and getting immediate reaction to moving stuff around and and typing but um there is no
reason why servers shouldn't have less than half a second response time other than your servers are too busy or you're
writing code that's not great um or you're working in in uh conditions that are not um ideal for this kind of
application which case maybe fall back to a different kind of application or maybe users have expectation that it takes
a long time right if you're in a place where you've only got you know downgraded 3G equivalent expectation and it's
certainly better to do it this way with an HTM X basically a hyperm media like uh design than having that poor person
who's who's on such a slow link having to download a megabyte and a half of of JavaScript code because they're not going
to put up with that so this is way better and yeah they might have to wait a second or two because they're on a slow
link um but that's way better than downloading a megabyte and a half that probably well all right all right time for for
for me to uh go get ready for dinner and such um as a reminder uh I have a Discord where we talk about all these kinds
of things um so go ahead and sign up for the Discord if you have questions about stuff you've seen on this stream um
there's a data channel for that uh we also um run a book club free book clubs so uh we're currently reading a book
called the programmer's brain and it looks at sort of how do we learn and how do we uh write code that that is easy to
understand and what are and really going deep into sort of a little bit about how our brains work and how that affects
the code that that we read and so um uh we run those every uh as basically Zoom meetings for two hours every Sunday um
the next one is Sunday at 10: a.m. Pacific which will be with the daylight saving time change uh I think 5:00 pm UTC yes
no yes because it's seven it'll change to seven hours um so sign up at the Discord uh if you're not already in the book
club and you want to join it's never too late to join we're we're only on chapter three and you get access to all the
previous recordings and such uh so hit me up on the Discord uh um that's about it uh so I do not we do not stream the
book clubs um mainly because I want folks to feel like they can talk about the things they are experiencing you know
relating what they read to their own experiences um we may do a book club where where we stream it as well um but for
now it's it's pretty much uh sort of anyone is available uh anyone can join but um it's it's private to only those who
have joined uh but if you do join uh you get access to the to the previous recordings and transcripts and so there's no
there's no um pressure to to speak or say anything or even be on camera um you you know if you if you join you could
more than happy for you to just sit there and lurk that's totally fine that's uh that's that's not not a problem all
right thanks folks uh I will see you next time uh have a you
