# ＂Song Themes＂ Episode 19： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=2VAsQpflZqM

---

## Transcript

all right folks welcome to another paring stream this is episode 19 of of working on Mike's themes at welcome everyone
how you doing Mike good and you good yet I would say I'm probably in a similar boat yeah we'll get there yeah so uh last
time we were working on improving our our experience when importing the songs have some problems in them so validation
errors right I think we were in the middle of a prepare refactoring if my yeah let's go take a look looking at what I
got here let me get rid of my Infinity screen looks like we're in the middle of coding something we got a a um left off
with a comment yep and a compile error so that's good yep so what we trying to do was um turn uh so instead of throwing
an exception so so our model for um doing this is instead of throwing an exception having to catch it maybe in the
service layer or the controller uh we decided uh to use a uh sort of result pattern and this is a much more Comm I
talked about this last time it's a much more common pattern than the net world not quite sure uh why it hasn't caught on
quite as much and maybe there's no no standards on the net there's there's there's support for that but in Java
specifically spring boo there's not I don't know that it just doesn't have it as and it's not as prevalent so um so what
yeah do folks do in the Java world do they just roll their own different yeah yeah so you'll see exceptions and
exception handlers or you'll see um I don't know I I've I've looked around at at projects and and it's mostly um like
the validation is done in the controller or um or just they don't or they or they rely on exceptions I'm actually not
sure be interesting to to ask around about like what what what do people do um maybe some people use a result type thing
but um this is something that's that's really hard to tell uh what what sort of real world apps are doing because there
aren't a lot of real world apps that are that have the source available there's there's lots of apps on on GitHub that
you know spring boot apps that are pretty much just toys and people learning um and just people copying one another uh
but not um not significant apps um I have come across some some uh some apps that are a bit more significant but I'll
have to look and see what they do what kind of pattern they follow for for um different kinds of basically business or
domain validation uh that yeah that's something I'll have to look at I'm going to take a note yeah it's interesting
because when you think about the concept of design patterns that they've they're basically nobody no one person creates
a design pattern they multiple people have done the same thing in different projects right and then someone notices and
collects um the information and making a pattern so like you said it sounds like in the net World they do have the
result pattern yeah um they'd be curious to see if there is anything in the Java world interesting hey Jonas welcome
welcome to the YouTube stream astd all right so um uh I think where where we left off was uh we converted throwing the
exception in our par song We converted that uh to return this result failure thing and that's there in in line 29 uh and
what we want to do is um converting it and before this used to throw an exception but now it's returning a result right
uh and we're currently I think ignoring that and so do uh was extract that part to um to the to that new method that we
that we had pars with result yeah so we we've got um the the parse method alone maybe make the bottom bigger because we
want to be able to see I was L just thinking that and I wonder if if maybe 150% Zoom is actually too much because it's
hard to code yeah I think that's that's that's GNA be have have to be our compromise because we need to see more codes
so we've got um we could move parse result up to yeah let's that's I was about to suggest let's move that up so at least
together yeah as I figured they're gonna record L&amp;L so I'll just watch it afterwards when whenever whenever um I
want to suggest uh the shortcut to use I have to go and actually do it in in intell and to figure out what is what is
that the moving up one yeah yeah instead of doing C cut and paste yeah so it's control shift up arrow and down arrow
okay so and just be anywhere in the line yeah so if you're on the method signature line where where you are now it'll
move the whole method if you're on a statement it'll move just that statement got it so move it up there down below yeah
cool now sorry I'm write that one down you said it was so I later control shift Arrow control shift yeah and and do I
have that I do in your uh in the Ted official Ted cheat sheet actually that one I don't I have to add that one that one'
s a lesser used one that's why it's it's not in my cheat sheet yeah come noted and what's weird is is uh shift up arrow
and down arrow on on Mac does something completely different well not completely different but it actually jumps from
method to Method method uh that would be just alt up arrow and down arrow for you what is alt up it does what again well
do it do alt up arrow and I do alt oh got move the carrot for carrot from from method to Method uh in that direction oh
that's so interesting I that you said carrot my brain said cursor but you are 100% right it really is the carrot not
it's it's the terminology is a little bit confusing um I try to use carrot because that's um because mainly because uh
uh it's what intell calls it jeins especially when you're in like multi carat mode it's the carrot but most people think
of it as the the cursor but the C so and for example the cursor is my mouse moving way over yeah yeah but the carrots
over there yeah I never really thought of them as two separate things yeah um yeah nice so what we want to do is we want
to have um uh want to have the so right now the um the par song Only returns no it returns a failure message if it fails
and it Returns the song If if it's success um and I don't remember what part of that we were extracting because based on
the comment here the whole par song method returns a result I'm suspecting we wanted to do a subset of it like this
maybe did we have um uh you can actually probably make the splitter a bit more even with the smaller text um what did we
have so we had test um yeah I don't know I don't remember what we what what Our intention was yeah seems like it feels
like a prepare something parse with result I guess our breadcrumb wasn't as thought so um did we have a test for just a
parts of an individual song with not enough not enough one doesn't look like it what's the one one oh sorry what was
your question again my question was where's this test ah the test for a single row as opposed to multiple rows um so
parse a single um we have that because we translated the exception into a failure message so that that's working I think
I know why because we were going to um well we I think we're doing that prepare refactoring because we're getting ready
for multiple rows wrong and starting to collect the errors so that the final that the error message at the UI is all of
these rows these are the rows that had problems right I'm just not sure why we had parse with result because we already
have the parse method the parse song method returning a result um what is the the par songs method return the one above
it okay so that's the one we want to eventually like we wrote in the goal is ah there we go is that but I'm not sure why
uh uh oh okay I know why so um can you take the method that that's currently not compiling and move it up to line 25 yep
oops got to put the Cur the carrot in yeah so we wanted to refactor out from here not from par song that's that's what
we even said pars reading yeah because we were just waking up right right yeah not enough coffee exception um so uh yeah
because right now the parse the parse method which takes the list of of new line to limited stuff uh does not return
result and what we want to do is um map the part that gets the result uh because right now what we do on line 22 is we
we throw away the result and we want to stop doing that right so we can see that um with with intellig little uh hints
we get the par song we we get a stream of then results but then we toss away the actual result and convert it to sorry
don't sorry uh so you can see on the right with the with the hints we go from a stream result which is what we want um
but but uh for backwards compatibility we then did a map uh to to a stream of song so we wanted to do is is basically
extract the from the the the lines down to the map basically want to extract from lines 19 through 21 and that's what we
want to put into the parse withth result so we should be able to do that as a refractor as an extract refactor ah so up
two there yeah no oh it's Control Alt yep one more time mode guess we got to give it a new name um well this is the one
we want to call parse with result and we'll just take the the method that we manually created that's fine oh if I hit
enter will it just keep it or I have to give it a uh hit enter and see what happens no won't let me um then sure yeah so
delete the other one we can it where uh I wouldn't trust it's in interpretation since the code is not compiling right I
wouldn't do a safe delete just delete it oh just do it manually yeah because it's actually the test that that's using it
but we're going to thing so somewhere uh we broke uh some test codes let's um probably because parse with results uh is
private we want public but now the return type is wrong but that's okay we we'll have to fix that but that method was
didn't we just create that method so how is it well we created the temporary placeholder which is what we wanted to test
um but that was returning uh but that and that was public we just deleted it when we extracted the method extracted as
private right but how could anybody have been using it since it returned nothing even though it had a return type of
well the test wasn't passing it wasn't even compiling so the test compiled the test code compiled but the production
code didn't compile got it okay now the production code compiles but the test doesn't compile because we're returning an
individual result as opposed to a stream of results um um now we have to decide what again hey aderan welcome so right
now result is an individual result uh and I think our goal is that this should be a list of both songs and a list of
failure messages right because we want the result to accumulate both or one or the other basically um so right now
result is for a single song right or single failure or single failure yeah do we want a new class that or a new object
that's a list of results no no we want result to be the result of the operation that we're calling and so it will
instead of um the question is what what what step do we take to get there got it so it eventually it'll be line seven
will be a list of songs right and line eight will be either a list of strings or one string with I think it' be list of
strings think go with strings yeah because eventually uh you'd want even the failure message perhaps to be a little bit
less stringy and and more structured but for now we'll just not worry about that got it makes sense are we doing
discriminated unit sort of kind of as best we can in Java um so now we have to figure out what our next step is which is
do we want to modify result to have those multiple things or do we want to um just return a stream of results get our
test pass and then convert this the result to be multiple um things oh generally I favor getting to Green faster not
yeah I think I also don't like if I saw a clear path to to the result um but I I don't see I don't I don't I can't
visualize a clear path so yeah let's take a small step to get get the grade uh so that means we'll have to change the
result type here um correct um that'll make a yes uh and then we'll we can do is in our assert that we can assert that
result and we can get Success um no no outside of the assert that what we'll want to do is is say uh has size uh
contains uh because I don't think we care about the specific failure message just that it is a failure so extracting and
then um we can do uh the method handle result colon colon uh is Success so third option uh and then we can basically now
we can say false so what that does is basically um the extracting is B is is very similar to to a map a stream map so
basically calls on each entry in the in the list because it converts the stream to a list and then uh calls its success
on each one fills up a list of booleans and then we're just saying that it contains only one Boolean and that Boolean is
false so yeah sorry I say I noticed that it says the variable name is two songs it's really one song yeah I think we we'
ll want to have uh two songs but for now we'll we'll just get it get it passing with with one got it and then we'll
refactor yeah run um yeah and let's see before we run the predict yeah I think that'll work okay because we're using the
extracted code which we know worked um and it should parse only one song cool so now uh let's add song you don't need
that for right right right right right today so now in this case we should have has size two uhhuh but would um when you
extracting is success will it extract two Fales and then we have to change this exact way to somehow yeah so then we can
say contains is actually false comma false ohy because this is just a list of values just happens to be booleans got it
yes yay for yay for text blocks for sure okay I think this is going to work too we actually no maybe not um what is par
result it's doing the filter yeah it's doing a par song each par song will individually return work learning the test
yep and yeah all right so now um what we want parse with result to do uh uh now I think we can uh start thinking about
how to convert to a single result that contains multiple uh multiple values um however uh this Parts with the result is
the one that yeah I was going to say we we we want to start converting our real code and our other tests to use this
method but it's not ready yet because it's returning a stream of result right would we would we do a parallel change
well we are kind of doing a parallel change because this is this is the new method that's going to replace the existing
parse method above it right this cursor because we basically want to get rid of the pars on on line 17 that's the method
we want to get rid of should we Market is deprecated did it pass for the raisin yeah uh yes we should Market is
refactoring for parsing returning a ad instead of list right that good yep est's still mad about code coverage as the
goal yes fight fight that fight the battle oh I'm sorry well uh right it's running all tests sure those should all pass
though unless we've broken some spring stuff y they all pass good good all right um so what's our next step so we've got
uh uh pars withth result but it's returning a stream result so I think now is when we result where we prepared to hold
one oh so internally yes got it so this this would be a pure refactoring internal internal so the boundary uh of change
is is just this class so the interface will stay the same but internally this will become lists yep list y got it let's
see how we do that from a refactoring can we say this is such a small class I think we yeah and then values I presume um
so we called it value when we were sort of being a little trying to be a little generic uh I think we can be more
specific and then when we generif it we can we can figure out what the name is so this should really be songs okay
didn't take must oh I know what I did wrong hit the down arrow yeah uh rename the parameter I hate that this dialogue
box comes comes up so tiny and I know layout is hard on on goys but it always comes out so small want uh and so then
let's um we probably want uh I don't think intellig is going to offer any help here um what we probably want to do is
have uh the Declaration of list like that yep uh and then 14's instead of an assignment we can just do an an ADD
somewhere yeah so let's consistent and now now here's where we we're backwards compatible and we just first using the
new sequenced Collections and I hate the fact that it's get but and not just first and not just first yeah I understand
why because there is a method that returns a specific one given an index um but I it uh so this should have been a
completely uh encapsulated refactoring um so let's run run our test to make sure that we commit rant better enough yep
all right so now what we want to do is we want to do some parallel change um we can sort of do so because what we want
is we want result to split I'm just wondering if we can split the editor panes in a certain way uh can we split results
so it's off to the right so we can have result up at the same time as everything else so just just drag and drop oh do
you mean like this yeah yeah what I'd want and maybe maybe in doesn't support it is I'd want result to like take up the
full vertical space Oh but I don't think it supports that uh unless you split do we need this parser yeah because we're
gonna be changing it uh we're gonna be Chang does it need to be wide like if we put this up not I mean it's temporary
just to get through this actually actually now if you resplit it uh it's probably what we want ah so bring this back
down yeah yeah no there ah there you go yeah so it's it's it's an ordering issue yeah uh so asra ask does does does does
get first blow up if the list is empty um I assume it it it's doing a get you know with a zero index and so if the list
is empty yeah you'll get an array index out of bounds uh exception so so yay we got our splitting right okay uh so what
we want is um a parallel change where we have a method called songs on our result uh in addition to uh oh we should
probably do the same for failure messages right since we'll want multiple of those in fact that's the first thing we'll
modify because we'll want this test um we don't have a test for failure do we or we do well we do right now but uh we'll
want this test to to remain passing because line 55 eventually return just a single result as opposed to a stream of
result so once we make that structural change then we can change this test um uh and add the multiple failure messages
so let's let's do another prepare refactoring for the failure process that's so might be a little confusing because you
renamed the parameter on 17 I think actually we did that before and realized we didn't want to and so we actually don't
want 17 parameter to be plural right eventually it will be but right yeah yeah um so that work oh oh because we didn't
uh assign an array list rerun the test unless you like seeing continue to seeing red yeah it's funny for such a for such
a mechanical change um it's still easy to make mistakes right and that's why we have tests all right uh so the test pass
commit protic all right so now um um we've got so we could so now I think we now we make the jump right so we've done
the prepare refactoring and now we can make the jump to parse with result um internally having the multiple failure
messages the multiple failures um would we drive that from the test and make this be a list of result instead of stream
uh well it's not no so it's not going to be a list of anything it's going to be just result oh right right right right
result holds list hold the list yeah yeah uh but I think we'd like to um we need to change our uh we're not extracting
result as success anymore we're extracting uh the failure message uh and what we're going to want is failure messages
but let's let's do one more so let's change our assertion so that we can track the failure messages um so we'll probably
want to copy the expected failure that we have in another test on this where we tested yeah and as a separate assert or
no so what we'll want is uh we don't need that assert line we just want the text so just cut grab the text out of that
and then delete that line uh and so instead of extracting is message this is the downside of of those inlay hints is
sometimes they get really big uh and so now we want to have two strings so instead of the false false we want two two uh
two strings that one and then probably on a new line oh it and if you run that that will fail how it fail Ted it will
fail because it will have uh the first string will match but the second string will not have artist 2 and song title two
thank you for for making me be more precise excellent so James asked what do you call writing the logic first and then
the test to validate the logic uh the typical way people develop after technically test after yeah yeah um I call it
test after sometimes because lots of times people just don't all yeah AST I was thinking exactly the same thing um it's
like oh this is easy we'll just you know you just do it and then you realize you forgot a trivial step yeah all right so
this failed as expected let's fix it up um perhaps provide maybe a little bit more variety in our input um so maybe have
three columns instead of two I forget title rerun it yeah and so now it'll fail because um the second message will be
three instead of two uh and the row contains will be wrong and what we'll do is we'll actually copy and paste the output
into our test oh you've got an illegal Escape y yeah my brain was going something was wrong with what I just typed and I
couldn't figure out what it was so or I gave it a few seconds of brain power but not much so you can just grab the the
correct string out and and we'll paste that in since we know that that's the right thing control W is your friend there
I know still haven't gotten in the habit of that one uh and you want to not you pasted the the strings you want to do
control W one more time to include the double quotes ah now Place yep yeah now pass excellent I imagine folks might
being isn't that cheating you took the answer that you got and then just pasted it into the the assert so what what
characterization kind of yeah so what's interesting is because we predicted exactly how it would fail right I said it
was gonna be three instead of two and it was going to have the the title at the end um yes we could have manually
updated the string but we know that the output was exactly what we expected it to be so the output was correct um we
just hadn't hadn't gotten our test up to date um uh and so yes sir it wasn't correct so why not copy what we know and
evaluated manually is correct uh so it is very much yes I approve of this um so it is very much thing hey there X proof
uh should your dto be modeled exactly how your you expect your input to be yes that is their purpose that is their
entire purpose in life is to transfer data hence the name data transfer object uh and so therefore uh they are the thing
that Define what exactly hey there NE uh nephine nephine um uh no we haven't done anything with spring AI um is it
mature enough to try on some toy projects certainly for toy projects I think it's mature enough um and know uh uh Dan
vagan and Deshawn Carter had uh I think it was yesterday did did a uh office hours on that so you could take a look at
that video on the spring developers Channel um yeah so I think it's with um all right so we now have a test that where
we extract the failure message now I think um now I think we can convert parse with result to um is there a way to do
that with a refactoring not really so changing this wouldn't enable a refactor no no there's not going to be any there's
not going to be any automated way for intellig to figure out oh you don't want a stream of results you want a result and
we'll put the multiple things in that result no that's not how to do that right um what we could do is there a smaller
step step is it worth it though um so the smaller step could be that we continue to return a stream of result but
results now had has uh multiple failure messages in it um so instead but I don't know if that's worth at uh wait a
second so the stream currently is being tested for having multiple res objects right with this content right not a
single result object with that content right and that is the next step is um let's actually I think we can do it in
slightly smaller steps so what we can do is um have another method uh so we'll do more parallel change um have a method
on on the result that is uh failure messages that Returns the list of string storing sure should we do that from the
test side yeah so let's change um um uh let's see um we want line 58 to be failure messages that's going to return a
list flatmap um don't normally uh and maybe it makes do you think would refactoring out of streams into a for Loop help
us as and then refactor back into a stream no um because we're not we're not using stream operations here this is all
assert that oh that's a right um so let's let's do this let's uh let's change that to failure messages plural that will
force us to create a method we'll go ahead and create that yeah and then uh we'll return and a copy of dot copy of yeah
of our failure messages y um and so now it's going to complain because what it's getting from the extracting there on
line 5859 is not individual things but a list of string so we can do is we can uh put did you add the P at the end yep
oh oh it took it away cuz I typed it in um oh when I made that mistake it deleted it I see so this now should continue
to pass because this equivalent okay great um and so now what we can do uh is we'd like to now make a change where parth
Parts with result returns a stream one so let's we yeah so let's change the fail because it'll be two instead of one
right good and now um now we need to go into our pars with result we might not be able to change it at this level um
yeah so this is this is interesting so um where do we sort of accumulate the new results so there are two there there
are basically two mechanisms one is um we could use do the accumulating parameter meth uh way of doing things so pass in
an empty result to par song uh and then it returns a result with either the song or the error failure message added um
or this method uh sort of par result um does the what's the word reducing uh to result I I've I've never been a I don't
know I I I don't know how much of a fan I am of of accumulating parameter it um I don't know I there's there's something
about it I don't like and I'm not sure it is um because it's not it because it's a totally fine pattern um so we could
do that uh which would make it a little bit easier um I do you have any thoughts on on don't I've us had accumulating
paradin a few times but not enough to like be like oh I have a a gut Pro or a con on it um if we go that route you're
saying Parts with result change will be a little bit simpler or do we just do a dual change try it one way and then the
other and see what we think yeah I think I think I don't like it because what it's going to do is it was it would force
um par song uh that you'd have to pass in a result kind of an empty result we don't really have that concept um but we
may we may sort of end up end up there anyway I'm not sure hey there lit uh no we're not using multi-threading um uh I
mean we may want multi-threading at some point more more in terms of background here in X proof to to answer your
question um if you have a class that only needs to set two Fields then you want a different dto dto are cheap um use
them for one purpose don't try to make if you don't need all the fields and you're not reusing it exactly as is make
another one in Java their records really cheap that so let's let's uh figure out how we would how do we want to uh so
this will probably require some more changes to result um and we might actually have to switch gears and start testing
against result directly um because we have no way right now for result to actually uh be given multiple like add this
failure or add this success because it's all through the Constructor at the moment 13 and 17 well it's all uh it's
actually all through the um oh the static yeah I mean yes through the Constructor indirectly through the through the
static methods yeah are these Constructors need to be public no they could probably be private in fact they probably
should be private yeah thinking one um actually now I'm wondering uh so I forget what did we say that we want from
result if we have some success and some fail was ah there we go no partial result All or Nothing okay um basically I was
so I was trying to figure out if we have one failure message then we're not going to bother saving any of the songs
that's that's right okay um so I think then what we do is is we do uh another map uh so we do a par song from that we
get a stream of results so online 29 um and then from there we need to are if there's failures in any of them then
immediately we need to accumulate all the failures right we don't stop parsing but we stop saving the songs yeah so I
think um we need to save that off into a stream of results so let's do that uh so let's take that entire return section
and variable and how do you go back uh hold on the shift key ah let me I'm gonna do it again and deliberately go over
and then got it to a variable right results want is if there are any failures return a single result with with the the
failure messages okay so we'll need um and this is where uh we might want to write a I mean I don't know how we feel
about writing a test for for something that be fairly trivial uh what we'll want is a Constructor or basically a failure
static method that takes multiple strings so I don't know if we want to write a test for that I don't feel from testing
the result class directly or via yeah because we're gonna test it indirectly here um do we even have no I don't think we
we have a direct no we don't okay oh we can always use it and toss it if it feels like it's not useful but if it gets us
to The Next Step well we'll get there anyway because we'll be forced to create a method that takes a list of failure
message strings um so I I don't I don't feel like I I I don't feel like I need to test drive the the result to get that
that method so uh I think here is where we can um change it to to return a single results so let's the signature change
officially uh no we're going to have intell help us so let's say on line 30 what we want to do is we want to return um
result. failure with error and so now we'll need to have a method so Alt Enter is your friend if you click on two lists
there somewhere Enter and we want to create a new method result um that's actually wrong uh that should be list of
string and I because we kind of skipped messages and uh yeah let's Constructor yeah so we'll result um yeah with the
failure messages Constructor yep yep then we'll add right you want to be sure to put the this in front of it to right
yep private uh catch all right and so uh on the left side bottom left on 30 um we actually do need to do a map so we
need to do a results. message NOP it has to be a method call oh nope no inside the the the map method call we need to
put stuff oh right right right failure um message singular okay and so now um if you do uh Alt Enter uh we yes and so
now that's going to break a fine well let's worry about the production code first and then we'll test what's the best
way to jump to the production code that's failing just the um nextor move move the carrot to the correct pain to the
bottom left pain because you're in the top left pain you want to be and then F2 yeah so here parse with a result is uh
return yeah so we need to say Do songs uh actually but there is no songs yeah okay and you can get rid of the rest of
there yep so list copy of songs all right because yeah there's an extra space between the of uh not in the production
code so let's now fix line 55 there on the top that should just be stream that should just be yeah so now result won't
have any size at all uh and we can drop the extracting the whole line uh yeah because what we'll do is we'll say result.
failure messages uh that uh and then we can drop the list ofs unwrap uh let's see what we a lot yeah oh my so how are
you feeling about uh what we've just done feels like we made a really big it I would roll back um to a certain point and
then figure out how to take a smaller step yeah so we'll roll back to our last commit uh and we'll take a break because
it's break time oh yeah totally break time uh and we'll roll back after the Break um sure yeah we'll roll back after the
break sounds good all right so we'll take a break when we come back from the break uh our brains will be a little bit
fresher and we'll we'll try this again um so we'll take a five minute break and break hey folks uh just a reminder that
um if you want to have discussions about the kinds of stuff we do here on the stream uh join the Discord uh as I've
mentioned before we are uh currently reading a book as a group and so what we do is every Sunday at 10: am Pacific 6 PM
UTC uh we get together on Zoom for a couple hours and talk about a chapter or so of a book current book we're reading is
the programmer's brain um it's not too late to join uh this coming Sunday we'll be finishing up chapter 2 so you can
easily catch up uh so go ahead join the Discord if you're not already there um if you're already there but you're not
part of the book club just send me a direct message and I'll hook you up um and uh no charge so if you join you get
access not only to the live sessions but also to recordings of past way all right so let's uh let's roll back we're
gonna roll back you have a preferred technique for doing that just go back yeah so so what I do is um I I do uh I open
up the the zero and basically hit the backwards facing button that one roll back and then select all the all the things
yep okay yep all right you run the test yeah let's rerun those tests make sure we're Green step is that what we we did
too big a step or did we take the wrong step well so we we basically um mucked with the parse method on 18 at the bottom
because uh we ended up changing the way the success first um to support multiple songs and and go that route so
basically um correctly yeah uh and so pars with I actually think we should uh sort of undo that because I think
extracting stream of results made it hard for us to take the next step of turning stream of result into an individual
result that has multiple things in it so you're saying inline this well if we inline that we we we muck up the test that
we so so can we so what we'd like is um what we'd like is is our parse song uh which is down sorry the the so the parse
song Let's see what we want is we want our parse method or parse with result to be a single result um can we make that
change without doing anything else uh or what would it take to be able to make that change without breaking anything in
other words make pars behave like par song No make pars continue to work but change pars with result to return a single
result that has multiple songs in it because that was the step that messed us up say it again make Park pars result
return a single result instead of a stream of results got it so what would it what would it take to to do that but still
leave the signature of parse to be say the same Still Still yeah because that's a that's I think is a separate step this
is where my my thin knowledge of uh streams is impacting my ability to suggest well put put streams aside what here um
so in order for this to in order for this to work uh where parse returns a list of song and we handle multiple songs the
only way that songs right um so I think we have to uh and resulted structured to hold multiple s yeah so let's yeah so
let's expose let's redo that part where we messages um as query methods uh so songs Returns the list of songs and
failure messages Returns the list of failure messages is there a uh you can create Getters for both of them we can
rename them yeah but we're but we're going to want to do a copy of as part of that but you can generate those you can
generate them where to put them oh there we are uh so unless you have the the live template post fix installed uh you're
going to just have to do it manually with aarg and a list dot uh list then I presume we want to rename these yep that
was it suggestions get songs or get songs not so helpful um yeah songs and then this one is look at that the suggestion
list kills me yeah yep well of course what else are you gonna do would you like these move to the bottom uh I would like
to move down I'm not sure about the bottom per se but basically next to where the other Cur meth are uh oh did we just
mess up yeah so one one problem with using the move method is it reformats as it moves it down which can mess things up
um when I'm moving more than one method I just paste hey there in marulu song I think down here is fine I'm not going to
be I I don't really care where else okay below the below the static okay um I'm gonna be annoying I want to at least
have song and songs together and pay your message I have no idea why but all right uh so now that we have songs
available um what we want is we want to change our parse with results to basically map it back into a uh a single result
um which they which we probably could do in a collect sort of way but uh I think that's a bit a bit um uh extract
variable alt I always get that one mixed up uh and these are going to be songs and we'll we'll we'll fix up the the type
in in a second uh so let's now um after we so out of the map what we get are basically a bunch of results um what we
want to now do is basically list um and that gives us a list of results uh so no we want to lists and so what we want to
do is we want to pull the that and so that gives us a list of song so we can change the Alt Enter to change songs so
success but where we're going to pass in multiple songs and that will and that will force us to create that sequence of
static Constructor so okay so do songs but then it'll Force us to make it a Constructor right a success Factory method
that can handle a well create method and result this one do we want it to be a stream of result no we want it to be just
yeah that's correct MH okay do we have a constru that can okay so let's change the signature of the existing one sorry
should I stop what I was doing no you're right okay create no no that's signature oh I see what you're saying go back
options change signature of result uh the song one that one to list of it and then what we can do is on line 22 wrap
that with a list of no inside of the parameter all right because what we've done is we've changed this so the list so
that way we don't end up with 14 no uh yes sorry you're right at all you you're right yeah no I was just wondering what
yeah okay uh and let's rename the variable to uh now we can start backtracking from uh result we want that method to
return a result Enter no I'm just looking yeah that one so we want that things so here we won't need to map it um uh map
it at all so you can delete the lists um but since it is returning a result and we're expecting a list of songs and so
now if we fix the test on the top change oh this one okay yeah yeah um here we want uh so this is this is this is
basically going to be uh a breaking change for us um because it's only going to return success uh and that's fine right
because because uh what we'll do is we don't want to break anything else but we want to change this Behavior this test
is is going to be new Behavior where what we're saying is now a result um uh will'll have multiple things in it um so I
think we can actually um for now comment out this this test oh the whole test yeah should we just disable it no because
it won't compile ah um because I want to make sure that all the other tests that that we haven't broken anything with
with what we just point okay great so now we have basically everything else working except for our our new behavior of
uh of of failure uh here um and this is uh parse with results returns a single stream all right yep committed and so now
we want to sort of redo this test um but sort of the right test and uh let's do that change we did title and uh so let's
redo our 58 so what we want here is we want to false um let's run pass actually I have no idea what it'll do no such
element okay um interesting element because what it's doing is uh parse with result we're pulling out the songs and we
don't want to do that uh let's swap things around uh let's do another refactoring so let's test I mean an at sign there
oh it's only one key off come on no and uh what we want um is we want pars with result to actually return the the proper
result we're sort of Faking It by returning it a a su a forced let's let's inline uh parse with result just into there
and then we're going to re-extract is wrong well no that is still our goal but it's really the goal for the method below
it but I think we're we can we can take that out or at least that line out yeah leave the goal yeah um and so now what
we want to do is uh so let's scroll down a bit because we 32 so out of the map of the Parson we get uh a stream of
results and we want that are you saying this no I mean we could use that but that's that's that's not gonna that's not
going to work for us uh so let's change the the variable to hold thing um so now what we want is we want uh let's change
the variable of songs to is so now how we convert a stream of results to a single result that's that's there well I
guess no it's are list of result and we wanted that for each one if it's failure we do one thing and if success is this
old school if if statement time unless you have a better suggestion test but it's a stream well what failing test are we
fixing if we're going to write an if statement what failing test are we fixing we don't currently have a failing test we
don't currently have one that so how do we get to so what what was the test that what test do we want a yeah actually I'
m not sure are we trying to get this one so we can undisable it or are we trying to just keep everything green well uh
what we'd like is is um we're sort of going so previously where where we went and then we had to back up we went down
the road Road of uh going down the failure routes because this test drove us to go down the failure path um but we've
been going down now the success path we inline the code so we're not modifying uh we're not changing the way the the
success the success works but we'd like to stop having that code in line there and we wanted to rely on our parts with
result so um I think it might be easier if we create a test that calls Parts with yeah that calls Parts with the result
directly um but actually is a successful outcome oh because right now we only have a well the disabled one's a failure
one right so we want one that uh like it except one that that passes and we probably have one that is calling the parse
directly right I think most are calling Parts directly yeah yeah and so we just want one that's that's successful and
inputs and so we want multiple oh this one this one right yep duplicate the whole test or just the first well I can give
you a name if you need a name sure so this is um parse with parse multiple songs with successful result yep yep and we
want to we want to hold on to the return value all far yep yeah that's fine and now we want to assert that uh result to
true know no oh result result dot is Success yeah right this will actually fail because we're currently returning a a
constant for is Success um but that's good because it'll it'll lead us to flesh that code so the constant personal
method found this is be results is a stream you want to convert it oops okay results it's a stream oh I see um yeah so
we basically need to to to do yes so in fact you could you could delete parse with result and re-extract to to a certain
extent or you could just copy and paste delete this whole thing or copy and paste so basically lines 23 and lines okay
and then paste them into after 31 uh so 31 and a 31 and change the return type of results yep so what I'd like to do
since we just did that to make those methods now look alike again is delegate uh uh the top method so let's disable the
test that we just wrote and the test should pass and then we can delegate lines 20 three 25 and and that line and so now
let WR return pars with songs did you say dot songs yeah but you got to pass in the parameter oh okay sorry yep reenable
so this should still fail um the failure false false say again oh you said we're we're we're having success always being
false right right and we're doing that is that here uh I'm not sure what you're looking at the is Success method is
returning false right so if I click on it it goes here oh it's just hardcoded defaults right okay I didn't see that yeah
uh so we'd like that not to be hardcoded so we by will we check if there's any failure messages then return faults
otherwise I mean we could I I I kind of don't like that um yeah uh I don't I don't like checking for for empty for for
either one um so I think we should just turn it into a field ah can I turn into a field directly uh alt a Boolean I mean
want to initialize it in uh in a Constructor there we go interesting that looks like a drop down but it's actually a
weird interesting yeah okay and we want to call it um we already have a method called success um so is Success right I
was thinking par success but I better so if you run that that'll still fail um then we make because that was a prepare
refactoring yeah and now we can make the one line uh easy now that we made the change easy now we can make the easy
change and run the test should pass now should pass now yes y yeah that's much cleaner than checking the error message
because I forgot that we had two different Constructors one for fail yeah and eventually what we'll end up with um and
this is generally how it goes is you end up with two subclasses because there's no point in holding on to songs if you'
re a failure and there's no point in holding on to failure messages if you're a success um and then uh it can then it
can once again return hard-coded values and then we'd get rid of it but for now um we're still ways away from that uh so
let's do a commit now that we have uh I think we're on a better path before message Success yeah did his success exist
before yeah it was just hardcode to return false oh right well it wasn't his success it was it was his success oh it was
oh okay yeah yeah we added the field his success right right not the um property that all right so now um now we can go
to our uh tests or not other but now the only disabled tests we have left does this show you if it's disabled not if
you're in result it doesn't that's too bad it doesn't is this kind of what is this little symbol here oh that's the same
no there it is right here it does show up oh it's really hard to see here I I me move the cursor down yeah it's still
too it's really tiny yeah yeah oh good good that tells you um all right so let's reenable it uh let's run it want to run
it see what happens uh actually it should pass now I think right and if not then uh oh no such element oh good good so
it failed for a reason that makes sense but not what we failed let me see the No Such element exception so get first
which I remember when we hovered over it earlier it throws no exception if the collection's empty right so if we're
parsing sorry which the new test of course don't we just enable ASD oh cool yeah Mark ordered a copy of my game cool um
so let's let's uh figure out why this failed right so somehow this is getting called probably within this par so okay I
want to stop you there you just use the word probably how can you know for sure exactly what called get first that fail
see what caused song no no okay so when we ran it and it failed it had a stack Trace right so so this to me this is this
what you did is is actually pretty yeah it's pretty common that it's like this gives us exactly who called what that led
to the failure and so what you can do is is um basically back up in the stack trade so okay we know result. song well
that's where it actually threw you know that's where it actually called get first and so we need to back up further and
we basically want to skip over internal Java stuff and the next one and we can always tell because one thing you notice
in the stack Trace is the links that are to your code are in blue versus the links to Java source code jdk source code
that in sort of gray grade out and so that allows us to then jump back in the call stack within our Co code and it's
these little things that that that um this is where this is sort of you know when we look at uh experts versus novices
experts know the pattern and so so I'm I I I don't even in a sense see those other two lines in the snack trays because
they have gr outlines and they start with javab base and so I I I don't even I sort of skip processing them and and I
just see uh oh okay before result. jaaval line 41 tsv song parser and that is um uh you know when you're when you're
practicing tdd or any or just tests in general it's like read the stack trace and and get used to reading the stack
trace and reading stack traces is hard because there is a lot of information especially spring you know any framework
stack stack traces are going to be huge um and part of getting better at it is is for folks to to to to read it more and
see what's important and what's not and so becoming expert in reading stack traces is learning what to ignore and what
to what to pay attention to uh and intj helps us a bit by by by providing the Blue Links for stuff that you probably
care about and as well as uh also collapsing the the code and I wish and I think in in more recent versions they're
doing an even better job of this because um so on the left side uh no no cancel um on the pan so on the right part of
the pane the right part of the pain inside the pain where your cursor is yeah oh in the right part of the right pain
well there's no left pain there's two yeah and so in the left part of the right pan you'll see the plus signs ah there
we go those are the cold folding um what I think they do they're supposedly improving is like I don't even want to see
those two ones that start with Java base I don't even want to see those those are not relevant to me like it folded a
bunch of stuff in between there but even those two I don't want to see I want to see a jump directly from tsv song
parser right to result and I don't want to see anything in between like I think it should fold that completely away but
it but it doesn't um you could manually but that doesn't really help you in the future all right so we know that that
there on line 27 uh that's basically where it's become a convert well it's through an exception exception yeah so so
this is where this is where streams get tricky in terms of Stack traces yes technically line 27 caused the call to the
song method that caused the get first to be called but really it's it's because two lists says okay all the stuff
previously defined in the Stream now go execute because streams are um they're they're what I call terminal operations
that kick off evaluation of everything before it uh so maps are not terminal operations they're not intermediate oper
they're there're what I think they're called intermediate operations and so they don't actually do anything at runtime
they basically build up this this chain of things and then two list says oh now I got to collapse everything and execute
everything that's happened so technically yes from a runtime point of view two lists is what triggered it but really it'
s line 26 that was the problem but that'll never show up in a stack Trace because right it doesn't it doesn't get
executed as part of this right so this is the song which is right this method which is calling this yes so this is what
we want we wanted this to fail because this is now our failing test that we can now go write that if statement that you
were anxious to that you were anxious to to to write that we were anxious to write um so now now we can write the
statement we have a failing test it's failing for the right reason um uh and now we now we can do the right thing um
which is which is so I wanna I want to say this is really interesting because you and I and and I thought this as well
if we were going to write the if statement we were going to write it after line 27 right but it's too late and that's
too late um and so this is the danger of of prematurely trying to to write code without having a test is because now we
see um not just that it failed but the reason it failed like we knew it was going to fail at least I knew it was going
to fail um but I and then maybe if I had thought about it really hard we would have figured out that it would fail with
the trying to resolve the song um but now that we've seen the test fail we actually see oh it's going to fail basically
on line 26 so if we if we do it after line 27 it's too late uh and so now we have to figure out what do we do it's
certainly not going to be an if statement based on songs do we have like instead of calling song we call a method which
well maybe calling isn't 26 well we can't map it to song Right map to in fact map to song is a backwards compatibility
thing right right we we wrote this code so that it would be backwards compatible with all of our existing code but now
this is not correct and our test has shown us that this is not correct um and so what we want to do is we need to
basically store everything above 26 uh basically from 23 to 25 in an intermediate variable and then Analyze That so
extract that too yeah so we don't want to return an optional we want to evaluate whether that so what we get from there
is we get a stream of results and what we want to do is then look do any are any of these results uh failing or are all
the results passing or successful so we're extracting it to variable right yeah I think that variable is fine for now
okay so so now we have a stream um that we could look at right we could in a sense query the stream uh and if you're all
success then we can just return the what we have in the rest of the method basically map it and then and then return how
do we query well so the so the problem is is if if we uh if we query and we can do um so if we're looking for Success we
could say uh all match but really what we care about is if there's any single failure then everything's a um the success
uh the problem is is if we try to do a you know result stream do uh find first to say find me the the first failure or
or maybe any match um any match for is Success where it's false that will unfortunately consume the Stream to query the
stream without consuming it well so there is probably a way to do it collector uh and ASD mentions uh partition so there
is partition partitioning by um and that might work for partitioning yes so that that will work um let's change line uh
so let's do 26 half sorry it's going to be uh an additional part of the stream so you'll want to put it in between the
semicolon uh and we'll say dot collect yeah collect uh and then autocomplete yeah and uh uh we want it to be uh actually
I'm not sure so let's do let's do a a regular Lambda so do R and then an arrow and then Success uh and then uh have a
quick fix to change the return value the return type because it's going to be a map of something to something yeah right
so what this does is it turns and you can actually have it um change that into the method handle version where your
cursor where your oh yeah uh and so what this this does is it is is it basically partitions uh so it partitions the
stream into two lists one list matching false uh we have a list of results and one MCH one matching true so we should be
this we can this should be a true refactoring if we do instead of uh result stream.map um if we basically say result
stream. getet like that true uh we probably want that to be an upper a Boolean true yeah it it would auto box it but
it's more clear if for do that um and then you can get rid of the rest of that no um so this Returns the list of result
and so we need to uh then do the map um so actually maybe undo and maybe we deleted it I I think we might have had it
yeah so uh so we need to stick in a do stream first before the map yep yep you can reformat control L thank you I knew
it was L I just wasn't sure of this control Al so what this does is it basically pulls out give me the ones that are
matching the true uh turn it into turn that list into a stream pull out the songs now we have a list of songs and then
return a success result with those songs um we'll we'll be cleaning some of that up but this should have been a a
backwards comp compatible so the test should should still fail but all the pass this will fail differently because we'll
get uh we won't be failing anymore on the get on on the song because we're not uh we're not calling that there um and so
now we get actually a nicer failure which is just a failure of of is success so now that we've partitioned statement we
write it on 30 yeah now we test what so we might want to rename result stream um to be more clear of what that variable
is map of I think we could just say partition partition partition without the Ed oh partition yeah name good enough for
now okay unless you just want to call it pants which I'm also fine with um but we are not calling result um now we can
now let's write our if statement and we'll we'll see with our usage here what what what a better name might be so key um
false this is so terrible I mean this is so so kind of funny uh it's very weird yeah so what we're saying is if if
there's a if the part ition well is it always going to contain the key I'm actually not partition into two no matter um
ah the returned map always contains mappings for both false and true keys so contained key is insufficient Yeah we
actually want to do a partition. getet on that key uh and then see if that list is shoot um so you actually want to wrap
the code we've got below and that belongs inside the if block because that's basically saying there were no failures
false right so if there were no falses right then it must have been a su then success so that means the test should all
still pass except for the one yeah except we got to get it to compile so we need to return something else here um we can
just return null if we if you want and that will cause our current test to fail with a null pointer exception but all
other tests should pass right you want to make sure that that refactoring didn't break any yes and so it didn't so
that's good so we we figured out our our our partition get stuff correctly yeah me a compile is overrated that's some
people think so um so now now now now now finally pass so we'll want to do something similar which is we want to map
over um oh no we yeah we want to we want to uh stream over the partition but we do the get uh to get the false ones so
would it be something like this and then FSE uhuh and then instead of mapping results song we want to map the failure
message singular and then we say instead of return uh and then we want to fix the variable type so quick fix yep and
yeah yep uh let's delete the 44 and then we method read 44 oh 4 yep uh now let's create that create that oh we don't
have failure and result ah well we don't have one that takes a it and we can do the same thing we did for uh song so hit
enter and then enter and then result s yep with failure messages uh change the signature not that one that one do you
difference uh so the thing that it's Crossing at is saying what it's going to replace we don't want to replace the one
that takes a list of song because that's the success one that's the success failure right the success one we want to
change the one that took a single string and string and then we want to fix uh 29 25 oh actually you could have could
have adapted argument using collection too whoa what is that collection Singleton it's a it basically creates a list of
one so it's a very specialized version of list of uh it's totally fine I wish I wish would have a different adop adapt
message but do we want to do that it doesn't matter this is likely this is possibly going to be temporary um but it
really doesn't it doesn't matter it's they you both end up with list that are immutable and and size of one one it's
just there different ways it I guess I would go with this one if I no that would that actually is going to change
signature we don't want to change signature we want to adapt our parameter and there's only one option it so did that
fix everything why does it looks like I can't tell what color that is if you hit F2 it looks like there's errors uh
there's two of them right all oh so it's the plural yes this needs to be plural then um but why is 15 not compiling oh
because no that's a list oh because of type crud so it looks it looks like to humanize oh these are two different
parameters types right a list of song and a list of string except from the compiler standpoint these are just lists it
doesn't know the generic types that's that's so type eraser means that um the compiled bite code does not know the type
of the list that's a that's a compile time artifact that doesn't doesn't come out in the bite code and so from the bite
code point of view these are two Constructors with the same list of parameters and you can't do that and indeed uh that
does bite yes um and this is why like making it sub classes would uh would eliminate the this problem because we'd have
more um we probably want to do that sooner than I thought we would but I don't want to do it now uh so um how do we get
around it now well we get around it by by having like a bogus ARG well by basically change yeah we could do a a bogus
argument um which then gets ignored which that's one way the other the the uh yeah says instance of we could you could
do an instance of so you could grab the first item in the in the thing and say what what type are you is that you can do
um yeah because that's not type eraser stuff that's just runtime type checking um I don't that seems even wor not not
worse but just more even more Awkward um the other thing we could do yeah so we could create a proper list of songs
object um I don't want to do that either uh I want to do basically the the the smallest possible thing that will get us
there um so there there are two options either we add a bogus argument to one of them uh or we change the collection
type to one of them right whether it's a list or a set we don't care about oh right uh so I might say um let's let's
change failure message to set um although that's string that might be more dangerous let's let's make it the the songs
are are are a set because then we know by definition those are going to be unique can we just we have to manually do it
is we'll manually do it it'll be one change there and then it'll be set yeah yeah all right still got an error uh yeah
because success is taking a list of song so we can just do um can you convert to set well we can see what what course
yeah we don't want to cast um I think we can just say uh uh set up set can we say set copy what happens if we say set
dot yeah we can do set copy of because okay let's run our tests I I ran it before asking the prediction if we did
everything correctly they should all pass um but I kind of suspected uh the set would would muck up one of them and
that's probably the one um so what did it say um yeah because the order matters for those tests so they're out of order
uh I don't think I don't think we care about the order should we okay so change the test to not be con contained exactly
into a yeah to just be contained contains exactly in any because yeah uh yeah because really we don't care about the
order that they're added because eventually they'll all just be added to the to the database and the order doesn't
matter because there'll be index by theme and so order doesn't matter whereas failure messages I kind of wanted to
preserve that because there we'd want to see it sort of in order of encounter where we have we have validation errors
right so now if we run all the tests they should all pass uh that would be my expectation yes and prediction uh oh
unexpected song oh same same problem so same problem but where oh it's a different test yeah ah that's weird that why
did it not run I don't oh oh because likely because uh or changes the set does not guarantee any kind of order and so
randomness of of the hash code instance variable stuff so yeah that was basically a flaky test and we might have some of
those yeah which argues for the the bogus argument might have been safer because it would have resulted in in uh both
still being lists right but if we move quickly to but yeah we're gonna move we're GNA move pretty quickly to uh
interance approach yeah to to to two types of results yeah all right yeah good enough or uh I think think we need to say
a little more I thought so clearly I'm a little bit fuzzy today um so so basically uh parse with results returns correct
result for success and failure yep uh so we didn't actually talk about our end time but uh but if we wanted to end this
would be a good a good stopping point when when did we start nine yeah our time I could go uh a bit more maybe maybe a
quick break because I'm to sort of help rejuvenate the fuzziness I have um yeah so let's do a quick quick quick break
and then um maybe we'll we'll figure out what our next steps are and decide if we want to start on those steps or just
uh uh stop here but we'll do a little bit of of a little bit of planning sounds good all right so I'll few back so uh
our tests are passing we did a commit um so I think we um yeah let's look at let's let's open Jura we can close the the
result so I think we are doing that we probably have some refactoring to clean that code up but I think we're sort of
doing that um we're still uh so we're holding on to them but we're only doing that with our pars with result method uh
are we have not propagated the result all the way out so we still need to do that so if you look at um just the parse
method it's still assuming uh it's actually assuming you're muted ah that explains it the double mute um so the pars uh
so that's kind of uh so refactor parse with result to there and then uh have all code have uh all all caller all callers
to or all clients of of tsv method right um and is the parse refractor would that include the refactoring of results to
having I think that that's that's actually a step I think it's a I think it's just a separate step so yeah um split
result into failure y good enough planning for now I think that's good enough yeah I love it when Sprint planning takes
minutes cool well you want to dive into it a bit more for do another 20 minutes of yeah coding and uh so let's um
actually we can mark this one yeah that one that we can now that we split out the other stuff we can mark that is done
so J 52 complete all right wo so let's see what we can clean up from uh this yeah this messy yay so uh this is this is
um yeah pretty ugly pretty ugly um I added it for just for you ASD you're welcome so you can't see it because uh
streamyard doesn't propagate uh rewards redemptions um but asid's been Redeeming the celebrate oh nice um wow I I this
is this is ugly I'm I'm just not sure uh how to clean it how to clean it um because it it's it feels like there should
be some um a collector of some sort sure what do you think any thoughts from well I'm just wondering if um we're doing
our next line nope would that enable us to write pars with result cleaner no because we're still going to be um the
creete sub classes will be success and failure but we're still be returning the base class which is the result yeah um
and I'm I'm still and I'm I'm not 100% sure of how uh what what the subclasses would look like um it feels like there's
a way reduce but I'm I'm not it because it's almost like it's there's decision I mean I I mean I guess this could be
each of these could be two functions it would make it a little bit easier to read in yeah I don't I don't know there's
there's there's probably some um uh I'm not I'm I'm sort of afraid to sort of prematurely do some of this without
understanding how the subclasses are going to work uh I'm thinking would accumulating nicer yeah I'm I'm not sure I feel
like we we would almost want like a custom collector that's similar to partitioning by and this is this is where uh if
you look at some of the implementations of an either uh or result like thing that people have written um it ends up
getting pretty pretty hairy in terms of uh things to to solve exactly sort of this problem of how do you how do you
stream how do you do a stream Where in a sense collapse like the the minute you hit uh a failure you sort of want to
toss away any any successes that you've had and then just accumulate only the failures um but if there are no failures
and you want all the successes and so it's not it's sort of an asymmetrical thing who would have thought the the parsing
would be gnarly well it's never the the not the actual parsing it's not the actual parsing that's the problem it's it's
it's handling failures and that's that's to me that's always the the more interesting part um true because it's it's
there's there's more there's more going on it's not just case so I'm not I'm not coming up with any anything that um I'm
not coming up with anything useful like we could do some straightforward refactoring of just you know extract 29 the
expression and uh and then extract the the part that the list of results into the success instead of passing and song so
there's some Su there um and that might then lead us to well then then that then this then we basically be pushing stuff
into into result so we'd be pushing the um sort of the collection of songs or collection of failure messages from the
results there's yeah that's that's the another thing I of uh Astro you're talking about the the potential two subclasses
or not sure what you mean by what two classes do we so what are your what are your thoughts I'm actually a little bit I
mean yeah clearly we could do the cleanup of 29 you know having a more descriptive name collecting up the the body of
the two if statements into a method each into their own method the thing I'm focusing on the moment though is that so
the fact that we say on 31 sorry on 29 if partition false is empty oh right because it partitions into two one where the
Boolean is false and one where it's true right Boolean false means success well Boolean false being empty means there
are no failures so we're basically that's why you know the first thing we might want to do let's just do it yeah since
you had had to think about it quite a bit is let's let's extract that right so we're currently using the um the results
success uh the failures are going to be used once we basically do Jura uh 57 um and we start propagating the failures
out to the to the UI so we do have a need for it uh we just haven't yet would having the need for it creating a test for
that I don't think that would help because we're already returning result here and we know what that looks like um it's
really more the internals of of pars with with result all right uh we would start with a test if we were working on that
jur but we're currently working on just a refactor of this method so we're not looking to Behavior there's no way to
functionalize this I mean because it's 31's different they're probably is it's just isn't worth it is really the
question right and then 33 is different what it's being passed into the two no but one returns a list of songs one
returns a list of failure messages yeah so so you you could extract that including 35 into a method and then
parameterize uh things uh um not sure that would help yeah I'm not sure it does either and plus this is Success this is
failure well right we'd have to move um uh we'd have to create some more General method in results that just takes a
list of results and then resolves to either a failure so you think value at least in just creating these this is a
method sort of abstracting it away a hideous or do you think it's going to hide things that we'll need to later better I
think we can we can extract that and parameterize it and see what like partition uh I would just say map to doing would
you leave the from or no keystroke uh map to messages that work yeah you think it's worth inlining these complicated I
guess we could try it and see what we think and go undo it if we it uh you're thinking about something else I I don't I
don't like I don't like inlining those I mean you could do it to see what it looks like but I'm pretty that because it's
valuable to know that songs I it it feels like it's just yeah wait okay all right uh I think that's as probably as far
as I i' I'd go at this point um I mean we could do an inline on on 38 and just return those directly and probably the
same for the other one oh I see 47 well let's rerun the test even though everything was automated yep and then commit uh
yes definitely want to commit uh let's run all the tests right good enough yep yep they a commit and push yeah since we'
re y so for tomorrow I think it'll have to be a hard stop for me at the twoh hour yes everything passed all right great
sweet all right so thanks for hanging out with us everyone uh and we will uh pick it up tomorrow 10: a.m. start time so
one hour later than than we did today uh 10 amm start time Pacific time which is 6 PM UTC uh and we'll um maybe we'll
have some better ideas about refactoring otherwise we'll uh continue with with uh starting to propagate now that we've
we've basically made the success stuff backwards compatible because that's what we've always done but now um we'll want
to propagate the failures to to the to the front end uh and be able to take those failure messages and display them
instead of just throwing an ugly error page should we add that to our jir prop or is that already covered by that's
already in there have all the clients yeah that's that's use okay yeah yeah all right that's all folks thanks for
joining us and uh we'll see you everyone
