# ＂Song Themes＂ Episode 6： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=a2XAcMGcsVI

---

## Transcript

all right hello folks welcome to episode six uh where we're working on yeah yeah already got I don't know 12 15 hours of
coding wow cool and it's on the one hand it's it's like you know we're making progress on the other hand I always look
at how long it actually takes and yes we get sidetracked which is totally fine we get sidetracked by stuff on the stream
um and conversation and please don't hesitate to to say hi and ask questions that's why you know we're doing this live
and not just pairing off on our own um but it always strikes me as like just how long stuff takes um it it takes time
hey F welcome nice to see you again it just takes a long time it just just JW so uh last time we we pushed to production
we did that was that was exciting um not not a whole lot of functionality but it's all test driven um so with security
by obscurity yes kind uh so where are we at should I put your screen up sure actually let's throw up should we do do you
think it's still worth giving the high level I think if if people don't know where we're at um they can go watch episode
one okay cool we we can we built they'll get it from from looking at what we're doing yeah okay so yeah sure sure throw
share my screen and I'll right I got jir brought up J of course that's the first thing you do in the morning there first
first I think you were beaten by uh FF who's on YouTube you're the first twitch ah you still get a badge or a star from
that don't you not from a twitch perspective you show up you show up on the video there you go that's that's your that's
your reward so um but yeah we finished two high level at least two highle stories yep and I think we were were we left
off talking about um what to do next I kind of after we stopped streaming actually this morning I kind of wrote up we
wrote two we just wrote I think persistence and AD via UI right and I was thinking about it and I was like well we could
add a repository first where it's not going to a database then persist to a database right um that's sort of the the
right hand side of the hexagon or on the left- hand side we could we originally talked about adding songs via the UI
which could be simple it could be even simplified to adding a single song right um and then there's also the sorry so I
was gonna say like whereas inside the code adding one or many there's not really any difference uh from the UI there
could be a substantial difference right yeah and that's why yeah I I just wanted to mention that there you know that it
is you know not always necessarily do you know zero one many um well at least one and many but I think in this case it
it'll actually be useful and then I realize I mean I'm not going to want to be typing songs one at a time wna I mean for
me I was thinking we should probably do the the right hand side of the hexagon first and then tackle UI that's kind of
what I was thinking but I don't know what what your thoughts were yeah so um so F no asks about you know have I already
explained hexagonal architecture and at least on this stream this this series of of episodes I have not uh so this might
actually be a good time to just give a very highlevel uh thing because it it will inform what what we do next uh so let
me go ahead and borrow screen yes borrow the screen uh see if this works um me pull this pardon me while I move stuff
around on screens so you're over there and you're over here and and there we go okay so this is my I don't know three
minute explanation of of hexagonal architecture uh so we start out with with the hexagon um and again and I think I
explained this on on my stream yesterday uh but alra Coburn who uh invented hexal AR architecture at least wrote about
it uh was also called ports and adapters um he does not differentiate between application and domain and and whatever so
he's basically saying that anything inside the hexagon is application and you do whatever you want um the way I apply
hexagonal architecture is uh very much informed by domain driven design so there are two internal layers so the
innermost layer uh and it's structured this way because this layer has no uh no awareness of IO it has no awareness of
the outside world it's like living in this platonic ideal of just sitting in Ram executing code no awareness of where
data came from no awareness of where the objects themselves came from this is where we Implement all of the business
rules processes validation constraints and variants whatever you want to call them uh that that's where this is and and
everything in here is using the ubiquitous language um all the good stuff from domain driven design then we have sort of
surrounding it uh sometimes I feel like it's it's it's like codling it and protecting it from the outside world is the
the application layer sometimes called the use case layer um both are are great uh and this is the thing that while it's
aware of IO has no concrete sort of implementations of IO it doesn't have uh awareness of specific database it knows how
to talk to some database through an interface uh but it doesn't have anything specific it can talk to an external
service but doesn't have anything specific and so it knows how to talk to persistence and send out maybe notifications
to the outside world but has no idea of how that works and is still not touching Hardware so there's still no IO and so
this is the hexagon this is the application or use case boundary and what that means is when we plug in things like the
UI um they basically talk to to talk to the application layer and if we had other ways of communicating those would be
plugged in as well uh and those are the adapters and their job is to translate and transform things from from our
perspective and where we're at um is kind of here uh we've been writing tests um against multiple layers against the
adapter as well um but if we want to sort of push forward from here we're going to have to involve the application layer
and so the application layers is uh also sometimes the coordination layer so it's coordinating hey if I want to execute
some command on a domain object like add a user to uh an event they're attending or add a song to a song database where
does that where do those objects come from well they have to come from somewhere and somewhere outside the the you know
the the process run space um it's likely persistence um but generally we're going to drive that through tests uh and so
we're going to drive that through through these these unit tests uh and it's generally uh the way I think about and this
is why I like hexagonal over other diagramming forms like clean is is there's a asymmetrical left to right direction of
how you think about data flow uh which also then affects tests and so we want to write these tests sort of from left to
right um and then persistence uh we don't need the actual real persistence we can have uh an in-memory like you
mentioned we can have an in-memory fake repository that that um fills the role of persistence but where we don't have to
worry about having an actual database up front so so um and we can implement the real persistence and other stuff we
need uh there's some other stuff but I think that's basically the the main thing I wanted to to talk about was just sort
of the layers inside the hexagon and and sort of how that informs our our tests question Ted did you mention that um the
dependencies all go inward uh I didn't explicitly um but that is that is the case uh and the dependencies can get a
little complicated because there dependencies there are different kinds of dependencies um but in general the idea is
that dependencies flow inward uh all the way into the and and the domain is and so each layer from inside out has no
awareness of that outer layer and that's that's really important um and so that sort of reaffirms the idea that domain
has no idea of anything else um application layer has has awareness uh and and has direct dependencies and calls
basically calls methods on the domain uh but not the other way around um and there's some stuff about inversion of
dependencies but I don't I don't want to go go too deep into that uh just yet until we see sort of some that I think
there was a followup question from yeah so um so can we use API first uh hexagonal architecture the same time I'm not
sure what you mean by API first uh so you'll have to clarify that um but the idea is that um here in the diagram I show
it as user interface but there's also external message bus all these could be apis they could be server side rendered
HTML like we're doing in in uh the song themes application um or they could be an a restful API or they could be an RPC
API uh it's totally up to you what you need um the important thing is that the application layer and the domain layer do
not change um they are there to provide the implementation for what is what problem you're trying to solve you're you're
trying to solve some domain problem likely some business problem um and all that is inside of of your domain supported
by the application layer to sort of manage integration with things uh but generally so this is sort of the structure but
you do want to do outside in and maybe that's what you meant by API first which is you still need to start with like
what does the UI look like what is the flow of operations what do users see and then what what are they able to do and
then what do they see as a result uh and there various techniques like event modeling and some other uh and story
mapping and things like that that allow you to to sort of organize that um and whether it's an API or a UI the the the
idea there is is the same um okay yeah I did a quick Google search I found something about API first if you um yeah well
I I want to know what what what Fela meant by API first rather than arbitrary term because right right right the problem
with some of these like um I had a question asked yesterday about domain services like I know what I mean by domain
services and I know what Eric Evans meant by domain services but what other people mean by domain Services is actually
something completely the opposite um so uh yeah uh so in terms of the package structure um we all we actually started uh
organizing our stuff according to hexagonal architecture um and so I generally structure things uh according to adapters
um and then application and domain so those are sort of my three top level things and you can actually see that uh and
I'll share also the project uh see that here in my Embler tool level this and so we can basically see so we've got
adapter and then there's um in and outbound adapters so the in is is what is what is triggering things to happen um and
I've got those subdivided into uh admin facing functionality and member facing functionality um and then I've got
various out which is basically things that I need to talk to in order to get things done so email jdbc um Zoom all all
sorts of things uh then I have application and I consider most people don't organize it this way at least from what I've
seen But I consider ports as part of the application layer because the application layer talks to to Ports to get things
done um and ports are the abstraction for our outbound adapters and then there's domain which is all of magic stuff and
uh if your domain is large enough you'll probably split the domain along uh functional lines you may even split your
application into a multim module in which case you'll see uh application and domain um sort of underneath another layer
but uh one of the things you'll also notice perhaps is the coloring that's used for the uh the background uh of these
different packages uh those align with with how I color my diagrams so yellow for domain sort of a peach orange for
application um blue for inbound and and sort of purple lavender for for outbound did you set that up yourself I did and
I actually have a video that walks through how to do that so you can check it out on YouTube I'll find a link for that
in a bit cool um yeah so that was that was the quick run through of and and we'll see we'll see as as the song thing
application grows we'll we'll start to see it filling out and flushing out um especially the application layer which is
which is probably what we'll deal with next okay all right yeah glad glad I helped and if you haven't watched I have a
whole video uh on on this where where I go through in a little bit more detail hexagonal architecture and again that's
on on my YouTube channel um and I'll find the link for that uh as well uh so AA says in my experience the client will
cause application layer interface to change so I feel we shouldn't build too much application layer too soon yes yes and
this is again sort of the outside in developments right you got you hopefully start with what does the client need and
therefore what do I need from the API what does the API need to support and then then you can say okay well what is the
API then need from the application layer is it something that's already there that we just need to hook up um or are we
developing something new where we now need to add new functionality to to the application layer um and I often uh um we'
ll even Implement some code that eventually will end up in the application layer I'll Implement that in the uh the
adapter temporarily um and use the refactor opportunities to to place um yes package structure is hard hard because you'
re trying to to so there's um uh a problem in that you have a choice do you use the package structure fully to say this
is what the project is about and and leave technical concerns aside um which is a completely valid way of doing it uh I
tend a little bit towards pulling in technical because want the package at least in Java I want packaging to save me
from accidentally doing things like having the application layer invoke something on an adapter so there is this tension
where the packaging mechanics of of a language like Java are just not sufficient to get us both and so I made the
decision of yes it means that my my top level things are adapter uh an application and domain but I get the benefit of
being able to use a tool like AR unit to enforce domain should not talk to application in terms of invoking and
application should not invoke a method on on adapter and adapter shouldn't invoke methods on other adapters um so it's
it so it it's it's hard to to get the best of both worlds uh so you have to sort of lean one way or the other um sort of
vertical slice architecture says just organize everything around the feature and then within that do that and in a sense
that's what I do if I had more features you'd probably see sort of duplicate um sort of trees there but uh package
structure is tldr so um so if we look at what we're what uh what we want to do here um we don't want to just add a
repository for no reason right we have to have something that drives it so we're we're uh we're gonna say well what do
we want to do right we W to a not have to type this stuff in every time the application starts up clearly uh so do we
want so in a sense what functionality do we want that will lead us down the road of eventually at least coming up with
an in-memory version of a repository and that's probably the UI to add uh a song I I would think oh I see that's why
you're heading towards yeah so because because again from the outside in we may not create the UI but we want to figure
out what is the UI what information is it going to send uh because then that we can say okay and this is where uh
sometimes we we use the term middle out um or I think you you use subcutaneous which is basically the same thing it's
like let's start one one layer below the UI because the UI is kind of messy and and we actually don't need that in order
to implement the rest but we do need to figure out what is what is the thing support almost is like question oh sorry go
ahead go ahead oh I say um so it's more along the line of song just below the UI or something like that yeah so this is
applicate this is basically use case what is the use case for adding a song um right and it's really interesting to see
sort of use cases come back a bit in in popularity I think that's one of those uh became really popular but then it
became too overly formal and and long and and and people didn't didn't like it and so reacted to that by basically just
tossing it overboard and getting rid of it and not using it at all uh but I think there's with domain drone design and
and some of the architectures have sort of brought back this idea of a use case um and Al alist Cobrin talks a lot about
that because he wrote books on the topic and what's in this context what's your definition of use case that we're
looking at uh it's pretty much um I want to add a song that doesn't exist to the database pretty much and then there's
like what are the different conditions what are the different uh failure cases that we need to handle um so to me the
hands each one of those is a scenario of of the use case but the use case is how do we add a song and what are the
contents of that uh and what do we um yeah pretty much that so then that would have like sort of sub right and here
because what we're what we're asking the application to do is not terribly complex there aren't a lot of rules and
processes around this um it'll be relatively straightforward um but we do have to figure out well what information are
we collecting so that's where we're we'll have to start defining what is a song right um and how are we adding themes so
right now we might just say okay just type those as free form text but we probably I don't know do we want to constrain
those are you picking from a list of existing themes yeah the idea is I had meant to find the only example I have is is
a of a UI example is a bit um it's proprietary so I can't show you or you know gives away people's names but I I've seen
one where it's along the lines of it's kind of like tag it is like a tag um and as you type it Narrows down out of the
existing themes which ones and you could select you know one or more and then each one would sort of be um I'll um and
this right and then you could have an so that would be like one theme so as your typing the word new and there's if
there's only one thinge that starts with new it would flesh it out to new years's and then the little X is an indication
of no no no I changed my mind delete that right from the fine right there' be a second one right so what you defined is
is the UI um the UI interaction what I'm interested in is the constraints around where do these tags come from from so
yes there's autocomplete and things like that can I can I type an arbitrary thing like uh Black Friday right no okay so
that's um because it's gonna have to come from a fixed set of data okay so that uh is new to me ah we haven't discussed
that we haven't discussed where themes come from um in which case we're missing a whole set of stories around where do
these theme tags come from and who edits them and who's allowed to edit them interesting I I assumed that it comes out
of the ad and the ad you can assign themes and if it doesn't exist it adds the theme that's why there's the whole
concept of um wait uh let me go back to let me grab you just contradicted yourself or at least the way I understood it
because a minute ago you said you have to pick from an existing theme you could not add one on the Fly and but now you'
re saying that that you're adding them oh it depends on the role so the administrator can that's why I was trying to get
the miror board up give me a sec I can get it up no worries I got it all right got um so if you remember so the the the
maybe not well clearly not clear because you didn't get it um where yeah administrator adds a single song and its theme
right but you know how we have a visitor or what is the term we use no member member contributor contributor submits a
song adds a single song in its theme yeah so nowhere did you mention anything about because we never got into it into
that level of detail uh where I was gonna I wasn't actually done sorry when contributor adds a song it can be any theme
but because the theme doesn't automatically go in until admin approves it so say the example you gave last week say um I
decided to use the word Christmas to indicate all Christmas related songs and somebody added a song with a theme xmus
right a member I could either say I reject because I don't want to have Christmas and in the theme list um interesting
thought which I hadn't thought through is could I just change it or do I reject it and say please resubmit right with
Christmas that whole workflow I hadn't really thought about um so that was my that not that part but the part about the
approval process is what is the gatekeeper if you will of which themes get added the administrator can add whoever
administrator being me so un uh so under what circumstance because when you were when you were talking about adding uh
adding the theme and picking from an existing theme you I said can you you know put in an arbitrary theme and you said
no but now you're saying yes well so as an admin ad it's yes to contributor it's it's so to admin it's yes to remember
it's maybe depending on whether the contributor or or Vis contributor sorry okay um and then visitor can only pick from
well visitor can't add so so that's that's non non issue so so I guess the answer to your question is it depends their
role uh so for admins can they can you arbitrarily add a theme as you add a song I would expect so yes okay so that
that's different from how I interpret it when you first explained it so okay when they're typing it in and it auto and
and there's nothing to autocomplete it should still allow them because they're the admin to type whatever they want
exactly from a curation standpoint that's not necessarily a great idea um because it can lead even if it was just one
you know one or two admins it can really lead to a proliferation of uh of themes but it certainly does make it easier
because then we don't have to restrict which themes are available um but it does make the UI a little bit more difficult
uh but anyway we don't care about what the UI looks like what we care about is uh whether for example we expect the
theme to be something that uh already exists in in the database or uh you would have to go through you know so we don't
have to go through some separate process to add add a theme that it's done part of adding the song is that correct yeah
that was the original Vision okay now of course you know my vision could have been hallucination so well and you know
and this is this is part of the iterative process this is part of the process right this is where we say h maybe I do
want that or maybe I don't want that uh and what was in your head wasn't wasn't what was in my head wasn't matching what
you wanted right um and as we get into more detail that becomes more clear and hopefully we're on the same page which is
why you want the product owner in the same room yes exactly I wouldn't want to have to wait a week to have that
conversation yeah uh so oh brings up some user has to be a trusted user so yeah so uh do you want to Mouse over to where
we've defined the different users in the Barrow oh yes make this full screen too actors that zoomed enough uh maybe zoom
in a bit more on actors yeah so so admin is is we're assuming that right now the functionalities is that we're building
is only for the admin so they uh are known to the site and they have rights to do anything because they're the admin um
the other role that that uh we were talking about was contributor which um is also known to the site uh and has the
abilities to submit proposals for songs to be added uh Andor corrections to existing songs you bring up an interesting
point now what's what's interesting for contributors is uh you could and I don't want to maybe don't want to go too deep
on that right now but you could have them only select from existing themes and not add new themes um or uh or you could
have some process where you where you basically say uh no use this other theme or just take it and you literally change
the theme and then and then submit it and the contributor has to live with your choice right and there is an interesting
that is an interesting idea where the contributor could just contribute a theme again it's a little bit around the
corner it's not necessar right away kind of yeah they could contribute a theme and that could be approved or disapproved
right even if there is no songs yet exactly like it's enough to go oh I know what you mean yeah right and that that
starts getting into how are themes managed because there's because having uh so earlier in my career I I worked on tools
where you basically do literally this um when I was at eBay I worked on what was called the attribute management system
which is all about uh so imagine eBay the auction site in the early 2000s and you wanted to find a digital camera
because that's what the that's what you bought pre iPhones and pre pre smartphones you bought digital cameras um imagine
you wanted to find a digital camera that had uh 4 megapixels of resolution and had this much memory and so on um how
would you search for that well you'd have to assume that everybody typed in the right keywords and used four megapixel
as opposed to 4 MP or four megix or something like that um and so in order to fix that problem they wanted to assign
attributes to categories and and and things like that and that was a managed application uh and I led the development of
building that and building basically what's a taxonomy is is uh very important that it be curated um and you do things
like say oh we're seeing a lot of 20 megapixel cameras we don't have a category for that so we need to create one oh
we're seeing these do we want to group these together at 16 to 20 megapixels so let's take all those and and and
basically crunch them down into into one um so there's there's a lot of management of like if we see Christmas and Xmas
are those the same things we still maybe want do we is there is there a difference if there's no difference then we
should not then we should basically just replace all exmouth with Christmas and get rid of that that theme um because at
some point it doesn't stay there's no way to have it in your head anymore and now you're seeing like oh actually these
two things are the same or or these two things that are actually different uh and this is funny how it it's very much
similar to the idea of otus language I had a thought that popped up that I wanted to write down before I forget yeah um
is we hadn't really talked about um I'm just gonna I'm gonna write it as I think it uh draft early releases just to give
you an idea of where my vision was where my head was at was version one would enter friend right um I'm these are just I
mean I'm really the the first two is what I was thinking about right was at first it would be just the stuff i' put in
let's in other words that's when I feel like hey if I've got a fair amount of data which I do now it's useful to the
world now it goes from being a URL that says coming soon to hear something right and then now had hey do you want to
contribute right and then maybe V3 would be the concept of a member right and I haven't really thought Beyond this I
literally only came up with this like five minutes ago yeah um that something I want to move into jira uh to uh you know
we can keep poking away yeah yeah um so full enough to ask uh when you handle roll when would you handle rolls before or
after finishing ad song feature yeah so so what's interesting is is like roles are domain um but there's also a very
technical aspect to it um and when we add it I would probably say is is when we need it um so like in the V1 plan
clearly we're going to need a way to recognize admin uh versus Anonymous visitor so in order to do that that's when we
would we would uh introduce introduce at least one role and then we would introduce the contributor role when there's a
need for that and so we' introduce whatever is necessary around that as as we need it um but there there's sort of a
balance between introducing it too early where it kind of gets in our way like right now I would see no point in
introducing any kind of security stuff until we have an actual database that we have to start protecting its data um
because once that's in production you want to make sure that that nobody's you lots of good questions coming in yeah uh
searching could be interesting um so we will never have enough data where uh we have to implement anything like at the
low level of of B trees that's my prediction um because if we do we will not be writing database um so I mention that
because from from one point of view if we just kind of hey I want to learn about be trees then great that would be a
useful thing to do but um we are not uh at least I'm not interested in that I'm more interested in the functionality um
and and I want to point out that this is what gets developers especially um well this is what get develop gets
developers into trouble is focusing on the technical complexity like oh be trees are cool I just learned about them
let's go Implement them in our production code now I'm not saying that that to added you suggesting that but I've seen
this over and time and time again and we see the same thing with microservices we see the same thing with other
Technologies and um I'm very much a boring technology kind of guy I want boring uh if I'm learning that's different but
if I'm implementing stuff as a product or as some kind of application I want boring I want to use a database uh I want
to use a SQL or whatever database maybe it's a document database or maybe it's uh search-based kind of thing um I want
to be very careful about not Reinventing things because that's not my purpose so um be careful that when you read about
shiny interesting techniqu Technologies you don't start go using them in in all over the place where necessary so yeah
exactly that you know and but we do have this question of because we right now we're doing the search in memory when do
we say actually let's let the database do that um and that decision will likely be coming up soon yeah if admins mess up
the the the theme taxonomy that's that's on them I.E yeah that's Mike's fault and I think yeah because it want me to
just be me and it'll be interesting to see if there ever will be an admin probably it depends on how popular yeah the
site gets I can't imagine it gets that popular so it'll probably just be me um but if it's two people then yeah they
need to huddle now and again and go what do you think of this one that's where you get into the human aspect of it I
think I think uh and this is where you know uh I'm not there's a lot of things I'm not a fan of of machine learning and
llms um but this one is actually a perfect use for for it where it can perhaps provide hey I'm seeing these themes they
seem to be similar do you want to combine them um hey here these this theme seems to be actually something we could
subdivide into two do you want to do that and so there's a lot of stuff there where um especially llms and things like
that can can can help and I always look at it as um don't do it for me uh but help guide me um uh and and I'll do the
actual thing yeah it's possible there might be some scoring uh for example if you got a bunch of songs and you're or if
you got uh a bunch of themes that you're searching on do you show on and we've talked about this before once we get into
multi- theme search I'm sure this will come up up um do you only show the songs that match all the themes you entered or
do you rank them in some way algorithm uh if you're going to have an admin role you must have authentication you can't
really there's no other way to do it uh unless you do security by oburity um which is not really a great yeah great
question yeah uh yeah so we have we we'll have different roles um and yes uh whenever shiny technology comes everything
looks like oh we can solve it with with that we can solve it with Bloom filters like that uh and yeah maybe somebody's
already said this is how we solve this particular are I mean come on like there's still interviews where they're asking
you leak code questions and things like that that have absolutely that are in fact a way to get people who can't solve
the problems that you have because they're solving problems that are not the problems you have talk about the problems
you have and then you'll hire people who can help solve those problems um I I to this I mean I remember when I when I
interviewed for Google what did I do I S you know studied all the Sorting algorithms and all sorts of stuff and that's
exactly what I was asked about is that stuff I did absolutely not had nothing to do with anything I was interviewed on
zero there was Zero overlap between the hours of interviews and the thing I actually got to work on um and that was true
for for many companies uh unfortunately it's still true today reminds me of one one interview I had toed um and it was a
standard interview right everybody you know technical question technical question and then the last guy was supposedly
the the not supposedly was the guru for the small company and uh you know he kind of was kind of a hard ass you know
asked hard things and was kind of you know rough um and he's like yeah I got this one thing you know I'm trying to you
know trying to fix this and it does I can't figure this out and I'm like looking at the screen and I'm like I felt like
I was doing a Fineman moment and I'm likew have you thought about that and pointed at the screen he's like that's it so
got that job yes he went from being Gruff to like a super nice guy and was a nice guy forever afterwards right yeah
that's awesome yeah it was pretty funny I think that was an intentional interview to no right that was a accidental yeah
um y yeah the some of the better interviews I've had is is hey come and pair program on this code that I'm working on
yep um and that's how I ended up having although I don't think it's there anymore some code in in Cloud Foundry um
because I was pairing with somebody at pivotal labs and we were working in go a language I had never worked in before so
it was that was interesting um sure Pinky Promise counts Wire yeah say like I if I remember I I had a phone screen and
they were asking me the question of if you have quarters and a balance and whatever it was and I'm like I'm I basically
said I'm not answering that question what does this have to do with the job and and that interview did not really go
anywhere unsurprisingly but I was like I'm sorry I'm not like you know I'm a sen I'm you know I'm a I'm a senior staff
level engineer I'm not answering this question even though I didn't call it a question I basically said I'm not
answering this question what does this have to do with the job uh there there's an assumption that there is this idea of
General problem solving ability and I think that's the underlying thing for for all these I know we're on a tangent we
we'll bring it back um and that is simply not true and it's it's just a lack of understanding of of how people solve
problems and uh how we learn and things like that so hello Moi welcome welcome all right um should we go back to so let'
s go back to what what what what information comes in when we want to add a song right so is this what we want to do for
our yes and then there'll be other subs at some point yeah so they'll I mean uh kind of discover yeah we we'll see what
what we run into as we as we get into what this looks like so there's going to be parts of the song itself what
information is that um and then themes uh and since and so this I I keep coming back to themes because if I you know how
do you handle things like typos so let's say because we're probably not going to start the UI the initial
implementations with sort of autocomplete so um and even if you do you can still have typos so what do we do about that
um so let's say you know you type New Year's with no apostrophe and I type New Year's with an apostrophe which one do
they both get accepted and now there are two themes right right and so that's sort of the downside of automatically
creating themes is is you can end up accidentally with multiple themes um this happens to me all the time I use a tool
uh or at least I used to use it more uh called pocket and one of the things you can do is add tags um and it had exactly
that scheme of it will autocomplete but will also if you type something that is not in its tag database it will just
create a new tag and I've ended up with like sometimes half completed tags like web de Dees instead of web design
because I didn't hit the right key to autocomplete it um and I hate that because now there's no they don't provide the
tools to to to manage that very well um so these are the kinds of things that that uh you're thinking about we'll
eventually want to yeah but for now we can make the simplifying Assumption of whatever you type we'll accept right well
again starting simple and growing from there y so you asked a question about what is a song yes is that the next
conversation at least what is the song at this level because again it's going to be iterative but what's sort of the
minimal requirements for right now yeah artist which really means slash band somewhere and that'll get into some Rous
language what do we calling that right um we could call it artist band that would be acceptable if we feel like we can't
pick one of the other yeah I'm fine with just using artist frankly um uh so for required you know like Old Lang Zine
right is I just want to know which one they asking for now this brings up now actually now that I say it out loud is
there the idea of a artist in other words the song is done by so many people that like oh Lang Z we but I mean I can't
imagine I wouldn't associate it with someone would anyone want to submit a song without an artist that seems like a
corner case so I think at first I would yeah I me mental thought is those two would be required yeah I mean you know
there are certainly going to be songs that are going to be added that might be in some database somewhere um and but I
think that's probably a later piece of functionality where it could help you pick the song that you're gonna uh that
you're gonna enter oh meaning you start typing and it finishes right right um or you type you know maybe not old length
sign but but something else and it says which you know which artist version artist plus version are you are you looking
at you know this song which was the live version from 1981 or this version that was on the EP or this version that was
right so there's there's all sorts of things that again sort of it can assist you with with entering that but I think uh
to start we would probably not wanna not want to deal with that I got an interesting one I I think we talked about it
offline before we even started this project and I can't remember if we talked about it or not but I think we did was um
songs with same title but are different songs other words right cover versus not cover that's which I'm not sure how
ubiquitous the term a cover song is but in the DJing world it's known as you know not the original but it's the same
song just sung by a different artist um or performed by a different artist proba always singing right um and then
there's just a song it happens to have the same name yeah just happens to have the same name because there are bands
with the same name with because they're bands with the same name yes right so that'll be another one right and hopefully
we'll handle this does how do they do it they just look at the name of the band and assume they're the same how do I
know this because because I get suggestions in my Discover playlist for a band called Asia which is not the one you're
probably thinking of and it's like what the hell is this crap um and I got another one for zebra it's like no that's not
the zebra that I like that is a totally different thing and it is not at all that band and I don't know why you think it
is and why you're suggesting it pen thing yeah so clearly Spotify at least in how they're structuring their data does
not differentiate or at least it doesn't surface it that way maybe internally they do but I mean I'm sure there's some
unique identifier uh because when you bring up the actual band so it must be for some parts of it like for whatever
their machine learning suggestion recommendation stuff it ignores the fact that this zebra is not this other zebra um
because if you go in and say show me the the the phography for for my zebra uh it does not show this other album so
clearly it it does differentiate it but in the recommendations it's apparently ignoring annoying but I don't have come
on how you really so yeah just a few things to think about for future yeah so we mentioned typos already yeah um yeah
like there are certainly lots of covers of of of some songs yeah yeah they rarely mark them as covers yeah uh you can if
you sort of drill down into credits you can figure out that it's a cover um but also like just because it's a what's the
difference between a cover and the the artist recording a song written by another songwriter before the songwriter
themselves made this or right which is a cover which is a cover like you know Pat bitar's song that John melan Camp
wrote It's like well which you know which is the original certainly Pat benitar is is known better but uh yeah there's
all sorts of interesting stuff minutia yeah which is which is why like I always tell the developers focus on the
interesting stuff that's in your technology uh datee release so that might help differentiate some of it right um but in
terms of what we want to enter now uh the question will become how much data do you want to enter that's minimal that's
still going to be useful to you like is is that enough to be useful to you personally because that's really all that
matters yeah um the moment the three that are starred or what come to mind as use immediately useful okay there will
come a point where it's like oh the um 7inch single version of that song is actually a different has lyrics about blah
but not the other way around maybe the full length version that's five minutes versus the two and half minute version
does have references to theme X whatever that is right um so that's that's a whole I was thinking about that but that's
definitely a Next Level kind of thing right right but there will be a point where but it's important but it is important
and so yeah and that might be where we start um which you know I really don't want to have right a nodes field um but it
could be a I don't I know if I want to show you I mean you might want a notes field but yes it it can start accumulating
things that you want in more concrete categories yeah yeah I was trying to see if I spreadsheet yeah do oh that's
interesting Apple music can't differentiate between songs in different interesting yeah I did I show this before I can't
remember uh I don't think we showed it on publicly yeah publicly I'm not sure it's um particularly a problem to do that
because it's all stuff entered by me um my artist band song title release title format whether it's a compilation or not
um that ties him with release title which I believe yeah that's funny because uh uh my son and I were in the car the
other day and listening to some Tom petti it's like which album was that on it's like oh it wasn't on an actual wasn't
on an album album it was on uh uh the a greatest hits or compil a compilation it's like really there was a new single on
the compilation is that where it's from and now I have to go do more research but um like sometimes not all songs that
are anyway yeah there's all stuff well there's a whole different thing so what you call a compilation I don't so I was
yeah we were discussing like is this a compilation is this the greatest hits what do we call this right like discogs
yeah has these two meaning the same thing to me compilation equals various artists oh interesting so to me and the radio
station I volunteer at okay okay they are so they are not the same whereas discogs they're the same interesting because
what we what we were sort of discussing is like which one of these fulfills the record contract that the that the band
was under it's like they had a 10 record like we're talking about Rush had a had a their first contract was a 10 uh a 10
album contract it's like so do live albums count okay but do collection where it's it's just songs we've already
recorded and released uh or is it songs we've we've recorded but never released or different versions of songs we've
already released what do you call those and do those fill the contract and so it was an interesting conversation that
neither one of us had any information about yeah yeah but like this this can totally uh affect what you know what song
what's what's what song it is like what is a song and I don't know what the call this one you know so in the compilation
column of the spreadsheet which where' It Go um I started out just saying compilation or not and here I actually wrote
down collection Just For the First Time right to differentiate so this is Nancy Sinatra just came out like a month ago
it's a collection of old uh Rari so some of it singles some of it stuff that's never been released demos Rarities so I
was like well maybe I'll put in collection just for Giggles let me see if I have anything else in here I guessing
soundtrack would be the other word I had that call uhuh right right because it's I don't know what to call it I'm
calling it VA which is not know you know soundtrack is release type a good name for that instead of I don't know and
again I want to punt on that I don't consider version right I mean I think the important thing is is like if you find a
if you find an entry in our in this database can you go play the song right because if you can't or you play the wrong
one like maybe you play the radio edit instead of the full version and it doesn't have like you're saying those lyrics
um that would kind of not be what you want yeah exactly so it's it's really does it Define it well enough at least for
you to to know oh that one and be able to play it that's really the question yeah and so for now I think we can do
without that record label is another one not necessary maybe it will be at some point maybe this is a radio only thing
um o um meaning it needs to be edited to be played has some objectional yeah yeah F us United States there's right the
Federal Communication and there's certain words and things you can't utter on the radio right right um but now the
reason I popped this up was the notes column because to see what right you know some of them um yeah this might be too
much of a this is a big tangent yeah yeah I'm not gonna dig into that one right now yeah um but yeah I think all the
rest of the columns I think are themes oh and that we had kicked around the idea of link to the music or link lyrics
right I think we can add those and then contributor uh that one proba out of the gate well no but it's easy because it's
always going to be you right until until you allow somebody else so that would be an easy you know upd triangulate into
it or not even triangulate it's just you know when we add that column it's just always the default will be Ry when when
we do the database migration so that part that one's easy there we go so I think these four are fine okay name artist
song title release title all right um do you think title if if you just saw release would that be clear to you or is
release it clear to you it is clear to me then that's all that matters well oh from a because you're because you're the
you're the you're the main customer right but I'm meaning from a somebody visiting the website if we had a we displayed
data and we said release title I don't want to call it album title because it could be a seven inch single which half
that's why it's not doesn't say album title it says release title I think if I saw a column header of release and
actually something some concrete example of that um it would be really clear what it was okay and that's we could which
is different for uh for data entry um where I'd have to know what do you mean by release and there we could maybe you
know assume that the contributor understands what that is that they're more informed about your taxonomy and and right
you I could say something like you know album or single title something like that yeah yeah cool we're at the top aren't
we yes so uh we'll answer this question then we'll take our break um so fof asks when should we use database migration
uh which phase of the project um when you start writing stuff to a real database that you where you care about the data
that's already been entered so you can go a fairly long period of time in the beginning where a you're not even writing
to a database which is what we'll do we'll write the stuff in memory eventually we're going to want to do a little bit
of data entry um and we're not going to have to want to type that each time or hardcode it in the application so that
when we actually start writing to a real database is when you want to use your data migration because you don't want to
try to add it after you've already created your schemas you want to pretty much start out of the gate um because
especially with something like Flyway and I I don't know as much about licco base but I assume it's similar you just
Define what is your schema you're going to have to Define that anyway so you may as well Define it in in your migration
uh tool of choice but it's a good question all right let's take our break how long do you want to take could do five all
right take our five minute break um and when we come back we'll dig a little deeper into what what we're five all right
uh so just a reminder to folks who are watching um you can find out uh more about me and where to find me on social
media LinkedIn McDon Etc go to ted. Devout and if you want to chat about stuff in detail that comes up on the stream
like hexagonal architecture or testing and test driven development things like that uh go ahead and check out uh my
Discord Community where we talk about exactly that uh and also we have uh a book club um we're currently about two
thirds of the way finished with a book but we'll start be starting a new book sometime next year so be sure to uh join
and so good yes I wish I could have actual more coffee but it's too late to have more um got some more questions before
we dive yes yes so uh so this is a a really interesting question so um there's obviously no data migration but there is
um the need to create basically mappings uh so depending on on how you do your database support you could um Direct
store your entities and by entities I mean domain entities you could directly store your domain objects um into the
database using tools like hibernate and jpa and things like that um hexagonal architecture says no don't do that uh in
fact most separation of concerns architectures say don't do that don't mix your concerns so what's nice about um
separating those concerns is is then there is no migration it's not like we're having to to change something that we've
already written uh we create our domain objects as we find it convenient and uh best and sort of optimized for code and
testing and then we just have to figure out how to convert that and map that to the database um but we'll look at look
at we'll we'll see that pretty quickly is uh it it especially with um the snapshot pattern makes it really nice to
separate the state of the object from uh from sort of the object-oriented well encapsulated objects that we have um one
thing we haven't talked about and we probably don't necessarily need to talk about right away but sooner or later we
will which sourcing for uh do we do event sourcing database yeah it's I mean the big reason for doing event sourcing is
to know well one big reason is why did that change right why did that change and what was it before right um because you
may not NE necessarily care why it changed but you may want to know perhaps when it changed and what was it before um
and there's an interesting tradeoff also around changing so speaking of sort of changing the the structure of the thing
um migrating the data is in one way harder because you're having to now say every event has to now have new data because
we've added hey we've now added uh release in addition to release title the the version of it or whatever we want to
call it and so we'd have to have have um I the there's no database migration because the database when it stores an
event just stores a blob and so there's no uh yeah there's no there's no change needed on the right on the writing side
on the change side um it does of course mean we'd have a read side for convenience sake uh so like everything else
there's trade-offs um but it does make the initial code a little bit harder to work with um and my my sense is uh when
things are unstable you probably don't want to start with event sourcing much I don't think it'd be too difficult to do
that so at some point we'll have to decide that start with it or switch over if we I was man understanding was switching
was harder well switching is uh so switching is harder because you now have to change the way the the object is written
um so so it's yeah so it's really the object that that makes things difficult to to switch um the data switching is is
actually I think the easy part um but you're going from uh commands change state to commands generate events and events
change state but there aren't a lot of commands here so I don't I for for this app I don't see switching being all that
difficult hard yeah um yeah and you say storing is a blob and my brain went down this path it's like so how different is
a relational database storing a blob from a nosql style database um in what's sense not sure I just it made me go huh
how I thought about comparing so for example postrest makes it very easy to store Json blob in a column so yeah that's
um basically the same thing and it doesn't even have to be Json blob because databases have always supported blobs right
of just some large object that it doesn't it has no insight into what's inside of it uh and for our purposes it
shouldn't care um so yeah well shall we get back to it oh sorry you were still I mean we'll we'll have to decide pretty
soon which way we want to go yeah but let's uh let's go back to our initial V1 release of song um which is it has so
does it have the first three or first four just the all right if you want to do minimum right the minimum necessary yeah
at this point well it's also I mean it doesn't cost us much to add more um and so you know because it's just it's just
data um in that case I would yeah uh full mentions uh vent sourcing need framework uh no you do not have to be at the
tyranny of Frameworks you can write code yourself um and I would say I would not use a framework for for this in terms
of supporting event sourcing yes it's certainly possible you might Implement stuff that the framework provides out of
the box but like all Frameworks you are now taking on all of their complexity and I've looked at axon and it's a very
nice framework but it is a lot of complexity that I feel would be overkill for something like this um so you do not have
to always adopt Frameworks and on that same route is the idea of by implementing it yourself at least once you now
understand the framework way deeper than you ever or maybe not ever will but then you it'll make it easier to understand
what a framework gives you versus not give you and then you could make a an informed more educated decision y about
which to which way to go exactly y yeah exactly and and I think it's I think it it really helps to have implemented
stuff even if you end up using a basically what you said and I think it applies to to any framework that you might pull
in whether it's a spring boot or a corcus or even smaller Frameworks um having done and written the code that the
framework provides gives you a better understanding of what it supports uh and where you might find maybe you don't need
the framework um so I was reading a series of Articles of someone who's who's basically here's how I I moved away from
Spring Boot and it's a totally valid uh thing to do now spring Boot and spring framework has a lot of complexity but of
course it brings you a lot of benefit you don't have to wire things together yourself uh but I think it's important to
understand what is going on underneath the framework um at least in the Java world most of them are going to build on
the servlet uh specification which has been around pretty much forever as long as the web has been around um and if you
understand that and filters and interceptors and these things then you will have a better understanding of what the
framework is doing and then when you have to troubleshoot things you'll understand it better but you don't have to use
Frameworks and or you don't have to use all the framework that the framework provides uh you might use pieces of a
framework and so you're using it more as a library but um downsides um and and this is one of the downsides so uh I've
worked on large applications where we have had a homebuilt framework um and it meant that so I say if you're going to
use a framework you're better off using one that's public because then people can learn from it uh outside and they have
to learn from it only inside your company so if you're GNA go to a framework prefer one that is public um or open source
yours uh but it's unlikely to get traction it's going to be very very uphill battle but uh unless you're framework is
doing something very specialized don't create your own framework um and so uh that's the downside of of sort of not
adopting a framework is now somebody has to understand the code you've written but if it's well written code and well
well structured that shouldn't be a problem but if it's turned into a framework because now you have a bunch of
applications inside your big corporation that relies on it now you got a different situation uh and I certainly know of
companies that have developed their own internal framework and then switched over to something like spring boot
specifically so a they can stop maintaining their own thing and B they can find people in the marketplace who know how
to do the framework instead of thing uh yes zigi that was that was the series was referring to um uh I I wish the author
paid a little bit more attention to uh Bell checking and grammar checking uh either English is not that person's native
language or they're they could use some editing but I found some of it hard to understand because some of the word
choices were wrong um but yeah um so that was that that uh so X proof asks inter what are interceptors request
interceptors and filters and I would suggest doing some research on serlet and those topics uh you will uh be well
served if you're doing Java stuff to to understand what those are yeah and it would be nice yes if we could have a
little bit more flexibility in our Frameworks where we didn't have to sort of adopt everything whole cloth um but a lot
of times the framework some of the framework benefits come with that and uh well like field level field injection yeah I
wish you could just turn that off um I know you can certainly have linters and things like that to say don't do that
because you really shouldn't do that it's just bad idea don't do that Constructor should um so when we add a song with a
theme um the question always comes up when you when we're thinking about what tests would we write is how do we know
that worked well we would then go back and ask for that theme and that song should show up right so that's one way to do
it um the other the other way is to say h maybe we need to be able to search for a song by some of the attributes that
we about to other attributes that we're about to type in but theme is theme is certainly good enough to start um since
we already have that code uh we can basically build build on that right and I think we did we did have searching by
other attributes as a as a later story later feature yeah y yep um so I think we have enough to start writing our test
sounds good I'm just going to run all tests just to make sure nothing of course ready didn't accidentally type something
happens okay so we want to write a test so are we thinking about doing this at the application Level outside in kind of
thing I guess that would be the case because yes um uh we're not at the stage of writing a DB out adapter we're still
writing the application layer for uh creating songs yeah it's still it's still not even a database because it's still
not even a there's no repository there's right now there's a hashmap yeah in memory that the Constructor populates so
it's in yeah it's in memory right right once and that's it so this this will this will force us uh to change that not uh
yeah so this is going to be our um So currently we don't have an application layer package uh right now our domain s Our
Song Searcher is in the domain um oh and uh but I think this is this is where we'll we'll start test driving our our use
case layer and that'll that'll Force us to adapt the song Searcher as needed no pun intended or maybe it was intended um
no it wasn't so uh yeah so let's write a let's let's write a new test a new package so let's create a new test in a new
package so um we want the package to be which which package would you like uh so this will be in our application package
okay I guess I don't have to do it here I could but I could do yeah you could right click on on the the the higher level
package so so up from that yeah and then you can do new from there yep what were you calling it again you said got it um
well first you want to type the the new package name so application dot they're basically doing two things at once we're
creating new package and then the name of the class um and for lack of a better better name this would be uh what song
entry service song creation service song Adder H do you like them to be verbs like song Searcher you said song Adder so
I was wondering if you were looking for symmetry there um there are sort of two schulls of thought that uh one is just
add tack on the word service because people recognize that not that I necessarily like it but it is familiar um on the
other hand I I do prefer if given a choice more precise ones that are um very much describing a case so you could say
you know uh actually well no it's a song you could song um song Adder basically makes it more more verby ad song very
much has a command flavor to it right which is good because at this level that's what we're talking about sort of these
high level commands Okay so we'll stick with that yeah let's go with that okay it's different from what I what I usually
usually do um but in a good way okay because we can also refactor names that's the beauty of it that's that's the beauty
so oh I just created it you created uh but this is test so let's let's rename it to be let ATT yeah and this does not
need to be public not that it matters you just deleted did you make it literally private no I just you can't public all
right so that um it asked for junit five that's why I was like right um because what if we tried to fix it we would we
can't use test containers properly that's all right once you add the first one then the others so we can go the zer1 so
whenever I'm faced with the blank page syndrome I always think of zombies uh so we could go to zero one many and say
zero but adding no song so so what does adding no song do for us um would only it would provide us with a test that
given a new whatever when we when we try to search by theme we get nothing back and so that sort of provides us with a
baseline is if the database is empty or at least has no songs of this theme uh we should get no songs found when we try
to search by a theme so we're we're saying add so it wouldn't be add it would be um no songs found oh I see now I know
what you're talking about yeah so basically the scenario of yeah yeah so this will this will help us Define define the
basically the API for talking to the to the use case right right okay yeah it's it's nice to try new things um but it's
also nice to be consistent and opposite well the search is is the is the uh the assertion part um but we still are
adding we're just not actually adding um but adding nothing is still technically under under adding is the way I think
about it if we've added no songs we should find those songs um then we then we'll add a song and it so what does it look
like to song so it' be just instantiating you know firing up an object and going hey G any songs and it's gonna say say
no right and this does bring up the question of does the ad song application layer service does it functionality or is
that a separate thing and so here's where if we just called it song service it would be easier um and we would just put
both in in one place but uh formulating as as as a more granular command like thing um we do get into this question of
of uh where is the functionality for query now the query we don't have the query already out at the layer no because we
have no application layer we have it in the domain layer um but we don't have in the in the application layer is song
themes application in the application layer no that might be my confusion it's not ah is that which layer would that be
in if we put it in the package uh would be uh configuration ah right right we talked about that last week yeah okay
that's the source of my confusion y yeah because it by default when you do the spring boot generate it it acts on the
word application which can be confusing which is why if we talk about his use case uh perhaps it's not as confusing yeah
maybe moving it into config sooner to eliminate could do that yeah we don't have to do it right now but not well we have
a failing oh we don't have a failing test do we we have failing test okay so we could do it okay and a move like that
moving one thing one place I'm not concerned about yeah do I just say config dot uh no no no you want to do a a move not
a a move which is straight F6 F6 right uh no config would be at the yes please sweet now I take it back that this may
actually cause some some problems so tests um because it depends on the auto scanning yeah um and that's why I generally
don't don't move that so let's actually not do that because um it's best if that actually stays at the at the top level
really okay I thought you had said you usually move it into uh that one is the one I don't move because I don't put any
configuration in it got it so like the bean thing would go actually in a separate config class got it so sorry as soon
as you did I'm like oh I don't think that's gonna work because the way the spring Auto auto scanning for component
classes and and other things starts from wherever the application is defined and and looks at nested uh Next Level next
level stuff you can configure it differently I I try to avoid configuring stuff differently um if I really don't need to
right right it and you can't rename it to song themes config application because spring boot is looking for uh actually
no you can you could totally rename that as long as it has this at Spring boot uh application annotation um you could
name It Whatever the heck you want so what's important is that it has that annotation uh and it has that main method but
the name of the actual class is irrelevant oh so if you want to just fine if you want to call it song themes startup
which I would think is a better name you yeah I like that one better let's do that that's shift F6 yeah I finally got to
use it yes song things startup is that what you said yeah that I like it too much more clear oh name test with the
following names uh yeah rename the test may as well yeah match quick yes sweet and let's run we probably r the test and
we probably should check in yeah uh it's full enough ask does song search uh be in the application layer with respect to
hexagonal architecture so the role of the of so song Searcher right now is in the the domain um because it's only domain
stuff but we'll start seeing some of its Behavior will probably move elsewhere um and we may end up with not much
actually in the in the domain um there will also be so it's sort of hard to answer that question at this point um but
again the way I think about the layers is uh does it concern itself with retrieving information from the outside world
if so that's application if it's already has everything it needs and just needs to execute code and rules domain all
right that worked so uh did you want to commit and we can yeah we probably should avoid committing the the test that we
haven't finished yet oh that rename good enough perfect woohoo okay so back to back to our original question of where do
we put the behavior to uh to execute the query of find me theme so it would be in the soon to be created surface layer
right which doesn't exist yet right now song Searcher is in the domain yes but it's a very odd domain class yes because
uh in the sense that it's different from probably how you think about how applications work nor typically with a domain
layer you'd have songs Get Found and the song Searcher what the song Searcher is currently doing would be done by the
repository Andor application layer right um the way the song Searcher is currently written is as if you go and ask the
database give me all the songs and then you create a song Searcher in memory to search it you execute the search and
then that song away which is certainly a valid way to go um but sorry so so do you know but do we in a sense want to
stop doing that stuff question so if song Searcher was always around we just would load it once from persistence right
um and then we just keep it alive unless there's a change obviously and then you have to do a refresh right um so the
question is whether we want to continue with that model or right okay yeah so do we want to continue going that way in
which case we would Orient our our use case layer around that um but if we feel like well we really want the database to
do that or we want the repository to to do the bulk of the work um then in a sense what we'd be doing is is pushing song
Searcher into the use case layer uh and likely actually just deleting song Searcher and retargeting layer part of me is
thinking well go is this the last responsible moment for making that or are we I think this is I think this is the last
responsible moment because if we start putting effort into saying we want song Searcher in memory that gets loaded and
loads everything that's that's a non that's a non-trivial decision because if we decide to change that um we basically
throw away our song Searcher and the supporting code in the in the application layer got it so pros are we don't have to
do any of the we let the database do the searching performance-wise it's probably not going to make much of a difference
that many songs so there well so run so what does performance mean right and this is um this is where we look at what
are what are most of the operations going to be are they going to be adding songs or are they going to be finding songs
mostly finding if it's mostly finding then you say what's optimal for mostly finding is have everything in memory so you
never even have to hit the database at all welcome yeah so suiga that's that's kind of what we're talking about is do we
say that song Searcher is in a sense the aggregate right and so the aggregate could be the entire set of songs that's
totally valid if that's the unit of editing if that's the unit of transactional locking uh then it's all the songs and
then it's basically you load all the songs put them into the map and then if you want to modify them you modify the
repersent um so we'd probably want to say uh that song Searcher is the read model um and that like a cache it would be
invalidated uh if there was a modification so there would be still a separate aggregate representing modifying a song
and that would be song that seems to make more sense to me where the inmemory read model song Searcher becomes the in
memory read model because it does seem weird to have to okay I'm going to rewrite the entire database right so clearly
that's not going to be the a useful aggregate for for changing yeah right but it's but it's always interesting to to
think about it to start there because that could be fine right um and so since it's the the read model if we say that
that's the read model now we are introducing complexity around eventual consistency because somehow we have to Signal
the read mod model to refresh itself right um or as part of writing it out we basically go and and refresh the read
model but this is still the time to make other or did that shift I think it I think actually in my head it's now shifted
a bit because if we say that song Searcher is the read model then that's what we query against and for now time um and
so it's an it's a very inefficient read model because it's it's D we read everything in and then we do the song search
and then we dump it uh although we don't have to do that but that's sort of conceptually how we we think about it but
that would just be for the period of time between when before ad song is has implemented when it's just right is it once
we start adding songs then we could at that point implement the hey we added a song refresh thyself that's true right
actually we could we could have the um the service layer I mean the service layer could hold on to the song Searcher uh
it sort of violates my service layer should not hold domain data um and so it's a question of sort of right there's this
Singleton song Searcher who hold who holds on to it I almost want to see your hexagonal diagram again just try and
visualize this yeah it's not a good fit well in the sense that um let's see because the domain so thin one so mainly
because uh songs are in the domain and song Searcher is also in the domain it's just got a bunch of songs in it um if we
want it to be remain in memory how do we do that that would mean the application layer has a reference to it um which is
not the typical way to do it there's nothing I mean these are all guidelines there's no rule that says we cannot do
implications the only the only thing I'd be thinking about is like how hard is it to test I don't actually think that's
a problem so we could totally do that so let's just say that the hexagonal rule was sac orank and how would we do it if
couldn't if the appc if the application layer could not more than during the execution of a single request coming in
right right right because that's the typical right request comes in the application layer coordinates loads stuff from
persistence which are basically domain objects and then calls method against those domain objects and so if song
Searcher is sort of the unit of of that process it means when we go to persistence we say give me all the songs
instantiate a song Searcher execute by theme and then it goes out of collected so we're loading you know for loading 10
songs not a big deal for loading 100 songs still not a big deal for loading 10,000 songs now we're talking about we're
loading 10,000 songs and we only end up finding three that's domain can't hold on to it domain is transient right so one
thing that this diagram and most diagrams don't show is over time the domain is is is transient only comes into
existence during uh and I think I have a sequence diagram that might make that more clear but basically the domain only
exists as long as this sort of roundtrip requests are happening are happening once the returns its information and then
the application returns to its caller all that stuff goes out of scope and is gone which makes it unit testable because
it's not dealing with persistence or not persistence but it's it's not dealing with with hidden holding on to State yeah
holding on no but it's just a guideline because generally you don't have so the danger of of of the application layer
holding on to over long you know in a sense over multiple requests um is that it will have be holding on to stale yeah
so elevating the hash map in memory repository means that we're saying that the database is responsible for searching
that's the implication of of doing that that song Searcher becomes basically song Searcher becomes the IM memory
Repository right so if we if we say song Searcher is the thing and we ensure its lack of it's its freshness because the
application layer dumps it every time there's a change um that way we can ensure freshness but that's still inefficient
because we're basically but if we're only making one song change a day that's fine one song change an hour that's still
fine one song change every you know 10 minutes that's still probably fine um one song change you know and so even sort
of the most frequent times You' make you'd make changes to songs it's still probably relatively efficient um until you
get to a certain number of loaded because in a sense it's it's basically the perfect everything so oh sorry go yeah
that's basically what we're talking about sui so this this the song Searcher is the entire domain in memory held on to
and it's invalidated when the right invalidates it and we reload it so if we had a domain that had some complexity to it
be um would that be are you are you basically just asking where would caching be yeah so if if we were not holding
everything in memory when songs were individual things and the repository respon was responsible for retrieving them um
the caching would be at the the query method so every time we've called by theme with this parameter every time we
called by theme with new years it returned these results that would be cashed so if we're doing that frequently then you
know because it's New Year's time that would be the popular search uh those would be cached and we wouldn't hit the
database and you would Implement that and that would be implemented in the application layer no that would be
implemented uh at the repository you could implement it at the application layer with your own implementation that's
also possible um depend basically depends on who's doing the caching is the framework doing the caching or are you using
an explicit cache of your own not that you're writing the cache but that you're calling a library like caffeine which is
library and I'd probably so if it were me I'd probably use caffeine so I could cach it at the in a sense the the more
semantic layer of by theme as opposed to does so what we're talking about is is actually not apparently not not an
uncommon scenario right if your data if the if your application like I'm actually working with an individual coaching
client where it's the it's mostly a read search app the data changes but very infrequently and so why not load it all
into memory uh then all your searches are in memory and everything is super fast um and it's only when when it's becomes
a tremendous amount of data where you're not where you're now starting to pay for that data right you've exceeded the
the virtual memory limits of of the container you know the level of you're paying for now you have to pay more than a
month to store that in memory um plus the time to to to refresh it uh if that has happening long enough then you switch
um but it is probably even though it's not rare it's it's the less common uh because a lot of most apps are are what
what they refer to sort of online transactional processing right you're editing this little bit here this little bit
here this little bit here all in dis disparate things um but I think there's a there's a type of app that this falls
under that has this very Behavior yeah none of this requires us to actually have a DB yet we're just faking stuff to a
certain extent yes but we are but this is what I would consider an architectural decision um not that it will be
expensive to switch uh and we may have I think hit the limit on how much we should we should talk about and just decide
um but it is it is one of those uh it it changes the basically the type is my head's spinning I'm not sure how to decide
this one yeah I don't know if all that has has actually helped this decide you I'm kind of curious to see what it would
look like if we kept going down this road where the song Searcher is this fully loaded thing in memory that occasionally
gets refreshed when a right happens and put it where and so the the service the service use case service layer would
have a reference to song Searcher and song Searcher does all the work and song Searcher is basically the database and we
only have just the the persistence mechanism to store it when when uh in a sense in case that the machine went down
because if the machine ever went down right if we could say you know and there AR maches that do this we would never
have to write to anywhere it would just be a memory um so really the persistence in this case the database would be a
backup mechanism that's all it is because used and from a learning experience if it turns out we've painted oursel into
a corner well we then deal with it and that's right you know yeah it is a learning exercise yeah so that's funny we
could flip a coin um and and I think you know we I I think since I haven't done this that's why I'm curious what it
would look like uh and since you don't care uh and clearly and and as well that um it's not like we have tens of
thousands of lines of code that would be harder to to migrate um I think we can go down this road and if it turns out to
be wrong we've learned something so what yeah we've learned something yeah uh so put versus post that's an easy uh
question to answer it's who decides what is that's it post assumes the server is going to create the ID or whatever
thing you're creating put requires some kind of ID that the client creates that's it uh for updating you would use
neither put nor patch yeah I don't know we we'll see because I think we're we're GNA start we're going to continue
writing our test now the one the one it could just be load yeah load the one it can only be one all right let's switch
back to you okay okay no songs added than I need some um I think we're going to need uh we sort of have an answer the
question of what are the responsibilities of of the ad song um and since I'm not I'm not sure how we want to do that um
I feel like I want to fall back to song service and have and do the queries reads and writes through it and then we can
see later if we want to split it because we've already we by saying ad song we've we've we're splitting it and I'm not
sure what the other thing looks like got it so rename this yeah so this is just song sure song service test for now you
just service yeah so so there is a there is a naming convention that I'm not sure I I like um uh but aliser coiner has
somewhat adopted it for hexagonal which is this is a port and what is its purpose it's for finding songs and so you name
the thing for finding songs literally F finding songs um I'm not I'm not I don't hate it but I don't love it so uh we're
gonna fall back to this and we can later yeah we're going to write as much as we can in the test uh and and move stuff
around and refactor yeah um so the test name still applies uh and so let's service Alt Enter okay yep and that'll be a
class make sure it's in the right destination yep uh this is one of those neither one yeah I was say what I hate when
intell does this you have to click the three dots um oh because this is the case where actually the package does not
exist so let's so let's um when I do go make a package no no uh we'll manually change the destination directory so go
into that dialogue and you can manually change it this dialogue um oh does it not allow you to actually go into the
dialogue it's only a drop down I can't it's only a drop down yeah um all right create it there and then we'll move it
really yeah okay because it it can't let it won't allow us to do what we want right which is frustrating um now let's do
an F6 move and now we should be able to uh oh up here so that's fine but I think the is it not going to allow us to do
package uh uncheck the show only existing Source Roots yeah I wonder if that was true before we did the move I don't
remember seeing that checkbox but it could have been there you want to try undoing and seeing do too undo one more Enter
go yes ah it was there okay and I'm just blind to it because I never I I never check shortcut yeah let's drop that down
to the yep all right so that's our our setup and our um so now we have to decide what do we want to call it so we want
to say um find by theme or search by theme we we've been we've been using the word search I think we have yeah yeah so
let's say search by theme theme and let's create the method uh actually let's store in a variable first so that yeah to
force the type y hey you won't be able to use dovar you will have to you will have to manually do it because it doesn't
oh my God it's it's only yeah it only it only knows what to VAR it up if if it knows what it's going to return otherwise
it actually want it to be a list of we want to be a list of song song or string at this point uh well we have a song
object and that's what we want to animal okay Alt Enter now we can create it with bears with knives and bare skins
method yep yep no no but good guess all assertion two hours in we finally writing test did you grab the um the live
template that uh that sui shared in the Discord for the assertion no we should do that okay do it live now or offline
later uh yeah let's do it live now okay let's see Discord which channel or which um uh it'll be in the intellig channel
intellig here I got it you got it templates uh and we want let's start with the as one what are those three are those
acronyms ASE yeah so they become the what you type uh click on Raw just because it's easier to copy and paste and then
copy the whole thing and in intellig open up your templates and click in Java on the right and then just paste or just
right here doesn't matter just paste magic whoa so that is that is cool but is totally non obvious yeah it's completely
obvious it is there is nothing that tells you that you can do that other than reading the documentation I remember when
I learned about it in a blog post I'm like you're kidding that's how you do it because I was modifying the XML files
directly that are that are where the configuration is and that was no fun oh wow uh one more thing is um I like to check
the reformat according to style yep and then if you hit okay the rest is all good uh so now if a and then hit enter so
it does two things that's nice so thank you suiga uh one is it automatically Imports the assert that if it wasn't
already imported um and then sets you up for writing a nice assert that statement Wei yeah sometimes uh yes it it feels
like and and and I have to remind people like typing is not the bottleneck that's that's not the the typing is not the
important stuff yes we have to do it but it's not the important stuff it's very easy to type a big pile of stuff that
you now have to throw away yes you can now you can now have ai you inconsistently uh so we assert that songs found um by
the way when you see the blue rectangle that means it's waiting for you to hit enter so it can guide you through a
little bit of AOW back it's already it's already done so we won't do that again oh won't do it again okay yeah so if you
don't see the blue rectangle uh it's it's no longer guiding you through yeah I was trying to get back to that stage
you'd have to you'd have to go back all the way to before you type the live template yeah right so now you see there's a
little blue rectangle y that tells you and you might see there's a very faint one on the next line because that tells
you where you're going to go next he empty uh and we want uh exactly that yes yeah it's a really smart template I knew
which one we wanted well uh in the template you can say give me a a good candidate and then it will yes and then it will
use intellig smarts to figure out what want um proper machine learning not this fake stuff so this will fail because
it's trying to dereference a null correct so we switch to um yeah we can switch to the ioe iio at well the simplest
thing will work is list so if you just type empty list lowercase e yep that one there go I trying to remember which
class it was in I never remember which class it's in I just know if I type EMP it'll aut complete the right thing it the
easiest the easiest application to write is one that does nothing or at least doesn't have to work correctly so if all
we ever care about is that it doesn't find any results we're done alas I think you want more from it than that yes uh we
probably do though perhaps time uh X proof the do we replace the resource with the data uh or partially update is going
to be it depend and are they providing a complete replacement for whatever unit of of data you're you're working with in
which case it's a complete replacement um or is it I'm just updating my ZIP code because you got it wrong uh there are
positives and benefits to either that are sort of outside the scope and would require a lot of context so it depends but
the benefit of something like a patch is you're basically saying change zip code from 94115 to 94111 um is the best way
to go because if it turns out that it somebody already changed it it won't try to change it in an incorrect manner so
you want your patches to be item potent item potent is a key key thing in the world of distributed systems which is best
it's okay perfect great all right we got the zero case let's go and and um one song added then one song found um mirring
yeah one song added is theme yeah item potent has has that weight of of of feeling very like a much term uh yes you
can't retry safely if it's not item potent um because now you don't know are you causing two things to be created for
example or uh is it going exists yes there's all sorts of contextual questions about um um what is the scope of what
you're updating and this is where uh I really find thinking about it um in that way helps you define and design your
your Aggregates because you may say um oh they're just modifying the address maybe I can just modify that without and
then somebody else could be simultaneously updating your order because they're giving you a discount because you're on
the phone with somebody because that never happens where you're both looking at the same thing or even worse I which I
encountered um so I have uh dental insurance from a company called Delta Dental there are two apps there are two web
apps both of which are available to the public both of which have billing and payments and both of them are out of sync
with each other oh my God so I can't make a payment because the current payment due is higher than what it thinks the
current payment is due so I want to pay the full amount that it's actually due but it's outdated by at least a month and
so I don't want to pay not the full amount because then it'll say you haven't paid the full amount but the news system
won't let me pay because it's broken because it says oh we can't do that try again well no trying trying the same thing
again is not going to work and so this is that um clearly they went the let's rewrite our application route and that
hasn't worked out well for for for them well they may not care but it hasn't worked out well for me so they're not
getting their money until they fix this um Unfortunately they can say well you're not getting your insurance until you
pay so uh I have I have to hope that um they will be uh magnanimous and say oh because it was insurance it's terrible
terrible like I can in this same sentence I'm not sure yeah I'm I'm I have I have very low expectations I I expect I'm
gonna have to call up and make a payment on the phone is what I expect and and cost them lots of money because they're
gonna have to pay this person to take my payment instead of was basically free but you know what not my problem it's
their problem as my son would say that's a you problem not a me problem oh yeah let let's let's not talk anymore yeah
okay back to the test um so uh assertion we will have to do something there but let's write our assertion expect and
here we'll use a contains exactly because machine learning can only do so much so what do we expect the song to be it's
not gonna be a string it's gonna right I forget the Constructor for the song uh you can hit is it contrl P control p Ah
that's a good one I don't know that one yeah since I turn off and I think we turned it off for you as well they
automatically always show the parameters because it's like if I want them I'll ask for them and how you ask for them is
Mac that's me typing it in my notepad so I'm thinking we should have a different song title for New Year's just for
let's mix it up of course I can't think of one off top of my head I don't any not sure I've ever done a New Year's not
oh there's ah could do uh this will be our year by the zombies yeah is that right yes ah interesting the fact he said bu
the zombies is GNA make some future interesting because we so long so far we've just been asserting on title right right
because I'm sure there's other songs with that title that are not that song not even a cover yeah so it's we're gonna
have to start our assertions are going to start changing soon yep y okay um so now I need to populate hi tkes so now we
can look at this test and say there's no possible way this could ever pass right um but we certainly could watch it fail
yeah for the right reason which is clearly an empty GNA be expecting y uh and so now we can um improve the setup yeah so
I think now we would have to improve we'd have to add setup creating go ahead yeah no I'm not sure do we yeah gonna be
it's gonna be different that's why I'm I'm I'm not immediately giving you guidance because I'm not sure what we want to
do here um we could simply call a method uh because it wouldn't I mean we could make a creation method where it loads it
uh and then we could figure out later when we get to actually well wait a second um sorry I got confused for a second uh
that well it's not add song by theme it's just add song right right um so sorry what was confusing me is I think the the
the Whit space uh because the songs found line 28 is actually part of our assertion oh um uh part of the assertion yes
because the the command the thing we're actually testing is the adding of the song not the finding of the song right
right good point yeah and that's where I got confused like wait nope that's actually yeah okay so now song yeah oh yeah
that's initially what I was thinking because I thought we were testing the the searching but no we're actually testing
the adding um so we actually want to call the method that right and right now it doesn't do anything right so do we let'
s see we've got that Implement well we I mean we could run the test just to make sure it still fails for the same reason
but it obviously will because it's returning a constant right yeah um so our job will be now to um potentially do a
prepare refactoring so what would make what would make the change that we need to make easier turn that into a field um
no because we're going to delegate to the song Searcher oh right so the refactoring that would make the next change easy
is to introduce an instance of the song Searcher in song service as a field or as as a as a as a field that's defined
and created in the Constructor right we don't have a we so you Auto way of doing this Al insert but we're also in Red so
we're experts at tddd so we can move ahead with a a prepare refactor even though we have one failing test got it okay um
and then in here we'll create Searcher can you do straight to field is there a um yes basically new one up locally and
then ah there's no one there's no one step I don't think gotta but we can new it up why is it not working uh it's
complaining about song Searchers what's it complaining about let me do it it's uh song Searcher may not have a
Constructor that's accessible to US ah shall we go take a look at it yeah private private because we have the create
method so let's use the create y and now you can assign that um I think you could actually extract that to a field it's
taking song song well it's taking variable arguments and none is is a valid variable argument got it and then you said
this can go straight to a field yeah so if you do um uh uh alt control F whoa or or Control Alt F yeah and that's
exactly it yep so now yeah so that was that was a refactor that shouldn't have changed anything because it inod a field
um sorry finish what you're were saying yeah so we could run our test and see that that test still fails for the same
reason but an interesting additional step that we could take it is still failing for the same one why is my brain um
couldn't we instead of returning empty list return song Searcher yes yeah that was the that was the next that's what you
were thinking thing I was GNA suggest yes what does it not like oh they types song touch return the oh our search by
theme is returning string ah interesting okay let's go look at that we're probably doing the simplest thing that could
work at the time uh because that's all we cared make we either fix this or or change the um well we could do a parallel
change that might be the a good way to go so we could deprecate this one make a parallel change that basically just does
line 27 basically does that method but doesn't do the mapping right what were we doing at the we need to do the well we
wouldn't map we we still need to check for null but we wouldn't need to do the mapping we list okay uh song Searcher is
in the domain because it's it's basically been domain oriented stuff but it may get blown apart um what do you I'm
thinking parallel change but yeah so I think I think um because we cannot have two methods that return lists that are
generified in different ways ah we would have to rename one of them so I suggest we rename this one to uh song titles by
theme and then the other one will just be by theme got it we need to make this compile so maybe do now we're now we're
getting into the red zone of of uh we have a failing test and we're about to do a a refactoring but since since it's a
rename um I'm pretty confident and what was the suggested name you gave I missed it I ah well we could see that all the
other tests are still passing and just that one yes is the only one failing which is helpful yeah uh so we could do that
or we could do an extract method uh to end up with the method that we want which is what I was thinking okay so let's um
theme uh wait is that the order we want to do it in or do we want to do the inline so extract that get a method that
Returns the song no I think we do want uh yeah I there's Pro there might be a way to do to do it more efficiently but
we'll just yeah we'll just grab line 27 extract that because that's the actual thing that um can I I know I know I know
what we can do okay okay uh let's switch around uh the if block oh so so click on itself huh my cursor control get lost
and now do Alt condition now we have exactly what we want so let's grab 27 through 31 extract method what are the multi
what points I one oh it's because it doesn't have an else maybe oh uh well we can fix that pretty easily on 30 we can
just assign matching songs The Empty list that's probably better anyway so replace the return on 30 with matching oh
because what'll happen is when it does the stream map on an empty list it'll basically just do nothing and return an
empty list should run the test sure yeah that's the one that was and this is where it's like after a certain amount of
time having that one failing test is is starting to get a little bit more concerning but yeah but I think we're almost
there so we'll go one more um so now let's extract that yeah to now we go back to the test and now now yeah and we can
refactor that later but now we can go back to our test which we were so we'll still fail um because we're not forwarding
the uh we're not forwarding the search by theme on the song server so let's go back to song service and yeah I know we
have refactoring to do on the on the Searcher but we we'll come back to that later oh right we're gonna do this yeah
okay so uh you won't want the class you want the field right yep nope no that one yeah yep that was that was the whole
thing we wanted one that returned a list of songs right yeah just took me a second I figure out which was which yeah and
why is it red okay there we go all right now ad song is still not going to work but now this is the last it's the last
of the prepare refactoring exactly yes now it should fail again but y so now we implement this what I I I laugh because
that's not going to be straightforward um oh well we can we can cheat so let's cheat oh and just add a song even though
it's well so uh actually it's not cheating this is this is kind of the way we were the direction we're going we're going
to Searcher oh instantiate a new one and give it the song we just got interesting actually wait a we already got a field
right so yeah you have to ass to the field because we're replacing well got it we're throwing away the old song Searcher
and we are creating a new one but now we want to use the same we want yeah yes we are invalidating the cache yes uh the
project is not yet public on GitHub um at some point Mike might yet yeah probably soon maybe even really soon thanks for
asking as proof um so it's complaining because the field was that all right now we're adding the song we predict you're
I predict this will pass now I think it will too now is it gonna break other tests no because they're not using nothing
else is relying on it right nobody else is using it through this interface so now the the the one was the easy one the
the the many is is is going to one uh and and what's really interesting about this is is uh those those of you out there
who are much more uh functional programming experts might say well totally of course you do this way you want to add a
song to song Searcher you take the song Searcher and it returns a new one and everything's immutable and it's just a
function it's a function that modifies a song Searcher and gives you a new one so in a sense that's what we could do um
there are yes indeed we are we are we are creating the perfect cache which is always has everything and it's always up
to dat eagerly hydrating the cach I like that phrase um alth I think it's I think it's usually called warming the cache
so we are we are we are heating we are boiling the cash because it has everything in it so so many interesting metaphors
for for hydrating and and warming and so on um but we have passing test so I suggest we do a commit and then decide how
much longer we want our stream to go okay sounds good second cut um I think we now the song yeah all right um how are we
doing so I can go longer and so up to you how much longer you want to go yeah I can go for a bit I wouldn't mind a quick
break just to kind of stretch my bones let's take a quick stretch break and then uh and then we'll we'll do the harder
part which is adding adding multiple songs yeah all right stay tuned folks we'll be back shortly all right so let's go
so one more test uh do we want to do any factoring on the Searcher so we don't forget good point so I think there up I
think one we can one thing we could do is is uh make the make that method a lot more concise so there's uh instead
default and so the default will be the empty list ah wait so get our default now takes two things value yep and we can
basically just delete the rest of it and just return it directly or delete the if statement and then in line of return
yeah that's what I was thinking which intellig is helpfully suggesting yeah so that's much nicer sweet uh let's run our
tests just to be sure that that works like we expect it to work and then we could inline this one yeah I don't have a
strong a strong feeling about that one but I'm fine to try it if you want to do it so could try it and see if you like
it yeah let try it see if you like it or theme I mean it's honestly it's going to go away at some point so I don't I
don't have a strong feeling I'm Gonna Leave it okay that way um anything else I think that was the only things that we
needed commit so one thing I I tend to do is when I do a refractor like that I don't bother saying much because because
if I wanted to see what was refactored I just look at the diffs anyway that's true so just refractor cool I'm not I'm
not fully uh Arlo belli uh commit notation bought end to to it um in that R uh I mean I guess it's it kind of gets into
how often do you look at the comments the commit yeah uh honestly I rarely do yeah me too or how often do you look at it
where you don't say I still need to go look at the diffs anyway right I would look at the diff in how James you just
missed us saying that we're not going to do that because this method's gonna go away but yes we could we tried it we
didn't like it and that method is gonna is has a very short lifespan so all right um we did zero we did one now is time
go um I want to say multiple songs yeah good with with you uh I might say there instead of its but otherwise yeah was
annoying to me nicking that's the right there yeah y well that's the there there yes that's the that's the correct there
but the they there um let's do it we need another New Year's song well we do have we didn't really in this version of
the service we didn't add old langine did we uh that's true we didn't so we could use it um or we could add funky New
Year by the Eagles funky New Year there you go yeah here we're expecting that we don't need to add multiple songs at
this no we do we do because we want to make sure we so ah so I wasn't expecting you to do that oh interesting okay so
what were you thinking because I was thinking that you would call AD song multiple times ah because we're we were sort
of under the banner of adding one song at a all right James see you Embler yes that's why we like you swegi actually
what is the perimeter for ad song Just song yeah Oh I thought it was songs with the the verog uh no the vogs is is in
the song Searcher at this level it what was it called funky New Year funky New Year I never think of the Eagles as funky
not and I'm and I'm not even familiar with the album that it's on apparently they put out a Please Come Home for
Christmas album which I was not aware of but I'm sure there's a lot of music I'm not aware of yep now here we wanted to
do we could still do oh yeah it's a verog UNC contains exactly so we could do the same right and this will totally f fa
so before you run it yep how exactly is it going to fail it's going it I believe that's correct let's see yeah I'm not
100% certain to that but I I'm pretty sure that that it will only hold on to the one you added last what last yes so the
actual is only funky New Year yeah I always I hate the wording of this expecting actual yeah I it this is the expecting
yeah I I I agree that um the assertion output messages especially for the contained stuff is not quite the way I'd want
it um I understand what they're trying to say yeah yeah yeah expecting an actual it was expecting here's the actual to
contain exactly and in same order so that anwers your question uh OA is contains exactly is these things in this order
as specified um if you don't care about the order then you don't use contains exactly you use contains exactly in any
order and if you want the cheat sheet I've got a cheat sheet for you that tells you the difference contains I see a post
to chat coming yes go ahead and and uh uh let's we can close that I'll find is so you can find the cheat sheet right
what's the what's the simplest thing we could possibly do to make this work are so I think this this requires uh so one
of the nice things is create song varargs right um and and so again sort of this is a very functional way of thinking uh
create a new song Searcher with what's currently in song Searcher that so we'd have to have a way I don't know if we
currently have a way to find out what are all the songs in song that that so we basically do is say create song Searcher
oh song Searcher doall songs Comma Song right although the syntax is going to be a little tricky because it's farog but
basically that's so we'll start with yeah I would I would say the immutable the more immutable style of oop tends to
look functional in in in the places where you're dealing with the immutable stuff yes and that's that's the question of
where where you know do we encapsulate the knowledge of that so we could ask the song Searcher itself to do that instead
of exposing all the songs yeah that seems better to me uh yes yes yeah I I I happen to agree so we'd make a new um a new
method on create song Searcher that takes so it would be oh sorry it Searcher but it would be create song Searcher
adding or s or add yeah yeah because it's it's not quite a create um it kind of depends on on how we want to how we
wanna song that returns that new song SE yeah that seems like which which violates because it's it's functional and
functional differs from object-oriented uh it does violate the command query separation concern um but for now I'm fine
with that uh because it it it looks like it violates it but technically it doesn't because it's a creation and creation
is is it's interesting because bur Meer doesn't really talk about creation as much but one of the things I've I've
learned is there's commands there's queries but then there's creation and creation is this third category that by
creating right so it's so a factory is neither a command or right because really this is a factory exactly and a factory
is not a command or a query right I mean it's sort of a command in it looks it looks command like it looks command like
but commands modify state of an existing object and Factory methods and Constructors do not they create something new
out of out were yeah I mean extend search it's really but it's really it's really an ad uh and that's where we might
want to use the word create and so I don't know and I don't know how much we want to worry about that naming because we'
re probably not going to stick with it that long so um I'm not feeling any need to to put a lot of effort into the name
if it's not exactly so we could we could just say add song and it returns a new song Searcher or just add don't even
have to say song uh but it wouldn't be static method be no because it has to have access to the current list of songs
right right right right of course so this no no no no no we're we're we're saying to the existing song Searcher give me
a new song Searcher with all the stuff you've got plus this one so it's just like you were concatenating no no song
Searcher equals song Searcher but the the the field not the class right no no replace the existing line oh change the
change the S on the right side of the Declaration make that lowercase change the method name to add oh because we're
holding I didn't yeah yes we already have it right it's and in a sense it's a type of concatenation right you would say
string equals string plus string here we're saying song Searcher equals song Searcher concatenate song yeah I was my my
brain was thinking son was the local variable but right yeah yeah weird brain y um oops not that y now verogs are just
the ones I would say just the one okay um what I would say is return this and it will and it should fail in the same way
let's find out or in a different way actually I'm not sure o somebody else broke right because we returned that's
interesting I wouldn't have expected it to be empty uh oh of course if this one would be empty because we created it
empty and so that's the only thing that ever existed right so we now broken both which is fine because that should that
should have been expected because we were when we instantiating it we were instantiating it uh with with nothing and the
ad does nothing and so therefore go oh I'm in the T in no I'm looking at the wrong what are you looking for I was trying
to see where where that where that creation is that's an Searcher yes here we're putting no songs though that's private
we're calling it through this right but we're we're doing the nothing okay so and and so what we could do is instead of
returning this we could get the first test to pass by saying song and now the first test will pass but the second test
should fail in the same way it did before you guys it still in the will yeah and it only remembers the last one because
we're not handing it the about right and so now we can pull the songs out of so the song Searcher knows the songs it
already has we can pull those out sorry I was distracted by shortcuts what was that again um so before so basically line
37 and a half we can pull out all of the values oh um this will be a bit trickier because we'll have to flatten map map
and we want values and so that returns a collection map uh and let's see what is how does flat map work here um what
does flat map take what are the parameters so it Maps a list of song to a stream of song oh okay so we can just say um
uh we can just do s and then an arrow yeah or songs in an arrow whatever um and then we can do s do stream I think
that's what we want uh and then we need to list you can just say to list oh although we're probably going to do it to an
array so let's do it to an array uh but not that one we want the one that takes uh a parameter because we want the right
type this one yeah and uh we need to say the type we want is song is song song and then uh I think open square bracket
zero Clos square bracket or is it just new song without the zero I always forget uh drop the zero just do open bracket
and then I think there's a better way I haven't done this in a while um I think we didn't just want to open closed curly
braces no square brackets yeah H that's not quite right how does that work uh let's do it without that and let let
intellig help us so just remove the parameter totally we'll cast it to to a song array and let uh so just create delete
the whole parameter um assign it so assign this song and that will require a cast so let that uh and then let's help int
let's have intell uh help us further uh no that's not going to help us no that's not going to help us either um well
let's not worry about it too much uh we can also take the this s. stream and that can be shortened to the method mean
you can either have intellig do it or you can type it I was trying to have intellig do it but oh then unselect it
because otherwise it's not going to help you so you want to be on the orange orange so you can just do Alt Enter you
don't I was gonna ask you is is the Alt Enter is the light bulb ah got it Alt Enter is always the light bulb yes oh uh
while we have a stream we could conat um not sure how how would we do that uh but I thought we were saying we had to
reinstantiate the song Searcher we do but it's EAS but so either we can do uh song Comma Song array I think that works
for VAR ARS I use VAR ORS so infrequently I forget the syntax um or we could Stream let's just let's just do it this way
and we can we can always refactor refactor later okay so uh when we call create song Searcher we want to pass in um I
think we can do song H songs let's see if that works if not is it going to change the order the order well order doesn't
matter it doesn't you certain it ah got it I mean does order matter I don't think I don't think actually order should
matter no why is it complaining uh because we probably can't way um so uh what we can do is uh we can concatenate that
and just return song so songs um yeah and that and then we can just do the stream Dock and cat so before we do the the
two array uh oh in here yeah so save save everything from there so basically um save everything after the FL from from
after the flat map so where where the cursor is up to and I don't do dot so select sorry let me give you more precise
instructions uh select from where you are to theme songs theme to songs map so go select up no no no not with that all
right select up select from theme songs map through flat map yes okay subract that to a variable stream uh and so what
we want to do is um stream. concat so put in front sorry put in front of Right Where the cursor was so in front of song
stream stream. concat uppercase s oh so we're calling a method that's what was it it was uh that yep and uh as the
second parameter after song stream it'll be stream of song and then that'll get converted to an array all right and then
just delete that dot that array there's probably a better way to do this um but again this code is not going to live for
very long so I'm not terribly concerned you can just do a reformat if you want I tried it didn't really like it but I'll
try again is it command Al L yeah yeah it's that lined up the concav with it toay all right it's it it this is this is
the problem with VAR args is VAR args is an array and once you start having arrays and collection classes mixed together
you get this kind of ugliness um and this is why I tend towards like VAR args serve their usefulness and then I I tend
to to migrate away from them because they start being annoying in exactly this way all right let's run our tests and we
think it will pass other than the order right the order might might throw things saying what's it saying I can't uh can
you have the line wrap oh yeah it's on the right all the way on the right there what uh it may not be able to do it
because it couldn't create that that object um that's fine uh so we'll just do way uh who wasn't able to create the
right object um so when it creates an array there you can't cast arrays um so we need to just do a uh two array with a
specific type oh um and so the way we'll do that is uh put in there song open close square new and then we can remove
the cast from the front of um I'm a little disappointed that intellig didn't suggest using uh because I knew we had to
create a new song array that was basically empty um I just don't use arrays a lot so I forgot the syntax um and the
method handle is is uh actually the easiest way to do that but I'm a little disappointed that intellig didn't suggest
that but hey here we go ship it we've got some factoring that we'll probably want to do but we have we'd have to decide
how much uh is is worth it and how much we're going to throw away because this immutable song Searcher where we add
songs by doing it this way I don't know I I don't necessarily see that as our long-term solution right commit text what
are you songs yeah and overloaded might might be useful um but we got it working so we'll yeah I'm definitely feeling
the uh late afternoon yes energy level I thought I thought we'd get it done in 20 minutes but it took 40 minutes so
because stuff takes longer than you think yeah it's all good yeah I I wish VAR args were much more compa able with
Collections and streams or streams one of the two that would be that would be nice but that's that's backwards
compatibility for you all right um cool that's all for today right so uh we're doing our crack of dawn tomorrow yes so
tomorrow um uh 9:00 amm Pacific which is what did I say 9 plus 8 17 5 500 PM UTC is that right um uh and we'll have a
strict two hour limit which will actually probably be a good idea yeah that one's a strict one because I have to go yeah
see my son perform yes so 4 am for you ouch thank you profess uh well I mean eventually we we're going to want to stuff
store stuff in a database the question is how and what that I think is we'll have to figure out but not today all right
folks thanks a lot for hanging with us on a on a holiday weekend um and as always you know where to find find us on the
Discord so join us there otherwise we will see you tomorrow for episode seven have a great rest of whatever day is left
for you or uh have a good sleep if F the end of day take care bye
