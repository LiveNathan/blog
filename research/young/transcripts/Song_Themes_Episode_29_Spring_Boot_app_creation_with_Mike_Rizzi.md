# ＂Song Themes＂ Episode 29： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=XEppm1QR8ew

---

## Transcript

all right hello folks and welcome to episode 29 uh working on the song themes app how's it going Mike doing well doing
well we're almost at the end of our fundraiser on the radio station so been a a fun so today's day eight so we they're
doing nine days so nice it's super fun but also exhausting yes I imagine I imagine so so last time we finally got to
start working on persistence not the database portion yet I think we will be getting to that um pretty pretty pretty
quickly uh but we basically had done some work around um some refactoring so let me uh show sort of diagrammatically
what we've been doing here so previously we had um in so this is our our hexagon for those of you who are not too
familiar with it in inside here is our our domain and what we started out with was basically no persistence so this
stuff wasn't wasn't there at all uh and song Searcher actually held on to all of the songs as they were added uh through
uh through the the UI um but what we've been doing is basically extracting a song repository so a a port in the ports
and adapters AR chitecture uh and we refactored that code into turning what was basically an inmemory uh cache for it
into an inmemory repository um and uh what we'll probably get to today is then Implement a real database adapter that
will talk to uh we'll talk to postcript uh not postcript post postgress postcript is something completely different and
a little bit old well so is postgress but yeah I remember I took a an independent study class or was an honors elective
class in type setting languages so postcript was was one of them W really interesting Xerox had their own language which
did clearly did not succeed I think it was called interleaf um and there was one other anyway um nothing to do with with
with printing uh uh we're going to use postgress clearly I have not had enough coffee this morning um and so this was
our line of refactoring and I and I I this is something that um I really think not a lot of people understand the idea
that refactoring is against a boundary um so for example our adapter didn't change and the behavior against the adapter
didn't change the um the song service didn't change because it's still talking to things it's what's below sort of below
the line between song service and the domain and other parts that's um that's what's changed and so uh we didn't have to
fix a whole lot um but we'll sort of see see where we're at and um uh one of the things we'll start seeing is now we
have these these outbound adapters and we'll start seeing um we'll start clarifying that oh well in order to do these
use case layer tests uh we will now have to have this test double um this fake uh in memory adapter will will be our
test double um and that's the nature of of the different kinds of tests so so one thing I I talk about with test double
architecture is your domain layer tests you never use test doubles because you don't need them because there's no IO
it's just domain objects uh but when you get to use case layer tests you will need test doubles um but you will also be
able to substitute in the real thing and those tests should actually work in exactly the same way uh they will just be
slightly slower because you're using the the real thing uh but that's one of the really interesting things um about
these use case layer tests and this is what people often say oh I don't need to write lower level tests I'm just going
to write integration tests they call these sort of integration tests and yes you could actually go quite far with those
kinds of tests um but you're going to miss out on on stuff in the domain important things in the domain that are just
more annoying to test at at at this level um especially when you get into things like constraints and and uh pushing
things into a specific State I think it just gets really awkward to do it at that level anyway so that's a that's sort
of a quick intw of of sort of you know what what our design is where we're at um so why don't we switch over to your
screen and we can look at at I realized we should um we could probably check off this jira 62 um what do you think I
think so I mean we still have that dependent column thing that that uh right I was wondering is the dependent column
thing part of skipping yeah I think that's that's separate yeah I think all of that was about having a header row and uh
required columns and and things like that basically the data being linked to to the header rows and that's all that's
all done are we're skipping that we're skipping this we even have a thing for is so I think we're on 88 um and we were
going to figure out what that meant ah uh so let's let's run all the test just to to to see where where uh where we are
see if we have any failing tests point and because it's all tests it's a little bit great so let's take take a look at
our inmemory there so we create the the inmemory repository um we have a way of of so we hold on to the songs but we
also index them so that's our our inmemory version um method so that's just a static me method to create and so we've
got inmemory and so we see there on 43 we have our ad which uh overrides so that means it's implementing our our uh song
repository Port interface so we've got the ad and then uh the related one below that is is the theme so one of the
things that um a uh a real database does that is not perfectly emulated here is if we modify a song and so this is what
we sort of ended with last time if we modify a song If you scroll up to the to the field to the map def definition so we
have a list of songs these are um so both the list and the map are have object references and that means that anywhere
in the system where that song is changed this in memory song repository change um that's not how databases work if we
change something in memory the database doesn't magically get updated although things like hibernate try to sort of kind
of do that um although that's a that's a separate separate issue about whether it should or not um but that's not real
database Behavior now if um generally though right at least at this point songs are are immutable we don't currently
have a way because we haven't got to the functionality around song proposals and changing songs we don't actually have a
way to change them uh because we've defined it as a record and so records are are immutable um and so that means this
isn't a concern yet this will be a concern later so when we do uh update songs and change them we'll have to figure out
what do we want to do with our inmemory copy do we want to convert it to a mutable basically a mutable entity or do we
want to um do something else uh which part would you want to make immutable the because if it's a list of songs and the
song itself is an immutable record MH would we then also make the list of songs immutable such that it forces a no that
won't do it never mind that would force you to not change the list or you'd have to rebuild the list entirely yeah so so
what what the issue is here is if if a song changes um we need we need to be able to explicitly save it right um so that
if it flows through into the database uh and the database tables get get updated um so we'd have to make a a version of
song that maybe not a version of song but immutable we'd have to basically replace the reference to the first song with
a new song right and so currently we only have an ad method that assumes that it's a new song um we do not have a save
method which would up or or an update method which would update an existing song um so probably this is okay for now uh
when we get to sort of modifying songs um it's really interesting CU cuz you know is is song an entity yes in fact it's
an aggregate based on how we we defined it in our uh initial uh event um but uh how that's structured in mutable right
because we can basically say let's create a new record based on this this other record making these changes uh and in
fact um that would be much easier with uh what are called wither wither methods that are uh proposed for for future
versions of java to make exactly that process easier um but it's not it's not terribly hard to create uh a new basically
a modified song um and so we'd end up with a different object right a new object entirely and so if if we so so it has
so the only thing that would remain the same is it would have to hold on to an identifier uh and that's something we're
going to have to have to have to do um yeah basically that that's that's what so we basically have um uh some kind of
probably be be be methods on song that would say you know um depending on what we allow to modify I guess anything might
have to might have to have a separate Factory yeah I was thinking like a factory that would take one song as take the
current song as the baseline or duplicate it with these yeah yeah so so that you know that we can basically say um well
we don't need that right now uh and so we can we can kick that can down the road um and because so this issue of the
inmemory version holding on to references is only a problem if record if if song were uh not a record and were actually
mutable because it's then we the object reference itself the content is changing um but in this case it can't change and
if we just even if we decide that you know or even when we get to being able to modify songs we may still decide that
actually mutable is nice uh in which case we would need to just provide a save or update method on our repository um so
either way we we may not have to modify our inmemory at all um what we will have to figure out is how do we want to
persist this song in the database uh and we'll we'll we'll be getting to that that's where the ID comes in uh well it's
more that's where if we're going to use an RM like spring data jtpc um we will need an object that is defined uh using
the omm uh annotations um and we by by rule or at least uh very strong guideline um in hexagonal ports and adapters we
don't do that on our domain objects right and song's a domain object and song is a domain object yeah at some point uh G
to take a note I want to add the coloring to to the project uh because that makes it easier to see what's in the domain
versus application so intellig config uh yeah yeah it's a Project based configuration so um we'll we'll do that at some
point or I'll do that offline so let make a note of that actually you know we could plan to do it in a future stream
because I think people might be I know I'd be interested in how you do it um I I already have it's it's a little tedious
and I have a a whole video on on YouTube on on how to do that awesome so I'll I'll throw a reference into that uh in a
bit um so I think we can uh def defer Jura 88 um and we may not have to do much with that at all even even later on so
we'll have more information and then we'll be able to decide what we go straight to uh Implement jdpc adapter or is
there an intermediate step we here so let's take a look at our repository interface Our Song repository interface so
we've got add and find by theme um I think that's that's good enough so yeah I think we can basically Implement our our
jdbc adapter so let's um let's oh so I just one last note on on what we're deferring uh with with J 8 if um again if
song were mutable and if uh if there's sort of more behavior um then we might uh switch to a different mechanism for for
storing information in a database what I call the snapshot pattern so instead of um because right now it song is really
there's no Behavior there uh it's pretty much just attributes properties attributes and validation right yeah we have
some validation so that's all the behavior that we really have um if you want to call that Behavior Uh I don't really
call it Behavior but basically it's just it's just attributes and so um there's no need to to have a separate um object
that just holds the data because it's pretty much only data already right if there was a lot of behavior and if there's
a lot of complex state that was hard to access um then you basically have a snapshot pattern where where you ask the
object give me a snapshot of your data uh and then you're able to easily then restore that object from that snapshot um
but here there's no need for that because it's very easy to access all the data this you know uh it gets harder when
some of the when some of the um fields are are private and not directly accessible like they might be used for for
Behavior but you can't easily observe them with the snapshot um that part of the snapshot pattern be implemented in the
concrete adapter or you know the repository so the repository would would only store snapshots it would never store
domain objects gotcha so something in between the domain level song and the repository would be creating the snapshot
and saying here Repository this is the snapshot to use yeah in fact it would be the domain object itself that uh that
provides the snapshot um and this is where this is another case where you'd want only persistence to access that
snapshot method right because nobody nobody else because because if you ask for that you're basically getting all the
inside data that's supposed to be private and encapsulated um and so you don't want to uh just allow any method to to to
access that the repository needs it because it needs to store just the data right um but any no other code should access
that method would we enforce that with uh Arc unit yes yes okay yeah yeah because it feels a little bit like you're
leaking from the domain at ttbit you are not not a little bit a whole lot um and and it could it could be a problem um
and so uh so pretty much yeah you don't want to do it um example oh cool of of the snapshot pattern um oops bump this up
a bit so this is from my my uh ensembl application this is the member this is the uh represents members uh in the uh
application in the system it's the aggregate route um and so it's got a bunch of data um not all of it is is easily
accessible uh because it shouldn't be um and so we basically have have two methods we have the reconstitute method which
is this one um and again this is only used to reconstitute the data from the database so given a snapshot um we can now
instantiate a member and so uh it basically grabs all that information um and then there's the symmetrical um give me a
snapshot somewhere there it is uh give me a snapshot of the of the data that's inside so basically package up all of our
Fields uh and then return a member snapshot and then that is stored in the database um and there are a couple of um uh
you don't have to do all sorts of weird stuff to get the state out of this thing you don't have to expose it in any uh
it's a much more stable way of exposing it uh the other nice thing is the snapshot then is easily copied over to
whatever form you want to copy into uh save into the database um so provides a little it's a little bit more work but
also provides a nice level of of decoupling and it's typically called momento when you're creating uh that was my
original name for it uh I now call it snapshot so M there is a momento pattern but it's not quite the same thing and so
I started with the momento name but now now I call it snapshot got I was wondering yeah I should probably r that and so
in just as an example of what an inmemory version would look like to deal with if the objects are changing out
underneath uh we basically when we save it um we uh we basically make a copy of it uh before we save it internally um so
it's a little bit of um so basically create a a copy of of of the momento uh and then uh then we basically manufacture a
new one um and that's and that's what what gets returned so that way uh it's acting much more like if you didn't save it
we won't see that change right so acting database but again since our uh song object doesn't have any uh since it's
immutable and it doesn't have any other thing that make it difficult to access the properties we can just not use and so
you know again this is one of those cases where it's like in a lot of cases if you have an entity that's mutable and has
has a fair amount of behavior and and state that's hard to get at then you'd want to use the snapshot pattern but only
use it if you need it you don't always use it don't overuse patterns yeah don't overuse guidelines and patterns yeah all
right so let's go back to song themes okay um so yeah so I think we uh we can Implement our our jdbc adapter so um this
sketch so the first thing we'll need is um get all our our database dependencies uh added because I don't um and since
we're you know we don't have to at this point but we may as well uh use Flyway for our uh database uh management
migration because eventually we will be migrating uh be updating the schemas in in our database may as well start uh
right away yes it's always good to use it uh right up front um and then uh create the schema I guess that could be part
of the Flyway because we we create the schema in the con in the context of of of a Flyway setup um and then uh so what I
tend to do is is then once we have the schema we need to create the database object that memory the schema in memory
yeah so this is what um will annotate with the um and we'll annotate with the Department of rendy Department um exactly
uh and so once we have that tests just to make sure that we've we're correctly and then um then we will write our
adapter that repository yep uh and then we will modify our use case layer tests to to also be adapter so as I mentioned
before when I was going over the the design we should be able to run the same tests against the test double and those
tests should also pass running against the real the real datab so would we would we set it up to run against both that
we're always yes somehow we don't have some Divergent Behavior okay hey there ton fam Ben howdy so um let's see so once
we have that uh then we then we need to wire it up to the application so wi up the concrete database adapter application
it run the application I didn't think we needed that as a as a as a as a step no no haven't done it in a while though
that's true it'll be interesting but yeah we'll see how far where are we looking uh so let's um let's scroll down and
see if we have anything oops sorry not how I did that let's scroll down and see what what dependencies we've got okay uh
so yeah we're going to want that got uh and yes we're gonna want the docker compos and we're going to want the post
grass uh we've already got our test containers so that's good and that coloring means what uh the coloring means there's
some cve reported orange maybe over here uh no you'd have to hover over unless one maybe on the right right there it is
yeah so there's some cves reported against something that it depends on that test containers may or may not use um this
is always the problem of bringing in libraries like Apache Commons that has you know 180 different things is there's
always cve being reported against all sorts of stuff so I generally ignore that if you want you can explicitly tell it
to ignore it if it if it bothers you but doesn't bother me I was just curious we don't care uh let's keep going anything
else uh so we've already got postgress uh we got all security stuff I think uh the only other thing we need um did we
pull in Flyway I don't think we did I think we thought about it but yeah I think we explicitly pulled it out um because
otherwise it does some stuff that we didn't want it to do uh so if you scroll all the way to the top of this section of
the dependencies section um just you'll see an edit starter so click on that uh let's go down to uh yep and yep yep and
put it at the end I'm always curious how that uh yeah I don't know where it puts it yeah I guess it puts it I'm just
thinking I think I think that's need so technically if we run all tests nothing should break well uh maybe um we can try
it mean I'm curious uh I I I I'm not sure if the database stuff now the flyways in there is going to do something that
that might cause uh because we don't have any configurations around some stuff so might so I should I run it or not well
run it because you yeah yep startup test failed yeah I kind of figured the startup test would fail um mainly because it
couldn't find the configuration uh so if we if we scroll down a bit more um keep uh that's interesting let's scroll down
more so what what what why couldn't it what couldn't it find pro probably something database specific well hold on um
yeah keep going so basically you want to sort of jump from caused by to caus by uh so that one that's fine so go to
going yeah so that's that's the real reason is basically um we couldn't it couldn't find a data source uh and that's to
be expected because we don't have a data source right so let's go create a data source okay um so what we need to do is
uh we need to create a a Docker compose file so what we're going to do so what uh I think we already have one if we go
to the compose yaml what have we got there it's all the this one yeah uh so we've already got that um let's let's make a
couple of changes here right uh let's um change our uh image from uh to a specific version so instead of latest alpine
lowercase a yeah like that right yeah and we can see it's already available yeah cool so what this says is we want the
latest 15 version um and the reason why I'm using 15 is I'm not sure if uh our hosting site has 16 yet um and so 15 is
more than good enough for what we need uh an Alpine is is just a smaller image um the ports we need to expose I don't
know why the default composed doesn't do this uh but if you go to line nine um put inside the single quote put 5432
without the okay yes so what this does is it says uh um inside the container that's going to be be running postgress um
connect that Port 5432 which is postgress as default Port uh and expose it outside the container also as 5432 if you
don't put the col in 5432 then it's not exposed exter externally useless I see a question Charles has um do I recommend
things like neovim for Java development no I do not I recommend intellig idea 100% no questions um there is I can't
think of a reason why you'd use anything else um unless you like typing a lot of stuff manually uh and not and doing
manual refactoring so if you like doing things manually then sure um but really there's in my opinion this this why
would you not use the most powerful tool that that exists um if you like the the vi bindings you can install uh keymaps
and a plugin for for that and I know people who do that um but otherwise I don't know why you wouldn't idea all right so
um let's also fix some of the settings for the postgress uh hyphenated uh no like that I guess what I meant was Kebab
case uh no let I don't like to there's no reason to have that and and I don't know if it's even allowed so therefore
let's yeah no I'm totally cool with it I just wasn't sure if there was a convention um and let's just put password user
just because it's easy to to remember and these are always going to be uh replaced at runtime on the host by um more
secure um hey exite yeah long time no see back yeah if he if he uh he also says tell I mean I I really like I see folks
who use um eclipse and I understand that because they might have been using it for a while or they might be in a
situation where that's um what they had uh but really once you try intellig I don't know anyone who said I tried
intellig and I went back to vs code I don't know anybody who's ever done that uh who used it who used it who tried it
seriously um vs code and and other things are are great for for some things but but not for master Java and I did a lot
of Microsoft development and I'm a total intellig fan so did lots of visual studio for decades intellig is just like so
much better uh so let's go to the application properties do we have an application properties that would be under
resources up there um sorry I was getting distracted by the tech the text message resources so in the project window go
up uh and let's open up um let's open up both properties and yaml it's really bad that we have both uh right I remember
we did the yaml because that was easier for for the OAS stuff um I guess that's that's fine we can we can leave thatth
all right so let's go back to our properties so I can close um let's uh let's see so what do we want um we need to set
up our data want to do that here yeah we want to do that here uh so let's let's create a blank line and source yep and
then username well if I do dot here will it fill it out yes it will sweet uh and we'll use our username which what
whatever which I believe was user password uh and then spring datas today y uh and that's going to be jdbc colon um and
then postgressql all all one word all lowercase uh and then colon um and then the name of our um y That's all good and
then we need uh just to be sure let's do spring data source driver driver class name yep that one uh that's going to be
just hit enter yep and I think that's all we need so so let's um let's try running the startup tests because those are
the only ones that those ah those won't work because those are running this so this is something that uh did I file a
documentation issue on this so what happens is um we set up the docker compose but Docker compose only automatically
starts the container um when you're running the application otherwise it's going to defer to using test containers uh
for it's going to basically say you should be using your test containers for for uh for your uh let's see um let's go to
the to the startup test yep which one class we want to go to the code the test no I know my mouse is acting up oh even
when it's plugged in oh that's a bummer is it I mean I wonder if it's a GPU I'm gonna try and get over to it usually
goes away if it's a GPU being active yeah see in that case I got a GPU Spike for some reason H and now it's back to
normal yeah I don't know what the root cause of that is but it does happen once in a while I hate that stuff really
annoying okay so now if I click here doesn't it jump to um I wonder if we just want to disable these tests for now uh
because they're not really serving any purpose um I think that second test uh is not going to make sense anymore once we
have the database so I think let's just comment out uh line 14 so it doesn't so it doesn't even actually um and we might
have to to disable the whole thing um can we disable it at this level I think maybe we can never I've always wondered
that that's why I asked I was like oh yeah just I guess so uh if you hit uh control Q on that so Target is also
available on type okay so we can do that if we run all now if we run all now it should it should not run yeah Should
Skip that and we should be back to passing commit and mainly what we did was add commit it's really confusing if you
start if you create a new spring boot project with Docker compose and and databases and test containers um out of the
box the the project you will get the test will fit fail which is really kind of annoying um because and there's a way to
do it by doing something that I think is just it's a workaround and and it kind of works but anyway I just think it's
it's uh it's confusing so there there actually are a couple open issues fixed all right so let's go back to jir um I
think we can check that schema so what we want to do is in the Resources directory in our project um main resources
there is a uh BB migration um which is currently empty so what we want to do is create a new uh oh you don't have one
set up so file and this will be um our SQL file so we're going to call this is uh so the way Flyway works is um you
create version versions of of your schema and so what it does is is the typical naming pattern is V1 V2 V3 V4 and so on
and what what flywell will do is um apply those schemas based on where the database is and so it has a separate table
that it keeps track of what version have have have I updated to um so like in my ensembl I've got 13 of these and so on
a new database it's going to basically sequentially run all of the the schema creation ah I see um if it was at 12
because I just added 13 then it was just apply 13 so the naming convention is uh we'll use V uppercase V underscore um
and we'll just call this uh song uh so all lowercase song underscore uh entity. SQL so basically we're going to create
um yeah change the dialect uh and you can change the project okay uh and you can close that at the lower at the lower
right oh yeah find they just linger there is I think a way you can tell it to not do that if you hit the three vertical
dots oh too late sorry or not next time I think there's a way to make that one uh there's a way to configure the
different notifications so that they pop up and then go away versus pop up and stay because of course you can configure
everything that's why the settings thing is has 150 different items actually probably more uh okay so let's go right
some some SQL um technically this is ddl not not SQL but whatever uh so we'll do create table and you should get some
that lowercase uh and then um on a new line we'll do an open pen and then new line so first we'll want the identifier so
ID uh lower lower case lower yeah so everything here is uh all the identifiers are lowercase got it um and then serial
uh and I and since these are are uppercase uh and then a space and then primary key yep and then not line um and now we
can start filling out all the stuff that we have in song below tab yeah I just use tabs because um basically to line up
uh all of the the definitions so do it like this yeah something like that you'll probably want one more tab once we add
other stuff right true but you can fix that up later um so we got uh yep now this do we mix cases okay um actually no
sorry uh you can do it but I think it's easier if we do uh uh snake case so what happens is um spring data will
automatically do some conversions so it will convert snake case into uh camel case for us really yeah that's sweet um
and so that basically makes it so that you don't have to worry about case sensitivity in database schemas and things
like that that yeah so that'll be not null that space comma is going to drive me crazy but that's what the auto
completion is doing uh that's only because you're letting it do that um but that's not that's not what it should be so
you can you can fix it up now or later you can do an auto format and see if it takes it away it probably won't take away
those spaces Control Alt L yep look at that it did it and it lined everything up too oh that's cool yeah so now now you
can just relax let it do the auto formatting release uh snake case right y it's funny it never autocompletes text yeah I
don't know why it does an autocomplete text um it's not like text is some super modern thing that's been around for for
a while so I don't understand it and so what are we gonna do about themes aha okay so what we're gonna do about themes
is store it in an array so you'll do themes um and it'll no that's it comma here uh no comma there because we're we're
done defining stuff um and then we'll want a semicolon uh you can delete the blank cines yep uh we'll want a semicon
after nine oh after nine uh are you me sorry I meant at the end of nine yeah got it okay if I want it then I would have
said nine and a half I guess um so that's our that's our that's our schema um so it's really straightforward for uh for
those who've done any kind of database we've got our ID um the ID will be assigned by the database and that's why we
have serial there uh and it is the primary key um and we're basically saying that nothing should be null um some stuff
might be um blank blank yes uh but not not null not not null we want no NS um it's interesting that auto I'm wondering
about that too like reformat didn't push the if I do this it still doesn't do it huh I wonder if it's because of the
array I think it's because of the array yeah it doesn't it doesn't know how to parse it I guess that's a bummer now if I
reformat is gonna put it back probably yeah yeah that that sounds like a a another bug submission a bug so um doesn't
understand text array all right um top of hour maybe take a quick break oh yeah this is actually a good time for a break
so take a break and when we come back we will um do whatever is next in jira cool all right uh so I'll set the timer for
five minutes five minutes it minutes e hey there 5G technician shout out to Java uh so um little commercial message you
may be familiar with uh my tdd game if you haven't already uh heard about it um it's uh a fun game that uh basically
lets you first of all it's great as a as a game on its own uh one of things it does is is help you understand the test
driven development process um it's great to play with with your colleagues uh provides lots of opportunity for um not
only just having fun but also uh exploring and and and discussing what is test driv development what are the benefits of
it um what's the process uh and so if you go to uh cards um you there's a video here that will uh where I basically talk
about predictive test driven development so all the stuff we do both on the pairing stream and on my solo stream um
where we do tdd but with that first step of of what is the test going to do how is it going to fail um or if it's going
to pass and being very precise about those predictions I talk about this in in this talk that I did for the agile lunch
and learn folks um and then I uh dive in into the game and I just got a new shipment of games so I'm I'm well stocked uh
so uh go ahead check out td. cards um and uh I'm also uh every every conference I go to I bring a copy with me so uh if
you find me at a at a conference especially open space uh come find me and and and we'll play play the game um it is a
physical game it's uh it's it's custom manufactured uh that doesn't work for everyone because we've got a lot of folks
who are working remote and so one of my next projects that I'll be doing on stream uh on my solo stream is working on an
online version of the game so I actually started an online version of the game a couple years ago actually probably over
three years ago where the uh if you know anything about JavaScript Frameworks uh you know that uh trying to build
something that's three years old and get it working is not fun um so I basically want to trash the front end and use HTM
x uh in cooperation with with websockets so basically a lot of the stuff that I learned doing the timer stuff for Embler
I'm going to apply to to the online game so stay tuned stay tuned for that um so check out td. cards if you're
interested in the game uh as I say and now back to our show yeah should have to be cold here I left the yeah it it got
uh it got warm for a couple of days like you know I was running and I was like oh man this is so why am I running at
noon on and it's like 72 degrees which is some people might say that's not hot but for Bay Area it's hot yeah um oh and
um say hey hey 5G technician hey and Jonas Brown hounds welcome wow and hi to exhibite for uh in Mumbai yes from an yeah
all right um so we've got our schema uh let's what was our next step I think our um so what we can do is run the
application just to get it to start up um because what we want it to do is we want to see it bring up the docker compose
uh which will bring up the post basically start the container start post grass connect to it um Flyway we should see
some messages from Flyway uh that will basically say you know upgrading or migrating scheme or whatever message it says
um and then we should be able to connect using intellig connect to the database and see that the schema has been
properly uh away well uh do you have Docker running I don't recall if we set it up on this or not oh um do you have
Docker installed yes Docker desktop yes I do all right so running all righty this good enough or do I need to that
should be fine um at some point you'll want to up upgrade it but not now so rerun yep yeah Flyway so your choices in in
migration or Flyway or liquid base those are the two popular ones um they're both fine I'm just so great so that's
working so what it's doing is it's downloading the postgress image uh so we see pull complete which means the pull from
the image was complete and then it's if you want to scroll back we can sort of read through what it was doing uh yeah so
pull pull layers so all past that won't happen every time right all right and then we see um bootstrapping our jdb
receipt repositories tom cat starts uh we see um more NBC stuff web stuff let's keep going uh there's our Flyway so
right there our uh Flyway Community Edition and it connected to the database and schema history does not exist so so it'
s going to successfully validated one migration so that means it ex it basically said huh I've never seen this database
before let me start from scratch and so it validated one migration created a schema history in its own table um M
actually did the migration to version one song entity successfully applied so so it's all good um and so now the
database is up and running uh so we can actually spelling uh so Jones ask how easy it is to get uh into using Flyway
towards an existing database um really easy what you basically do is you take whatever thing generates your whatever SQL
you have to generate your current schema and that's now that becomes your V1 file and so that's your Baseline um and
then any future migrations you will create separate separate uh SQL files um but you you basically establish your
current schema as as the Baseline and then Flyway will um and there's there's a parameter you might have to run to get
Flyway to say oh the scheme is already there uh you run that once it builds that separate Flyway schema history table
because that's what it uses to keep track of what Flyway migrations have has it applied um and then once it once it sees
that then it knows okay V1 that Baseline schema has been applied if you run it against a new day based then it will just
create the the schema as as you defined it um uh but once you establish that Baseline you can then use it from then on
so it's uh it's it's pretty straightforward to to get it to get to get started with it um so let's see uh uh we want to
go to it's it's interesting it's like what what what's different about my intellig setup than yours where I have all
sorts of things on the right side uh for tools that you do not have um what we want is we want the the database
inspector um and I just I just don't um so yeah let's look for database uh so that's the toolbar we don't want Explorer
this one yeah it yeah let's do that I don't know why it's stuff all right uh so what we want is um one uh Local Host
user password so yeah so let's enter in our user password which we know is user password oh right so that's the
authentication type and we want user themes uh yeah hit test connection there bottom it may have to oh it's all good
succeeded look at that it worked the first time that never happens uh so this oh wait we're recording it already Mark
Mark did this down uh hit hit the apply button and now uh and now we can close it will it then open the I don't I don't
know I don't know now it does let me see if there's a pin auto scroll show toolbar View mode doc pined yeah well I guess
it's pinned now um so let's minimize the the Run window and you can yep open that up and then open up song themes and
open up public and if you open up tables we should see two tables we see our Flyway schema history and we'll see our
songs um so if you open up songs and you open up columns we should see all the columns we defined and we do uh and so
that's all good so we verified that even though unsurprising that that that worked we we verified that hey live coding
yes it's the it's the basically the search anywhere um what we were looking for is why wasn't it a toolbar item already
there when in all my installs of intellig it's there so I don't get it and it's not listed as a tool yeah it's weird
yeah I don't understand it yeah all right it's there now that's all that matters um okay so we verified uh you can close
the current window because it basically opens up the console to the database we don't need that um so I think we can
check off 90 91 everything with flyways J 91 being closed y so now what we want to do is uh we want to create the
database object that represents the schema in memory so we're going to create a new uh a new class were so there's a uh
so there used to be a plugin called um I think it's called jpa buddy uh and then actually jet brains bought it um so I
think it's now available as sort of from jet brains the problem is it's jpa Centric which is really kind of annoying
because there's a lot of overlap uh between jpa spring data jpa and spring data jdbc uh because actually if you look at
the structure of the spring projects um there's actually spring data relational which is sort of the parent project for
jpa and and jdbc and some other stuff because there's stuff that that's in common this idea of of uh runtime generation
of repositories and so on is is the same across um a lot of them um but unfortunately the uh because what we could do is
we could point it at the schema and say please create an object um but we'll have to we'll have to do it manually it's
it's fine it's not a big um uh let's go figure out where do we want to put this this new class so where do we want to
put this class don't have a place for it we don't out yeah adapter adapter. out um. jtbc so let's create a we can create
a new okay um oh no won't let me do it here yeah so you can basically put in a adapter. out Dot and then the name of the
jdbc and then dot the name of the class which will be um so the the postfix that I usually use for these types of
objects which are basically the omm database object is dbo dbo yep and it's class so you can just hit enter and voila
we've got our package and our class sweet um so let's let's start annotating this thing uh so let's put an annotation
table yep and in parenthesis uh we're going to put the string songs uh what casing uh all lowercase so this is matching
the identifiers that we put in our in our schema right and can you remove that unnecessary space between table and the
open print oh that one I'm like where's the space there you go all right and so now inside our song we need to start uh
putting in our um so first we'll start with with uh our ID so we need an annotation at and then uh D uh double check the
import yes that's the correct import sometimes it pulls ID from other places but that's the one we want uh and this is
going to be private yeah uh and then we just need the the rest of our um the rest of our data so stuff private for
everything private for and then we'll do an array instead of a list nope it's a list oh it'll yeah it'll it'll do the
sweet you usually do The annotation on line 10 separate from 11 or yes or should and would I would you do this make it
yeah I might do that to make it more clear yeah so we're using spring data jdbc we're not using spring data jpa so the
annotations are slightly different um ID we still get from the same place uh but um uh you'll notice that we actually
don't need a bunch of other other annotations so um this should be all we need uh so let's go and do and create okay um
so if you do 17 and a half yeah you can close that um and then uh I think it's alt insert for Generate oh right yeah uh
so let's generate a those I think you can just do control a oh that's probably true yeah y um and then uh we'll do a
generate uh getter and Setter uh also for all of them even though it probably isn't necessary it string and that's fine
yeah interesting it selected time like by default I didn't select it oh interesting yeah uh so X proof asks about uh
equals and hash code so for a database object um honestly we really don't care uh because it is a transient object that
pretty much immediately gets copied over to uh to real domain objects and so this is not a longlived object this
shouldn't really appear uh in anything we could Define if we were to Define an equals and hash code um which we might
just to be sure uh we would not use the Standard Generation because by definition these these entities the only thing
that matters is the ID uh so let's go ahead and do that just just to be safe so let's generate an equals and hash code
and by the way I had the exact same question as X proof like should we do but thanks for asking uh can you select a
different template oh let me on that screen yeah yeah intellig default uh just leave everything else um basically
deselect everything but ID saw that one coming yeah uh is it always non null when it's first created uh no it actually
might be null so create okay and it should be as expected Constructor that um has everything but the ID does the
Constructor right all right uh so that's it for the database object um now we need our uh repository uh implementation
did we have that in jira and we had the adapter I think we forgot about the uh we got the database object um we can't we
have to have something to read or write it with so we actually also need the repository so if you want to add another
item that we'll pretty ahead and so this would be create uh spring data jdbc repository sping data they should just
rename it sping I always typo that one as sping uh create sping spring J DBC um repository yeah repository yeah
repository adapter be the application we got song repository here so it would be so this is this is the concrete
technology specific adapter got it just because this is the interface but then we have the concrete in memory here right
so which we will probably move at some point to uh to to test code but for now we can leave it there ah right right
right so we would create it in this package is what you're saying under application well it is going to be spring data
jdbc concrete specific so where should where does code like that go adapter then M okay it goes where the song dbo is
right because it's the repository that reads and writes right right right right okay what do we want to call it um let's
call it uh what is my it needs to implement song repository uh no this is not the adapter this is the the techn ology
reading and writing um so this is going to be actually an interface uh so yeah so new Java class um and it'll be an
interface uh got yes okay um so this interface will extend um it uh I think we can use crud repository so CR repository
Y and so it takes two generified uh two generic parameters um so the first one is the object that writing so in our so
you'll open up an angle bracket here ah okay and then uh the first type is the thing we're reading and writing song dbo
and then the second one is the primary key type type so we did it as what was it is it long long like that yep okay and
that's it for now uh so what we can now do is write write some tests that read and write the dbbo working so those would
be tests at the adapter. out layer correct yes so you can do an ALT uh command uh alt shift T from where we are on the
upper right oh I see got it uh Control Alt oh that's no it's all Shifty oh actually for me it's control Shifty I
flashcards and then is it automatically so what was that that was uh control shift T is go to test go to test slash go
to test subject depending on going so is this good to go that's totally fine yep okay yeah so there's some uh some
discussion in in in chat around equals and so on if you're if you if you want to test the contents of it um a uh the
assertion Library assertj will help you with that because you can um have it avoid using the equals for comparison and
you can actually say things like uh test these properties recursively against or um recursively test all properties but
ignore these and things like that so you have a lot of power for when you're comparing objects you don't always have to
use the equals methods in your test um and then it will give you good good error messages if it good failure messages if
it doesn't work did we answer about the at generated value yes annotation question we did okay yes that was part of the
this is in Spring data jpa got it okay so next all right uh so we've got our test so this test we need to do uh we need
to add an annotation to the CL test class because this is a special kind of test and this is an at data jdbc test and in
parentheses we're going to need to do a couple of things um so uh we're going to basically Define some properties so uh
say properties equal a lower case oh yeah all lower case and then an open curly brace and then let's let's hit a new
line um and then uh so what we're doing here is we're overriding or defining um spring properties so one of the things
we want to do is normally if you run data jdbc test it's going to create its own database um often using H2 we don't
want that we want to use test containers so uh what we say here is um open open a double quote and we're going to say
spring. test. database. replace equals and then in uppercase uh the word none do you put spaces around the so all all
uppercase no no space so this is just like a pro properties definition I mean you could put space but there's no point
to it right uh outside that put a comma because we're going to Define another property and then open quotes um and so
this is uh we're basically going to override the the data data source URL so spring. datas source. URL um I think all we
need to do is this is this is this is one of the annoying things is like stuff around test containers has and spring
boot has changed um a lot over the past year or so uh and so like I'm always forgetting like what's the modern uh
up-to-date way to do this um I think this is it let's let's try it uh so we're going to say jdbc colon uh colon um what
do we say 15 is the one really I could have sworn no was lower case was it in that application properties that was it
it's probably off screen uh no sorry wouldn't the compose because it's a Docker image ah oh it was lowercase okay yeah
my memory was Focus uh and then after Alpine colon and slashes uh spring boot all lowercase word all right um so
hopefully what this will do is it will start up test container so uh a separate container separate from the one that
gets run when we run the application um and so we'll start it up for the duration of the test and then um and because
it's at the class level it would be for all the test within this presume yes is it startup container shutdown container
between tests uh there's some there's some ways you can optimize that so if you have um lots of tests that are basically
using the database and don't interfere with each other uh then you can sort of keep it up during the duration of all
test uh test execution gotcha so the default is it's uh created and teared down torn down for every test for Every at
the test class level yeah uh the the life cycle is is is has changed a little bit or is a bit my memory might be faulty
um we could look containers uh we've got our database entity uh got up feel like there's something missing um just want
to double check there were there were several different ways to do this and it recently changed with what was called the
service container um yeah I think well we'll try it we'll see um uh let's uh so let's inside the test to line 12 yep um
we're going to autowire the repository the jdbc Repository we just uh created yep what do you want to call it we'll call
it song jdbc repository hey that's a really good idea yeah there's there's some there's we can use service connection um
and I and I know that sort of the there's a newer way to do that uh we'll we'll try that after um I I forget the the
exact syntax after to go find it because I now know three different ways to do this uh and I'm and I'm trying to figure
out which one is is but this one I think will will work this is the one that's actually documented on the on the yeah if
you want to throw a link in uh I'll follow it and we'll take a look hey stupendous follow uh yes the project is publicly
available um I'll throw a link in in a second um all right so we've got the auto wi repository and test um for now let's
just uh yeah J5 um can read and write dbo because that's about so we'll say um song jwc repository dot uh what that's
weird I was surpr I was surprised at the order of of what it's showing uh like all the good stuff is is not at the top
but I guess in your intellig you don't use database as much and so it's machine learning is is saying I don't know what
to propose here is there machine learning on this oh yeah autocomplete has machine learning and it's had that for years
um not AI machine learning basically per individual yeah uh so actually before we can do a save um we actually need to
create a dbo so 42 uh don't give it an ID we want to call the second Constructor because what we want is we want to
create an ID when we when we save it right of course let me grab my spreadsheet so I have to um yeah the latest update
in intellig depend follow uh is about the ful line autoc completion that uses um uh more llm type uh machine learning
but the autocomplete is always it's always collected statistics on what you which autocomplete option you use uh and it
reorders things based on on that which may or may not be what you want um but usually it is um the the model that it
uses the small model that it uses is is the newest thing for the full line autoc what am I missing uh what that junk is
I think you put the clothes on the next line ah that yeah no control shift J thank you I was doing the wrong one control
shift you're probably doing control J yeah there we go uh but you combine them lines that's too much yeah control shift
J there you go there you go all right so now that we got one of those now we can do song jwc repository. saave and give
it a song dbo uh we'll assign the return value to another dbo uh and we can do something like no oh it doesn't have aert
that uh if you do a and let it autocomplete uh probably because you haven't imported it so it doesn't see that it's an
autocomplete there we go ID because basically what we're checking is that the ID was assigned when we saved it um and
then that should be not null so when you have this this post this auto complete you want that rectangle you want to hit
enter to get out of that rectangle to the next rectangle and it jumps to the next one got it and then we yeah wow that
was really far down yeah guess you don't use it a lot um let's yeah so read and write dbo I guess it seems General in a
way we're saying can we rewrite dbo and does it ID get a sign or is that two verbose uh we're gonna we're gonna extend
this test so we're gonna take the save dbo um modify it and then and then write it back out gotcha okay uh yep run jti
this one yeah let's test um yeah we may not have set up the sorry I'm scrolling did you want me to uh I'm just looking
at the so in the spring Booth 3.1 that's when they change the way test containers work I think need one more thing but I
think let's go to um let's go to the more Modern Way of of doing it I see Jon has provided a okay that's really annoying
sorry streamyard doesn't allow me to easily select uh something that was posted in the comments I have to go to my other
comment window really it's easily selectable for me um that's because I have the ability to um because you're the host
put the to put the banner up and so uh it overlays the entire thing which it really shouldn't do let me all right so
let's go um let's change our uh our test stuff um so we can actually delete um actually before we delete that let me let
me let's just try one thing uh um so let's I think one thing we actually forgot to make this work uh half um and this is
going to be test containers so we forgot that important thing the lowercase C for some reason I don't I don't know why
they did that and now you can never change it um uh and we want to add a property so open pren uh disabled should start
Auto completing it l lowercase yeah and that one yeah uh so what this does is it says don't bother running this test if
no available so that looks good we see test containers pulling the the thing uh so let's scroll down and see what
missing keep going cause by uh let's look for another cause by uh uh it didn't URL I like that it says claims to not
accept yeah um let's try one other thing and then we'll go the the service connection route uh let's go and and in the
property drop Alpine I don't know if that's causing it to drop the whole Alpine oh yeah so just leave 15 yeah so let's
try that if that doesn't work we'll uh we'll go a different route I think we still yeah all right so let's go the the
new the new way I'm just gonna quick pause I want to make sure my sign the way has to go to y yeah it's not a Flyway
specific issue it's that right so what what you often see when when app when spring boot can't start up is uh can't
instantiate this because of this and because of this and it can't get Flyway because it can't get the the data source
and it can't get the data source because the driver says it it's not accepting that URL um so it's just Flyway is is is
the one that requires the data source uh but it's not a Flyway specific thing that's why you always have to look deep
into the cause buys to find the actual root cause of of all right so let's um let's drop line uh 15 okay uh and you can
I guess get rid of the com at the connection uh and then on a new line um static uh postgress so so this is name of a
class um you're going to want the auto S oops that was too early that's the one you wanted no container this one yes uh
and we'll generif it with a question mark so so generif means open angle braet yeah yeah okay uh and the variable name
will'll call uh postgress container or just postgress actually is fine that's fine I don't know why they they have SQL
in uppercase that's like just terrible uh no we need we need to instantiate it so we need to say uh equals postris y uh
and then in uh in the friends we don't need generification we don't need because it was already generified uh uh we need
double be I think just 15- Alpine so I think this is the the label for the image can what no documentation found uh
maybe here how about a no we need to know what the parameters are um uh not is it control P what do what does show the
parameters on on Windows control P okay uh so this is the name uh is it the full I think it's the full name so it's
postgress colon uh before the 15 right um I don't know where it's going to get the properties from uh but let's run this
and see if we get message I think we might have to add the properties manually but I think there's a way to get those
right looks like it worked so let's see so start started process um BL blah uh added connection yeah that's all good
test the test passed because clearly um the uh ID was assigned right all right so let's um let's add to our test items
so let's say save dbo do oh because we want to modify the saved one uh whatever set you want to do artist title song
title oh I did song title one all right uh let's put a blank line about that just to make it clear there a separate
section um and let's now do so here we don't want to hold on to the return value we just want to save it and what we're
going to do is is do a fine bu to see that we can actually find it okay um so let's do uh and that will hold on to as a
dbo uh and then outside we'll say is present present interesting yeah because it's an optional um and furthermore we can
then say uh let's see what do we want to look at uh we want to look at the song title so extracting oh extracting and
what we want to extract is uh song title p uh great so it does have a function okay so we can hand in a method handle
title oh actually yeah it's actually get song title right I forgot this is this is a dbo so and then we can say title uh
did we scroll it away anywhere stuff all right so what this is saying is um so we know that when we save it we get an ID
so an ID is is assigned we take that object um we modify it we save it that should update the database we should be able
to then find it by its ID it should be there and it should have the new song uh oh we didn't have a a default
Constructor all right let's create a default Constructor oh how did you see that uh right there uh in the in the second
to last caused by ah failed to instantiate see I'm an expert so I I I I I am very good at ignoring a lot of stuff that
we don't need to look at yes because I've looked at these thousand times uh so let's go to our song dbo and Constructor
no oh nope you want you want oh it was selected right right right yeah because because of the way that UI works there's
no way for them to make it easy to un select it so exactly um so okay I I guess I I always forget about this because I
thought the spring data would use the all args Constructor but I guess not I have to go reread the docs for that so you'
re expecting it to use the Constructor on 23 yes but apparently it needs I wonder if that's spring data test yeah I use
the the suffix dbo to indicate that this is an omm database object that represents uh stuff in the database and it's
pure data um but it's it's it's a way I look at this more specific kind of data transfer object it's very it's specific
database all right that worked commit getting close to break time what repository actually we we added storing song in
the database is really did yeah it's good to keep it not at a technical level if you can yep yep all right let's commit
okay all right so when we come back from our break um what we're going to do is uh implement the adapter but before we
implement the adapter we're going to need one more method uh we're going to need to to add a method to find by uh song
themes um which will require a custom query um but back sounds good minutes e so one of the things that I think it's
really important to do uh is when you run into a situation like we just ran into where um you get an exception the
exception says couldn't find a uh no AR Constructor and so you go at a no or Constructor the next step is learn why um
because otherwise what you end up with is code that works but maybe not for precisely the right reason um or maybe it
just happens to work but that's really a workaround or it's not what you actually uh intended to do and so this is how
sort of Cru builds up um is because you you sort of get it get it to work but it might not be the working in in the
right way and then later on you might regret it or or have some some issues so um this is uh the documentation for
what's called Spring data Commons which is sort of the the main project under which then a bunch of the other relational
ones uh uh sort of fall so this is common to to all of the spring data um projects so basically it tries to detect a
persistent entity's Constructor so basically when it's instan in the object to to restore it from the database it first
looks to see is there a single static Factory method with this annotation then it uses that one if there's only one
Constructor it uses that one and so for us we had two Constructors and that's why it didn't use the one that I thought
it would use which is the one that had the ID in it um because it doesn't really know and so if they're multiple
Constructors uh and none are annotated which which is our case then um then it's going to want to find a no argument
Constructor uh and so other Constructors are ignoring and since it couldn't find one annotated it's not a record uh
there was no no argument Constructor and so it basically gave up so we fixed it wrong in the sense of we created no
argument Constructor but really we want to use that other so let's go do that which route would you take would you go
with the static Factory method using no I'd go with the full the the the one we created that has all the arguments and
just annotate it with persistence Creator got it so let's go what is the yeah advantage of or what situations would you
want to have a static Factory method in this in this situ I don't know uh I mean I think it's it's more um for if you
are annotating domain objects basically if you're not following any kind of uh separation of concerns architecture and
you're annotating your your domain object then you probably might want a specific method that's used by your persistence
uh and only by your persistence and make that a factory method got it excuse me which um so do e the default Constructor
yep and let's annotate that one the first one okay because that's the one we wanted to use voila right um all right so
uh let's amend our commit so that way Al righty so um yeah we did 93 we did 95 we write a couple tests or just one test
we wrote one test it's fine these test um so let's put an at tag on 19 and a half yeah uh yeah tag and as database and I
usually use my tags as lowercase so I'm not worried about case um and let's check our run configurations I just want to
make sure that uh our IO free tests uh so go to edit configurations because we want to configurations and IO free uh so
it's um I mean we could tag our database test as an IO test if we want uh or the other option can um conate concatenate
some things together in the in terms of the tags is there value in having database as a separate tag we want to just run
yeah because then you can just run the database tests versus all the io versus all the io ones yeah got it so that means
here we yeah so they do um uh put in an Amper sand with some space around it great uh and then uh the bang and then
database so basically saying all tags it so just hit okay okay all right um I want to run io3 just to make sure that
they run fast oh yeah test our test fast sweet all right so we need to um have one more test because of the special way
that uh themes need to be found by um uh so spring data whether it's jdbc or jpa or whatever has ways of uh letting you
write queries as as basically complex methods so let's open up our uh song jdbc bottom um so what we'd like to do is
write a method uh so we could do something like um so let's write a method uh and we'll so the the yeah so public the
return value is going to be dbo find and so notice that intelligy is offering to autocomplete these are not methods that
exist that we're overwriting or implementing these are suggest questions of hey these are the way you can use uh I
forget the technical term but basically the method structure the method name structure defines how it's going to be
searched for in the database so we can say something like by and then we can say uh artist yeah do we search for artists
um this is just an example uh We're Not Gonna actually use this um and song PR and so then what we can give it is
basically two strings and what it will do is it will generate the correct SQL select statement to do this it will
generate a you know select uh where artists like whatever the first string is uh and song title equals the next string
that we pass it that is insanely cool um so it's great Fields so um full Nal mentions the criteria API and to me it's
like why would if the method supports this and it generates everything else why wouldn't I use that let it generate the
the optimal SQL um for more complex situations uh we need to do something else and so we're going to do that something
else so let's delete this it what we are going to need is find by themes right um so uh so let's create a a method um
actually since this an interface we don't need to use the public oh great uh but it is going to return a theme um and
what we're going to hand in and then semicolon now unfortunately this won't work um it uh spring data does not currently
support arrays um so we have to write the SQL basically ourselves so uh let's add a line at eight and a half query okay
uh and this takes a string so do a string um and so we'll have basically we're going to be writing the select statement
oh interesting so we're gonna say select star from and what's nice is until Jame knows that you're writing SQL yeah so
it songs which it knows uh and then we're going to say where uh and this is where we're going to have the the parameter
replacement so this is theme uh and that's going to equal so space equals uh and then the keyword for postgress to
search in a an aray uh column is any uh uppercase and then open PR uh themes so what it's basically saying is find me
songs where this theme column uh now we need to tell spring which parameter it matches theme it can't figure it out from
the variable name so we have to annotate uh the string theme uh with another with an annotation so in the parameter list
in our oh in the parameter list in the parameter list and so we say at quotes So that theme string there matches the
colon theme above so that colon theme will get replaced by the parameter that we pass pass uh and then it will return
any and all songs that have that theme anywhere in the list of themes it's really a bummer that that that it's not
supported I looked at the issue the issue is not new um not I guess there's just not enough demand for it uh and since
it's fairly trivial to write your own query uh I guess they they didn't want to add it because really what I'd like to
be able to do is say um find by theme in themes and then let it figure out and write write this um but it doesn't do um
so 5G technician asks what if the songs table had a relation uh if it had a relation if the themes were stored in a
separate table um then uh then it would figure it out because it would although it would depend on the structure that
you define for the for the song um if it was an embedded list where the where it did the autom map where it did the
mapping on its own then it then then it would basically figure it out yeah um but but generally uh you it would be sort
of an odd an odd structure um unless you you you truly wanted themes to to be a top level thing uh than it is uh uh many
to many and then they basically your your the structure of your data would would totally change we're not doing that
because we're saying we're okay with um the redundancy of themes in our table uh we're also currently saying uh about
the fact that we might misspell themes um so we're not normalizing themes either so it would probably be better from a
relational standpoint to have themes be its own table uh and then you can do things like when you're adding a song
select from existing themes and it would have somewhere to look for those uh and then when you're finding by themes you
basically do a different kind of of search um but from a from a from an aggregate standpoint it's it's it's a different
uh it's a different structure I imagine at some point when we get to list well whether we list the theme potential
themes for searching at that point maybe it would be worthwhile having a separate themes table possibly um that would
that would change quite a bit uh because it would change it would change um it wouldn't change anything in our domain uh
but it would change uh our our jdbc adapter and how we store that um right uh on the other hand um it's pretty easy how
easy would it be to find all unique themes AC there's probably a way to do it um and let the database figure it out
wouldn't be terribly efficient so probably would not right uh full NOA asks why use a relational database and my
question always is is why wouldn't I why would I not want to use one of the most powerful uh databases that exists which
is postgress um more and more I see postgress taking on all the abilities that um no non-relational databases it um I I
think it's it there's again fashion comes into play people say oh I want to just store Json so let me go use it's like
nope postest can totally store Json very easily very fast and you get all the advantage of of the fact that almost every
place you'd want to deploy your application supports postgress which is not true for non-relational databases and so I
always so I like boring technology postgress is boring because it's rock solid it works it's not fashionable um doesn't
have you know Venture Capital behind it push it and and stuff like that uh and I think there's uh from an operational
standpoint it's very well known how to operate it and so um over the over the years and decades I've learned stick with
stuff that if unless you have a compelling reason you should have defaults of use postgress you'd have to have a really
good reason and prove that to use anything else not to say other databases aren't useful they absolutely are but Oracle
decidedly not Oracle unless you like uh paying lots of money for no reason if you want to just throw money away if you
want to throw money away I I have all sorts of things you and it's and it's not you know and it's not to say that Oracle
is bad um sophisticated very powerful database um is it worth the return on on investment only you only you can decide
so um all right let's write a test for this works okay um I think let's yeah let's write a separate test uh find by
theme works these are these are very much uh oneoff kinds of tests um so let's create a let's let's uh create and write
a couple of songs that have uh sort of overlapping themes we could probably grab this stuff from from an existing test
where we test for fine by themes oh not not grab from here I mean you could I I don't I don't care I I have no
preference on what you're doing okay um you just want uh a few songs with some overlapping themes uh and at least one
Mojo Nixon passed away this year very sad you're not familiar with it me it's really funny this one is just money and
you said overlapping and then one that's not that's be different yeah so what we want is we want when we search by money
it finds two not three gotcha filter and the mouse is acting up again uh yes there is there's a way to to select uh L LF
endings um uh I don't so I know if you look at um you see in the in the bottom part of the toolbar there's a crlf um
just next to the row column indicators in the in the bottom right uh I I think if you click on that you can you can
change the uh the line endings um but you also have to be careful because git might be changing your line endings also
uh because that's what it what it does and so um my condolences on having to think about that because you really just
shouldn't have to think about that uh it's only for the current file there um let's see I'm sure there's a parameter
yeah I don't know I don't know what it is offand it may actually be reading based on whatever the current file is in
which case you probably uh want to modify your git configuration assuming you're using git um and because it's going to
be doing the so most sort of out of the boox git is is g to be set up to do like that's one of the first things I
remember doing when I when I set UPG is uh the Auto Line Feed conversion uh the auto new line conversion um and uh so
you want to just probably probably change that um setting because I wouldn't I wouldn't want my IDE to change that if
git is then gonna change it again then you're just not going to have fun all right so we got three songs um so let's go
yeah is it um or this is probably maybe a TBD have save not individually songs you mean save bulk yeah uh I guess I
think there is a save PN so I think there is a save all um we probably won't need that but I think there is a save an
alternate version already that's built in iterable so we've saved and now we want to do a fine by correct and this is oh
not fine by not well fine by theme um fine by theme yeah your current you may as well delete your current line it's not
there's not none of the stuff is right the parameter is wrong the return value is wrong so 20241 yeah because if you
were you uh intelligy would be suggesting Full Line Auto completions oh nice which may or uh so let's search for money
since that it's two yep then let's create a local variable and then it would be songs or found songs Y is it songs or
songs dbo I think either well I forgot auto complete doesn't isn't fast enough and assert that yeah that's why I have my
postfix set up so I would type found songs and then dot a and it would surround the variable and complete oh you have it
set up for that it's not uh it's not actually uh do you have do you have the postfix set up do you have your postfix
plugin I don't think so no Mike you're you're behind on your plugins you got to get the postfix plug-in and the the tab
shifter plugin um come on get with plugin tab shifter uh so stend is follow asks about the Java runtime version so that
um was used because one of the places we were deploying to uh use that to switch the Java version that it would use for
the build pack um if that we're probably not going to use that anymore because we're probably we're going to package up
our own uh Docker image and so then we won't be reliant on the build packs of the the provider but that's that's what
that was for anything let's um let's just be more precise in our assertion sure uh I was thinking we fine yeah we could
we could grow it but extracting and we'll extract the the title again right uh and then we'll off of that we'll say
contains exactly uh and I think in any order is fine because we don't care about the order uh and so we expect it to be
yellow man and Mojo Nixon sorry no songs uh donate money and where the hell is my all right looks right to me okay um
just run this look at that it worked right off the bat wow sweet um let's try this let's uh change money in the fine by
theme on 62 it is it currently case sensitive or we find we're gonna find out yeah I think sensitive indeed yeah all
right well we want it to be case and sensitive right I would think so I can't imagine a reason not to be yep so let's go
fix it um er how would we fix do we let the database fix it or do we just always convert to lowercase yeah I was
wondering about themee I'd rather store the theme in case see want to store mixed case display mixed case but search
case insensitive okay because I think it'll you know it'll look better on the site to see mixed case uh that's the way
you've been entering in the spreadsheet mixed case yeah it's mostly mixed case yeah all right I don't think there's any
lowercase actually so then um we're going to have to figure out how that or do we just say it's mixed case but I guess
if somebody else when we get be do we just say we expect to make this case and we want it to be unique um so for me I'm
going to enter a mixed case so there won't be a lower case right do we just say that's what it must be um or if somebody
when we get to the point we're building for outside people to contribute songs like if their bulk thing has them all
lowercase for example well then you wouldn't accept the proposal then it wouldn't accept it yeah or would it search for
money ah we got a money that's Upp case we'll just use that one and then change um I think that would require then to
choose from an an existing one right yeah I'm okay with enforcing it case so I mean enforcing it in right word but
allowing mix Cas yeah um yeah so I'm I'm not sure if lower works on any uh so let's try it experiment because uh I don't
I don't know if the function can operate on an array but I guess we'll try it so lower right before so so lower or yeah
no no so it's a function so basically lower open pen any ah and then and then Clos pen and then lower around theme where
wait I think I lost a quote there yeah you missing a Clos print oh I it and then lower around the colon theme it um it
was failing we're looking for lowercase M yeah let's run it let's see what happens nope yeah so it's syntax error so you
yeah take it out um so we're so we keep it the lower on the theme looks like what we're going to have to do is is what's
called an unest which basically expands the um the the array into individual items so before the uh uh so from uh okay
so after the where we're we're going to introduce a a a basically a sub exists is that yep plural excuse me and then
open PR open pen uh Delete the lower yeah uh and so from uh and what we're going to do is we're gonna uh unest so the
function is called unest so un and then Nest two ends yeah and that is the column name which is themes end quote uh no
it's the name of the column no no no so unest open pen and the word themes because we're already in a theme one word now
as and then theme lowercase ah so what we're saying is um unest themes into theme uh and now we can do a wear Clause um
so uppercase wear uh and then lower theme that's right and then instead of any themes it's lower uh theme basically the
variable we just extracted and you'll need to close the pen okay so we have to use any because the column is not just a
string it's uh it's an array so it's an array of strings and so um it's not a column that's searchable directly uh we
could if we wanted to uh combine it but why not use the features of of postgress um this query is not database agnostic
it is very specific to to postgress uh it's basically we provided the SQL template um and it's just going to execute it
and it looks like that's just an alternate for for what we're doing we might try some variations um but let's fast all
right let's try the alternate because it looks like um uh 5G technation and my research says query um and so we're going
to do select uh so it's also going to be uh lower theme a lower colon theme the lower the function lower and in
parenthesis colon theme got it uh and then I yes uh so I like uh is a case insensitive like um oh so uh from songs were
lower theme any I guess we don't even have to say lower theme if it's case insensitive uh you um let's try that since we
know that it should work uh let's see because this is way better yeah Tada sweet yeah that's way better um let's see if
we drop the lower for the the colon theme because if we're saying case and sensitive like then it should be case and
sensitive on both that all right that's our query cool 11 I think we can delete that that one yes nice to know that that
we could do that um but we don't have um change the name to make it clear that we're also deliberately checking against
different yes and in fact um full ala mentioned we should suffix our method that we just wrote in our repository
interface with ignore case to make that clear as well um so let's do a rename there and then we'll rename test yeah and
find by work find by theme ignore case Works uh we could say Works regardless of case yeah because we're we're testing
more than just the case yeah yeah everything yeah I guess I like is is postgress specific um and so is any so I'm glad
they work together and this is why we're using postgress because it's awesome uh you renamed your test to trying to
rerun the test that gonna be difficult uh you can just run all the all the database tests and just make sure we haven't
uh we don't have database tests we have no just run the test I mean if we want to create another run configuration we
can but we can just run the tests as a whole oh the the class gotcha yeah yeah I interpreted it as run the config gotcha
for database hey IGI you missed all the fun no and we're ending soon yes sadly um i' love to keep going but I have to so
let's uh let's do commit okay uh and this was jira um so that's our next step uh actually you said there was a three
three dot thing I could do don't show this one again yeah don't show again for do we want to stop here and we'll leave
the concrete adapter for next time yeah I have a pretty hard stop today because I have to yeah so let's do that uh so
push whoops might well do a committ and push now since it's got the uh yep I made a small change should I amend uh yeah
you can yeah uh so we don't have a regular schedule um as uh Luigi nicely uh pointed out there uh the disc is the best
place to to be notified I try to do it somewhat in advance sometimes that advanced notice is only half an hour uh but I
try to do it uh at least a few days in advance as we know so as Mike and I agree on on our schedule times um uh joining
the Discord and uh going into the rolls Channel and clicking on the alert for code stream alert you'll get notified by
Discord when I do do that announcement um twitch will announce it when we go live uh so that will only give you like a
two-minute warning um and uh it's actually not 100% reliable uh oh thanks Jin us for your for your uh Prime resub two
months thank you appreciate that thanks so that's it for today um I will likely have a a solo stream tomorrow or the
next day uh where I'll continue with with ensembl and start thinking about the the next project but that's all for today
anything else you wna mention Mike no I think um hopefully after uh next week we'll be able to start doing more than
once a week go to twice a week sounds good all right thanks everyone for joining appreciate it appreciate all all of the
the input um that's why we do this we love all the chats and all the input so thank you for doing that and uh we will
see you next
