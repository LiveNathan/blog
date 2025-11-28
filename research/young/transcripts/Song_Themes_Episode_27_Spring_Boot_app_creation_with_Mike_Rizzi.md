# ＂Song Themes＂ Episode 27： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=XPLXGfgmFUA

---

## Transcript

all right folks hello everyone welcome to another par stream this is episode 27 of working on the song themes how's
everything going Mike going well thank you good morning good afternoon for folks further away or evening or evening
although I don't think we have anybody where it's that late just yet 9:00 am here yeah that's true it's 4M UTC dinner
time I guess in in like Berlin uh India India is like 12 hours 12 hours off or yeah so um do you ever have folks from
India uh watching yeah occasionally um occasionally folks folks from India yeah yeah I've done I've also done teaching
live I mean remotely uh in in India and that's not something I'd like to do again yeah it's the 12 hour shift's kind of
rough yeah it's like let's start teaching at at 800m my time and I thought you know working with the client on the East
Coast was rough that particular client liked to start early so I actually had to get up at four I started work at 4:30 a
yes um because they wanted to start at 7:30 am on the East Coast so that was rough yeah such is a life so um should we
uh check into jira and see where we're at good using our handy three angle bracket uh yes our we currently working on J
77 or about to let's see require that header rows have specific columns right we're working on that one y yeah so last
time we uh improved or actually created uh our special assert class for the for our result class and that's made some of
our tests um nicer to read and write um and next up is that that where we're going to check that actually we have some
required columns um and uh probably need to to to do some refactoring around that we we'll get to that um and we
discover sort of a new requir ment around dependent columns which which is interesting yeah that was I mean it's a
beautiful example of like oh you think you know all the requirements UPF front and nope you don't and even if you try
and think about them you don't always know them because you discover yeah it wasn't it really was would be a hard one to
think of in advance like oh you know the type's not that important yeah hey there Sue and so I put the odds of us
getting to uh Jer 81 which is persist to DB at at at uh at 30% so oh wow I thought you were gonna say asymptotically
approaching zero no no no um it'll depend on on uh if we do decide to do number 79 uh how long that takes so yeah but
fair pretty pretty low odds of getting to a persistence today but we will yeah likely get it get to it within next
couple of episodes so pretty close yeah um so all our tests are passing so that's good um so let's let's dive in let's
see um do we have any disabled tests where all our tests enabled looks like something is this one uhuh so let see that's
where we left off yeah so let's go take a look at that yeah first all returns failure when missing require required
header columns right so let's take a look at at our implementation of how we're how we're currently how I things right
so we have hardcoded the 14 um but we haven't handled uh we haven't handled the multiple themes issue right oh come on
yes it's the doing of the work where we discover the work to be likes they're like we we want and it's handal multiple
themes good enough for jir 78 uh yeah that's that's more than more um oops wrong with tests now here we're testing at
the tsv song parser level right I think we need to be testing at the column mapper it was a note here let me see handle
missing song title at the parser level it's missing the song title so if I remember correctly the implementation I think
we can see it if you scroll down a bit below um we're uh oh not sorry not in column mapper but in the in the in the song
parser itself we're not checking for uh in Parson which I think is in the next method yeah so we're checking to see if
artist was successful we're not checking to see if the song title was successful so actually we probably yeah here theme
well go ahead the question is do we check this at the song parser level or at the column Apper level well we are
checking at the column mapper level that it is required uh and so it will return a failure we're just not detecting that
failure so we need to uh create a failing test to fix that at the song parser level at the song parsel level yeah okay
so and do we already have the sketching of that parse all no that's different that's parse all have oh what's this par
song Single song test interesting I wonder if this par song should be in this uh en closing class uh maybe so like parse
all for song with name okay so now it's go down class not enough columns success for row with required columns in
different order yeah it yeah yeah yeah so we want to check that it returns a failure um so I wonder since this is going
to be yeah do we what was the other returns failure test in in this there's only one for row okay yeah a at least a
parameterized test for for the for the artist in the song title because the reaction should be the same so it's result
failure for returns failure when uh required coln missing right and we'll start off with song yeah we'll start off with
song and then we'll yeah so missing column that oh this is a different order is this yeah maybe get a better example
than that that's the non-standard order yeah let's go with a standard order just to not make it to make it less title
are we passing yeah you can pretty much copy 186 yeah now we to insert can we actually change um wondering if we can
rename song result to just result what do you think sure and do it file well are there other results where it's not a
song result yeah there's result strings but those would be in a separate test so we just being inconsistent is is is
sure is it all J yeah was I about to do right and it'll wrap around right uh it should yes didn't me do okay and then F6
uh so it said you need to try it again if in order for it to wrap around oh there was nothing okay so then at this point
do you do the F6 because no because you've selected them all so you just start typing oh okay except for the backspace
button uh looks like you have to do it that way there we go Y no don't hit ENT there yeah just hit escape to get out of
the multi carat yeah uh let's run our test just to be sure we didn't break anything oh yeah I was in the middle of
hitting yeah shift F10 when you were saying that okay we just oh this is the one we started oh interesting no such
element exception I expected it to not even yeah so because we haven't even written the assert yet but of course it's
failing Upstream of the assert yeah so uh since that's unexpected let's take a happened oh okay actually that's that's
actually expected yeah until we solve that part of it right yeah well uh I think I think an assert what would our assert
be assert would be that it's a failure because we wanted to not throw an exception we wanted actually to get a failure
result right how are we doing that above we're just doing that and then we're checking for a message but we'll start
with just so so much nicer with our with our yeah okay so we know it's not there's no use in running it because we know
right so um let's fix it what's the what's the cheapest see y sh okay yeah ship it wait a second no uh so let's um I'm
curious what the failure message be uh well so yes so this is where the test will fail next is um the message in this
case is going to be wrong um so what we want it to exactly uh some message um are we going to just uh I think we can
just assume there message yeah we can characterize it yeah it's gonna be wrong though right but at least it'll give us a
hint in go oh oh uh and I and I I saw this before and and it it lodged in the back of my head and now I'm like oh yes we
are not returning the correct failure message uh um we're not even returning a failure message yeah we're not well uh
right we're not returning a failure failure um which of course makes sense because um there is no failure for artists ah
right which is what I I what we expected or at least I expected that because we're not looking at song title um artist
has no failure messages so it's empty uh so so we have to have a separate conditional for each right right um so let's
go look at what the failure message should be for uh when we column extract column so this is what I thought we'd get um
because right now on 33 we're not actually returning an appropriate message right yeah so suiga brings up a point if we
ask a success object for its failure messages should that blow up or should that return an empty list is an I don't I
don't have a good thought than I'm not 100% sure it's actually a fail like that it should like throw an exception or
something I mean is there some well it's a little bit of a yagy future value of having a success I mean the qu the
question is is do we feel like asking a failure result for sorry a success result sorry well either way a failure
success um sorry a success result for its failure messages is that ever useful oh I see is that is that something where
if you ask for failure messages on a success result should it exception but how do you ask for failure messages because
we're doing is failure and from that getting the messages well it would fail in in the um in the song pars or in the
parse uh so forg got to PSV song parser right so it would fail on line 55 because when we ask artists for failure
exception oh if it was empty so if artists succeeded yes um so it should have no the the only thing I'm not sure about
is sort of accumulating the failure easier maybe to collect across all the results and just messages yeah I don't I don'
t know that I want to seems like a rabbit hole uh I mean I'm always in favor of failing early um but I don't I don't
know that yeah I don't now so um so we would go back to or not this well we'd have to accumulate from we'd have to
concatenate both because we're not sure at this point which one failed we basically want to take artist failure Messages
Plus song title. failure Messages Plus eventually themes. failure messages so um I we're not going to do that but that's
what we kind of want so we want to basically concatenate all those lists together but we have a bigger problem right now
which is we're not generating any failure messages at the column that so I think we're missing a test at this level and
we need to fix that before we can fix tsv song yeah far empty string return one optimal column does optional column does
not exist failure when required column does not exist huh but this one's got a oh this is wait a that yeah because
remember we didn't generif our result so we don't have a a way to to do that and we thought that wasn't worth it because
we didn't have a lot of tests in um we actually need to add on to this test like to have a failure message yeah to have
a failure message so one thing I I I noted is this test starts with the word failure where do the other test start with
return failure um me oh here this one does yeah and all the other ones in the in the tsv song parser test which one do
we like better failure I kind of like failure it feels like return doesn't add any anything useful less less words is
always good well and and if we're looking for those that are failures versus success we're sort of skipping past the
word return anyway right so um I think our our standard should be failure or success is the first word sounds good uh so
yeah so we want to add on to the after the is false um but it's not going to be part of the same assert because we did
we don't have a convenience for that oh right um so message exactly uh what do we want it to say um this is not a
characterization because it's not returning the correct message so now we have to Define what exactly so I think it
should tell us what column or columns are missing something like this yeah and then in this one it's missing song quotes
Okay now surrounding song title with double quotes so that it's easy to read wrote so like this so an easy way to do
this uh because you're gonna have to escape the double quotes is copy this the full string with the double quotes from
line 27 and then paste it in here oh because if your clipboard has the double quotes in it it will escape it for you oh
that's cool well yes unless it's when you don't want it right of course so now here if I just do a paste it should
Escape it automatically yes sweet start run it yep so we expect it to fail because it's going to return an empty string
work well you can pretty much copy the whole thing yeah I was G to shortlived because right now we're just right but
that tells us we got in the right and so now um write a new test for a different or one to do other columns I think we
would best sort of follow the the 01 many idea um this worked for one and now the many can be missing uh two required
columns exist what do you think is better required column is not or when two required columns do not exist there's two
different ways of saying it here um I kind of like missing better okay uh does not exist sounds a little weird yeah
let's get of that and when so we yeah uh I'd like to say something about that that we're going to get multiple failure
multiple really verbose no I think I think we'll just have to not start with the word failure uh and just say multiple
failures when or we could be more precise and messages I like that better yeah except messages is picky yep actually I
don't mind at all I was just being a wise ass yeah so let's uh that and oh interesting okay so this is working at the
extract column level failures uh so this this message is actually wrong because this is too low level you're not you're
actually only extracting a single column so there's not possible for there to be multiple missing required columns at
this level but there will be we still need there will be at a higher level um true but I think we need to change our
message yes so let's um this will be a sing column I would un I would delete the body of the next test because it's it's
no it makes no sense for what we were going to do oh I see you're thinking of doing this and then let's force it to fail
yeah missing required column fail left in the wrong Cody thing yep let me rerun it it was an underscore in there before
it hit I'm mistaken that and then we've got to generified to generif is not the right word but now have a deal let's
parameterize it instead of writing another test we column uh so you're gonna replace test with parameterized test ah
that that always confuses me I'm like can I parameterize a test an existing test yeah um but I think it has to construct
uh do you have it memorized because I would go look and see what we did for other parameter uh it's values oh it's a
separate yeah it's a okay so does this need the pns or no uh no because we're not we're not adding any uh value Source
or or you said what kind uh in this case we want to to have matching inputs and outputs so CSV brace and it'll be easier
to read if we start a new line and then that yeah or have the curly in there okay no that's good um so this will be uh
what we currently have title and then uh inside of that is going to be uh a comma and this is going to be tricky um
because we basically want that entire string uh without the outer double quotes though yeah should I close this code
first no no no because it's this is one pair of input outputs oh that's interesting it it basically took out uh so I
think it's because of this if I did this oh I see okay that's what I was saying put the right um let's get this to pass
so that we make sure that we've done our parameterization correctly so we're going to have to uh replace um basically
delete 33 and move that as it yeah uh and then you can introduce parameter on the contents of our right and got your
message yeah fail your message I love how it introduce parameter basically the parameter disappear the contents
disappear because there's no callers but this is perfect for for for this uh this case it'd be nice if it could like
parameterize it for us but that's a little bit much that' as um if we did everything right with our parameterization
this should work yeah let's see excellent all right so now we can pair so but the thing is it depends on this also this
is artist but that's just strings who cares okay right they're just they're just strings got it uh so let's so what's
the other something along this line or it would be actually I just steal the whole darn thing you can just yeah and then
want this to be artist is also required yeah if spelled correctly that yep so that will fail because it's gonna arst to
not song title right we've got it hardcoded to right setup oh our column map mapper has to be adjusted oh so we've got
another source yes uh but that's the same as the first as the required column name so we can just pull that out into a
variable so if you select artist and then extract here what control V oh won't do a partial sure oh will okay I just the
wrong keyst Let's do let's call it name 29 delete line 29 oh I see got it no I was just trying to grock it what you're
doing so that's going to move recall I see yep okay now I know what happened I'm good we made it the same name as the
already existing parameter I'm gonna undo it I want to see if I understand um actually I think you I think what you said
before was was actually right uh and sui points that out that it's the the opposite um so we do need a third column in
our CSV Source okay and I think what'll make it easier is if we pull out the entire header into the CSV Source this is
the header yeah so introduce parameter for this uh copy it first because it's going to go yeah header sounds good yeah
header's fine and then that would be the third parameter want I just do it here let me fix it basically want without the
double quotes part this is easier I don't know why it double escaped the back SLT oh interesting is oh because I thought
you wanted that as the St yeah take out the the the need uh I'd probably copy what you what what's currently in the
above line arti no no no just the last parameter this part yeah without the quote Yeah and then yeah and then we'll
works good that that works in the sense expected right just right now it's hardcoded that's the failure we want so
success yeah what is the oh you you took out the other Escape you you'll need that all right so just pull out song title
do an extract variable ah okay and then we could just call it just call it column name which already exists yeah and
then we delete that line Y that's a that's a Nifty little refactoring that unfortunately actually doesn't work on text
blocks because it doesn't know how to it can't it can't do the concatenation with with text blocks but single line
strings um this is very handy for for parameterizing so now that should now it yeah it does it does okay cool uh let's
do a commit since we now functionality for what else have we is that okay for that part yeah I think that's pretty much
all we did uh oh we also were checking for song title success yeah or started to I don't think we should commit that
because we weren't done with that so let's but we disabled the test no we didn't thought we did uh we just disabl a test
that was just a rename but later on we were disabled a test those are all renames there it is that's the test we
disabled yeah so we don't want to commit that yet got it so we'll leave those three in all right so we now have useful
error messages from our missing required column at least at the extract column level so that's not columns is that
sufficient because theme it so remember this level it doesn't care this is a single specific column column right so it
doesn't it's at this point it's been told here's the required column make sure it's here right right yeah so it's the
next level up that we want um so column mapper doesn't know anything about multiple right missing columns it is working
at a single column at a time so now we can reenable this yes and so what do we expect we expect this to give us um so
we're missing uh song title so we expect it to be that failure message where it says missing required column song title
oh interesting but it's not yes because remember we're copying the because here we're just doing the artist failure yeah
so let's let's swap that with just song yeah we'll probably break some other tests oh no didn't break any other tests
that's probably not good so let's uh let's grab this and paste it into our test yep all right uh now let's change uh did
um did we check for messages elsewhere class parol because we're still at the par level right well so those I think
messages are going to change um because it's not about how many columns oh I actually think that that message is a
little confusing the error message or the title of the error the failure message because it says must have at least five
um it's like where does five come from right uh do we want to make a note of that get back to yeah let's just make a
note of okay all right um and that was the other the only other place we're checking messages um there's that one parcel
that's parcel but with two one's yeah that's the same that has the does it because what does must have at least three
mean where does that come from oh got it yeah okay it's that one and then this is the one where okay Cur ly working with
all right so um should we rename this um well we moted generic and purpose because we wanted to parameterize it right
the title would we parameterize it or well no remember we're going to do uh one and then many so this is now fine right
this is the one actually is this fine feel like something failed uh oh because we did song title um I think we want to
make this artist and then the multiple 1B song have have both artist and song title missing got it okay so change this
to song title right um I forget the Earth One in fire song remember that I mean you can change it yeah it doesn't matter
I know it doesn't but gratitude is what you had is what you had above what the Gratitude artist we run this this should
go back right yes and it does sweet all right so now we can write the the manyu version of this where we're going to get
two failure messages missing um didn't we start writing this time or did you delete the entire test no I thought we
that's weird wait let me look at the disabled no it wasn't disabled we just written it and deleted the body I thought we
did oh wait second if we deleted the B no it still should show up as would be the bottom one most likely there it it no
that's the one we're typing all right maybe we deleted the whole test I don't remember doing that was it no I don't
remember doing it either I remember I thought we were just getting rid of the body you sure it wasn't the column mapper
test um oh maybe we were putting in the look oh there it is right because that test makes no sense there so let's delete
that I just cut it so we could yeah because the name is pretty much yeah window two failure messages when missing two
required columns right so we could fix the name of this one while we're here here yep failure when required column
missing I think we might be useful to be more precise of one failure message when okay and here you could probably copy
yeah that's what happens when you miss paste so should certainly result in Failure um and in this case uh we expect size
of two um or we could just duplicate the both um yeah I think that's that's that's a little bit easier yeah and then
let's let's uh duplicate that when you say duplicate you mean because we're need two two values right and we want it to
fail um well we want yeah we want the message to be correct how does um contains exactly work with two messages is it
you just yeah comma separated because contains exactly takes a a variable number of arguments so like that yeah but with
the one will be artist second one be song title does the order matter uh if we're saying contains exactly order does
matter um do we care about order I I don't know do we care about order I don't know um well put your customer hat order
no because if we're saying the header defines the order we don't actually care right other words we're letting people
pass in with different orders so then let's change it to contains exactly order and I usually put the strings on idea
all right so we expect this to fail because it's only going to return one of yeah right and it tells us what we actually
got which is what we expected yeah it so we want to failure what what's the what's the parameters to failure messages
and interestingly enough we've returns will that ever be more than just a single message because if column mapper is
working one at a time uh as we bubble up things to a higher level yes right so what results song is going to return is
actually two failure uh oh right right I was more talking about here artist failure message it's saying plural well it's
coming from a track column which will always be a single right now right now okay I mean there's no harm in in expecting
multiple right okay it's not confusing so then in fact I'm not even sure if we still have a single failure message as a
method I know we have it as a parameter but I think we always return it uh at least I thought we always list okay so we
want to collect the failures into a list and return that that's our goal right right now we is there a um is there's an
is failure here I'm just wondering if we should have a guard Clause instead of doing its success and have the guard
Clause collect the failures and then make return success method because obviously this isn't working right the whole and
well I mean that's a a refactoring issue um but a guard Clause is going to be uglier because it's going to be not is
success or not is Success oh so there okay I mean we want to do the simplest work right so so we just want to append the
song title failure messages even if it's well if it's empty then it's then it's not going to do anything oh yeah good
point I didn't even think of that I was going down the path of we need to make sure each one is a failure but if you're
right if it's empty it's not would um in Java can I just say plus no you can't no okay um so we can either create a new
list and do an add all of both oh I see we could do it at this point no reason to create it early uh well you can't
create it earlier right well I guess you could you could it just wouldn't be useful until so if spelled correctly um
array list uh yes we could do a stream concat but I think this is easier okay and then you just do where be and then
just comma uh no you just have to call it multiple times ah oh add all because failure messages is multiple got it right
I was like it's only a single list something like that do you want to clean up those missing semis so particular uh hey
don't blame me I'm blame control shift enter yeah control shift enter there we go shift enter I gotta work on that
keyboard shortcut so will this work uh let's try so nope oh wait a second no no the test we were just wrote made it f we
may have broken other stuff yeah we broke other stuff yeah two failure missing so it looks like yeah we broke other
stuff but and now these I don't know about you but these seem like the ones we have over here in jir saying we got to
deal with this yeah but they're failing for a reason that has nothing to do with the problem I had with them okay so
what do you think top down bottom up um go in the middle I think we shouldn't be changing anything with with tests that
are failing for the wrong reason yeah so uh um disable our current test and then deal with those uh this yeah um how
want to say on this one uh need to fix required column error collection okay uh and then let's change the code back
because we want to get to uh what we want to do is a refactoring that does correctly which we're gonna have to think
about um can you undo the whole thing I don't I don't like commented out stuff okay so you're saying just gutter revert
yeah like that okay y because we know how to solve that problem when we need to solve it again we can do it true true
but we might not want to solve it that way who knows right that's a good point all right uh let's take a break and when
we come back from the break we'll we'll see how we can uh change some inerts to to make this not fail a whole bunch of
tests when we fix this problem all right so we'll take a break and we'll see you in in five minutes cool e hey folks so
just a reminder uh if you are not already a member of my Discord Community um great place to join us and talk about Java
design issues architecture testing test driven development intell all the stuff that you see us do here on the stream we
talk talk about in the community uh you can also find out more about about me and I do coaching both uh for teams and
for individuals so if you're looking for some help in making your code more testable uh go ahead and check out my about
page and contact me and um you may have heard about my tddd game uh so I've only got a few copies left before I run out
I've got some more on the way but uh production takes time takes like eight weeks to get stuff produced um so if you
want to order your tdd game now is the time otherwise you might have to to wait a bit and you can check out a video I
did on the site if you go to td. you'll see a video uh it was a presentation I did with the agile lunch and learn folks
talk about predictive test driven development which is we've been doing here all day um and uh then I run through the
game and and talk about that backo so let's uh where we're basically the test we we reason do you want to go look at
those tests is that what you're saying yeah yeah yeah so what you want is instead of find and files you want you want to
do uh find symbol that's the the more accurate way to do it so that's this one yes and that is control alt shift n oh
that's a gymnastic one yeah so it goes along with with sort of intell's way of doing shortcuts is the your always adding
modifiers to the same key so control n is is you know fine uh fine class because that's most likely what you're doing
what you want to do often uh less often but still often enough you do files so you add one key which is the shift and
then symbols which you probably don't do a lot um although I actually think maybe would do it more uh is then all all
three keys and so it's much more precise because it's looking for actual symbols right so it's looking at parsed
information right so it's always going to be more accurate than than a general find because a general find could find
strings right or comments or um what we want here so this failure these failure messages um uh the problem was at the We
R turning we returning basically right so what do where where would we look to figure out what's what's going on here in
what way well so why did we see it returning basically four error messages instead of two here what was sort of the
underlying issue oh that's what we saw on that okay I didn't it was pretty quick I didn't notice that oh well then let's
recreate it if you didn't groc it you got to tell me because I assumed you got it oh okay yeah no no I didn't um you
gota you got to be a good pair and tell me when you don't understand something oh well I didn't know at the time that I
needed to when we never mind okay it it didn't occur to me um so well let's create the problem yeah where was that uh
well it wasn't in the test let's recreate the problem in our in our in our code oh right right right right right was in
was it in colum mapper yeah no not in colum mapper in in pars song right parong not parol right right right you mean the
thing that I commented out we could have uhuh so what you can do is you can go uh you can go to local history show
history and you can show history for selection if you selected it um but it's pretty obvious where it change and so if
you if you click the that little Double Arrow it'll copy back what we had before got it and this is why I don't feel the
need you're right don't need to comment Y yeah you just let's run it and and make sure we understand on just pick any
test well that test right there so what's going on why are we two not entirely sure why um we're getting double for each
but are we missing both artist and that's irrelevant so it's that's not the doubling from that perspective well there is
some failure there um but why are we getting double messages where the so when we're troubleshooting something like this
where's the what's look uh where the callers happening no what's generating those messages I don't remember where it is
but what's generating those messages because whatever is generating those messages that's where we would start so where
did those messages get generated what's what's generating those failure I this sure and go where's that coming from yeah
yeah so this is in song parser this is in column mapper is this test checking the number of columns let me go back to
the one songs artist song right I almost want to change the name of that from malform songs to two with well let's not
lose context no I to so what are you looking for because you you did a search which was great um but then you ended up
back here and I'm not sure what you're what else you're search I just trying to see the usage the reason I was checking
here I'll show you again is this result failure is are they both the same so this is in song parser so yes this is
something that that popped out for me is we have three different places where it looks like we're returning very similar
error messages right there's this one yeah which is extract column so is that one same that's minimum columns this one
is the other the other thing so let's go to the second the second one is that even uh when you say go to it like this
you mean yeah first song without header it's not called yeah so we've got some dead code that where did that wow that's
a lot of code that we just nuked yeah because we switched over to um yeah so if we're going to select SL delete we
propagate it all the way down okay because we no longer have this idea of a minimum number of columns that was what we
started with but then we decided to go to minimum uh we decided to go with required name column so let's search again
because that that was a bit of a of a red herring that that there were two places for that right there's three actually
I mean that there was three three code places uh change in project I don't know how it got flipped to directory yeah so
now we only have one place where that message is defined yeah just a column map right now yeah so that's that's
comforting that we don't have have it in multiple places yeah I was a little bit freaked out by being in two places
that's what I was looking at I was like why what are the yeah yeah so it was first important because I noticed uh so
bdsl mentions make the message different if they were both in use then then we might have done that um but since they
were actually was a red herring uh we had some dead code um so that that was wanted to eliminate so now that we know
precisely where this message is generated why are we getting it generated uh more times than we were before okay we're
getting array of row columns in what does header columns do not match so does it make sense for us to do this level oh
extract column is called multiple times so before it wasn't a problem because we were only pulling the failure from
artist now we're pulling the failure from song title and eventually we'll also pull it from themes right so every time
we call extract column we're wrong so this means we move it up out of column mapper and into parser the check well is
that what you're saying or I I'm all I'm saying is that it's at the wrong level I'm not saying where where we should NE
what level it should go to information so this seems like the responsibility of colum maer to say if you're G to um it
seems a little odd to say there's a mismatch but it column mapper is the information what's column mappers Constructor
look like it's got the header and the required columns and the required columns so column mapper is is is the right
thing in in terms of it's the one that should evaluate whether the header columns match or not uh so since we know we
don't want it being done here or sorry keep going uh or different so let's so where is this from song parser I'm gonna
move song parser above so we can yeah so it's called in parong it's called four right oh No 61 what's that that's it for
the themes ah right but it is called Fort fourth time fifth time well technically it's being called up to right number
of them up to seven times right or eight times but um so we need to sort of rethink how we want to enforce number of
columns bother do we really care about number of columns what you're saying because really we care that required columns
are there and that's sufficient well is it so the the the failure that this is checking for is we have five columns in
our in our header and only three columns in our data so it's a mismatch right yeah so it's different than required right
because if we don't protect against this then our extraction when we do uh uh the the parsing um it's it's just we're
going to bounds so we need to make sure that that basically we have a rows so that means that our extract our our check
here is valid um but we're checking the same thing every time we call extract column that you mean versus checking it
once when we instantiate the column mapper or somewhere around that something else other than what we're currently doing
because what we're currently doing is is is reporting the same failure multiple times and that's problem and in fact
there's no point in continuing for this kind of failure because we're never get it's it's never going to work so at this
point it's an exception not a not a well it's not an exception because it's still input validation but we want to in a
sense treat it as something as a different kind of failure which means it shouldn't be it shouldn't be an extract method
uh an extract column right so would there be like a validate type method be called once yeah maybe and then if that
fails then we just fail and bail at that point yeah I think I think that's what we want I think we want a separate um
column mapper uh validator something you know check rows and then if it returns a failure we just immediately return
that because we still want that failure for that row um but we only want it once and we don't method so let's um let's
do that so let's revert the change of the bottom because we now one quick question so in the par song the reason we're
getting multiple was because parong is called once per multiple times m per by the pars all and we're getting the same
error and over again because the data is okay okay reverting well I'm not sure that what you said is is is entirely
correct it has nothing to do with okay right we're getting multiple so we want multiple errors if there are multiple
rows that don't match the number of columns in the header but we're we're getting multiple of the same error because we'
re calling extract times right so line 41 extract column will return the failure of the number of columns don't match oh
42 do the same thing and line 43 and line 44 and line 45 multiple times yeah yeah I got it so we're going to get the
same is coming yes words we're calling this is so another way of saying it is this test applies for the entire row even
though we're extracting one column at a time right and that's why we're getting multiples and this should not be called
multiple times once it's sufficient right and it's a fatal failure versus a failure failure well it's a it's a don't
process this row further failure um because we want to we don't want to completely fail because we'd like to maybe that
was just one row that was errant and the rest of the rows are fine right um so let's run all the tests I'm not I'm not
thrilled with uh sort of so let's run all the tests again before reverting or after because I wan to I'm not oh make
sure there's no other well we were looking at the song importer test for a failure um and I'm not happy with the
distance that has to the to the it can we look at parse single song test yeah I think this is the easi this is at right
so this one we're parsing a single song we expect a single message we're currently getting two messages so we want to
fix that um but first we want to the I'm just trying to find something test there it is s parser let's revert this and
then move it back to the bottom so bdsl no that's not the problem we want to concatenate all failures from extract Colum
because extract column causes other failures like the column is not found so column not found we want to accumulate all
those the problem is is we're mixing up um per row failures versus per column failures so that's what that's what's
going on here um because artists could not be found that's a failure but we don't want to stop there uh song title might
not be found but we don't want to stop there we might not have a theme we don't want to stop there we want to basically
give you all of the validations uh at once all right so we should be back to all passing right okay refactor um although
I guess it's technically not a refactor um but from our test our current test point of view it's a refactor uh we want
to pull out um the the guard the check here we want to method oh right um can that be no it's a method ah okay I S you
hit the wrong no you hit the wrong key ah so choire yeah well let's call this what we want that what do you think about
validate columns match they're kind of similar um so I'm using sort of the the the naming conventions that um the jdk
use so like uh objects has check equal or check not null and things like that does maybe validates better because we
actually are returning a result so I'm fine with that actually because check actually okay that was a p factoring
shouldn't have changed anything from a test perspective yep still green did it extract that if length not equal null is
that what it did what oh what's this I mean I understand what it's doing that's interesting that uh that that's how it
extracted it I see uh I don't like that no that's weird um let's well now that we know the refactoring work let's let's
clean it up terrible so in which in which way well let's not let's rename the variable because that's terrible yeah
that's the first result and uh we only want to return it if it's the dreaded bang um but let's also yeah is that what
you were about to say yes uh and then we need to fix up where hi so we should just return a success what do we have to
put it we just have we've been doing that I I think that's yes uh so we can't return result void because if it does fail
we need to actually be returning uh something there is an issue around s success um having a success object uh uh but I
don't think we want to um since later on we're we're we actually do return the success value as an empty string it does
need to be an empty string so on line 31 we basically have the rule that if it's an optional result um to ultimately we
want to call this just once right right so now what we want to do uh is we want to make the method public and basically
have all callers call this one column we'll call it just once as like a B so uh is that what you're saying yes but
before we do that um what we want to make sure is uh is how our sort of what are our tests doing um so which tests are
calling extract column directly uh three in the column mapper those so that one is where we got an empty string uh so
that has nothing to do with columns mismatching next one uh symbol oh yeah no well if you're if we're looking in the
same fil is you don't do search for symbols I don't need to okay you can just do old school well you could do an all J
that's what I tend to do all J ah because it'll just select the next one and all we care about is the context so failure
when missing one required column so again this is about required column so that's fine uh so this is the one that's
going to have to change um because it's no longer the column uh in fact this is going to be the the method uh we want to
retarget it to the method we just created right so we would instead of calling extract column we would call the new
method that the validate and then make sure so if we just I'm G to undo the um the Alt J so I don't change in two three
places this one here you can just hit Escape yeah well Escape jumps back to the top uh oh okay yeah right so that's why
I did it the third time then use the mouse to click to get the focus here so needs array of columns right what it doesn'
t need is the name of a column because that's actually irrelevant and that should have been a hint to us that um that
maybe there was there was something not quite right because we were passing in a column when the message and what we're
testing has nothing to do with which column we're asking for right yeah yeah um want yeah we still don't we don't have
the helper for this one so it's still success is false right yep and failure message is still should still be the same
still be the same so this is generated yeah so this should just be correct right and it is MH so then we have to remove
the this test from here but first we need to have all the production colors of extract column validate first no that's
what we're look why we were looking at the other extract columns is they don't care about this they're not P they're not
checking that part of the error message so all we now need to do is pop out um is is really cut and paste this here when
you say you mean so inside and extract column pull out the validation up to this level extract column in column mapper
take out 21 through 24 oh so you're saying cut yep cut that yeah oh the result type is different right so we need to
basically transform transform it into uh a result failure of type I probably need to do multi-line we do results is it
result song no no just say messages and then that will convert it to a type result song Yes Should so now F10 yeah run C
so technically yes maybe we would write a a a success test for validate columns match um I don't feel the need to I feel
like it's very well covered by all the other tests that are assuming that it it matches we can try that out by basically
inverting uh the validate through mutation testing covered so if you put a bang in front of failures okay so that was
basically a refactoring for for most usages um one of our tests now tests the validate uh directly uh but now um now we
can go back and make that other commit uh do you want to check the tsv song parser I will I just gonna write the
sentence for the first two first and um um not great but I'll let it the brain Sizzle on that one what are we doing here
well we deleted some dead code we probably should have committed after that but that's all right yeah but validation uh
I think that's redundant because that's what you said in the first line so really the only thing was we added a test for
sure it all right so now we can go back and uh we haven't done anything here because we actually haven't touched the the
yeah uh have we we haven't finished that because we don't get the failure message for that right okay so that's what we'
re about to do is re uh reenable that test which just this so this should Now fail because we're still not returning the
concatenation of multiple yep persective two size one now let's now we can redo that fix right the verbose fix is that
still the right way to do steal uh so you picked the wrong option you picked selection but you didn't select anything oh
I didn't select if you want to use that you can select the area that you know the change 56 go so now they should get
the test to pass does I don't like how big this method's screen for some people that's that's their maximum I agree it's
it's uh it's it's a bit long um but it it passed our our new test commit for all right so you're not happy with the
length this method what should we do about it yeah I'm wondering if this could her or is it just going to be a big I
don't know that's the first thought that came to mind um I feel like inline this would be a bit too chatty say again I
was thinking if I inlined uh result into 42 I feel like that's a bit of a well you can't because you use it twice so
that would be oh it's used elsewhere you're right you're right yeah so yeah the only idea I have at the moment is this
do you think it's worth it or do you think it's um I think we have a bit more work to good so um and this is part part
of this is because we're uh using a result class that isn't sort of fully functional in the sense that um sort of a a
more functional approach would basically have all of the code and from 46 through call and so what it would be doing is
is as as as you're Bas in a sense you're you're passing one result into the next one and then into the next one and sort
of carrying it through and so what you end up with is a single result object with any accumulated um failures um the
problem is is accumulating the the successes is not uh is there's no good way to do it um because they're it's not like
we're streaming across stuff we're actually pulling pulling things out out so um so there's kind of not not a not a
great way that sticks out for me of of doing this other than um creating a map of string to string which is artist you
know basically the the column name to it data and then when we create the song we map so as we sort of iterate through
we're just doing extract column right because one of the things that that I look for uh and this was a lesson that JB
reinberger nailed into my head is what's unique and what's duplicated along lines in this case 46 through so there there
only two things that are unique um the header right so the string at the end um to so if we EXT if we used a different
result class where what we get is we extract basically 46 through 50 into extract these columns and we give it a list of
column failure then um then we can just say is that result success if so create a song map but um I think we need to
finish up the extract themes uh before we before we go down that road and then later on when we introduced the newly
discovered dependency for a release type that's going to make it even more interesting yeah well that will um the map
approach it will it will will help when we have a method that that mean it help it'll help because it'll it'll be a a
more specific method that that basically is just um parsing uh parsing it into basically converting it doing that would
be our first cross column dependency where release type right if it exists and is of a certain type then release title
must exist validation yeah I mean we might I mean it might be easier to just do that as another initial validation right
rather than trying to extract columns we immediately validate that that up front because again there's no point in doing
anything else it's a trade-off right because if we did the validation at line 45 to say if you have release type you
must have release title then uh the the tradeoff the benefit there is we immediately stop and we don't bother looking
for anything else the trade-off is if you're also missing artist you won't find that out right um but it does make it
does keep column mapper only about mapping only about columns uh and that's all we'd have to do for requirement so what
do what do we want to do the uh this requirement okay just talking about for now okay all right um unless you think
implementing it will ensure we don't box ourselves in the corner later by our current design you always Bo yourself into
a corner with any design and then you refractor your way out yeah true that's why it's that's why it's uh evolutionary
design um I think we can check off 78 though J 78 completed um do we want to fix the failure messages and then we can
handle multiple themes probably should okay get that out of the way let's do that control shift alt n n really because
it's control n which you should know fairly well because that shift so it's just modifiers for the other ones yeah got
it I was yeah whereas action is a actions but actions is not uh looking through your code so it has nothing to do with
your code yeah okay uh do we have a single failure of this so this one has two failure messages and I'd like to change
one that has single messages didn't we pull out that in yes that's the one so what would we like it to say we'd like it
to say case well you're the you're the you're the customer with your customer hat on what do you wanted to say well at
this point we've got artist and song title and requirement is a theme so it's really not about number of columns but
that's what this test is testing about it's testing columns it's explicitly saying with not enough columns so what we in
the so the the column headers are irrelevant it's just there's a mismatch between the header columns and the data
columns so it's really a mismatch it's columns well it's for a it's for a row with not enough columns right it it might
be more clear if the the sample data we use has nothing to do columns because that might be misleading now I'm confused
well you said um but how can we have sample data without required columns because wouldn't it not even wouldn't it fail
because it's missing the required columns but the check of of column number mismatch is done first right right I mean we
could leave it this way I'm fine with that but you were initially confused about the required columns when this is not
about required columns right this has nothing to do with required columns yeah I was just wasn't sure but we still need
that test because we still want to check that there's not a here right so the the question still is what do you want the
messages to say because we found this message confusing because we weren't sure where two or three were coming from
specifically we're un sure is so write write write sketch out what you'd like as in writing because it's hard for me to
track when you're yeah speaking it out loud you can put as a comment above well I was gonna just do it in the in the
message because you asked that's fine look like I just thought a comment might be easier oh number of columns of two
must have at least three um something like that would that be helpful because we're looking at the names yeah I think
that's good I think now the problem is that uh the two is very distant from the data yeah oh I was suggesting going the
other way okay so what I tend to do in in my error message is tell me what's wrong first and then give me details so the
problem isn't the header rows that's the row so would you have it before the two the number of columns or after uh I
would put the number first because I'm otherwise I'm G to have to scan out something along that line I'm not quite try
how to punctuate it um I'd probably sure well it's not have at least it's must have columns matching because it can't
have I mean it could have more but but we're looking for a mismatch yeah I don't think you need the colon in front of
two oh I think it's a good start okay yeah if you're gon if you're gonna have a period there you're going to have to
have a thing yeah so the problem uh is that there might be eight or 10 columns and telling the difference between nine
and and 10 is going to be very difficult so this specific test is using two and three but uh there are scenarios where
it's much more than that yeah yeah sweet okay so run it and it should fail okay do we know row yeah you're just moving
the col moving it around yeah yeah so remember to delete the brackets because we get that string so the first s is the
last arrays to string thing yeah s now this we have to do we even have that no that's header columns right we have that
right there I don't know where you're going we have heter columns. on line 35 at the end so you want to raise the string
of headers columns ah so we want that keep that and then we want to parameter uh I think header columns is why because
it's a list so we can just yep let's see if that works we expect the other tests that use this to fail but what we're
looking to see is if the current one is passing which is this one bottom let's do a yep so now that one passes right and
now we expect the other ones to fail because me so you think just and is it easier to pull from here uh I don't think
it's easier to pull from there because that together well still gonna no no no you you've already copied it with quotes
so you don't need the quotes good yeah just turn green yep and do the same thing for that one this one are we really
another hour yep time fun so you could have just copied it because it already had the correct output oh sorry let me
undo it what were you saying copy I'm just saying you can look at the the error message the right right it's already got
the the right output and you don't and and you won't quote then you can just select select increase selection control W
one more time delete and then great there we go commit then break yeah that sounds like plan um this was just clean up
error error right all right we'll take a break uh and then when we come back so we can check off 79 and 80 we'll
basically have to handle multiple themes sweet so we'll do that when we come back from the break see and now we know
about persistent TB is now much lower than 30% yeah so there's a thing in in uh in baseball games called uh uh get
exactly what it's called it's win win percentage likelihoods basically a graph as the game progresses you know somebody
gets a home run increas so basically it's who what's the probability of some someone winning um and if it's going down
the wrong way you know your team's in bad shape and so uh slowly as as the couple of hours have gone by the likelihood
started low 30% has been going down now it's pretty much zero we need to make a plug in for that yeah we should and then
you can have wager wagering on on on that although that's not legal in California all right let's take our break and we'
ll come back and do our multiple themes handling sounds good e so as a reminder uh if you're not already a member of our
Discord Community uh go to ted. Discord and join up it's free uh it's a great place to ask questions about basically all
the stuff we do here here on the stream both uh this pairing stream and and the solo streams that I do so test driven
development design refactoring uh intellig shortcuts all that stuff uh there's channels for all of it including exagonal
architecture and domain driven design so all the good stuff that helps make your code more more testable so join up the
Discord um also announce uh when uh we're what the streaming schedule is so can find find out more than just when you
get the go live message uh you can find out in advance by uh looking at the announcements Channel if you go to the rolls
Channel you can select that you want to be notified and pinged um when I do announcements relating to uh going going
live um because I don't ping everyone because that's annoying um you can also find more about me uh go to ted. Dev about
uh and I do just like I uh I do the same kinds of things with with individuals and teams coaching uh to help make your
code more testable um so working with Legacy code making it more testable um introducing test driven development as
appropriate mostly focusing on refactoring uh and ensembling to to help introduce that and my tdd game um check out td.
cards as the site and you can uh watch a video that I did uh at the agile lunch and learn where I walk through
predictive test driven development which is what we do here on stream and uh then I walk through the the board the board
and card game and uh it's really fun lots of lots of people enjoy it and uh I've only got a few copies left in in stock
so if you me too handle multiple themes so we can uh close issues 79 and 80 oh yeah JRA 79 closed JRA 80 closed I like
that we still giggle about that yeah so that's at the column mapper level I annoying so actually since this is at the
individual column level there's nothing to do here yeah I say I'm not themes um are we not testing for multiple things
well let's look at uh let's look at our tests yeah I'm G try that other one was it control shift Windows uh it doesn't
go to the test yeah yeah it's class name based so par songs if I remember correctly is a nested columns want to rename
just get rid of the returns yeah while we're here y value result for a row with not enough columns sucess I love less
less words in a m method name a row with required columns order this one we need the one failure message one recorded
two failure messages when missing two yeah so we're not doing much in the arena of themes so what are we actually themes
is it just that we've not tested having multiple themes uh I'm pretty sure we've tested for multiple themes um we're
probably themes code all right so when we parse an individual song we don't check for any failure um on the them so if
we are I think it's we're not Che so if we're missing theme one basically if we're missing themes we're not checking for
that right because here we extract theme correctly uh unless we have an error so if we've got the themes we extract them
correctly if we don't have any themes we're not checking for that we don't have a test for that so we need a test for
that and again at the song parser level yeah just add it at the end sure okay what I want to call this one um faure when
missing them now we're doing at the song level one you have to have at least that right and so if somehow you have only
theme two that's not good enough you need theme one and if you're gonna have a theme two it requires a theme one so
theme one is yeah it let's go farther up oh that's an order one now it's too well that's fine too because we're going to
pull out theme one anyway unless you want to go up one go up one more and grab one that's in the correct order yeah I
was goingon to go theme oh wait a second we wanted the header you want it missing in the body no because then that would
just be a a mismatch of columns we want to say you don't even I didn't include that column right you you forgot to copy
that column from the spreadsheet got it so yeah search failure we could start with that and then build it out right so
that should oh we actually don't know what it's gonna do I believe that will fail because we're not checking for
failures because extract themes just returns a list so we're going to get we're going to get a uccess right so it's
going to fail to fail it's going to fail to fail yep yep should not have succeeded but it did uh I'm going to be
annoying and uh have us fix the grammar on that that's not going to be a symbol that you're going to want to do finding
files oh that's a Str touche uh can we put a comma before the butt should not have succeeded but it did yeah I'm now
wondering if we should flip it around uh succeeded but should have read yeah the IT thing was bugging me yeah always
keeping our error messages readable and incrementally improving them all the time it's like whenever I type the word it
I have to have this I need to have a heuristic going why are you saying it what how can this be changed yep yep seem to
do that more frequently than I would like okay all right pass so this returns a list not do we just check for an empty
list or do we have to have a guard within extract themes and then extract themes returns a list I think we're going to
you here in this case there's no themes or theme one is not defined but at the moment there's no themes defined um or
should this I think no it's different no no so the problem is in in the in we're basically 67 and we don't want to do
that anymore what we'd like to do is uh Group by can you just go before you go into the details of group by just high
level what are you thinking what we wanna what we want to end up with um from the overall map um that Maps basically
booleans so the the map will have two entries in it one for the results of failure and the one for the success um and
then basically if if the failure one any that would apply for any theme so would that still no because not all themes
are required so the only one that could possibly fail in other words give a result that is a failure result is if theme
one isn't there and what about we decide for theme two three and four could it be those become empty those become empty
oh sorry can you jump can I could the spreadsheet be something in theme one nothing in theme two and then something in
theme three we currently allow for that yes we do okay right because what we do is we just filter out any so since two
three and four are all optional um if they're not there we'll get an empty string and we'll drop them up from line on
line 69 got it so it can be theme one and then theme four we've said that that's okay um what we can't have is theme two
and theme three right you have to have frame one you have to have it you have to have at least theme one and then
everything else right and I'm just let me just check one more thing why what about I mean I see where you're going with
trying to do this within extract themes and with the stream within extract themes um I'm not saying it's the only way
it's a way it's a way I'm just wondering if it's in a way late uh uh because if we said let's just say in 44 and a half
we say you know column mapper must have theme one then that would be treating theme ones because what we want is if you'
re missing artist song title In theme one we want a failure message we want three failure messages right right right
right um where I thought you were going was in extract themes we could do upfront a a check a check for theme one right
and then would we then change the return type or the list of string is empty it just means that no I think we need to
change the return type I think we need that result of it's going to be a result of a list of string yeah I I because we
don't because it's just a su it's just a type so it's it's in the sense it's a result of list which is fine um but we
yeah so we're gonna need to to to change extract themes to be result of list of string so you should probably do that as
our first step right we just do it by um declaring it that way at the calling Point here and then have it autofix or
will it auto fix um I might change the the the return type in extract themes first and then uh gotcha actually I might
even change the no sorry uh what I meant to say was I would change what's what we're actually returning and then cause
it to propagate from there oh I see so we go to list um when what we really want uh I was going to map it but there's no
point in doing that so let's let's pull that into uh a variable and then we'll we'll change the return that meaning
where your Cur themes uh can you move your mouse because it's hovering over something at the bottom oh yeah thanks um
and so now we want to return is not themes but we dot uh right now we're assuming success themes why is it not happy
because our return type is now wrong oh great what we were trying to do yes uh so second yeah oh it didn't uh propagate
to the caller oh I didn't I didn't expect it to propagate that far ah okay because it signature yep is that right now is
that right is actually the is is is result string going to work for us um can we go open up result because I for so
values is already a list so when we do a success we actually can pass in multiple instances oh so we don't have to do
result list of string it's just result string it just happens to have multiple fine so let's go back to the parser and
what's the problem so that we just need values line yeah so this is the only one where first uh yes this is a custom
result class that we wrote a couple of episodes ago or a few episodes ago several episodes um are we compiling out nope
oh no compiling but failing so how are we failing uh was the test we just wrote yeah but yeah can we actually look at
what the failure is meaning here issue now we've seem to have mixed up the doing set and why are we using a set in our
result class that go to can we go up to our remember I mean I can see making sense if we want to ensure that it's a set
of um The Constructor is expecting a set too yeah because we assume that all unique is that a correct assumption do we
because set is not going to preserve order we I think we actually do want to preserve order uh so I think so let's um
let's disable our current test and let's refactor uh I wasn't going to bother typing a comment because this is not going
to this is gonna be on hold for a short amount of time so just just disable you could leave the comment there okay um so
uh let's go revert the change that caused the parser so let's just ref it well all right so let's change the result from
set to list and see if that matters can we just refactor it uh no I think we'll just manually manually change that to a
callers oh interesting so we just want to say list of here yeah I was only I'm surprised it option y I think that should
be yeah it looks nope what's going on here oh that's why we did it we were cheating so we needed that's why we did we
needed to differentiate between uh oh different Constructors Constructors that are you can't um is there a different
kind of list or you can't differentiate even if they're in the same hierarchy no if there were different it um but that
would be really awful right so I think we're gonna have to bite the and create sub classes in our result in other words
one for each of the two types of results yes so we're gonna have an abstract so result will become abstract um and then
we will have a success result that takes a list of success values and a failure result that takes a list of string uh
and that that way each one will have a Constructor that's correct and we won't have a problem because there'll be two
different two different classes should we revert back to um using sets and then refactor well compile of course uh I
would revert do a local history and revert and go back in time for the whole class or you could go into the commit
dialogue and do a revert there either way well I'm here um so click yeah this one or this one yeah that one is fine the
one's currently selected is fine then just hit the revert button in the upper left ah there it is y so now we should be
back to well failing no we should be back to green because we we disabl that test right right right okay yeah so vagan a
the the problem is that uh we want two Constructors one that takes a list of success values and one that takes for
failure a list of failure messages you can't have two Constructors that take the same arguments which is what we TR just
tried to do yeah that was our that's why we did way back when yeah so so the fact that the first one is is uh generified
with success and the second one is generified with string you cannot overload based on generics because generics uh are
don't exist as far as the compilers concerned so um due to type eraser you can't have two arguments he n no we did not
start persistence and we will not be starting persistence today uh the the odds of of us getting to persistence next
time are probably around 50% uh the problem is is ultimately we need real Constructors that have that take different
things um we could always pass in two parameters the the success and failures and and check that one of them is null or
the other one is not um that offends me and yeah I mean we could add some some arbitrary uh other parameter and we
talked about that before and and we had forgotten that that's what happened we could add a Boolean saying he a success
for failure um that offends me as well uh so Factory methods did not solve the problem we have Factory about this the
problem is we need a Constructor uh we need two Constructors that take lists the lists are of different kinds but they'
re still lists and so the compiler doesn't care um I mean we could take an a we could use the do the Boolean as a small
step towards uh towards sub that would we extract to or sorry what were you gonna say I was gonna say what are your
thoughts on that oh um I'm not sure I see how that plays out um I'm still just thinking about how we would we would
extract to an abstract Base Class well before doing that we could add a parameter right so consolidate I me I meant if
we didn't do the parameter thing I mean either way we're going to have to make result be abstract and then
implementations uh basically that are that are Nest that classes well right now they have proper values we're
initializing them in the field decorations so by values the idea is not to expose the type of of result so I don't we
don't want to be exposing failure result and success result to clients of the of this nested right and so um yeah so so
how would we proceed this the part I'm a little bit unsure about how we would move well so again do we want to um do we
want to cheat uh and and add a Boolean flag or do we want to just go straight to to does the cheat help us I guess is my
question not really then no I mean if it helped with the um yeah so we're going to have to pretty much apart so we need
two Constructors because one Constructor is for the failure and they both must be result and we want one type that
callers can count can count on so to be honest we we we we've been writing our own result class with sort of just enough
um there are more proper result implementations that do a lot more work uh that um and if you look at any any sort of
more real implementation that that sort of take their their hints from from other result implementations they do have an
abstract Base Class of result uh and then subclasses that are specific Success you're bringing that up because it might
be the time to um not write our R result class or were you more no I was just sort of pointing out that that that that's
that this is that it's it's unsurprising that we're going to get to to where we're going got it okay let's start ripping
what do we do um so let's uh so let's make results abstract is it before and after and Java before yep not replace yeah
there we go and uh let's rename 14 that Constructor we'll call that uh success result oh rename not just type uh no just
type because we're gonna it's gonna cause a compiler but that's okay uh we want then sort of make a similar change to 19
call that failure result um and then let's Constructor result um we want to generif that uh so so we're not all right
you can wrap finish wrapping it and then we got more to do yeah of yes um and what we want is we want to grab line there
and sorry paste it into yeah cut it from class um let's try this there's probably a better uh actually no let's delete
line 10 because we're going to Define that differently um let's method um we're going to make that abstract it uh
including so it's an abstract method so no curries ah right semi but you'll need a semi will this move up what's that we
move this up uh let's now um so now let's define uh is success in class so let's delete 17 and then and then override uh
o oh you could do that too that's fine okay uh so we want to return true because for the success result it's always
going to be true right let's do the same thing for for values we're going to make it abstract abstract I knew something
didn't look right um and again sort of hollow out uh turn delete all the implementation and we'll go ahead and class
values uh I think that's it for our success result so now we're going to do some similar stuff to our failure results so
class success and so we can delete 34 and then we can override uh the other two correct um Val is interesting so we're
going to want to we're probably going to want to change this going forward but we're going to not do the full
implementation just yet so let's just return a new array list or actually uh empty list we shouldn't even instantiate
anything lower Casey yep take me a second y uh you got an extra print there because they're fun um and we want to take
the field from the top level class for failure messages and move it inside the so yeah 10 failure uh and now we can make
that well and um we want to for the failure there's a well and you can copy that implementation because we're going to
that and let's go Implement that in our failure and we'll have to also success what was it called again pay your
messages you can just hit control o or or do that control method yep yep uh let's go back up to let's uh we can make
line 11 we can make that final and then we'll override the one override which one again uh failure messages the only one
that we haven't and here again we'll return an empty list I think that's it for the implementation um so now what we
want is now we want to become no no you want to leave all that it's the same thing it's just instead of result is
Success result oh I see just it I think that's it move these up now uh yeah you can move those up um no actually sorry
leave those down so move the basically move the static Factory methods to the top see yeah well did it did we do it such
that it auto change the cers the callers shouldn't care we've we've we've done a refactoring right a manual refactoring
a manual refactoring but it's still a refactoring we have not changed any external behavior um and now we can see if can
we change those uh all those sets to to be list so that should be list of and the yep so this addresses full no's
questions of why why do we need two Constructors because um as we can see online uh 13 technically 14 we're calling a
Constructor that takes a list for the success Branch uh and line 22 we're also passing in a list um previously we
couldn't tell the difference between are we passing in successes or failure because they were both lists uh so the way
we cheated before was we had one take a set and one take a list and that was a way to differentiate the constructors but
that's really bad as we just found because sets change the not so that cheat bit Us in the butt yeah so the cheat worked
fine until it didn't which is how everything works until it doesn't um so the error is it just simply wouldn't compile
because you can't uh you can't have two me two methods Constructors whatever that take collections even if the contents
of the collection right how they're generified is different types because generification goes away so the so the jvm
just sees it as it just compiler sees as two two methods that are overloaded with the exact same type right which you
can't over you can't have that right right that's why the fix fix of putting a Boolean at the end yes one of them one of
them would be true yeah so we could do that we could simply add a arbitrary dummy parameter to differentiate as well but
that's ter as well um so this is the correct way to to to do it and then there's some cleanup we could do in addition
but this is this is uh basically we've refactored the the result class um so asks about uh prefer abstract class over
interface um so the thing about modern Java with interfac is you can have default implementations uh but what um I I
personally think that that that was a language mistake I think that that was done I understand why it was done because
it was the only way to to deal with collection classes and the stuff they want to do with collection classes uh of which
there was a lot of interfaces but I think having TOA default implementations of interfaces broke the entire purpose of
interfaces which were purely that abstract class is is a much um more intention revealing way of saying this is a
partial implementation uh some languages call it a partial class right we've got some implementation and you have to
fill in the rest um and I think that that's to me I you know again though I've been doing Java for 28 years so I'm going
to of course like the one that does it the way I've always done it but I I think using interfaces and defaults um
because defaults get become messy I think I want to ask a wait what question yeah um so in Java and interface so for me
an interface cannot have an implementation and an abstract can and no longer true that's no longer true so interfaces
can have implementations now they've been able to have implementations for a while now for a while yeah oh that's weird
right right so you w to be so you want to use abstract basically since Job okay wow it's been a while yeah so abstract
is the reason you're choosing abstract because it Maps into the definition of what an abstract class means right dep
dependent of language yes okay I'm I'm with you and I agree um yeah so if you look at the implementation of list you
will find a default method called sort that is actually has Behavior it is an implementation um and I think that I
understand why they did that I think it it I pret I like to pretend that that is something that jdk libraries can
Implement and that I do not um they did that for backward compatibility and for other reasons having to do with
introducing lambdas and streams and such um but I I wish they had found a way to do that that only the libraries could
do that and that nobody else should do that because if you have an interface and you have default overridden it to me it
just mangles the the the the the purity of that interface MH yeah and the whole idea of of why you could Implement
multiple interfaces because you could be guaranteed there was no implementation so you wouldn't run into the the
infamous problems with mess yikes um and I just like to pretend that interfaces didn't do that yeah so um does PHP have
an an override annotation is that part of the language I know in Java you you include it because if you if you don't
you're fine but then your compiler won't complain that you're not overriding um so that's why it introduces it so full
uh mentions this implementation which is uh has uh first of all looks very much like cotlin um but it does indicate that
there is some additional things we could do to make the result nicer uh first of all we wouldn't use a throwable as our
failure result that's the whole point is we don't want exceptions uh we actually just want failure messages um but we
could make result a sealed class um and what that would allow us to do is to make sure that nobody uh other than inside
here nobody else extends and uh and implements a result um which I think would be kind of that and what we want to say
then uh and usually I see it on a new line so basically for the opening brace on a new line permits yep and then uh no
the opening brace will still be on the same line uh and then we want success result result really I have to type it I
wonder if it's not visible enough now it's got it there go took a while oh it's result dot comma doesn't seem to like it
though yeah because the sealed class subclasses must be uh final and that's fine so let's make failure result final and
let's make success result final there we go and let's reformat that a bit Control Alt L yep so now what we've done is we
basically said um and this can help in some cases uh especially for exhaustive now so let's see uh success result has
final so that's okay uh so there's something with the permits that I'm not familiar know about that mean it's a good
breaking point for this uh I think this is a good good stopping point yeah uh so let's do a commit and then good we want
to mention it's because of the set um or just put that in our J yeah um yeah it yeah I mean if you're going to allow
interface to have implementation you got to allow private methods actually wait a second if we enable this test now uh
oh yes will this pass now yeah it should because they no longer right because we're passing in list so order well it
wasn't this it was it was that um we changed it to to uh is that other test we're we're failing right so this is this is
still failing so but that's actually yeah a good bread all right um so that's all for today uh next time we will um
handle uh the required theme and make sure we we propagate that failure um and I give it a 50-50 chance that we'll get
to persistence next time and we and I think we decided to skip yeah that sound like you wanted to to to punt on that I'm
kind of like some of the folks who are watching Keen to get to persist to datase um then That's all folks uh so uh next
time we'll um I don't think we have anything scheduled for this week so it'll likely be next week um at least for
another pairing stream so next time we'll uh we'll finish this up and we'll then move on to persistence and so as a
reminder uh join the Discord that's where you'll find out about when we schedule as soon as we figure out our schedule
uh I post it in the announcements and uh there's other stuff to do in the Discord as well um so I'll probably be doing a
solo stream tomorrow uh and after that we'll we'll we'll see how it goes so thanks everyone for for the great chat and
and hanging out yeah Mike what you want to say oh don't me to push even though we've got a failing test yes please push
okay uh because I want to ask chat GPT about the result class okay done all right thanks folks thanks for hanging out
thanks for all the good questions um always appreciate uh questions and some of the help that we got from suiga earlier
uh yes the repo is public um I'll Post in the the Discord uh where uh the link to that so That's all folks so thanks a
lot for for spending some time with us on time
