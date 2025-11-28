# ＂Song Themes＂ Episode 26： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=_UVD4fZzOFw

---

## Transcript

hey so what's up Mike what are we doing what's going on oh nothing much it's been like a while what was it like a week
or two ago let's see the 207 I guess it was last week not too bad yeah yeah last week um yeah doing well uh trying to
get caught up on stuff the nature of my life I think probably gonna maybe even get to uh persisting the database today I
don't know we'll see I don't know I keep I keep saying that and I and and it and it doesn't happen so I'm like I'm not
that requires estimating and prediction and uh I'm just going to stop doing that uh so should we look at should we look
at jir sure let's look at jir all right switch over to j. txt files for new viewers yeah so looks like we left the
breadcrumb at jir 72 right so um yeah so we finished converting uh our exception that we were throwing for what was
really a validation failure um and I have a pending article on basically uh result versus exception and I've been sort
of reading a bunch of or re reading and rereading a bunch of articles about guidance on exceptions in Java um especially
checked exceptions and uh uh it's really it's it's just interesting how um Frameworks like spring and so on basically
made the decision we're not going to expose checked exceptions but there's still exceptions um but figuring out uh so
the the heuristic uh I've also been thinking a lot about heuristics and mental models um heuristic here for me is if it'
s sort of input from somewhere outside the system that's outside of our control then that's really validation and we
probably want uh to not throw an exception and to use some kind of result cost um which does require a little bit of
work and uh to do and to build um and uh but databases are different like if we fully control a database I would not
expect any validation problems like if I load an object it should just work and if it doesn't that's actually an
exception um if it's a shared database then all bets are off and problems so hey swegi welcome um anyway so that's the
that's the her ristic uh and uh hopefully I'll get a chance to expand on on that in an article and maybe a video but
certainly an article but one of the things we've been doing um maybe load up uh one of our t test that that asserts
against the result one that one's fine so one of the things that that we're we're doing is of course asserting on our
result that if it's you know in this case it should be successful um and that there should be no failure messages uh but
if this fails so one of the things that I've started doing more um mainly because I'm trying to get better error
messages is for example if that assertion on 62 fails all you get uh is basically an an assert error saying true is not
false it's like great why why do we expect that now you could look at the test and it's pretty obvious um but it's
especially when you're getting multiple test failures it's nice to be able to yeah we did it in in in this case here um
but one of the things about assertj which is the assertion Library we're using is uh that we can write custom assertions
um and a first step would be well we're we're constantly doing these assertions like on on is success and so one of the
things we want to do in our in our test code like we do in our regular code is raise raise the level of abstraction so
um probably the first step would be to uh uh to so what we might want is something like assert that result is Success
right where the is success is the actual assertion uh method um rather than than just checking a Boolean and seeing if
it's if it's true or not and that will certainly help because somewhere we we assert that is success is false and that's
just hard to read like I know from for me uh if you just just search for like an is false I'm s sure we have yeah so
that's that's a little hard to read right it's like assert that is success is false wait does that what does that mean
oh it means failure um what we'd like is assert that result is failure uh so these are the the little things that we can
do in our code uh in our test code to make it that much easier to read as as write so should we start working on on this
then yeah so we're going to write a that so let's see this is the custom assert that works for are we customizing the
assert that library or yeah so we'll we'll create a custom class but we're gonna we're gonna take some some small steps
towards that yeah but eventually it'll be assert that song result and then um the other nice thing is we'll be able to
collapse both of these separate asserts into something like assert that song result is failure and has failure messages
contains exactly uh and so it basically be one nicer fluent uh more domain domain specific uh or at least specific to
the the result domain um and so that that'll be nice yesil successfully um let's let's run our test make sure that we're
in a good State before we do anything else yeah let's do all just done that yeah and I did notice they commented out
disabled which I thought was weird yes I saw that too uh I was like how did we must we must have commented out and yeah
there it is yeah and all the tests pass switching back to io3 let's delete that and then do we need the common on 52 as
well does it I don't think that makes sense anymore because yeah because there not that's a huh comments out of sync
with code that never that never happens yeah now I'm like scanning is there any other like crunk junk lying around
number of coms and hit or match I think we can delete all those we either have test or or pending test for for or we
have jurors for that so yeah yeah sweet all right uh do you want to do a quick commit just to say removes something the
from code was redundant but the office of redundant redundancy required me that's that's a very chat GPT thing it's
verbose did you hear about this one trick this professor was using to catch his students using chat GPT I don't know
heard this I've heard of a bunch of Tricks which one is oh you have this one was embedding um some absurd text in the
question right but making it white text on white background so they won't see it but if they copy and paste right in the
chat GPT it starts giving crazy stuff about bananas and applesauce yeah on a question of related to I don't know
political history or something right right it's funny that was that was the old way you used to um what was called spam
dexing um where you'd put white text on a white background with basically just you know have hundreds of keywords on a
page so you people wouldn't see it but Google and the other search engin would see it and then bump the U priority of
the page like oh it's got this keyword word a lot um because it's all you know it's always the battle the battle of of
of you know it's basically cat Mouse it's like you know we'll do this it's like oh we'll look out for that okay then
we'll change it to do this and oh we'll look out for that never ending battle should we just use the first test in this
one to yeah I think that's um or do you want one that has the as uh we could do one with an as or we could do um start
with success is a yeah I guess simpler to start is probably yeah this is sort of the um yeah so let's let's start by
extracting 56 and 57 uh actually extract to a static do I we extract and then make it static or do we need to do the
popup version well um actually I don't think it matters I I just usually do it with static but it won't matter I think
what what do we want to say um so where we want to get to is where we have an assert that that takes a result object and
this one would success let's try that um I think uh it'll become more clear yeah because that I think that's fine yeah
and should we replace all or just yeah we should we should replace all what do you think the static and see if it it
should be shouldn't be different but I'm not seeing any intense variables being used so I think so so let's think a
little bit about what our destination is our destination is is we want an assert class uh um object yeah so maybe let's
let's sketch it out so we want uh a Constructor that takes the result object and then a success and so how do we get
there from I so if we extract this to a CL or move it to a class it's still taking the result object is there a way to
then move the parameter of is success to the parameter of the construction yeah manual hack well I think there's going
to be a manual step but then I think we can use another one so if we create a result assert class with a Constructor
that takes method and push it out and then we can move this method over so manually yeah so let's let's create a a a
result assert class yeah and where would we put that clearing the test World um so I'd put it sort of in the same
package that result is in right because this is testing result which must be which I'm not searching so uh no because
you're looking in the test and so it's not going to appear there actually I could just hover over this guy yeah so
application that makes sense yeah uh some questions in the chat uh so uh how can I determine whether to focus on unit
tests for specific functions or integration um so this is an interesting question uh you're GNA at least my my strategy
is I'm always focused on on unit tests but always thinking about integration um and I think sui's advice uh which I
which is for me Echoes Kent Beck's advice which is what what are you nervous about what are you anxious about um but
there's this uh I don't know I see it a lot where where people I think get caught up in well if I'm doing unit test I'm
not doing integration tests like no you should do both so I think the idea of focusing on one versus the other um as
long as you're not saying exclusively focus on unit tests um then uh you want to to to fully test an a class that should
have behavior and should have constraints and should have allowable States and and not allowable States um you test that
and then you have then you want to you know and I think people get confused in integration which is why I've switched to
to to calling it IO uh based and IO free um you can have classes that work together right so we've got our um we've got
a song class and we've got a uh the song parser song Searcher and all these work together but they're none of them are
doing IO uh and they're just so they're just sociable tests and so you're going to unit test them even though multiple
classes are involved multiple objects are involved you know and it's like is that unit or integration and I basically
say it's it doesn't matter um what matters is is that you're testing things working together and those are associable
tests um and so where Universe integration comes for me is uh are we dealing with the outside world are we dealing with
with API calls are we dealing with databases are we dealing with Hardware like getting the clock uh that's where we
would use test doubles to help us write write those tests and so um in terms of determining what to focus on if you're
especially you know depends on if you're doing test first or not if you're doing test first then it's what Behavior do I
want and then where at what level am I observing parel looks like Ted might have Frozen there uh y that was weird am I
back yeah you are back okay that was weird I don't see any was it just me everyone could be my internet con it could be
my inter connection it looked like streamyard was was was causing some problems or noticing some problems anyway uh long
story is short if you're doing test first then you want to figure out what are you testing and this is where outside in
I think is useful you start with what do the API need or what ises the UI need uh and then you follow down from there if
you're writing test after gets a little bit harder because you got to figure out what are you testing um are you testing
the code you just wrote where did you write that code what does it use so um there's there's a lot of it depends at that
point hopefully that gives you a bit of a bit of a guidance so yeah so let's create our result ater and it's a class uh
yeah it's class uh let's go ahead and and before we create the Constructor we want to actually do an ex so here we want
to extend the um the abstract assert extend is this can uh we don't want to no we want to extend abstract uh yeah
abstract assert that's what we want Even though that's the oh uh and let's go ahead and and Implement for right so
that's what I that's what I expected um so so we want to generif abstract orer so we want to give it uh so undo that
part because we're going to want to generif it and then regenerate The Constructor so abstract assert um no on the
abstract assert part because we're basically going to say there so there are two types that are are needed here one is
um result no sorry self is result assert result yeah and now let's Implement that yeah right so what happens here um and
I think uh so this so this a search a if you if you look at its code it's like it pushes um it pushes generics and and
and stuff like that to the to the edge in order to get a fluent interface um and so uh what we want is we don't want the
caller to this Constructor um to have to to specify the self type because the self type basically there there are two
types say what are you what are you asserting on and what is the assertion class itself and what happens with the fluent
API is you're constantly returning itself because it has the knowledge of what you're asserting against and so that's
where we'll be able to say is success and then failure messages and and things like that so is there like a factory
method or static that create no so what we'll do is is basically uh change self type on line eight to literally be
ourselves class and then we can remove self type from The Constructor and we can make you can just just manually do that
or no have it do it it's not used yeah so Alt Enter oh right Alt Enter yep sweet uh and then there's no reason for this
to be protected we can make that public in fact we kind of want it to be yeah I was wondering about that I'm not sure
why it did protected interesting so so what this does is now when we create a result assert we give it a result and then
we'll be able to uh to do some some method on so yeah so we can go go back here is this was it here uh I thought it was
yes okay do you see it um uh no I e yeah it was that file okay it was that okay um so just search for the the method I
think we called it yeah unfor it's got the same name as yeah there we go there it is so what we want to do now is um
extract result uh there on 63 into a local variable which seems weird but let's try it um stick with result one for now
because we're gonna get rid of it anyway let's see do we need to do this uh oh maybe we don't need to do this uh let's
let's not do it and see what happens so what we want to do is on line 62 and a assert and we'll give it the result and
then we'll hold on to that yep sure now do we want to push it out as a do yes so let's push out uh let's introduce
parameter from of result assert of yep uh let's just check on one of the callers and see what that looks like colors of
a success yeah yeah right up above 56 oh right there okay great perfect so what we're going to do now is um now this is
feature Envy even though it doesn't quite look fully like it um what we're going to do is we're going to use now move
method so F6 all right and where's it going to go it's assert because it's pretty good yes so what it does is it looks
at uh the parameters it does two things it looks at parameters and it looks at contents of the method for references to
Fields um there are no Fields here because this is a test or at least this test has no Fields uh and the only one that's
sort of reasonable to move to is is result assert and so we just get one factor so now what we see on 56 is new results
CT right is Success now result is going to be redundant we're going to get rid of that but right now um our test should
still pass because basically that we created the object and it was a no op yeah where were we here yeah so now um yeah
um and now what we can do is replace on actual so actual comes from the Base Class the ract assert so when we did on
line 11 when we did Super result um it saved off the result and calls it actual um so now uh to answer sui's query um no
we get rid of we I mean could we' have gotten rid of it before no because we need to replace it with with actual um so
that's why we did it in this order so I'll delete yeah so now we can now we can do a safe delete safe to wa one so now
we got new result assert result is Success um so now you can put line and so that gets us right so now we've got a
result assert and that reads much more nicely uh so now we have two directions we can go one is um make assert that work
for for a result assert uh the other is is to to to start slurping in other other assertions like the one one below it
so the assert that would get rid of the new correct and basically it would be it would become a static method on the
result assert I'm GNA move this down here I know it's test code but just so we can see both sure hello Jonas so we're
gonna We would or uh so what we so if if we want to go the assert that route and that's fine that's uh what we need to
do is in the result assert class we need to do two things one is provide a static Factory method for a new assert that
method so um let's grab go ahead you said if we want to go this route what is the other route that the other route is
just start slurping in Failure messages and other assertions that we want to do on our result assert but we may as well
get the assert that out of the way it's pretty easy okay cool uh so let's extract the newer result assert on the 56 so
the whole the whole result of that extract to a method through the method or to it uh so just just 56 so just the the
creation of the result assert okay extract to method to to a method yes uh and we'd like that to be a static method um
but we're going to call we're going to call this that and yes we want to replace all duplicates uh and because it didn't
um because you're not using the modal it didn't pop up let's go to the that um let's make it static did you actually I'm
forgetting Java static before private or after uh it's after okay uh and so let's now move this assert uh I think You'
hit F6 on the wrong thing you want to put on the method yeah I did the right thing otherwise it tries to move the class
yeah yeah fully qualified name this one would be so there result assert and let it autocomplete refactor so now um we've
got some errors because uh we're um we're our result assert is getting confused so there's one more thing we need to do
which is in our uh result assert uh definition so where we Define the um uh oh we moved this to the to the wrong class
my my bad um so do this uh do yeah let's undo it because otherwise fix uh sorry I forgot the the assertions need to be
in a separate class we're going to take the assert that still move it but we're going to move it to a new class got it
we still have the failure here should we yeah yeah yeah that's that that'll be fixed once we finish the the uh assert
that move on line 64 let's method and so um type result assert so to let auto complete yeah and then we're g to change
the class name uh and we're gonna add uh uh to make it result assertions so I O refactor and yes we want to create it
there assertions the Jupiter one no one of course de and so now uh we should be back to compiling yeah run the test yeah
run the tests then delete that common end 14 and their result is search yeah we're yeah uh and so now the last step is
um currently we're importing uh result is we're we're not we're we're if we go up to our Imports there's probably the
assertions being remove because we're now using our new result assertion all the time uh and now what we can do is we
can go to one of the calls and uh have it import static on that so I think if you could do an that uh on demand static
import yeah oh it was there I didn't see it it was yeah second option ah so that'll basically do a static import like we
had before but instead of using the default Asser a one we're going to pull in ours but we get all of the other ones
because our assertions extends their assertions but now it recognizes uh assert that that takes a result so if you look
for um one of the factored yeah so now there on line 57 we see assert that result is success that's what we want uh can
you hit escape to UNH you and so indented driving me crazy yeah so just do a reformat yeah alt L I'm right yes good yep
so now we have assert that result and for anything that does is Success that that works fine so then the next thing is
to pull in Failure message as part of the success yes or we can pull in uh is failure because we have a bunch of those
that might that might be a a good Next Step one so we want to move it we want it to do the refactoring steps if we can
to Move It from move this rough logic to results assert yeah so let why don't you sketch in comments what what it should
look like in in place oh in in this place yeah at the Target twice so what is the use use site what would what do we
want it to look like yeah I'm going to steal this oh the something along these lines is what I'm thinking right now this
one doesn't have a message the one above but in this case we would probably want well let's not let's not since there's
no message in what we're replacing let's not add in yeah yeah what we don't need yet right so if that's what we want to
look like what might be a step to get it to get is we could uh inline just one occurrence of EX success to here and then
extract it out then extract the whole thing to a method and work so give me those steps again so I was thinking like
here for is Success inline this into that spot well you can't inline that because we're not calling that method right
it's calling the other it's calling the it's calling is directly on yeah well before we did something along the lines of
extract this to a method and then did some intermediate steps that I forget and then moved it over to uh the result
assert class do we need to do something with assertions no that's fine because that's that's that's the general uh that'
s that's basically our way of of of making assert that compatible with our new with our new assertion so you you can
probably even close we we haven't quite fully generified it but you can just okay so suiga mentions you could inline
assert that not sure where that would get us uh I assume you mean this this assert so that assert that would inline IC
method we could try that see what that looks only so we make yeah I guess if we made this a method and then part not
sure that'll work though but yeah I'm not sure there's a direct way to to do that because we don't have I mean we could
let's undo that um can we just clone this make a new one yeah I mean you know so so what I you know you know me I I
always like to try and figure out is there a way to get there uh through automated refactorings right um the normal Pro
the the process we used before right extract that assert that to a static method uh introduce the the variable um it's
harder here because there's no field that represents uh the result assertion uh the result assert instance so if we
right so if we extract this make it static there's nothing in it that that allows us to move it into result result no
because that's part of the definition of of of the types that's not that's not in the in the hierarchy new if we do a
new assert that we don't Constructor there might be a way but it's probably not not worth it at this point um all right
asterid have a good night good night I guess it's I guess night so I think what we want to do is uh let's pretend we
have the method that it so basically what you what you had what you sketched out above and then let's uh oh you're GNA
say something let's pretty much um yeah actually you can delete it so yeah go ahead create create that cannot find yeah
so let's create it manually you mean uh option enter and create the method ah okay yeah I did the wrong click that was
the issue yeah and then um you can probably you can copy the 15 and 16 and just or just false hold a second control
contr shift J no no that's Jo Jay's for join Jay's for join oh right right right but isn't what is the completion don't
tell me I'm gon look at my list oh control shift enter yes that one I need to practice on and not do it in my notebook
there we go all right now we to this yes and if pass the downside of this is it doesn't automatically change all the
other tests correct and that's one of the advantages of trying to find an automated refactoring yeah so it may still be
worth it to um to find other usages of our uh is false extract those to a method do the right thing and then inline it
all to sort of spread out the the second so that's the so besides taking uh besides saving us time that's the advantage
of the duplicates I wonder if that enough yeah so let's find another one uh false yeah so what we can do is we can yeah
uh and we'll just call it um temp or applesauce or pants whatever you want pants that's a good one pants um that's
interesting is that the only usage is there no other is false called oh oh that was a wrong click um it's false oh the
other ones take a message uh is that it though is there any other at least within this class oh okay uh so that's it
there just two usages in this class yeah oh there only two all right uh then let's undo that because it's not worth it
wrong okay there now there's the other one but yeah so let's let's take a look at uh we can start with either one either
the success or failure one of the ones that that uh does the As and then we'll push that into into our results assert
okay there's one um I think that's generic enough that uh we should pretty much just just move that um think I'm not
grocking what you're saying uh so maybe that was a thought not an instruction um it was clearly not a precise enough
instruction uh so let's 42 and uh paste it on uh 20 and a half bottom ah I see uh and then let's replace 41 with um is
failure instead of the whole first AES I don't know why that just was funny to me um that's under yeah that's under
values there's a success but we're currently dealing with failure success so um we've Zed around so let's so let's find
all of the isru and correct there's two of them wait a second um can we run the test I feel like this is failure is
going to break because there's more than one is failure right and they didn't all test for the same message so this
message is not part of any kind of assertion it's just what we fails so that's why I was confident as as a cut and paste
got it because it's not affecting any any anything other than when it does fail uh we'll see the message if you want to
see it we can go and just put a bang in front of actual 20 and now it should display that that message all the time and
that message is valid in all those situations yeah because basically should have succeeded right but you know yeah yeah
should should not have exceeded but it did yeah okay so back to the is Tru so we want to replace uh we want to keep the
as where it is um because there because it's custom for this specific test uh but we want to drop the is Success
basically move move the is Success from from there to true yeah no more is truth all right there's still that's it's
failure but is there any and falses uh oh there's no more is falses okay yeah that's right we covered them all all right
I think uh as long past right um that good enough or do you want more or different NOP perfect great shiing all right uh
there was a question that X proof asked before hey X proof have I ever had to version my apis due to break changes in my
code um I don't like versioning apis uh sometimes you have to um but I prefer uh making sure that the apis so my IP is I
haven't had to do that I basically uh add new Fields um and then uh because versioning is is pretty tricky uh but you
know sometimes you have to do that um as a last resort uh I'll I'll version them but you only need to version things if
you remove stuff so apis can grow you can add Fields uh and doesn't break any back of compatibility if you're providing
more information to to someone um if it does that's their fault they shouldn't blow up because there's more information
than they expected um but you know some times if you're I I I feel like it's it's often not versioning that you want to
do you basically if it's breaking changes that means you're changing behavior and maybe you want just a different Endo
uh so I prefer I guess in a sense a semantic truly semantic in that I'm using a different term for the API uh perhaps
even a different uh basically a different resource um for for what you want to do if it's really a breaking change
because that means it's different it's not just different data it's different behavior um but overall it's again one of
those it depends on the concrete with all right um I think there's a little bit of cleanup we need to do for our Sur
before we add uh um before we add uh before we move the other other methods uh one is right now on seven we need need to
generif our result mark because we don't know I don't think is uh result assert might itself need to be generified by
that term but we now uh so Su man said don't use raw arrays for for your requests yeah so I've seen it I've seen places
that you make a call and you get this array right the first thing you see is like a square bracket and that's terrible
um I'm not sure if that's what what suija means but I've seen that it's like no everything should be name value Pairs
arrays uh okay so um now we want to work on um our other assertions that we're result just go top down and test their
using result uh no I think we should just go into through our test and uh that we were in and continue um oh within this
one collapsing stuff so uh so here we have on 173 that we're checking that the values contain exactly um so this is
going to be interesting because there's going to be values um uh there's going to be value so is Success what what would
we like that to look like we'd like to say assert that success we could just say values do we want to say something else
meaning like what would be the yeah we then just say values and then uh well values would return a uh a collection
assert and then we would just be able to use the standard stuff so it be like this then can change exactly yeah
something like that that create oh interesting because is Success yeah I think we could do not what does that mean
replace with qualifier it might be confused because you added the the contains exact why now huh that's interesting uh
is is Success not a void is success is that's why so let's make is Success return self in fact in general we should be
uh doing that yeah I was wondering why they were returning void because we didn't need them to return anything else um
so these should these should all be uh um uh uh result assert basically return it no no autocomplete won't work because
it's going to try to autocomplete it in value failure and uh let's make is Success public just so we don't all just be
public when we did the extract and move we didn't we didn't tell it to make it public gotcha I didn't noce it all right
so now um now we should be able to create that method yeah Yes actually let's um let's see if it's if it if it changes
the way it does this uh so let's copy and were you piing this yeah let's see ah did sort of was uh returns values it
returns kind of not quite what we want but at least it has a I'm not sure if that's actually helpful um let's let's not
do that okay you can comment it out though or delete it whatever uh so let's create it um what we actually wanted to
return uh uh elections success right but what we want to be assertion because we're going to then want to call contains
exactly so uh can you click on 176 there on the top uh where does that come it so what are we in we're in abstract
itable assert um that's not going to be good enough for that uh oh collection assert okay great so we can close this
file uh and what we want is where we created values we want the return type in void instead of void to be uh collection
assert uh and furthermore we want it to be collection assert of what did we say these are um mean over here yeah yes ah
okay so here's where we have to generif but what are we using right now we're using song so let's do song and then we'll
later got it okay so back to result assert the new void so you're saying right and so now what we do is we basically
manufacture this collection assert handing in uh the results values so we can do return new values so is it actual
actual dot values oh dot values right because we're basically saying here is an assertion class uh on should This Be
song Here Yeah it may uh right because because we haven't generified because it doesn't know what values contains
because we haven't generified it so let's let's go fix that um let's go to that question mark we put in in our class
header in our class definition here uh let's change the song so that'll concretize it and so now it knows then you don't
need the one on 29 right because when we call actual values because we said question mark we were saying that uh we don'
t actually know what kind of values this concrete um now we should be able to uncomment top pass and if we want to see
it fail why don't we change on 174 let's change one characters there we go now here's where we could start getting
really fancy um and make the stuff easier to read because right now in a sense we're still calling we're falling back to
sort of the generic contains exactly um we could get fancier and say uh you know values contains song or something like
that but um I think that's probably more than we point all right let's change it back and so uh sui had a a nice
suggestion um to display something like that uh if the is Success fails and I like that um but before we do anything
else do we want to take a break yeah probably should yeah so we'll take a break when we come back uh we'll Implement s's
suggestion and then we'll um we should be able to change all the other is Success contain stuff to use our new values
method and then we'll continue with that so I'll take what a up where is my is for so some of you may know that I have
uh a game to help you get to know and and learn about uh test driven development called Jitter teds tdd game and this is
a picture of a bunch of us playing the game at the agile open Northwest coup weeks ago and um people had fun we we
played this several times with um probably close to 20 people and everybody had fun everybody learned something oops
that was loud um and uh we I've been proposing this at at various conferences and it's been played uh by probably
hundreds of folks around the world um so encourage you to take a look at if you go to td. cards you'll um and uh if you
got tdd cards you'll see this there's a video um so a few weeks ago maybe a month ago by now uh on the agile lyion learn
I did uh a walkthr of predictive test driven development so basically what we do here on on stream uh and then walk
through the game and and and talk about that so currently have uh not that many copies left in stock so if you want one
um I ship internationally go ahead and go to td. cards and you can order today and it ships out pretty quickly assuming
I right uh sui's suggestion um now the only problem with putting our own failure message here is that it would override
any callar description change so for example on the top there fails and we put an as in our result assert at the one can
we do a can we do uh a check um can we change uh uh on line 16 at the it and then let's run no no don't run oh sorry I
know that the Rhythm yeah uh because basically I just want to run the one test there uh on line 186 whatever that test
is I know it's going to fail but I want is okay so we lost the F so that's what I was concerned about um and we need to
fix that uh does this have to be after a success Well it can't be um because the as basically says Hey when it fails oh
this is a message um and there's something about uh the way the as um see what do the docs say see oh so it so it
returns a new described as um yeah let's jump into that as well let's just let's just keep jumping until we get to a
yeah keep jumping or this is the well uh we're now in describle so we're now in an interface um so uh back one no I
don't I don't think this is going to help us I think we need to look at some concrete assertions um so as call described
as which does that uh wonder if it's the condition it I wonder if we're actually um No actually that's fine uh no let's
let's close all all these um I'm GNA have to this is a bit a part that's sort of a bit underdocumented in terms
undocumented versus how to use it or how it's implemented well undocumented in terms of how to handle the specific
situation uh so let's look look look Custom Custom assert examples let's look at it like employee sir you do a look a
yeah yeah so we've been delegating so what happens is is um we have been delegating in a sense to the the default
Boolean assert um but at that point the one that sort of captured the description message is our class but then when we
delegate it to this other one it uses its own and so it's lost um it's lost that so I think we need to be a little bit
more manual in terms of uh work um so where we actually generate the the message ourself um instead of relying on on the
Boolean assert uh and then have a message uh where we can where where basically we do the check instead of basically
instead of delegating to somebody else's assert we write in a sense write it from scratch so I think this is the way we
should go okay um because this will give this more uh more control over the message and um then I think we can can
capture uh then I think we can use the message if it's def finded um if not we can replace it with one of our own all
right so let's switch back to you screen okay so let's modify our uh first of all let's fix our um let's let's undo our
change on line bottom my mouse just got weird there we go nope so what we want to do is instead of sort of delegating to
assert that we're going to write this manually so um uh on 15 and a half we're basically going to say uh is not null
we're going to call a method is not null yeah okay so what that does is it ensures that actual is is not null so somehow
actual no no you don't need to do anything else it it just does it all all for us okay then then what we want to do is
um instead of uh instead of 18 and 19 so let's let's um delete 18 and 19 okay is there value in commenting them out will
we need some of those or no no okay Success when you say not actual you mean bang actual yes okay so basically if it's
not success then what we're going to message uh so the first parameter I believe is a message um can you have it dis can
you display parameters Yeah so basically it's an error message and then uh and then the message um but let's let's let's
do something simpler okay um let's just booleans so can we go up to the super class fate of what we're in this one yeah
because I'm trying to figure out where stored uh no no no don't search for anything um so I think info is what we want
uh can you scroll down a bit Yeah so we get is um uh we get appropriately let's try that because basically that's what
the Boolean assert does so let's let's sort of emulate that so um instead of uh so let's let's let's take a step 19 and
we're going to Leverage The Boolean asserts that are already there so let's new uh sorry booleans do instance so
uppercase B one uh the second one no oh that one okay yeah uh do instance and then actual sorry first info and then
actual true let's and uh let's um let's go up to the to the test top um I'd like to see this fail uh can we success and
let's just run this test so we're looking for is to see what is what does it do when it when it B fails okay so that's
the default the default message um let's put an as up up above line 22 so 22 and a half say as this shouldn't fail or
just some okay so now we've we've preserved the as message if there is changes uh and let's um let's run all the tests
just to make sure we're we're back at a good State you want to do it yeah all yeah free cool all right uh so let's go
back to our bottom so um so here what what we're doing is we're basically uh saying use this info which is BAS which is
the the error message um or the description the default description if there is one uh if we want if we want to display
our own message um then I think we'd have to look at if info is there or not but I I feel like I don't want to do that
right now I want to fix up his failure to emulate what we've got here um there's the other thing we want to do is is uh
sort of the the idiom and I'm I'm blanking on why they want to do this uh but instead of returning this we returned
myself on line 19 really just the word myself yes because it is an inherited variable and I think it's because it has it
okay uh and let's put put some empty lines between uh so 17 and a half and above 19 just to separate out the sections I
see wait a second you mean like this yes got it all right and then let's make a similar change to to uh is failure on 24
can you hit escape to turn off the be be oh right comma false correct and then the only thing that's weird is we here we
yeah yeah so let's let's comment out that assert assert that block um let's return myself and great so in this casee we
wanted to have an as within our custom result assert correct so it' be some sort call uh I think we can just call
described yeah now who run the tests well we won't see it so we need to see we got to force failure it's not the best
test to force a failure in what about this change no no just change the line 28 to True oh here yeah and then when we
run them we'll see at least three three fail tests right but we'll see the the okay um there's probably a way that we
can uh check to see if there already is a description before we we overwrite it uh but I think right now we're not going
to worry about that we're not using um should we put a little breadcrumb here for us if we're ever like hey how come our
as is not showing well our as uh um on failure right now yeah uh that's good good question we had four of them but we
haven't even gotten to the incorporate I'm not seeing anywh we're failure yeah let's let's put in a a comment above
above the method and say that yeah I might put a big warning uh it yeah uh do you want to turn that into a a a block
comment so it actually comes up in uh when we do an an F1 on it oh interesting um how do you convert to is it manual or
is there a way to say uh I don't know you can so you can always do Alt Enter and see what it suggests oh uh replace with
Java do comment oh Java do or block no Java do ah okay um you don't need to say it's failure you can just say this
currently because it's documenting his failure yep so now if you do an F you know a help what is it control Q on it that
y okay good to know all right um it just show Java do help or is that um all help well I guess it is only possible
implement it through Java do yeah the control Q okay yeah uh so let's run all our tests make sure we're back at
everything passing uh and then we'll commit and I think the main thing we did convert uh or uh customer CT uh no longer
messages that's true for success but not J no we've done it now for both right because they're both now using the
Boolean instance assert equal no but oh I see what you're saying um that's true right so only for for the is Success
actually yeah I'm gonna have to search through enough okay uh so let's so where are we uh so we did the success messages
let's do the failure messages so where we are is actually a be um so what would we like this to look like I think we'd
like it to look like uh is messages versus failure messages yeah because I think it's it's clear in context that is
failure messages contains exactly I think that will be that will be clear okay um so let's go ahead and uh Implement
that yep so this is going to return also a return similar to above but with the right there we go right yep and then we
should be able to delete there no the other line 25 just yeah so faill uh I think we again we can uh since it's a
failure message I think we uh we would just change the contains 25 oh I'm not sure I know what you mean so change the
message that we're expecting on line 25 oh what do oh to be something different yeah got it right because this is a
failure right right right we're not gonna for that's the that's the hard coded message we you know we give it right and
now it doesn't doesn't have that so now we know it's falling into this this assertion so now pass cool so now do we
search out the other is failures oh there isn't oh no bad do we not check other no it's my badp yeah okay um oh
interesting so this one's got that should just work but that should just work because has size is on our our collection
ofert uh so so we should be able to replace everything from line 41 the semicolon through the end of line 42 I don't
know if that appears anywhere else yeah uh no sorry undo um see if you if there any other instances of that now so
reselect what you had okay from here to to the end to there okay yeah and now do uh control search and then uh so there
are two instance of two instances of it yeah so turn that into a replace so hit the whatever keystroke to do replace
that one in my sure top my head I'm going to assume it's control R yep all uh no that that's couldn't have been right oh
I see what it did okay never mind so undo that because in this case it's not um looking at the it's not off of the
failure so there was only that one right yeah so you can go back up to the previous one and and just delete it hit the
so I noticed that you don't use your end key to move to the end of a like no it didn't work um oh I know why it didn't
work I still had the control going so if I go to here then end so if you hold down the shift key and press end ah shift
I had control down so that's that's much much faster than trying to to word your way across and and and um these you
know these little things I I notic a lot of folks don't use their home and end Keys um and I understand on Mac why
that's the case is because the Mac makes it actually really difficult to type those uh if you're working on like a a
laptop because you have to hold down an FN key in order to and then figure out and remember which key is representative
of that uh but if you're using a keyboard and I think most Windows laptops as well have an actual separate End Key um
it's uh it's it's one that's saves saves a lot of time uh so we want to add in we actually want to replace that with um
messages cool excuse me oh here's a different one oh it's probably because we're not consistent in our use of whatever
variable name we're asserting on yes that's what so you can do the same thing replace the the semicolon through the
again end NOP no shift so shift is your select key so holding down shift means you will no this one yeah so shift new
line and okay that works and then if you hit enter that uh and then do messages so you can just hit enter and it'll
replace what you typed okay and uh we should pretty much be at the point where we only have one assert that in each test
so can we um can we just scroll through our tests yeah you can jump from assert that that so this one so the one 188 we
replace and we could get fancy with uh bother now this one's values right now this is going to be a an interesting issue
um that we'll want to fix right now we should never be we should never have access well we probably don't want to make
it easy to access values if it's failure and similarly we don't want to make it easy to access failure messages if it's
success and uh I don't know that we want to do it because what what happens is instead of returning an instance of the
result assert you return an interface where it's only in a sense it's it's a very state-like pattern we only return
things that are allowable from this point so from is Success you're not going to return just a generic uh result assert
what you're going to return is a result success assert and it would not have values values in fact it wouldn't even have
is success or his failure it would just have values on it and similarly for uh so sort of this this idea of narrowing
down the the interface as as your fluent thing goes um I don't know if we want to spend time on that we can make that
choice but let's clean up all all of our assert thats to make sure that we're we're using all our new stuff yes looks
good uh that one's that one's fine we're testing it success and we're checking oh yeah I mean to a certain extent that's
a test against result itself um fix yes typed fluent interfaces go oh I see I was doing is Hing the delete key instead
of the End values and you want to fix that dot is Success so it's on a new catch fix so I want to point out and this is
a really really really micro nitpicky kind of thing um in in the way that that I approach an edit like this so what
you're deleting is you're deleting the semicolon that's great uh and then you're you're uh deleting the entire next line
except we know we want to call values uh and so I'd actually leave that in place so I only select up up to just before
the dot delete that mean like that yeah so hit enter not delete you mean after you just told me about doing end I'm I'm
totally messing with you yes no you're right you're right you're right right and and you know and it's these kind of
things that that um I know it seems like to to some folks like who who the heck cares uh but um it's it's some of those
these micro optimizations that you know part of it is is just my tendency to look for any way to to optimize even the
10est thing um but I think it it uh if you do it a lot um it becomes second nature and then uh it's one of those reduces
you know how much working memory you have um but if you're not fluent at it it's going to you're going to spend more
effort and so sometimes falling back to what is is less effort even though it may seem like it takes a little longer
right um but I think also it's important uh it becomes more important um because uh then what you can start saying is I'
ve done this twice so uh are there other can I do a search and replace or I can do a multi carat of what we've done so
if you select just from the semicolon all the way through the result values and then you do Alt J do you get any yeah so
do Alt J again is that one we want to do yes and that's it and so now you can do enter and then end and then backspace
and then control yeah so backspace deleted that closing pren that's no longer needed I already did it yeah you did it
okay the back no the one you did okay yeah uh and now you can do a control alt L to reformat yeah don't we wanna but
actually now you want to escape out of your multi karat otherwise you're gonna get really messed up yeah we just want
this one yeah and you'll do need to do a reformat again yeah yes deliberate practice which means practice where you're
practicing on a couple of micro things so this so practice on shortcuts practice on key maneuvering um with that as your
as your as your focus and those kinds of practices you don't have to spend a lot of time on uh because once you start
practice doing the deliberate practice then you become more aware of it uh and then when you're actually doing it you're
going to spend that little little extra time and uh if you if you do it enough it will become second nature um there is
a trade-off though because if you don't do this enough um if you just don't find yourself coding a lot um you're GNA
spend more time trying to recall and remember these things than if you just fell back to your default way of doing it uh
so I only recommend this kind of optimizations of of key navigation and things like that if you're coding a lot because
otherwise you you are going to actually increase your your your working benefit uh is that it for all our cert thats did
we clean all of them up yeah check that one special speci uh can you go back up one or the all right cool got them
commit so what' we do we basically converted or converted multiple assert dos to to a yep cool yep uh so so we've
created our result assert although we have typed it to be um uh result of song we do use result tests song parser test
is the bottom pile which we already covered right service yeah so let's check that out that might be the only other
place um so these are also songs so I think we well so this would be that to no be careful the second assert that is not
asserting on result at all oh we just want to convert that assert into assert that result is Success which will require
a different import God it I hav forget what the what it looked like sure that song result yeah is Success got it I'm
still no it's just that you're pulling the dot is Success out of the true what a mess uh and so now we want to change
our static import right manually do that or yeah manually do easiest just delete this one which will then Force the
other one or uh yeah if we delete this then it will ask us to import because now there'll be multiple multiple choices
and we want hours which is a second one do you want me to op suggest an optimization for something sure okay did and now
do Alt Enter again and uh import static method now there are a bunch of these options that you will never import and so
what I do is is I basically uh have uh if you go to the third one and arrow don't try to use the mouse because you're G
so from there the third one right arrow oh on my keyboard right arrow on your keyboard right arrow got it uh honestly I
think you should exclude oric ham Crest because you should never use ham enter and then repeat that process and what
you're going to do is for each one that that you're never going to use you basically are we're we're telling intellig
don't suggest these in this popup so go to the third one hit the right arrow key uh I would say the second again third
one third one it's always going to be the third one because the first two we want and it's always it's going to be the
second enter there's a lot of these and it doesn't mean that you can never import these it just means it won't suggest
them which is because most of the time you're GNA want the one this one yeah that this one this one uh what's is test
container shading it so you actually yeah that one is coming from junit and that this one be careful of because you don'
t want to exclude uh entire J unit um I think it's probably one so now you only have two choices right and so now um
when you don't have two choices for example uh if you don't have a custom assert then you won't have to do anything
because it will just import it for you right because it will only be the one choice but this the one we want that one
yeah so I I spend you know I spent over the years a lot of time adding to that long list of don't try to suggest these
uh and after a while it becomes a lot nicer because then a lot a lot of times there's only one choice um which means
when you type something it just it just Imports it is that list exportable uh it's stored somewhere whe whether it's
easily shared with other people as a separate question is it per project or no that's a that's a global per per intellig
instance which means if you go like me go back and forth between different versions uh you may end up with some things
out of sync because I've never set up my settings sync properly do all right um was there any other assert that'ss in
this that we wanted to take care of what about this column that's not against song this is against string yes and we
Wills right this is oh this is our custom stuff yeah that's the custom stuff the second one in song a service test what
was the second one this one yeah uh so that one we want to fix in well so your optimization is not going yeah I wonder
will this no but we don't want is Success we want is failure that's why I saying trying to optimize this is not going to
yeah yep all commit y so then the remaining one is this which is completely different we're going to have to think about
how we're going to assertion um meaning something along the lines yeah uh not sure that's the right syntax but just it's
uh if you fix up the result assert to the left then that will because you need to generif that one as well ah can I um I
don't think you yes but uh so if we look at our result now uh on so generics get so we how how do how would could we
even do this we could um but there's no way to tell through an assert that what the type of result is what the
generified uh what the generic uh type ouch there's proba probably a way um but I think it would require more effort
than I think is worth it for the couple of asserts we've gotten in in the in the so we just leave the um ones that
assert against string to just not use the custom assert just leave it so we could we what we would probably have to do
is uh create a different assertions class and then we'd import so we'd have result song assertions and result string
assertions right and again there might be a better way uh but damned if I know so should we rename this one result song
assertions or result song assert um oh wait a second result assertions needs to be uh yeah that's the one that would
have to be renamed uh but I think since right now there're it's we're just going to I think we're just going to leave it
like not bother with the I I would say just let's not bother yeah because how many tests because I think we've got like
two or three tests in this thing fine yeah it's it's more it's it's more not because it's it's going to be terribly
helpful yeah I agree yeah I mean it's only two tests yeah testing screen and so the first one uh I mean that test is
going to change Behavior anyway very shortly um and the second one I think uh You' be slightly nicer but it's not that
deal all right uh do we want to take another Break um yeah that's probably a good idea okay so we come back from the
break done and so that's the next one we want to work on yep yeah all right so uh we'll take a short break when we come
back uh we'll tuned e while we're uh still on break little commercial message so besides my tdd game which again is
available at uh td. cards and again you can watch a video there for uh an introduction to it and and see how uh how the
game is has played as well as a little bit about um my process of predictive test driven development uh as you may or
may not know I am a technical coach and trainer and so if you or your teams need some help in getting to be able to do
tdd or just want to be able to write tests better and write code better and refactor to both of those uh go ahead and
and contact me and uh if you just want to set up a chat to see how I might be of service to you or your team so I coach
both individual developers and I have a lower rate for that uh if you're paying on your own because sometimes companies
don't reimburse uh for that kind of personal uh attention uh so I have a low rate for individual developers if you're
paying on your own if your company's paying I still uh coach individual developers or payers of developers um uh and of
course uh will Coach uh teams as well uh I use use uh ensembling so either pairing sorry I forget that that timer is
always so loud uh so I uh do pairing coaching and so you know very much what you see on on stream is the kind of stuff I
do for individuals and for teams as well we do it as an ensemble uh so we're all seeing and all working with uh code
examples and katas uh as well as working on your actual code to uh to help you get your code into into better shape and
so sometimes you you need that kind of help uh so again you can go ahead and contact me um one way is is via the Discord
so if you're not already on the Discord uh you can go to ted. deev Discord there also an about page so ted. deev about
and you can contact me uh through there um and even if you're you're not sure if it's a good fit or you're not sure what
help you need uh happy to set up a short chat and and that looking for the right button there it is aren't we all okay I
always forget like I I I don't usually use that timer I use that timer um uh when I run my training uh and I need that
noise but I always forget how is all right um so we finished a j ticket we we uh now want to move on to to this one um
and I think we actually yes so want you hit a Escape so we can hide the search stuff so we want to change behavior um
right now uh when a column doesn't exist uh we don't want it to return an empty string because that would really be just
invalid want so this is for a required call colum or for let's see we've got one two three four five columns there I
think this is completely separate from required or not this is basically asking for some reason we're asking well like
that's a good question so what what what does it mean to to say that this would be a two like what would what would it
mean to ask like does so the so the the question I have for this situation always is is does this test make sense and by
Mak sense is I I mean Behavior something that would actually happen like would we ask to extract a name and I think the
answer is no no yeah um so well of that name column and that column doesn't exist so what do this can we go back to Jer
for I yeah so yeah so what is the behavior we want um will we so if we're importing data and the spreadsheet that it's
coming from says there's a column there then that column exists so we're going to extract through all of them actually
how are we column we're generally extracting specific specific columns specific columns right so and we're extracting
specific columns expecting so let's let's be more precise we're not just expecting those columns those are the required
columns right that's where I was going with that yeah does so there's required columns and then there's allowed columns
we haven't really gone down the path of allowed yet right we haven't gone we haven't we haven't done anything with with
with those non-required or optional columns that optional but allowed columns um so is this about then is this test
really column I can't speak to the original intent I if but I mean the original intent was we're returning it empty if
if the column doesn't exist but that doesn't have meaning from a from a functional standpoint anymore right or it might
might have changed so what I guess you into is this the beginnings of of our do we have any required tests at all I don'
t think so because that's a feature I think we haven't even implemented can yeah well we've got some tests that they
were oh maybe we do uh maybe we're looking though yeah let's let's let's see do you want to increase the bottom splitter
oh yeah would you prefer I do this switter um well while we're here let's take a look uh What uh do we have a failure
for required we do have a disabled test maybe that something yeah so this so maybe so we basically don't have a test
that says if you're missing required columns we fail because that's what this test is meant to do which doesn't ex
technically doesn't exist yet exist yeah because just looking at the um I don't think there's anything that required in
there right it's just saying yeah and we're basically always returning a there right so all of these required test our
success return success for row with required columns we're not actually checking required we're currently checking
existence we are we are basically we have no uh failure tests and that's why we had the disabled one um so I think uh so
this is this is the the do we start inside out or do we start outside in um so these two are actually yeah they're
they're definitely related yeah or part really part of the same thing so um I where was that here yeah so do we start
from here or do we start from the test CU certainly this test is no longer the behavior that we that's right so do we do
inside out or outside in I think for a change of behavior of this type um we can try changing it from here see if that
breaks anything uh yeah because it will break some of the outside it might larger T it might break some of the outside
int yes yeah especially the ones that are succeeding that maybe perhaps well we can do a we can do a test test we can do
an experiment that's what I meant um we can just change the Behavior Uh at the code at the bottom happens so instead of
always returning success we can return failure if it's if what's not found I'm kind of on the El uh no so push 28 above
uh into the into the if Block it's all nope did I Okay and then yeah and then uh return a failure uh and it this doesn't
matter we can just do an empty Casey so this is basically now saying if it ain't there we're going to return a failure
so this is our experiment to see what uh fail yeah few so two tests fail um because the column Apper that's the behavior
that we want to fail so that one's actually okay uh so what's happening with that one so what's the what's the test
testing it 51 oh that's never mind yeah so what what's what that L that 51 in the in the parser what is it doing yeah so
it's successful oh right we just do arst success yeah um but that's not that's not that's not terrible I think that
that's okay uh and I assume that one um actually nested so yeah three tests that failed so those are all yeah so it's
all about the the sort of required columns stuff um let's take a look at that see yeah so let's go back to the
implementation in our song parser so right now in a sense what all 1 two 3 four five those are all I forget what our
what our definition of required columns was yeah me neither um 81 theme artist song title okay that's so right so
release title and release type right now our code requires them right um so I think we need to fix that first and mapper
meaning this meaning 45 and 46 we can't assume that the return value is Success right failure is okay in the sense that
if it's a failure it means um empty we just skip it yeah we don't um we still create the song but we right populate with
empty test the reason that went to fail is because because now we're returning a failure if we don't find it so we're
not finding release title because it's not a required column so we need to fix that experiment never mind I should have
just done this yeah here we go so we should be see test at song parser level at the song parser actually we need to
write a failing test behavior or is this really a refactoring I think it's actually a refactoring because we have the
behavior we three right and if it's not there we want an empty string so line 178 in our test on the top is ex that is
the correct Behavior that's the correct observable Behavior so if our observable behavior is correct and we want to
change the implementation um it's a refactoring from this boundary point so from par song we don't want the behavior to
change but we want but we do want we do want extract column to change so it is a it's a refactoring at the par Song
level but it's a behavior change at the level um column mapper the column mapper doesn't have required no it does not
and is that it it needs to understand that or does parong need to understand it and colum mapper doesn't that's an
excellent question whose responsibility is it to optional it seems like parser and not the column mapper because the
column mapper doesn't well let's see what does it do header columns do not contains can we scroll up in in column mapper
bet how far up uh just so we can see the rest of the code so all it is is it's a mapper it has no concept of required
not required it doesn't care what columns are this could work in a song theme or in some other application so this is a
generic kind of thing so do we push sort of knowledge about required versus not required into we column mapper would
return an empty string for an optional column uh and would return a failure for required saying I think that's much
easier than parser because here we'd have to say for release title and release type if those are failure results map
that to to right yeah I see where you're going with it which wouldn't be unreasonable but it feels like I mean I don't
have a strong feeling but it feels like I think it's okay for column mapper to have this idea columns CU that would mean
that that song pars basically doesn't change right it would come back right and it's already because it would make this
method well I don't if that's a complete justification would make this method this being parong more complicated because
it's doing all this checking yeah I mean it it we could do a map of of some sort from a functional thing but um but it
would make it it it this so um so then I is then only a behavior change right now only a behavior change in the column
mapper so we want to add the idea the behavior around uh required columns versus optional columns and we only have two
tests here so that's easy to yeah and the first so so I think we can change this first test to say uh empty string
returned uh let's drop release title from our columns and be the one that that and then be and have that be the one we
you mean okay now and now and now column mapper needs to not have release title as well cuz what column mapper oh is
doing is we're is we're specifying this is the header so how do we want to do that um is that right well no this is
saying this is what's being passed in so I'm actually now confused by the parameter to the Constructor right is it the
header it is the header it's the header of what we got right so it doesn't declare what's required and what's not 13 is
our data and I'm and it's confusing because we use the word the generic word release type which I think is is confusing
in this test so let's fix that let's use a real world value for release type on 13 oh I see what you're saying got it
actually I forget what that is let me check spreadsheet ah okay got it yep and what would be uh and so extract column
release title that's actually the column name that we're asking for so there should be 14 right so now what we're saying
is uh quick one yeah I'm just gonna sorry I just gonna write this down before I forget um this is gonna be make it
complicated if release possibilities it's G to make this ugly um yeah for now is compilation then release title becomes
required fun yeah exactly so sometimes you uncover new requirements while you are busy working on and I think that that
pushes it even further that column mapper is the one that needs to handle that that level of complexity right yeah yeah
I'm with you uh SMY core asks wouldn't it be valuable to have a separate method that expects to always return a string
uh not quite sure what that means I think for extract column that's what I'm guessing what they're talking about so if
you go to uh the the song parser so what we want here is we want song parser to just ask for these things so for artist
and song title those are required we should get a failure if it doesn't have those columns uh similarly for themes as
well for release title and release type um again we want to defer any requirements of should this be required or not uh
to the column mapper to basically our configuration of the column mapper uh having song par song call two different
methods if we decide that we want release title I mean even the so the situation just came up I don't know how we would
do that here I mean I know how we do that here would make this much more complicated right because it would basically
say if release title equals this then call this other method if we push all this into the column mapper um then uh then
that complexity is hidden from here and I think it's at yeah so uh all test uh our test does not look right because our
header has an extra release is compilation a release title or release type type okay um one two is there another release
title yes um can we use that one let me see if there is I spoke too soon there's one that I I probably I'm not even sure
I would use is the concept no they all require a title so the three values here I'll just show you the three current
values are blank um and then soundtrack well if it's a soundtra I need to know the title okay if it's a compilation I
need to know the title okay if it's a collection yeah you need a title so because I can't think of a reason where you
would not need a title for those two uh are there other optional columns then that we have so release title is optional
unless release so can you have a release title without with an empty release type definitely okay okay so let's have our
data reflect that reality so let's switch it so that it's um so let's remove release type from the header right and then
instead of compilation it mean probably should make the data consistent all the way across so yeah I mean as long as the
the fields make sense um I'll leave it to you oh right okay yeah greatest H oops no don't type there over here I'll just
say Greatest Hits all right that's a title probably exists and so now the what we're going to look for on the next line
instead of release title will be release type let's extract release type that string who uh and let's call this optional
column name uh you've got an initial uppercase letter oh oops so what we expect here then pass does so I presume now we
want a test of a failure mode now we want to test if it's missing a required column right what does the next test
currently do okay so that's mismatched column data so that's clearly wrong yeah so now we yeah so now we want so empty
string return an optional column doesn't exist that's cool and now we want to test for um exist rame this one to does
not yes I that so really you could probably just copy 11 yeah I just wondering why do bar is not working uh because VAR
there's no there's no variable there that's the name of a class oh I meant new new was doing it and so I similar so I
right that's good I don't know why I have it Aras it a r form that was just a reminder to you of what that was without
what the curly braces so now we want a um now we want a name that's the one we got rid of right title so here yeah so
remember that we don't have uh our ah for string our convenient yeah string which is unfortunate uh but we we can fix
that uh no we check the values right we want to check is right is success is false right it's so funny it's still like
yeah it's awkward even when writing the simple test is success is yeah it really is a cognitive friction um we may want
to if we're going to write much many more of these we may want to rethink writing a separate assertion for for that
right yeah for sure so now this should fail because it's we're because we're always returning success yes yeah so we'll
run it anyway so we expect true to be false yep white uh can we uh put an as message in here yes do we want to specify
which column in the ads um no what we want to say remember this is the message that gets displayed when the when the
test fails I don't think this is a good enough message because this is not enough context so what would we want to let's
run the test and see what we see and and it so does that message tell us why different so so what I would do is I would
say um because like that it right so what I what I want to see from from failure messages is okay we got true we
expected false why are we expecting false right and so now this gives us enough context that just that message uh can
can help us interpret the uh the assertion failure message is header columns contains in I don't think we could ever
make this passing the column mapper doesn't have enough information to evaluate oh it doesn't know which it doesn't know
what's required yeah yeah so I think refactoring right would we pass it into the Constructor of column a a hard a a list
that is a static private field of column mapper that holds what the required columns on um I think it probably makes
sense to start with hardcoding it in the Constructor because then we could push it out although right now we'd never
really need to configure it except maybe for tests uh right but the simpler thing is Constructor so prepare refactoring
um what can we do from that perspective well we could add this field and and and check it um first we want to green so
get back to green by the simplest thing that'll get it to pass even though no you said it'll break other tests yeah so
we want to get it to Green by disabling it disabling it okay because we're about we we're basically doing a prepare that
will prepare us to get this test to pass yep yep of course your go back to green so we can do prepare refactoring right
and then we right so what you thinking trying to figure out what to do from a prepair refactoring okay it's not jumping
out at me at the moment so I'm so what are what are what are what what Behavior do we preserve oh I see what you're
saying so it extract out the behavior we're going to change so what is what in in our in our column mapper tests what
what do we what do what does our first test say because preserve so it's saying an optional column returns an empty
string right we have no idea what an optional column is well so an optional column is a not is a column that is not
required right sorry when I said that I meant the column mapper doesn't know right but we're gonna hard code that so
let's hardcode that let's add a let's add a field a field okay yeah we can add yeah and would it just be a string with
the column name um or no I would say it's a set of required column a set of string of required columns and then just do
an array literal for this uh well this is a set so you can't use an array literal and we probably Constructor so
initializing Constructor uh we probably want to first and so it's going to be set of and then our required columns so
themes is going to be interesting y but certainly at least theme one is required yes good point but as a string so
particular some parsers don't care uh some languages actually don't care but this one apparently does yeah are those the
three I mean are those the three required columns putting aside the fact theme artist all right so now that we have that
that's clearly a safer factoring because we've just added a field that nobody's using right um so now what Backward
Compatible change can we make uh in our implementation that will change so the next change is to make that every column
name that comes in is one of those three so I would look at it from the point of view of what change could we make to
the code that would that would help us with that but make the first pass the first test is getting so you don't have the
first test in view just so you know oh thank you I say the first test is missing um required column this one does one
and an optional column so how do we use our required columns in our extract empty so it's I'm getting tired yeah so we
only care we only care about this when we don't find the column because if we find it who cares we just return the 30
right if yeah else if what did that do I see that has a whole Branch um so now we can look at uh if it's an option
column then we can just string so we don't have optional columns we have the opposite we have required columns right
because we can never know okay where is column defined is that a well we don't care about the actual column right this
would be this oh that right right but we don't have a way to check for it so it would have to be not right is that right
yeah so we but we need to use the variable we defined columns and then do name so this will not break the existing I'm
still not entirely comfortable with with it you may think yep yeah it does okay so we didn't change any Behavior we
didn't change observable Behavior right um and now we can do a bit of cleanup we don't need to to set the column string
to empty uh on line 26 because we're no longer going to return that so we can push line 33 oh into here into there um
can we manually do that I mean sorry not well we can't do it yet because if we if we do that uh since we're not handing
the but that's what we're going to do so we can't quite do it yet because we need uh to return a failure as as a result
but now we're backwards compatible um what kind of refactoring might we do though for further to to read reverse it
right because it this this else Clause is dependent on us not finding the column right we can't like invert the if so
what else do we do with Boolean Expressions that are hard to okay and so what would what would you read what did you
have before when you were sketching oh I forget what I wrote but um there's not no no it's is optional oh right if this
column is string yep so now that we have that um we could stop here or we could uh reenable the test and try to make
that work let's do am so we still expect this to fail and we expect it to fail for the same reason because it still
doesn't failure failure ideally right away well let's let's do the simplest thing uh oh we could do it right away sure
without guard Clause right would be can we go ahead and finish and and and and and type what you're going to like oh
yeah I'm not sure what I was gon to type actually because yeah I I I I think you were going to try to try to do a guard
Clause but there is no guard Clause here right the column name is a column name we don't know if it's important until we
data what I was going to do is basically replicate optional but actually optional is legit and that's not so yeah
optional required we don't know yet if it's okay we don't know until we hit line 30 basically 32 so can we make one
change that gets that gets the current failing test to pass knowing it'll break others knowing it'll break others oh so
then you can make this failure yeah so let's comment out that failure and we'd want to to say something like required
column not found or something just as a temporary message we're not asserting on any message so we can just oh oh right
that's an ad it's not that's an yeah required column not found is that what you said um we can actually just make it an
empty message because there's uh we're not asserting against it okay so now if we run this we're expecting 23 to pass
but everything a bunch of us stff to break right so it did yeah got the little green there yep so clearly that's not
good enough it's in the right direction and so how can we and so this is the typical well I can't make it work by always
returning failure in this case and I can't make it work by returning success so we need to do some logic evaluation yeah
so what do we know us at this point we know well no this is a return so we so we know that it either or well when do we
want to return success so clearly 31 return success if it's an optional call and we didn't find it when else do we want
to return success if it's a required call and we found it well who cares about if it's required or not if we found it
we're not returning it now if we found it so let's it yeah so let's return it inside that block oh in the block oh so
basically move 34 to the current are right so if we find it we return it if it's optional because we and we didn't find
it then we return an empty string if neither of those cases is true failure voila voila voila any kind of refractor to
make this easier to read well one thing we can do is now column we don't need to have uh right no doesn't let you pull
it in huh did um you could just push it in push it in and then join no you don't want to in line I mean you could but I
don't think we want to I would just push 26 down a couple of steps join alj no that's multiple J and then should we just
um inline column or does that a little bit too agree so there probably further fact we could do um but we now have uh
all our all our tests passing with our new requirement that it's okay to not have optional but required now there's
there's probably some other stuff we could do further up the chain um but I think we can go to jira uh at 75 this one we
did in we we approached this from a different direction we're still currently not like we are essentially we are
requiring that head of rows have specific columns we're just doing it in a way that may not be obvious uh from the song
parser and we're actually not actually checking it at the song parser right so here we're either getting success or an
empty string so the one we're not checking is is song title so if song title is missing that should be a failure oh here
we're not testing for it yeah should we do an and there well I think there's more to do and I don't think we should do
it now yeah yeah uh but I think we should uh update our update jira to say that um we don't currently level yep is that
an uh I think that's part of that yeah yeah like that there um yeah there there there might be some some so right now
we're relying on column mapper to return a failure but we know at tsv song parser even before we call the column headers
right so if you if you uh scroll parser basically what uh right at right at when we create the column mapper right there
we know and whether that's the column mapper uh the column mapper knows which ones are required and if you try to create
and so the question is if you try to create a column mapper with a header should the Constructor throw that doesn't have
yeah that doesn't have the right the required columns should you bother you know I I don't tend to like Constructors
throwing an exception um so there there's some there's some interesting stuff about whose responsibility is what do we
bother if you were oh sorry keep going do we bother at all checking in the Constructor or just assume that we'll check
it later or would or would we create a factory that does the checking and it's not checking in the Constructor so we're
not throwing an exception we're returning I don't know I no I don't I I I would I would not want to throw con throw an
exception from any Factory method I think unless it's something really wrong uh from yeah that's no different than the
Constructor yeah for for validation um I would want a method that says contains required columns now who implements that
I don't know but I'd want somebody to to tell me whether I should even bother creating a not because right now we don't
fail until we've started processing the rows whereas which isn't that much further right we're as soon as we process the
first row we'll find we'll find out um so we may be fine with that uh but that's an open question yeah should we write
that down or no I like to I like to say if if it's if it's really something that bothers us we'll see it again and if it
doesn't then we won't worry about it sounds because that is truly an implementation detail from a behavioral standpoint
we get the same result and so it'll pretty much be whatever whatever makes it easier to read and reduces duplication and
passes all our tests etc etc so should we commit what we got yes because we now um fail appropriately when a required
column is appropriately what was that again um missing in in col uh column at the now all right I think that's all folks
so um do you want to do a idea uh control shift k yeah so control K does a commit and if you don't do a push from there
control shift K will show you all your unpushed commits and then we'll push them down shift all right that's all folks
um I don't think we're streaming again this week uh but hopefully uh next week we'll we'll do some more work on this
yeah I can't remember if we talked about whether the weekend was a possibility or not we'll play that by by year um yeah
but certainly within the next week we will uh continue with another episode working on our song themes um we we'll
basically finish up the the required column stuff and then maybe persistence see I told you we wouldn't get a
persistence today right yeah I know um I'm eternally optimistic yeah but I I I I I think this is the last validation
stuff that we need to deal with um and I do believe next time we will at least start on on persistence we will certainly
not finish it but we will at least start on persistence so so stay stay tuned for that uh as always Discord is the the
place to find uh to find us and chat about stuff um so join the Discord uh and and feel free to ask questions about any
of the stuff that we've done um I still have some of my tdd games in stock so get them before I run out go to T do cards
you'll see a video and uh otherwise That's all time
