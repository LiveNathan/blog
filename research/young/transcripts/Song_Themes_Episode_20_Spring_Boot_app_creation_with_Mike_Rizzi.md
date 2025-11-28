# ＂Song Themes＂ Episode 20： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=ud-zS5ch1eU

---

## Transcript

all right folks welcome to uh episode number 20 we at the big 20 wow how you doing Mike good good a little bit more
awake this yeah so uh yesterday was only yesterday uh we were able to get our result uh instead of throwing exceptions
we able to get our result thing that returns information and so now that we have that um we need to start replacing our
code or modifying the code to use this this new good I got jerub did we forget to put that part down or or is the
splitting the results going to be necessary for that um maybe it's just reordering these two yeah so uh we could we
could go ahead and just split the results um because I was thinking about it uh and it and I think it's going to just be
relatively straightforward uh because we'll basically refactor to two um inner inner classes um that are going to be the
the subclasses so we could go down that road um which is just refactoring uh or we could move towards the more important
part which is have the uh service and controller use the new pars with result method i' go either way I'm inclining
towards the more important and then we can deal with the refactor later all right let's do that I'm really Co TOS as far
as I'm concerned all right well let's do it um so let's take a look at method a lot of tests actually not that many
tests that's not that many tests well I thought it kept going but it's just that one page so uh let's take a look at
song service let's look at the production code for that right so it's just going to get a list of songs and then uh it
it adds the songs so maybe we want see here um what tests are are calling import songs I think no one's my guess oh no
one all right um I think then what we can do is treat this as a refactoring um so call the parse with a result pull the
songs out and then it should just be the same basically in other words assume success here in the in the code uh and
then just pull the the songs out of the result that comes back so you're saying change import songs to call parse with
the result instead right right now songs no it's turning the result object so we'll have to right so if you look at uh
in fact we could just service so leave it but but inline it so if you go back into song service where were uh just in
line right there if we did that but keep everything right else it'll give us that along with our comment yes I think we
can uh drop the comment from here yeah right so that's back that should that that definitely should work because that
was an inline of working code so that that should should unless something else is completely broken that should totally
uh continue to work oh I see because it it added the um right the train out to dot songs yep uh we run all tests yeah
let's run all let's run all tests yeah um we do know that every time we do a push that they all get run and we did do a
push last time so we know that all the tests have been run yeah all right that was fine um so let's go uh look at the
rest of the calls method it should just be the tests and they're all in one test class it looked like yeah yeah so I
think um what we can do is um start retargeting those tests to results uh and then we can get rid of it would you do it
by inlining and then because we could do the same thing here right where we inline and the test will just all work but
we're now not looking at result though right I think we want to look at that that result is is Success um in in all of
these these test right we want to assert on that yeah yeah yeah yeah that makes sense um but we could I mean there's not
much to inline right it's literally calling dot do songs so there's not not a whole lot to inline um so let's just go
through it one by one and and and call The Parts with the result do you think manually do it or um yeah uh this okay
because we're gonna have to change anyway so this is what I was thinking um I was going to do this turn into result look
at result then extract songs from yep rename this actually I just want to rename I wouldn't do a rename I would just do
result and then we we'll extract the songs from the result you mean type the word result is what you're saying yeah yeah
got it and then here we do an result yeah don't wait for it to autocomplete it takes it takes yeah what is the the the
instead of waiting for auto complete what was the technique that you had mentioned don't wait just type just type just
type ah okay got yeah because if you wait then then eventually it will come up but you right so that's what we were
thinking right right and then instead of songs we can do result. songs and then run it and we expect that yeah all right
okay I we'll just do the same thing is this I wonder is this a pattern yep I figed just blindly do it if it doesn't if I
got it wrong yeah we'll quickly now this one no uh we've already we've already replaced so there's nothing to do here oh
this is okay good ide thank you I'm like why is that structure different uh wait a second this is actually wrong because
we're testing it should be that yes yeah so that one's also using uh that one's direct directly testing the parse song
so we don't need to modify that right um if you hit if you hit F2 will it jump to the deprecated method no it jumps to
that first okay but we interesting huh looks like the variable changed changed name yeah me here actually this we got
the C wrong and then this goes away oh was funny uh on on Twitter um somebody suggest said oh but what about tear tear
down that would make it seat and I'm like no you don't do tear Downs in your in your in your seat stay standing up don't
yeah just just go to C don't have a seat looks like there's one more so uh I'm looking at the rightmost gutter you see
there's a little bit of of yellow Amber here yeah and the so in the scroll bar gutter basically shows you those those
kinds of those kinds of things so you can jump to it oh wait a second I already did that one okay yeah yeah I'm I forgot
to command uh control shift V will will help you you don't need to one and the variable name is tsv yeah yep I'll pass
him all right so it my guess is now I think we've eliminated all uses of parse so if we go to pars and see if there are
any usages there any all right interesting it didn't gray it out deated yes and that's I guess I understand that because
if you deprecated it maybe you're you'd be worried about um that there are usages that you don't have access to um but
it is what it is so we yeah let's see if this yep cool quiet today yep okay so back to J uh well let's do a command yes
um there was a nice phrase you used repo was that retarget retarget is that like do you need the hyphen or no word one
word I think it's one word okay you no actually it's all of them y good enough yes do we want to rename parse with
result to parse yes so that that's sort of the last step and maybe we should have done that before we did the commit
like actually I'm GNA undo that was one interesting oh I also asked uh uh chat GPT if there was a better way to do the
uh partitioning and stuff um and as as I suspected there's a way to write your own reducer um and then it can reduce it
down to a result that either has all all success uh songs um or all the failure result um but we can leave that for when
we do more refactoring on that should we put it a note of it so we don't forget or you want um yeah you can add it sort
of after 57 because it'll sort of be part of that so I might because it's kind of part of the refactor of of result got
it and you were saying I was busy doing the commit um I didn't get uh just just reducer yeah t t is another option um
it's one of those where it'd be interesting to to have a few different ways of doing it and and see which one we welcome
yeah so so it's really interesting like chat GPT is you know it's a it's a pattern generator um and you know is it the
best way no idea um but can it offer Alternatives uh based on in a sense based on or almost literally not almost
literally literally based on code that's out there um what other code you know what has other code done so um that's
right it's all statistics all this High futin AI it just comes down to statistics so if they're building their knowledge
mostly on toy projects out of GitHub well even worse they're they're they're doing it out of stuff that is that the Lev
have you seen the level of quality of stuff on on GitHub that's where I really want want to and I keep saying this and
at some point somebody's gonna help me do it um like gener gener generate an LM based on my code bases or code bases
that I've hand handpicked curate so basically instead of curated song themist right you're you're talking about curated
um curated data feeds to an llm yeah yeah that would be actually kind of cool yeah what I don't know is is like is is
like how much data do you actually need in order for it to be uh sort of useful um but I don't know I don't know I mean
I believe some of the plugins will also sort of learn from your code and use the code AS context but I think it's only
the Cur the current project whereas you know it's not like I have a whole lot of code but I have enough yes enough code
to be Jitter or jittery I don't know all right um so we've tested we've got all our tests pointing now towards our our
new parse method which returns a result uh and so now I think we need to go and look at who's calling um or what are we
doing in the import song So now sort of need to propagate the result um we've sort of been doing inside out uh and now
here we're basically ignoring the fact that there might be failures yeah so we need to uh songs and probably want to go
to the yeah um so now we uh now we need to change Behavior yeah so now we oh change behavior of the test or produ oh I
guess we do need to change behavior of import songs because we want it to test right right right so we'll need um
another test that uh where the fails um and we have to decide what we want to that lack of a better name just to start
fine so we could just de sorry uh well before we do anything what what should it do if it fails so right now if it
succeeds it adds it to its internal uh internal database through the return so at this level would we want it to throw
an exception at no I and and so this is this is sort of the the the result who's um so besides the the test who's
calling import songs is that that should be called by the adapter right the song reporter yeah yeah so what we'd want
here um is yeah what we want here is we want we want a result to be returned by line 29 um because if it's a failure we
want to be able put yeah put put me put the messages in the in the model um and then redirect back to the song import
page again so I think um I mean we could throw an exception but that makes it really I mean the whole point is the whole
point is of of what we've been doing is to return a result so we return yeah no I'm it wasn't really it wasn't long to
be convinced I was convinced a while ago but I like that we walk through it all the way up to the adapter yeah I think
that really makes it clear yeah because it shows what what what we actually need at this level yeah exactly um it's
interesting because because commands aren't supposed to return information but it's not actually we're not actually
returning information we we uh we are either returning uh a success or or failure um and I think that's that's okay at
this level my now it's interesting at this level success at this level do we want the result object to just be success
and not added I mean if we want it to be pure then uh you saw where I'm going with it yeah that I mean I went through
yeah in my head I went through the same thought process of do we want to slim down the result um if if it's success and
so if it's success you can't ask for the songs uh to prev the service through the service to sort of prevent looking at
at the actual data that was that was processed I I don't I don't I don't think that's necessary do you think it's not
necessarily because it's just the two of us working on this or I guess the way I would think about is if this was part
of a large decision this is more of a gentle person's agreement we won't it I don't so o over time I've I've I'm being
devil's advocate here yeah no no that's that's really that's really good no um uh o over time I've been been sort of
incorporating new nuances of of the command query SE separation and uh I think it's almost always apply uh almost you
almost always applicable at the Domain object level at the service level I think commands need to return some kind of of
status of did this thing work or not or were there errors in it so at the application layer the rules oh sorry I miss I
Mis phrased my I'm not saying we shouldn't no no so so that's so so building up to right and so now then at the
controller level um it's okay to actually get if you wanted them to get the songs like I don't think that would be a bad
thing here because you're getting the you know at this level level you're getting the results of what's essentially
creation so import is interesting because command query only applies to change of state to existing Creation uh and this
is this is subtle and this took me a while to sort of get through my thick skull of when I say for example you know
something as simp is add a new user to a system you with a method called create user that's not a command it's command
like in the sense that you're changing state of the system but it's not command against a specific object changing the
user's name that's a command against a specific object and that's what we're we want to avoid that method from returning
something right but a creation especially you might need the identifier like hey we just created a user and here's your
ID so that we can show you your profile page um you absolutely need that uh and for a while I was like oh why why is
that the case right so if you think about you know the flow of of a page you basically you know you're you're the admin
you're adding a user uh you type in their their info you hit a button if we didn't return that user's ID there would be
no way to to look at that user's details we'd have to then basically go and find them which makes no sense right uh and
so returning the ID or even return the full user but you may as well just return the ID um then you can basically take
the the admin directly to the page of here's the user you just created and that's okay because it's it's creation right
and not modification of an existing object and so command query separation applies that's why I say it applies at the
the domain object level when you have a domain object you don't want to return anything from a command that modifies it
state but creation or anything that does creation like stuff layer command query separation doesn't doesn't yeah and and
that's really awkward that's you know that's the place where uh you know you can you you could do that right so you
could have at the application layer uh import songs and then query hey how'd that go give me the result um but that that
makes that makes no sense I mean going back to the DB thing yeah would that um that's assuming not a high transaction
rate or high like well you're doing it within the context of a transaction oh within the context okay so it's not like
after never mind I was gonna say what if you get five at once it has to it has to be the context of of what of what you
just executed okay that makes sense yeah so I see creation is sort of um similar to a command but uh but the rules are
are different right because it is it is changing the state of of the system um your ask your your request the intent is
to change state it may or may not it may not be able to create the thing it may not be able to change the state of the
thing uh so it's very command-like but creation is a a special case so with all that said um I think we uh I think
import songs really make sense for it to to return a result so I think what we should do first even before we write this
test is make that slight change um to our test above where we currently are basically get a return um do it manually do
you can't well you can't VAR it up because it's not returning a value smart so you're saying something like this yeah
and then Force the signature yep and yeah we'll return null that's fine we run everything now it should still be yeah
everything should still pass yeah we can consider this a prepare refactoring we're returning a returning a null that
nobody looks at uh and we about so even before we do this one we could check for success in this uh yes and and probably
should check and we should it don't forget to close the run ah can always tell when like the the um the indent is wrong
it's like oh I must not all right so that should still pass yep because that's actually no no null right no it's not
good good I'm glad it failed because I was like oh I don't I don't we change we actually change Behavior I didn't like
that it failed so myad great right so of course we get a null pointer exception yeah now now it's not a Backward
Compatible change oops didn't to do that okay so now so we actually don't even for now this test can be empty and we can
work off this one yeah yeah so we can leave that that test to where it is and just yeah we now have a failing test pass
we so you don't have to select anything if you do an extract variable extract variable at what point like at the parse
like here doesn't matter really yep oh it'll ask me which one right ah sweet excuse me and then we'll call that result
so suiga is is uh the postfix dovar is that the one coming from the internal intellig one or is that one coming from the
custom postfix plugin because I know the custom postfix plugin if lumbo is present in the project uh will uh use the
lumbo version uh if lumbo is not present then it will default back to the the typical VAR I was doing some more postfix
custom yesterday shall We Run The Test uh before we run the test what do we you think is going to happen I think it's G
to pass oh wait a second no parse is returning result yeah yeah yeah that should pass cool all right um how about we uh
clean up the code a little bit in import songs yeah I'm looking at trying to figure out I was thinking it seems
cluttered to me um we need result oh um that just you can just do the four each on the result. songs and get rid of
holding so no no no oh uppercase no you don't want to change the for each you want to attach the for each to result.
songs so basically combine it is there an automated refecting for this I just manually do it like that uh you could
maybe inline it in fact not could you absolutely could inline right there in line varable yep that's what there we go
sweet so suige one thing I know is that if you have modal the modal dialogues on for the refactoring dovar will not work
which is why I reprogram dovar as a custom postfix plugin template um and they won't fix it uh because apparently
they're multi-threading issues uh with the m modal dialogue box and the dovar if you're not using modal dialogues and
it's still not working I can't help you all right um yes I'm on we're we're on team modal dialogues I much prefer it but
yes that's that's the price you pay is far Stop's working which kind of sucks but I I now just either use the custom
postfix one or just the shortcut for for uh introducing a variable because interestingly enough it it it it appears that
intellig built-in dovar doesn't do a postfix like change it actually invokes the refactoring um and uh that's why it
doesn't work because you are invoking something that would cause a modal dialogue to appear and it and they basically
said it's too hard for us yeah so I I added just a couple um uh I'll I'll post my link to it at some stinks how can you
have different projects with different preferences everybody needs to be on the same page but no I get it I I I think
VAR I don't know VAR as a variable declaration I I just don't use it and and people I talk to is like yeah we don't use
it either it's occasionally useful for complex stream temporary variables and that's about it but I'm an explicit type
kind of guy all right um now test failure mode right so that works uh so let's do a commit before we yeah yeah I I I
don't like VAR I see it in code and then I'm like I have no idea what type this is and it's really frustrating
especially since I'm I'm often looking at at code like that on GitHub and then you you you don't have I don't know how
people do it when they're doing when they're processing pull requests on on GitHub and it's like I don't know what this
is all right um so what are we doing here well we want something that's like an assert failure whatever the exact name
is right that's our y our goal I am so so tempted to write uh and maybe we should add it to the J is uh write a result
because it's really annoying me that we're constantly writing result is success is true and result is failure is true
which will which gives us really not great failure messages um plus it's just annoying to have to basically type two
extra things what I'd like is an assert that result is Success um we might do that sooner rather than later this part I
feel like we can just copy um well we want tweak it right well why we grabb the failure stuff from from our previous
test yeah that was in the tsv song parser class yeah absolutely the the let's right tests like let's right more and
better tests um is definitely a higher yeah oh 100% agree suiga I actually have a a a pull request um that I have to
submit for dispatcher type that Mike and I ran into uh I think last week maybe the week before um where it was not
documented what which one it was importing and there were two possibilities and we first uh let's grab one with two
lines we can get two failure messages point oh my God asra every time I hear this but how do you code if you don't like
how do you test if you don't know what it should do yet people think it's okay to code without knowing what it should do
and it and it boggles my mind like you actually do know what but in a sense they don't and and and I've seen this
especially when I've done training where it's almost you figure it out as you go along like you write some codes like oh
we're gonna need to to put an if statement here and then you get into that it's like oh we're need to need to Loop here
and then you get into that it's like oh we're gonna have to need another if statement here and so basically you're
figuring out as you go along and that's why people who code first test after will often say how how do you know what
you're going to do because I don't care what I end up doing I care what it does and it's a very very different it's it's
it's the hardest mind shift for people uh and the only way you can get them to shift is for them to experience it it's
yeah it's it's like but it's but it's true but it's true that when you code first and test after you actually don't know
what it's going to do and that's why it's it's it's just you know they're they're as they're as baffled as about test
first as as as I now am of of of code first that's a great term Perpetual Perpetual spiking yeah yeah how nice yeah and
then you then then you write it and it's done and it's like okay now I got to figure out how to test it to see that it
did what now I know what I want it to do um and so they so they were using the coding process to figure it out which
makes sense right when often you know when we're writing articles or text or or documentations like or not documentation
maybe but like when we're writing right we're clarifying our thoughts um as we're writing it and that's a forcing
function for in order to be able to put into words on paper or on screen it can't be this fuzzy stuff that's in our head
and and and it's a great way to think about things really to get concrete about it um and people code the same way most
most people code that way uh unfortunately then when you get to testable yeah that's a different problem 70% whatever
doesn't matter like any com any any non-t amount of comment that code yeah what are you doing um all right there is no
there is no is failure method right yeah yeah so I changed it um yeah looks good to me so and then we'll get that to
pass and then we'll do the second assert was what I was thinking um well there oh for the yep so we expect this to f
fail because it's oh no it should pass right because right I don't know that I feel the need to to test the messages at
this level oh because we've already tested it at the at the closer in level here so this is this is really interesting
because I've had people toss uh toss out codee that appears to test nothing like what is this testing um but it is test
so so even though it's it may or may not rise to the level of of more complex tests this is telling us though that we've
wired stuff to correctly together that we understand how things are you know how how code is calling other code um and
so see sometimes people throw a test where it's like oh it looks like it's just you know not really doing anything but
this actually is doing something that's I think just about deserving of a test but that's it once we know that that is
success is is false we know that we're we're actually getting false we don't need and the actual error messages we know
we going to be there and we don't need to test directly um and yeah so I guess is there a scenario I guess it that I'm
GNA Devil's Advocate again yeah so is there a scenario where the result message at the point in which the result object
or we're writing to the result object failure messages if somehow somewhere between there and here it gets corrupted or
deleted in some way by having a checking the the failure messages were putting in guard rails against that fuar um it's
kind of a major mess up right to somehow in between when we're setting it I don't even know where we're setting it have
to go through the hierarchy right and then pars and then here so if somewhere in that chain someone decided to well
actually can they even delete failure well you first of all you can't modify an existing result because it's it's
immutable it's immutable yeah so okay so um so there's that and the only place you could change what gets returned well
you could do it uh so let's go back to song service for a second so you could change it here um we also could do do
something like uh make the failure and success static methods pack package access you couldn't even create a new one
here at this level that would be probably useful we should probably go go look at that um so let's say we changed it so
let's say um I mean let's actually let's 35 right instead of returning result result right so actually there's a Factory
method isn't there yeah let's return uh so we're going to expect failure so let's return you know success uh yeah so
this was Luigi's suggestion let's let's try to break it yeah but don't we want it to be oh the test yeah so if we did
this that'll break the test well no because it's expecting our well actually let's let's let's see what happens if we do
that yeah let's hardcode failure um and I think it requires some some parameters otherwise it's not going to compile
right yeah yeah so it fails as as we would have expected it to right um and if we success and we can just pass in null
we oh it's not going to know which null so we can uh uh it take so it either takes a song or a list of song and if you
pass a null it doesn't know which one to call ah so you'll have to cast it to song so it nulling I want oh of course it
won't let us what am I saying um let's uh let's let's do um let's just do song dot did we have a static method on then
oh we can't access it because we're in production code right um so let's create a variable song and assign it null and
then we'll just pass that in sorry I couldn't resist the joke even though it's brief well that would be actually not all
useful doing uh so now we just want to do null oh the whole point was to avoid okay yeah right and so now this broke a
bunch of other tests right so um if we didn't have the test uh above right if we said oh the whole test isn't necessary
then we could accidentally not accidentally we could we could change it on the other hand why would we do that and would
we be we'd be changing behavior and we wouldn't have a failing test and so I just I I think it's a useful test I I don't
think we need we need any more of it because we changed the failure messages then the test directly against the parser
would fail right so so message changing is covered by the parer direct by closer in tests yeah and then the farther out
test just test to see are we returning the expected results is it being passed along right that it didn't get either
process yeah so I'm convinced we don't need a fail test at the well we don't need to check for the failure messages is
what we don't need to do still need to check that that's failed yeah right okay so let's go back let undo whoa I must
have done a cut or something uh so you've got the a test in the wrong out so so just clicking the gutter yeah okay now
everything should yep and we were looking at this test s importer you can go away so what's interesting here note that
we're not in our import songs method at the bottom we're actually not checking for success and failure everything is
working because if it failed songs is empty and so import songs to a certain extent doesn't not right because if it
failed songs is going to be empty the four each will basically Loop over nothing and then and that's nice because we
means we don't have to have a decision statement yeah good um I might say what we're actually result yep so I'd actually
like to go into result for a bit uh and change the um and and and check the the access for methods yeah so let's change
all those static methods uh let's just remove public yeah so let's just remove public so you can do all J if you want oh
yeah yeah of course yeah yeah um you want to capture the one above where you are was there a static above there was uh
so hit Escape otherwise you're going hell so what I tend to do here to make sure I've captured the right ones is I
select public static then do the multic cursor and then reduce the selection to public ah so saying this yeah that way
if I happen to start on the third one I can wrap around and capture all of them it okay now go home key yeah and then
delete yeah you could have selected the word but same thing yeah I wasn't sure about that the way multicar yeah every so
multicar everything happens exactly the same control W Works moving the arrow selecting works you could even do control
W here um everything works it's just now operating on on four different points in the program right sweet don't forget
to escape out so let's compiled okay and now if we um just go back to the song service and if we try to for example uh
return a result success we shouldn't be able to access that from here uh uppercase R because want to see if the static
methods should no longer be available huh well just because it shows it to you doesn't mean it's available ah uh I would
choose failure because because that's going to be easier to whole so it compiled uh so that that in you need you need to
scroll up because I can't see the package oh result is in the application um I guess that makes sense because it's about
the pars well so wait so who is who's can we go look at um failure and see who's calling that I'm wondering if that's in
the right package sure song parser okay so what package is in hey application okay so our parer is in application yeah
all right let's not worry about that too much okay it was it was a good experiment but it's still good to have uh not
default everything to public is is is the basic guideline yeah um let's fix this yeah fix this I could have just done
revert but oh well and let's go back to result because I also want to check the um the Constructor I wasn't sure if
those fact yeah so those should be private because we shouldn't be access we're not right yeah so those are inside so
that should be private and that should be private no so the word was already selected so you could you could have start
typing I know still getting used to it yep run I did run oops run twice all right let's commit so I prefer to use the
term visibility here because accessibility is an overloaded term right um and it really is about uh the rest of it was
fine not visibility visibility uh because you're missing an it good you um did you want to take a break now yeah might
as well okay just a quick all right so we'll we'll take a we'll take a break and when we come back um now that we've
propagated result uh now we can start using it uh and we'll test drive uh the controller to uh do the right thing so bit
all right and we're back woohoo so um being the kind of person that I am I went and looked at the Java um language
specification because it's like what do they do they call it visibility or accessibility they actually do call it
accessibility um there is a visibil visibility used in another context um so technically accessibility is the correct
word but yeah I still find visibility I I like visibility better right well accessibility like you said is overloaded
term yeah you think about you know software being accessible or exactly building being accessible right yeah actually in
C++ they call it accessibility and that's the language I know that right the the best um so that's where I was coming
from interesting I do like too all rightl result next or actually you said something right before as I was um I think
just that we propagate result all the way to our control it so here um this is uh where we'll I think we have a test
against this yeah maybe even two one so that's the happy scenario um we handle null specifically there in the next test
and so now we're going to need to write a new test so we're we're in the change Behavior portion of our tdd cycle so we'
ll write a failing test let get it to fail in the right way and then it I'm just mimicking your previous um naming not
that I like it handles failure I don't know I don't really like that yeah I'm I'm not crazy about the word handle yeah I
don't like this astd import adds adds failure messages oh the name of the method is handle song import yeah ah so sorry
what was it you were saying again uh so song import ads failure messages um to import so it's going to be pretty simil
to um the one where you got the test highlighted the one that handles null because we won't we're not actually importing
so we don't care about the repository uh all we care about is what uh what gets what what we're actually import so the
whole thing or just the E so there there are there are two there um uh one is the redirect should redirect back to song
import so actually it is the same as 40 and that um so we can start there by uh and then let's let's sketch out the next
it um Sorry by sketch out I meant make comment and we can just use English to say model see we're writing we're writing
a list of things to test um so now we want to pull in uh instead of null we actually want to pull in some bad song data
so we can grab our bad song data from the previous test this is a well the previous test previous test temporarily
tempor temporally what was the last test that yeah so previous is in what we worked on TimeWise not spacewise right
right right getting all Tardy on us here um I'd like to rename that variable yeah uh and maybe we should rename it in
the other test as well um because it's basically not too songs songs yeah and this is the kind of cleanup that would get
uh that would get me into trouble it's like what why are you making changes here this you're not modifying code what why
you why you making changes outside the scope of the code you're working on because we noticed it and we want to keep our
code exactly have more of those but that's expectation it should still work because we're not songs if it fails we won't
know as the color of handle import handle song import because it's not throwing an exception no ah yeah no it'll P it'll
fail because it'll go here right yeah yeah so it'll fail because we're going to redirect to root instead of redirecting
back to song import back to song import yeah yeah yeah which is good because we want to we that's our change in Behavior
yeah let's run it watch it fail make sure it fails in the right way which it pass I hate to write an if statement um H I
guess it be the yall like well so what I what what I would do uh is a avoid that so what what do we want to return if it
is successful if it is successful we want to return this oh sorry this yes so basically wrap wrap that in the it no and
then make this the um the default if does now what do we think we can refactor that and simplify it yeah I'm not liking
um so what I wonder is what happens if does our import songs handle null words yeah what if we commented that out what
would out ahuh so we don't handle null um I don't know if we want to uh but I was just curious if we handled it or not I
think honestly I think we could um yeah let's let's let's leave it there's some other things we could do but I that path
as far as moving the null check elsewhere is that what you yeah I think we'll we'll just have to leave it um so the
question is is can we refactor the welcome I guess if we did reverse this no I don't think we were I'm not concerned
about refactoring that part I'm concerned about refactoring the the success if else right ref factoring the code we just
wrote got it are you talking about inlining result or is it something else you're thinking no I'm thinking is there
anything I don't have anything specific in mind I was wondering if there's that nothing thing's jumping out me I mean we
could turn it into a turnery cleaner so let's try we'll see how that looks you're saying a turnery here no no no no no
if you uh put the the carrot on if and then Alt Enter one so I generally also am not crazy about Turner um somehow
though it looks cleaner to me and I'm and I'm not sure why other than it's many fewer lines I'm not a fan of Turner well
turnery can be valuable but the but does look cleaner what is my why do I have a a gut reaction against it in this
situation so I generally format my Turner um not as one line so I I find that it looks almost like an if else it's just
more compact um so done that before like this uh so I put that yeah and then what break here or the colon uh so sorry I
put I put the question mark at the front and then the yeah wow I've never seen that before yeah so what I like about
that is is it puts the oh what's which which one are we doing and then oh we're doing the it well I I'm with you AST my
initial reaction was I don't like it but I don't I wonder if it's because it's unfamiliar not because it's actually yeah
not better yeah yeah and so endofunctor zero Hey there um there's there's a there's a little bit of a functional taste
to this and that's why I I do it this way um because it really is a mapping we're values so I like that you called it a
taste of sorry you gonna say something I was just gonna say that that it's it's not really functional because we're not
calling any right well I'm I want to channel Kent Beck like I don't like this therefore I want to try it some more so
all right um to let's leave it and let it let stew and then we can it well we're going with the yeah stew is a good one
marinate both continuing with the food theme that's right the torture you good okay um let's re run the test even
refactoring suggest what would be the worst possible way to do this the worst possible way is is uh maybe a switch state
actually a switch statement might be interesting actually switch might not be so bad we can Will intelligent this to I
don't think it'll offer um so let's uh but if we went to if yes let's let's convert it back to an if and see if it'll
offer a switch I don't I don't think it will you have to be on the if if statement itself all right no I think we'd have
to make an an else yeah so let's go to the block if so to braces uh and then do uh an else block one we need an L if
around the other one no because it literally is the else condition because it's only no I meant for the no that part I
knew I meant for the for the having if we're trying to make it ugly oh I see what you're saying um yeah then you would
say result not result uh result success not or not result success whatever yeah yeah so now would it suggest a switch no
what is it suggesting so now it's highlighted in Orange what does it suggest if you Alt Enter on the variable oh no it's
now it's just an inspection um well let's write the let's write the switch manually okay I'm really curious what this
what the switch looks like since we have switch okay return switch Success um have we Is Res is that correct syntax
return switch I don't think I've seen that yeah so that's the switch expression uh syntax that's within the past few
years um so now if you if you uh Alt Enter on the red it may offer to fill no oh selector type Boolean is not supported
yeah we'd have to do we'd have to do uh an enum or something all right okay we're getting we we were trying to make it
make it worse and and it's just not not possible um so you can undo your way there if you'd like if if there's a way to
do a for loop on this then then sure you could Loop through both possible values of Boolean I don't know that now now it
feels like it's we've gone past the point of absurdity yeah okay so I'm just going to run the test because that was a
little bit chunky bubbled uh well now we redirect appropriately based on failure um but we're still not done test so T
asks know the shortcut to open dialogue to create a new class or interface but had to navigate it inside it without
using the arrow keys without using the arrow keys why would you want to navigate without using the arrow keys the whole
point of dialogues and such initiated with a shortcut is you want to navigate with the arrow keys so tell me more h okay
okay so now we want to do this part yes so how do I hit the model in the past that part has been too far in the past in
my brain well uh we can't because there is no model so we now have to modify the method to accept a model well there are
two ways to do it um there's always multiple ways to do it with spring uh we can pass in a model and then inspect it uh
in our assertion or we can change the return type of string to uh another class called a uh a redirecting view um I
maybe I'm old school I I don't know uh I don't I don't know what what if any is the preferred or or quote modern way to
do it um but I tend to uh like injecting the model so it's called redirect and view which is of course what uh uh I
think that's what it's called maybe it's just redirect view this yeah this one so the redirect view is is a class that
uh I think can contain model stuff in it it's I'm not even sure if it has the model in it let's go with the way that
that I actually prefer and and know about sounds um so so uh in our test we'll need to create a a model instance that be
in the setup um I I sort of consider it part of the the execute okay um I just group it there uh so so we say model and
then um then a variable oh it's model and view not redirect view that was the class I was thinking of ah because there
was one called redirect view as well yeah no then I realize that that's not the right the one that had the and in it and
I just got the first part of the name wrong um and then we're going to do new concurrent it uh and then we'll pass that
in as the parameter yeah just add the yeah yeah um so this is a a uh no Behavior change so this everything should still
just work aha ah so other places um where we're doing it we need to also uh and so so this is sort of the downside of um
adding a in this way uh so let's let's actually undo the refactor and I think we can do it again yeah I think no is that
what you were saying yeah so refactor yeah add add add it and now here uh we need to specify default so click in there
got it um and the default value should be new concurrent model really yeah because the places that are not I know you
could do this from here oh yeah signature cool now refractor now refractor and I just noticed that the dialogue itself
uses the word visibility for public private and package even though technically it's accessibility so I'm not the only
one who feels that way um so now this this should should correctly excellent sweet um now we can start asserting welcome
uh so what do we want in our model is the question we want the failure messages I forget are those an array or uh those
would be those are a list of strength um so what we can do is uh jump to our HTML n that narrow it down it will yeah
okay y oh asid I missed the celebrate from as I said streamyard does not forward redemptions so I end up having to have
um so what we probably want is uh above the form like like n and a half what we'd want here is um I don't know we can
start with uh yeah and then as part of the P we can do it uh inside the P we can do a th colon um want do we want an
each I think we each so uh yeah th colon each and then in quotes So equals and then in quotes oh okay um we want uh we
can just call it colon and then a space and then uh a pair is that a curly brace it is okay um and this is where we want
failure messages so lowercase f and then uppercase M and that will be the name of the attribute that we add to the model
got it uh and then what we want is we actually want to display the the the message so we can do a um after the the colon
um text and then equals and then in double brace uh message like that yep so the for Loop basically is for the each is
basically message give me right it's basically your typical for Loop you know for message from failure messages and so
then the local variables message uh let's um and this is the th is time leaf for folks exactly all right uh let's let's
add um a little bit of style just so we know these are eror messages after the after the double it uh and we can just
say uh color colon red answer um and that should be fine yeah uh inside the the inside the the pair of P's let's just
put in just say failure message so we can preview intellig yeah good enough okay so that will show up if there are any
failure messages and now we know what we're looking for and so now we can go back to our test and assert that model um
uh no we can do it outside side I um um oh because it doesn't see it as a now um for now it just contains attribute and
the attribute that that clipboard true uh we can delete our comments since we now know what we're doing um we can close
the HTML at the bottom and go back code um want the song think so it should fail because we haven't populated the model
with failure messages out failed yep as expected as expected yep um so let's make it now doesn't our friend the if
statement was useful now yeah yeah so we might want to uh convert it back to an if statement an if else block which
intelligence should help us with Y although it did it horribly that is really ugly really there's not a like introduced
oh think uh you can yeah over okay so now if failure we want to right now interesting well I guess we'll cross that
bridge and we get to it this test is also a failure but we have not populated failure messages yet yeah so but we're
focused on this path yeah I honestly don't think we can ever really get null um because I think no matter what the only
way you could get null is if calls this method the a post directly oh body so in that case because if if if it's ever
submitted by a web form there must be an entry for that field great and so it so null the null protection is really
against somebody hitting it directly all yeah Al it's really interesting when you when when you make the shift
especially to tdd um you end up almost never manually testing like we haven't manually tested this thing I don't think
we did it yesterday we probably we might do it today um but it becomes the sort of just double-checking yeah looks okay
um like we'll do it because we want to see the failure messages because we don't have tests directly for the HTML but
other than that you end up spending most of your time in the code writing your expectations and then making them and
then fulfilling them and it's a it's a very different way of thinking um but it's powerful and and just so much faster
overall it's faster and less stressful I'm definitely less stressful yeah so uh what we want to do is add attribute and
then you give it the name of the attribute and then our failure messages and you so it's just name value then do we pass
it as a as a list of strings yep so like that okay okay so it can handle that yep okay so now while we were passing
right well no we were failing now want to pass now want to doing and it's testing if it contains the attribute okay
right right right yeah so this is actually a bigger step than we need so let's make it a smaller step so instead of
saying result failure string when you say empty string you yeah and shift it 10 that should pass nope because semicolon
so a shortcut I recommend you learning sooner rather than later uh is the auto finish my statement for me yeah don't
tell me I think I have it in my lists thought I me no I don't have it I thought I did okay what is it um it is control
shift enter so delete the semicolon at the end of the line on line 35 I will I'm just typing it in my note okay and now
sh enter but hold on um move your carrot to inside the pen anywhere is fine okay y control shift enter that I'm typing
so basically would so in fact delete the last two characters on that line yeah speak okay I'm back all right so you were
saying so delete the semicolon and the closing pen and then move the carrot somewhere else in the line control shift
enter again so here it couldn't necessarily figure out that you needed a closing pen um but often it will do the right
thing but I mean at least it moved me to the place where yeah you needed to finish yeah so I almost I I I almost never
type a semicolon wow uh because that's one of the most common keystrokes I do yeah so it's not just add semicolon it's
close pns close close other stuff um and needed I couldn't figure that one out well it won't close it won't close blocks
it's only going to close the the current statement got it right it does say code complete current statement yeah has its
name okay so now that we've got that it should pass because it's just about exists cool now we jack up the assert yep
the same assert or have a new one uh so now we can transform this assert instead of contains attribute we can actually
get the attribute contents but do it to the same assert yeah because now we're sort of now we're as you said we're we're
we're ratcheting up gotcha assert so this will return what we hope to be a list right so so we can just start by two uh
oh it doesn't know what it is um it's type object so uh we can either cast it or pull it out into variable I gener like
to pull this out into a variable to make it clear what its type is that's what I was going to suest because it just
knows it as an object because it's an untyped basically an untyped map and then we'll string and and you'll need to cast
it you'll enter y sweet and it's complaining it's it's an unchecked cast and we don't two we think it's yeah two Mal
yeah that y well actually there was two songs Oh cannot be cast right because we did just enough to make the previous
test pass we've ratcheted up our expectations so we should have expected this to fail in that because we didn't change
this yeah yeah yeah so that failed for the right reason we just didn't predict poly and failure messages is coming is
that right no no that's not result there we go right and we were saying there would be two right is it so this is
they're both M for actually is it has one or has two uh why would it be one no I guess it's yeah neither one of them are
nine never mind right right yeah yeah that's why it's two malform songs and not one okay song and one malform song
that'd be a long variable name yes it would be okay so possibly useful all right so that pass um and now what we can do
uh is do a characterization test on the message I don't so again why oh at this level at this level we don't we we know
the messages are correct what we're just saying is that whatever the messages are we know they're correct here we're
just testing were they put into the model are um now we can do is we can actually run the application and see what the
like so this is where if we really really wanted to we could write uh uh an HTML test that would test exactly what we're
going to inspect manually but I feel like inspecting it manually is a more fun and B uh easier to and once it works we
know we know then it works right and new ey uh be oh I got to do my the one thing I didn't too so this is the kind knows
guess I should have done that off screen oh um I mean we could paste that but let's grab something from your spreadsheet
where you have the wrong yeah fail interesting well it could have been the stuff so let's look at so it looks like um we
got an error page uh we did yeah so if you look at the stack Trace we it looked like it redirected to an error page or
it looked at it it had attempted um it mapped the song import uh not sure why I tried to dispatch the the error and I'm
not why the error page is not showing up can we go and check the web security config because I thought we fixed that
sure so that means I've log into kind no no no uh the web gotcha I'm not sure what exactly what we or there it is yeah
um now that's interesting we did do dispatcher type matchers for forward and for error to permit not is it expecting a
page called slash error kind of looks like yeah so yeah so you see there it does a a get error um 403 on trying to
resolve what what looks page do we have an error page an error page is automatically uh generated but and handled by
Spring boot unless you tell it otherwise ah okay I don't remember us creating that let's where your C where your carrot
is right now let's actually add a a comma slash a comma double quote slash error um I restart um just so we know where
we are if you uh click into there yeah um clear is there a clear there is and I'm just yeah I'm wondering if if that's
and maybe if if it that yeah so clear it because maybe that that's not the the problem um and maybe I was reading the ER
the the stack Trace wrong or the the logging stuff wrong all right so let's UT uh can we look at the um uh the song
importer so let's stop the this one yeah so the problem here is um because we're doing a redirect the model lost uh and
and every almost every time I do this I forget that this is the case ah so we are adding attributes to the model um the
model though only lives for one request response so the response the model exists we redirect and it redirects and does
a get request and at that point the model information is lost so it redirected properly it's just uh we don't want to
add it to a regular model we actually want to add it to a special kind of model called the redirect attributes so in
instead uh so we'll need to write uh modify our test so I had misinterpreted our run time it was had nothing to do with
the the slash error um got it should we UND that yeah we can undo that just gonna do it actually I'll do way okay close
it um yeah we can close it I was going to suggest some something that's off oh off off yeah tangential thank you uh so
let's go to our uh importer test um we want uh instead of a concurrent model what we want is a map yeah same is this a
we run it and find out uh or do you think well let's run the tests they should still pass um but we'll need to change
the tests the type on line 57 on the left hand side song imported test is failing oh let's do you want to do that no we
shouldn't need to do that uh I wonder see um so redirect attributes uh acts in a different because uh it has to it it
basically gets added to the um what's it called the basically as a as a query string um I think that's not actually what
we want to use here if it was a if it was a simple one you know a simple scalar value then this would be fine but
because it's it's a list I think we actually want to use um what are called flash attributes so that would mean is this
add attribute is no longer attribute it's add something like Clash attribute uh so we need to use um me it so weird
about a time um oh we can still use the redirect attributes we're just doing uh the ad flash attribute instead of uh add
regular be oh but it thinks it's model it needs to be right so let's let's not change code without um right updating our
our our test I think our test is actually still okay uh but we need to change the type of uh the the model that's being
passed in okay so let's um let's let's do this through refact ing sure I just made a mess there we go um so let's uh
let's do this through a Method Song importer so the handle song import we want to change it signature because we want to
change model to to be uh redirect uh attributes oh here yeah got it but you need to change item no no I forget the chain
signature control F6 it's not an obvious keystroke uh and so we want to change attributes yeah uh let's rename the that'
s fine no it's fine uh let's rename the parameter this one yep yep the first choice to redirect we now need to update uh
all all the places that's not using we're not passing in redirect attributes model map we're now well we're pass the
problem is we're passing in uh too high level of an interface in from our test and that's it so what are you what are
you doing next I'm trying to figure out where to go next actually so up on the top line 58 we can see that that's not
right we need to type no we need to change the line 57 declared so that that type is not correct it needs to match what
we're passing into the Constructor so we need to change the Declaration type not the instance so here yes and is this
still a Model A map yes that is an implementation of a redirect attributes redirect attributes is an interface just like
model is an interface got it okay yeah but we don't you want to still call this model though here same redirect
attributes mhm um and there are probably two other places in the code that are uh broken because we used to use new
concurrent model we want to replace those with new redirect uh attributes model map um so I would yeah so we can go to
each I must be getting tired because I'm now forgetting what the name of that class was oh was down here this guy no it'
s not that it's the same instantiated thing we did in the other test if you just start typing it'll one of the
autocomplete options will be what you need yeah I just want to go to this and see well that's the failing it that one
yes and you hit if you hit F2 it'll jump error think we got them all all right right uh so let's let's run the tests I
still suspect that um actually I don't know what this will do let's let's run a test and see what happens I'm currently
running all I'm me free time all right so what we want to do is um to change uh our our code to be uh redirect
attributes add flash attribute 35 like that yeah does that mean this one becomes a well um let's see I'm not sure let's
run it and find let's run the test and find out well there is a get flash attribute there is but I'm not not sure uh I'm
not sure what get attribute actually does because it's still part of interface okay so we do need to to look at the The
Flash attributes so in this uh yeah so we're going to have to do get that so get flash attributes doesn't take any
parameters because it Returns ah so what I would do is I would delete that line of code oh entirely okay yeah and
instead of failure messages uh get map from the redirect attributes so redirect attributes. getet flash attributes ah
and that's it really so we expect that that uh let's see this so the size of the map is actually one uh so what we can
do from there is we can do a that right because um yeah I was thinking we could check the size of the map but I think we
want to be a little bit more precise so let's extract that variable so you don't have to select if you're doing extract
very oh right yeah um and so we do the same thing so this will be our failure messages and we'll cast this to a list of
string so you can change the type first and have cast yep now we're sort of back to where we were but using flash
attributes but now now we're looking at the flash attributes yeah run the test and predict or predict and run the test
that's the correct order pass all right you like my order correction on the Fly there yes uh so now let's run the
application uh and works right nice wait a second that's a useful error message what are we okay that's a useful error M
there's something wrong we got to fix that we got to make it more obscur yeah we just have to say uh fix your input
something like that yeah invalid input invalid perfect yes it's less words we're saving pixels yeah that's right the
world will we're we're saying bites being transferred yeah um so the one thing that this doesn't do uh and we can we can
fix that next time um is it doesn't preserve the input uh it's it's basically what we need to do is take the input and
put it back into the flash attributes map and then it would would come back um and that's sort of even better it's like
now it's like your input's gone but you got the error messages but you may not be able to know exactly what you typed so
uh so we can we can fix that for next time but let's um I just wanted to get that reminder next time yeah um we actually
didn't really make a j ticket the project managers I can hear them all screaming right now we didn't make what we're
doing just now I thought we did did we do it not lower me no oh I thought we did oh it's okay all right beside being the
product um you know owner I'm also the PM so right it's okay well we get to create an item and check it off so let's
yeah it's a jira after right create ticket after that's the order I prefer yeah exactly um so let's actually we haven't
well let's see we failure message uh yeah display failure messages in UI that's a better way than I would have phrased
it so thank you now we should commit yeah I think we said he is the customer yeah owner customer yeah user everybody I
have so many hats oh maybe I should next time I should come on with like five or six hats St commit commit and push
because yeah push well right so next time we'll put the the original bulk import screen back in the Box we'll look into
splitting the result into two concrete classes oh I think you really wanted to move up the customer SE for result yeah
so that's a bunch of sort of inner stuff um do we want to think about what major so we now have like a working UI right
so when it works it adds it we we know that and when we've entered something wrong we actually get useful error messages
instead of an exception um so from a a highle feature point point of view what what what might we do next well there's
either this this skipping over unused columns the header that's the one you want um and then there's processing to a
database I'm inclined to go with skipping heteros first then um is it just skipping ah header Ro or is it matching skip
over UNS needs a head a row yes um I think that's a a good next feature yeah to me it feels better to do that before I
think so I think so um yeah so we'll do that next and then probably persist a database is is then the next big technical
I mean it's certainly a yeah a a feature that our customer wants they don't want to repport every time every um every
time the server reboots uh so yes um that's not just a technical thing it's actually useful all right yeah I think
that's a plan yeah so um That's all folks thanks for for joining and and participating and celebrating our our little
wins uh not sure when we'll pair stream again maybe the weekend we'll see um otherwise as always thank you so much for
hanging out with us yeah um as uh I'll push the the the Discord and the weekly book club um so again never too late to
join hit me up on the Discord and I'll get you hooked up we're looking uh we're going to be discussing chap the rest of
chapter two and then chapter three of the programmer's brain um really interesting book uh and jenders really
interesting conversation so so join us for that otherwise we'll see you next time uh have a great rest of your everyone
