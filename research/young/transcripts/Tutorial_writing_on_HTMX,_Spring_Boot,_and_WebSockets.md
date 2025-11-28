# Tutorial writing on HTMX, Spring Boot, and WebSockets

**Video URL:** https://www.youtube.com/watch?v=uNSnRObAwHE

---

## Transcript

all right hello folks uh welcome to a rainy stream here on Tuesday Tuesday afternoon my so I decided to uh continue
picking up from where I left off on my last uh writing stream we were looking at um this stuff no this stuff this stuff
there we go this stuff uh which is um HTM X websocket spring boot um and basically looking at the different aspects um
and basically all the pieces that I used that I discovered that I learned about that I implemented uh when implementing
my uh countdown timer or actually rotation timer not countdown timer uh rotation timer for um my ensembl which I will
get back to um but I thought uh since my brain is not fully in gear I did a presentation on my tdd game this morning and
uh since it's raining so I can't go out and do a run um I figured I'd do some writing so let's let's see where we left
off in our writing uh so uh here so one of the things that uh that I introduced um uh or or was starting to write so I
want to write about HTM X um how the swapping Works what's called outof band swapping uh and basically how you can then
use those to create a nice little uh tool um and one of the things I realized is I was writing this uh which is why I
like doing it when I'm I like writing tutorials on stream because it forces me to to narrate and I find that that's
where I can find those Corners that I don't quite have fully understood um and so one of the things that I found was
actually there was stuff I did not quite correctly in my uh Ensemble timer um but worked anyway because uh a lot of
times when you learn things you put a whole bunch of things in and maybe some of them are some of the pieces aren't
necessary or some of the attributes aren't necessary or some of the code isn't necessary um but you're not quite sure
what actually is necessary and so one of the things I want to do with this tutorial is very much um kind of explore
what's what's necessary and what's not so I wrote some examples here with with targeting uh so let's go ahead and run it
and remind myself it looked nobody else uh where where I page um so here is one of the things that that I like is uh and
I try to do this as much as possible um is not just provide examples but provide negative examples uh one of the things
we learn from is not just what the right way to do things is but what happens if you do it in kind of the wrong way and
that can help us understand things oh hey Josh nice to see you uh so this is the second stream I'm doing with writing
this stuff um so there's one more uh before this one um and then there the the stuff I've been doing for the past like
two maybe three weeks uh on ensembl that's where I was basically trying to figure out how to use this stuff so um
depending on what you want to know uh you can either go to the twitch videos which are the insem specific stuff uh or I'
ll paste a link to the previous YouTube video um but you it so um what I did was I kind of colored this a little bit uh
to sort of indicate this is this is the right way or a way that is sort of proper uh and this is indeed not quite
appropriate proper way to do that um link yeah so for those of you are just go to searching There's the link so the the
I think the the fundamental aspect of what is HDMX is you could totally write this in JavaScript and honestly it wouldn'
t be a whole heck of a lot of JavaScript depending on what you're trying to do but the idea is that if I don't have to
write JavaScript then I can do it more declaratively um why wouldn't you uh so if we look at kind of think about okay
what what's what might be a goal what might be a thing you want to do um with HTM X is I want to click a button and have
it fetch HTML from the back end from the server and then basically inject that HTML into some place on the page right as
they call it the Dom which is the document object model which is basically all the elements all the HTML elements that
are on the page so um unlike the HTM X documentation I like to show you kind of the before and after so one of the
issues I've been having with the HTM X documentation is it kind of shows you how to set it up but then doesn't show you
well what does it look like after it's retrieve the information from the server what does that look like um and what
exactly does does some of the stuff mean uh and I think that's you know the nature of of sort of documenting your own uh
libraries and products s can be difficult because you you have the curse of knowledge I certainly did not have the curse
of knowledge so I came at it from a very um and and there's some interesting stuff and I mentioned I talked about some
of this in the last video of like it says it correctly in the documentation but what we do when we're reading stuff and
we don't kind of know what's important what's not we tend to skim a lot which means when you're writing esally for a
novice that doesn't mean somebody who is um you know early in their career doesn't know programming very well a novice
is something where it's like I've been doing this stuff for forever uh sort it seems um but I don't know what what these
specific things mean and repetition and good examples right we tend to when we're looking at tutorials and so on is we
tend to at least I tend to and I find most people do is you just look at the example in fact sometimes you might skip
all of the actual narrative and just grab the example and paste it in and this can lead to problem so one of the
problems that I talked about um uh recently was when I was pairing with Mike Rizzy we were trying to call a method using
some stuff from the documentation but because there were two places there were there were two CL there were there was an
enum called dispatcher type same name same values but in two different packages the documentation didn't say which
package to use now it's kind of obvious you try the one that didn't work so you try the other oh that worked but what if
there's five packages or eight I've certainly experienced that then it's then it's like well which one do I use um and
so I find that that examples that are incomplete or partial and leaving out some some details you may may not even
realize it if you're writing yourself but that's why we we you should have uh test readers as well as people who test
your application um so anyway so what I want to do with with this tutorial is is very much uh what have I what have I
learned and provide some some good solid examples um hey there tkes welcome so this example uh the targeting example is
basically how does how does the the HX Target thing work right so um I want to replace the div right so I want so my
goal is to replace this div with content received from the server so I might have an ID here and uh I've got my HX works
uh yeah vegan eyes um yes absolutely import everything from java X swing that will totally fix everything um I I I love
S I mean I don't know I really liked using swing I did a lot of work with swing I taught a whole bunch of courses with
it develop non-trivial applications with it um and every time I try to use Java FX I'm just totally lost it's it's again
it's like I I know kind of I know how awt Works underneath I've I've custom written stuff on top of awt directly uh uh
but Java X I just haven't worked with enough to to to get that you know intuition um so here we do an HX get replace div
so what this does is it does a get request takes whatever is returned and the question is at least the question I had
was where does that go now you might not want it to go in the button but that's where it's going to go because you
didn't specify anything else and so what happens when I click this is it replaces the button text itself probably not
what you want but again it's a negative example which is something you might try and wonder why is it doing that uh yes
directly on awt before swing existed um uh I worked on a project where we had implemented a really beautiful interface
um very much before its time for was actually an applet uh technically because it was just it ran in browsers when
applets were allowed to do that um and it was called design omatic and it was for Designing custom stationary uh so very
much before its time very much ahead of its its time in terms of of anticipating what swing would would do um and so
then when swing came out it's like oh of course yes you solved it pretty much the same way I did uh it was just bad
timing all around product didn't go anywhere but it was really nice I wish I could find the source code for it I know
it's on a floppy disc um uh two exensions while trying to improve typing skills do I type with my 10 fingers no I keep
trying uh every every few months I I I make a conservative effort to start learning how to type properly again and it's
really hard to to to to build that habit um I forget the names of the tools I'd have to look them up if if uh if you
can't find them there's there's some that are typing tutors that are specific for coders um and I think that's the best
way to go because regular typing teachers they're not going to teach you the you know a lot of the syntax we write is
you know curly braces and and parentheses and equal signs and plus sign and all that kind of stuff that generally is not
what's what's what you get practice with with most typing tutors so look for a coding specific one um yeah uh in terms
of keyboard I mean I'll I can tell you it's it's a a keyron um I forget the exact model it's a 10 keyless but the thing
about keyboards is they're very much like any other sort of personal item you got to try it uh see if you can try it
before you you like it uh some people you know especially mechanical keyboards everybody's got an themselves so we know
that uh what HX get does is basically Whatever Gets returned is by default replaces the inner content right so the text
that was on the button Buton gets replaced not what we want what we want is we want to Target where the return value
from that get goes um so in the in the in the working example we we add on an HX Target so here we're saying when we
call replace div whatever HTML you get you get back put it here and uh unfortunately intellig doesn't know what this
target is but we know what this target it is it's basically this right here so this is using the standard uh sort of CSS
syn query syntax um so pound sign for or hash sign for for an ID reference um I also learned last time that you can
Target multiple IDs if they have the same ID which you generally don't want to do IDs generally should be unique so um
this one basically says hey whatever content you get back from this HX get uh put it here because that's what we want
and so if we do that it does the right thing right so it replace this content here now you might want to do something
where this is what I I call um uh these two are basically uh controlled by the client the client is saying what the
target is either it's not saying it at all in which case it doesn't go where you want it to um or here it's basically
indicating I want the target to to go here um so the client is deciding here um the uh server is going to decide so
we're using what's called um swap so here again we've got our h checks get with no Target and as we saw with the first
example it would go right here unless unless we're calling the replace div Target of OB so that's this one and notice
what this is doing so this is this is saying um this div has this ID and what we want is we want the the out ofand swap
to be true which what that does is it tells HTM X when it receives this content right when it receives this HTML to find
this ID if it exists if it doesn't exist I'm not sure what happens I think it just ignores it but actually that's an an
interesting question we just try that out um so it looks for where this current ID is uh and then swaps it with this
content because we said Swap and so out of band means the scope of the HX get was this button and so it's out of scope I
don't I find the outof band terminology to be Mis not misleading but just confusing as some other way of signaling and
maybe that's kind of it but I I think what's more important is is out of the scope in which the get was performed right
so here the get is it's on this button element therefore the scope of that is this button and therefore if you do
nothing else it replaces the contents of that button but if I want it not to replace this but to replace something up
here to me that's an out of scope um out of tree hierarchy whatever you want to call it we can specify the target but
the target can come from unless unlike the client before where we did an HX Target uh the server can decide where is
this going to go so it's said so when it it kind of works right we we we got the replacement in the right place uh the
problem is the button now uh its content is gone uh Hey sin bed um I am currently using WS but I don't know that it
would matter I'm only doing that because I'm not on https locally uh but it should WSS so this is a problem because I'd
like the button not to lose its text and if you think about um if you think about it's like well why did it do that well
what happens is the out of band swap right so this is what this is the HTML that got back and that gets sent back to
here and HDMX says oh you're targeting you're doing a swap out of band so therefore I'm going to match the Target and
put it there um but because you didn't say a Target here it means whatever other content so you can actually have
multiple of these outof band swaps you can have you can Target five different things five different places and return
call um and so basically what HTM X says is whatever is left over that doesn't have a an outof band Target gets put in
the button since there is nothing else there's just this one div it basically replaces it with empty and we can prove
this by saying it right so we see leftover text in fact that might be more clear as an text so but what if you don't
want to change the button what do you do well what you do is you tell HTM x and by the way for this element don't swap
it um so you can tell tell it with this HX swap because what it's doing is is it's taking this text and sending it back
but if we say HX swap then it it and so we can text right and so we see that the div was replaced but that leftover text
nothing happened to was basically completely ignored uh and our our button text looks fine so this one gets replaced
with the leftover text this one doesn't um and we can press it multiple times right each time it does a get request
takes the div and we can see that that's why I put the time here is is we can see that change as I click it same with
all these um this one though is changing the button text itself and that might be useful right because we might do a get
probably not a get request but if we did a post request it might change the state which means the button text might need
to change so with my timer it needs to resume Endo functor zero at least 80% yes um 100% agree like I think most single
page application whether you call them a framework or a library I think it it's irrelevant to me the question is is do
you have like a separate build cycle for your front end and if you do um I find that really problematic I find that a
level of complexity that yeah 80 I agree 80% of warranted um I mean honestly they could have been done I mean again HDMX
is not some magical thing it's you know JavaScript code not a whole lot of it uh but what we tend to do is we tend to
copy we tend to copy what we see and so this is where you see you know shifts in in the industry happen because people
start saying oh this this works really well and then people start using things without being thoughtful about is this
complexity worth it it's not to say never use react angular view but be thoughtful about it does this complexity that
we're about to take on and you may not even understand how much complexity you're taking on um is that worth it because
if you don't need it and you're just presenting what are sort of you know you want to have some amount of interaction
without relo the whole page and some pieces of the page uh what is referred to sometimes as as is of of interactivity um
you don't need a whole framework to do that and I I I just I've I've worked with teams where where they're just buried
in that complexity that's that's not warranted um there are certainly applications where that are heavily interactive
and hold a lot of state and a lot of complex State um you know certainly something like you know where it's not just you
know what I would call a business app um there's certainly a lot of those where where they're that complexity is
warranted because you're sweee yes absolutely there's going to be parts of an application that require a lot of
interaction with with the back end um and you don't want to reload entire Pages um and this is is where I think is The
Sweet Spot of something like HDMX uh or just like a little bit of JavaScript like I went back to my tdd game that I was
writing using Vue and I'm like I don't even know how to build this thing anymore because it's it's a couple years old
and like I don't even know if I can build it anymore it's using vue2 and vue3 is the current um and I'm like I don't
really need that uh I me it was fun because I was also learning it and and doing some other stuff with it um but yeah
there there are lots of applications that have space for that interactivity I don't know it feels like rant um
absolutely if you need that complexity then you better test drive it uh and there are folks who I I totally think know
how to test and tdd your your frontend complexity um but boy the last thing you want to do is is like deep sit in the
browser debugger to h i just it hurts me to think either ah I I interrupted your you're watching it so um so pretty
happy with these examples um uh and I like the leftover text I think that's actually more clear than blank and this
would be ignored text but as I was mentioning like there are times when you actually do want the button to change right
so the the toggle situation you click it right before you click it it says pause you click it now it says resume right
and this this gets to the to the to the underlying Foundation of why it is getting HTML from the server and not Json
which is let the server figure that out why get a bunch of Json that that you then in the browser have to turn into HTML
and process and transform why not just do that on the server um the server is the one that has the state the server is
the one that knows if the timer is running or not the server is the one that knows whose turn it is so let it drive the
UI and this is what hyper hyper media as the engine of application state or about yeah I mean if you don't if you don't
have much state right to me what do you test drive you test drive decisions you test drive places where there's some
kind of decision saving it I mean yes there's some other stuff in terms of wiring things together but a lot of what we'
re testing is like in this situation did it make the right decision and therefore the state has changed in this way but
if the front end isn't really holding any state you don't need to tdd it like I'm I don't generally do much testing all
alt together for my front ends which means I do run into some problems but obvious logic I prefer decision- making
because things like switch statements um don't look like branches thing yeah I'm I I might go that far um I think they
they have their place but it's such so much smaller than than so much smaller than the current usage that I hope people
will come to their senses um and because HDMX has become popular I think it will help push things sort of back to where
I think they should be which is you know maybe five% of the apps need the the react an angular view level of of kind of
front end and then there's just purely custom front end you know like like a canva where you're doing design stuff or a
figma um you're not going to you're going to need so much more control that that a frame workk or Library isn't you all
right um so let's see um oops we don't need that Imports so one of the things that um that HTM X provides uh is in a
sense making everything clickable right so I was clicking on a button because I think that makes sense in that UI uh but
you could totally have just a div that is clickable I don't know how I feel about that it gets into accessibility issues
um like if you've got a div and clicking on it does something that makes me uncomfortable uh and yes I know you can sort
of put um what I call it areer roles and things like that it just makes me uncomfortable to have um what's basically an
interactive element that fetches updates or or or changes state on a server and have that not be an obvious thing uh so
I'm not sure how it's possible you can basically put an HX get on anything um but if it requires you to click to do it
then I'm not sure about it if it's reloading itself because it's on some timer or something that's different uh but I'm
I'm not not so sure about this but um I'd have to look at some more examples to see what um what folks are are using
sort of non- button non input elements uh that are that are things all right next oh I wanted to try the the multi uh
yes I care a lot about about thanks um let's do the multi-target thing so duplicate this targets uh so we'll create a
new get mapping this guys yeah uh if I'm not doing ensemble work if I'm doing stuff like this uh I'll multistream or if
I'm pair streaming then I'll multistream um but I haven't gotten OBS to there's nothing stopping me I just haven't
plugged in my third Monitor and and done some fiddling around so want targets swap here oh thanks John glad you glad you
uh enjoyed it okay uh so want another Target for equals and let's uh put some class on here hold uh text 2 margin
actually work because we got to swap it ah yes the rewind is true yes uh that YouTube yeah YouTube um the only downside
of one of the biggest downsides of the chat is y'all can't post links period end of story not not gonna happen um
whereas on Twitch I can allow it and and stuff gets held appropriately that did I do the HX get wrong this it's
targeting over here well that does show that the you can Target anything right uh what did I mess up one so one thing I
haven't figured out intellig um there does not appear as far as I can tell to be a more permanent way to in to inject a
language into a string so here I did the inject language as HTML and now it colored stuff um now it understands
semantically or I guess syntactically not semantically it understands the syntax like I can grow pieces and it makes
sense whereas here it's just like I don't know what it's like there's that word and then there's the entire string
because it doesn't know anything about the content um until I go ahead and inject it I have not figured out all although
I haven't looked very hard but I haven't figured out how to turn this on like I want all strings in this file to be
treated as HTML that I I would love that I thought there might be an annotation but I I couldn't find it there might be
it just not didn't find it documented oh the at language even that like I guess that that makes sense um it's just kind
of kind of though I'll have to figure that out because it's really annoying because every time I load this file like I I
didn't uh I closed and reopen the project and those those temporary injections are gone of course it did say it was
temporary um but I asked the AI assistant that it couldn't help me I like if Jeet brains doesn't doesn't have if Jeet
brain's own AI assistant doesn't doesn't know intellig what are they this all right reload the page okay so it replaced
this this text um this one replaces that one uh and notice it replaces the entire element so it's not just the inner
text right it's not just replacing this part it replaces the entire div and we can tell because the color changes in
fact that might be a good way to do that is let's do in swap um let's also do a class uh whoops come Me sure let's do
border green 300 background background yellow text um now the H2 wasn't replaced because we didn't put um the class I'll
I'll uh we'll update it 400 Ah that's what I was looking for I was looking for the statement version of it that's blower
case hey that did it want I assume that doesn't apply to the right that's a a statement thing so it's uh indexes so that
can only target a method it cannot Target a class which I guess makes sense because you wouldn't Target a class you
would only target a method a variable that's too enough all right so uh we reran it let's here so we see that this
background changed color when it was refreshed um and this also changed did it not I actually don't know did and the
reason why is I didn't say addab band swap uh so let's make this um background no appreciate appreciate the link that's
rerun refresh and so we see that this was replaced and this was replaced with a single button click and the single
returns return of HTML um so we proved multiple oob targets uh works unsurprising because that's what it's designed to
do but good example and because we change the classes we we are also showing that it replaces the entire element as a
whole not just the the inner text um what did it add to my pal oh I have the jet brains annotation okay I usually
actually have that in my projects I don't know why I didn't have it in this one all right so I think we're done with
targeting uh so Jonas not only will the repo be public but this is part of what's turning it what I meant I wanted this
to be like a a a quick a quicky article but I can't help myself uh so it's going to become more of a tutorial so um the
the repo will be available before the article is done uh is is what I can assure you uh and then the the tutorial will
use the examples from from the repo and that is the reason I'm creating these examples is we learn so much from examples
uh that it's a shame not to ones and so notice so I always go meta when I do these things notice the sequence of these
examples right I didn't start out with hey let me go and Target multiple IDs with the same with one HTML string from the
server and here's how look how it replaces a whole bunch of different things right that is what I see from most
tutorials is you jump from like here's how you use one thing and then here's how you use five things alt together and I'
m like wait no no back up a bit um and especially uh negative examples like what are the mistakes that people make I
made mistakes what were they how can I document them so that people not only can learn like oh that makes sense that
that's that makes sense why is this not working um so that's what I'm trying right so is there anything else I need
swapping could look into morph swap but I feel like if I keep doing that kind of thing did I use morph swap no uh I
could explore it but if I do that I this thing will never be done um so what about uh I'm GNA say yagy right now for
that all right so we've got the HDMX get we've got the target we've got the out ofand swap uh out of bound swap multiple
targets um so that's all fetching information from the server uh now change Changing post and how that can change the
and so then I can finally get to websockets no I don't think H's delete I think to me I'm again it's like I'm trying to
like uh give just enough especially sort of along the lines of of what I needed to create my because honestly I think
once you understand HX get and HX post HX delete is just another post put patch they're all state changes so initiating
those are all going to be basically similar and eventually it would result in um something uh something on the UI UI
changing um it does bring up you probably want HX delete though to actually remove something um so maybe unlike all the
others where it's sort of changing existing content to something else delete might actually need to remove something
Maybe too okay see now I want to go look at at how I do bed type so once you know how to band swap it's actually
actually is actually pretty straightforward but a delete straightforward all right now now I now now I'm satisfied now I
now I can it's like I just had to know um that's the very it's it's you know some Superman has has his Kryptonite I have
my hm what is great so um so swapping these are all the options um none is not the same thing as delete uh so we could
have some fun um so I think you could do uh button button doesn't have an ID let's give the button an does find it
interesting that uh intell on the right side because it's inside of a Java string uh Auto prefills the a single quot
pair of single quotes uh in the HTML it prefills it with a pair of double quotes even though on the right it's using
text blocks where it could introduce a single quotes uh double quotes that sounds like an issue I might dudan uh oh I
missed the dark mode sorry um one thing that streamyard does not do is forward uh reward requests which is actually
really annoying because uh I have to explicitly switch over to the twitch chat in order to see that so tokes I will
redeem that okay so that should show up better I'll do that after I finish this here oh I put it in the wrong place so
if I say HX swap none does that get overridden by see does button's gone um yeah do I have my dark mode plugin oh no I
don't have my dark mode plugin oh dark read is inactive replaced wonder if it still works I go oh it was saying disabled
because I disabled it that was confusing okay uh let's pin dark reader it's interesting that it didn't work on its own
page I love when when shortcut keys like get captured by different things so here uh what was it there's a shortcut to
add the current site but that's also this keystroke so um let's do it only for 880 there we go okay perfect okay I have
to turn it off off and on again because uh it's also filtering the rest of my monitors all the rest of my browser
windows but it's just making them like grayscale like you saw um Tukes you you uh you request you you redeemed uh 20
minutes to dark mode so that and someone remind me in 20 minutes to turn that off because I don't have my countdown 20
minutes counting down all intellig there we go minutes all right um so that worked that was fun uh but let me take that
out so it looks like um so this is also interesting uh the HX swap oob overrides which to me would make sense that the
server can totally override um what the client says right because I I I really like this mentality of of the server's
first class darn it I know more than you do so if I say delete you delete I don't care what you say right now um so I'm
very much in favor of that but that's because I'm a backend developer power to the back end uh so we'll go ahead and and
um that yeah you won't you will only find dark mode on solo streams not on pair streams um so let's go here does it work
regardless of the element work I guess it does and so we can see we can go to inspect uh I guess it doesn't do a dark
mode for for the inspection sorry about that um so let's look at the network uh let's reload the that so we see the
fetch yeah I know I could but I'm I um so the response right was the P but it actually replaced so it doesn't matter the
element type it only matters matters the ID totally makes sense um so tkes depends on what you mean by easy to test so I
I think one of the strengths of any sort of server driven right server generated HTML server driven flow um is that it's
going to be so much easier to test overall um because the front end is just sending a get request and whatever it gets
back it just puts it in the page it really has no control over it because you don't want that control and so um not sure
how much you were you were watching me create the timer and test driving that into the server um but it meant that I
could test test drive the server because the server had all the state and then once that worked when I basically plugged
in the worked all right so we can stop that and we can go ahead and revert that um so let's use the example then uh of
an server and let's say it has to go through uh so we won't need the targeting page anymore um this will I'll just copy
this page we'll call it um do that and so let's see so what do we want to happen um I think the simplest example is just
toggling going to be an HX post and I'm going to um I could use a example change the state on the server which causes
the Buton to change we won't need another div because we're anything and so this will do active right uh let's go ahead
and create another um controller so one thing to notice is I'm using this at rest controller because what I want is
whatever response I return to be treated as exactly what gets returned um if I use just a regular controller which you
might think you'd want to use in this case uh that Returns the name of a view that then goes through a view processor
like time Leaf but here whatever HTML we run a return new oops a new file new Java post it generate I think this is
terrible I don't think it should make it that easy to create a set of dependency um let's do Post mapping and we want
post tole active um so I um let see that nope server that sounds like an old old code base if you got XML in there and
I'm sorry to hear about your Setter dependencies all right so if we activate it does a post causes uh the server to
execute this method it return deactivate which button um straightforward of course Now doesn't appear to do anything so
we'd like is is for this to uh actually respond and actually change some external internal State one oh gosh yeah spring
framework 3 yeah one hopefully you're slowly transitioning them uh that's not what I want that is um oh right yes of
course Spring spring framework 3 was not spring boot yet or probably wasn't anybody remembers spring R uh okay so this
one is constant this active so here what we'll do is that uh and let's turn this into that one all right let's r that
yeah spring 2.7 is not not too shabby I have I think I still have an application on 1.5 it's not an important right so
that just turns a constant this forth yeah this is pressure especially if you can uh it's not the best pressure to to
use but is one that often ends up working is uh we're out of LTS on on our stuff and we won't updates it sucks if that's
the only nothing um so let's do one more post that sort of Cycles through a thing I I don't know how complex I want to
get about this but you can imagine there's around oh dark Mode's over uh there's all sorts of things around um since you
have control over returning a completely new button not just changing the text you could basically disable a button uh
you do get it to some other interesting issues around like where are where are you holding the templates for these
buttons I'm I'm doing all the generation quote generation of HTML with just mainly hard-coded strings but uh this is
probably where you you want to look at at using Elya templates and so that will not be in my first article because
there's already resources out well oh that's good so you didn't have to just rely on uh uh you didn't have to just rely
on on oh we're out of LTS that's really good one of the nice things is is when when a a team and an organization
prioritize staying up todate then it just gets easier that initial push to get up to date the first time is really of
course not easy um but then once you're there and you continue to stay up to date uh everything else is so much um Okay
so we've got the toggle we'll do one more toggle to go through three states and then I think um so we'll basically have
a one that basically just pushes us to the next state it'll be sort of like a mini State machine um go ahead and create
field um mapping iterator is an interesting choice but no enom here I create an in enm we'll start out interstate I don'
t think I can do this all right Jonas have a good out that see why would I want get current state state knew I wanted
that because I wrote here this so waiting to running like oh it's fine okay what doesn't like um create a uh I think
called button field and we'll create that as a Constructor parameter and then we'll create that here and so one of the
issues is what happens when the page first loads is we'd like it to reflect the current state um and I'm turning off
dark mode because eyes so what I'd like to know um polling triggers load pulling that thanks veiz gotta use enums not
gonna use a Boolean could use a pair of booleans but it didn't make sense for that um trigger yeah I kind of want the
trigger load oh static yeah static PRI final would not uh would not be as nice uh I guess I could try load see what
happens all right I'll leave that for another example um so what does the state start out with mode request let's make
sure this works then I I'm gonna put I'm gonna I can't resist I'm G to put in a get mapping uh for next state which
tells us is um but let's try it without it so let's run um that the one I wanted did I not implement the oh I did oh
whoops so I actually did not this is the Toggler and so then I want another one happen uh and so this one is Toggler
this is going to be post uh this is just be page so togg us through all those States um but we would like oh so here's I
think I can do an out of band swap with just inner HTML right let's return uh so we want it to be I don't think the
element matters well let's see what happens so let's put a p in here with an ID equals three-way HX uh then the HX swap
having a language injector is really nice because you get all the all all the auto completes from HTML so I think that's
that's worth it uh so want the H to be I think inner stuff so enter HTML is the default but hey coros yeah language
injection is so awesome um I need to turn off dark mode folks uh so I don't know if this is going to out oops oh would
help if I actually did um we're going to do a get to now look so we call to get State we got this and it looks like it
replaced the entire inner HTML of this div um least we know the load works but the oh uh right we need to do an HX swap
none so we don't get the leftovers okay loaded again I'm going to put this one surround this by parenthesis just so I
can see it in the interesting so now returned so what actually happens interesting so we do a trigger load of state
which caused the element to come in targeted here uh but future post are not see this yeah so this one got initiated I
think by the load uh let's let's re page so one nice thing is click to end is whatever the current state of the server I
haven't restarted the server so it's retaining the state so this is getting whatever the current state is and this next
state was initiated we can sort of see the long call chain um was initiated by the the load of this div and we can tell
because it's also in that when we click though the response is click to reset but it's not putting in content I wonder
if this HX swap is one but this HX swap o should be overriding oh but this is only for the for the get by default it
might be doing um because the content is not currently out of band I feel like I don't know how I feel about this um on
the one hand this can be confusing on the other hand it would be would it be better to always do an outof band response
other always specify the idea of the thing you're returning but let's HTML it is all uppercase I wonder how matters so
let's go ahead and restart the server curious how much that matters so did not having the right case here throw off so
click to run yeah so we see it it it calling that and getting the state changes but it's not populating it so now let's
do working attribute feels like it changes tree yeah that's not a note I feel like I need a stronger inherited all right
um to me that that warrants a warning I don't know maybe it's natural to some people like oh of course it's inherited
that avatar uh okay good to know that because I set the HX swap up here this HX swap none now applies to everything
which means it stopped working for the button uh which means I needed to change it back um this feels really prone to
note not a warning not look out this will confuse you if you don't um yeah all right so we can take out the where is it
this thing and so now what's nice about this is uh page refresh the initial load and Page refreshes the button will have
the correct State because it's getting the correct state from the server um but also I don't have to mess with like if
this stuff on the left here were in in some template I wouldn't have to uh I could put the template could go retrieve it
rather than the template also having to figure out what to put for the button here you do get a little bit of a flash um
and that might be the default settle delay I I didn't I haven't looked much into settle settle the swap is how long it
will wait received now wait that's Swap this will wait one second before doing the swap after it's received uh so the
settle is it will take it will it no that's not right that's the swap setting I don't know what settle helpful I can
understand wanting to wait for after you get the content in before you swap it in because maybe there's some usually be
usually because of some animations that you want to take effect um I don't know what settle means and me it's like when
you look up in the dictionary for some word that ends in Ed like settled and it says past tense of settle okay you could
have just told me what settle was without me having to now go look up what settle is but this means okay so this should
this this detail should be more clear this is delays so this is explaining why which is um CSS transitions so you only
care about swap delay and settle delay if you care about CSS transitions because the way the transitions in CSS work is
usually you define it like fade in or swoop it or or other kinds of changes or or morphing or scaling in all those kinds
of things um usually they have Transitions and they have uh transition delays it's like this one um so what it does is
the swap is new content but with the old attribute values then any attribute values that have changed those are then
settled in so swap delay so swap content right so delay for whatever the swap delay swap content except for attributes
sense hey there RAV uh is there a way how to authorize websockets yes so you can do websocket authentication in the same
way that you do or similar to how you would do MVC endpoint authentication and authorization um because uh it it all
sort of goes through the same the same stuff um that's something I'll be looking into probably not this stream uh but a
but a future stream because I need to figure that out as well um so you don't uh you don't have to do session ID or
anything like that because when you connect so this will be the the second part of this article which will look into the
spring boot stuff so if um here when you implement where basically by extending the text web socket Handler which is
what I'm doing uh you got a um connection established and you get a session object and then you you don't actually need
to hold on to that but if you want to sort of associate that with somebody you can hold on to it and then uh you can
then when you get a notification you can then broadcast to specific sessions and you can match up sessions with with
specific people um so a lot of that is sort of handled uh sort of tracking sessions now obviously somebody could
disconnect and reconnect as a new session um but there's some stuff around how how you could do that uh that I'll that
I'll get to but um a lot of it's I think not 100% sure because I haven't fully implemented it but my my understanding is
is a lot of that will be handled by all of the filters that are provided by by Spring Security yeah so it's basically
like I want my CSS transitions to work without yeah so I'm not 100% sure about some of this um but uh some of the
because I I have I haven't done direct websocket stuff in the past usually I've gone through um basically making it look
like a message cu which is using the Springs uh websocket stomp Handler stuff um but I believe it goes through some of
the some of the similar stuff because for example things like csrf uh because it comes in through a post uh those um
those have some of the same restrictions uh maybe that's not websocket that's HDMX I I I have to look but I believe
there is there is there is support for easier but you'll have to stay tuned or if if you want me to answer that because
I don't I haven't quite gotten uh to that part with this kind of websocket but from what I read I believe us but I will
that uh okay change did it actually change anything or is it just here I'm not I'm not seeing Oh the differences are
ignored okay so that's probably just uh some white space yeah some white okay okay so that was just white space changed
we'll do yeah probably not this stream but if if uh certainly the next stream on this next going so I'm not going to be
able to go much longer off um where is it is where is oh smart Keys here we go uh refor that's fine that's fine that's
fine that that's table stuff um no and no I think that's what's annoying me is the way it's Auto handling the lists yeah
because I do my lists differently than than it does um know you might have missed the rants that I had earlier um but I
think it can replace a lot of usage of react angular view um probably wouldn't do it partially although you might have
parts of re application where this page needs to be all the stuff uh single page you know stuff gives you but only this
page everything else can be regular T typical regular HTML Pages maybe with a bit of HTM X for Interactive all right
good night russl um I think that's it for me today uh so next time I think we're done with sort of we've got the HX get
uh we've got this targeting we've got the swapping We Now understand also that uh HX swap is inherited um so I think we'
ve got good stuff there in terms of using just the HDMX with basic posts and gets and deletes um so now the next step is
okay how do we take that knowledge and combine it with with the the text websocket Handler uh extension file uh and then
um adding um I'm using a simple text websocket Handler I already got the code for that I just need to clean it up um uh
I think this would be good here I don't know if that's B but uh there is also um and there's something around
associating uh connections with users I'm not sure I want to I I feel like uh I think I'm going to split this article up
and there'll be sort of multiple parts to the websocket so I think sort of here is is where I'm going to draw the line
for one of the Articles and probably even maybe even here for for one of them um this one is very much related also to
to to this one all right that's all folks so thanks for hanging out thanks for keeping me company thanks for your uh
wonderful questions and comments I really do appreciate it um my schedule for tomorrow is undetermined I will be
streaming I don't know when um mainly because it depends on the weather and when I can get my run runtime in uh and then
on Thursday uh two Thursday morning uh we've got back P we're back uh with Mike Rizzy pairing on the song themes
application making good progress uh so that is at 9:00 am Pacific time 5:00 pm UTC and uh if you're not already a member
of the Discord why not join doesn't cost you anything um one of the things that it gives you is if nothing else um a
place to ask questions about the stream and even if you don't care about that it also gives you a way to find out uh
about when the next stream is I don't always post them on on social media but I but I always uh post it on on the
Discord so you can get a little bit more notice perhaps just 10 minutes like today uh but a little bit more notice than
you might get just by following on on on Twitch or YouTube so I appreciate if you uh you're welcome to join the Discord
and uh follows and subscriptions on the appropriate platform are always appreciated uh and That's all folks I will see
you next time have a great rest day
