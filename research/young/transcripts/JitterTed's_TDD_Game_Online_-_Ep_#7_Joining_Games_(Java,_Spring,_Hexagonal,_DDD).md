# JitterTed's TDD Game： Online - Ep #7 ＂Joining Games＂ (Java, Spring, Hexagonal, DDD)

**Video URL:** https://www.youtube.com/watch?v=32GaBRX2L0o

---

## Transcript

so yesterday uh we started talking about um what happens once a game is created uh and then a player so a person which I
I think I'm going to call member um it was clear that that that's been a confusion between player and person um that
they are two different things and I and it it's clear that it's very obvious for me to Mi mix them up so uh I'll
probably re rename that um because I don't like user um but I like member uh what again that's what I use is in the
terminology of of ensembl so I'll probably go go that way anyway so once a um once a member joins a game they are a
player so members are the the things that have subscriptions that have accounts that have profiles that have names um
they're the thing that they are the entity uh that has a a user login uh so they are the the long-term thing uh which is
again very much like ensembl you are members and then you can join uh ensembles and then you are a participant or uh an
observer spectator so here the only I'm basically and so when a member joins a game they are a player and the first
thing they will see is is something like this basically a modal um that will sort of show you know uh you joined
somebody else joined somebody got disconnected uh and then a big old start game button and so when the start game button
gets clicked that starts the game um uh and then things will things will go from there uh I use the term user login
because that's the concrete Spring Security name for things so there is a uh user login authentication um but I'm going
to subass that and I will be calling that a member but there's there's a core user object in there I will be avoiding
using that term because that doesn't have meaning that's a technical term that's not a domain term so so the domain term
is member uh which contains information that comes user um yeah no I'm not going to do tdd game user uh although well as
the technical implementation possibly yeah but as a the domain object the the main value object no sorry domain entity
CU they will be an entity um then it then it's then it's member yeah all right uh so let's click there um I guess let's
go ahead and do the rename because we shouldn't wait any longer on person uh we will rename this member badly chosen
Aggregates or aggravates I love that I will be quoting um is that the only variable used oh it must be person ID for all
the others no no no just do the refactory refactoring I don't know why you're offering to preview it just just do it I
didn't say preview just do it uh let's go to person ID because this those no no just do the refractor just do it hey you
yeah remember it is um do we have any other reference to places wait that I'm surprised it didn't fix it didn't change
that that um let's do a file change um I honestly think I can do a search that uh are those all lower case 22 matches 11
matches 22 matches where is person uppercase ah uh so what we want to do is preserve case did you know that this was
there this little hidden thing here um so what nice about preserve case uh is that it will preserve the case so if you'
re doing a case insensitive search which is what I'm doing uh it won't change things to lower case if they're in
uppercase so for example uh which one is in uppercase this one so if we go all note that this m is uppercase to match
what it originally was as person I feel like sometimes like uh uh there should be you know huge Aver vertisements like
use this feature and it's such a um you know it seems obvious like of course you'd want that that seems like otherwise
you have to basically do two search and replaces search for the uppercase version search for the lowercase version um
but it seems obvious after you know it already exists that this isn't always available in all situations in all
applications uh all right so let's run all our tests I hope we haven't broken anything but we may have uh look at that
we didn't break anything let's run all uh looks like all the tests passed so let's go do another search for person
person no longer exists in Java files how about in uh HTML so that's a problem uh we'll have those uh so of those we'll
just do a replace uh which me leads me to believe that that is not tested but that's the UI we know yeah um uh when
spring Booth 330 comes out although I don't really have to wait for that um but I do want to start doing some uh HTML
whether it's HTML unit um I might also play with playright uh we'll see but I do want I do want some tests for that
because that's right now a hole in in in my testing that I'm totally upfront about that I have not been uh yes I think
we're down to the one disabled uh I basically put aside The View loader so that that'll that'll come back um oh game's
not used created game can repository uh sure why am I holding on then uh so let's run on the test again and then we'll
we'll do a our visibly useful work uh so renamed uh confusion you got to be committed to industry or if you work in this
industry know all right um player has member ID and player I'm going to swap these because that feels uh let's see so
player player player they're in the ones in the game uh member ID that's just a record I assume player ID is also just a
record yep uh all right so let's go let's go again um where where we processed the join uh right now we're making up the
ID uh and we want to redirect to the the game in progress so the game in progress page is the is basically this uh this
will eventually be the the uh and this model will be on top depending on the state of the game so this is the page that
will have the websocket the HTM x uh all that so the next step I I want to take then so someday this pain will be useful
to you that basically does this although now this is per member ID and member store uh so let's go okay yeah I think I I
think I basically need to finish out sort of this code uh before I can go to the game in progress because right now this
is this is hardcoded um so this is going to require me to now implement the the member store um am I doing event
sourcing for members so members are certainly a yeah you got a problem with comic Sands that's the default hand sort of
hand it's not comic sand I'm not sure what it is it's actually more just handwritten um so member turns into a player
when they join the game have uh they get stored in store okay there so I'm not sure I need to say as a player cuz if you
join a game by player oops what the heck okay uh I probably am have going to have to go I didn't want to do a full
search and replace but I think I'm going to have to so let's uh let's do a replace all so this this already makes clear
what what that transition y all right um so let's go look at the test for this which would be not that so I think what I
want uh is to make clear where that member ID comes from because right now it's like well how do I know it's this one
this is not not obvious from this test no where do I see in this test that number 42 uh so K let's see so I will always
be able to get the principal or an authenticated principal um I can also directly using Spring Security also have uh I
could have the member injected but that's the domain I don't want to inject here I think I'll keep it simple for now and
I'll do the lookup so sort of the way I the way I think of of what I'm going to do is uh look up member in member store
Cody um and then once I have the member then so does join so the so the question I'm pondering is does does join take
just the member this join certainly takes a member think no this might take the member as well so uh yeah so I I done
member ID because game should not hold on to a reference to member as an object because it's an aggregate however um
when it creates the player the player needs to know the name and so it needs to get that um because the question is is
when this call comes in so this call this is a post from an endpoint uh I will know a principal right now principal has
just username that's all it has uh I can use um another object the quest so the the thing is is I need a member ID so
how do I get the um I could just store that in in on the page site I've got the srf so I'm not too matter well that's
the thing so so this is this is what what what I'm what I'm uh s going round about so here if I get principal I get
their their name and so I can do a lookup in the members store using that name the question is is now I've got a member
object do I basically just pass in the member ID if I do that then here um I have the member ID and they join the game
and then here when they join the game uh we basically create um where is that uh here they basically we create a player
and all we have is the the member ID um so so this is this is always interesting it's like so do I store the name inside
the player this is this is what I'm I'm I'm wrapping getting wrapped up about uh wrapped around the axle as or uh do I
store the the member's name in the player or do I fetch that when I'm going stuff and this is really minor and I'm
probably overthinking it um but basically when uh when something happens so when we display these events or these names
in here um do we get those is it already in the player object and then we just have to transform it because it's already
a string um or do we just have IDs and then we do a lookup when we translate it view yes AST I was I was just thinking
about what if I want to change my iname that would lead me to the player's name player and if it's so if it's just name
then I think I can just pass that in as parameter and then I'm not worried about passing it a member object um so and I
saw your other comment asra I'll get to that um so here I pass in basically member ID player name and game handle uh and
then that would just be passed down in into player and then at some point there'll be a feature to to to play you know
what would you like to be called in the game and then that gets passed in I think that's probably the most
straightforward way to go if it turns out there's a lot more information I need to sort of move from Member into player
I'll deal with that at that point more um do I need a Game host abstraction I so I I think it this is I think that's the
game Joiner right now um and the the player Joins game um application use case that really is what what this is doing oh
look 44 not found redeemed dark right so I was actually pretty amused um there's uh uh a course on accessibility um that
I'm taking and uh inside the course you can choose between light mode and dark mode except for one page where it's only
in dark mode and I was I was amused because it's like you offered light and dark everywhere else except there it was
kind of funny uh all right let's go to what did we like did we like Violet I forget what we used last or no not storm
Oceanic I think Oceanic I didn't like so it's either Jerry dark or or Jerry Violet anything dark Works um let's go with
Jerry dark what plugin is it bug me about ha that's funny it wants me to upgrade the new I like the fine uh let me
update it this won't what no I'm not restarting for that too bad all right so let's go um let's go to Violet it's like
it unloaded the the plugin because recently there was uh over the past year or so there was a change in the plug-in
architecture and you could for some plugins didn't have sort of certain types of features um it could unload it and then
load the new one so it loaded it and anyway no not now okay what else are you bugging about no go away all right me set
the timer for this there we there we go okay so we will look up the member in the member store we will hand in the name
um and that's what we're going to do so that means I need um I need a member store this is not where you buy members
this is where you find them uh so back to my my earlier got is just an ID and I'm about to add on a name uh so I think
I'm going to not worry about event sourcing this yet cuz I saw that cuz when I do need it it'll be easier but regardless
a member ID and a name are going to be required so those are going to be in the Constructor anyway uh so it won't change
anything um so how often is that used well it's so I think uh we'll modify this uh no this is name that record I mean
eventually it might be a class but for now let's let's make it a record eventually this will will this this match now I
can convert it no why won't you let me convert it to a record I had a heck with you let's just do it not sure why
intellig I must uh I must be missing something that I'm not sure why manually that should be the yeah don't know why I
didn't do that uh um that was just clean up that was just the okay uh okay so now we've got that and what we'd like to
do name that should be Teresa uh player doesn't have name yet so we'll so player is only called from there that and
we'll create a field for all right yeah B usually uh it does I I I don't know there must have been some mismatch between
something that I wasn't seeing and that's why I couldn't do it but it usually offers it if it's as simple as it name so
this will fail because I don't along we are not so that's right right we got our hardcoded thing here so let's pass that
along um player so that goes here we'll have to pass it up from here uh and then we apply it in our apply which is here
uh so player join so the player modified so you it thinks it's not used unless it's not directly referenced no it's
directly reference right here all right Jonas I'll I'll reset the timer uh no it's not just in test cuz I'm doing that
right here um in the apply method that's interesting I wonder if it's not picking up that it's used as a a uh a record
intell um cuz clearly if I if I go to usage it takes me here but it doesn't seem to to joined um oh no it's in CED of
course and cue it right here so it's used right there I have found the record the find usages of Records is has still
been a bit uh weird um but that's that's really annoying uh okay um so where do I get the member ID I get them when they
join right so if we if we back up from here we get to here and if we back up from here we get to here which is where we
know we're going to need to add the name um all right so let's let's start pushing out then so so when we inq a new
player joined two so is it player joined and then uh name or is it just player joined with name yeah I'm thinking one
event to as well um cuz sort of as a as a constraint we can say a player has to have a name all right event um let's
just add it and we'll do uh name uh actually I should do that as a signature someday intellig will finally fix the
layout problems on these dialogues someday I know it's a hard problem uh so this is a string ler name default value is
default player usages it must have had a a bad index inq where it didn't actually change the anything anywhere again why
when your tools fail you it's really heck even if I didn't provide a default then it would it would basically uh it
should still it would still put something there like it would put null or so what time is it uh this has been so so
change signature so I I have a feeling it's very much related to the fact that it thought it it wasn't used and so
therefore couldn't find the usages in order to change them that's what I suspect right so if it's looking for usages and
then for each one basically fixes it if it can't find the usages that's a problem let's see if we everything works now
no that's not true let's see if a rescan of the project indexes index nope uh and I don't think it's a dropped restart
uh uh let's just restart because we um yeah I don't think I selected Violet let's see yeah I just selected dark yellow
let's go to Violet that's a little let's see can we convert class okay so now it finds usages so it's definitely a
record usage problem um and I've seen this before where it gets confused about finding usages of that uh so now if I do
a change signature here and I add um the type of string uh that's player name and default player refactor now that
actually worked uh and so now I can convert it now it won't let me convert it back into a record uh oh well this time I
know why because this this isn't stored so let's go ahead and and create a field for that uh and then let's go ahead and
uh create a getter for it uh and then let's go ahead and move that up now this is interesting so here it's now
suggesting that it can be a record class note that this method is not in the style of a getter it's in the style of the
way records do Getters this one's a getter but it seems to be recognizing that it's a getter but if I change this record
well now it still offers to be record class so I don't know what's wrong there but now I can convert it back to a record
uh um and it's kind of hilarious that it basically gives me all this again so lesson there is convert your record to a
class do the refactoring and then convert the class back to a record which is not the fun way to do it um but now we at
least get get no that's not nightbot newsletter I guess maybe I should it newsletter all right this okay so we're
getting closer we're now getting we now have the default default name so let's go and propagate that out close that it's
so frustrating that I can't freaking find it oh I know dark Mode's notice um I'm I'm giving you some bonus dark mode
time uh so where the heck did that go default player name right there uh so this needs to come out as a parameter so
let's push this out as a name uh and now we can go and find the callers to this so here we have default player name uh
and all right test I can now put in this name here um although it should actually get uh no I have to copy it so I can
basically do member player yet oh it's just called name right that was Cody's fault I'm blaming Cody cuz Cody suggested
player name but pass and it passes uh let me just make sure I probably have in some places uh default player tests right
member has so me the member's name name gets copied into and becomes the player name later on there'll be an option what
name would you like hello astd what name would you like in the context of the game by default it will be your member
name but it could be something else but right now I'm just going to be copying it but in the context of a member it's
just their name whatever your Let's tests uh let's actually pull this out irrelevant and then we'll change this to be
irrelevant go to this test class we'll thing uh actually this one we will keep name uh what was I looking for oh yeah
default that's fine this one I want actually to be paid attention to so we'll do the same things we did before which is
player player name no player name uh this one will be again a tuple of that okay uh let's run all the tests I don't
think anything should change there then commit excellent uh let's just make sure that default player name is only one
place which is there okay great uh so let's do player name to player right get on your sunglasses because I'm about to
to turn turn back uh let's do that you've been incoming all right um so now uh now we've got uh we're still going to use
principal to look up the member we'll get their ID and name that's what's get gets handed in here uh we still want to
get away so I think the next step is basically get rid here um because what we'd like is is um this is the up
implementing so this is a little bit of an interesting situation like I know this is a single access single abstract
method therefore uh I can use a Lambda here um but I can't seem to figure out how to ask intell uh F1 which tells me the
interface I'm implementing which is principal I know that uh but I can't hit info tell me what the interface name is
that's unfortunate CU I'm like what what is this actually here well I can just expand the the Lambda body that doesn't
help I can convert it to an anonymous class and that tells me that basically it's it's get name um which is the username
uh and the reason why I was curious about that is because this is not the username this is where is it actually this is
the username I was thinking the lower case but the lower case that's the password I username there we go uh what does
extract Lambda do um does extract a method reference which basically creates a method and then you get a method
reference which maybe is useful but that doesn't help me Define okay so what I expect then in this particular test is I
wanted to look look up in the member store this thing get its member ID and then have an Associated name because that's
what members have uh and use that game in order for that to work um game Joiner is going to need yeah so that means I
need to define a member uh here I don't want to use 89 so that's a members is there's actually another name I need so
this is the name name like hi there what should I call you uh what's actually needed is the username so right now I'm
just sort of sketching because I realized there's actually two names that a member has uh what's basically the key that
I'm going to be looking up is the one I get from Principal get name um and then there's their hi what should I call you
maybe nickname is the right term there um required yeah I don't like display name cuz that has connotations of it being
displayed um I'll probably I'll probably go with is is probably what I'll go with so all then uh this name is actually
nickname is that all lowercase I guess so preferred name I don't like display name even though that's how it'll mostly
be nickname uh but then we need in addition to that well it's not an alias it's like there's a minimal amount that you
need to uh to sign up um and aot it'll actually probably be more than that uh because this is the name that will be used
sort of uh like how to refer to you when I send you an email um how do I refer to you uh basically in outside of game
situations and also then your default situations um it won't hold all of the information that I might require you to
authenticate because I'm going to be uh externalizing uh delegating authentication to somebody else like kind or one of
those need because what I get from authentication is your username right I know you're this username usernames are to uh
in fact they may not even be readable like I might be using a service where it actually gives me some uid like uh thing
that is actually not not a name um so I'm going to keep that as nickname this is the username uh this is the uh or
authenticated name um we'll call this offn name because this is the name that this is the name this is this is the name
that I will get from authentication so if you authenticate through gith Hub it's whatever your GitHub username is if I
authenticate using uh uh kind then it'll be whatever username you used there it may not even be a username it may be
kind's unique identifier um but this is basically what's going to be the key to look up in occurrences uh so I'm only
using it in two places so this will be an easy fix um let's do that uh let's add it as the um do that we'll go to our
usages so that's um is that okay so that's let's do a all right so let's go um so this is our storage of uh members of
that's the nickname becomes the default name or when joining the game uh and then whatever so we use this basically to
cross okay all right so now um now I've got a member they have the three pieces of information that we require uh when
they join the game so we got to basically create uh some way for them to uh so this username uh name equals off name
that's what kicked this off is this is name um and we want this to contain exactly 89 uh I could ask for the player name
at this level I don't I don't see that's necessary um okay so now this test will clearly fail because we're going to
because now uh now we need some way to look it I'm not going to make a pass by just here uh so we now have enough this
and so we're M mapping boy I don't like want do I want something else I would but I'm not going to do that yet so this
uh maps to member and then this is uh member map uh member uh so we got find all I don't all and this is offn name this
is basically a wrapper for a map but that's fine because this will eventually become a true Port uh that slower save uh
and then I pass in the member store parameter and we'll go ahead and create that uh now spring is not happy that's fine
we'll go ahead and make spring happy config hey look at that Cody knew what I Cody uh uh sa asked why did I choose to
name it store as OPP post to repository because um two reasons one is uh certainly at least for game and eventually
probably for member I'm going to be using event sourcing uh so it's less like a a it's not a reposit it's still a
repository of Aggregates um but store for me provides more meaning around oh this is storing events um the other reason
is it gets very confusing when I name my port member repository or game repository and then the Concrete technical
implementation is also repository because that's what spring data used and sort of that you know I think it it's
unfortunate that they're using a domain term for a technical implementation but it is what it is uh So to avoid
confusion uh I'm using store so for both those reasons that's why I'm using store because when you see if we saw game
repository and then game jwc repository adapter and then game the boo repository it it gets still so all right so now me
it has a member store um so now if I do uh instead of this let's pull this out this is member um member store uh find by
off name principal get name uh and we're getting a member so we want yes store is definitely uh quite overloaded in the
uh number of meanings yep I think I'm going to have to do an else actually I do need to check for a correct so this will
fail um we should be the ID now uh but it'll fail because nickname and that's exactly how it fails so it fails is
predicted uh now we can basically get rid of this get rid of this this comment uh and this comment and then player name
becomes member dot no not player name stop it uh nickname that should not pass excellent all right all right join by uh
so asid asks how does a new member become a value in the store uh when they whatever the onboarding mechanism is which I
have about um likely the for likely for a little while uh it will be I haven't seen you before uh so when you log in
it'll give you uh ways to log in and if you register and it's like I don't know you I'm just going to put you in the
member store eventually there will be an onboarding process of how does somebody become a member uh either you've bought
the game the physical game or you've bought a subscription to the online right those are the io free tests let's tests I
thought that there might be uh store uh 404 depends on um where you are located if you go to this site uh you'll get the
information on that it's about $100 for the game plus shipping uh plus uh so this fails uh unsurprisingly because um
when we join uh there's no principal or at least there is which is this fellow um so let's get at least a somewhat nicer
error message um all right astd have a good night thanks for hanging the that's the member store that's member um that's
throw uh not a runtime exception we'll do all right that thanks Cody oh yeah I won't forget the timer I wanted to get
that exception message in there all right so now if this when when that test fails I'll get a better oh interesting um
because it's an authentication failure uh it's actually not as useful because spring interprets this in why didn't the
timer flip goes all right so now we've got to make sure that uh this username so I'm going blue username um what we need
is to make sure store no member store that now come on Cody at least give me code that that works there is no member
member um but it takes more information than T member ID I don't think the member ID is relevant here so we'll just say
work yeah it does great so let's go Jura um well we haven't gotten to here yet um because now we got basically joined to
to sort of be correct so now we have join uh and now it's the actual person who is logged in is joining um which means
we should actually now be able to see uh what we weren't able to see last so I'm going to switch to the browser there I
don't have a dark mode for um the app I guess I could create one so blue is going to log in uh there are no games we see
that it recognizes us as blue we'll host a game player count is now zero uh if we as blue join the game redirected uh no
because uh we're not putting this is the question to as's earlier question which was how do people get in the member
store uh we don't actually add that so in our uh uh security config we basically create these users I think what I want
to store um this does not actually give the member an ID eventually that will be the responsibility of the member store
but that's not currently what it's doing uh and I don't want to add that to now so here looks like I so I guess let's
add the member store as method uh cuz then in here what I can do is member store save uh this is not username username
um right now this member ID needs to be unique field yeah and this is all temporary until we get that onboarding
mechanism for uh sort of registering new new members so here in a sense what I'm doing is I'm creating the security uh
aspect so that they can log in and then I'm also saving them in the associate the logged in user with the member out and
this is all scaffolding that uh that this is expected um because we don't have a game in progress page yet uh but now if
we look at the lobby we see player count equals 1 if we log out and log in as something else someone else uh and we join
game we now see player count is and that's what we weren't seeing before because we had hardcoded the member ID so it
was always the same member joining regardless of who was logged in now it's actually who's logged in in fact if we
inspected the game itself we would see both blue and yellow are are in there um and we can host a new game uh I guess we
can join multiple games do I want to allow that that's a separate 7 so now this says player count of one so now yellow
the yellow user is in both both games I guess it's not my problem if you games okay so that all works uh let's go do a
commit and then I'm break so we'll take a break uh when we come back from the break uh we can finally start looking at
the next uh thing which is now that I have members uh We've identified authenticated uh we have so we know who they are
we have their usernames they're in the member store uh now when they join we want to start working on the game in
progress page initially it'll it'll just be here's who's here uh but also then start to set up the web sockets so that
we can see dynamically as people join um but first we'll take a break and then we'll go ahead and do that and I'll
switch away break uh now that uh we we are having our members join the game and we know who they are and we can
different shape between different members now we can go ahead uh and start setting up uh showing the game on a page so
let's start from the outside uh we're going to create uh a new HTML page uh so what would we like we'd like sort sort
it's kind of alert like uh but it's really an overlay yeah here we go a I don't think the alerts give me no yeah the
slide overs are sort of coming from the right that's not quite I want either yeah um and the notifications are just
going to be sort of upper right stuff yeah I'll probably use notifications uh in game once the game is started for
things like somebody connected or disconnected now so I think we'll just grab something like that that one thing that
would be nice that if they had I don't know if they're working on it but they have have a playground and it'll be nice
to sort of copy it into the playground um it's funny actually this layout is actually almost more what I want that's
that uh so let's take out their image got that so instead of that I probably want something mockup uh so we'll say
something like H1 so class text XL uh thoughts image uh uh something uh let's say so and something like that um and then
in this section over here this is going to uh I don't know where that line is coming padding that's the shadow offset
for the whole color hey swegi I am baffled where from it's got to be a border top but I'm element oh The Divide gray
that's what it is yeah not the Divide y uh which just divides stuff it's so if we say um yeah that's what it is thank
you sue instantly helpful uh so let's grab that okay I think I want a bit more uh assesment height screen oh that's cuz
these are doing it yeah I and let's see what we got uh that's all thing and let's go ahead and create page uh so the C
CSS course and taking is is actively not Tailwind um which is toally totally fine um not tailin he does use some
Tailwind for certain utility classes uh but in general he's more concerned about um sort of to me it's much more
important to understand CSS because once you understand CSS then Tailwind is just a different way to do CSS uh where are
my resources uh all right so let's go let's copy this one this is our game in progress I want to call this game in game
i' been going back and forth about this cuz it feels weird to go to game in but uh so we're going to get rid of all of
this this paste all that in um yeah I mean you really like you you can't use CSS effective you can't use Tailwind
effectively if you don't understand CSS and I think Tailwind is is fine for sort of I mean different people things I
think if you have a component system then it's fine because then you can just push all these classes up to the
components um but it does get hard to manage if you're copying and pasting a lot of classes uh you're probably wrong
yeah I mean in this situation it's it is a game view it's just there's this dialogue but that's still part of the state
of the game so um if I was going to have an intermediary page uh of like waiting for game to start page and then it
redirects you to the game then I might have a game in progress page and then I differentiate with the two but since this
is one page that's that's fully Dynamic uh then yeah I'm definitely going to need to redirect to a specific ID yeah yet
pretty soon uh so what I do need here um because I don't have Tailwind project grab I could just grab the generated SE
lot like I don't think I'm using all these um but it's not that huge so I'll just that's a very amusing um that's
amusing what it what it suggested there uh let's go and create uh resources static so create a new file static uh game
all right so let's see if that previews correctly no uh no because it doesn't understand the same thing um so let's do
href uh static game CSS and then wave all right so we joined we redirect to to to the game uh what we want to show there
uh is let's clean this up a bit uh so we're going to this Li is going to repeat um so that means I don't need these
others so the LI is going to repeat so we're going to do on this we're going to do a th want um and then for each player
uh we're going to have everything this player I have to figure out a way how to change it so that it displays that this
is you when it's you um I'm not going to worry about that right now um notifications okay I can just leave that here for
now uh I think that's all I need so we're going to need player and I probably want to change this icon because right now
but I'm not going to worry about it right now yes eventually I'm going to have to assign pawns to players uh and
therefore colors to actually I think that's it for now okay um is I need another controller uh that will serve up this
endpoint and convert the information which is and this might become a link so that way it's easy to invite someone um so
game view handle so then this is actually uh from the game view views this adapter is going to be uh this game let's try
that um so let's go ahead game playing controller and let's start writing a so we'll grab uh stuff like this I wonder if
I should have a base and so this is playing okay yeah I mean it's it's like this is going to be the same for all of them
this is like oh this will probably be the same except when it's not uh um this is certainly different but I could create
my composite annotation to to have to provide that class and then this is like oh this will probably be the same except
no maybe not and so it's not worth it uh especially since the class is just so small so this is going to be a uh get
request I'm just fascinated um by the suggestion of Cody nope would you like to try again Cody there you go now
apparently um I don't know if I should say this out loud uh apparently the free version of Cody is supposed to have a
limit of 500 suggestions per month I according to the dashboard I have exceeded that so not sure what's going on here uh
sure that's what we want um that likely is not going to work later on but for now that should be need um except we are
going to want that import static method what the that's really weird why is it not uh suggesting uh that will for an
exception yeah I think I I I feel like I would have exceeded 1,000 anyway like the dashboard shows you're at 500 of 500
and apparently it's not counting past that um because clearly it should be know yeah definitely a a a live template uh
or just a code template for this for MVC tests would be really handy because I'm always going to want to import these um
except in uh I think it's 330 we get the new uh Mach MBC assertion uh which is the assert J version of The Mach MBC
stuff and so I think I think that changes so maybe we don't need it um it is 330 right uh think I can get rid of this
page rc1 uh when is rc2 coming out I have to calendar because they recently changed and I'm pretty sure it was post rc1
they changed how they were setting up the mock MBC for let's see uh would this be in Spring boot this might not be in
Spring boot uh this might be in Spring uh yeah so uh they renamed it to NBC tester uh so let's see what that looks like
that's the Json path I actually don't care about that because I don't do Json path stuff uh let's see what that looks
let's see move response body directly because essentially you do uh mock MVC class um but it looks like you still have
to do the perform get which I guess makes sense like there there really two parts there's the do the thing and there
there's the ass assert on the thing uh this doesn't help us with the do the thing being like the gets being static which
is actually the part more so yeah the setup is is still is still pretty similar I have a feeling this is this is still
in flux because it doesn't look like everybody's in uh let's see today is the Thursday um I guess that's going to be in
there or I guess technically that's in Spring framework I mean the issue is closed uh but this is in 62 right so 62 of
the framework is not in Spring 3 boot 330 which you can absorb a different version of the spring framework uh if you
need it uh all right anyway that was an interesting tangent uh it doesn't help us get code written though uh so let's go
ahead and run this test this will fail cuz we've got no endp do a not what I was hoping Cody would Supply what oh right
the template uh is accessing stuff that's not in the model that's fine um so yeah uh if we commented that stuff out we'd
be fine I'm going to just say that's fine because it's clearly working uh I'm not going to do much more here for this
test I'm going to call it passing um I guess I could return something else but that wouldn't help so uh let's move on
then to the next test uh now an interesting question is can you look at a game that you haven't joined well if I can't
get it to pass uh with this test passing then I've got a problem but in a sense I need to put that other test on hold
until I get this to pass because I need to put stuff in the model so if you want to think about way it it's failing for
the right reason let's put it that way um uh I think in question uh so this is done you might have missed it suiga but
everything's now or at least oh it's no no person um yeah um uh okay um I just realized and I mentioned this before and
I realized that I hadn't put that in here is this can't possibly work uh well I could basically I don't have a game
handle uh or an or a game ID uh in fact games don't have IDs we're gonna have to add IDs oh wait the aggregate has the
did I add the ID to no um so pretty quickly although likely IDs no they will certainly not be able to oh no um so one of
my uh goals is to not not so or I guess one of my non- goals anyway I don't want to restrict players too much because I'
d like people to be able to experiment so you will be able to do things that technically are against the standard rules
uh in other words I am not going to have at least in the initial version who knows that might be configurable I'm not
going to enforce rules so if you discard five cards when you're only supposed to discard three that's on you if you move
your Pawn to places where it doesn't make sense that's on you um because in in a sense I'm I'm very much emulating the
physical board where it doesn't prevent you from doing anything uh and that has two benefits one's less code uh but
actually more importantly too is it allows people to to experiment uh and and come up with different rules so if you're
a player you can do whatever you want observers though should not be able to do I I might even want to have a special
Observer view imagine I can imagine doing this over a zoom and then the shared screen is sort of the Observer view uh
actually no I don't think that works because if you're a player you kind of need to to see the screen and so the zoom is
only adding on the sort of the people's social aspects so I take that back um so there's an observe review because for
example uh if I'm facilitating the game I'd like to be able to see the board but it doesn't mean I should be able to to
push stuff around and yeah yeah event sourcing um what's nice about the event sourcing is it also in addition to sort of
undo it also is like hey I noticed you did this and this and this let's talk about uh about that now there might be a
couple of different levels of commands um so there's the event sourced events uh I think we'll we'll see how it plays
out how much those match sort of the the the highlevel game actions um they're probably going to be see uh either way
one of the one of the nice things will be sort of for as a retrospective you can sort of replay the game fast forward uh
have sort of you know I could imagine a timeline view and things like that so there's all sorts of fun stuff you can you
can have but um we're not there yet so I'm not going to worry about the ID right now uh let's get this to to pass uh and
then we'll probably end for today so um playing game is going to need access to uh right now it's just going to retrieve
the first store be nice if uh Cody was a little um that's the game oh no not yet we want to uh no not member store want
game join want uh so we created the game member has join the member has joined the game they are now a player and now we
can yes game um then we need uh playing game yes you're smart enough to figure this out except actually that's not what
I need I only need the game store right now oops and not uh we don't need the page we just need it to load the model so
we need to that uh and now we can say assert uh actually it's easier if this is a map so we'll convert to a map and
contains uh so it contains a game that do I have a game view I do oh right cuz I just display that uh oh this is a
different view um this is a different game View want I think I want to rename this I'm not quite because it's like is
this a value object which was I think my which was my used yeah it's only being about okay so I think this I'm going to
move this um so I'm going move this to uh adapter in uh game Lobby view because that's what this is about uh and I might
want to subdivide the lobby stuff into its own package but for now I'll do this to disambiguate that uh then this is not
game Lobby view because we want just game um all I'll leave that for now all right so let's create game view this is
going to be for record and what did we say we needed on at this so we said game view has a okay and then we need player
view that's also going to be a record that's also where it's going to live um and what did we say player view needs uh
name let's start there um could the lobby and the in progress game be put in different bounded that um because they do
have certainly uh very different concerns the lobby doesn't care about anything that's going on in the game handle uh
and probably what state it's players um but all the other stuff about players in their states uh that is not needed for
the lobby so could certainly uh likely see a a read view so uh or um I mean that is that was the intent of the game view
loader that the game that the game view is all the lobby needs and that that's a projection of the full game event sourc
it's so I think it is a separate bounded context um but that's of course that doesn't mean we split it but I think there
there certainly uh certainly would warrant a a read a read projection of the of the game that's that makes the lobby
easier because I don't need to retrieve the entire game right once the game is started the lobby like nothing from the
Lobby's point of view cares about that like how the players are doing where they are how many what what cards they have
all that kind of stuff is is so bounded contexts give us the opportunity to split it doesn't split um and and it also
depends on like what's the split so certainly uh maybe game status might even be a better word than game view um the
lobby only cares about game status which is a tiny projection of of the actual state in that other aggregate um so there
certainly uh so yeah so they are different I'd probably say they are different bound to contexts um and so it certainly
like you could say the Lobby's super busy we've got tens of thousands of games going on we want to optimize for that and
that could even be a separate service right God forbid we have a a separate micros service for for the lobby um but I
could totally see that uh and that would be using different all right so let's uh let's do this um certainly this is
going to be null because get attributes going to return null so we'll go ahead and run our IO free tests yep and now we
can put in the model no add attribute um game view view uh we'll just put in a um I think we can now say sort of uh is
equal to view actually might as well just ask well I'll do that here so new game view um nice try on the game players
but that's not going to work um what we want you players and I think this is just going to be players stream map view uh
so this is player new player uh so this will certainly fail because the game view is just has an empty list of match and
there's no way to get the players to match either because this basically doesn't have yet a reference this again goes to
how do I want to request the human readable name is is is here uh or do I use the internal identity fire so the upside
to using the handle is I already have ways to retrieve that store the downside is it's a bit of a ver Bose thing but
that's that's not a downside really uh it's slightly guessable like there is a limit to the number of words used in but
unless I use a A ulid or something like that uh an incrementing sequence of Longs is is much more the game Joiner I've
already got the game handle so it' be very easy to redirect to that so let's do what's let's uh let's let's actually run
all the tests though um because I think the test that was that was failing for reason could pass why isn't it passing
view uh argument type mismatch oh because this is concurrent model that's not there we go so now that test that was
failing for the right reason is now passing for the right reason uh and I think uh this is a good place to oh no K
kademlia is raiding with a party of 43 and I say oh no because uh I am but welcome thank you for for bringing your party
here I appreciate it um but I'm basically wrapping up uh I'll give you a little bit of insight into what I'm I've been
working on so I'm working on an online version of my uh physical tdd game which looks like this um so I have the
physical version and I'm basically con creating an online version because we're not all in the same place anymore we're
all remote uh or often remote it's play uh the physical game when you're remote so uh this is sort of my mockup um and
this is what my current mockup of of the online version looks like I nowhere near this I'm just uh building up some of
the inside stuff um and it's uh Java spring boot on the back end and for the front end it's HTML and CSS uh eventually
I'll be pulling in some HTM X for the websocket interactivity um but otherwise no front-end Frameworks or or anything
like I have a Discord as lots of folks do uh I have uh whole bunch of people there who are uh who talk about the stuff I
do here on on my stream which is test driven development um Java spring boot refactoring all all that good stuff uh uh
yes the spring server it's all server side generated HTML uh and so uh um uh I've been doing a lot of bunch of a bunch
of playing around with HTM x uh with one of my other uh tools which was uh a timer uh and all of the HTML is being
server side generated and you can't tell the difference because browsers are really good at taking HTML and rendering it
and the amount of HTML I'm sending over is on the order of like K like not even a th a th000 bytes um yeah so actually
previous version of of this online game that that I started some time ago was vue.js which I think is is nice uh but
don't need it CU like everything here like I'm not sending the images across each time right there it's referencing
images like anything else um and so it'll just be little bits of HTML uh and so I it it just uh will be be really nice
and the other nice for me the the main reason why I like it is it then makes it so much easier to test because then the
server is the true source of Truth um I know I said true there twice it's a source of Truth for the state of the game uh
I don't have to worry about like synchronizing between browsers even though I know there's Technologies to do that and I
don't have to worry about updating States like the knows it saves it it knows it and it broadcasts it uh and so it's
it's going to be just just right and it makes it then really easy to test because the server is the only place that has
state that changes and so that's easy to test so I'm I'm all about testability uh here and so um I I I really I'm
looking forward to like we're just at the point where I now have enough code um where the next step that I'm about to to
work on on my next stream is basically nope not that uh this which is um when you've joined a game it's going to show
you uh sort of who you're waiting for who's who's available uh and then you can actually start the game and start
playing and so the point we're at is building this page uh and then the next step is is hooking up the websockets so
sorry I won't be doing that today um but uh another reason to join my Discord is to to be notified of when uh when my
next stream is so my next plan stream to work on this is Thursday uh so I'm usually streaming between uh 12:00 p.m. and
300 p.m. uh Pacific time which is what 7:00 p.m. 10 p.m. UTC uh uh so if you join the Discord I I basically give you
lots of advanced notice or you could just follow me and I think what we'll do uh is uh we'll go raid uh bald bearded
Builder um so we'll pass along whoever of you from uh cademia raid uh hung around we're going to we're going to pass
pass it along so uh that's all for for today um let's uh what that was so you're welcome to stick around for the raid uh
otherwise thanks for hanging out and uh we'll see you um so I'll be streaming tomorrow as a pair stream likely with with
Mike uh that'll be here on Twitch and YouTube uh and then the next solo stream uh is is Thursday check out the Discord
for more information about that and about all the other stuff that that's going on we got a book club coming up so um
find about that uh otherwise let's
