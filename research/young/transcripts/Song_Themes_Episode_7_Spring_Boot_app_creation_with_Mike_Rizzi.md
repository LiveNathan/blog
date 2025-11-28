# ＂Song Themes＂ Episode 7： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=Ti5yGWCSxjs

---

## Transcript

all right folks welcome seven and let me bring Mike on board there he is howdy good morning Happy New Year close to it
do you have to say it can you you say Happy New Year's Eve I guess is probably a more accurate way of saying it huh
Happy New Year's Eve morning I don't know so it's not morning everywhere that's true in fact let's see when what's is it
New Year's let's see is there UTC plus three somewhere yeah it must be so it must be uh getting pretty close to New
Year's for some folks so welcome to uh our episode we're we're uh definitely only going to spend a couple hours today as
the last pairing stream of 2023 so yesterday uh we started what did we do we I know we had um we did some refactoring we
talked about some architecture stuff uh we talked about yeah like deciding whether to start off with having song search
or hold the uh right yes we were we were discussing whether whether it was uh we were GNA push all the searching to the
database or or leave it as basically one big read model that's in memory and I'm glad I'm glad we chose uh the path we
did which is let's let's try try it out in memory uh because that I think that worked out more straight at least a bit
more straightforward than I thought it thought it would welcome I was checking uh somebody somebody uh last night did it
did a caffeinate usually I disable the the twitch where you can do reward requests usually I replace I turn off the
caffeinate at night but I forgot to do that but I'm gonna caffeinate right Muhammad welcome welcome so should I share
your screen all righty sounds good there we go should we open jira let's open jir and let's see where we're no let's see
where were we we were here right so we were doing the Addis song that doesn't exist to the database um is that done um
we had we had the zero we had the one we had the many let's go look at the test was it uh we don't need these it was the
song yes hey AB welcome no songs added one song added multiple songs are found by their theme now but we've only added
what about if we have well I guess that would be on you know closer to the I was thinking about I can tell you you're
jumping things that you're not actually saying so why why don't you tell folks what you're thinking yeah no exactly I
was totally I actually recognized that I was doing that jumping parsing thing um so far we've done it only with one
theme right so we don't have multiple themes in the database and then requesting one theme and we actually haven't even
done what happens if you request two themes which is actually a bit of a um product owner decision as to what they want
to right happen right I would consider that a an unimplemented feature as of this point but but what I think you you
were going to ask a question then you an partially answered it like do we need to test the multiple themes at this Lev
level right and the answer is no we test that closer to the song Searcher right so and this is really this is really
important because uh a really important concept that I that that um is why I like the layering is here at this level and
maybe I'll bring up the hexagon diagram um at this level what we're testing when we're testing against the application
layer which is what we're doing with the song service saying hey uh find songs from by this theme um what we're testing
is does it connect to the domain does it talk to the actual song Searcher object underneath and does it does it then do
we create a new one that then has the the right stuff in it but um there's no reason to to basically fully test
everything from the application layer right we've got lots of smaller smaller tests directly against the domain so
there's no need for us to to to do the comprehensive testing at this layer so then I would say as a devil's advocate um
did we need all three tests layer no we could have gotten away with uh with probably just gone to to many um but we did
grow code based on this approach yeah and and so so it's you know do we still need those maybe not right and so I think
that's that's even a more interesting question is do we now need all three of those since we've tested the connection um
do we actually need the other two tests uh and I might argue we can delete them myard infinity stone screen yes um yeah
I actually like that idea um in some ways I almost want to like we know that service level tests are checking to make
sure that we're talking to the domain right and we know that is there do but I guess I'm wondering is there a way way to
by eliminating those two that's a breadcrumb in a way to somebody else looking at the code like why are they don't why
didn't they test zero and one um but I guess it's not really yeah I'm thinking of like self-documenting perspective
right right documentation and so it's it's a the right it's engineering so they're trade-offs y um if we leave them how
much does it hurt very various aspects of what we do runtime of running tests it's irrelevant because these tests run
five tests or 10 tests there's no difference 50 tests or 100 tests there's no difference for the io free tests so
there's never a concern that oh it's gonna add time to running tests if it does that's a separate issue but um oh I
think I'm I phrased but you're right in terms of of the of the value of the tests there for people well actually I was
going a different route actually sorry okay I think you were thinking that I was talking about keeping these tests I
still think we should get rid of them no I saying the the the tradeoff of of of keeping them is there are multiple
aspects where there's there's trade-offs so keeping them doesn't hurt runtime but doesn't hurt other aspects like why
are you testing at this level you just need to test as a connection um another perhaps more important thing which is
probably what more folks I see talk about is well what if you don't return a list of song anymore what if you return
some other type of object then you get three tests to change right then now you've got tests at two levels to change
right so there's there's there's these link tests that if they're testing the same thing um and you you it would not
surprise me that a various search things are going to return something other than a list uh or a list of song especially
with multiple themes and with certain ranking there might be some larger object that gets returned or a different object
um or if it just changes in some way we right for let's say for example uh I can't I can't think of anything El but yeah
like a different kind of collection class has to come back for some yeah or just or just different Behavior yeah um so
that's something that's something that this is why you you want to reduce the number of of tests that are basically
testing the same thing at different levels yeah I I think we should get rid of them yeah zero and one yep uh Seda asks
how you gonna enter your songs and themes into the database through the UI um Anna sprit that's another story yeah yeah
yeah but at least what we're working on right now is is a single song entry from the UI we'll uh ad song seems like the
wrong method at the service layer maybe add songs to theme or add theme um no the the at least the way I understand what
we're being asked to do is there's going to be a form that's going to have the song and part of that form will have its
theme so it's not uh there may be other reasons to have there may be other uis where it's like hey enter a whole bunch
of songs for this theme then that might be useful uh but then that would be a different service layer use case uh
command and then that name would be a good name add to theme yeah and then it may be that that we create themes and add
the songs to that theme and then that theme gets added to to this to the database um but all those are are predictions
of things that we about um so what I was going to say so I'm I'm going to delete these because I think I'm in agreement
are you y good do actually can you do it from the void I'm curious no it needs to be on yeah has to um less stated or
was in my brain but I probably didn't say was actually I'm gonna do it I'm gonna type it as a comment and then uh then
that'll drive the conversation um test now correct me if I'm wrong um connection I don't like the word but I'm going to
use it for now connection to domain um hexagon in other words saying what this test is doing right like we just had the
conversation yeah we don't need one and two right because we're and connection is not the right word you use the
different terminology which I thought I use wiring wiring yeah you could also use dependency but that's that that has
wiring or wired yeah so and this is I guess a a it's like we know that that's what it test that's kind of where my head
was going I didn't really go that deep in it but like would um would it be more self-documenting to call this um I don't
know I'm just GNA pick one song service wiring test or is that too specific because we might have more things in wiring
so this specific test is more about is is this it's not just wiring yeah so the um the test that did nothing that that
could have been just pure wiring because you're never going to find anything with when the song database is empty right
but here because of the song Searcher uh the song Searcher structure the service is actually orchestrating song
Searchers so it's not just forwarding and delegating a request which is what we started with with with an with a zero
zero case is just did did it delegate the method call um but now the the application layer is doing work as part of this
test right application layer and service layer are synonymous yes okay yeah sometimes I'll say application service layer
but it's it's the application layer but even that like and I'll also refer to as use case layer because that's basically
where we talk about what do you want to do um things I want to do are add songs and search songs by theme those are
those are in a sense highle task that the that the user wants to do got it in that case I resend my suggestion I think
I'm I'm good with so uh end funter zero uh suggests removing added but actually what we're testing here specifically
explicitly is is that it's that that multiple added songs are found by their theme that is that is the entire purpose of
what the application layer is doing added and that's an important thing is when we look at this test and we say what is
actually being tested what Behavior are we testing um what we're testing is the middle part right the you know whether
it's rrange act assert which I don't like um or uh setup execute and assert which is my preference what we're executing
the commands we're executing yeah oh was it the when you said uh assert assert it's sea which is nice oh that's nice see
yeah the problem I have with with arrange act assert is people get the order confused yep um there's also given when
then but I feel like that is uh in almost too abstract um so I I I adopted Mazar actually calls it setup execute verify
um but I like assert because it's it's very specific to what you're going to be doing which is writing an assert
statement yeah yeah verify has has some uh other meanings that that I didn't want so I was very straightforward um so
yeah uh should we do a commit just to yeah register that one thing I'm trying to do more in in my own work is is commit
more often um yeah because I'm I'm very bad at that is that correct spelling I need I guess yeah shift Escape okay uh we
haven't run tests today so let's run everything yep so have you have you ever tried uh TCR no it's on my to-do list but
I haven't tried it um I know we did it once in an ensemble were you there for that you might have been there at almost
every Ensemble um that was when we used uh so there's a plugin for TCR for intellig and it would then pop up um every
time something pass it would pop up do a commit and you and you make a choice from that uh I have I want to try it again
because the way that I do something not quite similar but um is I tend to write and we've seen this on on stream here is
I tend to write the the larger tests and then get it go from one red to a different red perhaps even to a different red
where each one you're you can predict exactly how it's going to fail uh and then you get to Green whereas uh with TCR
you would do it you you customize those assertions to each each little step so I already kind of do that idea of really
taking these Tiny Steps um but uh I just have to I I'd like to try it again one thing I wanted to say about the um TCR
was uh I was lucky enough to have uh a meal with uh Kent Beck like around when he was doing TCR it wasn't me it was like
a larger group right but um and he was saying talking about TCR and he's like yeah when somebody proposed this idea to
me in other words he didn't think of it right somebody he's like I thought this was a horrible idea right and he's like
I gotta try it right and um and so that was really refreshing to see that approach to to to work and to life um and it
kind of made me go oh yeah I should be doing more of that like and not just give it a quick yep I was right that doesn't
work right but like really um let go of expectations and give it a role seriously and find out what you can extract from
it it's a value or if all of it's a value right yeah so yeah so it's cool so I think uh so you mentioned did not produce
very good code in the end uh hard to focus on the big picture can see getting sort of caught up in constantly having to
to redo the code if if the test fails the idea of TCR for those who don't know is test and commit or revert so you write
a test that fails your next action has to be where it passes otherwise the code gets reverted um and either you do that
through uh a plugin that does it for you or you do it manually um but I can see how you it can if you're just starting
out with it you could get wrapped up in in in a lower level stuff um I would think that yeah so so so you're focused on
this uh and so I think that that's really interesting because whenever you learn a new skill you're going to be uh and I
posted this article in Discord about how people learn it's like novices executing the instructions the rules and
applying the rules and and so you're you it almost feels like you have blinders on because you're focused on just let me
do this right uh and so you have to get to you'd have to get to the point and this is where I think folks don't give
whatever they're trying out a chance um because they don't get past that stage and so it's like oh this doesn't work
because I can't think higher level um well you can't think higher level because you're still focused on learning the
skill and I think if you really really wanted to give it a try you'd have to do it enough so you say now I can do it
without having to think about the steps and thinking about uh getting getting the code to to not be erased um and you
start get more fluent and then you'd probably start be able to to think higher level or it may be that you practice it a
lot and you never get to that level and then you say okay this isn't this isn't going to work so so that's interesting
hey Next Step actually uh so I think J closed that's really more of a note than a task what the hell I don't care it's
not like um so what we don't have is saving in any kind of well in a sense and this came up yesterday uh in a sense
right now our song search our not song Searcher service because it has the reference to the song Searcher uh the song
Searcher is so what do we do we want can you toss up the hexagon what we talk about yeah I think that will it certainly
help me but I imagine it might help people who are thinking or I mean watching so repository would be over in the
persistence right the right hand side yeah and so the application layer would talk to the port for the persistence right
and it's um it's really right now it's basically can we can we hold the song Searcher restarts because right now as long
Ser is running we we keep adding songs it'll it'll it'll find them um but at some point we want to restart the server uh
and or it may be restarted for us but certainly every deploy that that you do is going to they going to restart it so so
does that mean our the song Searcher should be moved out no if well if we're going the direction from the design
direction that the song Searcher is the domain uh and it's in memory um then it stays where it is uh but the application
later layer needs to to load and save it right okay so load and save would that be our next chunk of work yeah to a
vertical slice where we're so what's interesting is the yeah that's going to be interesting because typically your load
and save operations are are basically the the unit of work kind of thing right in in your in your application layer so
you do a load execute behavior and then do a save uh here our load is happening when the server starts and then the
saves are happening uh basically after we modify the in a sense create the new s song Searcher um so this will be
interesting yeah so I think I think persistence is next uh and the way we would do that um normally I would create sort
of the repository Port right off the bat because it's it would be fairly typical uh here I'm not sure what that's going
to look like what do we what are we so what's the unit of of stuff that we're loading from the repository I guess is our
is so if we're if the stream search is going to be reloaded every ad oh you got a picture yeah there's a repository so
the application layer talks to to the port which basically eventually is the repository adapter and say load stuff
presumably it's it's basically presumably right not presumably right songs without just a big pile of songs a big a big
list of songs because right now a song contain and we instantiate the song Searcher from that right so so again this
goes back to the idea of Our Song Searcher is the aggregate songs are entities but song Searchers are aggregate right uh
and how to and and which doesn't match our original uh event storming um that's fine uh we may eventually get there but
um but yeah so so our uh I'm GNA bring your code back so if we go uh expand expand the window for song Searcher you're
in it right now and so if we look at this we see there's an ad method and therefore it's in a sense the aggregate
although it's not really because we're not the unit of what we're saving is actually not so so I retract my statement
song Searcher is not an it it is really some uh I'm not sure what it's just a service um but anyway I don't think we we
need to discuss much I think we can just start uh writing tests and we're still going to write tests against the um the
service layer um sorry you're in the song Searcher class I meant to to for you to show the song service class oh sorry
this one yeah so what we're doing is we're not loading and saving and doing anything we are adding songs but we're
adding songs we're not adding song Searchers and we're not reading and writing the song Searcher um we're going to
recreate that each time well I mean yeah I don't want I don't want to I don't it'd be very easy to sort of talk for a
while about whether song Searchers and aggregate or not I think we we have enough information to write our our next test
yeah um which is about persistence so do you want to add a j purp yeah let's I one I think I might have had it in down
here yeah yeah like one of these yeah so I would say it's um you don't need this one right that one's well I think
there's two steps uh there's uh create inmemory repository and then create database uh specific rep adapter we don't
need to write Jura we have Jura we just add stuff to a to the Jura it's easy easy peasy uh what was again create our
yeah there's all sorts of stuff we've talked about in terms of third party stuff but right now we're focused needs okay
sorry I was looking at the chat um so song service test is that right we gonna say that yes so how how do we write this
what is our so I think that the it comes back to when do we load songs right are we going to load them every time a song
is added because at that point we would say we have we've added some songs now we need to shove them out to persistence
so we don't forget about them if the server dies now um and then we have to well we could probably continue to using use
what we have which is create a new song Searcher with the new song appended to it um and write it out to the database uh
so it's sort of a a lower level question of do we want to read our rights or do we want to basically write it again it's
very cach like it's it's basically uh uh Cash Cash ahead I forget the the technical term but it's basically we'd be
writing to our cache and then writing to the database and certainly something could happen in between writing to the
cache and writing to the database where now we have stuff in memory that's no that's that never got written to the
database but I think we can put that concern aside um and focus on uh when do the songs get loaded I think they get
loaded when we create the song service when the in a sense the think because if we look at uh the startup class whoops
right so when it creates the song Searcher that's that's where we really need it to get loaded right so um yeah so I
think I think we give the repository wait a second yeah sorry if we already loaded it with these two songs is this test
actually so this is a startup class so it's not used by anything except the real application ah okay right right because
it's part of the spring world and we're not we're unit tests are not spring yep never mind and whether we write a test
for this I don't know I feel like it's it's obvious um because once once once we get the repository and inject the
repository into the song Searchers Constructor uh then uh then we'll swap out the the be here for that right okay so
what will we name this test startup uh past tense for Save it so uh what we need is should we sketch this one out in
comments or do you think we can do it without uh we can do that so the first step is going to be repository and then uh
create the repository uh uh and I think a step in between those two uh is add songs to song repository add songs
repository and then our assertion is we should find that those directly added songs via the song service search by theme
yeah does that make sense I think so I just want to finish typing it then I'll uh via the song Searcher theme is that
said the search by theme method basically search yeah yeah you can just say a fan by the song search it will know
exactly what yeah that okay create repository um sorry not song Searcher song service because we're we're not directly
talking to the right that's going to be a little confusing I keep confusing those two because they both start with they'
re both yeah song service and song seure so yeah we may have to rename just for avoid that confusion cognitive well song
service was was always kind of temporary anyway uh so hopefully we can come up that so let's see create song repository
add songs directly to the repository create a service passing in the song repository and then assert that those directly
added songs can be found via the song service yep that seems relatively straightforward yeah um and so here's where we
could write all the code we need um creating the song repository code on the fly or which is a very outside in way of
doing it or we could say we know what the song repository is going to look like and basically test that um test drive
that I don't think the repository is going to be that complicated so I don't feel the need to sort of inside out test
that yeah works for me all right uh so let's repository now this one is gonna want to know where should I name it and
and you can even new it up if you want really want do that uh well one with not with a postfix you'd have to man do it
so you could just create it right right now yes yep uh and application there right or uh it is application layer but uh
it's actually going to be this will be our Port so let's put it in a sub package called do called Port so don't use it
don't do it by the directory do it by the package name up above okay hey there Albatross welcome howdy all right that's
good enough um now we could do the same thing here is uh we could do it via a Constructor um the adding of the songs
basically the pre-populating of the songs in the repository we could do via a Constructor uh will that be a frequently
used construct or for tests it would so it be very much a a test oriented method gotcha so like a VAR kind of thing yeah
or we could just do um an ad so and the ad method would be one song at a time continuing that pattern yes yes like this
uh I don't think we need the word song there because it'll be obvious that that's what we're adding because that's the
name of the repository good point as well as the um yeah sort sort of uh for now yes there's other stuff we could do but
I'm trying not to take too big of a step because we're already GNA be taking a big of a step um yeah you can just copy
stuff from the previous test I was thinking something different see if I have it handle just to get some variety for for
ourselves in for I wish I had one on waves because we've had a lot of big waves hitting California right now oh yeah but
I don't do okay Ry know S I don't know if you know it uh I'm not good with titles so I might I might be familiar with
yeah if I play it for you you'll hear it you probably recognize it so we want to do yeah that'll be song yep uh go back
to the test yeah and I think what we're going to do is is this is going to be our inmemory implementation we'll extract
the interface out from it um so multiple uh so let's well let's rename the song repository first to make that repository
hello we don't need to change the local variable names right that's no in fact we don't because we actually uh
eventually that will become the interface and so we then have to rename fine um so uh sure so let's now do the next or
no I don't think we need to do that okay so yep basically what it says on 30 let's create the service passing in the
repository so do we have that service yet or we're creating a new one we're creating a new one um but we're gonna
Constructor oh creating a new one we're gonna we're gonna instantiate a a song service okay oh song service okay yeah
yeah I wasn't sure if we had it we were making a new service no we're taking the existing service and we're going to
pass in the yeah which it doesn't support so we'll go ahead and create that we want a new Constructor right uh yeah yep
and let's hold on to that field so go ahead and hit enter and then we can add the field did you want to call it song
repository or just reposit uh yeah song repository yeah that's good okay I always like my repository is named even if
there's only one yeah you were saying hold on to that buffer uh no uh click on on the gray and do on Alt Enter oh create
a field uh create field yeah final yes and so it doesn't like it because the other Constructor doesn't create uh doesn't
create it um which is fine so let's just create an uh uh we'll just be actually we don't need to this right sign you
want to assign to what uh we'll just do a new one a new in memory one yeah since yeah now I guess yeah that's fine yeah
song search is not final so we're good okay uh can you delete that blank line intell always adds a blank line whenever
it does that and it's really annoying at least annoying to um and I would put a space before 30 because basically that's
what we're testing we're testing uh that when we create a song service with a repository that has songs in it we now
expect if we do a search we will find that song so assertion uh so asks uh any advice for on Spring Boot and so my
advice is um spring.io and spring Academy has a bunch of good materials uh there are lots of other materials um
elsewhere but that's that's where i' start I started with the spring guides and I'll give my advice that I really need
to put into an article so I can just point to it which is come up with a project that is of interest to you just like
we're doing here here we're creating a project that's of interest to us uh create a project that's of interest to you
and Implement that um follow tutorials and modify the tutorials build on the tutorials don't just follow them and then
say you're done and move on to something else use the tutorials as a foundation for building other stuff um but if you
can find a project that is of interest to you that will help you um come up with interesting features and that's what
you want uh so that way you have to exercise building building stuff um above all learn uh learn how to write tests
that's my right you were muted muted I was muted so uh so we want to call the search by hey right and what's our
expectation is that song i s it in the buffer I do not actually there I do have a little cheat for the control shift
yeah control shift V let me get my cursor back where I want be yeah you never you never saved it to the buffer ah I
never did okay yeah oh it was it was saved in the OS buffer not right and that doesn't get that if intell doesn't see it
as being does know as being a copy yeah it doesn't save it yeah is that good yeah gloriously well let's be specific how
was this gonna fail I know you were gonna say that um so well won't have we haven't even written the code for ad but
that'll be a noop so we won't know it didn't do anything on Line 39 line 31 again well it'll assign the song repository
object to the field but we're not going to do anything about it so then do anything with it so then on 33 when we search
it's going to be like I got nothing on fire so it's going to have a search result of empty so I think we're going to get
a null poter exception you think we are okay cool uh let's not run all the tests let's just run the io free yeah yeah
yeah you right and that's because in the other Constructor for song Searcher which we do not do uh in in the second oh
right I was gonna ask like why we're not we should be doing something with song serger at that yeah so let's let's um
what we'd like is we'd like it to fail not with a null pointer exception we'd like it to fail with with an empty list
right so let's so this is where in TCR we basically just assert that actually we couldn't assert that from here um we
would assert that we would get a null pointer exception which which is why I don't think TCR would work for me because
you'd want the test to pass our expectation anyway that I guess we could we could modify the assert if we were doing TCR
we could say okay we got a failing test uh we want to do one small thing to get it to pass so our assertion is too broad
so to sort of take a smaller step we'd assert that um the search by theme returns an empty list and then ratchet it up
to actually return that song um let's um I think uh what we want to do is we have we want to basically duplicate the
here so now we won't get the null exception right perfect cool um even though it's I was going to say even though it's
not refactoring time we could refactor the constructors and and centralize it um but I think we can I can we think we
can wait on that all right so on I'm not sure why that empty space is there do something uh so now there's no no code
that song service needs to do just yet um yeah and so this is this is sort of the the the problem with not testing the
repository right now there's basically two things missing there's the implementation of the repository to track songs
and there's the missing functionality of song repository that feels like too much code to write for one test song
service or song Searcher you meant song service right uh yes song service okay so there's the repository implementation
that has to track songs where ad has to work and plus we don't even have a a way to read stuff out of of of the
repository um I think I want to take a step back meaning disable this test and work a little bit lower later um no I
think I think uh instead of I think I want to throw away the usage of our in memory song list and then we can
encapsulate that list into the repository because what we're basically writing is is a list right we're our repository
is going to be have have an method and a way to get all the stuff in it and that's just a list so we're sort of we I
think we're we're premature in in extracting the the inmemory delete yeah so so unsafe delete uh no no let's let's just
instead of in memory s repos repository just say list of song call it internally we'll still call it song repository but
we it'll be a list of of song so you just say on the list and then open close angle bracket and then on the left side
it'll song uh no service is not a controller service is part of our application use case right uh and now let's change
our 32 to be uh to be of type list so let intellig I think intellig will let you do that let's see what it says yeah
change signature signature yeah um too too fast I'm not sure change it on I don't know which one it did let's go back
let's go back into let's look yeah changed the wrong one undo can we spe so again Alt Enter is your shortcut for the
bulb light bulb yeah so we want the third one because we want it basically where it shows it removes the memory s
repository yeah right okay um and now let's change our song service on the bottom on line 11 uh what is it doing in the
Constructor that we just modified it's probably broken yeah let's change its we want to change the field yep now cause
the Constructor above to to be a problem that's fine and there we'll just say uh empty list is there a no there's
nothing automatic that's G to here like that yep uh and we can go ahead and delete in memory song repository because
we'll bit all right so if we run this test happen well song search is still building its own thing right independent so
it'll get the same I think it'll be the same it'll be the same thing yeah basically the the empty yep yep all right
that's good and it's exactly top of the hour do you want to take a quick break yeah actually I wanted to um for the the
folks who are watching who I've often wondered this and it came up yesterday when I think I said something about like oh
it's top of the hour so how many people know or don't know what the phrase top of the hour means because it's I think it
comes from analog clocks yes right so people that have grown up with only digital clocks yes does top of the hour have
meaning to you or is it do you get it so I just wonder if it's a term I should stop using because there's a certain
generation that doesn't know what it means you know so that's interesting because uh uh we got Asher my son a new chair
uh for for Holiday birthday um and so we're putting it together and I said turn the the screw clockwise right same issue
uh so same issue it's like if all you I mean heck nobody even wears watches anymore unless it's like a digital Apple
watch or something um would you even know what clockwise means uh so yeah so same kind of I think he knew what it meant
because basically for years you know whenever we build something that's what I say it's like okay clockwise is this way
and counterclockwise is this way right but I think it's I I feel like you know there there are idioms we use that
doesn't necessarily mean you had Direct experience with with the thing where it came from yeah yeah yeah yeah that makes
sense yeah on that note food for thought for a break I think five probably be five all right folks just as a reminder if
uh you want to find me on various social media Mastadon LinkedIn and so on uh ted. about is where to find me that has
all the links to my social media where where I'm at uh and if you're not already a member of my Discord community and
you want to talk about basically the things we talk about here on stream uh writing Java code spring boot testing domain
driven design test driven development hexagonal architecture all the those things uh uh join the Discord and there's a
great Community you can ask questions you can participate in discussions and uh we'd love to love to so test fail as
expected uh let's see if we can get it to pass so where were we my brain so oh right add song is not actually adding a
song to uh no that's that's fine it's um it's the Constructor that we need to to fix right because what we're testing is
is again on the top line 31 our Constructor that if we give the Constructor uh a repository a repository oh um then it
should be able to create a song Searcher contents so I think uh this is actually going to be Searcher it has a
Constructor that takes vog list yeah so we've got two choices uh we convert from the call site we can uh we convert the
list that we get into an array uh the other option is we create uh an alternate creation on the song Searcher list so
the array can go in as the vargs the vars will understand the array yeah so vogs is is basically syntactic sugar so the
pros and cons of each approach if we Constructor well I guess it depends what we ultimately want to use well I think
both I think both are useful so I would I would lean towards uh creating an additional Constructor that takes a list
instead of the VAR ARS or an additional create method actually oh instead of the Constructor you mean additional create
method well here's where it's like do we do we create since this the Constructor is private um it would have to be a
create method we could make the The Constructor public um the other thing is we could migrate The Constructor a list
would be more convenient for the Constructor because right now we convert the list to a stream uh sorry we convert the
array to a stream um down here it's a little bit so and it would make that easier as well if uh create song Searcher
took uh took a list in fact really a stream might even be more optimal because we're we're always doing something we're
always processing what we get but we'll start with a list so would we just change the signature of create song Searcher
or make a new Factory do parallel change um well we want to H we want to have both so we don't want to replace it yeah
so so for this one instead of this we want a new version that takes the list thanks right oops name's okay y uh so here
at this level song Searcher should the the name repository what we call it songs I think idea so now we can call the
other Constructor and convert the list here to to the array does it take oh it does HT wait second no okay sorry I was
runaway driver no you were not runaway I I oh you did give an instruction I'm actually not sure about this part of it so
that's actually a better description so here uh yeah we want it to continue to array is there a songs like to array
there is here we go and we have to give it that that type structure again so it is yeah right there song open close
right y so if we do that is it gonna pass I will no it's shift F1 no why did shift at 10 not work there we go I don't
know I must have had the cursor some way funky sweet all right terminology I don't know not so much business e but yeah
so I I um you have a different idea I I think something more towards uh song from uh and in sort of in quotes from a
outside you want to change repository outside yeah because it's that's really what it's doing it's basically from from
actually how uh let's say song service loads songs upon startup that's actually more a little bit less Technical and and
so now um what would our next test be so they're loaded on Startup and we probably want to look at the symmetrical
what's the what's the loaded unloaded well so uh so we load upon startup what's the other aspect of persistence is when
we yeah added songs you say persisted uh I think we can just say added songs are better so now like this would be a um
setup and then we'd add another song uh is that what you're thinking I was thinking that it starts at empty and we add
one and it should have that song we could do that and then it should have both um that might be better to show but uh I
is too big a step or you think not that it's too big a step um somehow it feels less precise to do it uh but I guess we
could build on the previous test so is it is it better to add one to nothing and we end up with one or is it better to
add one to one and we end up with two which is sort of more complex behavior let's go with let's go with basically what
you had that we start off with with one song as part of the setup um and then and uh when song you got another fire song
oh yeah I'm not I'm G to do ring of fire but uh let's do something that's so there's one it's about fire but fire is not
in the title so that's what makes this interesting right thematic songs right right if it's in the title well that's
easy to find or easier to find right so what were you going to say uh so here though we want to add it through the song
service not through the Repository right yeah I had it right did I the as1 will want Ah that's a tab was what I was
missing So You tab or or enter or enter again enter ah that works too cool so now we want to make sure it's saved and
again we're working through the service we don't have a query do uh we do oh well what's our what's our Repository right
so here we're we're here we're testing the interactions between the service and the repository so here we're saying when
we add a song to the service it is persisted and our right now we just want count is that sufficient we could certainly
start size yeah now is that going to work and so maybe we in our test we want to say we maybe want to be more explicit
and say save to two yep oh interesting it does uh it dumps the yeah that I wonder if that's a recent change because I
don't remember doing that before yeah I remember seeing that that's interesting and it's the Asser I like it cool all
right so now um now it gets tricky uh because um it never it it so we we pass in a reference to this repository uh but
it doesn't actually use the repository as its storage mechanism right and how do we and so the goal is to move it to
that without breaking all of creation we probably we have a lot of tests that other so parallel change the parallel
change to get this to pass then moved everything to the new what are you thinking with a parallel change I don't beyond
that I don't know the specifics I'm just thinking it a higher level like if we did a parallel change could we right I'm
not sure what yeah uh I think we have no choice well we do have choice but I think the the next Way Forward um is to do
uh a prepare refactoring which pulls the class because once it's in its own class right all problems are solved by
either adding or removing a level of indirection uh and what we need is to right so let's test and since we're going to
do a refactoring that may or may not work out and so we can just say factoring and so now we can use the magical uh
extract delegate ref factoring on the song repository at yep alra doesn't have his own shortcut does it Mak refactor
this yeah it doesn't yeah I guess it's not that commonly it's not it's not terribly common yeah and so here's where we
we can call go uh would it be package application or we'll leave it an application when we extract the interface around
okay um make sure you generate accessors there at the bottom and which do we anything else we're checking NOP nope
firing who it's unhappy because uh it wasn't necessarily initial ized and so final is is having a problem which uh is a
bit annoying um but that's fine we actually don't want it to be final I don't know why it made it final that makes no
sense was it Final in The Source before we did the refractor yeah but that shouldn't M I think that's a bug because we
we basically said provide accessors and if you're going to provide a Setter then it can't be final then it can't be
final so that's good point that's a bug that's a bug I should I should file that let me write that down you make a note
so hour one 25 book okay um so all of our tests should still pass this shouldn't have ch this shouldn't have changed
anything uh especially okay service and what we is I think that's fine and now I think we can reenable the okay
rerunning make sure we got the same failure yeah thanks for the hydrate request go for code and go hydrate actually it'
ll be a caffeinate enough so we had the same though uh oh no we need to make one more disable yes okay and the what we
want to do is the reference that we pass into to the song list ah here yeah what's the usage we got on it two of them so
what we can do is we can introduce parameter with what we want so the parameter we want to pass in is the actual song
repository class so would we do cursor on song repository and then do the um control to P for work maybe doing one yeah
I didn't I didn't think that would work I was sort of surprised it suggested that because that's not what we what we
want um what we want to do is we want to have a local variable that uh so we want to push the creation of the song here
so we don't want to just do a set song repository here we want to do this song new um I'm not sure what happened there
yes that's that's fine now what you had what you had was fine um but delete delete the we're not going to call the a
Constructor with a stuff is that what you meant by the red stuff yes okay um what's it complaining about oh song
repository is final is that what it's complaining about yeah but it took oh oh oh oh oh okay yes because it was already
assigned so we can't reassign it uh do we no longer need to do the new online 11 and have it yeah so let's let's new it
up um in the other Constructor as well probably could have inlined the let's let's undo a step a couple of to yeah yeah
uh if you Alt Enter on where you are what does we can we inline it I don't necessarily want to inline I want to inline
the creation oh can you go up to the um line 11 the song Repository field and Alt Enter there uh move initializer to
Constructor want ah can uh let's make line 22 yeah do you is this shortlived so song reports already one is fine uh yeah
that's fine that's because it's conflicting with the incoming name and then what we want is uh so the red stuff on 23
that should have signed it to the local variable not that this one second Ted I have to pause for y yeah and so once uh
once we do that then we'll be able to extract both those I think as we should be able to introduce that parameter
although we may not be able to yeah go ahead yeah um I didn't hear what you were saying I had no no that's fine I was I
was I was talking to to to just to the viewers uh so yeah so let's do uh that assign that to the local variable s
Repository ah I'm sorry call no no you were you're right so call set call the set on our local variable ah got it yes
and now assign that local variable uh to this do song 23 there's a bit of a roundabout way and I'm not sure it was worth
it yeah I'm not enely sure where you're going but I'm just uh definely in driver let's I was hoping to introduce uh
introduce parameter right but because song repository doesn't take anything in this Constructor H it's not going to work
were you thinking of so let's let's try it I'm I don't I don't know if it'll I don't think it'll work but let's do an
there like that yeah and enter oh it did do the right thing good on you intell you made up for the bug so um if we I
almost want to like watch that video really slowly to see did it really do the right thing yes um so it didn't quite do
everything we need uh because we're still calling the set song repository on the on the inside here but we want to
actually push that out so it actually didn't do everything that we needed it to do so I take back my admiration it it it
looked like it did it because deleted two lines but it um is there factoring that could push that behavior out uh not
really once you're in Constructors it gets a little bit hairy so I think what we'll do uh all our tests should still
pass though let's make sure we because we've got we're in a really odd State I was just thinking like we haven't run the
test in a while yeah okay good just yeah let's let's delete line 22 sorry or 22 and uh let's go into the callers of that
Constructor there two yeah um so that one think uh our variable names are are now getting confusing so let's uh because
now that we actually have a song repository class um let's rename the variable on yeah and now we can uh create a song
repository and do a set on it you may not like this huh yeah because you basically you got some red so it's not going to
be able to auto plate um so you can just call the song repository delete the word new so you can just delete the space
oh right a new and then say equals new song repository actually we could have extracted to a variable uh let's do that
so undo okay how far back uh keep going keep going keep on basically until we get song repository new okay yeah uh on
the next line at the end extract new song repository to variable and look at that it actually selected the name that we
want so do that uh swap 32 and 33 yep what there you go uh let's drop the word new while we're here let's just rename it
and now in our uh and let's go basically we could probably copy and paste this okay and go to the other usage which was
45 yeah so uh let's again rename song repository list and then you should be able 45 oh you didn't copy the creation of
the song service thought I did yeah so you want 32 to through that and then basically replace that yeah um let's run our
tests I still think we're good uh so let's now clean up our Constructor because I I think it got a little messed up in
the song service yeah so we don't need uh so let's uh let's delete the first parameter on line 20 uh interesting oh
actually ah so what we want to do first is on line 21 instead of getting it from the list we want to get it from the
Repository so uh in instead of song repository as the parameter say song repository new DOT get oh yeah and now we can
get rid of the yes and run the tests all right great uh let's rename that to let's we'll clean up the other Constructor
later uh so let's go back to our tests um let's reenable this test so still expect it to fail in the same way yep great
uh let's change our assertion because what we want is not to assert against the song list what we want uh is to actually
assert against the repository right so we want to say the repository when we get the list from the repository getet that
should have size of fail yeah um now we need to update the the repository when we modify it so now in our ad song that's
where we need to so all this was was our prep Preparatory refactoring to get to the point where we can finally in adong
uh modify the modify it to update the Repository so do you yeah so so far it's all connected to we would this be a
parallel change thing where we work with song repository get that to work it's not a parallel change it's it's we have
to update two things we have to update the inmemory and we have to save and update the external memory so we're we're
basically synchronizing uh our storage okay yeah I hadn't add and yes this is very much uh uh feature envy and we'll fix
that yeah yeah wait a second no just need the field no no you got to do add because we need to add it to the repository
oh right I was thinking I had to put it in a local variable but I don't I can just yeah right yep yeah now the feature
memory is very yeah I was concerned that we might get that uh and that's we you'll notice failed so a different not the
one working on yeah right um and this is because an empty song service gets starts its life as an empty list which is an
unmodifiable list right because we originally had it that it was and here's where TCR would basically revert our unfair
yeah so SE line 17 we uh we want list and so that's sort of the danger of if you're not sort of aware of it there the
danger of using something like that something like that meaning meaning uh collections. empty lists which is so if you
use empty list or use a list. of you're going to end up with an unmodifiable list oh right they give you the immutable
list yeah so would this fix it this should fix it okay we'll find out yep yeah commit how would we phrase this um song
service now saving to repository and I think you can just say uh uh song service now to ads like that yep so uh so it
works we probably should do some refactoring yeah so one we're factoring we could do is um pretty much the the feature
Envy we want to fix is any any use of Setter or or getter and so uh we should basically that should just go in the song
repositories Constructor this one here yeah is there a uh no there's no unfortunately once you're in Constructors
because they're it's interesting how intellig doesn't treat them as regular methods um and so you end up uh you could
extract it to a method and create a create Factory method um and then you could inline it that into a Constructor so
let's do that so let's take 16 and 17 and extract that to a method and we'll just call it create um now we can uh
interesting why did it do final we don't want yeah that's weird just do a join on those two me I really need more
monitors H oh I closed that no it's still here control shift J final okay we should be able to make that static so you
can uh click on create or you could just type static and see what happens or we going say click and create and uh and
bring up the refactor this menu ah that one would do it yeah I always recommend folks on Windows assign uh a different
Global a different key map because Control Alt shift is really awkward yeah so make static uh yes refractor I don't know
what yeah perfect and so now we can basically Repository and escalate because we want to make yeah um I think that's
fine for now so let's go back to here uh let's go to where we're where else uh let's go so let's do this the sort of the
proper way um let's go to song repository and look for access to the the setter is there any other access to it we might
have some in our tests so the setter not the getter yeah know took me a second yeah uh so let's go and fix method um
maybe that will will pick that up automatically so let's um where is this create this create is called from here right
yeah okay yeah want go back to the to the get right on yeah but first we need to to uh make it so that the create method
um take takes a list so let's on 13 extract that as a parameter introduce parameter on that the whole thing on the array
list ah what do from here it'll do it from list all right and now uh if we scroll down oh that's it um what's that other
construct there oh we we'll leave that the on the getter on line 17 where is that used service uses it twice it right um
so I think I lost the the the train of thought here I wanted to add a parameter to the create method because I don't
want the setter oh so let's look at usage as a Setter okay that's what I wanted to get rid of so there's the internal
usage which is kind of ridiculous let's let's not let's just assign do the assignment on line thir oh no we have to do
Setter never mind sorry oh because because it's a static method right uh so let's do the setter let's look at the test
yeah that one um yeah so we can replace new song repository with uh just song repository. I was hoping intellig would
pick up the fact that that was exactly what we just refactored to but it didn't and I can get rid of this complaining so
uh hit control uh go to the reference calling ah so what is the what is the what is the error message that's being
reported 31 uh so don't hit Alt Enter if you want to basically just Mouse over it uh and it tells you so what it's
telling you is the required type is array list but what we have is a list and so when we did the extraction uh it it
took array list instead of the instead of list so let's fix that on bottom yeah uh let's run our tests yeah I was just
thinking time yep and let's fix the other test to do the same thing to use the create method yeah so on the Top Line 39
Oh 39 you can jump to it also yeah oh yeah create now I can delete this and it's yep all right so I think this is a good
place to stop especially since I know you're you're up against time yeah in theory I'm about to find out but um actually
I did tell them to come tell me so uh so this was pretty much starting the starting to fix uh F or fixed some feature
repository sounds good should we do commit push sure we been I think we haven't looked at uh I didn't I know there's
some chat messages but those were sort of off off topic and I know they were okay you're up against time slot so I
figured you you could uh head out and and I would talk about those or we could those until you have to leave so oh man
the whole thing yeah so just skimming but yeah major sigh yeah all I can say is sorry situation I'm gonna mute for a
second and before I sign off and just double check um estimates are sometimes a fact of life there's a whole other topic
around doing estimates uh but estimates are estimates they are not guarantees they are not promises they are estimates
they are I don't I even prefer the term best guesses they are a guess uh and so a you shouldn't feel bad if you don't
hit your estimates very few people do and certainly almost nobody does on a consistent basis um secondly uh you
shouldn't be blamed by others for not hitting your estimates estimates are guesses and anybody who insists that that
they want actual promises um you need to then say if you want a promise how sure do you want me to be you want me to be
100% sure good I think it should take me two weeks but if you want a 100% promise I'm going to say two months but if you
are willing to put up with some uh possibility that I exceed the estimate then I'm willing to say okay I think the 80%
chance is I'll hit it in three weeks there's certainly the possibility I could do it in less the problem is is most
management doesn't recognize the idea that that these are guesses and that there are probabilities associated with it so
there's a whole area of estimates and things like that yeah um and so uh so the fact that your scrum Master is forcing
you to put estimates that's not their job the scrum Master it shouldn't is not management and and it's unfortunate that
it has become uh this is why I think scrum is is a complete and utter failure mostly because of how it gets implemented
scrum Master should not be demanding anything scrum Master is there to help guide the problem is in most places that do
this they do tend to be see their position as basically project managers so uh I've been through this stuff in in the
past 20 years and seen what was wonderful about agile has become basically another word for yeah it's horrific yeah um
and so scrum Masters in most places are project managers and all they care about is estimates and schedules and things
like that in which case they're not really scrum Masters uh and you're not doing scrum uh you may be doing something but
it is agile yeah and so uh this is a common anti a common problem with scrum like and because this isn't even scrum um
and with similar things is spending hours discussing and estimating tasks which which is pointless stop doing it do the
work there's no point in getting more precise than I think this is going to take a day or two I think this is going to
take a week anything that's takes longer than a day or two though should just be split and so I think one of the key
things that really helps uh in a lot of these situations is learning how to split whatever you're given whether they're
called stories whether they are or not um with call requirements whatever they are if you're given it and it's going to
take more than two days say what piece of this can we Implement that we could verify and do that so what you end up with
is not estimates but a bunch of things that take one to two days and if you can't split it um I would challenge you to
to to really try and split it there's almost always a way uh if you look up splitting patterns you'll find some some
good techniques but there uh I used to do this early in my career take lots of times to do estimates and there's no
point to it you will not get better at doing estimates by spending more time on it what you want to do is as a team
don't do planning poker put all the stuff on cards virtual or not and basically say is this one or two days or is this
more and put it into two piles and then go through the piles of the ones that are more and say we need to split these
until we can put that in the other pile and then you end up with a pile and it shouldn't be a big pile you shouldn't be
estimating more than a couple of weeks work at this level and you end up then with a bunch of cards or or things or
stories whatever you want to call them each one of which is is one to two days then you don't need to estimate you just
say how many cards do we got multiply by days and sprs yeah go ahead I don't know I just have something about um they
avoid the Trap of falling into getting better at estimates yeah the industry has had 40 Years of failure at estimates we
know that we cannot estimate well and it's not us as a failure as humans it is the the fact that we're building
something new and so it's not like hey how long is it going to take you to build a car well we already know how to build
car a we just building a second one right that we know but we're not doing that we're we're we're designing the car and
that is much harder to estimate matter of fact it's we've shown it's impossible to estimate so well I will I will say
that there are techniques to improve estimation um this Monte Carlo and this this forecasting things like that the
problem is that most management doesn't understand probability right they don't understand probabilities I would I would
call that forecasting not estimating in other words they could improve their ability to plan by using the Monte Carlo
forecasting stuff I guess I wouldn't call it estimating I would say gives maybe I'm being pedantic here it it it serves
the same purpose but I agree that um there's there's no point to to me the best way to estimate is to break stuff down
until it's obvious how long it takes and the stuff that you don't know about you'll say look we don't know we need to do
some research on this so it takes as long as it takes um but it's it's a it the whole idea of schedules and dates and so
on is is is management dysfunction in understanding how software is developed unfortunately as developers we have little
power over over changing that and um and I want to Mike and I want to say that um Sprints are not deadlines Sprint
commitments are not promises and anybody who says that they are does not understand scrum period and I'm very adamant
about this because it is an extreme dysfunction and completely unfair and really makes life terrible for people by
saying You must finish this by the time you promised um I would never work for such a place and I would be busy finding
another job if I if I felt that I couldn't change the situation but I think this is uh a completely 100% ridiculous
thing to say your Sprints are deadlines and you must finish this work by this date that is ridiculous that is unfair and
that is not how software development works and any place that is doing that does not understand how software development
works and is treating developers like uh basically order takers short order cooks not and I think this is what has given
agile and scrum a bad name is a compl complete lack of understanding and misinterpretation of what the hell Sprints and
scrum is all about you look at the scrum guide and it says nothing about you should be penalized if you don't hit your
commitment that is ridiculous because here's what happens you're gonna say I'm getting burned by not making my
commitment so I'm GNA give you bigger estimates to protect myself I think this is going to take a day I'm going to say
it's going to take a week and therefore I'm sure I'm going to get it done so I don't get burned and that is how software
goes out of control and I think this is ridiculous but unfortunately it's commonplace but you then have to decide do you
want to continue working for this company or not um how much you can influence uh change um but ultimately you're going
to have to add a lot of buffer to your estimates if you are getting forced to abide by those estimates and that's what
happens and that's what uh management doesn't understand is that they say I need you to get X done by a certain date
what date do you think you can get get it done by if you know you're going to be penalized for not meeting that deadline
you're going to put in a huge buffer and what happens is those buffers get added up by over the team and over the course
of multiple releases and this is why stuff takes 18 months two years to deliver anything scrum Masters are not project
managers if you go and look at the scrum gu gu nobody reads the scrum guide and therefore nobody very few people are
actually following scrum and it's terrible and it and it's horrible and you shouldn't stand for it um this is why I
think we need unions for developers we see ourselves as white collar workers and therefore knowledge workers and
therefore we don't need unions the fact is though we don't have power and we need power because we need to push back
against this ridiculous idea that we can estimate how long things take to the Precision that management often wants and
we can't and that's too damn bad for them that they they don't like it when we're late well then let us do our jobs
we're professionals um and so uh this is where there are small unions starting to to grow because these are some of the
issues these are horrible working conditions if you're asked give me an estimate I'm going to hold to that or penalize
you I'm going to give you crappy estimates why wouldn't I um and and that's just not going to be good for for anyone um
the fact is is that this misunderstanding of scrum is commonplace I hear nothing but but horrible stories whether they
call it agile or whether they call it scrum um I hear nothing but but bad stories because all management does is
basically replace the word project management right in the old days we call this project management now they just call
it scrum but it's the same thing of management else um so I mentioned this before yes break things down into smaller
pieces you will you will be able to estimate smaller things rather than larger things uh and so break them down into
smaller pieces but don't break down months worth of work break down the next two weeks of work right because you're just
talking about the the next Sprint if you're forced to to to commit to that um and break it down to pieces that are
smaller than a day but if you are going to be held to your estimates your job then is to pad your estimates because what
else are you going to do if you're penalized for missing deadline then give them longer deadlines they're going to say
no we don't want it by then it's like you either get it when when it's done otherwise don't ask me for estimates just
give me a date and we'll write crappy code to get it out and then we'll have to spend a lot of time maintaining it and
this is companies yeah exactly right they give deadlines whether they know it or not and I think ignorance is is not an
excuse management must must if they're going to do software development they must understand how software development
works and they don't and they don't care uh they most of them do not want to understand and they think it's it's work
that uh is just like anything else you push people and they get it done and that works for a while um but it ends up
with a crappy software with people who don't care with people who are looking job and that company will continue to lose
good people and only get people who choice so the thing I look for when I'm hiring people if you want to modernize and
you want to inov um I'd be careful about cost saving I don't care about cost saving I want to be modern uh which means
very much having lots of tests doing lots of refactoring and what you want is somebody who is willing to learn so
questions I ask people when they're when I'm looking at at hiring them is what new things have you learned and how did
you do it what do you now what things have you tried to learn and decided yeah that was an interesting technique but
that didn't work for me me because it's those people who and we were talking about this much earlier in the Stream those
people who try things out to see if they like it or not rather than just say I don't like it Without Really Trying it
which is the reaction I get a lot to tdd is oh I don't like it and I ask them well have you tried it how long have you
spent with it it's like oh yeah I spent an hour and I didn't like it like I'm sorry an hour is not enough time to know
whether you can really like it and be it and yeah a lot of what we see as quote agile is not agile I've been around
since since before agile was a thing agile was a reaction to very heavyweight methods and the Pendulum sort of swung the
other way um but again management has just replaced project management with quote agile and it's not really agile and so
you end up with the same name uh yeah unfortunately when you know you've got lots of layoffs in the industry and you've
got lots of lots more sof developers looking for jobs um it means that uh management has more power because we don't
have unions if we had unions and widespread unions you can you can bet your rear end that we would not have the massive
layoffs that we have had because you look at the the recent wins that uh unions in the car industry and elsewhere have
had and they've prevented it and so unions are power and the fact Society we as workers at least here in the US in other
countries it's different because they have different laws about firing people but here in the US you are generally an
atwi worker which means you are at the whims of management so if any management or company says you're part of a family
family that's a load of crap you're not um if anything you might be part of a sports team like Netflix sort of uh uses
that metaphor but you're just to a lot of companies a replaceable Cog and so it does put more power into management if
they can basically fire people and now have their pick of people who are desperate to get a job I know lots of people
who who've been looking for many many months if not a year uh who are but it will come back to burn them I hope that
software developers have a long memory and say what happened in 2022 and 2023 when you fired a whole bunch of people are
you going to do that again yes they are and then don't work for them are you did you treat your people bad when because
you could I'm going to remember that and tell other people and you're not going to get good developers anymore so it
really be a question of how long a memory do we as as software developers have yeah it's sad because it doesn't have to
be this way um and goo Hill talks about this that the the amount of of money that we generate because even doing it in a
crappy way even doing software development in a really bad way makes so much money for companies that you could do it
really bad B and make a lot of money and until you actually need good people to make money this will continue forever
yeah so hopefully if nothing else you're not alone you're not the only one struggling with this yeah deadlines the whole
idea often is to push people um but a lot of times it has the negative side effect of I'm not going to make it anyway so
what's the point I'm going to get penalized no matter what so I'm just going to relax and maybe I'm not going to even do
as good a job as I might have had there not deadline yeah and we're treated as code monkeys because they have all the
power and by they I mean management especially at large tech companies but elsewhere too because I again this is I am in
the US and so this is very us-centric um there are other countries who have much better and much stronger laws about how
people can be laid off and what happens there they have most likely different dysfunctionalities but because of this
fundamental aspect that companies make a boatload of money from software that it doesn't have to be well yeah so I I
don't not quite sure about what you're asking here but um kbon is another thing it's it's a great technique for for
sequencing work and figuring out what to do um but ultimately until the S the ideal way to work is don't have iterations
don't have Sprints just work on the most important things to do next work as an actual team which most companies don't
they're just a group of people um and work on the most important thing get that done and then work on the next most
important thing uh the saying start finishing and and stop starting new things start finishing what you're already have
in progress so limiting work in progress is one of the key ways to to get stuff stuff moving but ultimately um there's
just you know to a certain extent a lack of trust uh and management has all the power and so that that uh comes up in
all sorts of ways um and if if a product owner is looking at code like that's not their concern um even management uh
you know they can help you with code and and Foster building learning processes and getting the team to work together um
but you shouldn't uh but like product owners and scrum Masters they they shouldn't be code uh this is an amusing
question because is anybody doing scrum by the book as it as it was actually meant to be done and I'm and I know there
are companies that do that but they are in the the the the small minority of companies most have uh like I said
basically just replace project management with a different name which is Terri a terrible way to develop software but it
works because it's so darn efficient to create software uh and make money off of it in in most places even if it's
really terrible software um because just the Leverage brings so I think um yeah combon doesn't I don't know that it that
it doesn't encourage it it doesn't force you to break things down into small pieces um but if you are doing kbon where
you are limiting work in progress because in my mind if you're not limiting work in progress you're not doing combon
combon means not just you have a storyboard you go from you know to do to doing to done and delivered um but that it's
you can't be doing more than one thing or two things so if you limit work in progress and your items are huge uh you're
gonna find it better and have better flow to to make them smaller so I actually do think if you do it correctly with
work in progress limits it will eventually encourage you to through oh yeah I mean you know and this gets into all the
the story splitting and delivery and continuous delivery I'm a huge believer in continuous delivery um getting getting
you know oh it hurts to to deliver we'll do it more often right that was one of the things from extreme programming
which is it hurts to do these things it's painful to do these things it's timec consuming to do these things and this
almost non-intuitive way of saying well then do it more often right it's a pain it's painful for us to release well if
we do it more often you know then it actually becomes easier because you find ways to to adopt uh different techniques
and you deliver smaller pieces um and uh we tend to like to pile on rules and Gates and and things that stop things from
going to production but you need to do is easier and this whole idea of releases right we want continuous delivery
doesn't mean we're always delivering new features every minute every time we push um but we want to be able to uh and
that's that's that's the fundamental and continuous delivery is is I see sort of this overarching thing that really then
encourages all the other good practices like if you're doing tdd it's more more likely that you can releasee stuff that
you know Works um doesn't eliminate all bugs but it makes it if you do find a bug it's faster to fix and uh you're much
more likely to have have fewer bugs but you still need to do things like do some design and talk to your customers um a
lot of times developers are at multiple levels distant from the people who are actually using the product and that's why
so a lot so much software is terrible right I always think of expense software like concur it's terrible because the
people who are using it and the people who are developing it they're not on the same page and in fact the people who are
buying the offer are not the people who are using it so you problem well different companies set budgets for roles and
hiring in in many different ways um and so that's completely up to how the company company does that some companies will
have you know here's the the salary band for this position we have uh budget for these three positions that we're going
to hire in in this period of time um and then you you hire them you do the best you can uh sometimes it might not be
enough and you might have to search for longer uh which is something that often isn't taken into account by management
if we don't pay as well then we may be able to find good people but we probably will have to look for longer um or we
might be able to because right now there's there are more people who've been laid off and so there might be more people
who are willing to accept a lower salary and so we might be able to hire them but we may not be able to keep them once
uh things turn around which they always do uh and ultimately if you are hiring and you've got a budget and you want to
hire somebody who's really good and can and can help you know grow the team and and and help the team get better uh
that's going to cost you and if you don't have the budget for that there's not much you can do well in some ways apple
is lucky I worked at Apple um and not everything is is uh as good on the inside as it is from the outside but the places
where they really spend the time to understand what customers need that's best but it's not just that you then have to
have the developers also understand what the customer needs so what gets shipped is not what the customer needs it's
what the developers understand the customer needs sometimes that's very much in alignment and sometimes it's completely
out of alignment and you get products that's like who's is for this this makes no sense all right um that's all for
today uh that and the ranty portion of of the stream uh so thanks for hanging out and hopefully um it it helps you if
nothing else realize that that you're not alone um and that uh good developers are still hard to find um but that you
know currently where we are it make makes it difficult and you may not want to risk your current position because you
know two years ago it was easy to say screw you I'm going to go and jump to another job now it's it's not as easy uh and
so you may have to do what it whatever it is you can do to to survive um but know that things will turn around and uh
and then we will sort of be back in the position of of having a bit more power but um in the meantime do the best you
can overestimate if you have but protect your position the company is not generally on on your side uh so you need to to
protect yourself all right thanks for initiating the the the Randy discussion um and uh have a great rest of your day
have a good New Year um next year I think will be better uh than the past you know the past year that's that's my
prediction for the next year and uh I may have a stream later today but if not I will I will be streaming some some
stuff tomorrow so um have a great rest of your day have a good New Year's Eve have a safe New Year's Eve uh and I will
see everyone
