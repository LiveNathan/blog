# ＂Song Themes＂ Episode 24： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=MGJAPFapi5Y

---

## Transcript

all right hello folks welcome to another pairing stream apologies for the delay uh streamyard has bad UI you tell it to
if you accidentally click on the end stream it won't say are you sure you want to end the stream unlike any other tool
where the action is destructive and completely ends the stream and causes you to have to completely recreate a new
stream from scratch because you can't copy anything so uh if they don't improve that soon I will uh I will not be
renewing so that's that's my uh frustration for this morning hope you're reason oh that's weird yeah I fixed it there we
go um doing well doing well you know you're on a Jitter Ted stream and we got a rant yeah so but out of the gate usually
it's a more happy rant as opposed to a very frustrated at a tool that really should know better true true yeah good
wreck but we're here and helloe welcome Hey um yesterday we had started off sort of thinking about uh using a library
versus writing our own and I'm I'm glad we went the the route of of writing our own because there were some really
interesting uh refactorings and and um it may not have been the most efficient way to to get the feature done uh but I
think there were some really good examples of tdd breaking things down to small pieces taking small steps um and then
backing up when when when things don't go exactly as we want um and I and I talk about this a lot on on various social
media and I get a lot of let's say uh feedback on on tdd and and the process of doing it and things like that uh and
it's you know speaking of sort of frustration and rant I'm like look I've got 700 hours of me doing this either alone or
as a pair and clearly it it works because we end up with almost no bugs if you think that it doesn't work well I have
700 hours that proves that it does and if you think there's an alternative because you have a better way of doing it
then great you go and show that on video and show us because I'm really tired of folks saying well that doesn't work we
do it this other way that's much better and then they never actually explain other than at some handwavy level here's
what we do and and it's frustrating because like maybe they do have a better way maybe their way works probably in some
like most things tdd doesn't work everywhere and so maybe their their method and process works really well for them well
then tell us what it is uh and show us what it what it is because it's it's really frustrating that there's potentially
a different way to do things that might be just as good but I can't learn it because you're not giving me the enough
information and so uh basically it's uh long story short tldr put up a shut up right put up a video that walks through a
realistic example of you doing your process where you end up with just as much um maintainability and quality as I do or
stop posting about it so that's my real rant as opposed to the frustration here here huzzah yeah and you know because I
I recognize that like you know tdd is is hard for all the reasons that you know even you and I struggle with it um
because it's not tdd per se it's it's breaking things down and figuring out what you want and how you're going to test
it and how you um but it works and so um if there's a better way I I want to know about it but nobody's ever shown it so
so there you go um so let's uh let's see where we're at I think we had updated jira at the end of our last episode to
leave us uh some good restart points so let's take look at at where we're at we had added U well we rewrote J 67 added J
70 67 we're talking about supporting the remaining columns release Tye right type and the other three themes and then we
also came across or observed the um uh column index of right right and where is that in here here oh it's at the caller
level was in the parse individual song right hey there Mino welcome from India there it is so this right duplication
indicates primitive Obsession yes or certainly even if even if you're not one isn't familiar with primitive Obsession or
or the the different code smells I don't know I feel like sometimes I overfit uh everything into primitive Obsession
because but it's you know sort of part of this really feels like there should be a class here uh that has this behavior
um and mainly for for if nothing else for uh testability like we know column index of header with artist works because
we substituted zero which was a hard code column with some computation uh which is a general way of of increasing
generality in code right we replace a constant with with some kind of computation or decision-making and so um we knew
that worked but it's that testing at a distance problem which is well are we sure it's going to work when we swap
columns around well in order to do that we had to right if we were only interested in testing column index of in a sense
which we were uh we had to write a fair bit more test code because we had to yeah like exactly that we had to have the
header and and the thing and then write this and create that and do that and then finally look to see if if it was is
successful or not um I think later on we actually compare against uh one of the other tests We compare actually against
what it parsed and make sure that it parsed it correctly even though it was out of order um and that's really awkward uh
and so sort of another another rant is is people say oh unit tests are are are are too hard they're they're they're too
brittle and they're you know I'm just going to write more integration tests like you can certainly do that but you will
not be able to your tests will be more complicated they'll be more set up there'll be a little bit more difficult ways
to get access to what you want to check and valid validate um yeah and and then it's harder sorry what did you say and
they'd also be fragile actually at that level no I don't think so in fact the claim is is that they would hide some of
the implementation details oh I see yeah yeah so that is actually not wrong at this level right not necessarily end to
end that's going to be more brittle but at this level you could certainly say although I wouldn't call this an
integration test I'd call this a sociable test but whatever you want to call it um the fact that there are multiple
objects involved or multiple pieces uh one could say that if I was wanted to test column index of uh I would have to
test it indirectly H but that's fine because then I don't care that there actually is a column index of and to a certain
extent that's correct but once we are relying on column index of I might feel uncomfortable of for example what does it
do when it doesn't find it Well we actually saw what happened is it returns negative one um and then when we try to
access negative one of an array that doesn't work and so the failure modes become harder to figure out like how do we do
and te because one of the things that we as software Engineers probably don't do enough of is testing failure modes I
know I don't I'm guilty of that as as anyone because it's hard because it's like oh and I got to write stuff that's not
sort of the happy scenario and getting things done and providing value directly um and so it's much harder to do the
failure modes at a distance because you have to add in all this other stuff just so you can put this column index of
little piece of functionality in a certain State and then you have to check it in a very awkward Way by catching an
exception versus if we could directly test column index of we would write a method well column index of here's the
header that doesn't have the thing and look for the thing we should get negative one or maybe we want something better I
don't know um so whenever somebody says oh you know I just want to use inte you know integrate quote integration tests
without defining what they mean by that that's my other certainly ranty this morning um like if you're going to use
these terms then you got to give us examples like to say test suck and integration tests are much better because they're
less brittle I'm saying good show me an example so apparently today so all that being said um whether it's primitive
Obsession or not my solution to the question of how always can we push this private method to be a public method on some
smaller object right and so whether you come at that through primitive Obsession or something else that's sort of the
the real question is how do I test this exactly so what do you think going back to jir should we do we want to tackle
the Primitive Obsession first then support the other columns or the other way around I don't know I don't have a strong
I mean I kind of I think I got the sense at the end of last stream which was actually only yesterday um it seemed like
folks were kind of interested in seeing how we solved that so I think we'll get I mean I think we'll get to both um but
I think if we solve the Primitive Obsession earlier it will make implementing the other columns easier because one of
the things we're going to have to do is is say okay we're now looking for release title what do we there um and in fact
column index of may not actually be the right level of abstraction because what do we do with the information that it
returns is we basically then use that as an index in the columns but that might be too low level right we might want
something more along of give us the data we need yeah pretty much you all hide the implementation from it yeah please um
right and so whether we push in the entire just the tsv song Raw string um or whether we or we push in the columns
arrray um either way it would be nice to have a method that says give me the data for this column name and then we have
a good default right so in a way it it it does feel like primitive Obsession because here we are in the parong method
and we're saying hey um can you let me know what Index right has this right right and so it's like hey other thing tell
me what index is because I'm going to use it later to find out literally the name of the artist right right and so that'
s there's a fair level of or lack of it abstraction yeah and a bit too much IND Direction yeah and and and and a lot of
detail like yes I honestly don't care about the index I just care about the data right um so let's let's let's uh let's
solve the Primitive Obsession column oh kill me now okay um so so since this is a refactoring uh we should make sure
that all our tests pass they do and I will run him again I ran him during the running of the intro theme so um run that
fast it's crazy what you mean the test ran too fast they did I was like did they fast well not really but yeah it made
me go did I they actually run pretty fast yeah it's all compiled we haven't changed any code so there wasn't any
recompilation necessary yeah that's usually the slowest part that that and setting up the jvm is is to run the test is
the slowest part everything else is super fast yeah so um I think what we want to do first is sort raise the level of
abstraction of of the meth of the column index of method right because what we really want like you said is is we just
want the data like uh given this header um Here's the the the column name the the the name of the column we want uh for
the data uh and then just give us the either the data or or an empty string um um I'm I'm thinking of two different
directions okay one is we could refactor that constant of the empty strings there on line 71 into into something that
that calls the new method but I think that might be behavior um but I could sort of but I have this this so sort of
figuring out you know the small steps along a path One One path is we end up with a method that say say uh you know data
for for column or something like that whatever we call the method and we give it the header the name and the columns and
for this column which would be release type I believe it is or release title release title title um it would give us an
empty string but that would be Behavior we'd have to be writing not testing it yeah we're not we haven't tested that
yeah and so in this case though because of the incoming test that test this this method we expect the the the empty
string there um but if we go down that path I along the way we're writing code somewhere that says uh you know if the
index is negative one then return an empty string and that's new Behavior right so uh so going down that path is is
actually implementing some new Behavior whereas going down the path of let's raise the level of abstraction better and
we would push it into a new class yeah so we'd push it into a new method and then we'd figure out what the what the
class is and then and then move that over makes sense hey there Tom fan van welcome uh so let's do that so let's um
start with extracting the variable on that yeah yeah I assume that's what you were looking at looking for yeah and then
you can inline the artist column so that actually I'm G to practice my control W well if you're extracting variable you
don't have to select at all right yep we'll leave that one now this one's going to be interesting I guess we would do it
at this point yeah right now we're just we're not handling new themes we're not handling multiple themes we're yeah I
don't know what to do on this one yeah this one you can tell this one I think because it's at the end I think take it's
all automated so everything should still pass yeah and then inline yeah right and so so what we've done is we've
basically created not quite a new abstraction but preparing for a new abstraction because we now have on the left side
the variable that we want with the content we want so we have artist song title theme one um and then we can extract the
rest of that line into into another method and you don't have to select here either if you want to extract a method
whoops that's interesting I never that scroll to Center control M what does that do it takes your current line and
Scrolls at the center want I can y now what do we want to call this puppy um so we probably want to call it the general
name even though it's going to use it extracted artist we'll introduce a parameter on that so yeah so what do is extract
extract column let's start with that does it extract a column extract a cell in a column extract well we're only working
on one row so there's no I let's let's go with extract column and I know it's not great but it's it's it's good enough
uh and then let's introduce parameter on artist and again you don't have to select because so most of the refactorings
you don't have to pre-select but it does give you the expression to say which one do you want exactly I was gonna say
extract column value swegi that was the next thing out of my mouth but we decided to punt the value is so generic yeah
that's what like I yeah uh you want to do introduce parameter not variable so P not V not V yeah yeah this will be the
column header maybe column name column name sounds actually okay yeah actually I think yeah let's do I like that now
this is what I was hoping intellig would do it's like oh look you generif this method would you like me to replace all
these occurrences and absolutely we do you can just click all I like I like I have the joine you go One By One The Joy
it's like it's like yeah it's woohoooo yeah woohoo exactly so this is this is uh the standard process that I follow for
doing these kinds of refactors you extract the method introduce parameter to generalize it and then rely on intellig to
find what are now basically duplicates um and then once that happens we can then look to see how we can take that method
uh and and see where where we can move it so let's run our test this was all automated so shouldn't have uh changed
anything but our test run so fast why not oh good and just a a meta note when when your tests and sometimes when you're
doing when you work on Legacy code you may not be able to run all your tests right so maybe you're doing tdd but you're
doing it sort of in this bubble of stuff where you're able to tdd um but you can't run all the tests because some of
those tests are slow but inside your bubble if you can get a sort of a bubble set of tests around what you're working on
to run fast you're going to run the test more frequently because you don't not going to have to wait it's not going to
take away your context and blow it up and then takes you 15 minutes to get back into it which is what happens when a
tests take five minutes to run um and it's this sort of reinforcing cycle where if you can run the test more frequently
you're going to run the test more frequently which means if you're taking smaller steps you can run them more frequently
even if you know if everything works because uh they run so fast yeah but then like you were saying yesterday it's like
feedback loops that means if do make a mistake which we will you'll find out much sooner which means you won't go down a
road where you're you're now in mistake having been made mode uh and having to figure out then it's 10 minutes later it'
s like oops what did I do in the last 15 minutes that that caused it as opposed to in the last minute and you can affect
that take by taking advantage of run configurations yes and so this is this is where you you slice up your applic um and
when you're working on Legacy code you're going to slice it up into here's my sort of tdd tests that run really fast
because they're all running in memory uh with no IO and then here's the larger set of tests which I want I do want to
run maybe I do that only before I do a commit um or maybe I run those sort of on on a larger cycle um and then there
might be a set of tests that uh take much longer um that maybe I don't even run I just push it and let the continuous
integration exactly um so stupendous follow ask does spring have some kind of continuous testing like corcus uh it does
not um I I've heard about corus's continuous testing I I actually don't know what that looks like uh I have to re add it
to my list to to take a look at um but I I I I suspect it's not going to fit well with the way I do things because I
like to segment my test but that's just a guess based on very little information so I need to go verif verify that but
Spring by itself does not have anything uh like that um intellig uh does they added something recently which I keep
forgetting to to use in Earnest um somewhere there's there's uh uh continuous testing um but I don't I don't know what
it's called um it's clearly not called continuous testing uh so I'll have to I'll have to test check that out um and I
know there is a a plugin uh infinit test which will basically every time you you make a change will rerun all your tests
I like I don't know I guess that would be nice um if it if it did it automatically uh the problems I've had in the past
with something like that is it runs it too fast uh oh so apparently it's it's a rerun automatically okay um is like I I
I I'm a bit of a control freak so I want a little bit more Precision about when those tests get get run um but again
it's it's something that you know uh I need to just just play with uh um and to to your other questions depend is follow
uh when making a new repository is a good idea should make one for every entity no um you want one for every aggregate
you want one for the things that you're going to store and retrieve uh and it's unlikely uh unless you have a trivial
domain it's unlikely that you're going basis but that's one of those it depends um but I recommend if you're not
familiar with with Aggregates from domain driven design uh that that uh that you look into that um and there's I think
in the dis in our Discord uh in our domain driven Design references back to it oh yeah so so I so this is one of those
things that um like anything else right you know new features new language features new IDE features anything or even
just new techniques um it's good to try them out and see what they feel like uh before making arbitrary decisions about
whether you like it or not so that's that's on my list is automatically and uh look more into testing all right um our
test pass uh that's the other thing about fast running tests is like if you do lose your context for for a bit because
you get on a tangent um it's very easy to just say can you just run the test again and let's make sure we're we're okay
CU I don't remember what happened last time and okay they passed and because it takes so little time um so now that
we've extracted that now I think we have a pretty good abstraction for uh for what we want um parameters well if we it
depends what we class yeah so let's let's say if we if our abstraction whatever we EXT whatever we extract the two
header would be in the Constructor likely um and so it might be a column mapper uh and then so headers in the um would
we even pass columns because we could put put that in the so would the columns go as a parameter or as part of the
Constructor it feels like we're gonna call the same header thing with multiple different so in this scope there's just
one set of columns um paring only one song yeah but I think at the I think at the higher level the pars all when it
extracts the header would create the mapper and what we get here instead of mapper you're talking about this point um
and we haven't done that yet because we haven't finished the the other handling the other columns but basically the idea
is that header would be the first line from that list uh but then we'd create a a column mapper from it right and pass
that into par song I think that works fine um so the question is is do we return an I I I think I can't that feels like
I'm trying to predict without enough information yeah it does uh like I can see in my head what it might look like but
um let's let's I think we should just take it one step at a time so I think the next step is to extract uh uh a column
mapper okay before we do that can we move parong underneath parcel oh yeah absolutely because to me it's don't even need
to ask yeah because it feels like it should be right after all yeah totally because all the other stuff is sort of mini
support details yeah okay so now um actually I'd like to move extract column and those guys up too yeah yeah I'm going
to do that more manual way okay so you were saying next up is to so we want to um let's see how can we do this through
refactoring uh we would we make a header class out of the string first since it's a PR uh could we create a parameter
object out of that um that's an interesting way to go or at least try um let because I I normally the situation I'm in
where I'm solving primitive obsession is there's a field called header and then it makes it easy because then you can
basically take that field and and wrap it up in a delegate and then move stuff over um I haven't done it this way where
it's not a field so I don't know if this will work but let's try it um so I think if yeah but you could also do that
right at parse all oh we don't have the header yet I mean we certainly could convert header to a field and then follow
the typical steps but I'm curious if this is is going to work so let's do before we do anything else since this is going
to be a little bit of a Spike let's do a commit Jonas good no worries Jonas and you missed uh the problems I had this
morning with streamyard so no worries which is yeah yeah um yeah that's something that so so uh I've played with wabby a
bit um I don't know it's speed I'm I'm used to things running really fast and so uh James Shaw has his his test Runner
which um sort of runs consist constantly and has sounds um which I really like I think that software I feel like
software has regressed a bit and and doesn't use sound enough like it can be annoying but I think there's certain sounds
that that basically add you know what you see and is and what you can read uh but but sound can provide sort of a
non-intrusive information as long as it is non intrusive um it's what I like about uh James sh Runner and then I
actually wrote a little extension for junit is uh it plays sort of a happy sound if the test pass or a sad sound uh if
the test fail um because really I don't need to see the output uh except when tests are failing and that's when it's
useful but enough yeah I have to I have to um put my sound thing into into open source list uh so let's um let's try to
extract parameter object string that one I did not have yeah I don't think I use that so rarely um not even a and
there's no shortcut for it yeah so um I think we want to call it what it is and so I'm think column mapper um even
though that's not a great name it's it's not a header class because it's not about the header not just about the header
it's about using the header to extract specific columns by name um let's see name we'll leave it an application for now
um so the parameters we want to extract is really just yeah just header um not yeah not the columns not the column name
because those are going to be those are going to change depending on the parong so so let's try this see okay all right
all right um and so what did it do made a record uh that's interesting yeah um oh it did new H interesting good uh so
now um where do we exract one to a local variable and then use a local instead of no I think I think the signature for
extract column uh so what we need to do is inline of because we want to basically move this chunk and and intellig won't
move multiple methods that were that are dependent right so we we sort of have to to wrap it up in in I always think of
of you know packaging it up into a nice box and then you can unpack the Box on the other side so inline and remove all
yeah and it that's the only usage so that should be fine so now um so in this kind of refactoring process when we're
trying to move right now what we've got is feature Envy um when we have feature Envy uh because we're basically and we
can tell we have feature Envy because in line 52 we're basically asking column mapper give me your head header and that'
s bad give me your header so I can do some stuff with it um but really uh we don't want to do that um but because it's a
parameter now we can do or we can F6 um and so it's asking what is going to become the this uh and it's column mapper um
so there's really only one uh and so now we have an extract me extract column method um that does the right thing how do
we know do you like this your design yeah I that's I do too but I want to check uh so let's go back to tsv song parser
there um so now we now what we have is new column mapper header extract column and so that's close to that's very close
to what we want um but let's run the test to make worked oh I thought I did it let me try F F10 F12 yeah they're all the
same they're all the same all right so test pass and so now what we want to do is we want to push out um uh as a
parameter the new column mapper header because what we want par song to accept is not header and then recreate new
column mapper every single time uh we'd like to create that once but we would it shouldn't be the responsibility of this
method to do that parameter and yes replace all three occurrences and here we'll see some magic uh maybe was I too early
um no that's fine uh mapper and interestingly enough it didn't get rid oh because we're analyzing on Line 39 if the
header is empty that's why I was expecting it to to drop the first parameter ah um but we have to I so again it's it's
like I'm always seeing like you know the the the different possibilities so one is we could say this is fine and we'll
get rid of header later is have col Colum mapper take that responsibility it's kind of a dead respons it's it's an
obsolete responsibility and that's oh right we're getting rid of it once we get Once once we do all the mappings um then
then uh so I was thinking like oh maybe we move some idea of is empty into column mapper um which would make sense if we
wanted to keep that behavior around but I think because it is so temporary uh that we'll just leave it as um yeah uh and
so then what we can do up online 28 is now extract new column mapper to a variable because we only once containing block
um oh it's doing the whole thing you did extract variable and it didn't let you select that let me do it yeah when I did
it without selecting oh it's asking you for the Target code block uh we want the containing Block it's basically saying
where do you want the variable scope defined so that's why it's Target as opposed to sort of the extract portion um and
that's fine yeah um yeah and we only do this once because we just we only need to do it once the creating of the mapper
yeah IGI that's probably our our our uh an upcoming step is to default the header once we get the full mapping um I mean
I guess we could even do that next but I wanted to sort of get it out yeah uh so let's run our test that work clearly
F12 is um uh I think we're we're done with the mapper um still a record yeah that's fine right no point in I mean we
could create a class and then it's just gonna why is it showing gray uh because it's date um I don't I don't trust the I
don't trust intellig grayness because usually means there's some indexing glitch uh what we do want to do though is put
Constructor which means we want header columns to become a field actually we want the list to become a field so let's
change the the the name of list to be uh header column list I hate that suffix but we got to thing let's let's go with
that for now columns plural well header columns is the array oh that's why I saying we need something different right
right we could swap it uh let's swap it because that the the the header the list is going to become our field so let's
let's call this um I know parsed header columns or just header column array I don't know well this then we don't have
array we doing the yeah pseudo hungar uh and then let's rename that the header agreed uh and then we need to create a
field for header columns because we'd like to access that as the field is that control F yes and I'm not sure what it's
going to do uh I think it doesn't make sense for it to be a record anymore um yeah yeah basically you can't have an
instance field so let's undo that let's convert it to a class and then let's do option uh because this will make it more
clear now that we want to do that um so what you want is uh yes that um and then we want to do that 16 and 17 we won't
actually do that in the Constructor there's not going to be a paste but header okay yeah that'll work okay yeah you'll
have to do some finagling um what I would say is inline uh the header worked uh no it worked but it's it's it's this
weird uh it's this weird thing so go ahead redo it redo what you did oh okay because you asked did that work and I said
yes but it's weird right because we now on line 13 we're accessing header through the accessor as opposed to just
directly accessing it ah um we don't need the header once we process the header we don't need it anymore so we actually
don't want to save it so let's inline uh the call to header yeah uh and remove the field remove the method um that's
fine we'll we'll just go ahead do it again yeah redo it okay uh I yeah uh drop the this in front of field I don't think
you're going to be able to do that because you're using it in line 12 but let's see want try it let's try it it's
probably gonna complain but maybe it'll yeah four us okay so the other approach is get rid of that that then do this
yeah and so the reason why it's still used it's used in the equals in hash code uh this is not an entity class really so
we don't need equals and hash code right now so we can just get rid of that two string as well yeah get rid of two
string because it doesn't it won't have header that okay there we go uh let's run our test make sure we haven't broken
anything because we did a good um we can make uh just to make intell happy and me happy we can make the final um and we
could optimize this class we could instead of having a list we could create a map basically a reversed indexed map but
uh I think we that's an optimization we can leave for later um all right so let's go so our goal has been achieved right
we've we've basically extracted the behavior and now we could write um some tests around what what happens uh if um it's
not found and I think we should do that because we're going to need to because the rest of the columns they're optional
we need to be able to support that um we generate a test class from here against mapper or were you thinking something
else um no call mapper test is okay do matter okay y move this up above oh results up here we need that no no we don't
so um I think we're going to need some tests around uh uh I mean we could backfill some tests but I think we don't need
to we can focus on sort of new Behavior so I think what we want is um if we have an a column that's empty basically if
we ask doesn't exist yeah if we ask for a column that doesn't string like it's an okay first name but I feel like I
should refine that name I think it's it's it's fine it's it's a um I had this discussion I think on my stream the other
day uh there are sort of two forms you know putting us side punctuation underscores and other possibilities um there's
either sort of a uh a given when then like way of structuring this right um which is you know the Contex the the
situation first and then the outcome right so column that doesn't exist is a situation the context uh returns empty
string as the outcome um there's the other form which I think I am finding more useful which is outcome first so empty
string exist and the reason why I I am leaning more that way these days is just I'm finding that when I'm looking for
Behavior to change I'm looking for the actual Behavior which is why did I get an empty string I'm not often thinking of
oh yeah and that's the that's of the structure um that's the outcome outcome context and so I'm trying to be more aware
of is when I'm looking for tests what am I looking for right because when you're modifying Behavior you're often saying
well what does it do now and I'm trying trying to be more aware because I'm trying to think about what I'm looking for
because I want to optimize for the looking uh not for the the creation right so like here if I want to scan these test
names right it's like you know find me the test where we get a failure when there's not a header row right it's hard
yeah it's like how do you find it whereas if you make it the first part right if you say row you still you know at least
now you're looking I mean you could group up your failure ones and that into nested classes and that might help look for
failure ones um but you know if it's if it's missing a header column that's required where's the test for that so anyway
just food for thought uh like it and because it's always it's been one of my test organization and test naming has been
something that I don't feel like I have figured out so I'm in agreement on that all right um should we write the failing
test and then take a break yeah definitely could use a break um why don't we write the failing test after break sure we
can do that biology is speaking to me yeah all right so uh we'll we'll take a a quick break and when we come back we'll
we'll write some tests for this shortly e reminder if you like talking about the stuff or have questions um deeper
questions about some of the stuff that comes up or even if it's not related to the uh the stuff we're working on if it's
related to Java or design or test driven development or hexagonal or other separation of concerns testable architectures
uh or intell um join the Discord it's free lots of different channels channels on hexagonal architecture uh not
surprisingly uh also channels on domain driven design and intellig and test driven development and testing in general uh
and we have a book club which uh is always open even if you're coming in the middle of the book um I still recommend you
know depending on the book it's still possible for you to join and the book we're currently reading is called the
programmer's brain and we're just getting into chapter 4 so still a good time to join uh so go ahead and join the
Discord if you're not already a member and if you want to join the book club just send me a direct message uh just click
on find me find me uh find Jitter Ted and click on that and send me a direct message say hey I want to join the book
club and uh I'll I'll get you in there and you can get uh access to the transcripts and and recordings of previous
sessions so what we do is every Sunday at 10: a.m. Pacific which is now uh 5:00 pm UTC uh after the time change uh we
get on a zoom for two hours and and chat about the book and it's been really good uh really interesting um the topic of
cognitive load and learning and so on is is near and dear to my heart uh so um some really good discussions so join the
Discord for the it and the cognitive learning stuff is infectious so now I'm interested in it because it's been talked
about in the book club y all right so let's write that failing to have a new one of these it takes a want what are the
methods in colum M again extract this only one method that's name M what is like oh something like that okay wait a
second no it's an array right uh that is an array yes so it's already parsed correct for purposes of this matter because
it's gonna pretty much well let's put in some some data so let we so you can um just create the array directly so if we
do new new string yep uh and then outside of the the brackets so this is the the What's called the array literal form
and now strings so we want some real columns or these we real right this is actually real data so we would need
something along the lines of not don't care but along the lines of something like this right actually we could just
steal all this couldn't we well I don't know about the list of parts no we can just drop the list of yeah because it'll
be just all those as an array so something like that yep and then we want to assert actually extract columns has a VAR I
think we just can say column column that's what I was leing towards fast is empty right uh you don't want column oh I
typed column but then it autocom completed my bad so let's yeah do we have everything we need oh the column mapper
argument is the header right so the header is tab separated so test uh without the backs slash end though let me copy it
then I'll delete it okay oh um I just realized we don't need the the new string I think uh because it's been I I so
rarely assign direct stuff to arrays I think the new string here is redundant in some cases you need it I think but I
think here we don't so we could just do this open yep so I think we've got everything now should F by the way for the
for the folks who are watching I did a search because uh and we talk a lot about you know when you're coding even if
you're a quote expert or been doing it for a long time there's stuff that you're not gonna that if you don't use very
often you will forget and so I forgot I knew the curly braces were there but I wasn't sure if we needed the the new
string and apparently we don't so I referenced the Java language spec and said oh we don't need that so wasn't that I do
that offand I I I had to look for it and I've been doing Java since Java existed so don't feel bad if you have to search
when you're coding all right so what's our expectation this should fail actually yeah it should fail because right now
we're not mapping so it should throw an exception with an index of minus right sweet so actually I want to see where did
it throw that from 915 here no cuz the index of their return negative one right so that means we have to extract this to
make it pass into a VAR and do test yes a local I mean when I say VAR I mean a local variable is there any other kind of
R well you know the type of R which I don't like to use oh oh oh yeah I would never you yeah um you'll want a double
equal yeah I out practicing my control shift enter I noticed Okay so is that good or not so we think that so uhhuh so do
now we can think about refactoring yeah we do want to ignore it's not an error it's just we're ignoring a column we are
we are saying that this is the behavior that we want we're saying if yeah if the column doesn't exist um we just we're
just gonna we're just going to return an empty string string yeah okay I just need to get my head back through that and
then refactoring I mean I was thinking turning this into a named method so it's clear what it means yes although there
is an alternative I think um which would be ask the header columns if it contains the column name ah right and then run
it and if should didn't interesting it broke multiple things so we're working on this one let's go uh so let's take
another look at what we just wrote so this isy common we flipped our Boolean so let's let's do it the uh so yes we could
put a bang in front of that but how about we uh we flip the the the if contents so return no no oh that kind of flipped
yeah so so swap out the return empty string with the return columns index invertive condition you don't want to invert
the if condition because right now the if condition is well you could fix it and then invert it so put a bang condition
no yes is that right oh I see it yeah I didn't the change was so fast I didn't even so it move this into the if and move
that out inside the curries and we could take the uh line 15 and move it inside if block because we don't need the index
if we haven't found it oh right yeah and then delete that ex space and pass yep sweet so it shows to go you that even a
very simple thing you booleans they're rough you you get them wrong but immediately we ran the test and it's like oh it
must have been something we just did Y and so we didn't have far to look um would you inline this index I like I don't
know let's let's try it and see what it looks like yeah part of me leaving it the way it is frankly yeah columns heter
columns index of yeah I preference I don't I didn't have a preference so so this is fine it's kind of a coin toss to me
yeah all right um one thing that I'm a bit concerned about is our test setup above um The header artist so uh I kind of
feel like ah we got bad um so let's so let's change the data meaning get rid of notes yeah get rid of notes um and
themes and the contributor and I'm I'm wondering do we want a test that uh throws an exception or something if the
number of columns that we pass into extract header so if there's less header that's definitely a problem right if there'
s more columns then we would just assign empty to the well that's still a problem right because if if we're thinking
that validated means you copied it from the spreadsheet it must be rectangular right so if the columns are empty you'll
get just an empty tab but there'll still be a column there right we're assuming they'll do this and there's no other way
to do an angular selection I mean you could but that would be really yeah you could you could select individual cells I
think you have to press like on the Mac you can do it you can select just arbitrary cells oh you can whoa but you're not
going to do that and that's not what we want so yeah yeah yeah um and so the only thing where and we've already tested
where like if the the final columns are empty we still just get empty empty tabs so I think we probably want a test that
says um something about that that the uh what the heck what did you press I have no idea so I was so busy looking at
that weird one drive popup that so we wanted to do something like uh uh header columns header columns must match data
columns saying and so is it header columns count much uh match yes that would be more correct head columns must match
how was the second word um data I don't have a better term for it data columns song columns data columns I like song
columns better I mean nothing in the code below says anything about songs true value or data because I don't know any
any what else to call it if you want to use value I'm fine with that but I like data slightly better all right um and so
I think what we need to say is what is our outcome our outcome I think in this something meaning we're expecting an
exception I think right now an exception is this a positive test or a negative test this should be a a negative test so
basically exception thrown when header columns don't match data columns header think because this column count uh does
not match data column count yeah or you could just say does not match data this is probably more clearer yeah I think
leave it uh and your H in the win is uppercase isn't it supposed to be that way yes thanks for catching that all change
so I forget the Syntax for checking for an assert for a uh so we can say assert that um so back up on the PRS uh assert
that I think in this one it would be just an illegal argument so assert that illegal yeah that one the y and then enter
and then Dot is thrown by and then the code up on there on 29 no no we want the column app extract column the method
call is going to throw it so do open close so delete column we want an open close paren Arrow ah okay uh and then grab
the the method call from is yep I was what I was thinking of doing was putting column there and then inlining it into
then you should have done that well I was way better I was just a try let me do it again see if it works see if my
thought was was good so if I did this here column doesn't like it so then we do in line so doesn't like it but then I'd
have to do this yeah yeah either both work it's a little faster okay cool um so let's see should we're not checking it
so it should uh it should fail because we're not throwing an exception um oh it should fail because it's not gonna throw
yeah so we expect an exception but we don't get one y yeah whoops no no no before cool so you can say trr and let it
auto sweet do we pass anything on the argument for this one um well our test doesn't require it so no yeah so no we may
want to do that but right now our test doesn't require it right as I say we don't want to uh add functionality yeah I'm
just thinking the uh the um metaphor of of uh leaning too far skis because then you fall into a tumble yeah all right so
that passed um yes let's let's have it give us a nice message now can we say y with message absolutely and do we want to
stick with using illegal argument exception or do we want to make a custom I think I'm okay with with illegal argument
okay because the message will be should be clear will be clear yeah you always start them with uppercase or do you low
do lower case for messages like this um I treat it as a sentence so okay you do a period because it's a sentence uh no I
I don't think I usually do a period okay um but I think we want uh more information oh I might I might stick in header
column count of uh three does not match does not match uh does not match data columns uh data column count of one two of
three all right yeah I'm not grocking it but I'm not sure why um what do you not okay data column 3 is release type oh
count of three for okay never mind I'm good okay all right so this should fail because we're not getting a message yep
and I foolishly ran just that one I Kaboodle yep yeah then we got to parameterize it yep right would we wait to write a
second test to do that no I don't think I'd okay no the length is not a methol ah because it's on it's it's because it's
old okay and what's the Syntax for uh is it uh I think it's not this is it no that's for format for for exceptions uh
actually I'm not sure I I forget what exceptions do by default in C I know they do this um I don't know if the parameter
position matters or if you can just do open close curly up I wonder if there's a uh Quick Fix remove uh there may not be
such a Constructor call we may yeah we may have to do the format ourselves that's why I was Wonder it's like I don't for
logs I that exists but not for exceptions out oh you're pulling it out okay oh what were you thinking I was just going
to say dot format in line ah so right after the the close of the string put do format and then the last two things
become parameters to the do format or oh interesting yep because it's a string it has a method called for right right
learn something new and percent s is correct uh yeah percent s is for string um we could do percent but I don't I think
it'll just do a two string on it so it's totally fine is it in the Java world is it better to do it be uh I think it
would be a percent d that would be for decimal I just do percent s because I don't because we're not doing any kind of
it um and if we had string templates this would be even easier those string templates at upcoming yeah and it's and it
looks like it might change quite a bit uh between its preview and and the next the next release uh I think it is
currently though available if we wanted at as a preview feature so so this is the current preview um but yes they are
going to change there is talk uh on the mailing list um about changing it about moving away from making the processor be
this Str Str uh and just having it be an a regular API call um so Brian so there's quite a quite a detailed discussion
on on that curious U but that's what we do you do uh yeah uh so what do we think we think yes so now should we do a
little mini mutation test should we remove another yeah and so let's take out title actually what I would do is uh what
do you um I think it is irrelevant what the column names are so what I'd actually prefer is they be unnamed and just
have four like that no literally the word literally the numer one or the numeral one but I might use the the it might be
too hard to see if it's just individual digits right so you mean yeah and then what add one more for yeah you want T
though oh you're so picky I'm not picky the compiler's picky the compiler's picky but not me okay so now um we would
change this to four and uh well no what I would do is leave it at three have it fail and have it fail um because it's it
should now say in fact I might even add a column to the to the columns data so that we can expected okay I'm G run it
again so five should be M does yeah I think the string template stuff is nice you know once folks get over the syntax
which eventually they will because they won't have a choice because the syntax is not changing um it's it's actually
quite nice yeah that that is kind of the point of the compiler its job is to be picky exactly absolutely run again now
it should P pass because we increase the column count to six and yep uh so the syntax that people complain about is is
the backslash why don't you use dollar sign because dollar sign's already in use and if we use dollar sign then that
would break a stuff uh and in fact so this is the link to uh Brian get's email on the uh potential changes for string
templates let's um and uh one of the things he says is is uh basically before he goes on to what what the changes are he
says uh um I'll bigger um what has not changed is our view on the syntax of embedding Expressions so basically he's he's
trying to Forstall like more complaints about it it's like oh look you're changing stuff so please change the the Syntax
for embedding expressions like nope nope dollar dollar sign syntax is out backslash is what we you okay but uh I
recommend if you if if you care about um and I say this a whole bunch um if you care about Java uh keep up with the
jeets and if you really care uh subscribe to the mailing list uh so there's a bunch of mailing lists where these
discussions happen clearly and um uh it's really interesting so um This Thread is is quite uh has gotten quite
interesting discussions on it all right um so are we back to passing we are um uh so I think for line 28 also as well we
should sort of use sort of non-meaningful data and here maybe we can use the clear yeah reason why I didn't like it with
the with the tabs is it's hard to read because it's all strung together but here since there comma separated I read and
the reason you're doing this is because the error message you'll be able to see that this six matches this six yes that
four matches that four right makes sense so actually this would be setup right it was like this implying that was the
action but it's um huh what are you thinking I'm so yeah I don't I don't know this is um the data is really an important
part of of the assertion like I I'd almost inline it if it didn't make the uh if it didn't sort of hide the the data a
bit but I I think the this setting of The Columns is actually part of of what we're validating um it could certainly go
different different way but I feel like having it having it separate calls it out a bit more now would you do it this
way because it's part of the I might but then somehow that's harder to read so you know readability uh trumps trumps
yeah yeah and so the other option is we um uh into its own thing but I don't know I think that might even be harder to
read could try it you want me to try it yeah so extract the do an extract variable on that without selecting without
selecting this part yep uh so we want the inclusion of the yeah yeah so the so the defin the the type is going to be
awkward because it's it's a it's a throwing cable so we could do use VAR but I don't it we tried all right um do we want
to uh do any refactoring passing oh that's true we might not even be able to use VAR uh cuz it would probably what would
it assign it to yeah we wouldn't know and it certainly would not be a throw callable yeah even if it could inverse infer
some type it would be the wrong one so what refactoring do we want to do um the only thing that's jumping out as me is
we could turn this into expl explaining method but I think it's pretty clear without that um so what I generally do is
is when there's an exception being thrown as part of a a check that's a guard Clause re and I yes think was that too
vague that's okay that's great maybe it require matching column count yeah yeah I forgot I really like require um guard
Clauses which you can do with exceptions yeah if it was a return then we wouldn't be able to do it um right but it but
if it's going to throw except like if we that's the thing we had with like result returning result is we can't easily do
the guard Clause um although result would have other benefits uh but this is this is what we got and so this is the way
I would do it makes sense all right um so we've we're handling both mismatch of column counts so failure failure State
uh we are um returning a good def uh I don't know about good default but a default that we want if the column is not
found um mapper I mean if we passed in a a null header would throw an exception but do we need to test that I don't
generally test I don't write tests for nulls I assume I assume no nulls or nulls are being checked elsewhere that at
this level a null shouldn't have gotten this far that's kind of what I was thinking because it's like if you got the
code wouldn't work right it wouldn't even I mean it would still throw an exceptions so like yeah you would get a null
pointer exception and and since jdk 14 you'll actually get information about what caused the the null pointer exception
and it'll you'll get an an NP that says header was null and here's the sack Trace go figure it out so I don't I don't
feel like we need okay um what do you think yep hey there Muhammad um what do you mean by end tier architecture because
it's already an end tier architecture um but often the definition of end tier is confused with layered um so tell me
more what what you're what about so tiers versus layers is something that is often conflated uh but it is layers are
code organization tiers are deployment organization and the two are not the same so we currently have two tiers because
we don't have a database um but the two tiers are uh often called client server um since this is a web app the client is
your browser and this is the server so it's already end here where n is two uh if you're asking are we going to add a
database yes we will add a database um but if you're asking something else uh then then I'm curious what what what right
let's um jir uh yes we get to check something off I'm always in favor of dopamine yes well the great thing about tdd is
we got lots of dopamines along the way this is true just a steady drip of of of success true should we move to jira 67
so I rarely use overwrite mode it's a hard habit to get back into yeah I I I don't I I I just don't bother because I'm
always worried about being in the wrong spaces okay you could get you could get fancy and and select the first one and
then do Alt J Alt J and then just press space but I don't feel like that's any faster so um talking about modes again
talk about once again actually top of hour should we uh make another quick break uh I think we're Sho are we are we
still shooting for noon yes we're shooting for a noon ending so yeah let's let's take a a quick Break um and we come
back we'll we'll work on jir 67 right e so just uh another reminder um in case you didn't know one of the things that
that I do besides streaming is uh I do uh coaching and training and so kinds of things I help individuals uh and teams
with is the stuff that you see us doing on stream the see that you see me doing uh solo on my Stream So doing test
driven development even in Legacy codebases it is possible um doing refactoring uh so you can get to a more testable
codebase uh that's possible as well and so um I use two techniques uh one is uh somewhat traditional uh instructor-led
training where uh and it's usually remote um although I can do in person but these days most people are remote uh and
that's sort of a more traditional uh with me showing things assigning Labs doing the labs on your own uh and then that's
mixed with uh learning ensembles where um four to four to six people in a group um or at least I separate you into four
to six people and we do exercises together in what's called a mob programming or Ensemble style um and that is very
effective uh it's a great way to learn and um we can either uh work on code bases that that I have designed for learning
things or work and or work on on your code bases so uh you can contact me you can find out uh my contact information
ted. about um or you can uh so for inperson uh us is probably the uh the only reasonable cost because I'm based in in
California in the US uh but for remote training um uh I can adjust my hours to fit at least partially in the the
European time zone so time zones are are the main issue uh but tend to do no more than three hours of uh sort of
learning a day because I think anything more than that especially in a remote environment is is overwhelming so uh feel
free to to get in touch and we can discuss that all right and we're back 67 what do you think go with the easier ones
first um or dive into the challenging one well I think um I kind of feel like I want to do the hard ones first and get
those out of the way there is value in that so yeah because it's like my um although it's so it's interesting it's like
uh my general that's my general process when doing software development is what's the next what's the next thing that is
we're we know the least about or scares us um and do that one next uh on the other hand we also here on stream have time
limits and so do we think we can do that in this amount of time I think we can so let's let's go for it okay and just to
tag on to your riff about that and the advantage about that from a at a more project level is you get your your known
unknowns right known sooner so you have a better sense of when of how long it'll take and how far you have to go yeah
versus waiting to the end that's when you're really bled yeah okay so let's see where are we so I think we have some
disabled we it's even I think there's a disabled empty test that too failure and that one is is the one we want so I
think that one actually uh that's the one where where we tried to to make it work by using the header that was passed in
um and that didn't wonder let's try it again I don't remember if if we're if we've succeeded or not so this will fail
because header all right so pars song pays attention to the header parse all ignores the header so now you go into
parall and actually don't assign an empty string but assign the first element in the list in our in our parsol so
actually we before we even can get to well I guess we could work on this or we could make it so that it's working all
the way up to pars hle right because right now I think that I think I think that's a that maybe is is our prerequisite
yeah um and and we'll probably get stuff along the way uh yeah I'm not sure I'm not sure where the code is now versus
the last time we tried this right yeah so let's let's try it so I'm sorry can you hit escape to to thanks so right now
it's just yeah using a blank so we could promote that to parameter no we don't need to we want to grab stream list get
first oh right right because that is our header and now let's let's look at one of the uh orange Amber failing ones so
what's the diff um let's the next one yeah par song with only one theme yeah so let's click to see difference oh because
we're not dealing with release type and so maybe we have to do the simpler one first well let's let's take a look at uh
oh right okay so I think what I think test can we use this failing test to drive our Behavior because I know what the
behavior we need is at least for for this one because it's still only one theme so if we implemented yeah so let's run
this test in isolation we expect this to fail because we're not paying attention to uh release title and release type
and now we can go we can go fix that yeah this is Advanced uh uh an advanced thing because we've got multiple tests
failing but we are actually treating this test as a change in Behavior test as opposed to oh we broke something U
because we want this Behavior to song and now we can replace the empty quotes with uh the column MPP or extract would
you extract this to a local yeah yep because that way we yeah so now if we run the test it should fail a little bit less
yes yes there should only be one one one yeah and that's true and that's great because it tells us we're on the right
track y it's so funny that that um it's interesting that you didn't copy and paste the the row above which is what folks
would typically do and then sort of modify it uh you basically typed it from scratch but those who are looking closely
noted that you didn't type that many characters because most of the work was done by the autocomplete right and so I
think it's actually a bit safer to do it from scratch uh and in fact in intelligent uh idea 20241 uh they now have the
full line completion which likely would have completed the entire line likely also with the correct string at the end or
at least something close to it because it would have looked at the the variable name and presumably would have said oh
you must want release type with a space in between as your parameter because I see previous instances of doing that so I
think it's even less less useful to to copy and paste code when it's sort of this somewhat boiler plate that's true all
right run and should pass oh it should pass that's the prediction all right did so now if we run all the only ones that
should fail are the ones that are failing on multiple themes correct that are that are specifying multiple themes of
which there's diff that's yeah so it's a multiple theme issue so you can see like um the the actual has just thank you
whereas the uh expected as thank you thanks and gratitude um so we can uh I'm curious what that parse song from one oh
multiple themes yeah what I was confused about is it says parse song and I thought it would call the parse song directly
and I was wondering why that failed but it's actually calling parsol with one song right let's rename that something
yeah would it be better to say parcel on single song yeah no you don't need to rename here because it's just a test name
that's true all for single song yeah is that what we said yeah yeah so now we can use this test as our uh to drive our
Behavior change so if we just run this single test this will themes and we can prove that using the difference yep and
it's basically themes so now we that so that one the way we're going to is theme gets pulled out there so this extract
column yeah that'll work regardless so if we go back NOP to here now do we want it to be blank strings though or the
list are we gonna have to stop we want the the size of this list to be the number of themes we don't want to have empty
strings correct themes that aren't there correct but I think we can I think we can do that a step at a time since this
one has all four themes the the data let's assume that it always has all four themes then we'll run all the tests and
find another test that will drive us to change that behavior got it so here I think you can actually times I could have
done the um the Alt J thing yes next uh and then let's pass that into of I noticed it auto selected what I thought was
the next one yes which was I thought I foolishly moved the mouse the wrong way okay so if we run this test this one
theoretically should work yeah this one should pass yeah yeah sweet we go back to yeah so we should still get failures
but only for those that don't have four themes oh we went to 12 from Seven failures yeah because now we're requiring all
themes so the ones that right that had anything other than four themes failed even if so the ones that had one theme
were passing so which one will we use now we can go back to par song with only one theme has pick and so now we can just
run this own oh actually let's look at the blank so I'm confused by that error message can we go look at what generated
too ah okay so it's a little confusing when applied to theme um because it's basically blank for other attributes it
would make sense like artist is blank and song uh can we change do we have uh I'd like it to display something like
theme where oh here yeah um what I don't know is do we have attribute because we can't just go change code without
changing a test yeah so here oh we're adding to it oh right because we we're accumulating yeah right right right right
um let's let's put that on hold because I don't want to go I don't want to push another change on the stack without um
yes without getting getting back to to Green so that makes sense that basically it's saying one of the themes was blank
which is absolutely true um and we'd like to fix that so that but it's actually so it's always going to be par song's
fault yeah so it's not colum mapper go so now what we need to do is we basically did theme 1 two 3 four assuming they
all exists now we need to um to to change that so we might want to extract that into a that into a method to make it
easier to to work with oh extract the list of well method uh extract the list of into a variable and then extract the
variable plus the individual themes into a method right so there yep and then you're saying this plus the list of right
y confused by where the cursor is I know that's why I don't I really don't like the inline stuff because if your scroll
point is is off the the new method that it's basically showing you overlaps where you actually can type in the name of
the method yeah let me try it here now let see if that helps I think there we go yeah I think that's a bug they need to
fix it has it it really needs to scroll uh line like line 49 into view so that you can actually change it it's yeah like
move 49 yeah yeah all right let's see that and now we would start ad like if so are val um not validation but our
requirement is that uh once we hit a blank one we ignore the rest oh unless you don't want that as a requirement um
which might be easier it's easier to implement it's easier to implement the current requirement or not having it as a
require no it's easier to implement if it's blank we just ignore it but we continue processing themes would we ever have
so do you ever have a theme in column three but not in col column two no my guess is not yeah um do we want to data that
well I guess the scenario where you could have it is like here I decide later on that I mean this is only I mean later
on isn't the right like that maybe this theme is not valid would I do um I think the real question is would would it be
o would it be okay if we allowed that yeah I don't see why it wouldn't be okay to allow it um I mean in theory we're
doing this sorry then let's allow it because it's easier code yeah good point okay do we have that written down anywhere
that requirement about you must uh we might have a if it's not written down we probably have a t we might have yeah so
yeah so let's um let's modify this method so we only add ones that are okay Oh blank versus empty what's the distinction
again uh blank uh so if you hit um forget what it is on Windows is it control Q or something I know it's F1 on control
control Q is blank is if it only contains white space so that's a bit safer H but on the other hand we are only
returning an empty string if we yeah and I don't like the fact we have to put a bang here but for now well got yep oh
right we haven't so what I might suggest before we do this um is generalize loop I'm guessing that it's not gonna I
gotta do it manually yeah I yeah I don't think there's gonna be any way that it's GNA figure uh yeah for each because I
don't not seeing we don't care about index well there's no such thing as a 4 each it's Loop like old school like with
the int I equal kind of thing well uh depends on how we want to generalize it um we could do sort of string
concatenation and that in that case we'd use an index Loop but I I would find that to be harder to comprehend than
looping headers so what I might do is basically create uh a list of our theme that and that's just a list of theme one
four and that could become a constant if we wanted it to but for now we put it yep and now we can create the empty to so
if you do uh theme headers do4 it'll yeah oh wait a second we haven't extracted early yep yeah and then what we'll be
able to do is likely uh convert this into a stream operation because what we're basically doing is we're mapping the
theme header into an extracted from something else but only doing if it is if it's not blank but let's see we'll see how
we'll see how good intellig is converting that yep so what I might do is um we could have done a bit of a prepare
refactoring uh if you comment out 50 basically the if if part of the block so 59 and 61 but there this is the
pre-existing Behavior where we're not skipping empty so we should still see it fail because there were attributes that
blank yeah right so that that proves that this is equivalent and now we can add in oh blanks and now this should code
and it does it does okay so now we yeah right we're down to four failing so now we had some additional constraints um
and so we're seeing at least the song Service Test failing because we've got bad data so we need to fix our tests first
let's let's go fix that one data bulk ad song fails but what is it failing for what are we testing here yeah so this one
is basically missing the header oh because this is not right right right right right um so this is an interesting
question uh we're currently throwing an exception but really we result so is the setup wrong no the setup's right it's
just that we're throwing an exception instead of returning a failed result I see so uh let's hold off on that one should
we disable it or just leave it and move on to another uh let's just move on to the other ones that are failing in a
different way so why is failing aha so here's our our test that says we should have ignored this theme because it there
was a blank right we change the requirements we change the requirement so that test might be invalid completely so what
I would say is Let's uh let's make our code fulfill that requirement oh and then we can because I'm uncomfortable having
to go back and now fix some of these tests uh I we're we're we're a bit far away from Green get back to green yeah I
know what you're saying okay um and it's an easy enough change yeah that let's look at what else is failing so let's
look at that test oh yeah that wasn't very helpful diff course all return to multiple failure actually was failing there
right right so basically because requiring uh five columns anymore test so were the requirement uh let's let's change uh
I think we might need to disable this one until we change our acception to be a result failure and then we can do the
once uh we return result failure instead of an exception for mismatched columns okay or mismatched column count and the
import should we go do it to that one as well yeah and that's likely the case for that failure yeah so that's the same
high level test disabled yeah it's interesting how both results the result pattern and the exceptions are sort of of
infectious and you have to go one way fully um otherwise you get into sort of now we've got now we got an exception to
handle and we could fix it by just changing our data to still be wrong but wrong in a different way um but what we want
is we basically want to get back to green so we can which we are forward which we are okay great um so now the thing we
we put on hold was uh if we hit a blank theme do we want to continue processing themes right that was this part right
here the break so we had a test that basically said no the rule is once we hit a blank theme we ignore everything else
um we could leave it like this or requirement because the code's just as right so I guess changing the requirement well
not changing the requirement is the easiest because they don't have to change any code at all we're done right right
well no we have disabled test yeah but that's a separate that's a different um is a separate issue um you go say a
little bit more because the other ones have to do with an exception that's being thrown this is having to do with themes
so how much more to switch this from break to continue would it would it remaining Test Now work I'm do that see yeah
just one test basically that one one I mean I could see a scenario where somebody accidentally or intentionally deletes
a mid theme it's not too gnarly to implement it I would say let's do it that skipping is okay it's changing the continue
to a break and then we can convert it later to a to a stream API um so let's change our test to reflect our our our new
understanding of a requirement this test one that failed yes uh so let's change the code back so that it passes then
we'll change the want now just run this one test no now we can run all of them okay because they're all passing and
there's just a bunch ignored um so here we want the list of uh so let's change our last theme to be theme and then we
would add to the list fail because it won't have that one in expected and now make a continue and now continue and now
it should pass and hopefully not break anything else well we've seen it we've changed we've flipped it a few times so I
confident that it was gonna do that that was the only yeah true and now we can uh Loop see What intell suggests um yes
boy that's long we'll reformat but we'll yeah we'll reformat it do do you typically do it at the stream or after this
the first after y actually I'm going to see what control shift L does yeah won't do anything because it won't unless you
have a setting turned on it won't Force breaks got it uh we can make this a little bit nicer um first of all we can
return this themes Y and we can change the filter uh to use the not predicate to make it a little bit easier I'm
surprised intellig doesn't us so if you're inside there does it option it that's a bummer okay then we'll just do it
manually so the method reference no that won't work no because it's going to extract a method we don't want to extract a
method what we want is so let's do this uh remove the bang in front of the theme is empty okay um and now uh now take
its offer to version uh and then surround it so if I don't know if a ARG will work here but you can try it yeah then you
just say not no sorry the word not oh lowercase n because it's a static method on predicates that work yep uh and I don'
t know why it did collect so so suiga asks the difference between uh collectors collectors to list versus a um it's
pretty much do we return a mutable list or not uh but we don't need a mutable list so we can just directly say uh
instead of collect we can just list like that yep nope I'm not gonna do do control end oh interesting yeah it won't
remove extra yep excellent that was true so that's much nicer than the than think looking good um so let's see let's
let's do a commit while uh no it's it's actually the the other way around sui so two collect uh oh so collectors to list
I believe Returns on array list I'm 80% sure um two list definitely the yes the collector's to list uses an array list
uses a yeah so I think what we've done is we basically support um we've actually finished both jeras so supporting uh we
now support themes yep okay do we have some parcel support her header so I think there's one yeah one final step we need
to do which is um I think we can get rid of that if if block this one uh yeah so let's let's comment out 42 see what
happens and the Clos brace oops uh happens oh we had one so yeah so that one uh again is is is again we're we're
throwing an exception instead of returning a failure result let's look at that um test well so let's see incorrect
because it doesn't have a header at all oh yeah good catch so um but it's just but we still want it to fail for having
not enough columns so let's put in a a three column header uh not there because we're going to throw mapper right so
we're going to oh in the right here yeah got it um do we so we want we want three column headers there yeah that's three
there's two songs so that'll still fail with an but it will fail with an exception instead of a failure message but at
least now the the the test is correct just test this run this one uh we can run them all because only okay yeah uh so
that one also needs to be disabled for the same reason right which you might have in your clipboard buffer yep let's run
them all we should have a bunch of ignored but all all the other ones should pass they do um so now we can drop the our
comment that out code and we can drop the no longer needed string header all right are now the test make sure we didn't
break anything yep that was already automated but just in case uh and so let's look at the uh let's scroll up to the
parse all and take a look at that still a pretty freaking huge meth method yeah so we we we've got some um but I think
uh this is probably a 67 and uh I think the only thing then left is convert our illegal argument exception to a failure
result and then we can undisable or tests this codebase 2 can be yours if you just continue to use extract method I mean
in general like yes there's probably going to be a certain point where just extract method extract method extract method
is not going to get you to a small enough method but it can get far but yeah it's it's I mean for example could this
it's 20 lines of code oh sorry pretty fraking huge I gotta get the lingo correct would you consider extracting the
stream into a descriptive method name because that that's a big chunk of the um I might I so the reason why I'm I'm not
eager to do that to to do that is I feel like uh I want to get result to the point where we don't have that if object um
I still have I still have hopes that we can that we can figure that out um we probably could clean up the uh you know we
could collapse 23 and 24 not oh just inline it you mean just inline header yeah but I like the I like the name so um we
could extract it all into you know we could extract those two lines into a method of create column mapper again it's
like it it doesn't doesn't get us it's it's not attacking the Met of the problem which is right the the stream and then
if block which talk I have to rewatch it I haven't watched it in I can't remember when I watched it um all right so I
think uh so do we want to figure out what we want to do past fixing our illegal argument exception like what's our next
set of features I think we were talking about getting it to to the database yeah yeah I think that's next yeah and I'll
clean this up I get some yeah comments amongst our tasks that I should move but I can do that offline well let's move
the database up to above 74 to make sure we know that that's our next big feature so would that be out dented I think so
I think that deserves yeah and then we some other things we did Skip I would still like to do like a custom assert and
um maybe do a little bit more on the results uh so maybe once we we finish the illegal argument thing that might um
provide us a a good opportunity to do persist you didn't see mode switch I saw no mode switch was typing what we what we
just said so yes yeah so I think let's um let's make sure we don't forget to do uh so let's put some annotation next to
uh certainly 61 I certainly want to custom because we're going to be doing some more of those and I I certainly want a
custom assert for result so for you annotation is something like this or did you mean something else uh definitely
something like that but maybe only one instead of three three has the the connotation of we're doing that next one is
just don't this all right look at that and we're finished on time too cool and then what's it there was there anything
else no this is just the parent parent okay cool yeah I find it amusing that um look we finished on time it's like well
we always finish on time because we take small steps so we could stop at any point so it's a bit of it's a bit of a
cheat to say oh look we always finish stuff on on time because we always have generally not always but uh but generally
have a good stopping point and that's what happens when you take small steps yeah and I'll might as well do a push yes
please well it failed on the um commit any way and push those are ignores yeah all right so That's all folks for today
thanks so much for for hanging out um we don't have a we don't yet have a scheduled next stream so uh but it might be a
little while because I am going to the agile open Northwest uh open space Conference next week um so that'll uh suppress
our streaming for a bit but as always best place to find out about upcoming streams is on the Discord join the Discord
cool and yeah I wish I was going I accidentally I had too many things going on so I can't make it up up to Agile open
Northwest I've heard great things about it so if yall are in the neighborhood if you're if you're in Portland uh next
week go go to the conference you uh you'll you'll get a lot out of it I think so all right um sui says wasn't well on
your content you got you've got other cool stuff like uh Socrates of various sorts to for a craftsmanship um open space
conferences so those are those are really good um most of those are too far away for me they're like the UK and other
other places in actually on Continental Europe um I know there is one in Canada but it's so far away like it's it's it's
almost East Coast Canada or it's like Toronto I think is the closest airport but then it's like a drive from there and
so I'm like no and that's only a two-day thing so it's just not not worth it for me to travel all the way to that um but
but uh look out for the Socrates ones in in Europe those are really good all right that's all folks thanks a lot we'll
see you next time have a great day
