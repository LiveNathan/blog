# JitterTed's TDD Game： Online - #11： ＂WebSockets, CSS, Card Deck＂ (Java, Spring, Hexagonal, DDD)

**Video URL:** https://www.youtube.com/watch?v=hjoUL5H3s24

---

## Transcript

all right hello folks welcome to Tuesday earlier astd first hey there Benny hey narf anco anko you have to tell me how
to pronounce that if I'm pronouncing it wrong uh so welcome to um um I've lost track of what episode on where is it
there it is work on putting this game online um so yesterday uh for some reason seems like a long time ago um we the uh
waiting I guess waiting screen stuff hey suiga uh we got the the waiting screen um done where uh we update who's joined
uh as well as uh sending notifications when stuff happens here right oops that's not what I want uh this and see
something um yeah suige didn't even make good um I was kind of bothered about yesterday uh is the fact that we run ran
into a bug um for what was basically an outof order uh out of order processing so let's go here um mainly because I
don't have a good way uh currently uh to test this uh websocket inbound Handler so this inbound Handler is basically at
least right now uh is handling all websocket inbound uh requests um including both connections and and handling the
messages uh and the protocol that we currently have is that when someone joins with a websocket um so when someone
connects with a websocket keep got to keep on my toes for for using the correct terminology players join games uh
browsers connect websockets um and so there's code in here where um the actual connection that's established by the
websocket right now I don't care about because there's not there's no information that's useful it's not until actually
get the inbound message which is triggered by uh HTM X basically sending a message after we've connected um which is
telling us that uh basically they want to this websocket would like to connect to this particular game here's the game
handle the problem that uh we encountered yesterday was we were doing the telling basically the the use case the
application layer hey this player uh has connected to this game before we registered them with the thing that's handling
everybody's sessions uh which is this shared websocket session Handler I need a better name for it um so what would
happen is the we'd inform the player connector hey somebody joined it would initiate a broadcast um which would then
send through the connected yeah imple um but because the person who just connected wasn't yet in the session they
wouldn't receive this broadcast and uh this is generally the way I like these things to work is I want them sort of
one-way data flow CU I could have as a response to this connection basically sent something back through the websocket
um and that's fine if you're doing sort of HTTP request response but websocket is is just this pipe where information
goes through and it can get very confusing if I'm updating things this way as well as updating things this way uh so in
order to to keep things easy to understand um it's basically this oneway data flow so it has to go like this and then
basically like that basically back out to to the web socket um but if you add it too late then they don't get that that
that initial message um so that's what this ordering of these two lines really mattered and so what bothered me is that
I have no good way to test that uh which really there there there is a solution uh I just I I don't I don't want to take
the time to to to to do it just yet until I have sort of more more websocket stuff but it's basically um abstract stuff
out uh because this websocket broadcaster is a class I can I can substitute or detect or stub if I need to and same
thing with a player connector it's really I can't easily trigger this because um I mean I guess I could it's it's a
little harder to create some of these objects and really to test is these are these two methods being executed in the
correct order doesn't need all this detail right what does it use it uses I mean it uses the session for the for the
connect um but I don't need a a full-fledged fully qualified session uh websocket session itself is an interface um but
it's a pretty big interface and so I wouldn't you know I could probably create a there's probably a subass I could
create um like a standard websocket session but I but it's really like a you want to try and minimize creation because
you don't want to go down the road of using something like makito uh to provide a an instance that you can you can test
against and so this connect while it uses the real session for the purposes of testing in a sense did I get the message
that was triggered by this um I don't think I I'd need that or I would connection um because in fact uh yeah so that
would require some some abstraction that I'm that I'm not quite PR prepared to make um I'd have to uh abstract this away
a bit really what it's used for is is when we send it and again we might want to have uh we we we want we want to have
an abstraction there so we can test it without having to use uh something like makito so all that's to say is is this is
this is was on my mind um and this is where uh code in adapters can get really hard to test because you're working with
a library or framework that's doing IO that you don't have full control over that's hard that's hard to create test
instances for and hard to to handle when when things happen and so um you either use something like makito and go down
that nasty Road uh or you create abstractions um or you just test it manually and and do yeah I think this is a little
bit lower level abstraction um than something like a a venue manager because this is more about uh you know like if I
think about how would I test this code in fact really how would I test um you know that I got the right payload and
especially once I start having to dispatch messages based on the payload basically parse the thing and do routing based
on the messages that are coming in that's where I'm going to need uh some lower level abstractions around um routing so
this is this is more technical so even on the technical side we need abstractions to to help test us to still avoid
direct IO access um so I would need to figure out what do I need to abstract from these things uh that I could basically
pull out so that I could have all of this code working in that in that new properly and this is where some of the um
once you have that then you have some of the stuff around uh output trackers and things like that that that we could
leveraging um so let's go to jira and what did we say button so let's go here um so what we want is we want uh somewhere
to be a start game button um I think I can drop I can finally drop this now since I know the notifications are working
uh uh and I think I'll probably want the button somewhere here up let's see that's um put that there um we're all we're
all good so uh what like yeah pretty much a some kind of nullable inbound adapter um and yeah any any any messaging kind
of thing is is going to have a similar you don't want to create those raw very technical things um yeah so I'll I'll I'
ll end up doing that so yeah because I'll definitely want you know especially once again sort of as as the right now we
have one websocket message which is connect um there are going to be lots and lots and lots of of websocket messages um
most of them will be wrapping uh player commands but but things yeah so it's one of those things where it's where it's a
trade-off and um right now I don't I am I am ing on the on on the side of of trying to get uh something working over and
and it's a balance right I want to make sure that stuff is easily testable um but I want to use use just enough so we
need a button let's go grab a button um are uh good old primary buttons uh what do we want the button to do that's the
next question diagrams so this is the join sequence uh which we now have have working um so let's go and no control
shift n is not what I want I file uh so this is going to be start game actors and we can delete all that uh game starter
I really am getting getting close to this idea uh of formalizing more of a command query structure um but I'm going to
continue sort of treating these as tiny tiny use cases until uh I get enough where I can kind of see what I need from
from a command set so player one is basically going to talk to the uh the game files um and it's going to do basically a
post to the um not yeah I'm not going to worry too much about um about how how restful that endpoint is uh so that's
starts the um pretty itself yeah something like that also so it'll once it starts it's going to now start Gathering up
the information uh of the current state of Jonas see here I try to start early and you're late um you didn't you didn't
miss much uh so we query the state and then starter um brought CS uh basically refreshes the entire I mean this is this
is the big this is the big rants um so uh once they click the start um I'm thinking do I want to remove it Dom um all
these slots will be there when this dialogue comes up what won't be there uh are basically the cards well actually yeah
so when it when when this dialogue appears no cards have been the the deck has not been even created yet um so the the
board will be there uh the slots for the players will be there those containers um um and I'll probably have some
indicators cuz uh at this point because the game hasn't started yet uh players can still join um but I'm trying to I'm
trying not to I'm trying to like remember minimal like the there I'm just trying to think of the the the layout that I
want um let's go with with some kind layout and then we can start filling in these yeah so it's going to be something
layout yeah I'm going to prep the then at some point I need to display at some point the the back end needs to tell the
front end who's playing they well I guess I have to send a full update out anyway when they start the game so I'll just
set it up then all right so let's go uh let's go into the uh uh I'm not doing the Observer just I'm just thinking like I
really need the Observer because I will personally be an observer um so I'm not I'm not sure I'm going to do that yet
yeah the only problem with I so I could be a player um but right now I'm limiting it to four just for layout purposes uh
so I don't want to take up one of those slots and the other thing is I don't want to take up cards uh so I can't uh
prevent them from being dealt so there is some stuff that I am automating like um doing the initial deal uh so the
Observer is is really it part game hey there kiss killer um how how many lines does it take to do a basic hello world uh
you could look at the spring guides and you could say it's dozen so everyone I can recommend for for beginner stuff go
to the spring. academy there's lots and lots of good learned uh okay so what we want in here um we actually want a grid
um want a grid layout do I want a grid layout how do I want to do mle be uh a one to a 1:2 um yeah I don't need any of
these uh so we got mxo grid so let's do uh 3 um and then uh so what I want in and Gap four and then inside this div uh
so this is going to be the thing on the this side uh I don't know if I want to divide it 3 uh but for now that's the
easiest grid what the heck grid that was uh so what's the height on on these that uh I need to look at some CSS stuff on
on grids uh hey not raccoon um consider minimal setup where game happens in real yes uh I mean that's in a sense what
I'm doing I'm basically um not having the the code enforce any rules um it'll do things like like deal cards manual so
my assumption is that uh people are using this but they're still connected via some video conferencing like all right um
yes we're going to be suffering with with grid stuff now uh uh so I think I want specific Heights rows uh does a minmax
of zero and I actually yeah the hardest thing to deal with uh so I've actually as astd knows I've uh hosted a game where
uh we're playing where I have basically the camera on this this is actually a game that was in that we were playing um
the hardest thing to deal with is actually not uh the tiles and the board and the ponds uh and the rist counters it's
the cards so just getting the cards online that if if uh is is actually my Prim my of of all the the goals um in terms
of staging things that's the first thing uh and in fact it's the action cards that is the first thing cuz that's the
stuff that's been hard to manage because like it's hard to uh to manage these cards and have the people who are playing
see see them all um so I am definitely that's in in my head of uh sort of what I want the game to to do so dealing the
cards having people be able to see their own hands um be able to to basically manage the cards on their own that would
be a big step forward in being able for games so does let's see template cols order um just trying to figure out the
yeah I I just want to to to to stretch out the space cuz I want to get some some sense of what those are um so let's do
this so what is it grid grid template rose right that's what this is uh and so this needs to be then um flow if I do I
don't understand the grid template unless the outer thing is not taking on the full height that's probably the problem
um so I need this to be right all right well I'm going to have to do some more figuring out because I'm not uh I'm not
understanding the the grid stuff um so that'll be the placeholder for be um so this will be column right or no I don't
that would help there we go so grid and then grid calls three uh um there we go so I was missing the grid part so now I'
ve got these rows where I want them so this is uh this is player one player 2 player three board here then uh so that's
column uh and then what do we have here deck Oops I did not realize I would be doing grid layout stuff otherwise I would
have prepared uh so action deck what else we got uh and then in this section is area uh except this needs to be inside
of hey there cus welcome here and uh so that's going to be we're grid okay okay so now I can thinner so now I can see
sort of the boundaries of of stuff uh so we've got a bit of um so we got our our Gap here so that's fine uh so we got
our our decks here um your play area and then below your hand later yeah uh once I have this set up then um actually the
the dev tools make it uh really uh really nice to see more details about the grid but sort of that takes up its own
space so I could evenly space these uh so we can here uh wait a second that um and we'll do a call span two um just
let's go back to this okay so this is basically our layout do we need anything below the board no we we'll um so I think
that's it that's our basic layout way I don't need as much padding that way board uh so then what we want in player one
font um bold uh clipboard it yeah since I have um Macky which is a clipboard memor memorizer uh that's my my commit uh
okay so we got our player names um we're going to want uh basically a place for their cards I'm just going to display
them uh how do I want to display them right now I guess I can just further um so this folks is how you get like 35 divs
nested uh so this is that that workspace does looks bigger yeah um uh definitely stuff is going to be be templatized
yeah um so I I really uh I I have been going back and forth in my head around um using timely fragments uh because all
of the information I'm sending across is going over the websocket and not HTTP um that means I have to manually invoke
the template um a lot of the stuff I did with Ensemble timer was all the string string manipulation and the current HTML
stuff I've got is also like I feel like to the the the time Leaf stuff um I mean I can invoke the template directly uh
and I can the time Leaf template generation and I can give it a context uh it's just then I lose type information and
it's a little harder to test um I'm really leaning towards basically creating my own component system CU you know that's
what um uh uh Thomas sh's uh uh view component but he's using a different template framework uh and it's more HTTP
oriented uh so doesn't doesn't really work for me either so I'll likely create something on my own so these would be um
I mean I've created visual component Frameworks before so what you know nothing new here I mean there's not a lot of you
know there's not a lot of customization I need uh but my goal is to be able to have components like a card and then it
can display itself um in in different ways uh either overlapped like like here or spread out like this of sort of HTML
CSS for that because those are just images like most of this the hardest part about this layout is I mean this is not
the final layout anyway this is just where I've left my mockups um is the larger layouts but because once I have the
spaces the the um I'm a little annoyed at why workspace and hand are not the same height uh CU it looks like I would
have issue yeah it's not a Justified content because you can see the container is uh different um that's going of annoy
me so let's go see if we can figure that out let's go inspect so what have we got here uh is it lying to me because it
feels me like my eyes say these are different heights except it's saying they're both 72. 75 yeah let me turn off the
debug and then we'll we'll be able to see it so this is the overall three three uh three columns um this is the first
column each each vertical section is 148 pixels I think it's not taking into account um this header because this whole
thing is 148 and so 74 oh it is overlapping why is it but I want it to take up the full but I think that that's already
going to um I don't know what hfit is it's suggesting it I don't see it in the in the docks um that doesn't seem to do
anything or at least not what I want uh so right um I feel like I want the fractional units uh but it's not taking up
the full height I don't understand the the fractional that what was it stretch feel like it's it's just not the this is
this is why like CSS is so frustrating for me because I just don't um interesting the line content stretch and I feel
like I've got exactly this and it's not doing what I want uh yeah I was going to go to chat this is pretty much what I
had all right display grid uh um the vertical head of the whole thing is fine uh the nested grid is also grid fraction
so it did 100 vertical height yeah the item was just for formatting important yeah okay so just changed the um I think
that's what I'm because I've got so I've got the the grid I've got grid template rows right that's what it's suggested
grid template rows 1fr 1fr um it had a gap grid so the container did an auto and a 1fr so I wonder if that's it uh cuz
my so I wonder if that's how it did it uh grid yeah I agree Jas yeah so so that's that's that's apparently how how to do
it um basically this container here somewhere here here it is um we needed to divide it further into two parts um so
that it's Auto which is however high this uh this header is going to show um then take the rest of it and divide it into
into basically then take the rest of it is the rest of the fraction um then once we have that then this part here now
takes the full height and want uh what happens if we remove the Align column stretch does that do anything yeah so
apparently that is some so we can justify the content towards the end uh for the whole thing or um or I'll just leave it
but now I can I that yep I have to uh pipe the sound so it goes directly uh out instead of going out of my speakers into
the into the microphone all right so um so this is our our basic layout there uh I think this is now good enough so
player two is basically just going to be duplicate of of player one uh let's convert this to sort of proper CSS I'm I'm
using the Tailwind playground but I'm basically going to call this div uh this is a player player this is the player
grid um player container yeah probably because the noise suppression is is uh is trying to do its work I'll pipe it
correctly later uh so player container um uh display header and and then we here here and then uh this is the um player
what do we want to call it player okay uh then we want um which div is this this is uh these so this is a display grid
and what else do we that's interesting uh looks like display grid interesting so it looks like it already divided the
grid into as many rows as I this is the all players container so column uh let's uh let's do replicate the other stuff
so up so what's the difference between this and not having it it looks like there's absolutely no difference uh so if I
don't have this and I happen to div then it basically just divides it as as many rows as there are so basically it it
evenly divides it unless you specify it otherwise learn something new every day so if I put this back then player four
basically says eek um so I'll leave it at uh if we ever have more than three other players then that'll be handy okay uh
and then for uh the board here um four um which I probably won't our I probably won't group these into to one thing
anyway uh call it last column because I can't grid there we can turn that off um some kind of borders would be nice so
let's add a little bit of player uh thin uh like something that looks a little bit more card likee uh so let's go to um
card so let's grab of margin uh so let's put some space here um grid uh Gap big uh so that's the all players container
the player container padding yes so I'm cheating here I'm basically applying using the tailwood CSS inside what do I
have in my go um we'll do something similar then yeah I don't have anything for that so what else so here uh so our
works so we're going to want some hand oh it tighted up too much don't do that I want these on separate rows uh so this
is class uh player workspace this is actually other player it here's where I want to rename it's uh I want this to be
other player container and this header all right uh so this is all header uh what other other oh I should just cut and
welcome all right uh so we got other player workspace which we would like um I think also um order padding uh actually I
don't want a this that looks then other player style uh where is it here other player hand uh we'd like some space
between container it looks like these are the same I same here they go uh web socket with spring um so you can go ahead
and and look at uh the code base um it's not necessarily going to be easy to understand uh CU it's a work in progress um
so there there are two projects that you can look at uh there's ensembl which has a lot of other stuff in it uh The
Ensemble timer code does the the websocket stuff um if you're doing this for a school project you're probably not going
to understand the architecture is my guess unless you're you're pretty experienced uh so it's not um as as
straightforward uh the current project I'm working on uh the code's there it might be a little easier to understand
because the code is small um but it is using uh HTM X on the front end and it's not using any protocol on top of
websocket so that's another consideration um lots of folks tend to default to stomp uh so B which is basically a simple
text protocol on top of websockets um I'm not sure I have a that yeah so I I'm not using stomp because um I don't need
it uh I basically am making up my own my own protocol um stomp is fine though I used it in uh the older code that's
actually inside of of this project uh uses stomp but then it uses view on the front end so it may not be a simplified
enough example either um stomp has the advantage of of uh but for me it gets in the way because I want to communicate
directly with a raw websocket on the front end using HTM X so HTM X doesn't support using something like stomp uh so
that's actually the main stomp but if you're not using HTM X if you're writing the front end code yourself uh stomp is
is great there's couple of standard frontend libraries that that support that um some people use socket IO I don't see
the point of that I think that's you don't need that overhead uh and so if you're writing your own front end then then
go ahead and use stop that's probably a better way to go um I just don't have an example uh I have a Discord so um that'
s a place uh you can ask more detailed questions there's channels dedicated to to Spring boot um so I don't care about
topics um I'm kind of I'm kind of handling it myself because uh topics would be myself um it's actually something I need
to explore because it would be nice if HTM X support websocket extension supported stomp um because the topics would be
useful because uh then I wouldn't have to manage myself the communications that games but right now um I'm not worried
um let's just apply these and see what that looks good because it'll actually wider uh so that's that's looking pretty
good um yeah my pleasure so let's uh let's let's commit that uh let's I think I think that's all I I would like to
convert this out of out of Tailwind I remember coming across utility um yeah tail window uh so let's say that I want um
that and I think chat we GPT we can say thanks uh display grid top bottom left that and come back here and so this game
uh padding top and bottom it could optimize that not sure why it didn't optimize that uh because this is basically
padding uh top right uh where am I missing a semicolon oh you I always have to laugh at missing semicolon it's like well
if you knew it in uh Gap half R Max width 80 CSS yeah it worked out well for the JavaScript them that that's weird why
is this Json like I don't that's really weird uh I wish it would combine that stuff here oh to put it in react that
would is that really what this expands to the Box Shadow maybe I want to keep around those let's see CSS components
utilities uh all right let's just grab this and let's put it finally back into here no not that uh into a game we'll
come back to the sequence um so what's going to be fun uh I think div um where is my CSS is uh so I want to link uh I
want a thh ref for that close uh a uh CSS and then uh in here I basically want in debug is unused yes thank you I know
that uh let's see correct that looks correct there's our button um I want that to be green though uh why is the right
okay so that looks good white font semi bigger okay there we go all right um now let's uh before we throw in all of the
HTML that we just created uh so we'll commit that uh and then we can close this for now um going to take a break uh when
we come back from the break we'll will drop in the full game uh and then we can start figuring out what uh what we're
targeting um the initial thing that we'll want is um once the game Stars query the state it's going the component that
is for the um for the different parts of of the game boundary like that uh so we'll figure that out but we'll take a
break or at least I'll take a break you can do whatever you want uh shortly all right and we're back uh so now that um
we have at least a a template placeholder for all of the pieces of information that we're going to need uh sorry just
what popped into my head was what am I going to Target um and with HTM X you can Target IDs uh but you can also Target
classes um I don't think I'm going to want to Target classes though it just sort of crossed my mind is like oh maybe
that'll be so I don't have to also have an ID but each player other players going to have going to require different IDs
so that's not going to work okay uh but before I do um let's see if we can get this to I think I'm going to have to
change this this stuff which is because it's basically a modal into an actual modal um but let's stick in where's the
browser there it is let's like so that's all great except uh this thing is all the way down here uh that's not what we
want um what we want is that actually to be a popup so let's go figure out how to do panels that's that's not what I
want uh I want overlays dialogue uh not sure why it requires HTM um well let's grab this uh copy that go into our
playground where we already have this thing all right Jonas have a good night thanks for stopping by and dancing so uh
should we put this first this and I don't need all these comments cuz I'm not uh see fixed inser oh so this must be the
the back ground so it basically dims brighter fixed inset zero screenflow y Auto okay and we'll grab this is a bit over
much we can just say this uh I don't know what text that is so I matters just TR to see where that is uh we don't this
yeah and so then um okay so that's that part uh let's we uncomment this is that going to work no how about now out let's
let intellig uncomment it copy and then recomment it and then we can stick it in go and go and so then uh do I delete
this or do I just say style display you say HTM X delete I'm not going to disagree what do you what why why do you none
I mean my thinking for deleting it space yeah that's that's my feeling all right so um you see hide I haven't even
looked at HTM XX delete like is it just I will want the placeholder yeah I will want the container um because I will
want to have a place in the Dom to uh show future modals I see um so what do we need to change then here uh where is
that so okay so that's the edge of our uh relative Flex H screen we don't want this so we want basically everything
think I've got one too few divs too many divs what's the problem here uh no I need one more clothes another one there we
fun uh are the rainbow dips uh I used to have a plugin rainbow brackets I don't think I have that installed anymore I
think that might be standard issue oh look Jerry themes is updated again um now I wonder if they're ever going to
upgrade refactor Insight bummer uh yeah I got some updating to do I do that later yeah I think the coloring must be but
must be built in um let's put it up here where did I put it here it was at the top and then the game screen was okay
awesome so then uh to make this disappear um I could just say uh all right borders what happened to all my good borders
oh I wonder if it's not pulling oh it's not able to apply the Border stuff right uh because that's not being processed
uh so we want to do is one there we go so those are that those borders let's I think I I guess I'll keep these as
separate I was thinking do I want to combine these classes uh but I think I'll keep them separate for border let's see
what it comes up go yeah had a background of slate did that not get converted did I not paste it oh it slate uh so
background slate what are you that there we same for this there we go all right I uh I didn't have borders for anything
else all right so that's the modal dialog currently it's hidden uh and so now we can start thinking about so the game
starts um the information we need is who are the players um so we'll um so the identifier for this is just one uh so we
got other player name one two and then similar okay so uh so we post to start the game um we grab um basically grab the
players and then we um we need to broadcast the player names the does a game start I guess we could populate it before
we do game start so we do game would be nice to assign Pawn colors uh but I think I can get away without that for now uh
I wonder if I just should just group those together into a single component and just Target other player uh so then I
can transform each player into the component yeah that and there's some Loop here I forget how groups I guess I could do
grouping yeah uh so group oh can I actually just say Loop n yeah there we go so we need a component that takes a player
and box um what do I want to dive into first so I could either do sort of uh depth first um basically just render the
player's name um or I could start dealing with all of the card decks shuffling uh dealing for okay so your choices are
uh and then I need to take another uh quick break uh your choices are full render for player um so that that's the all
the way to game grab the player render just the player name because that's all we currently have um or dive into game
and start doing all of the stuff around cards and dealing cards and things like that so vote early vote once because
that's all you get uh and I'll be right back all right looks like we've got uh dive into the domain and deal with the
stuff there all spoken um well even if you had voted as you would have basically start game uh is going to have to do a
bunch of things so let's and we this uh let's do a commit um um so basically uh we'll defer sort of the UI aspect
because now we know what we need uh and we'll go back to the to the behavior of the game um so let's take a look it's
been a while since we actually looked at that stuff So currently game only has uh create or reconstitute and it's got
join um and we can get the the list of players so uh the next step is um we need our action card deck so again sort of
focusing on what is the minimal game support I need in order to for me to personally host games uh and that is I need
action cards so we've already got ACH code from our earlier implementation so let's see what we can there uh so we've
got um we've got Card Factory let's take a that and so uh we've got um playing card which takes a playing card
definition and playing card definition is here so these are the the playing card definitions uh but I think I don't want
to take it um so the first thing I need to do is deck so our uh default deck Factory this and this defines uh basically
the cards that are in in the action deck so um when one of the uh important features of most games that are card-based
is you have the the pick the choose pile or the pick pile um and then the discard so um so the discard pile then when we
run out of cards here we Shuffle this and those become new cards to pick from um and so I treated uh the deck as a
component that had both parts so if we look at deck let's look at deck so what is deck deck has two things it has a draw
pile which is a Q and A discard pile which is a list um and then it has a shuffler and uh so what happens is when we try
to draw um if the pile if the draw pile is empty we basically uh replenish from the the discard pile which shuffles and
then adds all the cards to the draw pile and then clears the the discard pile so what's nice about this is when I create
the card uh when I create the deck uh I just have to add them all to the discard pile and the next draw will will
basically do all the shuffling for me so I don't have to shuffle it right right up front um what's nice is then I have
one place where where I do the shuffling so I think I I'll keep that design because I like that that's nice Deck that so
this is going to be really interesting cuz I it's been a while since I've sort of scavenged code from another uh another
project um like once you pull on one of these objects like it pulls in a whole bunch of things so this one its
dependencies are on uh does this depend on anything this there's no no other dependencies here so directly uh so we've
got which depends on a card Factory it I got random card shuffler which is a shuffler place uh this it should be a port
and implementation um but I it's funny I I kind of remember creating uh these factories um it I'm not sure I'm not sure
I'm I I abstractions so I like the deck abstraction um I don't like the deck Factory abstraction maybe I'll end up there
again anyway but right now uh it feels like a bit much uh the way the the the old implementation was deck was fine
because it relied on the on the uh on the port card shuffler so card shuffler itself is just an interface so this this
should have been in a port um but you're right actually the card not it should not right because it can't rely on it
because it's in domain H so I remember how we dealt with this in in the Blackjack game I might have to do it the same
it's a bit annoying though I remember being annoyed by it before and from a strict concerns it's kind of I mean it's
it's too bad because uh yeah basically it it's fully encapsulated and and and and it can player yeah so what if I if I
uh continue to be pure about the separation then it means that when a player draws a card the code that does sort of the
shuffling is then in or at least the code that causes the shuffle to happen I mean it's not terrible um because the draw
is going to happen based on the user doing something so it has to come in through through the application layer actually
let's dig into the start game game deal so would it be game player uh deck yeah I don't know if it's if it's better even
from a testability standpoint I'm not sure it's better yeah I mean the way uh the way it would work with the pure
separation um is when the draw uh before it says draw it says can draw um or basically something like you cards um or it
can even just say something like if draw pile is empty shuffler um the problem is is is here in the initial deal I mean
we could assume that the initial deal you never run out of cards um and then we don't to worry about it so it be
something like uh the game tells the player um player draw to full from from deck so I guess it's if we make an if we
sort of say um testability is not harmed and capsulation is improved uh by allowing by relaxing the constraint that that
domain cannot access even indirectly so for me as long as test ability is not um as long as it's not like IO uh even
though I sort of put this onto the io access so let's let's look to see what that um um be not in the domain be in the
application game shoe actually do we do we do that in the blackj game I know we Shuffle it here uh uh we create a random
deck uh we actually don't reshuffle do we we just we just run out of cards and that's why we had the shoe for for
multiple decks um so yeah that's right actually we didn't deal with it in this version of the game did we do that in the
other one I remember implementing reference yeah and this is called only shoe yeah so I'm now I'm wondering uh here we
haven't had an orange stream in a while an orange Ensemble so oh it's indexing don't index let's change the SDK don't
index that so where did we Shuffle uh we may not not done that at all in this Universe uh I'll close this one for now
yeah so that this so it's not this one yeah um I kind of I kind of want to do it cuz I feel like the the fully
encapsulated Deck with a shuffler that's given to it Purity and the other way just feels like interface it the interface
is inside of would be inside of the interface um but it would not be externalized uh and I'm I'm I'm in favor because
it's not like there are so there the only reason to have mult multiple implementations is for testability so create null
would uh so yeah the embedded stub yeah it's I mean technically it's an interface but you're right it's not a way
because then uh things like this are going to be much easier um the player just has to draw until they're full and they
know when they're full they know when they their full um cuz likely it's going to be uh and uh to to action deck draw
and then uh do you what to get the embedded times oh the nullable dice roller yes well everything in yacht we did
together um cuz the old one had I'd have to look back and see what CPU uh so way back that was a score what uh so we did
the dive first yes so we inlined the dice roller into the game roller um and so basically we use the random wrapper yeah
so it's you're right it is exactly the same thing um so we're going to go that way because I think that that that's a
lot better and so we'd have a crate null we can do a little bit higher level uh I likely want to specify CU here it was
easy because the the sort of the the abstraction is literally D dice um and here are the dice that I want cuz I'm going
to check that these are the in the game uh we're going to want cards this this might be the deck and the deck has a
crate null about how we want the cards to be produced we either want want them shuffled or we want them in a specific
order so I think that's the level of abstraction that we want so the nullable uh with the embedded stub will be the deck
right because basically it's do we use shuffler or do we use the order yeah in internally it's going to wrap it's going
to wrap here Shuffle it um the configured order or it will it will randomize it yeah yeah I was I was thinking more what
is what is the what is the creating all parameters the creating all parameters are going to be the action cards in a
list of action cards in this order um internally what what gets wrapped uh is right because you always want to wrap the
the the hardware yeah that or let's start doing um Bo having tdd game and tdd yacht in my list here is is going to
confuse the heck out of me uh so since we've already established that this deck is a nice abstraction we're going to
basically rewrite it um to use to use the nullies so let's do that uh and we'll start out we'll start out generified I'm
wondering if I want to copy the whole thing uh so let's see so what do we want to say about a new deck um probably that
has cards in a specific order yeah this test isn't going to help me much so let's uh let's go start um this one we might
use uh we'll close that and I think this we'll we'll use in another form uh so let's go ahead create okay why do I keep
forgetting what it is it's oh it's option n there it is um but directory let's go to our real code which is down here so
this going to be in our domain create deck and then we'll create a test for this oops uh and we're going to start
nesting is so it's interesting that it it that it pulled that code from the test from that other code I was just looking
at um I do kind of want something like that but it's going to be a much setup so we want to say that um when we created
deck uh we should be able to draw all the cards in the deck card uh I called them playing card but um action card uh we
pretty much just need the and this might turn it into an enum I'm not sure right in my previous design I had enums for
the definitions and then the cards themselves uh but then that leads to the title being a string when it doesn't really
need to be but we'll we'll start there um all right Astra thanks for thanks for so let's go ahead and um say that uh we
want action card we'll go ahead and create that class right now it basically won't have much in it um other than uh we
won't call it name we will call it uh title test uh so we've got deck of action that uh and here we're just going to say
deck it's like it's now Cody's now been poisoned by the other code I was looking at which is really frustrating my my my
llm has been poisoned by its training data um I'm just going to create an empty deck actually and no I take that back
cards uh and we're going to basically is I know we're going to need proper uh action I kind of actually want to make
this an enum to start out with so let's go to our playing card enum and we're going to change this to an enum and get
rid of all this and put this in here uh um eventually we're going to want some of these aspects of it which tell us uh
which tell the game when you draw the card where does it go most cards go into your hand uh but a sometimes they go into
the Inplay or Tech neglect area um when you play them sometimes they go into the workspace and sometimes they get
discarded immediately and that's what these are yeah okay uh and then we will need to expose title yes just like cards I
don't know where Cody's getting that like we'll just create a few cards so we'll say um yeah I guess I don't know where
it got draw to from um it it must be Uno because I don't know anything else that has a draw two uh so we want action
card um we'll add a good one has to wonder what the training that okay so we've got action cards we've got cards uh so
we would like to do a deck. draw I don't need your comment Cody um and uh we would like to assign card return null and
so our first assert that oh man you are so infected by my uh I don't even think you uh do we need to test the non-null
yeah that would that would be fine I would probably wouldn't even need more than two cards um and then yeah basically
draw four times and we should have two of each technically I could put one card in there and I should be able to draw it
twice um but two cards might be easier close but no guitar predict all right so this is the most basically uh well if I
had few I would add fewer cards so for the for the uh if I'm testing that when I run out they they Shuffle I would use
fewer cards in the first place so i' only have two that um all right so this is the most basic yes so now I think we um
what do we say uh draw pile is a q so is uh right because that should be a link list list are there other
implementations instead I'm really not going to worry okay yeah so the question is is what does this Constructor mean uh
um they should not be going on the que uh they should be going on cuz that's how I I designed it um basically add to add
to discard so uh a new cards uh the draw pile is empty so let's let's actually start there um cuz I don't want to add
these to those I actually want to add them be to the discard pile draw we want another test um I'm fine with keeping
that one so we're going to have another test which is uh new okay so here um where it doesn't matter that's our deck uh
so the question we want to ask is assert that so that'll fail because it's false the other one all right uh and so now
empty yeah that's all I need for this test okay so now I can go on to this test um card so let's uh that we already saw
that test fail so um say discard pile add I think I have to add that code so empty so I can start by saying uh stuff
draw pile remove this will this should actually now still still fail because draw pile is empty but we're trying to
remove from it and no such element um and so replenish from discard is now um what did we do we just shuffled it and uh
do I want to assert that the discard pile is is now empty I'm okay with doing this okay so okay uh I don't know why you
made that public now it would be convenient to have a draw multiple cards um but I'm not quite sure what that's going to
need what that need is going to look like from the application now um I'm going to inline this cuz what I want to do now
is this should be right code ref do I want to assert that the draw pile is yeah that's true I could I wonder how much
more I wonder how much more readable that is that's probably a little bit more pass okay uh so let's say instead of that
we're going to say card that's funny that's close you're close draw assert handy draw end cards uh I don't know I could
just say draw cards cuz I don't think this does what it does list of return a mutable list I don't yeah in fact does
intj warn against that it does very um we could have used an instream and then map to drawing cards but no this is a lot
more clear all right so this I'm just wondering why oh right so I'm wonder I was wondering why why is this test this
player connector test taking so long and now I softly is slow it is because it's slow uh and I remember reporting this
issue I have to go check on what happened um but like this test is noticeably slow if I run it by itself like you can
see it see the spinner um like it's it's it's 3/4 of a second and it's all because this takes like half a second uh it
it must be um I I remember looking into it I don't remember the details uh but it's basically yeah it's it's terrible um
and I think I I think the last time I used it I ended up taking it out because it was too slow time oh 3.24 they're up
to 3.26 I don't think they've fixed anything this area um right I think what I did is I moved verify that's what I did
so let's let's do that because I know it's only half a second but it's been annoying me all day uh let's call these
actual player and this is actual game create the field uh take this out of here and put it here out take that out take
that out uh and game and this is actual player yeah boom like the whole thing took less than test yeah lesson learned uh
I want to commit and I think is that it for uh oh so uh the reason why I moved it to call uh then it's harder then it's
a little harder to tell what actually what actually happened so if I do the direct I mean it it sort of doesn't matter
uh I'm already doing an assertion here so it just feels more consistent to to do it here and I did the soft assertions
because I wanted to see if both matched but I think this is this but yeah I don't think there's much that it's kind so
the uh the other thing is if um if I do the assertion in in this method that I had the soft assertions before what
intell will show is that actually this failed when in failed if nothing else it's it's more reason all right so I think
we're done for today uh tomorrow we'll continue uh working on drawing cards from a deck um so got draw we've got um so
what's the next test that we're going to want is we're going to want so we're draw already repes repes replenishes from
the discard um we're going to want to be able to add to the discard pile um and then we're going to uh make it nullable
are uh so create action container able to draw and with an embedded stub for we stub is it really a stub it's not really
it's like I mean cuz it's not a stub a stub only returns values It's actually an embedded fake I'm not sure let's see so
because it's two ways uh it's it's it's an embedded not modifier I don't I don't know I'm not sure what to call it it's
though because basically you give it give it the cards yes if I say give me um well actually that's a good point what am
I going to use it uh it's an embedded Stu if if I've I guess it is an embedded stub because when it's when when I'm
using the stub it is just returning the cards that I configured okay thank you I was still thinking like I want to
shuffle it in this way I think that'll that'll and that'll become clear once once we start implementing that uh so once
we nalize the deck we will have a deck uh that is shuffled we'll draw a full so that gets that that gets the cards in
their and then players uh before that I actually so if you draw a red card a media gets area um we probably don't need
it until uh so once we have that we will be able to draw cards for each player draw a hand to full um if along the way
any cards get automatically played those will turn up into the technical area uh then we can switch back then we'll
basically switch back to working on the UI so that'll be tomorrow uh so thanks everyone for hanging out and helping out
as always I appreciate it um if you want to get your own copy of the physical game right this thing uh you will then get
access uh early access to the online game otherwise I encourage you to join the discard if you're not already there and
you can ask all your questions and bring up various discussions about this or anything related to to this stuff
otherwise uh tomorrow same time same channel uh and we'll pick it up from
