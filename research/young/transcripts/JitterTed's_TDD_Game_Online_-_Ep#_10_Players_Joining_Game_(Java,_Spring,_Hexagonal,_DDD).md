# JitterTed's TDD Game： Online - Ep# 10： ＂Players Joining Game＂ (Java, Spring, Hexagonal, DDD)

**Video URL:** https://www.youtube.com/watch?v=uU1TJQRaonA

---

## Transcript

so what are we trying to do where are screen yes Jonas uh I have uh when I can I try to do it do it earlier so uh today
will the rest of the week will be earlier starts so uh hopefully that'll help you all stay awake yes earlier woohoo I
love how long that confetti takes so uh what we're working on is of to um I guess an MPG a minimally playable game um
not miles per gallon but minimally playable game uh and where we're at is um the sort of waiting to for the game to
start uh which is kind of this component but we have a much nicer uh layout in the real thing so let's go take a look at
that um one of the things I've I've been uh thinking about sort of it's a bit of thinking ahead but you know just
because we we are doing tdd and sort of in the moment uh doesn't mean we don't also think ahead uh so things I've been
thinking about are for example um what if uh a player joins late do we want to allow that so right now for my MPG my
minimally playable game uh I'm not going to allow that uh but um it actually wouldn't be terribly difficult to just add
another player assuming you've got room um and then dealing them cards and in in the game again as long as there's room
uh one interesting thing I was I was also thinking of is if a player drops out so if they time out uh then again because
the minimally playable game does not enforce turn taking it doesn't enforce any rules uh you can just skip over them but
it might be interesting to to have uh a little machine learning um I hesitate to call it an AI because I'm not going to
do any of the sort of game oriented AI uh techniques U but it certainly could be something where if you don't have
anybody to play with but you don't want to play solo uh the computer could probably play a reasonable game yes bring AI
but it's not it's there's no llms here there's no I I would pretty much honestly just have some her istics like you
don't need anything that sophisticated here you know it could have you could have the the conservative uh computer where
it it never goes and takes risks and just plays the cards it's dealt um or you have the risk-taking one which always
takes risk uh as much as it can uh those would be sort of the the basic opponents that you'd have um the other things uh
that I was thinking about is is the Observer um so I definitely need that and thinking about how you might observe
multiple games so for example if if I'm a coach and I'm using the game to facilitate sort of learning about tdd uh
especially like as said that doesn't mean it's no design it just means you don't go deep into that design and start
designing your class diagram remember doing that way back when yeah find out State yeah it's kind a state machine just T
to figure out what the the optimal thing is um and so uh so the Observer would have a different view than sort of what
we see um sort of in this in this mockup um it would be close to this uh but s there would no be no sort of primary
player so it would be pretty much this layout for for each player um and things that I'd want the Observer to be able to
do uh for example is literally stack the deck uh so what I'd like is uh for example to set up a certain situation uh I
might want to Stack the deck and say you know these These are the cards um so being able to manipulate these objects
sort of behind the scenes um would be really useful from Observer facilitator point of view uh in addition i' sort of
want to be able to see events as they happen uh from from multiple games so there's all sorts of stuff that for for that
view that I think will be really really interesting um not necessary for the minimal playable game um though the minimal
playable game does need uh to have just a straightforward uh Observer view so we'll we'll figure that out when we get
there but we are not there we are here uh more and uh let's see yes so let's go is uh why my icons not showing up there
they are took a little while uh so this is a slight updates to my uh previous um layout I wanted some some icons here
that we're not just sort of check so basically I'm using the font awesome set of icons uh I might switch some around I'
ve got some other choices but this is uh uh what are you seeing astd for this stream um talking about the title or or
something else I might have to check my what what that looks like I haven't I haven't looked I don't expect people to
sort of browse or around I guess and hey swegi welcome so anyway so what we're working on is um we've basically defined
two what I'm calling uh UI components and these are basically areas uh you might call them elements of the screen these
are targets for um basically for HTM X to to Target updates so the top one is if we bring up our websocket sequence
diagram which I have updated to be more accurate uh we've got two UI components the who's connected component that's
this one top one and the notifications UI component which is the bottom one uh and so that way when we broadcast when
the websocket session man manager does a broadcast which is basically here and here and then again here and here uh we
know targeting so that's what uh we're working on we got all the websocket stuff seeming seeming to work uh so let's
take a look uh let's leave that open we'll preview uh and so one thing that I noted uh that I that I uh posted about is
there's order of operations so for example um player one uh really it's more player two when they connect with the web
socket here um right because they got redirected to the game page and that's the page that has the websocket connection
uh it's possible that this websocket connection doesn't happen until actually after these messages are sent and so the
websocket connects and uh so what I did in the ensembl CH will'll do the same thing here is a is uh the websocket
session manager we sort of cach the last um last things that were sent and then sort of send connections uh I will
likely not do that for the notifications um but definitely need to do it for uh the who's connected um um this thing is
basically I will just send the current state because that will that will always be be up to date uh so there's some
interesting sort of technical you know caching going on here um I don't feel like I want to and I think I mentioned this
before I don't think I want to cach the the notifications but I definitely need to cash this stuff so that uh when you
know so blue connects they just say blue yellow connects but maybe it's slow for the websocket to get set up and doesn't
receive this uh update when they connect blue will have gotten it successfully uh but then when yellow connects through
the websocket the websocket will say great upon connect let me send you this which means um my websocket session manager
I'm going to need sort of this this idea of what's the container so I'm thinking about this like this is the websocket
is concerned the websocket manager there's a manager or session manager whatever you want to you know waiting uh waiting
screen manager that's holding on to to just this um and then uh then once the game starts it can basically toss away
anything that it has regarding this waiting screen um all right so we've got test and let's fast so we've got player
connected message broadcast when player connects to game um so what happens is is uh We've set up our mock broadcaster
um and we have now our player connector connector is in our application layer it's a use case uh and so it's the thing
that's sort of managing um connections and so on so we see that when uh a player username connects so this is what we
get when the websocket connects we get the uh along with other session information about the websocket we also get their
security username so again that's one nice thing we don't have to worry about the security cuz once they're logged in
they're logged in whether it's uh HTTP or websocket we we know who they are um so we'll get that username uh we one of
the last things uh we did last time was set up these finders um so we got a finder a game finder and we've got a member
finder uh and then we basically um find out what uh what their player is so their player uh the player information and
then we can then we broadcast that out there invos Alta welcome yes diagrams are awesome so this is uh the application
which again sort of has no concrete references uh or references to to concrete implementations um right now our member
finder and our game finder are pretty thin wrappers around um our game store uh and our and our member store which
themselves right now are just in memory so we haven't gotten to True persistence using uh uh the spring data jtbc we'll
get to that at some point but for now um so the player connector so we've gotten a connect we already know that that
they joined um and so what we'd like to to do is I think what we want want to do next is hook this up to the real
websocket broadcaster so actually there's there's two things diagram so we've got um our inbound adapter uh websocket
that's our our Handler and that's this guy that's this Handler um right now it's it's a very generic inbound Handler
eventually it might be something like the the waiting room and uh what we want is when the connection happens we want to
then call the player connector so we know this code works we know this code uh we also know that this code works so
these two things work um we know that uh we broadcast when it's connected so we know that that that works and now what
we can do is is start hooking up uh the real thing so let's see how we'll do that so we want uh after connection
established we're going to want it to basically call the method on on the so where this can get a little confusing is
wait player connector has a dependency on broadcaster so remember broadcaster is the outbound thing this um so the use
case of course needs a dependency on that and so we inject the port because that's the the abstraction uh and and we've
tested basically this inbound um now we want it uh the the thing that triggers the whole the whole thing so um I'm just
thinking about the the more precise class here but I I'll just start start adding stuff to to this so we want so one of
the things that that I want to do when I'm when I'm testing a real inbound thing like this is um I could probably write
an automated test that is driven by like playright uh but I think right now I'll just I'll just test it manually so
rather than try and it with using HDMX it might be useful also to um client does intellig have a websocket I know it has
knew so the so intellig has a built-in HTTP client uh and it looks like as part of the HTTP client it supports websocket
um so this is really nice so that means I don't have to be out outside of intelligent because it's a scary world outside
of intell I like to all right so um we certainly don't need the content type uh and it's just the request let's try it
out so it's just web path oh and there's a live template look at that create a new HTTP client where are where is it why
do I not see it there it is htb request it's like it's not in alphabetical order and it's not in the order of like
common usage and so I don't know where the heck it is uh but it's right there uh so we're going to player socket and uh
we'll get rid of the comments and we'll type wsr which is a websocket request look at 80 game and that's it um I like
how it's oriented totally towards towards Json which is oh that's really interesting so there's Server that's cool um
let's uh let's comment that out and then we'll rest yes jet rins are a awesome um I actually I'm working out some uh uh
a deal to to get and give away various things I need to follow up on that um yeah the problem is like most of the dev
advocates for for for Dre Rin are in Europe so that the timing doesn't always work uh but yeah I'll I'll hit her up and
see see if she's interested in coming on all right so we don't want content type Json uh we're really Bare Bones uh so
what we want to set what we said our our kind of protocol is connect and then the game handle um so I think we probably
want up um I guess we you can just look and see what it is uh so it's going to be connect um we'll just do any game for
now uh we get to write what how we handle this and we'll just um find the first first game and connect to it I don't
know we'll communicate um so now what we want is we need a dependency on player connector so yeah no that's not what I
want uh I want um and I know this autowired is not necessary but I like it we'll go config and we'll go ahead and create
a bean okay there we go and no we don't want a gamefinder connector and and perfect uh it needs a broadcaster so to I
think broadcaster right now is just a single abstract method so we can um a I got these as stores these are not finders
um so close uh but that's fine we'll just translate them since they're simple rappers so what we want are member finder
and game finder oh I guess we could just do that game one through M case yeah I I totally get why autowired is optional
um like it's smart enough to figure out oh look I found a Constructor that matches what I have um but annotations are
not just for telling the framework what to do they are also documentation uh and so I personally Find removing this
means I I I it's no longer in my face that this is going to be autowired by Spring um and I personally think that's bad
uh and when you have multiple Constructors then you kind of have to have the autowired so if you do a refactor and you
add another Constructor well now you got to go back and add the autowired so that's why I always put it in for those
reasons all right uh so we've got our player connector spring is happy that um let's run all of our tests just to there
yes if you see autowired on anything other than the Constructor that is definitely bad um uh I've asked around and
nobody has yet convinced me why it would be reasonable to have an autowired on anything other than the Constructor other
than Legacy coat and I'm like fix that uh okay okay so here uh game handle is not found that's fine uh so let's nulli
right because I'd like to use gam store. uh oh I don't have an elble entry for that um it would be nice to use uh game
game but um it's just as easy to say game store and that uh you need a little bit more name and that's the game handle
okay it has always been thus therefore way there is there is the saying about misquoted um it's a foolish consistency is
the hobgoblin of of little Minds some sometimes people drop the foolish part and say consistency is the Hop no
consistency is fine but a foolish consistency is the hobgoblin of little Minds another words don't just be consistent
for the sake of being consistent be consistent but also change as needed yeah it's unfortunate if you've got Legacy code
that relies on that stuff um and all you can do is change it can and yes it's funny how hysterically and historically
are are are very similar at least in English all right so this should uh pass directly and there we go all right so um
didn't really change much other than uh ejecting uh player connector into web socket inbound Handler okay oh yeah I
haven't I haven't watched that talk yet that's that's on my long um all right so we've hooked up our player connector uh
kind of want to abstract this out right now this is a dummy broadcaster so I want to make that more clear great um all
right app oh yeah so let's go back to the config for a uh uh command line um that's funny it's like yes I want to want
you to generate a bean uh but but Runner uh and there's my args um but store again it's like why is Cody pulling in code
from another project it's not player account repository I didn't even say player I said member to member store member
store member store me store no oh that's a nice quote uh tradition is not to keep the ashes but to pass on the fire
where's that from so yes uh no not new game what are you doing okay now I know which project it's taking this from so
some of you will recognize uh funny uh so there's our our our Blackjack Ensemble game that was using those as sample
names yeah my mic uh this is more like what we want create and the member takes the member up oh I don't have an of yet
for that so is that okay all right swegi yeah I'm not I I don't need a broadcaster yet um we we'll get there and I'll
use the the your nullable stuff uh we don't need the ARG so we can rename that so we store a new game uh we save the
member and then we would would like that member to join the game uh so we'll need to hold on to this game um oh I guess
I can extract that out to member and then this is just number ID all right so the reason we did this was so that uh when
we start up the app there's already a game there's already uh a oh how is so the question then is how is the htgp client
going to handle the websocket see how would we do so I would probably have to off and then I can do the web socket hey
Bel Lo welcome ice to see H oh I don't trust the AI assistant for oo o configuration oh see you know it's like I could
or I could just read the docs uh so we can basically create a new environment Dev got it um so what do we need here we
need o that's interesting that it it talks so off there we are um oh yeah okay duh it's just authorization okay uh uh
authorization if we try to connect directly with a websocket will it request authorization let's try it uh so then we
don't need this right now this and our username is yellow uh no actually our username is yellow the password is yellow
that actually that doesn't m match what we set up here um I'm probably going to want to change uh I don't know um likely
I look at in we can stick in this stuff uh so we secret it's funny it looks maybe uh so this is probably more than I
want to do but let's let's go ahead and do this um why did I bring up my this and then we'll close that uh doesn't close
that it closes secret this might be Overkill yeah I I think I think uh it's not clear for me how to do that um and the
password I I don't really care about uh so let's just a um so what's our password our password is that okay there we go
so we want authorization uh basic and that's our password uh yes that is an uppercase Y for the username got yep that's
the username yep that's username I might want to change that but for now it's fine um uh in my uh startup um that's
because member has has the nickname which is uppercase uh and the off name which is uppercase and then I change the
player name to be Mr uppercase so the only password yeah I mean anything else anything other than like I just need this
for for for testability um one once once we get past this and we have real off and this this goes able um let's first do
uh copy and so we said this is basically that and we want uh Local Host 8080 uh game uh actually what do we and it goes
to Lobby okay go away lobby uh what I don't want it to do is then kick off the websocket one um add request separator oh
that's the request separator that doesn't look like a request separator that looks like a request separator I don't know
why the W there was a w in front of it uh so that's a okay all right so uh we expect this to work let's try my um oh
like what the oh that's interesting I could do a post so I've got htb basic with the addition in uh there's no content
type well I guess off I might do that during testing and let's see what we get uh oh this probably has to be URL encoded
you know what I'm going to turn csrf off because that's going to be annoying for a little while so let's go restart I
never understand csrf uh so csrf what it does is it makes sure that um when you do a post to an endpoint that it's
nobody's faking that post uh so timely will automatically inject a csrf token and it's a unique token um and then that
gets sent back because it's a hidden field and so that way uh the security filters match that up and say oh I sent you
this form I just got it with the same token there for it's oh did some page refresh yes this page weird okay uh let's
clear that let's go to our I don't understand oh that's because it thinks it's a header that's why has to be a blank
line between your content uh Response Code 200 all right so um so I think I don't need this authorization so I'm going
to stick this down here uh and we know what the game is we're connecting to what did we say it 83 oh so we shouldn't be
yellow we should blue okay and now we should be able to cut text um oh they didn't join so they need to work so let's so
we posted join uh oh is to just join with game handle okay uh that's fine and then it's uh game so we're now on the
waiting screen so that's what all this stuff socket so two players spider I wonder if that's going to be a we're yellow
um this yellow not connected is temporary stuff that I should probably comment out okay so we are now uh we're now
connected we're websocket um we could send other messages but that's actually good enough for now everything that all
looks good um let's close that for now we don't need the config with uh actually the config uh let's who are the other
here okay uh oh what tool am I using um the HTTP client in intell apparently supports websockets along with a whole
bunch of other stuff it's much uh it's much more powerful than I thought all right so we start up we have a game it's
joined by by Mr red um let me go to the uh game out um I thought it might be easier to to to test through the websocket
that way but I think it's actually just as easy to test through the HTML page cuz that's fine so uh we can close that we
don't need that anymore so our inbound Handler see uh what we want to see is that we want to see some connection
connection string yeah I think uh um for you know unless you're playing back a lot of scripts uh a lot of complex
scripts already that are already done for you in Postman um yeah the built-in client uh is really good because you can
do multiple messages multiple you know sequence things um and it's in the same repository as your code so use it um okay
so we get our player connector we want uh after the connection is established um oh right so at this point we don't know
which game they want all we know is that this was was uh connected um it's not until here that we yeah so I think here
we basically call the call a connect all right Jonas have aspect so I think I'll write the code to connect it to my
connect my connector uh to call the connector and then I will um then I'll be basically have that payload uh information
well I've already got test against this so I know it does the right thing so it's basically I just need to parse out the
the game handle and then I'll do that hey there suw yes HDMX just like it says over there uh all right so what we want
to do is player connector close it's not session it is session uh get name and then get payload what type is that oh
it's a type t uh then shouldn't websocket message be also of type string no I can't override it that way it must be
bummer all right um so get payload is basically an unknown or I could just cast it because I know payload create that as
a local variable string message get payload except we're going go hey it's a websocket message it's got Getters that's
it's a it's a technical dto I um all right uh except we don't want to send the entire message payload we want to um oh
look at that that was handy I was going to do that anyway uh but thanks Cody see it's that kind of stuff that that um I
think these AI assistants are are good at it's like the boiler plate the stuff that GH I have to remember how do I split
and then which one is it and and it's like yeah you split on the colon and I want on the right side of the colon uh I'll
leave that join and there we go we are joined um if let's open up uh another so this will require me to log in green I
do do I I do okay so we'll log in as green green sign in there are two players here go away uh and we well we won't see
anything unless I refresh this page but when I get this page uh I should three so I've got all three if I refresh this
three so uh so our connect is working we can now connect two it uh and now I just disconnected um but celebrate I need
to get some Fan Fair confetti and so here we basically see the the websocket text message um and the connect and the
payload details and so another uh okay so I have a tool um from the wonderful Folks at uh rogba who uh create a tool
that it's one of the Main Stays of of my Mac and streaming and so on is loop back but there's another one uh I bought
the whole pack and it's um oh I'm blanking on the name of it uh it's one that that basically has uh a screen it has
buttons for different different sounds that you can play I'll have to bring that up next time okay so we are connected
um the uh so we told the player connector um we do need to handle the uh the waiting screen manager the waiting room
manager um which is sort of going to be this sort of session stuff uh but I don't think we need that yet okay so we now
have uh uh we now have the web socket we know that that sends a connect to here and we know that that talks to the
player connector and we know that that talks to the broadcaster because we have a test for that um so now what we want
to do is we want to implement uh the broadcaster to basically send back out um uh that information of I think uh let's
go implement it so this is going to be for now our websocket one um this is not a an application Port this is an adapter
uh websocket and we'll Implement that method um thanks Cody that really was not um The Ensemble timer uh I don't think
there's anything in it just does a session send message yeah so I think uh I think I just need to to have a central
place to store the messages um and that just iterates through all of them and sends them all right thanks for then the
session map is not actually in the inbound Handler cuz it can't be as we said in our diagram it's got to be uh somewhere
else so I think I don't need this class so let's go ahead and delete I'm just thinking about this direct connection
between uh the inbound and the outbound uh it's kind of an implementation detail so I think I think map and I don't
think we want to do anything here oh thanks in inosa been doing it for a while so uh so let's put that here map it needs
to be game handle to list of sessions right oh so what did I say say about uh um a multimap did I want to pull in a
whole library or just do it myself I really feel like pulling an entire myself gets a little complicated when I need to
but I do feel like I've implemented this before but I I looked around a little bit and I didn't find a handy
implementation um it is something that is straightforward enough that I might be able to get uh chat GPT to generate it
for me or I mean or Cody um let's go ask I don't know if I want to make it um if I if I dare ask it to make it thread
safe let's let's see how it do all right that seems uh pretty uh pretty decent um I don't think I need the contains
value or the contains key um it was the it's basically the remove that is the the the quote difficult part um so does
the values get null if it's not null then it removes it um if it is null then who cares uh then it returns false uh if
values is empty it removes the key from the map uh and it uses a hash set so getter default so it doesn't return a want
that should kind of never happen but that's fine uh and then a put is a Compu of absent um so if it's absent it creates
a new hashset and then doesn't it uh yeah streaming is is there there's a lot going on especially if you want to pay
attention to chat y should I ask him to make it threat safe safe cuz like all it did was basically replace the hash map
with a concurrent hash map um I don't think this is threat don't yeah this this is not film me with safe uh I mean I
would certainly use a concurrent um instead of a hash map I'd use a concurrent hashmap and I think implementation uh do
I need the I don't need any of the contains I don't think I need size uh I think I pretty much just need till here um
we'll make it uh a class here uh we won't make it public just yet um multimap uh let's make it final I don't know why it
didn't instantiate it up here how about we there and then we can take out that um that's fine that's fine think I just
need put get and need yeah all right uh so then what we want is our session map is actually a private final and um
websocket broadcaster we can make this a component because we are in framework land so we can just mark this as a
component which means we can then uh have this it I don't think there were any usages I um I'm not sure what methods I
want yet on the map I'll have to see when when I use it in context what it looks like um this is for game handle to so I
could make it very specific to this domain and and call it connect and disconnect um at least for put and and but I
don't I don't I don't know that I have a problem with this internally as as a map we we'll see when when we use um do I
want I think I want the whole to so we're going to talk to the websocket broadcast um actually we'll just call it uh
this is interesting I actually want to do a remove of the websocket so yet said uh and I'm going to copy this there so
do we need a two-way map I think so because I need the the game handle to session so I can broadcast out to this game
but then I need uh for this games yeah okay um so now here this is where they actually connect uh right now I'm going to
assume I'm getting the connect message so we know the game handle we've the broadcaster as well so websocket broadcaster
um connect and what we want naming is here at this level I don't uh because it's in the application uh it knows nothing
about websocket sessions it just knows uh player usernames and and game handles um so it could be that this is not
really needed uh that we could sort of out of band just send messages out but I don't like that feeling of not going
through the application for that so here when we connect uh we want to do a game handle to uh something like announce in
front of broadcaster I feel like this makes it a clear so when we announce what we do is we basically um from the game
handle to session pretty much that um except we don't have a connect message uh but good try Cody um what we want to
send is simply uh eventually it'll be HTML now uh what did I want the HTML to look like so notification container that
and I'm going to eliminate this stuff uh messages notification no notifications will appear here do oh you want to send
Json don't you no don't uh I don't know what the heck that right there stop trying to do H uh not want that we don't
care care about the that we want a list item um we'll leave that there for now uh so what do we know we know about the
player's name uh so this will become that and then we do formatted with player username close it's not player just we'll
surround it with a tri catch for now and we'll throw runtime so this is going to be the same HTML no scope uh yes anro
yes thank um it would probably autoc close but it's better to to close work this is sort of the um tight RPP I'd like to
have a better way of of testing this in an automated way um all right so uh let's run the game yeah browser it all right
uh let's go lobby umy spider I oh no I did right here uh and am I sure that worked yes um cuz I know this is being
called with the correct information because that I have a test um is this getting oh this isn't getting the real
broadcaster that's right because in the game config I use a injected so we create that as a parameter value that will um
let me change the order of this I'd that's not a call that's weird oh I guess essentially that is a call uh that's
interesting intj knows that this will get injected over here um but there's no direct calls from it and so now because
we have this as a component spring will actually use the uh we got to go back to the lobby back to the lobby uh join the
another one uh actually I want another one of these yes let's all go to the lobby uh we want to go to the lobby um oh
that's interesting so it's I would have thought the separate browser window would have all right let's log uh and let's
log back oh because I'm not tracking uh closed uh exceptions uh so let's handle disconnects because otherwise we're um
yeah because I rethrow the exception here um which actually I may not want to do because if I get an exception on trying
to send a message uh I'll probably want to do something more sophisticated like um ignore it a certain number of times
and then basically say they're disconnected so for now I'm just going to do uh let's yeah so once I broadcast to a
closed connection it basically blew up the whole the whole thing uh and then it uh that's a good question whether I can
um let's do that log is a little Annoying in this way we'll just pass along that robable um what can we ask the session
we can ask if it's yeah I'm sighing because there's um logic here that it's not going to be that see that's actually
wrong cuz it replaced the concatenation so now the second basically all the rest of the arguments are considered objects
to the message it's been yeah basically that becomes the second argument I don't know what that that'll um so at some
point pretty soon I'm going to want to provide some abstractions for this uh and this is some of that nullable stuff
might be handy so let's this will be good enough for now yeah yeah I was thinking is it it's really more some of the the
output tracking related stuff I don't think you missed any good rants uh okay so let's restart game and now we'll go
here and we'll go back to the lobby and join the out green and that should have been an after oh right I need to specify
the swap on message um but hey we at least we saw the updated message we got the message for each one now it's now it's
now it's just a matter of doing the right thing with with hmx uh so what we want here is in um what is it exactly is it
HX o o let's go look want and we want that to no not be true we want that uh after begin after before no after begin
after before what a comedian yeah I can't wait either um cuz this is really annoying to to forget that uh and I cuz cuz
I keep thinking it's like well I've specified it uh here ignored because of this so let's take it out so I don't get
further confused um all right uh um no I can just use I'll just use instant so now um that's going to be too much
information I just want to look I know it will be wrong for people in okay uh do i l all lose all my connections yeah
game let's go here go back to the lobby game what did I mess up unsupported I messed up oh is it try oh right because
instance is not a local time um then I'll just do time I don't really care it's fine uh what does instant look like no
that's too much information I just want time yeah because if the a is not available okay let's join and then let's what
oh it's still hour okay I don't understand that's times Time stuff um when we do a two string on that what's that going
to look like I don't there it goes that was weird uh it's probably a bit too not why what is he what are you yeah I
could do do that it doesn't it really doesn't matter this is all totally temporary there it is what I guess it still has
that Precision whatever all right I'm now he says as he basically goes and looks to see uh should I just do of that um
what so that's the notification uh what I also need to broadcast and announce is um the itself generation so we'll do
HTML that yeah that's an optimization astd I'm not going to worry about that right working uh um oh I moved my register
I probably haven't updated that I'll have that uh it's basically because it's it's not um I didn't tell the registar
here's the new DNS and then told the DNS here's where where it is cuz I moved registar and that didn't get transfered
over oh well uh so what do we want here container and inside that one is going to be so this one's going to be
interesting I probably don't want to spend a lot of because the idea of um of of these icons is it's green when they
have when they're joined and connected uh and orange so it kind of looks like uh looks like that when they have when
they are joined but they have not um I think right now that's a that's a want because what I'd have to do is to figure
out if they're connected player uh I said it was nice to have in here I am thinking about it no it's nice to have I have
the information but I'm not going to worry about it right now okay uh what we want is we want where do we want to insert
this thing we want to um that's the flex items Center duplicate no that doesn't need to be in Jura I will not forget
about that and if I do it will come up again so we want this list item and we'd like it invented properly please um we
don't need the th each here uh what's the target for is the uh this is the not the notification container this is the uh
so what's in the box here are the people who have joined the game uh so if I refresh this and it works still connected
we see the same list on both sides um so these are people who have joined then the ideas the icon would show also when
they connected uh but right now and join will generally be the same as connected there might be a slight play all right
ASD I know it's late so thanks for hanging out see you tomorrow uh and we want the HX swap but not after begin uh we
want this to completely replace what's text is what uh will be the player name this is all fine uh but we need to
iterate through Yeah so basically I'm building the the websocket HTM X version of of this list item uh technically of
this looped list item so let's put in the Target ID cuz I left that oops um and so extract uh extract this out and it's
HTML for player parameter and then we want game players and I want to do a stream and then we want to map uh player to
yes that and then um interesting idea to reduce uh that's actually pretty much work I don't know why these are static
static boy I'm writing a lot of code without tests um sobody should have stopped me once I got into this level HTML uh I
I need to go back and and and test drive this um maybe when I componentize it I'll do that all right uh so like this
code I'm fine writing without a test because I don't have a great way of testing it this code though should tested um
what uh I don't even think it needs the game handle uh let's see so bdsl hey there uh do I think that for this HTML
generation code Golden Master testing um might be as good as tdd uh I don't know the difference between Golden uh oh um
that would be a characterization test yeah sometimes it's it's referred to as goldm um I use Michael feather's term of
characterization so I could characterize it um that's what I'll I'll end up doing uh in fact now that I've split out the
HTML generation from the other stuff let's go do that so let's pull this out uh this is going to notification I guess
technically it's notification that uh and so now let's move this up I don't know why this this doesn't need either um uh
can totally do tdd and um yeah I I mean that's kind of what I what I'm doing here is manual characterization testing if
that's a thing uh it's really manual manual testing and just looking it and inspecting it but I'll write tests uh I'll
start off with characterization and build it from there so in fact that's what I'm going let's actually make these
static again all to new file so let's move this uh so this I don't know what to call us HTML generator waiting room view
waiting room Transformer now okay order Factor yeah I guess render is a better word thank you uh bdsl uh or connect
notification and then here um make those non-public this should not this uh canano why not send them a separate messages
I could but why bother once it's easier to build up a bunch of messages that Target different places on once it's
probably not a lot of overhead so either way but I need to send them out anyway so may as well uh all right so let's do
we think we can ask Cody to write our first line characterization tests let's see uh before we do that let me run all my
while oh got a failing test all of our MBC tests uh I suspected as much we're somewhere uh player uh does not have a
really oh because it doesn't have a broadcaster might want to create now a test that um I think I want to yeah I think I
want a test configuration all right so let's move this to a test configuration I'm really not thrilled about using a
mock Bean on that even though it kind of doesn't matter uh let's go create a test um I never know how to trigger that
from within a file control shift is that what I need oh it is control shift okay uh so what I want is a uh basically I
want a dummy broadcaster though that's hilarious that it did an anonymous inter class no you don't need to do anything
and you don't need those either that that's funny uh hey tkes um am I using the latest release of spring boo 3.3 not uh
all right so we got our test confix so now we need do I need to import that I always forget whether I explicitly which
now leads me to believe that I want to um pull some of these annotations out either with a meta annotation or with a
base class uh but for now I love how intellig when I type comma here it has the braces for me it's such a little
convenient thing that's beautiful uh we want test config class all right so that works and so we'll just grab that for
all of our MBC tests tests all right so let's go do a that so is it just me or did it not add this this test class to my
change list which is good cuz I don't want it but it's interesting that it seems to frequently I probably want to turn
the csrf back more because um Turned out it just wasn't hard to use the application itself to test the websocket stuff
than trying to use the that okay uh bny yes I have um I've basically settled on their MVC tests since it's named as part
of The annotation we use a mock MVC and we do mock MVC stuff uh and the new assertion stuff is also yeah it's shorter
let's see what it came up with render room okay um I like how it's doing the 01 many so that's that's a that's a plus
right did the empty with one with multiple uh uh I don't think I need four and five though so let's go grab these CU
there should never be an empty player name oh well it was a nice try um but uh and it instantiated it which I guess
technically is fine methods and its assertions are just completely wrong like what what good is is is AI llms if they're
not going to even like look at like okay even if it didn't quite compile like the intent of calling this method that's
fine but like it's its assertions are pointless like it it's as if it's as if code um let's see if we can be more
precise uh cuz there is some like boiler plate that it would be useful for for it to to to do uh so let's see if we can
get Cody uh to generate a test explicitly for that so that's of so like at least this was reasonable um so it got the
right name because I gave it more context so that's kind of that but like John Doe come on I expect my llms to be more
creative than that uh let's use assert that actual HTML is equal to like I don't know that it it's like having
compilable code is is like my my Baseline if you can't generate reliably compilable code you're you're not terribly
helpful um yeah which means that their uh which means we will have to be the creative Parts all right so um we're going
to say our player name is murf bonus points to anyone who knows where that's from uh this is going to be our expected
HTML are we not in what the heck where did this quote come um so chat GPT for python will be able to compile and run
code so if they can do that for python um oh it came from my code oh look at that well at least at least it was
consistent so that's good we already found a bug um and this is why you want to do tdd because characterizing that would
wrong okay uh did I do that in multiple places or just there just there okay and voila it failed uh it should just be
because of the double quote and it is so let's go fix our code and now that should Let's uh let's since Cody Cody did a
graph oh my Cody you are just so wrong that's terrible how how do you even like what what led you to believe that after
reviewing you shared code context and configurations uh yes the colors are the CSS colors um that's the primary and
secondary colors icon oh wow it is just totally confused now it's totally confused let's try this again uh let me see if
I can get it to execute a command I may just have to do it here yeah see uh intellig uh automatically injected HTML
there it recognized it and I don't know when it does it automatically and when it doesn't I am whatever heris it's using
is it's possible it uses the this the variable let's see if I can execute the command against here if context oh now it
thinks it's go all right you can stop generating so this must be the prompt and the prompt is is yeah that's a that's a
great prompt if it detected things properly I don't um I don't know what to tell you three strikes you're out all right
so let's uh so let's do that one here so test um HTML uh so we'll expected so that's correct we want the notification
container want after begin fun um I guess I'll have to pull out the local and that should have updated back here and
that's fine okay now um sure except I'd like a different player uh the second test is for connected connected does imply
joined yes because you cannot connect to a game unless you have join the game right now at least as a player um when we
get to observers uh then you can connect to a game without POG and then we expect uh so let's replace our expected with
is log uh yes that's correct um except we have to generate a player from this do we want to do that or you just want to
pass that into the renderer I think that actually should be not our job works uh so there's a a television series called
Star Trek Prodigy uh that's where these characters are from that's the actual and so now we can and that's exactly what
we want it to time and that's all it failed on so we we are good to go change this um not sure I need to test this for
join players um I mean I could I could generate it sort of it contains for for all the player names can I get it to
write a test for just this one well is that work but hell and it's interesting that it did AR of sorry Cody uh is is
this vulnerable to cross- site HTML injection player name no because I will uh have prevalidated the in um certainly you
could put offensive do but there's no there's no uh cross sort um so let's go and do uh it's going to test it's actually
going to be more joined in this case it's joined and connected because I don't have joined um so let's basically take
this we will duplicate that um put that in be actually probably want to name this to just for joint player uh and this
is for jooin players uh variable that's and so let's say that player and then this is list of Cody got that right um
this will be correct modulo some perhaps new line let's insert a space see what happens this should not pass then
because we should be off by a blank line we are so now let's take it out wrong this is wrong and this is why tdd is
important this is not the output I want because what this will do is swap in this container and then completely replace
it with this swapped in container no what we actually want is that which you obviously not do yeah all right uh uh so
let's fix this um so we need to pull go here can I put it here and then can canate on the other end somehow that oh and
my for single join player is just totally wrong uh so this is wrong here we don't here and now we're just back to this
one failing because we're missing the closing Swap and and that's what's missing and there we go all right so it might
have been faster if I just did tdd up front um there was like several bugs already like I can't even be relied upon HTML
um but good all right so all that's uh all that's now tested um I think I'm pretty satisfied with it as is my only
concern is uh indentation is is likely going to be an issue going forward but other than that uh we've got our happened
where this entire set of files is not being added to get that's really weird I wonder if I hit a keystroke or something
because it thinks those are ignore oh yes I do terrible why do I even have do I even have an out directory I don't even
have an out directory I've got a Target terrible well that explains why I wasn't seeing those files in the in the in the
checklist because it was ignoring the maybe certainly looked like this was autogenerated though cuz like I never include
the STS stuff and I never include the Gradle stuff or exclude it uh and the view know all right seems better so if I do
uh so I think that's it for today so next time um what we're going to do is uh I'd like that I'd like the web
broadcaster to uh uh to Cache the notification the um the game page needs to do uh an onload trigger does doesn't if a
connects and then B connects B will get the list of a and b and a will get the websocket message that A and B are are
joined okay so I think that's fine I thought I might have had to do uh an a checks on load to update this unordered list
um which I might do anyway because right now I've got duplicate HTML generation I've got this being generated Through
Time Leaf as well as generated uh on the broadcaster side and I probably want to Jura um what are we doing anything let'
s out um yellow okay so this situation um where where where is the there it something oh player is null oh let's let's
stop the app let's get everybody back to the point uh let's clear that and let's go here yeah cuz red should have been
in there so right okay so I do need to uh so there's a little bit of a raise condition um the websocket connects we
connect uh but we're be I know the notifications we won't get so let's uh let's go back to the restart and so we'll
restart here says High green connect ah the order is wrong yeah so we need to add them to the session before we actually
tell the and this is this is where uh I'd want to test uh or I write automated so let's uh let's prove that uh so let's
go back to the lobby let's go back to the L here all right let's refresh the lobby we are yellow there's only one game
join and now we see that stuff cuz it's in the correct order so now uh yellow is us we just joined Mr red was already
there um we see the notification that we join this is updated we have green notification this is updated they only see
the latest notification and that's want all right uh so then next time so then that's that's working next time what do I
want to do we've got the waiting for game to begin uh so the waiting room functionality is basically done I says um now
we need to start now when do we want to start the game I to whoever is looking at the screen I don't think so I think
that's fine um button uh so then the start game button we click it it starts the game um and then uh yeah and then we
can finally uh get back to um our actual domain implementation uh so we got this um and we're basically at this point so
we can start the game and then uh start dealing with all the stuff around decks and players and how that gets connected
uh yeah so that'll be next time um so my next stream is tomorrow uh it'll be earlier than today uh what time did I say I
think I said uh yeah 11:00 a.m. Pacific time which is 6 p.m. UTC so a bit of an earlier start for all you folks in in
the UTC plus time zones um so we'll pick it up from here we'll we'll basically get it get into starting a game uh and
dealing with all that so thanks everyone for hanging out as always if you want to chat about this stuff um my Discord is
the best place to do that and if you want to buy a copy of the physical game look something like that uh you will get
early access to this online game cuz the online game will will not be free uh but so you'll get early access to it um
best place to take a look at that there's a video also of a walkth through of that at td. cards uh so check that out and
that's it I'll see you next time bye
