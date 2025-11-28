# JitterTed's TDD Game： Online - Ep# 8： ＂WebSockets and HTMX＂ (Java, Spring, Hexagonal, DDD)

**Video URL:** https://www.youtube.com/watch?v=5jt0gQD-S6g

---

## Transcript

hello folks welcome to uh yet another stream on putting my tdd game that thing uh putting it online making an online
version so we're making progress um sometimes it just feels slow like why am I not done yet um but we're getting there
uh so and look at this um so what I'm working on right now so this is the again for those of you who are relatively new
uh this is the second version of my mockup um there will be further iterations of it um and what we're working on now is
the game has been created you have joined the game and now you're waiting for other players to join before you start the
game so we're sort of in basically building this um right now I'm kind of thinking of it as a modal dialogue where uh
you'll see uh information about U maybe a little bit about the you know what the game was called if it had a name and
then um basically who's that code um so we were looking at uh when you get to the in progress game page um which is
currently at the game Endo although we know pretty soon we're going to need um um uh some identifier for games uh I
right now game itself as an entity does not have an identifier um it's also an aggregate uh route um so uh we'll
probably need to put an a real ID in there at some point but for now we do have a unique identifier uh which is is this
string here that's the handle of the game um and I think I decided I was going to stick with that for for a while um
what we need is uh to add that as a path parameter um so when we redirect from I'm joining this game that becomes part
of the the path parameter so yeah so let's go and and uh tests uh the reason I'd want another identifier is one that's
more database uh identifiers that are um although it's changing now like you know now you can have u a uu ID as as an
identifier as a primary key column uh and databases are getting much better at indexing that um the other thing is this
game handle is actually not 100% I have to look at the spec but I don't think it's it's 100% guaranteed to be globally
unique um because there is a limited number of words that it uses um so it has sort of an adjective and and and an
animal name uh and then a number I don't believe it is uh meant to be 100% unique in fact I'm pretty sure it's not I'll
have to look at the the spec um the idea is that it's it's human readable I'm okay with with repeti with sort of another
game that happens to have the same name if it's you know one uh different from one that was a long time ago um but that'
s that's mainly wise uh and then if you get into foreign key situations uh then it's a lot easier to just use a uh an
internal ID identifier hey key well so when I use the word globally unique I use I I mean it in terms of globally unique
in my database um but I'm but there's no guarant uh there's no uh like a a uuid is guaranteed to be unique anywhere uh
but also certainly in your database um whereas something that's randomly generating things random numbers are are you
know especially Pito random it could be repeated uh un unintentionally so um I mean I'll probably do some checking
anyway so that when I create it I do a when I try to save it um or do a search to make sure it's not already in there uh
but again it's sort of not my goal for for having this readable name was to be readable um as well as unique among
currently available games to to uh let me click here for a second and click that okay so um for now I'm I'm just going
to use the the the handle uh what are we failing uh yes we're failing here but um I think I want to take a step back
from here so when you join um I guess technically this this doesn't have to be a request pram this could be a path pram
uh I'm not going to worry about that right now uh what I do want though is I want to redirect where this goes to
whatever the the handle was so let's go and uh modify that test that would be test uh and what we'd like is it to not
game uh that matches this this game handle uh in fact let's pull this out into a variable just to make it clear is uh so
this will uh in fact let me go put uh so you all probably can't hear it or hopefully you can't hear it um but they're
doing a lot of tree trimming uh which involves a lot of noisy chainsaws and uh tree munchers and stuff and it's been
driving me crazy all test and we'll go back here and then uh so this will fail cuz we're not using all and that's uh as
expected uh we could hardcode this but there's no point in that we'll just tack on game handle um there is sort of an
assumption here that uh the game handle exists um this join will blow up if the game handle does not exist yeah so
that'll that'll blow up we probably want a better way to handle fine uh okay so that's that's fine uh so Jonas asks how
do you deal with having layouts header content footer don't want to manually import header footer each file um I mean I
don't do a lot with fragments but fragments should be what you want um so you'd have a fragment for the header a
fragment for the footer uh you there is also way again I don't do it that there's yeah I mean I think fragments would
would be fine have the fragment be more of a container and then the content is then provided by fragment um I I'm I'm
definitely not an expert in that area I would I would if you don't already have it uh whim de blau's book on um taming
time Leaf is probably my go-to for for that kind of stuff um but yeah I don't I don't I haven't done a lot with time
Leaf where I've got a lot of pages that require the same kind of thing so I haven't I haven't that trying to think of
the yeah I don't I don't use I barely use fragments and I don't use much with in the way of the the layout stuff um but
that's also a good okay so this test passes we'll do a commit um oh my uh we haven't done a commit in a while that's bad
things yeah I think we pretty much just rename of game View to game lob view stuff commit yeah I did a couple of updates
to to nightbot so didn't sound like so cuz um he was taking credit for for all my work noticed uh all right so that's
working so now we can go back to here uh turn this off uh and this now fails um so what we want is we want this uh to be
the uh game handle so we're going to need to pass that in here uh but I think we're first actually going to need to go
to the MBC test Pass unless I missed passes um spring boot 330 was released today and I was going to put on the list to
to upgrade to that I used I tried the um release candidates they worked fine so um I'll probably do that at some point
you yeah some professors um one thing I've learned is that they are uh not usually incentivized to be good teachers um
that's often not why they get hired um it's unfortunate uh I know here in the US there's some really good teachers uh
but there also a lot of mediocre teachers and then there's a lot of those who see teaching as something they have to do
because they really want to just do research or something else um at least in the US that's the nature of of the
academic industrial complex as it were all right so we're going to need to um you weren't supposed to make that stream
let me click here there we so I think I want to start at this end point well basically uh we'll probably need to
autowire the game store to put in um I'm going to do this second so I'm going to leave this here uh I know I'm going to
have to fix this this test um because I know I'm going to have to add in the game handle here um so this should still
pass because basically it's going to be ignored pass okay and uh intellig is saying that uh we should create a path
variable that now if you know spring MVC if you know spring spring boot if you know basically if you know about it you
know that it will take to this path pram variable name here so this is a variable name here and it needs to match that
by default it will use the variable name the problem with using the variable name is if you rename the variable but you
don't rename this um you've got a problem uh I don't like having that magic connection between the two so I always add
the string there that way it's really clear what uh tests uh right I didn't do this as intellig did not do this as a
signature change man um but that's okay we're only we only have it in one place and actually in this case we do want
that uh in fact let's pull it out um now this test will still not let's run the io free tests and so this one fails
again of course as expected uh because we've hardcoded handle right here uh so we should be able to now change the test
sorry change the code so that the test fails differently um and this is something I do differently than than others do
and whether it's better or not it works for me um and so by changing this to this variable this test will still fail uh
the handle will match um but the player views will still be empty and then we can go and fix that so let's go fix this
part first all right so now we get the proper handle uh but now we got to fix the player views and the player views is
going to have to come from um somewhere uh right now there's nowhere where it can come from uh well it can come from the
game store but uh the test um well actually I already put stuff in there so never mind it actually should work uh so now
we just just so instead of an empty list uh let's pull this out into a variable this is our player views and so instead
of an empty list will'll go and grab from the game handle and uh Cody seems to have dreamed up and hallucinated some
methods um Cody should know better I don't use players uh except it's not uh so we find by handle what do we get from
that uh we have to do a get first because it's an optional so we're then so let's do that so find by handle gives us an
optional uh we'll throw and we'll fix fix that um we get the players we stream those we map except again Cody is
hallucinating a method that doesn't exist um we want to map uh player case actually in this case I have no idea what
what player view is it's just a record uh and it takes the player's name and that's all we have in the view um oh I know
where it hallucinated the it didn't hallucinate the from it got confused I saw the from over here uh is is my take uh
because this does return a list of player views so in fact um this method now remember I actually wanted to move over
into player view as a static method uh so that this would then work um but this takes actually a list of players uh so
we this and say this is a list of players uh and then this would be the so let's move this over uh would you like to
make this method from static and then move yes please okay I every time I do this I forget uh that this is a bug uh we'
ve reached our quer for the stream this has been a long-standing one um I consider it a bug I don't know if intell
considers it a bug I have to go look to see if I ever filed it I don't believe I did um so notice what happened said
there's no would you like to make method from static and then move and then move then move so my expectation based on
the and then move is yes make it static and then it would present me with move non-static uh helped me make it static
but then then provide the the and then move fart uh so we want to move this to player View and we'll go ahead and
refactor becomes player see I'm just I'm just thinking about like what what was going on behind the scenes with Cody
that it that it suggested that yeah it predicted the future but that's not helpful if if it doesn't get me to the Future
on its so we got player view we've got uh game and if we look at game we've got player view name that's the only thing
we currently have in there so Blue uh you need to stop doing and this is who's window uh actually I need to open up an
incognito window or private window uh Local yellow and I need to stop that uh so we see there's a player count of one so
we game and we see that that they're both there now because we're not using websockets yet um if we uh look at blue
screen of course we don't see any see any different um so that will be our I think our first I think we're here I think
we're at the point where now we can start uh incorporating HTM usage um so there are two things that I want to happen
when uh when that other player more so what I want to happen is um well certainly this should appear is basically a
message so update this but also a message that hey uh yellow yellow nickname just joined um not sure what I want to show
yellow nothing uh do I want to show sort of all the notifications from when the game started or do I want to just show
uh basically what's happened since you've joined I'm not sure the past is interesting yet so I think it'll just be show
um basically show just what's new since you joined so uh so when yellow joins they won't see any notifications um but
blue will see both yellow pop up uh as well as a notification saying yellow joined so plan uh and then at some point uh
I need um it might also be close to time uh and maybe I'll do that at the end of today's towards the end of today's
session production uh oh time stamp of those notifications would be interesting yes enough trying to find I was just
reading another uh uh post about time zones and stuff and it's just it's just such a it's such a such a mess um I
generally don't like relative time but in this case it might be useful um so for example uh yellow joined 3 minutes ago
uh the downside to that is once time goes by that's out of date and that's one of the problems with relative time um so
never mind I'm not going to use relative time uh it will show the time for now in whatever is convenient but eventually
it'll show the time in um either based on your browser Lo local or um I will also be adding things like what time zone
are you in or what time zone should we think you're in uh to your profile So eventually the member profile will grow uh
to have things like besides your preferred name um and other stuff it'll be what time zone are you right yeah it'll
definitely store it in UTC I don't I mean if you want to select UTC as your time zone that's totally fine uh but I'm not
going to force UTC on folks I'm really good at doing the trans but that's cuz I do it every day and I still get it wrong
sometimes all right so this means that what we want is instead of uh this kind of of what I sort of think is a is a as a
push model uh this is a very I guess it's a static it's a it's sort of the the static model right so it's a static page
we generate it um we generate it when you ask for it um but once you've requested it it's it's by definition out of date
um so what we want is to use HTM x uh the first thing htx should do when it loads specifically when it loads this UL is
to basically ask for the players um one thing that uh working with especially HTM X has has sort of brought back for me
is this this um very component based things and in fact you know you can now create your own HTML components I mean
depending on how complex they are that's not a lot of JavaScript to write um I may eventually write my own web
components uh but not any team not any time soon so but we want to think about why I'll be tempting to say oh let's just
you know load the reload the whole div right which was basically this entire box um you want to think we want to think
about it a bit more Gran in a um because what we want is basically this area of who's here uh and then this area of time
uh first I think the notifications one would actually be more interesting because that's going to happen more frequently
because you're going to get connects and then you're going to get disconnects and then reconnects um so I think uh we'll
we'll do this one so what we want is we want a websocket connection right up front uh so I'm going to have to go is what
plugin what plugins are updated oh I'll ignore those for I forgot the name of the tag what is the name of the tag oh it'
s an extension right uh it's not it's no longer an HX DWS um which has hasn't been true for a while so what I want to do
is uh let's now um which means I probably want to pull uh actually let's let's do this let's go to um hmx you've been
this and we'll go open you I can close no I'll leave you open too come on on there you are so let's go to the top and
put in that extension uh except they haven't updated this because this is no longer the case it uses the extension yeah
it was already deprecated but I guess in hmx 2.0 which is actually now out in beta um they'll make it official so let's
grab button is there really no copy button here Sor I don't know what Cody's thinking here but it's not one even though
we'll eventually go to web jars just because that's easier to manage uh from a a spring Boot and deployment model this
will get us up and um I'm also probably so I am to be honest I'm a little undecided about deplo about sort of using
Tailwind in my final version um I like the initial experience of playing around with Tailwind uh but since I don't have
a good component mechanism um there ends up being a lot of repetition uh I may combine the two so I won't put them as
classes directly on the I won't put the raw Tailwind classes directly on the elements but but pull them together into a
separate CSS file um but for now I'll leave it as as Tailwind all right so we've got our HTM X we've got our websocket
extension and now what we need is somewhere um we could probably just connect whenever when the page loads I think that'
s so where do we want to connect to uh we'd like to connect to what my endpoint be it could just be WS it could be if uh
I'm going to need to keep track to so I probably want to connect to something like game game handle that uh we actually
have that information H oh I guess I can just do a th in front of it so th and then we basically do something like work
I know uh before next the my next stream or maybe in my next stream um I have to get some testing in place for for the
output of the templates the spring based testing because I don't need this to go through spring I just need to hand
model uh yes that's correct that the websocket would connect when you join the game um because currently the lobby uh I
am not planning on the Lobby being websocket based anytime soon so once you connect to the game this is the page you
will stay on forever at least during the game um once the game starts the the dialogue goes away so pretty much just
like the mockup the dialogue that we saw will be over here but the background of the game will be there um and then once
the game is started you're now on on the game page you haven't left it it's just stuff disappear appears that's my
current thinking uh okay so we have that this connects uh let's so we'll go host a inspect and we can look at um so
that's all I needed to know so the websocket connected um it did not work cuz there is no place for the websocket to
connect to so we probably see some console errors and indeed we do uh that is not surprising um so it tried to connect
to Local Host game the game handle websocket um but that's what I expected I don't know if that's what yall expected but
that totally works for me uh let's go off this page because I don't want to try and connect anymore okay um so what next
uh so we connect to the who's feeling like a sequence diagram sequence I find it interesting that sequence is the first
um I don't know what order it's it's it's using for ordering these options but but it's interesting that that's first uh
so we're going to say sequence it it might be the most often used but then why is use case second I I do not believe
that use case is the second most widely used uh I see a lot of sequence diagrams uh I don't see enough of them but I see
I see a lot of them all right um so what we want is I don't want Auto do I want Auto numbering yeah I figure if you've
used plant uml you have I think I feel like it's likely that you've either used sequence or you've used Class but even
class I don't think is that popular um so I think sequence is probably the most most uh most common um for me sequin and
state machines are are my main main thing okay um so player no yes they are player at player uh so what am I modeling
here I'm modeling the um browser server web socket connect oh look Cody's going to um yeah but that's not terribly
useful what else you got ideas um this is yes correct but I don't really care uh what I want is um once you update um
what do I want to update I want to update the uh what do I call it players joined the heck did I call Cody's reading
some other files isn't it um and I decided it would not load the history of notif did I decide that what did I decide uh
I think right now that's a nice to have right I I need to I need to keep focused like what's the minimum I need yes it
would be nice to know what happened before I joined um but that is not required than uh I'm going to do this in it these
aren't really sequence diagrams I I'm not sure what to call it um yes there's a sense of sequence but the things that
are I'm talking to are uh not really objects here here's what I mean so there's browser to server that's fine um but the
way I'm thinking about this um which of course is in a sequence diagram structure so I may have to do that but it's
basically I'm targeting uh a specific um actually I'm just going to call it who here component the fact that it's an
uned list is an implementation detail um I don't think I want Auto number no it's not an actor I mean I guess it's an
actor name yeah it is it is very much a uh oh I guess there's our order for why it was in that order that must be
because that's the way plant uml has it ordered up here uh so um technically it's a boundary but I don't really care
about that uh I'm just and uh participants browser um cody getting Cody's getting cocky it's like oh I know what you
want um so we've got the who here and we've so can I Nest my participants how would that um all right I don't want to I
don't want to Rabbit Hole too much or rat hole um actually this is uh player one actor and then uh maybe I don't
introduce them just yet server um but player two is an actor so no let's put it up there uh so player two does a connect
and what the server Target uh who here with an updated list of players in the game uh let's be specific now so it's
basically um player one player two here addition it targets the to I guess technically uh if this is the case then uh
this is player one has joined so you see a notification that you've joined in addition to seeing you in the list um at
some point I can filter it out so you don't see notifications that you caused um but I I think this is um I kind of like
the the action being uppercase and then I don't really need the has meh you can submit a PR it um I think that's what I
want this was I I needed this to sort of get out there what what kind of um uh because what what we're doing is
something happens I need to broadcast over the websocket so that goes to everybody who's connected um and that's why I'm
not targeting any specific players in a sense I'm not targeting any specific player just yet when we're in the game
that's going to be a totally different situation because now I I'm going to need to Target different players differently
which is going to be interesting okay so that means now I can I can move a little bit forward in um in um we're going to
want application layer to trigger um to trigger these things so maybe let's let's go a step further uh player one
websocket connect so how do I identify a websocket connect or more precisely how do I associate a websocket connect with
a well I'm wondering do I need to to transmit that from the browser or can I trust or does websocket now I got to look
at the spring stuff um these components are browser side components uh if I could color them differently that might as
boundary so let's take a look at the where is that's not it I want the that yeah I didn't want to color the messages I
actually wanted to color the um the headers I guess um but then I realized I don't want to color them just the shape is
fine so let's see so when we connect uh where is the connect stuff so that's the T this part um so that is after
connection established we get a web socket session that I assume it's a standard Docks so let's go to uh do spring um
not spring data I think we just want spring websocket so websocket I guess technically this is not web MBC so Spring
websocket Security so yeah I did the the color after that did um reuse the same authentication is found in HB request
when this second connection is made so that's good uh if using Spring Security the principal on the Ser request is
overridden automatic okay uh all setup is okay um that's all config I'm I think I'm all already those this does not look
quite simple to me I really wish like documentation writers would not use that phrase it might be straightforward but it
is not simple because this ain't simple um what I want to know principal when the websocket connects so that's the
spring messaging abstraction I don't think I'm using the abstraction yeah so we got the principle through um uh where
was it uh through another get mapping so I can put the principal here and spring when uh when I session I don't know oh
never mind there it that all right that's all I need to know Hallelujah all right uh so now we can go back here and we
can basically say um sorry go back here uh so we know who they are so when basically this web SOA connect happens um it
carries uh uh security principle um which is exactly what we need because then we can go look it up in our uh member
store and and get that information well on the flip side uh five minutes of looking at the actual object can save me
hours of reading documentation that doesn't want um this is something that uh I do need to once I once I finish this is
uh uh extract this into to my websocket tutorial uh okay great so now when we connect we know who you are we can
associate that um probably just want to load that up um yeah this is not a traditional sequence diagram usually you see
sequence diagrams where uh the the things at the top are actual classes um this is more uh more about a sort of a a
messaging you know which messages go where um but I find them really really handy to figure out especially when it's not
just sort of back and forth between two things it's it's like go here and then broadcast out here and then sometimes get
stuff from different places so um any tool that that sort of forces you to put useful um this is one of those where
where and this this is just a a hard problem to solve this is one of those cases where it's the answer to my query about
where is the principle is is that a spring security question or is that a spring framework question and it's like yes
it's both and that's why it's like where do I look um but all right so now we've got that figured out uh so when um when
we get the page we're pretty much going to do nothing um cuz we're not going to need to do any of this uh unless I
decide that I kind of want to paint the game background in sort of onef swoop um uh or let the websocket uh populate
yeah yeah I always think it's worth drawing a diagram plant uml is convenient because it's here and it did exactly what
I needed it to do um I have to look to see I haven't seen anybody do it yet now I'm going to go look because of course
we're all about tangents uh so there's a cal calad dra integration um but there is not integration with my preferred
whiteboard system which is tldr um but the excal draw uh integration is interesting um but has not been updated in quite
some time which is too bad cuz what I'd love is I'd love an I'd love integration right all all uh all editors eventually
accumulate behavior until they're also pull in your email um jet brains intellig hasn't quite reached that yet but um
but TL draw is my my preferred no basically excal draw is very similar to to TL draw in fact most draw um I use excal
draw occasionally so what's nice is basically this the it's the idea of sort of a an infinite canvas um so you can
basically put everything into one and then it's like everything uh I I don't like excal there's some aspects of the
usability of excal draw that that I don't like uh there's I find T TL draw to be a bit smoother in some ways although I
do like um there's something it's like I want the best of both that's the problem all right um so we're not going to do
this anymore instead what we what's the first thing we want to do then is handy uh is we'd like to take care of scenario
so you connect and the websocket updates the who's connected uh um yeah same same same here astd uh cuz especially if
you're on a team um you don't want to have to go far to figure out where's the diagram um you want it right right in
place so what would the test for this B uh upon connect we get a web s web session web socket session um so that's
technical uh but at some point we register them with so somewhere in the application layer they're going to connect
they're going to interesting so there's there's sort of two things happening there's the player has joined the game the
player has joined the game so that's this game but at this point we have no idea if they've so this join is sort of a
logical join like you have joined the game I don't know if you're if you're paying attention I don't know if your
browser's working I don't know if you're still connected to my server uh but you're part of the game you can go away and
come back uh and that's fine so the websocket management is is separate from and the session manage so there session
management and then there's game management um under normal circumstances it will happen right away right so you we got
here by coming from the endpoint join so let's maybe add this to our uh to our sequence uh so we've got player one uh
this goes to what is it uh game Joiner blue uh and it's much higher there um going to have to change server server is no
longer server server is manager so the player one um post to uh when I write the class I I'll add that uh so the first
thing that happens um maybe I want to turn do I want to turn on the auto numbering what does Joiner uh sends back to
player one uh redirect uh is it session management implied in websocket manager uh it might be but I I that um so let's
actually now name this can I rename socket uh uh click on the post button click on the join button which does a post so
that's this um game Joiner redirect but actually before it does that uh what it does is Joins controller although it's
not a controller it's boundary controller entity so this is basically our application layer uh this is actually not our
uh peach uh light orange dang what is the color light all right I'll stick it as orange for now uh this is actually um
uh blue CU technically this is our adapter right now I'm just going to say particip oh that's terrible blue uh okay so
you click the button that sends uh to the that sends to the controller I'm joining the game we then uh tell uh the
application layer that the player joined the game um at this point they have not joined the websocket session um when we
redirect them then they connect to the websocket so that happens here whereas they are part of the game here and we
persist that so this is permanent in a sense uh this is transitory so you can disconnect and connect but you are still
part of the game that's why I'm sort of think about this this is the the logical part of the game this is sort of the
physical check that the player who joined the websocket who connected with the and there's some other thoughts that I
now have and again this is probably getting into the to the nice to have um so the only reason I might check this is
without point and I'll be like who are you why are you here you're in the wrong place um but again that's so I think I I
need that but I think that's a nice to have uh what's more what's more interesting is there's actually two two as two uh
two pieces of information that I that I have per player one is hey yellow's joined but yet versus um because once they
once they join and it should be pretty much right away but it could be they got disconnected we were still expecting
them so maybe they had some they had some trouble but there really is is sort of two aspects but what this is connected
so there's joined and there's connected and those are two different things um they will probably happen very close in
time uh but they are they are yeah I'm I'm about to do that connected all right Jonas have a good night so hand hand
over your shift yep um so uh okay all okay all right so there's joining a game and game so you could potentially join
multiple uh so you can join multiple games but you may only need or want to be connected to one of them why you do that
maybe you're facilitating multiple games um yeah so so here's where it gets uh this might be needed for my minimal
playable version um you could be connected to a game but player I have to say the the the um some of the terminology
overlap between this and ensembl uh is really interesting oops uh webop manager should be connected I don't think the
game cares connected yeah so there's there's are like timing out that I guess the question is is what happens if you
time do we well so so remember um this online version the the initial playable version is not enforcing anything so if
you go away anybody could do anything at any time um it it's again it's like it's as if you're all sitting around the
table and somebody walks off it's not like you have to wait for them to get back before you can physically do anything
you can move cards around you can throw them on the floor whatever uh and that's the initial idea for this that I don't
want to enforce those kinds of things so that I don't on the one hand because it's more work and on the other hand so I
all uh to igi's point is like my assumption also with this initial version is that you are connected over some kind of
uh video conferencing so you know if somebody's gone um so my so because uh my assumption is you're playing a game as a
group um I am not supporting any kind of communication between folks you're going to use a zoom or Google meet or
something like that um so that you can talk to each other and discuss and say okay your turn and then then you go uh so
those are not those are basically not at all something I care about this is basic again sort of like my and what I also
need to sort of keep in mind is my main goal is I want folks to be able to play this remotely uh as if you basically
virtually um because you can do it like I I've done did it the other day uh I can have somebody who hosts it um but
otherwise you're still communicating and talking conferencing um yes so I think right now uh it's totally the websocket
session manager's concern that people are connected or not because it's merely a technical issue logically who cares um
the only thing you can't do that you could do if you were physically in the same place is I can't play cards for you or
move your Pawn Yeah Yeah so I think right now game y feel like I want to put that um I'm putting it here because I don't
basically for folks who okay uh I'm going to take a break when we come back uh we'll see what we've clarified um I think
we uh I think we've now that we've differentiated between this I think we can now start looking at the the player Joins
game application uh and see how we'd fit the the web socket in all right astd have a good night thanks for hanging out
thanks for your assistance and uh I'll see you after this coffee break uh except for astd who I won't see be right um so
that means uh do I actually want so this is the application layer uh when they join and I save that they've joined do I
want to broadcast an connect so what that would mean is there would be two things here there's um this would be more
like uh where is it uh whoops sound like that um let's see so what would the what the SP2 look like uh doesn't matter
what the the colors are but that's that's the idea um so when they join we got an event when they connect we get another
event um it's a little extra work uh but I think from a troubleshooting standpoint it's going to useful uh oh hey for
for not found um funny you should ask uh so two ways to figure that out um it's generally uh it's it's what's called
file Scopes and file coloring um so one thing you could look at is uh sui had submitted a PR that I had merged that
provide the coloring um so you could look at that commit uh to see exactly what um what was added uh the quick answer is
basically um some Scopes were defined for each sort of layer uh and then file colors was defined to basically say what
colors are those uh you could probably even just pull those into your own project if you want to just rename um pretty
much defining the Scopes is going to be different because um I also have a video on on how to do that so if you look at
YouTube you should be able to find it yes this repo is on GitHub um it is uh not technically open source um but it is
Source available so if you just want to look at repo there that's what I wanted by the way uh for those of you here
watching on the stream you probably don't need to do this um but if you're interested in uh being updated when I start
providing early access to the game and or when I fully launched the game you can uh go to that link and sign up uh for
uh a certainly a low volume mailing list um although I might also sort of uh use that list to to talk about progress um
on on more than just a yeah I mean I'm I'm I'm not terribly cons like the source available um yes technically you you
can't borrow from it uh you could go to ensembl it's it is the same thing um my main concern about the The Source
available versus open source is I don't want somebody taking the game and basically launching their yeah so it does mean
you want you know I I actually think uh the recommendation to not commit anything under idea is not quite true anymore
because there is useful stuff under there um but I agree that mostly historical reasons it is not easy to figure out
what's what should be yeah so I think uh uh so notification um uh actually I want and we probably want some some kind of
uh so hypothetically speaking I would send them a cease and desist because they would be violating uh copyright um if
they were a big company that had but you know that's the way it is in in anything it's like even if I didn't put any
license on it it's by default copyrighted that hasn't prevented um AI from using it as training data which is um all
right so I think this is this is what I want um the wording I'm not happy with but I'll fix the wording later okay so uh
which event do I want to do first joined uh so let's do a commit because things it's amazing how much effort like just
this is is taking like we haven't we haven't started the game yet episodes uh yes I am using time Leaf uh in fact this
thing on the left is a Time Leaf template um and I I just added HTM X websocket support so we can start working on on
this because this is all see um okay so what I want is let's let's do just the notifications part so we're going to
focus on on want is this um a container would help so let's um we'll make we'll make it a div uh we'll give it an ID and
this is uh notification container uh so it's going to be the target of a response from a websocket uh so I don't think I
need else yeah I wish um I wish fleet was better there all have to say to that uh okay so no no the expand select inside
HTML does not work the way I wanted to and I don't know how to fix it okay so uh do we want these events to be top
latest on the top or latest on the bottom we certainly wanted to expand when we get new events right so it'll expand um
so this is this is always interesting it's like do you treat it like uh like our our chat up here right so latest is at
the bottom or do you treat it like um social media where the latest is at the thoughts I kind of like at the top but if
somebody has a strong opinion let me know uh so what we're going to want to do is when we uh Target this we're going to
want to do uh before is it after start I always docks oh I'll have to open up um so it's not in HTML uh is it insert the
response before the first child of the target element so okay um I think I could just put that in here let's put that on
there okay great okay so we know how to Target it we have an ID we know uh how the swap is going to work it's going to
be after begin so it'll go right here uh we know what it's going to contain it's going to contain a paragraph element um
and that happens upon join so we still need a websocket uh session manager and if anybody has a better name that so we'
ll want that to happen basically once we save the broadcast um do I want to do inside out here or outside in let's do
outside in uh so now let's go to uh and this is um this is going to be pretty much um well let's set up the
configuration broadcaster uh so our endpoint what did we say it was um oh huh okay this is going to be interesting um
cuz I thought I would have the websocket that because that makes I don't even how you how how would you would you set up
oh I don't even know if I could do that I mean there's probably a way but that seems to go against the grain of having a
single websocket uh Handler Al righty then uh so we don't do name websocket uh and then um the Handler the session
manager will out so that's going to be our our uh and that's okay because we know who you are because we get the
principle when you connect um we don't know which game you're connecting H so registry hand add Handler what does so I
can specify multiple paths but that that so this is a problem if you want want to connect to multiple games so when you
connect so there are some handshake headers but that's not enough I don't socket so let's see um let's look at the API
uh so that's handle text h um so when the browser connects it's connecting over a basically a global URL of gamws what I
need to know is I already know who you are but I don't know which game you're joining you're connecting to because you
could have joined multiple games uh as an observer and now you're connecting and so which one are you looking at and I
need to know that in the web socket session manager because when I broadcast I'm broadcasting based on the connect to so
no I can't that's the thing is I I can't see a way to add it to the websocket URL because I don't see a way to register
handlers in some general way because it looks like it has to be hardcoded and this is config so this is a startup so I
don't have any of the games configured there is there there are no games when when config happens um and the docs aren't
helping uh and has no information it's just configure a websocket Handler at the specified URL path so I can pass
multiple paths uh but once I'm up and running I don't know how i' would be able to do that map Interceptor yeah that's
that's that's where I was I was going swegi like I think I might have to do um in a sense my own protocol so this is
kind of the downside of websockets you have to basically decide on your own almost everything protocol um uh so here are
the like it basically adds a Handler adds an one so it basically creates a new Handler yeah I don't think I'd want to
create a new Handler for for h one yeah all fun um so that means when we when this so how do I send stuff the um so quit
go away let's go look at HTM X again um websocket where is the docs for that uh docs websockets websocket extension so
it's a WS send okay so we send hi here here here we are we're uh basically game right game handle at I need to submit
another pull request or issue because it says in the example above the form uses a WS send attribute do you see a WS
send attribute don't uh 404 I'm using the library directly because uh whims um Library um when message has just been
received so we really want an event uh after so uh whims um Library uh is all about um a a Tim Leaf dialect uh that that
works well with with HTM X um uh and it's almost exclusively about using uh HTM X for your typical restful stuff whereas
I'm using it um for websockets so uh last I looked I don't think he had any any support for basically for for websockets
or if it was it was it was pretty and you know this is sort of the problem with some of these libraries like um Thomas
Schuler has has some stuff in this area and the abstractions just don't don't fit my my mental model and so I'm I'm
going to end up writing my own my own Library especially around websockets because there's there's definitely some
higher level stuff that that I want regardless of actually the front end whether it's HTM X or or not um but spring
itself doesn't have the right abstractions for what I want I don't want a highlevel thing like stomp which you know is a
reasonable thing to do is to say I'm going to you know use stomp um but that requires then stomp to be supported on the
front end whereas so it's too sort of high level and then I can't use it with HTM X so there's nothing between sort of
the websocket Handler that I'm dealing with right now and something higher level at least from the spring boot side um
other than the Handler yeah react I mean then you're using you're not using rest and you're not using HTML generated on
the server so want so I don't want to do this on load I want to do this when the websocket connects so um so we want
when this event is triggered we would like to then do a w can we do a WS send or do I have to write HTML uh no it can be
a I forget how to do events the events were were I remember a little bit yes and I'm trying to remember how to um uh
where did I use events I know I use them here H all right let's see if I can re learn do I have events somewhere all
right let's go look at the reference uh that's just the reference that's not me okay so uh because it's the HX on that I
want yeah want so HX on and then the event uh the question is what I do as a a I think I might have to write some
JavaScript oh no um because I can I can do H HX on HTM x uh WS after connect the question is what do I do as a result of
that uh unless I use hyperscript which I Yeah so basically I want it'll be something like like this either the colon
version or the the Kebab case version um yeah yeah and that is what I was doing with with the audio is I was executing
JavaScript let's see yeah so basically I had um after message uh uh where the event was the websocket message and that
was set up here yeah so this was this was that that's how I did it but thank you for reminding me that we took that out
because we found a better way um so here we can do HX on hmx WS uh after connect and then call what whatever uh you know
handshake um and then basically say hey we're connecting to this connect uh I guess I don't ignore the connect I I want
to have I want to record that so one of the things I want to do from a troubleshooting when this thing is live
standpoint is I want to see all the details like your web socket connected I want to see that because then I expect
right after that uh uh join this game or connect to this game let's use the right terminology connect to game here's the
game and I want to see that um and then if I you get disconnected I want to see that uh so I want to see those sort of
lowlevel lowlevel events um yeah so I'll have to JavaScript cuz there Pro there is a way I could use hyperscript but I I
don't know I don't I don't feel like I want to get into get into that grab this actually I'll just grab the whole script
so uh so let's stick in the script up here um no we're not going to play horns um and this is uh after web socket
connects uh so that's the message I don't care about the message I just want the uh so we wanted the web sockets which
event is that's connecting uh that's open so this is the element that holds socket uh or we could get the socket wrapper
I'm not sure which I need but uh HX on open and this is after web socket connects that I don't know why it's trying to
do uh you um so do we want the socket or the socket wrapper the socket wrapper it exposes a few members sends a message
safely so it want uh and it persistent so it has a little send I don't think we want to use the from element so I think
we just want to send message and we just decide what our message is that seems simple enough uh so then we just say uh
event dot um wrapper and we'll do a console log um we actually want to say something here so what's our protocol going
to be going to do colon and then the game handle fascinating that's not what I want but uh so the question is how am I
going to inject the um it's probably easiest if I put um an so the game handle is here uh but that's easily injected div
uh I could submit a form from JavaScript CU what I'd really like then is when it loads uh when it when it connects form
then it could do a w send and submit itself um and I was thinking about this when in the back of my head uh one nice
little feature might be if I facilitating multiple games I might want to drop down to select other games without having
to switch to other browsers and so if I then expose that as a dropdown and it does the same thing uh then that would be
basically a free switcher as it were um but let's uh if we if we create a form that's just appear uh so this is going to
be our our selector um I don't need any classes what I need is an uh the event I copied um this send okay that was
really annoying and now it stops doing it okay like this this must be broken like I cuz I don't understand like the
there's no um I assume it's it's what we think it examples oh it's this example thank so it's going to send it to here
uh when uh so then what we want is we want uh an input hidden uh type is text um what do we want here uh the name and
the value so the name is going to be game handle and all right so let's let's try this out um so I've got that let's go
to our websocket Handler uh I'm just going to grab the now so the websocket configuration that's the uh except here I'm
not going to implement now and we are all right so what I want to check is connect upon WS open we submit this form and
we get this um which means we need to make sure that the configuration is set up right that's game WS so that's cool it
connects to this thing uh this thing is after connection established uh after Connection close this handles the incoming
message uh so basically this is where we should here happens blue we'll host a game now we'll join a game rude and uh
let's network uh oh I forgot to record this but shouldn't matter we should have seen something here um uh we were going
to take that out anyway uh although why does it have no such element um oh because we're not passing along on the path
okay we knew that wouldn't work not sure why it's uh how's this working at all wait join join yeah this should should
have come across I'm not sure what's going on there so let's look uh so we got join that's the request to the game I'm
not sure why it wasn't finding the game empty um oh probably because it's all in upgrade I'm not sure what's happening
here um there's a problem with trying to do something uh what's that's basically experimental in in a non-trivial
project uh let's instead of doing a this submit uh let's do an after websocket connects still not sure why uh this game
wasn't found because that's the correct time uh do we have the configuration set matter matter yeah so what I'm
concerned about is uh the websocket seems to be opening and then closing because the um yeah we may not have our socket
uh cuz we're not seeing any any connects yeah yeah it's actually the logging in that's more annoying than than creating
the game uh so let's clear game yeah we're not we're not getting okay well we are getting added as a called and our
websocket Handler is the broadcaster it the Spring Security shouldn't matter because because it it basically gets the pr
security principle from the HTTP request upgrade to the websocket and then it then it just works yeah and an Embler it's
all secure stuff so let's do this let's uh let's disable the connect so I wonder if this is forcing something to happen
that is causing it to disconnect before it has a chance to do anything else uh or isn't giving it time to well it's
clearly trying to connect um apparently there's a syntax eror somewhere oh I wonder if that's causing a problem that was
Cody's fault uh that was sitting out here uh so let's that I know if that is causing a problem that uh so let's go back
to the console uh let's go back to the network clear game all right well that was not the cause but at least gets that
out of the failed why feel like it's something really obvious ensembl I wonder if having the Ws connect on the out um
and the other thing I want to look at is game it who takes precedence at this end point way I think that will work
better too stop game that's there no errors in our console uh our network is currently connected we've got all right so
now that we've fixed that um wow so how do I prevent that kind of error future I feel like that should be a
configuration error I think spring should should handle that I think it should say you already have something mapped to
um all right let's clean up a bit uh so let's go back to um here no not here here uh let's put that back and we can get
rid of that so this was throwing exceptions because it was receiving the name of a game of WS um and this will learn me
to put message in here which might have helped um so let's put a message here uh whoops that should be on the string
attitude um yeah I'm going to reset the timer for a bit because I have not made as much progress as IID so if I had had
this this probably would have let us to um figuring this out sooner because I would have seen WS I might have seen WS uh
although the long stack Trace didn't didn't help are you talking about the same video the response to safe I I actually
haven't watched it yet um it's always the same all right so now that we've got that connected uh I'm going to keep this
on a div just because there's something about putting it on the body that makes me uncomfortable I don't know um but now
we uh let's turn off all our break points here we don't need it yeah so you know what this is we weren't seeing this
before we weren't seeing the websocket connection established so I think that somewhere deep inside of the it but did
not throw an exception which I think it should have deserved an exception so here we see the websocket connection
established um if we go into the thrown oh wait there's the websocket connection oh never mind then oh I connected to
both hold so I think this is basic I think this is the problem async request not usable exception I think underneath uh
it's trying to also hook up the websocket endpoint to the same endpoint that there's already a get and mapping uh unless
that's the front end trying to connect it might be the front end trying to connect so I think we get that's definitely a
bug yeah the connection established async Handler is likely the Tomcat serlet Handler wondering what the heck is going
on with this websocket thing um but by then it's too late but it's clear that the websocket connection on the server
side failed uh and we are not told about it bug because if it had thrown an exception it would have saved me what half
an hour 45 minutes of troubleshooting yes make sure that you've got a clearly different endpoint prefix um my guess is
probably not a lot of people use the raw websocket configuration um they probably if you're going to use it I mean for
the longest time I was using the stomp version um so it wouldn't surprise me message um but it clearly there clearly
somewhere an exception is being caught know um I think a nicer two string there correctly um so we see we don't see
anything here either I wonder if I turned up the the logging if I might see something um but it won't be until the front
end connect that we actually see see a logging message which is probably actuator um yeah all right so let's uh um let's
now this so uh so we got the web socket connection established um oh and I changed I changed it to call the so now we
should see something on the console again uh so we said we wanted this to be inspect uh so we've got the form here it's
hidden so that's nice um even though the form itself is not hidden because the only thing that's inside of it is a
hidden field uh but it does have uh let's see if we can get it all right thank uh is that looking like what we think it
so we got the connect uh this submit button and then we can troubleshoot whether this does the right thing but right now
I'm not sure what this that refresh the I did send this is the get is and there's the payload which it's fine so uh
let's try it again let's restart server this page all right refresh the page create a that's the socket okay so uh the
wsn is working the form is working and sending the right information uh I just need to have the right incantation for
the form to self um but I'm I'm happy that at least we got to this point uh and likely if we look inside the payload uh
which is inside of our websocket broadcaster um payload I'm not sure what uh oh it's the message that we want is it get
payload because I don't so that means that will have to um parse his Json and then do the right thing uh but that's
restart oh I know what I wanted to do also so I want to see if if I've got the event wrong or if it's the submit the so
must be that I've got the event wrong because I'm not seeing anything in the console I wonder if I can should try the
other way let's even though it it should work the other that yeah so for some reason what if we move this to oh and this
bug has been open for a while oh interesting so there must be something with the with the initial load so I guess I
could uh way um let's try that I didn't even think to look that this was a bug um so let's go uh register another script
uh we want open um I don't are people spelling event EVT because they don't want to be confused with another EVT or
something with with a vent is that like another keyword or I don't know I see that all of the place like this works fine
I don't understand okay characters are expensive I mean sometimes like people do that because um it would conflict with
some keyword or some class that that's everywhere but yeah I should be able to I was just wondering like the person who
suggested the code um wrote it with EVT which I don't oopsie let's all go to the lobby all right hope I don't get copy a
copyright that there we go uh wait a so my guess is uh there's some order of operations issue um my guess is yeah my
guess is there's an order of operation issue that the websocket is is being initialized before it has before loading
yeah I feel like this WS connect is happening before it had a chance to process and add the listener register The
Listener for the form yeah though can I not use event here is that there because otherwise what's the unless this is not
allowed I'm I'm confused by the error cannot read properties of null window right I don't understand that I'm I'm no
there's the event it's open that's all good there's the type sure yeah I don't know what the right place to do the ad
event listener would body I don't know can we submit the form now um so we know this works do um document oops uh how do
I the um it might be safer to put them at well they're not deferred so they're executed pretty early thank you get
element by I'm like query query query uh get element by ID uh what did we say the ID selector uh can I just say submit
well jav script do that for me um let's try that first selector no oh we're not on the page like why can't I find it
there we go let's try that again uh documents get element by ID no not animations selector okay and then on that I
should submit um so it did something but this it did reload the page which was a concern I had uh when I first thought
about the form being submitted does wend post um and that's an interesting question because if it does that sort of not
great uh I don't remember seeing that in the connected uh so we get the game handle but interestingly enough as part of
the headers we also have the current URL anyway um so we have access to the to the game handle uh let's clear uh so it
cleared the console and it does look like it reconnected uh so I is yeah so I don't understand why uh directly invoking
it doesn't work unless HDMX just doesn't event it might just be easier for me to write some very small amount of
JavaScript instead of trying to get wsn to work because it's something I'm I'm which I think is fine I yeah I don't know
hey there Yu um well learning any library takes longer than I don't I I would not necessarily agree that it would take
longer to than to do it than to hardcode it although I think the websocket stuff is yeah well the current aodot attitude
is that uh um when when I when this form is supposed document uh uh get element by ID hey how'd you know this is exactly
what I wanted thank you Cody um we expect that this when the websockets open it'll do a submit and I was trying to kick
it off in the console by calling submit which send um let's try it this way and see if that works and I got to stop
sitting on the page work so I have a very strong Sub sub wsn um is also causing a post because we can see it's it's
constantly uh reconnecting and we can also see in um can I basically say none uh it wouldn't be action none it would be
method I don't think what I don't know I don't know what to do here um I don't think I know enough about how wsn is
working uh but it does not seem to be behavior yeah now course it it's clear that um the get element by ID was working
uh it's just that wsn does not does not seem to be preventing the the behavior of the submit trigger but now that feels
like I may as well just write two lines of JavaScript um so let's do that so uh what the heck oh now it's got really
confused about um so we want on a when we do the Ws open uh we get the uh and so now the question is how do I from can I
pull it from the URL I could pull it from the URL that seems kind of there um because I know I can use uh th to inject
uh code into JavaScript I did let's let's just do that let's just do so here we'll add to connect it's a few brackets um
we'll basically do something like handle and this is uh what was handle it's not all that many brackets yes okay so we
got that and look at connect so now I just have to interpret I don't I don't think I want to go and convert it to to
Json although I feel like I might regret that if maybe I all right and on that note uh I am I am overdone for for today
uh so uh so next time we will finally be able to uh so I'll have to reconfigure all the websocket stuff to now that we'
ve gotten it uh will then start be able to br broadcast the notifications and and all that stuff so um this was much
harder than expected although um thanks to suiga and and folks for for helping out appreciate it uh so have a good rest
of whatever day is left for you um if there is none left then have a good night uh and I will see you next time my next
plan stream is tomorrow same time as today uh 12 p.m. PDT uh 7:00 p.m. UTC and I'll see you
