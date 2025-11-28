# ＂Song Themes＂ Episode 33： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=4rG7Im2DdKM

---

## Transcript

all right welcome to uh episode 33 of uh pairing with with Mike on the song things app how's it going Mike good good
been a while it's been it's been a while yes I think I've been immersed in trying to get my um vegetable garden planted
you how there's time sensitivity on that front so yes yeah well hey at least at least you're not using GPS PS related
tractors which were uh apparently um the solar flares that caused the beautiful uh Northern Lights also cause major
problems for some of those uh fully or partially automated tractors they couldn't they didn't work because the G there
was interfered with the GPS and they wouldn't work without the GPS do they not work at all or do they just create like
weird like crop circles they basically could not use them wow yeah yeah um y so yeah watch out for automation yeah a
friend of a friend actually has a 700 Acre Farm down uh near I guess Watsonville broccoli farm and they use GPS of the
tractors to lay the roads out nice straight wild yep hello estd hello Sue um yes I uh twitch over the years has has has
never gotten that reliability of like um uh sometimes it depends on how you're expecting to be notified like I know uh
if I'm on my iPad uh if I haven't logged in from the iPad for a while then then it won't send notifications um but this
is why I always make sure to do notifications on the Discord so uh that I know works but then you got to make sure
Discord is set up welcome swegi swegi and yeah so alarms are intermittent which is why uh why I try to both SCH announce
it in advance but also then announce it uh on on the Discord so join the Discord if you're not already a member um tag
the roles for uh getting notified about the Cod stream alert because I don't ping everyone uh I ping the Cod stream
alert um so that's the way to do it so uh it has been a while um last time crumbs yes yeah keep going what youon I was
gonna say so last time we we we we fixed up some some issues with with the bulk Import in terms of validation um and yes
we did leave ourselves uh a breadcrumb so let's take that clearing switch to here here we go cool I just ran the test
they all passed awesome um and we've got this three greater than symbol red crumb right uh so um we also wanted to uh
eliminate usages of the create column mapper that took a string I was wondering why we had this here and do we want to
just do this get it out of the way uh yeah so we had the the the hetero stuff was part of our previous stuff around
error messages um this is part of the refactoring uh sort of the post refactoring cleanup so um I remember we wanted to
eliminate it because it's only used in tests yeah so we wanted to look at uh what we should be replacing it with um
because we should always use the create that returns a result which is the one yeah just the straight up create not the
one called yeah create column mapper so why we why don't we do that sort of get warmed up by by by doing that love it so
let's see what do the tests look like I just grabbed the first one yeah are they all in the same class let me so what
are we doing here empty string exist optional column does not exist right so the column so in this case uh the column
mapper will succeed um so we could just uh so one thing we we could do is we could just say that this create column
mapper that we have uh in our production code um um I was thinking do we want it I don't think we want nullable I think
we could just put it in uh uh as a test helper in other words move this method into a test helper class or into one of
these two test classes own it either way um just get it out of production code but get it out of production yeah but I
don't think we want to because if we call the crate directly then we're just going to have to do what we're doing at the
bottom of line 33 and pull out the success so we may as well so we'd want to probably wrap that anyway um so I I think
we should do that sounds good let's see if we've got um so two tests are in column mapper test and three are in tsv
parser test we just uh pick based on number or do you prefer to make a separate class um let's just take a look at the
tsv song paral usage I'm pretty I'm assuming it's pretty much the same yeah it doesn't even in line so I I don't I don't
have a strong preference um I don't either frankly so let's see so let's just make sure so this one is uh failure result
for row with not enough columns um so here we've got uh those the three required coms I forget what our required coms
are yes artist s and okay right so this has the um the song only has two but the the column mapper is fine okay oh I
just sorry yeah tangent but finish your thought no I was just gonna say let's look at the next test so so okay so I
vaguely recall and let me just grab the that I think there are some songs that in the spreadsheet don't have artists oh
so that's going to be interesting let's see well no maybe uh maybe there is usually there's like a thing called blanks
oh blanks there is blanks yeah well then so that's probably that's definitely a data entry problem it was probably like
I was gonna say I made a mental note like remember to figure out who did that song or this one has multiple artists yeah
so never mind okay I wanted to like I said back in my brain actually what's this question mark one too what's that oh
Plant versus Zombie video game music right who is the artist I have no idea but maybe we'll just have to do a standard
of like you know unknown or you know something where you don't know the artist I think that yeah I think that that makes
sense yeah yeah okay are there any other weird ones let me just I think it's mostly question mark and blanks and I did
use the word unknown I just noticed that when I was skipping by um data unknown and oh various this one's gonna be
interesting one I'm curious about that and what else we got who so let's see what some of these are ah okay so this one
would need to be broken out so this is a double CD of poems of Edgar Allen all of them count as Halloween right I just
didn't do the data entry on it right you just each one same with this the the various songs right from this compilation
right same with Harry Potter themes okay right so then the who probably heard the song but I even figured out who does
it um and question mark well we'll figure it out okay cool I just wanted to make sure we weren't boxing ourselves in in
a bad way but I think it's I think it's a legit approach that we're taking so okay yeah not the who but but we don't
know it's not guess who it's we we we know H band names yeah um so uh so this one is fine can we look at the other
usages in our tsv song person test success Ro right so in fact that one is the same as the other one which is create
sort of minimal column header or minimal valid column header or column header with required columns or something like
that um and the third one usage yeah same thing so I think uh I think what I would do is um move the method to the
column mapper test and then extract another method for these tests because they're always just creating here's the
minimum required column kind of thing got it so well let's do the first one so that's move this not rename those two
backwards um but why they're so memorable F6 come on uh and we want to move it to column mapper and there anything else
we need I don't this used oh was just saying it's used by not that it uses ah okay cool so we just refactor yeah and
then it'll escalated to public because there's usages across two classes yeah it's already public so it here where it
put it probably the top oh interesting of course at the top that's where yeah just making sure everything's still
working we're good yep um and then for the other one you were saying instead of do you want to inline this and then
extract a larger what were you saying about um yeah so I I think uh if we inline the header and then extract the entire
call into uh a better named cre method that's what I was thinking so is the header the same for all three it should be
because that was that was why I was looking at all of them because uh that's what you were checking I was checking to
see that they all had the same basically the same header okay so in this case inline them all in um to make them all the
same although no because this one has the columns in a different order and that's I I I was thinking oh do they all have
them the same order uh so let's not do that then um I think let's leave it uh let's leave it as is actually the there is
one thing I want to do which idea because you know yes in the future we're gonna be like yeah oh let's just inline these
all together they're the same they not yeah um I think the first usage in in this in this test class whatever that first
usage was you won't yeah not I'm just gonna search it for fine this one yeah that one uh let's extract the header like
like it is in the other test so that it appears above the song because that was exactly a so artist unknown is a band of
course ah of course and unknown T is a right uh let's move I don't know if you're going to do it but move 176 above 173
yeah I was wondering what you thought about that yeah that's why I left it yeah what I want what I wanted was like sort
of simulate you know because when we're reading this what we're saying what I want to pop out for us is immediately like
oh the header has three columns the song has two this is clearly uh uh not not a happy scenario right and then here it's
three and three ell yes naming is is definitely hard especially for bands I think I've mentioned this before on this
particular stream but Spotify really annoys me in the way that they don't disambiguate bands with the same name so what
happens is then in in like the they do this discovery weekly where it's like hey here's new stuff from artists that you
follow I'll be getting like what the heck is this and I'll look at it's like oh no that's not the Asia that I follow
this is some other band that happens to be called Asia that is nothing like the the band that I am in particular want to
hear from so it's like that's what unique identifiers are for these are entities why don't do they not have unique
identifiers what is wrong with you I don't understand it data modeling all right I assume has a somewhat a different
problem yeah is that sometimes the same band has multiple entries for no for no apparent reason or for no apparent
reason okay like I could understand okay maybe they have different instances because different lineups or something like
that right yeah but yeah if it's random then like what NE neither one is good no but it is interesting as like you know
what is it um uh the's ship is like is it still the same band like yes is that still the same band they've like gone
through so many changes like is it really still the same band I heard speaking of on the radio this morning the DJ was
announcing that the Kingston Trio very famous Trio from the 60s was performing at the UC theater and um he said oh and I
don't know who's performing because as far as I know all all three original members of The King and Trio no longer are
alive right so it's like I don't know who's performing but they're called the kingst and Trio so maybe it's their kids
or kids's kids who knows that's funny all right uh let's do commit since we did that clean up yeah and we can check off
the J too um J all right dopamine hit jur 105 completed all right it's a smaller amount of docine than usual but we'll
take it hey a hit is a hit um so so I think this is more about uh because we we literally just saw a test I think for 10
109 yes um that was which was in the tsv song which was one the one we literally yeah I think I remember seeing them in
play grenwich Village at some point really yeah yeah I saw them in San Francisco that was a while ago um by definition
so this one uh so this one is giving us a failure uh because I think our goal was we don't missing so in other words if
we had the same situation for the header but the song had just blank entries for artist and and theme that was the
scenario do we want to write the test and see what it does yeah I'm actually where's jir there it is so you're saying
this one's covered basically by yeah the test we're just looking at even though it's actually missing the theme but it's
still missing one of the three um and then this one is missing two of them right so the the current test we were looking
at we cloned it and then uh is green eyes the song title or the theme uh song title okay do we want to put a back SLT at
the end to indicate that that it's sort of blank on purpose what happens when we do that yeah I wonder if that's what
we're checking for or if we're just checking that there's not enough columns because those are two different things yeah
ah okay so then this test does not cover the situation that we're talking about this is literally there's not enough
columns which is what the test name says so that's good right um but this situation okay so I thought we covered this
yeah and this is situation is more likely to happen right right you're you're in a copy of a rectangle so yeah yeah um
all right so let's uh let's should we UND undo that because that test I think is useful but not what we're yeah not what
we need to check so just clone this one um and then modify it to do the failing test we just had yeah I think so let's
see is this success for R okay probably an okay place for this uh now the name is failure result for row no required
cell not column yeah y that right F result for empty required cell one well let's get it to fail and then work and then
figure out how to make it a little bit more jumping out as to the distinction you know I mean from a browsability yeah
I'm wondering abil I'm wondering if you want to drop the the song title instead here and put in the theme oh that's a
good idea that's better um yeah so what would be the theme for that besides green eyes because that would be confusing
no it was the theme for that one is cats just to grab real data so like that yep so now it should still fail with a
slightly different error message yes yeah let's see what it match okay so that is fine interesting so ah different
failure result for which yes uh fail is failed uh I um how could that have succeeded do we not have do we not not theme
so we did we had artist and song title and then theme oh I'll have to go look at the code I guess um the validation is
in colum mapper test yeah so this validation would be in the extract column uh it so are we not passing along the
failure result for for that yeah let's column well here we're not checking and I think I I remember this we're we're not
actually checking to see if the contents of the required column are empty ah which I think is why we we created those
Jas because we actually are not uh why don't you create the situation that we're currently in yeah I know I at okay but
we did get a failure message if song title was empty uh I wonder if column um because that's just checking that the that
the column is there it's later in the process or or the caller to extract at uh oh we are looking at at theme Result
title uh oh but can we go back to yeah sorry go back but if the column's there we we're uh we're not act so the only the
only time this fails is if the column's not there be right so we're not we're not checking for required columns being
non-blank that's what we're not checking for right what's interesting though is is when we had blank for song title it
was saying missing a required column I want to reun that yeah I'm I'm like what one these attributes are black song oh
so we we were I so I think in our parser we are checking for blank but not for everything oh look at where that
exception is uh look at what's what's happening um so I think what's what's confusing us that I just realized and this
is where it's like read read the the out output Clos message the error message um this exception being thrown by song so
this is not even validate this is this is not ah now why uh and and we're also not checking I mean this tells us that
we're not doing an exception check uh uh for themes um that's a a separate issue that we might want to yeah we're
checking we check for artists we check for uh we do check for any match does that not work the way we expect it oh wait
a second theme oh no never mind no no that adds it to the list of invalid attributes right well that's interesting I
thought we had a test do we do we have a test for that get three well do they do right so we got uh should not be empty
nor plank sign title should be empty wait um I assume that should be artist yeah so that uh and then let's scroll down
where's the theme one uh one we've got artist is title yeah artist song title and then what's the last one uh that
they're all that they're want me to run it I mean I I'm asking it rhetorically because of course it passes but it's like
that's interesting that that test passes so so we don't have a test specifically for for theme one being uh being blank
so let's let's write that test because I'm I'm a little perplexed uh and Mazin says to hydrate so I will and while you
do that I'm gonna B head of people code for more than five plus hours a day we don't if you're actively coding I don't
think there's any way you can do much more than four maybe five uh if you're ensembling if you're solo coding I mean
yeah some people can do anymore oh no it's not a string might uh yeah was just about to say fix that 33 so yeah I I mean
this should pass so let's go take a look well the cursor has to be in the right window when I press shift F10 yeah yeah
picky so it passed okay well that's good I guess um let's make sure we wrote it right just double checking so now I'm
wondering if there's a parser issue uh about removing trailing entries so I think we can we let's commit this because we
fixed this up and we added a test that that really clarified that themes should explicitly not be I wouldn't bother with
the fixed I would just say what with the major changes added added explicit test for empty uh just uh I would I wouldn't
commit that one yeah I was not commit that one that's how I was checking it yeah okay rip all right so now we we've
checked that it should throw an exception um so does throw an exception for song title so that's good uh so let's switch
the test back yeah so what I'm wondering here is is it a mismatch now on columns because it thinks there's two columns
so can we drop 197 or just change contains exactly to string sure cuz with the theory that it's dropping off completely
the last entry it thinks that there's only two columns of data uh that's my theory so let's see okay well now I am
confused can I do a quick here now so that so that but how could it be a valid song If there's no theme can we do an
assertion on the song that we get so remove the space there the test is is saying that it's succeeding when it should
fail so before we do that can we dot uh oh actually no we can just apply to result and then say uh in there we can say
um why uh I'm not seeing the autocomplete I expect uh um what are you expecting I could start typing it can options yeah
so we want is is success or success values yeah and then that know that's a that's expecting an a song object right you
see that on 196 a collection of C of song so that's telling us we're now getting songs out of it right that's what we
expect if it succeeds so let's just create a a a you know uh fill in fill in all the values just with one two three or
whatever the uh you'll need one more string before right so this will clearly not work uh but it'll give us some
information as to concerning hey there nikochan uh we are working on jdk I think we're on 22 um we appropriate unless
there was something specific you were asking about so so this is really interesting wonder so what do you what do you
think I'm trying to figure out what to do without going debugger to see what's happening well I mean you know it might
be the time to do it it it might be uh but I like to to to to theorize a bit um so we noticed that when we put a space
there then we got the expected you can't have a blank theme theme my theory is that there is no theme uh so we get back
from when we when we parse the columns back nothing because there's no column there um can we look at the tsv song
method so we currently um we got a success on line 55 when we extract themes can we look at extract themes because I I
have a suspicion that yeah so this is a side effect of us filtering out blank entries and not adding them so my theory
is is that song allows list and that that and song is okay with that when it shouldn't be because we validate hey are
any of the themes Blank That's not allowed but we never enforce do you have at least one theme in the list so let's as
as as Ali says it's like okay now we have a theory uh let's test that theory and this is why like going through the
debugger we might have been able to even find it quicker um but I feel like it doesn't it doesn't help us form theories
and around and then write tests for uh things that things that are wrong right plus the more you practice working in
that way rather than reaching to The Familiar debugger yeah the better you get it the yeah because you know this yeah
exactly and and it's it's very easy I think what happens sometimes is uh jumping to the debugger means you're not
learning about the code base in a way that I think is is as useful this is just my my subjective feeling about it but um
from a cognitive load Theory point of view when you go into the debugger there so much going on uh what cognitive Lo
Theory says or at least suggests um is that if there's a lot going on just to figure out something you may not actually
learn anything in in your long-term memory because it's it's so full of just trying to process what what you're doing so
let's write a test directly against song where it should be invalid if the song is empty and just looking at the code
it's like that's clearly the test where is it uh what did you do stop I just searched for test no no don't don't search
control shift t shift I know I was actually just curious to see how many tests there were but yeah the problem is
looking for looking for um big list like that it's too much well yeah looking for references to that is not just the
Constructor it's it's it's everything yeah yeah so this is what we've got so we don't have a test for for this specific
scenario so let's um we probably do want to throw the same exception so it's going to be very parameterized right I
heard the joybell let me just important yeah for for me it's it's what do I sort of want to you know am I am I trying to
figure out and troubleshoot my code or am I trying to to sort of troubleshoot somebody else's code like the framework or
or a library or something um then I'm happy to to to drop into into the bugger especially if I'm trying to figure out
sort of data flow or call Flow um but it is it is a I I do believe it is a crutch I do believe it is a uh if you if you
jump too it honestly I I think you still have to have a theory even if you go into a debugger you have to have something
that you're focusing on you can't just look at everything um it's because it's just overwhelming there's just too much
going on so even if you go through the debugger because maybe it's deep inside and and maybe your code isn't isn't
amenable to to testing like this code um I still think you've got to have a theory to guide your guide your debugging
yeah all right so uh I think this is just theme list not okay I was yes okay I wasn't sure if you said anything or if
you were just I did but um theme um list is empty is that what you said well we're testing the negative case which is
them less should not be empty right and otherwise I think it's going to be the same as the test on 31 with I get some
extra lines there didn't consistent probably because we did exactly what you just did which is a copy paste into an
empty method yeah yep so list of creates well I think we should just put here you're G to want to not do it way yeah yep
uh lowercase e otherwise it's not going to got the auto completion right one yeah huh yeah because it's preferring
method names keep going empty list yeah we go yep sooner or later to get it yeah eventually uh do we like that error
message no um I guess essentially they were blank so I I think that's good enough uh if we had say empty list uh yeah
that's fine we okay now I was going to suggest something else but I think that's fine because there's enough context
because it's going to be an exception so we expect this to fail um right uh but let's look at the right test yep so
fails exactly as predicted and now we now we just have to make it work that's the easy part yeah s where would we put
this oh because we're accumulating errors or this one too egregious that it just it's just the one and that no I guess
uh I I mean given what we stated in our expectation this would check so baale and Bale up here um hey Auto Complete full
line successful and did we specify what hey there go for COD type of exception we yeah it was still a missing attribute
exception oh it's song test sorry move this back up here where it's supposed to and should we just put a blank text for
now and then characterize it well we already stated our expectation so we know what it should be yeah yeah we could have
done it multiple steps but I I am totally fine with taking bigger steps because we know exactly how it's going to work
did not so notice that that now throws an exception as we kind of would like it to uh this one now is interesting oh
another test this is the is this why you're thinking maybe we should continue with the cumulative approach and no no
this is exactly what we want uh okay right our song tests are now all passing these are now the test we had before that
was failing where we were confused um but now we also caused a different test the song importer test to fail so that's
why we have two failing tests uh so I think what do you want uh so we should look at so the par single song we know we
had to fix right that was the test we were writing that that got us on this journey so this one tells us that as a last
resort the song object itself said I'm you didn't give me good data so I'm going to blow up right um what we do want is
we want that to fail uh with a failure message and and that's that we need to change that behavior we're not currently
checking for that um but I'm C what the song import is right that's a problem theme is does not look empty to there's
are we miss are we missed number of columns one two three four uh so I think intell will let you edit that um you were
thinking we' have like a table view or something yeah yeah I know they have something like that for CSV files I don't
know if they have it for tsv files um but yeah so are we sure we we've got uh well how approach did it break it no uh
well you can ask it to I believe if you uh when I do the paste uh paste special no no no it's it's it's under um if you
paste it and then you data I think that might be it it implies it's going to a database to get it so yeah oh oh that's
an import um text to columns that's what it is and it's delimited so go to the next next and here's where you say tab
yep that was weird can you select just the two cells no no just select the two cells just those two yeah so delimited
wait go back oh I'll just do it again since I didn't do anything limited yeah uh oh because there was aren't real tabs
so let's change it to uh let's change the limited to other no you can still do it I'll go back yeah yeah yeah delimited
change this change it to other and puts back SLT it only allows one character uh that's G to be good enough slash is
good enough yeah oh right because we don't care we don't care about the data we just care about the number of columns
and just stuff line up yeah uh so looks like it doesn't line up that's them our theme one is is wrong uh we've got notes
uh we're missing record label and so skip notes is under the wrong column right so we need something here yeah before
skip notes before skip notes yeah yeah it did seem like when I was doing the trying to line it up manually I was like
something's missing here I think it's record label so so we w't record label there yet okay so now let's rerun it now
let's rerun it that should that should pass and we should have the one remaining test failing which is the one we're we'
re changing behavior on and then we're at the one hour Point anyway and it'll be good time for a break perfect awesome
uh let's ship it or at least commit and then we'll take our attitude yeah I was looking it's it's it's funny it's like
because the the the the ribbons are customizable it's um not is I'm just seeing exactly what we did so we got so we
fixed a test we didn't know was broken right and and now we explicitly check for it for the main thing is explicitly
check for empty coffee oh you met Arlo B where'd you meet him cool yes after our break we'll make it Arlo's a gas I like
Arlo oh that must been mender con yeah I couldn't couldn't make that good enough for commit message uh yeah uh do you
want tsv song par your test committed as well or do we said that we're still in progress we don't want to do that I
think that was the still in yes that's still in progress okay yeah all right hey there singular sing singular from being
in an invalid State because song wasn't doing its job it wasn't protecting itself uh against a case that we obviously
hadn't thought of so when we come back we'll we'll pop out pop that stack and and get back to uh to where we so just a
little uh commercial message as it were um you may be familiar with uh my tdd game or perhaps not uh one of the things
the the game promotes is this idea of predictive being very precise about our predictions so this what you see us do
here on stream as well as what I do on my solo stream making that prediction really precise helps us determine whether
we understand the code as well as telling us whether the test is working properly um so this game if go to td. cards uh
you can see a video here about uh where I talk about sort of more about the predictive test driven development process
uh and then I walk through the game so currently it's a physical board game you can play it you can get it you can play
with with folks uh great fod for for discussing uh the benefits of of tdd and and as well as how how it works um but I
am also working on an online version and uh that's what I'm doing on my solo stream and so this is sort of a mockup of
of what it something what it'll what it'll look like and so if you you buy the physical game uh you'll get early access
to to the online version uh so go ahead and and check it out and brilliant uh every time I watch people play this I've
I've done it uh at at several conferences now um everybody always has fun and and and and has uh good conversations
about you know what is tdd what is the you know what is the predictive aspect um one of the things I find great about
games is it's it's sort of a low stakes low anxiety environment because it's it's fun but also you have opportunities to
to discuss things that maybe are would would seem sort of and let's see yeah so that's the link uh td. cards um I also
have uh special offers for for that if you uh want some coaching along with it um so I will uh facilitate uh a game or
two uh as well as um run through uh the the process itself um and so provide sort of uh copies of the game as well as
some some coaching built in so just uh you can contact me go to Ted tedamy young.com that's my email address hit me up
uh happy to talk about the possibilities there and uh you may know that also that uh I facilitate a weekly book club so
what we do is we take a book we read it about chapter by chapter uh and spend two hours on Sunday talking about what we'
ve read discussing it clarifying things uh trying to get a better understanding of it and um we're basically just about
to finish the programmer's brain which is the book we've been uh reading through for the for the past few months and so
that means we're about to decide on the next book um you can help uh guide the selection of of our next book uh in the
Discord we have a channel called the book club Channel and there's a thread going on for uh not just suggesting books
but also uh sort of indicating why um why you think it it's it's a book that that would be interesting for others uh so
there's uh been some suggestions already we'll probably go to um starting sort of the the the voting process in a in a
couple of weeks and I expect the new book uh that will start the new book um probably some sometime uh early to mid June
is is sort of my my my guest toit at this point based on probably have a couple more weeks of discussion then we'll
probably take a week off uh and then we'll we'll give time to for people to vote on and then actually obtain and then
actually read book I can guesstimate but no no estimates estimates are are useful um so one so so one thing that that
woodyz uh talks has been talking about a lot recently is is sort of not no estimates but sort of Beyond estimates um and
I'm always in favor of basically what are you using these estimates for what is the purpose of them because while
generally I'm against sort of committing to we will finish X features in y amount of time because that's very difficult
uh more than though to say can we fit this thing in by this time in in some way shape or form and get a sense for it um
so I think you know there's a lot of it depends what you're using those those estimates for all right trying to see what
I missed just looking at the chat window no estimates you talk about no estimates oh my oh I was just saying because I
was I was guesstimating about uh how how many weeks of our book club we have left before we start our new book and so I
guesstimated that we have left yeah this is this is this is common it's like what business wants and what we think they
want are often two different things and so um words like estimate it's like what do you mean what do you need them for
what how are you going to use them uh I think how are you going to use this information is the most important question
to ask when you're asked for estimates like okay why what you know and not in kind of an obnoxious way right in a very
collaborative let me give you the information that will actually be useful for you um and some of that information be
like we can't tell you that why you know and and you might have to dig a bit deeper because uh there is a long history
of of asking for estimates and it being used as deadlines and then business getting frustrated when you miss the
deadline it's like that's you didn't tell us you were using it as a deadline or the usual what date do you have in mind
so let's talk about that because usually uh because that that's pretty frequent is like you've got a date in mind
business what is it why is it let's talk about what we can do to to meet meet your needs because this is this is not the
game of of find me a rock no not that rock no no not that rock either it's like if you if you're looking for for an
estimate to fit a deadline that you've already got in mind just tell me what the deadline is yeah and then we'll figure
out which how to De feature it to meet the deadline yeah yeah we'll say this one the most important things right yeah
like this we're highly confident in this we're not so confident in and this yeah exactly we we often estimate based on
on how much we think we know about it and how difficult we think it is um and they just want to know when when is it
gonna be done yeah we just committed it's like okay you've committed to to to to date and scope uh you realize that
qualiity is what's going to get what's going to suffer whether you like it or not yep the delivered on time all the
features oh you wanted the features to work oh you wanted them to work you didn't say that oh you wanted us to be able
to then add more features after that you didn't say that yeah either either before or after that deadline uh uh every
everything yeah that that I just don't don't put up with I'm like I'm sorry no um by the way no you don't have to say
yes we are not order takers um insist on being collaborators not order takers I know that's such a revolutionary as in
not as in fostering a revolution uh idea all right but back back to to to more uh manageable fine graan things that we
don't need to estimate um so we now have an exception being thrown instead of a failure Val a validation failure message
so now we're now we're in a good place because now at least we understand what's going on uh did we want to did we want
to do a refactor of the song uh Constructor yeah let's go back I mean typically i' I'd extract the number eight as a
requires but I feel like the entire thing is validation so I'm I'm more than happy to just leave it I'm also like why do
we not have it blank line after 16 but we do in other one minor but fix it yeah I would do that yeah I think that's fine
yeah in a way all of it is required but the first one is a literally a bail though whereas this one is a I guess this is
a second requires yeah it's yeah I mean it's it's basically it's it's all it's all just two different requires but I I'm
fine with it being being one thing cool all right okay so we were looking at this test yeah so uh Java does not have
validation headers um various libraries such as the bean validation Library which is included as part of spring boot um
uh does have that um but they're way overkill for for for something like this um plus you you end up getting a lot of
messages and you have to explicitly validate it doesn't throw an exception um so again this is so this requires like
validation that song is doing is basically it's a it's a last ditch effort to say something is wrong right because as
we've seen if you don't protect your domain objects from being in an invalid State then you get you will get higher up
you will get you know observe problems at a at a higher level and then be confused as to what's going on which is
literally what happened to us today um if we' had this validation in upfront it would have been a lot more clear what's
going on uh and so that uh if you use something like a validation library that means you still have to remember to call
the validation L but this isn't validation in the same way as what the result stuff is doing again that's the difference
between exceptions and and and validation validation is is we want to report back as messages exceptions are basically
saying we're in trouble and and there's nothing we can do about consider at the calling of part Song level should that
result in an exception to this level or should we or is it at this level going to be a is failure is going to actually
be true right so so what we want is we want at this level it's validation and so we don't want the exception the
exception means that we're missing a validation right so we're gonna have to catch it in uh well we don't want to catch
the exception right the exception means you've done something wrong and you for you've you've for you didn't prevent the
exception from being thrown catching the exception means you so in this case we could have prevented it but we didn't so
we want to do just like we've done for others is is actually is actually prevent it um so what I think we should do is
is take out that first assert because we actually want it to fail that was an experiment yep yeah or yeah experiment
debugging you should kind of now run this one yeah and so this will fail failing right because an exception is being
thrown because we didn't do the validation check for that right so full no asks what if a new column is added this code
will break um yep we have not gener we have not generalized this code right yagy applies uh if and when that happens
then we would decide do we just add that column so let's say you know release title became required at that point we
would address that and modify the code as appropriate um and if we that at that point saw hey we're going to be want uh
you know wanting to import all sorts of different kinds of data where things are going to be different and so on then um
then we might look to generalize uh things um but it's already fairly General like we have one place to change the
required column list uh and um the validation is is is a little bit tricky here on on the themes and we could generalize
it but but very much uh you ain't going to need it applies don't overgeneralize code yeah vent driven architecture is is
problematic from like traceability of of code flow um and that's the downside of of of a of aent driven is that you have
no idea how you got here um and it's a problem um and this is where you get you're almost treating it like you've got
different parts of the system and you have to have some correlation ID like to trace back the request because it's not a
method call to a method call to a method call all right so um we'd like to make pass so we'd like to get a failure
result for um an empty list for where there's no theme yeah empty list theme or no okay because we treat themes
differently so for these columns we're doing extract column for theme one so can I suggest something um I think by
starting with theme we we're starting with the hardest one because theme has this weird thing of like you can have one
theme or multiple themes and some of them can be blank and it'll skip over the blanks and so there's that's more
complicated uh did we verify that for example having a blank song title gives failure because this test is pretty
generic sounding it just says empty required cell but I think we need to be more specific right do you think run an
experiment with this one or create a new test with that EXP experiment we it's an empty uh I think we should just change
this test to be failure result for uh uh empty theme empty yeah change this one to empty theme and then we'll create
another one and we'll disable this one and then we'll create another one for an empty I think we could just say uh do
this one cells so then we would basically just created a new test yeah guess we do it right before what's the not enough
I want to see what our naming pattern result for empty do you want to go in quote order so artist first then song title
then theme sure uh why don't we say empty required artist just to make it clear that it's point uh let's use the word
cell to to sort of reinforce that language yes do we not do that what do we use here column well here it's it's it is
because it wasn't enough columns and here it's now uh now we're now we're sort now we're because this is what the jir is
about is testing empty cells right I'm just wanting do we have another one would needs to be changed to cell no because
I don't think we have any tests that are that do that might yeah okay cool just want to double check um so this is very
similar so I could do some so we so we ran this yeah sorry I was um I can't remember if we have code that checks for
this or not I thought we did no we don't have validation code so I believe this will throw the exception at when we try
to create the song okay so yep missing song attribute so we don't want that we would like to validate that before we
actually song we create the song in here it's is so here we're checking for success for 50 we're clearly getting a
success we oh so extract column right so we're saying extract column for a required column we're not checking anything
about required column other than the entire column was missing right and we don't extract column doesn't have the
concept of currently is that even checked we got yeah so column mapper is the one that has the knowledge of that right
because we do check that so if you go back to song parser right that's what we're that's what we're uh and then you go
to sorry column it knows about the required columns we because we said that that's part of column mappers role what what
it it what the knowledge that it has so we're checking that the header contains it but right right so this situation is
the header is there but this cell is empty so previously we've been checking for the entire column is missing but now
we're checking for the the column is there but this cell is empty but this say head column contains column name so it we
get the column string so we should only be doing success if the string is not empty right yeah I hate nesting if
statements well make it work and then yeah we want I think we want blank blank is the meta one right that's the larger
of the two yeah didn't mean to so you can just hit control Q yeah that's what I was trying to do I just clicked the
wrong okay guess we would just use the same because we're expecting that are we well test right now we're just really
checking for that there's a failure message we have not been precise about what that message should be right we haven't
decided on that yet so for now just go with well whatever it takes to get the pass well not that that yeah yeah right
that's all the test is asking for we're not going to give the test we're not going to do anything extra of course they
say you don't want to ski in you know uh lean lean too far in front of your skis yeah whatever the saying get over your
skis yeah I haven't skied in a while hey there Jonas welcome oh we broke all kinds of stuff this um because there's a
there's a uh uh uh another requirement right it's not empty we don't always want to fail at the same time yeah it's only
if it's a is it contains any no no no no we want to ask the column mapper the column mapper knows whether this this
column is not is there a we already have a method we do okay ah now we got is optional column and if we don't like it we
can create another one got it so we could do is bang or you know the opposite we'll start with that and then we'll
extract it into its own yep actually you know what we could do is this extract that and say is required no that's fine
too we'd end up yeah why did not like that I probably hit the wrong one oh it's oh no no not column name uh no it is
column name let me see the ah right uh do we want to rename the because technically that's not referring to the column
that is referring to the cell yeah as our ubiquitous language grows we have to update our code to match it yeah run this
I wish it would actually display display like disabled test colon or something like that yeah and the name of the test
and yeah with the name of the test yeah all right uh so let's commit and then we can look at refactoring this mess uh or
we could refactoring commit now either way is what you're saying tests are passing so we uh it's because we
intentionally not clicked this earlier is that what you were wondering about yeah that's what I was wondering yeah the
control k thing because we had previously unselected it it looks like it learned oh that's interesting that's not the
behavior I I remember but anyway uh we want to commit that though so if you if you uncheck that and go into the code K
oh okay I guess it leave I guess it it does learn okay I guess I just don't do that enough to to remember what the
spacing so that not actually what we did details right so I not I notic persp yeah I noticed you looked at the code to
figure out what we did and I think it's much better to look at what was the test that we wrote that is now so it's empty
cell now fails validation but is it for all we've only tested for artists true then that's all we should say yeah well I
guess we we don't know anything else well theme we can no but that test is not passing oh that one's so it may end up
disabled but it's disabled yeah right sorry brain part um I mean you could literally say we now get and then the name of
the idea and that's why I I really like paying attention to to the test because it it helps us focus on what is the
functionality what is the feature we want as opposed to yes we happen to right goetic yep now we tackle with a disabled
test well so uh there's two two things yeah go ahead yeah I just say probably some refactoring first uh I would not
refactor at this point because um even though I believe we actually have generalized the code uh we don't have tests
that prove that um so I don't like to to ref and I've been talking about this on on my uh Mastadon and and elsewhere
that I don't refact I don't refactor at every single tdd cycle even though it says red green refactor I'm not
refactoring every single cycle ccle um but there are points where I feel like I've I've covered a few scenarios around
some functionality and then I look for refactoring because then it's likely that the code is either been generalized or
or needs needs help generalizing yeah um but I think before that we currently don't Define what the failure message
should be and we should do that true I'm just GNA write something and then maybe something like song requires um an
artist what was wrong with must I think must is a is a simpler sounding word than than artist uh I I might say uh must
have a artist um and what we've been doing with other failure messages so we can use that to inform what this one looks
like I think we've also been displaying what we actually got right for the whole song we doing the entire yeah so I
think if we should if down period contains get the exact phrasing we us before yeah row row contains row contains I'll
take it even though it's wrong uh nothing yeah I don't know what it's going to I guess it will display nothing yeah um
which may not be what we want but it's yeah what do you think front it see what we get um well we're going to get a
failure because it's we turning an empty string so yeah that's our that's prediction oh yeah I should check the pass
well I'm just gonna pull this over second I always say light light cheat steel I could get this to make it pass the the
variables and and it might see to to those watching it might be like well what was the point of that um when your code
is complex you might not be changing the code you think is going to be affecting the outcome so it's certainly possible
that we changed a string in some other result failure like we could have been changing line 44 thinking that that did
what we wanted um and so by doing this copy and paste it means that we're changing the right thing um uh without doing a
lot of thought and without writing more code than we need to uh and so that's why uh I I often do this and then we can
basically now replace it with with sort of dynamic code uh that will should should be the same thing uh wrong place I
got the format in right which does lead me to believe that perhaps we want our failure to do this for us um but that's I
think a a about yeah so we get to Green as quickly as possible um and one might say it's not didn't take us all that
long to do the formatted uh but if we had done this and it turned out to be in the wrong place um we might have written
the code for nothing but getting to Green as quickly recommendation okay all right and that allows us to basically test
are we doing the formatted correctly are we using the two string correctly and we are yeah I was wondering if the two
string we were we were unsure whether it would do right whether they' be yeah you know y welcome M mrin sorry I'm that's
gonna be hard to pronounce but welcome welcome ice to see you from Brazil there is a chat about having the message X to
gen I guess when we start to write the I guess that'll come out once we start doing the other Fe required column yeah I
I think it was more you know do we say song must have but didn't um or song is missing uh and I think probably his
missing might might even be more clear I was gonna come back to that when we finish this want to do it now yeah okay
what was it everything else good I think that's good yep okay well I know it's gonna fail so I'm just gonna go fix it
what no no we want to see it fail in so you know the trivial scenario well it it gotta see it fail before we see it pass
so I'm just there are some points where it's so trivial it's not worth it I kind of thought that one was in that
category look like you you didn't I um when it's when it's really fluent to be able to run the tests with without even
thinking about the keystroke involved it's a natural like I'm not even necessarily even thinking oh I need to run this I
just hit the control R right uh and so it becomes this very automatic thing where I make a change and I just hit control
R because it usually just takes no time at all um I mean I I would have been fine if we skipped it but uh when you get
really fluent about and and becomes uh automatic then it's almost like you just do it so new test for another required
field that non theme required field uh so we could do song title which would be very much exactly like this test which
means then maybe we should just parameterize this test um so the way I see this sort of there's there's no failures
which is Success we've got tests for that there's a single failure which this test covers right a single missing cell um
then there's uh many missing cells which is what happens if we're missing both song and artist that's going to be a
different error message that will need a different test for but I think I would parameterize this one because this one
will force us to to generalize our code a little bit more uh and then I would go to two things being blank because then
that will force us to generalize the code even more uh and then go to theme because that has a a fairly different uh
yeah and suiga bring brings up a a good point besides uh don't deprive of us of our dopamine hit um also uh by really
getting into the habit of just constantly running the tests you'll start to notice if it takes longer than if you start
noticing how long it takes yeah we do a CSV source for this one no it's really just no because it's uh oh actually this
one uh yeah we should probably Source um we might want to use the uh yeah I've tried I've tried infinite test and
similar I feel like it it runs the tests at the wrong time um so I'm kind of not not quite prepared for it uh but that's
that's that's me I anything that love uh what are you doing I was gonna try go to a text BL we want to do each one with
a text box right um let's actually just write the the fields first and then okay textb so be sorry we're not we're not
changing the header what we're changing is the be so is it a testb uh yeah I guess it is what's that sorry I'm just
talking to myself um You hker there's no e at the end no e yeah yeah cats what was the syntax again do I have it right
yeah we want just the failures so we don't want any success ones so it would be this uh so I thought we were just going
to check artist and song title because we're were going to handle theme right did I miss anything uh well yeah I mean
our your csb source is not correct because we've got the inputs but now we need the outputs oh and this is where textt
blocks gets um so just convert this to a text block yeah so what you have to do is you have annotation so instead of uh
using curly brackets you delete the curly brackets oh uh and then you just convert it to through uh text blocks you can
put um there and then you can delete the quotes delete the closing curly brace on 194 Oh it uh and then so what we want
is um on 191 what do we want uh we just want to say artist right because we we want to slot in the thing that's missing
and the and where does the second one is there a second parameter is that how it gets that's what we're going to do y
like this so it' be be we can just call it missing attribute or just missing I think it'll can we do present this and
then format sure look at that it knew exactly what you wanted and so let's change the test name since we're since it was
mentioned so will we do it plural because we're going to test multiple as we run through well each one is only
referencing single missing cell soell yeah it it's going to be broken because our failure message is broken oh right
right oh Astro's tired all right as have a have a good night yeah thanks for joining thanks for so we parameterized the
the uh test but not the production code no no what's why is the test broken again because both tests are broken I would
have expected if we did everything properly one of the tests should be so why is this failing not sure break mean the
SLT uh no because that's not our delimiter our delimiter right let me look at the other well one's using a text BLX and
one's not so yeah so let's let's so I want us to to look more closely at the at the test can we go look at the test sure
so why does it think the number of columns was two so it does look like uh sui is suggesting that the the the the text
block is stripping the leading white space Oh this one yeah so we can put quotes no sorry not that what I mean by comma
yeah let's try that for both rows or just no let's just see if minimal changes so we can see if that fixes that test
because that test should pass okay so now we know right so this is this is why we always want to make small tiny changes
because we want to verify did that work because if it didn't work then we would have made changes that were that were
wasteful um so now we know that works just for completeness sake we we probably want to put in uh single quotes around
that uh so right so we expected the first one to pass because we just replaced parameters but it should have been a pure
in a sense of refactoring uh that that one should have passed and it didn't but now it does um that might be our our
quoter for today that intellig is not warning us that that leading white space is going to be ignored um I don't think
it's a text block issue though I think it's a CSV source issue that uh except within a quoted string and this is a bit
confusing on the part of the documentation uh here I'm gonna I'm G to switch oops wrong browser window right here except
within a quoted string and by quoted string they mean single quoted um leading and trailing Whit space in a CSV column
is trimmed by default uh unless uh you say ignore leading and false um which we could do if we wanted so the text block
is fine the text block is actually preserving that leading tab that's that's my my firm belief uh now it' be nice if
intell had an inspection for text blocks within CSV source for junit uh but that's a separate separate thing so we could
if we wanted to take out the single quotes um we could then say ignore leading and trailing whes space equals false and
add that in does that help in making intention clearer I guess we could try both of them out and compare possibly yeah
see which seems like it yeah I would I would say uh uh let's let's try it okay let me get my screen clear again okay
well actually which chest is see you make sure this passes now right well we it won't pass because we haven't
generalized our code um but let's take and add in that option and that was that'll be after the triple quotes you can
put a comma because it's another parameter to The annotation and you can say ignore and it should autocomplete it I
spelled it correctly if you spell it correctly yeah true is the default we want false so just select false so now we
expect it to still pass should I get rid of this uh that one's failing anyway right so we're only checking that we we
changed it so expect only two to interesting uh now I'm wondering is is actually is the text block not preserve beding
whites space but it's supposed to because of the indentation one has a space after doesn't oh because it's not ignoring
space at all so we have a space after the comma but it's saying leading and trailing they're saying it's saying it's
basically saying keep leading and trailing which is you have to go one way or the other uh that I agree that the sui
also says the flag is is confusing whenever you have a flag where true or false and it's ignore mean I believe I believe
that trim would have been would have been better we have our issue for the day we can file it against J it all right uh
this is probably a good time for another break oh yeah good point so uh so we've got one of these working um so now we
basically have in a sense we're factored our test to be parameterized and now the second example we expected it to fail
because we have not generalized our failure message not hardcoded for artist right right so we'll do that when we come
back from our oh yes I just I just took a note to to I don't know if they if Janet is gonna warrant changing ignore to
trim uh as but but it's a good suggestion um uh but it is it is a good guideline to not use to really try out what does
it mean when when a Boolean is both was is either true or false and this goes back to I think I was saying this on my
last stream is like are you sure you want this to be a Boolean in the first place maybe it should just be an enum clear
uh I think it would be a lot more clear bullan because if it said um uh you know you had an option of you know where it
was like whites space equals keep leading and trailing versus trim leading and trailing that would be so much more clear
so just goes to show you just just don't use booleans I they don't you them so do we want to am I muted no not yeah do
we want not use this ignored Boolean and go back to before I think it's a little bit easier to read um mainly because uh
uh having the space having no space after the comma makes it read so get rid of ignore leading and trailing yes sorry
yeah that's where I this that's very bulling of you okay exactly um so I feel like we're missing something oh right it's
the single quote Yeah we now need to put the single quote back yeah yeah and and that's the the advantage of like if you
start out with Boolean you're boxed in you're you're you're yeah you're you're boxed in exactly and uh why box yourself
in like cuz now if they want to say oh I only want leading I want to keep I want to ignore the leading whites space
because that's what happens with commas right because we usually put a space after the comma so I'd like to to ignore
the leading white space but trim the the trailing white space all right so now we can finally address the generalization
to get this test to pass that okay hey the Moroccan um this is my channel you're welcome to to visit um but if you want
to see some SE or Pearl that you're not going to going to see it Channel can't remember the last time I did Pearl like a
decade I think for me oh that recent that recently even more well actually let me think about it it was probably 2010 so
I guess that is 14 years okay so we wanted to put in song is missing required call name row contains that should pass
let's see yeah so no uh right because we're we have not included the error message correctly so we have the input we
have the column name uh and now we need to parameterize the uh that basically the the row columns that we actually have
which we could just take from from input oh because this is hard code yes that's it okay now this would include the did
s well you want your squares because we're just gonna grab the text well uh no because we'd have to convert tabs to
commas I think we should just add another column for this part ah okay but won't we do a two string on it wouldn't it no
we'd have to parse it because right now it's just tab text tab text we'd have to we'd have to do a split and then
convert to the raids at the string I think that's so we're just gonna that's a lot of work in a test yeah so instead we'
re like uh green eyes is the song and then you need the leading that Y and you got a space at the end that you don't
want y probably want a comma before that you're um nothing to string column uh well this is the row contains so I might
actually literally uh that's in the wrong place that needs to be inside the formatted no oops did you see it all
required why is it expecting oh where Source this is the song tsv song that's the input here missing oh because it's got
embedded it o yeah um these commas no no around the whole around the square brackets because are out not double quotes
single quotes I guess you could use double quotes since we're inside of a text block I think the single quotes is agree
there we there we go few y That's a mini slug all right let's totally so there's no need to escape because we're inside
of a text block uh we're just standardizing on single quotes just because it's it's easier to difference and yes if you
want to run Java applications um you could compile to Native image but if you're going to be doing development you need
a Java development kit um no different than any other language you if you want to develop Ruby you got to have Ruby on
your system if you want to develop python you gotta have python in your system so if you want to develop Java you got to
have Java on your system yep yeah so Java at least on the desktop is not as popular as it used to be um but I still
think it's a great great way to stuff uh I'm not sure even by all three I think it gon be explicit yeah artist and song
title yeah what what happened test got are let's run it for Giggles should fail should fail because the message will be
wrong I don't know what the message will be oh theme one okay um is that what we want I think maybe that's just what we
want so maybe uh since it is a required field we are handling it correctly um what we wouldn't handle and uh I don't
know if how much we care if you have theme one is blank but theme two is has stuff in it this will make it fail yeah I
think we even decided that it had to have yeah same one so then I think this is General enough to then cover our
scenarios so we could just plop that in as our I think we can plop it into the parameterize and then what we want is we
want to test where where multiple are missing yeah all right singular atarian have a even uh is it hard to to learn Java
no harder than any other language it's been around for for 28 years or so so there's lots and lots and lots of good
resources Java is easier than C++ to learn uh yes I will certainly grant that garbage collection makes life a lot easier
yeah so let's see this is such a long string actually I don't need this yeah do you want to delete that line it's in the
way that should now pass and then we can basically parameterize it yeah parameterize it into the or move it into the
parameterized test yep and look at that no disabled test anymore just oh I didn't get us to enjoy the yeah no disabled
test so let's move that into the do we when you say do you want to make this perimeter tized test or you saying just no
I'm saying add this now since it's testing it in the same way let's add it to the parameterized test and then we can
delete this test oh the other one okay got it because I thought we might be handling the theme differently but in this
scenario it's ex heardest song title theme one who's it now will it what did it do was it yeah space then square bracket
okay run it see yep H that's GNA fail because you didn't change song title to be theme one ah you're right but that's
okay I predicted that that's how it no now just pass excellent cool now get rid of that yeah we can now get rid of the
parameterized haven't done safe Del we in a while do that very fun yeah if you found a Java book and it's fairly recent
uh even if it's not it'll it'll might be something you want yeah all right let's commit and then we can finally look at
generalizing or at least well we've already generalized the code now we can look at sort it all we did was combined yeah
test or basically enabled yep some 110 right we have it so that one would be can we still parameterize that one can uh
depends on how we format it if we say missing required artist comma theme one then yes sure Y and we wanted to say not
just theme so that means our expectation is that it'll say song is missing required artist comma theme row contains that
I'm not sure if the code handles that does it uh no it most certainly does not so that'll fail it'll fail on the artist
so the artist it'll fail on the artist first because I because it presumably checks that ah okay so this is the trick um
and this is why we did it this way is we actually messages oh so which is going back to jir just to memories we wanted
one failure message for that scenario right because we get the failures but but we get them as two separate failures
right uh this this we'll have to decide is is it investment because currently we're doing we're failing at the extract
column level so we have no knowledge of any other column being missing right which means we'd have to level or we figure
out a way to combine multiple failures into a single message or we just say you know what enough I mean my feeling is I
think it's good enough but the test how do we write the test to show that that's GNA be well we'd have to write a
dedicated test we can't of what I expected kind of the hint yeah okay so we take this one out yep uh so we might want to
just be clarify to test even more the parameterized one ah emptied for single empty yeah right so this is clarifying
that this is only for single case and then we'll write a test for for multiple all right suiga good night if you're not
already gone good night I know it's late for all you UTC plus people yeah for two empty required cells so I think here
we want to specify messages how's that uh spell messes yeah good I'm still not used to this pinning of the title you can
turn that off if you don't like it I actually have turned it off oh you have yeah I have found it distracting okay let
me turn off it's it's really kind of interesting it's like I I like it for HTML and that's about it because anything
else language uh actually I don't sticky oh there a lot of stick Keys No that's just broken there we go we go uh it's
appearance yep show sticky look yeah it's not per language which is unfortunate that's why I turned off it's like it was
annoying enough for Java and you know you're mostly doing Java I'm mostly doing Java and so yeah um hey there's our our
quota of one I mean it's not a bug but quota for for one intellig issue uh make sticky style yeah Java Java's fine
language um curious which book you found uh because some books are better than others of course um Pyon is also good uh
I mean if I were to to sort of learn or relearn a language I'd probably stick with either a Java or a python or a
JavaScript those would kind of be the languages i' I'd start with all right yeah and that gives us some vertical space
that we a bit but delete the empty row 220 I was can get to it but okay I just didn't want to forget about it so that's
why I asked first uh tsv it's funny didn't show didn't suggest the name in interesting then this would so we could build
this up and messages um you can do then failure ah and then you could comment out the yeah because this will still fail
um will it fail no it's it'll this will pass because this is what what currently doing and now we're just and now we're
just specifying that that's what it's doing well if it doesn't pass then we okay so I'm not I I'm not familiar with this
book that's book is a textbook which I tend to believe is not as good as as other books um but I think pretty much less
important about the book and more important that that you uh just write code that's what I always say is like you learn
by writing code not by code um Java certifications are are not really necessary uh like most certifications they don't
really most places don't really pay attention to them but um that's not to say no places ever pay attention to them but
I'm not sure they give you much of much of a leg up it's really much more important that uh that you learn it the reason
why is because the certifications and I am certified except I'm certified on Java like 1.1 um uh is they test a lot of
obscure nuanced stuff that is really not relevant it um so on so I think it's much more valuable to spend your time
learning language learning a bit about data structures and algorithms uh and just writing code working on a project
building it out something that you use or somebody close to you uses uh and that's and that's what you want you can
start out by just creating a to-do list creating some other small tiny project um and build it over time uh but write
code um You probably will find pretty reasonable help on the Reddit uh the subreddit for learn Java um most people there
recommend there's an online course a fre online course uh and so there get some good references there so that's um a
good Community to hang out with all right so I'm turned it into a characterization test yep ran it so the new text in my
buffer yep now should pass yep and it's exactly in that order so sweet now we've tested all scenarios of required cells
yes now we can check that one off in J oh yeah let's go do that um or we can explicitly say we're not doing that oh
right we should probably we should probably document that we're we're not that we fixed all we did all the others but
we're not we're not trying to commit um tested all completed testing all required that's sort of like saying the entire
thing or should we say this one is dealing with two missing I think it's this one deals with with two missing because
that's the only thing that we so we can just leave the second attend to S of yeah we can then say this completed yeah we
can then say this awesome all right so what's next um do we want to try running the application because we've got three
three tests failing which means we probably have some adapter level stuff failing oh Nonio Yeah so basically let's run
all the tests and see what's failing all right the Moroccan thanks thanks uh come back care uh so let's see so failed to
load application context so that's not surprising so what's exactly failing uh so song importer error creating service
ah right we don't have a uh a available so let's go it that configuration or uh no it's it might be in our startup which
would probably want to move yeah so right there um it's expecting song jdbc repository to be uh injected and we don't
have one so we want to jump to interesting do you have doc do you have Docker ring oh shoot nope I thought I had that on
my um to-do list let me go check uh yeah clearly you either missed the checkbox or checklist no it was the last thing in
um it was so um my my checklist fit in the window oh no if I scroll up it's the one line not visible of course I'm
changing the size of that window for the future so there we go that won't happen next time okay so goes uh so looks like
something else is wrong something else so let's let's scroll down let's um can you turn off the um the wrapping on the
right in right toolbar yeah undo that go to the bottom uh yeah let's go down a bit more because what we're looking for
what I do is when I'm scanning spring errors like this I stop at each cause by okay let me go by eror creating be with
name so you so there's a scroll bar at the bottom there oh it's so yeah so that's saying song importer it can't create
song service so then let's go down to the next cause by where it probably says that can't create song service yep so an
error creating song service is there another cause by that's at so it's saying I can't find a song jdbc Repository okay
right so um surprised that it couldn't pick that up why couldn't have pick that up uh is that the last cause by is there
anything below that no mean should it be is it getting the attribute from list cred repository well that's what I oh no
it's explicitly marked as no repository Bean yeah I just found that too oh interesting uh all right well then let's uh
let's mark it as a adapter outbound but outside the hexagon so it's okay to use it's an adapter so we're fine yeah yeah
okay we're we're literally using list crud repository so adding The annotation is is totally fine got it yeah look I
could have just hovered here and it says no repository be yeah rerun repository I'm just wondering why it's do you have
repository highlighted is that why it's colored okay sorry I was getting I was getting confused as to why it was so you
have Auto highlight um which I which I tend to turn off you're so you're on that thing and it and it highlights it and I
thought that was actually a warning got it that's why that's why I turned that off because I find that I find that
confusing let it h ER creating song importer yeah that's the same thing we had before and then we go down and it's song
not it's saying No Such be so I don't know um spring that well but this is still a repository who's no so um so my my
mistake uh uh the tests are failing differently now if we actually ran the application it would work um so thank you
swegi uh the the spring data um doesn't get loaded uh and this is this is a configuration issue that we'll have to we'll
have to fix um so let's uh let's look at the failing tests again back to the um so these are these two are failing in
the MVC the yeah so these are all MVC tests are failing so let's uh so we can we can fix this um because in these we
actually do we care care so let's we can close the test and so this is sort of my fault for letting us have those tests
fail for so long because then it means we're we're not keeping everything up to dat so um what we want to do here uh is
I think we can just do a uh um I think we can do a mock Bean for the repository and that'll be fine so on 21 bean and
then we're going to declare what's missing which is the uh repository and then any variable we'll do class yeah I'm fine
with doing mock Bean to just say here you go we don't use it there's other ways to do it we can um in fact I was going
to suggest that we do that uh but let's fix all the tests and then we'll do it so let's pretty test and now we can run
all the tests excellent cool we commit uh actually wait a second do we still need that uh this here yeah I guess we
don't we didn't and then try run the yeah yeah as long as we're not mocking uh as as long as we're not making it making
these things a stub by saying when it's called return X as long as we we're basically doing it to say look you need you
need this thing it could be a null object implementation uh rather than hand coding it which we could um we're just Bean
so as long as we're not actually use referencing contents of the repository in our test I'm fine with just using mck
Bean that's probably the only place I use it anywhere and yes the test is already a little slow so another couple of
seconds for Mido to do its thing is not going to make much of a difference all right we've proven that that it was not
long broken IO test I'd be more precise the yeah before you commit can you hit the dialogue yeah so we got optimized
inputs on I was just checking it'll remove the unused import okay all right um now we can run the application oh is it
running yet um you seems like it's trying to run all tests test that's weird oh because it was because it committed yeah
we committed so it was running the tests two ignored tests oh they must be so maybe my take of running the oh we are on
only Java one we should get to Java 21 we should get to Java 22 should do that oh is that something in chat let me uh no
I was just seeing the when it when you started running the app it was so we want just the straight up app not the song
import right yeah that's a good question Jonas if after it optimized it there were no changes it should not have
committed it uh that's interesting we have to look at the commit history do you want to do that or yeah let's take a
quick look uh do uh what is Main and then look at that and see what did it actually commit ah so that was a bug it lied
oh you know what I think I was doing we had changed and then changed back song jdbc repository. Java yeah no I know that
and and when it optimizes the import it basically now was not something that it would commit except it said committed
three files oh so it lied there's there's our today I don't know I'm not gonna file that one I got so many other maybe
I'll file that one so if you have optimize Imports as a pre-step before it does the commit um it gets confused all right
I just ran the theme search so that works yeah um what I actually wanted to test was the bulk import because that's what
we've made some major changes to mainly to to to trigger some some bad Imports so I think it's just song import yeah I
was looking for the word bulk I'm like oh I got to go do the back oh wow I've just been been threatened here what I'll
I'll look I'll look through recreate you could save up and and uh there's a longer dark mode I don't know if I give you
a discount for the longer one let me go see I know I have the really long one which I turned off because I'm like no uh
I think you get a dis I think you get essentially a discount for the dark mode for 25 minutes uh I'd have to go look at
the actual settings for that I used to have a I have the 90-minute dark mode but I have that one disabled I don't think
I think only wheat law has has enough points for that one um um so let's yeah let's let's import something with some bad
data okay with multiple like let's start with column right we'll start with missing column so I just grab something it
does yeah oh no I need the header row well you could do that and see what happens let's let's let's just try it awesome
so now the header is missing boom that's what we want that's great only and it's only one error instead of an error on
every single line so that's good yeah now here it is with the header row so the header so still just checking first and
so now if you if you tack on uh into the input if you put a a tab and I have to yeah copy and paste the tab and then say
theme one now it's going to give us errors uh failure messages for fine uh oh so this is different so this is saying
that we still only have three columns so let's add some some spaces to some of those some of those rows it's basically a
tab at the end with nothing I think it's still in my buffer probably yep yeah I add it to a couple of different ones and
then I can wa a second what's the YouTube that must be a um right that's a um I'm just gonna take that one out yep and
so now we get different error different failure messages y excellent well but blank is it gonna yeah this isn't gonna
help because it's just gonna be blank yeah so yeah yeah it's basically the same basically ignoring the empty columns so
that's fine yeah um now let's let's do want do we have some data that we want add that's actually valid yeah what do we
I don't even know what we have in there um that'll be interest I guess I have to go from the bottom of my list to make
sure we don't duplicate well I mean you know we could reset the database and not I mean we could not worry about this is
your local yeah developer database so I'm not too worried okay let me get something but it does mean that we might want
think about what happens if you import duplicates right we should add that to yes go grab some data oh but actually I
header oh I know what I can do I can I okay Jonas I think you probably mean I need to stream more in your in in a at a
time amendable it to your time zone data import excellent and this was the issue that we we have in our J which is maybe
we should redirect you to something that's more useful right and surprisingly it's the next thing on our list it's the
next thing on our list and we did add coffee was one of the songs themes we go so we do have a a uh a form for that
right so you can just go to theme search without the question mark right because we do have a I forgot we did that I
just want to make sure that that's still there yep there we go um we do coffee again excellent uh cool now will that
come up if you cigar I think we look yeah I'm not sure I no we're we're we we check for ignoring case but we don't look
for in uh substrings so that's right yeah we're not looking for sub strings yeah and we're not dealing with with
plurality well we're not doing anything we're basically like if it if it's entered as cigarettes and you enter cigarette
singular it's not gonna find it but if we if I may Segway into this if I can back that's weird okay yeah so now I know
the problem my wireless mouse seems to not always behave the Wired Mouse seems to always work whenever have that problem
which I think is mostly happened offscreen but Ted's well aware of it because whenever we're doing stuff together um let
me drag this over so my my searches what I would love for it to ultimately be is to kind of this style of a a box kind
of like for t so like you look for this was just provinces but you know they start with c right so we we've talked about
this before this requires you to have um a known list of themes yes which we could extract and just get the distinct
ones that are currently in the database um y so we could we could could do that this particular example is not as good
as I like because it's got this extra yeah this is one of those cases where it's like you're doing too much in the
example I don't want that yeah uh if you if you but basically what you want is um do you know another yeah so the
shoelace one which is the one that that I use uh shows this so I can share my screen or you can just go to shoelace
dostyle multiple uh select and then on the right side you'll see multiple in the under disabled next one down oh under
it yeah and so that one has where you see option one option two oh cool so this one is this one is um uh sort of
multiple select check box as it were um but there are versions that uh basically it has all the the sort of the the
things you want which is sort of multiple selections but then with with autocomplete yeah the one that I thought this
was the one but as you as you type so like if this was there's only one state that starts with calal so it reduces the
list right whereas this one it shows all the options even though these three have been selected already yeah there's a
version of it um that you know of from I'll have to find it but there's um basically this this project has sort of uh is
one of the most popular ones in fact they just Lo finished a Kickstarter where they raised a whole bunch of money um to
basically add add functionality and add features to that so oh cool um and there's one that I'm I'm pretty much have
decided to use with uh with my applications as well as um with although I won't need it very much but for for my tdd
game yeah I just um but stumbled across this one example is a bit chatty bit wonky yeah now I think should we put that
we probably should add it to the jir though um yeah so if we want that that that can uh the basically the themes you're
searching for are you know autocomplete on themes um that would be that would be a feature and that's where we would
start playing in HDMX right I'm just going to put it here for now but uh themes but you know when where we do it is
probably doesn't the sequence doesn't matter at the moment probably definitely after this this we should definitely do
next yeah which we can do now um maybe take a break want yeah let's take a break and when we come back we'll we'll do
that because it would be nice to have here's how many songs you imported and something other than coming soon so yeah
that would be all right so we'll take a break and then when we come back we'll a so as a reminder uh I have a Discord
where um you can come and join and discuss things that we do on stream things related to the things we do on stream such
as Java design testing test driven development uh all those kinds of things so uh can join the Discord you go to ted.
deev Discord you'll find an invite link and you'll join up with Discord and that will uh give you access to a whole
bunch of different channels um recommend that you look at them re skim through things see see what people are talking
about uh ask questions um post code if you if you need help things like that uh lots of folks uh including me will be
around to to discuss whatever you want to discuss and as I mentioned before we have a weekly book club and we're about
to select the next book so um you can be part of that uh selection process um if nothing else you can vote on on the
book that uh we will uh start reading so we're about to finish the next few weeks we'll finish up our current book the
programmer's brain and then we will uh vote and start on our next book um something that I'll I'll be putting into the
uh the Discord uh after we're done with the stream is a little bit of guidance of kind of what kind of books work really
well in a book club like this so they tend to be not very specific around like a framework so it wouldn't be something
spring specific or angular specific or anything like that uh because we want to even though I'm generally a Java guy uh
I do want to uh we have a bunch of folks who are C and PHP and and and other languages and I want to make sure that as
much as possible the concepts uh the topic of the book covers uh at least the majority of of those languages um so we've
in the past uh we've done domain driven design uh I think we probably won't do another demain driven design book for
quite some time because we've we've done enough of those uh but those kinds of are more um sort of not just about
specific code but how to organize code and and how to uh sort of some philosophy around that some of the books we're
looking at for for next time are sort of at that level something um either about testing in general or about uh how we
think about designing software those are kind of the the level of books that we'll likely be select all right I was just
scanning what we had above where we were that was not completed oh and uh that's me uh adding songs actually I do have
tap shifter installed this haven't played with it yet um so like check that off yes um The Next Step should be learn to
use learn to you years actually I tried that some of the things and it wasn't like it the the manual gave different
instructions that were uh I would not read the documentation I would read the it I would look at the menu because the
keystrokes are wrong ah okay for Windows ironically enough because they're expressed as Windows shortcut keys but
they're not correct got it right these are the two things left in the way up here of adding songs via bulk import if it'
s a comp then release title becomes required create result combinator to help refactor the huge par song method yeah
we've got we've we've deferred a bit of our our refactoring uh I think we can defer some of that till till next time
yeah sure um I was just curious what was no it's good to scan and see what we've missed so we going to tackle 113 I jir
113 I think we should yes I think J cool so where would we like it to go after we import um do we want it to go back to
the same page I would think so and just and just have like a flash message a message that shows up saying import
successful yeah or you're imported what does it look like right now um I mean it could even go back to this and then
underneath import have imported 25 songs or whatever sure then you get some visual feedback like wait I thought I past
it in 30 right you know whatever um or do you think there's value in showing what was inputed but not in this box but as
a I kind of would I would kind of like that yeah that basically goes to another page um yeah that basically shows
literally what you what you imported that it processed and uh that's easier to read because right now when you dump in
something like this as if I had it selected but Tech we didn't um what's going on here uh oh oh I see what happened
there we go that's not so readable yeah you know because in your but to have it then present that'd be cool that's
probably well not probably it is a larger task um yeah I think the the way I see this this is this is a feature and we
can we can slice it up into a couple of pieces yeah so I think we should redirect to another page uh and initially just
say success okay and then that's then add on to that success page here's how many songs were imported and then add on to
that here are actually the songs that to actually this is like worded kind of janky um why we just yeah describe the
whole feature and then we can break it down um import yeah it's actually not current where we don't really care where it
currently bul import success page that's what you're saying as the first St right and the Second Step would be um would
we also in include just success or include the number of songs no that's that's that be too big of a slice small steps
so um so we can say say you know just show and then then what you've got on 11 18 yeah and I guess it makes sense to do
that before the auto complete as much as it would be fun to get the auto but really having the bulk import so I can have
data and then having autocomplete working then we can go I feel at that point we can go from coming soon to something
because I feel like that's sort of the minimum right is me having a bunch of real data there um this might be a a nice
to have could be yeah I think I think um I agree I think we can do 114 and 115 uh and then jump to autocom complete yeah
okay shall we all right dive in yep so probably want to look at inweb me right so we want to do is look for a um
whichever whichever one is checking for the redirect that's what we want so that's we want uh when we're it's successful
do we have one this one success yeah we're not checking the redirect right do we have anywhere where we're checking
that's failure what's the next one that's failure yeah okay so we can go and add it to to the successful yeah probably
want to grab the return Value First oh the redirect page is that what you mean no I mean you need to assign it to a
variable on line oh and that's redirect page oh okay right I did put in my buffer for reason I was like wait a second
okay so now just I don't know why I did that that was unnecessary what do we want to call it um well let's let's have it
pass now it does this yeah so so we'll confirm we'll confirm this is the behavior that it currently does and then we'll
change the behavior do the whole thing or just this one uh well this is an i free test so just Rite them all do them all
there is no time button uh it passed by the way yes I saw so now we wanted to redirect to what do we want to call the
new one um song import success results well is it do we want the success and the failure pages to be the same well right
now we the failures is a very specific scenario where we show the messages but we put you back where you can change it
so that's right I don't think we want to change that I think what we want is now now it's interesting we're calling it I
don't know if I muted there for a second sometimes if I take the headset off I mute oh you're fine did you hear me mids
sentence at all no okay you're fine if I do this can you still hear me yes but if I do this you can't yeah I can still
hear you really yeah I mean you sound further away but I could hear you interesting this headphone used to have this
thing when you take it off it automatically muted oh but it won't automatically mute on here I don't know oh it could be
that's true it might just be for Zoom okay so I'm actually wondering about this name because we call it song import but
it's actually bulk song import if we ever get to the point where we're you know I don't know if we're all have a single
import page yeah I that to me to me that's sort of an oxymoron of single import the whole idea of import is it's
multiple M and bulk um and it's probably good to make clarify it song import because we might import other things
someday yeah so well a bit verbos this is probably okay I think that's fine okay so if run it we expect it to fail
totally yep okay and that's easy enough to fix success run the test again right now should right can so we got the
redirect part and now we need an endpoint for that right I just forget where we put the end so it's uh song import MVC
test there under go but you want to probably have the test on top oh whoops oh I've got several that landed down below
somehow this is the one we care about one so what we got here uh you're on the wrong one get to song import is it just
me or that a horrible name for a test get into suggestions but that's what we're doing request do you think what do you
think about requests that's fine but then two is weird get request two as opposed to from because it's a request from
you the way the way I the way I say it is you make an HTTP get requests to an endpoint and so that's true yeah I don't
know that I say you you make a get requests from an endpoint that sounds weird to me I mean maybe people say that but
not me I might say I get like I I make a request to something and I get data from something something I wouldn't make a
request from something that to me just is something else you just sold me on it okay so if you're gonna change that you
got to change the next one to be yeah uh all right and so what's our next test yeah what is the next test we wanted to
oh we're in test failure mode request right because we did redirect so oh so what do we do in a get request that oh the
um to what's it called again import success M end point I think I spelled success wrong this would return 200 as well
yep yeah at this level of test that's all we care about right you could let the autocomplete do the work for you see
what it says so if you backspace up one back space up here and then hit enter yeah oh I see so it only trigger the
completion if you're if you if you've just started a new line so that's close so you could tab it it if you hit and
whoops if so if you want to auto complete then you got to because as far as I know there's no way to say please try and
autocomplete it uh with the Full Line Auto want so we run this this should actually MVC test we'll need to run all or
just run this particular class I would just run control shift F10 now I know yeah that runs context so whatever test if
you're inside a test it will run just that test if you're inside of if you're outside of a test but inside a test class
it will run all the tests in that class okay so as expected we got a 404 yep so it didn't just fail but fail for the
right reason with a mapping I think before to is starting to slower yeah that tab looks fine sure why is that right uh
well uh it is correct um except it won't pass because time Leaf will complain that it can't find a template of that name
but that's fine we're gonna go from we're gonna go from a 404 to a 500 error because of time Leaf um but that means at
least we've done our get mapping correct I always forget about the timely stuff yeah so now we got error resolving
template so that's good so that's a different failure so now we were making correct progress and you're gonna want to
look in not in the test stuff so stuff that the green background that's your test stuff yeah I knew that I was I might
just take that and copy it and then delete stuff can you just do uh uh you can do F F5 to copy the that look like it's
the same bring they both bring it to the same dialogue it looks like yeah because F5 is is a refactoring uh and happens
to work on F at the file level right I mean because I was doing a control C control V yeah that ends up doing a copy so
yeah so it does call the same thing but F5 is one one Strokes one only one keystroke y y and it's a generalizable
keystroke because you can be inside of an actual Java class and hit F5 and it class okay so we'll change the title to
include the word success yeah we can uh we don't want failure messages either right we probably want uh I don't think
they're going to be multiple messages right so we can just put a p and and have a p success message as a Time Leaf thing
or just Ty yeah as a time as a Time Leaf thing okay because it's GNA come from oh right because it's going to be dynamic
it we don't know what the message is going to be so we don't need the each so pull out the whole each got it yeah and we
can change message to success message even though there's context it's probably better to be more specific specific uh
we might want to change the success and there's a style there that's probably not what we want for a success that it so
now we have to populate success message uh well before we do that we need to make sure that this works as a temp and
we're missing uh we're missing something from line two and a enter uh and we want to probably copy that uh so somehow
that got dropped when we when we copied it's basically the um that's interesting it's not here either that's not good um
what we're missing is yeah that line three so let's add that yep it doesn't really cause a problem but but at least it
it it tells at least if nobody else that tells intellig what mean uh preview do anything with time leaf or it choke yeah
we can preview it and it'll be a fairly boring page yeah but it says what we want it to say um so now if we run our
tests what do we happen now it should pass well no it should barf on not knowing what success message is no um cuz this
was just the default oh is this show shows this if this is does oh you may be right yeah yeah not sure I'm pass oh I
didn't want all test did you want all all all oh no the is all this is the only ones we're working on and it failed
before it now passes um so I don't believe that it's a requirement to have anything in the model uh at least not for the
get request so yeah so we're fine um and then now we can we can drop down to the the next layer we probably want to do a
commit and maybe we want to end here or maybe drop down I want to see what you were G to say there all right um yep then
you going to say go down a level which yeah so if we go to uh why does it look like something's still running oh because
it's now just started running all the tests okay uh so yeah so let's go down to the uh oh there is a cannot resolve
success message over here yeah so you're were saying go down to yeah that that's basically because you have success
message highlighted in the current file ah I see got it um so if we go to song importer test right so the test the the
io free test or at least the lack of framework test now uh start testing against this new page so this would be a new
page that uh Su success page does whatever so uh this will this will force us to create um a model as a parameter and
then fill in and we'll test that the model is filled in ly um we probably from that we would pull the success message
and then from that from the model we we we' assert that the success be so why don't we go to jira and make sure that
that we Mark that is the next uh I think we're we are working on 116 so the next step to do that will be to write a test
got it oh so I was just the goal here was just to check off 114 yeah I would say maybe um okay uh failing test from here
so failing so on 115 just say uh fail failing test ah like that yeah and maybe leave a slightly better breadcrumb of
that test will be in song and that's it that leaves us set up for next time so next time we'll we'll basically write
that failing test so we'll test that it puts the right message in the model which means we'll have to as part of our
setup do a successful bulk import um so that might be a little little that won't be straightforward um because we'll
have to uh oh simulate we may not actually be able to write this as as a a framework free test because this is again
sort of um uh the redirect attributes right so we'll have to see um you might want to put a comment at the end saying
will be in song attributes it's really an interesting sort of general question because um and this goes back to sort of
command query separation uh by returning information from a command right so basically having doing a post that
redirects and the information that's the result of that import is carried only that one time and then it's lost um means
that if you never if you did the post and the internet hiccuped you'd never see that result and there would be no get no
way to to get that um so we'll have some things to discuss next time about design the easy way is to do that and then
okay oh well you you know you refresh the page you don't see anything uh or we we basically return information about the
last bulk import and assume it was you but we'll discuss that time yeah sounds good yeah have we we've only implemented
the database on locally we did not in production yet correct right yeah so when we go to production that's uh that's the
first thing we'll have to do is is is configure the database and configure some some settings and then uh but then we
should just be able to to push it and it should just work all right cool well that's it folks uh thanks again for for
hanging out for participating for asking questions always enjoy that yes um and whenever uh our pairing stream is next
we'll let you know so as always the best way to find out don't rely on Twitch notifications don't rely on YouTube
notifications um although if you subscribe or follow that's very much appreciated of course uh best way is to uh not
that one that one join the Discord go to the rolls channel uh and click on uh the code stream alerts and then you will
get and then make sure your Discord notifications are set up because if it notifies and you never receive it well did
you really get it um so that's it so uh we will see next time I will definitely be solo streaming next week uh Mike and
I will figure out uh when uh we'll pair again and I'll announce that in advance so until then have a have a
