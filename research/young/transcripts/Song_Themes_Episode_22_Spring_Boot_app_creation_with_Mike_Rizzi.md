# ＂Song Themes＂ Episode 22： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=S100FP9piGs

---

## Transcript

all right hello folks good morning it's Thursday for some reason I thought it was Friday I was very confused this
morning how you doing m are you confused this morning or are you less are you okay um hanging in there a little confused
maybe a different emotion than a confused but yeah we'll just leave it at that yeah so uh yeah it's funny because I
streamed yesterday uh and it was it was good stream and for some reason I thought today was Friday yet we were streaming
which was which anyone who who knows us is know knows that that's not possible because usually uh Friday mornings I
facilitate an ensemble and so those two are incompatible um but that's what that's what happens when when you don't have
enough coffee I guess so hello hello uh ja the coder and stupendous follow hello again back uh so last time time um we
were we had somewhere somewhere in there we were struggling with uh something that wasn't working that that we felt
should have worked and it turned out we were we were mostly right so I did some work after and fixed that um so at some
point you will want to do a g a git pull or an update in your in your IDE yeah I'll do that so let me go ahead and add
the code to the stage there it is oops gotta get rid of warning let's see let me close this I'm just get my setup a
little bit better there we go really it's really interesting because there is uh the thing we we were hung up in was was
some time Leaf stuff of different input types so we're basically trying to figure out you know why is why is our form
not repopulating uh and different input types act differently and and so um uh when you do a a pull if you do a I think
it's a control t or an ALT t or something if you just do a git git menu control T control t again it's like does does
control T does ALT because on the Mac it's alt T so it's like does map to control or alt goes both ways so yeah welcome
might as well rerun all the tests yes I can't remember if we left our a breaking test breadcrumb or I don't remember
either it was only two days ago yeah well that's the disadvantage of disjointed programming and not yes yeah working on
something regularly yeah um look like while the test pass um so then we probably should test the uh uh the UI change
actually we should probably bring it up huh yeah let's let's bring it up and while you do that I'll I'll uh I'll give my
opinion on stend it's fellow follows uh keeps some onest say fellow and it's it's follow both are great both stupendous
follow and fellow um unless you're not a fellow uh so what do we think about documentation of business rules should they
be documented in something a Confluence or should test be enough I uh feel very strongly that um specific concrete rules
should be expressed in tests because um they're always going to be up to date they're always going to be correct they're
always going to be indicating what the code actually does um and they can often and we've discussed this before on on
stream they the test should be readable enough especially at that layer of the code right we're talking at the business
domain uh layer of the code the test should be readable enough that um business folks you could could look at it maybe
not on their own but certainly be walked through here's what the rule rules are by going through the test code and it
should be readable enough uh and that should be a goal to make those readable enough that a business person who knows
the rules could understand what it's doing once you put stuff in in comments and the same code let alone described in
some other place like Confluence um now you're like I I don't know if this is up to date anymore so that's that's what I
think Mike do you have anything you want to add to that yeah I would say um I agree and one thing is also you could if
your team isn't familiar with specification by example um that is a great technique where it's a it's actually the title
of the book as well but it's where you specify business rules through examples and the idea is that you do these
examples together with your um whether it's called a product owner or subject matter expert whatever you know internal
lingo you have for someone who fulfills that role that that the developers that are working on that particular area of
business functionality work together with the product owner to write those examples like when this is the input we
expect this when we and enough to fully qualify all the business rules um even if you don't certainly writing test for
it is great um but yeah High highly recommend even just the having those conversations yeah is insanely valuable and
until you do it you don't really get it but then once you start doing it there's so many aha moments where I as a
developer misunderstood what the goal is of the uh the product owner um and those disconnects are what cause production
bugs you know that escape so having those conversations super valuable yeah definitely during the the definition of
those you you def yeah you want you want everyone in the room um who who has knowledge Andor uh some kind of involvement
in in the creation of of what whatever you're creating um and definitely Define those as as examples and sometimes they
can get complicated enough that you might need like a spread sheet um and uh that's fine um what you can then sometimes
even do is and and there are tools that they sort of went out of favor like Fitness and fit um where you use the
spreadsheet to actually or spreadsheet like thing uh to actually Define tests that actually get executed against code uh
but I still think there are places where that would be useful if you have sort of very complex calculations um you know
not talking like you know highend mathematical you know integration of of of you know simultaneous equations or
something like that but basically where where there's enough calculations where expressing it in something other than
formulas might might be awkward um and what's nice about that is is uh this you can have it so the spreadsheet
calculates it and everybody says the spreadsheet is correct so that becomes your golden Oracle that becomes your your
your master and then you can integrate that with with test Runners to basically say well okay now operate that
spreadsheet on the actual code uh but that's probably uh that went out of favor because again it's like this extra step
that you have to do to integrate it and could you not just Express that directly as for example you know junit tests so
it depends on the on the domain you're working in um but if you have a lot of those like you've got you know a
spreadsheet full of them then then that might be worth it and also related to the writing of the tests um even if you're
not doing domain driven design using the specification by example approach make sure you use the language of the domain
experts not what we as programmers might think of as implementation details so if you write them in that language one
it's good practice for DDD um but it's also makes the test readable by the product owner if it uses their language so
then they can look at the test and go yeah that's right that's what I'm expecting y right so that's another goal you
might have yeah I think even if like you know what does it mean to do DDD is is a is a I think a an interesting question
perhaps a philosophical one uh but certainly the the consistent language uh has has to be there right that's why um
having the tests be expressive enough uh and a good test for the test whether they're they're expressive enough is can
the domain experts read it um if they can't or they're confused um you might want to look at what are they confused by
is it is it just the code that's getting in the way or is it the terms that are being used and then that gives you the
signal that maybe you're not using the the correct terms so my new phrase for the day is do DDD uh I brought this up y
oh you want to get question I just want to get get these questions and then then we can dive into it um should dtos be
validated before internal objects um yes so uh uh you asked basically where does API validation logic go and um I don't
know if I have uh an article on that yet but basically there's there's two levels of validation there's the API level
validation which is I expect this thing to be a number is it a number I expect this thing be a string perhaps an email
okay does it have an at sign in there and a DOT to the right of the at sign and that's all I'm going to check I'm not
going to do anything more than that right just to see does is it what it is um is it non-empty right and then looking
for just basics of like is this string non empty uh are you know trimming off blanks and things like that so basically
non-domain validation there's a certain level you can do like this is supposed to be a forn phone number um depending on
how you input it hopefully you strip away all the punctuation and and so on and um maybe you just see is enough digits
uh I'm not sure I'd go so far as like make sure it matches the country code that I might leave for for the other for the
next layer um so uh basically it's like the things you can detect at this level that are not having to do with the
domain um basically domain rules like the domain rules that we talked about so then you've got your your validation you
know just to these inputs correct and then then you basically convert them to Value objects often uh which are then
guaranteed to be well this is at least a number that looks like it's supposed to be an identifier this is supposed to be
an email address um and then the domain can do further further validation uh and so that's a a great question since
we're doing validation right here in in our song importer um and there's multiple layers of validation in fact can Mike
can you bring up the the song importer controller where we actually get the input right so the first thing we do there
in line 29 is is the thing null so we can detect that here we could also detect if it's completely blank and just
respond immediately anyway um but we defer that then to uh import song and what we get back from import songs is lower
level validation of like now it's doing the parsing and things like that and where you do parsing is also interesting
like is that domain parsing or is that just converting something so for example I have um my kid money Manager
application that takes strings from uh a text message and I do parsing at that level because that's not domain
information the domain doesn't care how somebody said I want to
spend $20 what it cares about is that there's a trans action that needs to happen that is withdraw $20 from the account
so the parsing in that case is actually outside of the the domain and that validation happens there so um sometimes it's
a little ambiguous about where the validation Falls so I always always think about is is this something that a business
domain expert would talk about or is it just how we're handling input domain and so yeah so if you're using um some
basic spring if you're using the spring validation which is basically the bean validation that comes from hibernate uh
uh the annotations of like you know must be a future date you can annotate that must be not blank must be um maybe a
minimum size in terms of length like for names if you're asking for a full name because you should never ask only for a
first and last name uh you should ask for a full name probably needs to be at least one character but not much more than
that having an interesting conversation uh about names speaking of names MH um at a place that I volunteer and it has to
do with um last name versus first name and so these are for um you know you know hi I'm trying to think of a two name
person that's famous um I am so bad at this hi I'm Michael Jackson I listened to this radio station right right um that
little spot might be filed in our system as Jackson comma Michael right right which in some ways makes sense but what if
what do you what know which is their last name and their first name right and so this is common or this is a challenge
in the US where like Chinese Japanese other languages sometimes have it in their different order than we do right and
what's really frustrating is well not frustrating but makes it challenging is some will switch it for the US market
right right and so it's it's already reversed so how do you know which ones unless you know literally the name of that
person for real right um yeah just just write name that way you can respect what they they've specified yeah it's so
funny it's like I remember like you know you know used to have a a collection of physical artifacts for music like
records or CDs is like how do you alphabetize your collection so you could find things and it's like well is this the
name of the band that happens to have the person's name in it like the pat methany group like do I file that under P or
under M but it's not Pat just Pat methany it's it's him as part of the group and so his name is part of the group and
and it's like okay I'm just gonna I know the whole name and so I'm just gonna do the the full name and and it's it's
like that's fine so Pat so what about a pat mathini soul album was that under Pat as well right well yes because I got
to be consistent so right right you know right near Pat pitar yeah right there you go so just use full name and and let
the searching uh expert says I need to check if if an end date is after start dat is at domain validation um again that'
s that's kind of tricky because what does after mean is it 1 second after one day after is one hour after okay same date
if you're not taking time then clearly then it's then it's just date uh and and yes I might do that validation because
it's clear like this is the start date this is the end date and they must be um after sometimes it's on or after uh but
um that's fine and I would make sure to test that but yeah I think that's fine just to basically what I like to do is is
can I figure figure it out at this level right so the controller sends in some stuff I've already parsed them as dates
so first I check are they dates are they validates um if you're planning a trip are they future dates uh how far in the
future because maybe there are business restrictions like you must do this seven days in advance that I would defer to
The Domain but if you're just saying are these inputs relatively relative to one another valid then I I would do that
and again it's like can I do that sooner because then I can give more quick feedback in a sense I always think about
like the domain is like this like um this worker who doesn't want to be bothered unless everything is in proper in
proper order and so it's like I don't want to bother that worker with with data that's not valid um because that just
annoys the the worker and slows down your system and it might hit the database which might actually slow down your
system so I like to avoid that all right some great questions to to start off with yeah So speaking of validation let's
go and and see what happens now uh when we put in bad data um we want two things to happen we want the two things to
happen I think they're working now is uh data that doesn't have enough columns or has the wrong columns or actually we
don't even have a header which we'll need um so we expect it to basically give us some failure messages but that the
input that we have uh so click the button click the button voila so it's skip the first row because we now assume uh
although we don't validate uh and maybe that's the next thing we need to do uh or we'll see we'll look at our list yeah
but it might be the next thing to do is like what are the columns um but we got the failure message and our input stayed
so all is well yeah and that was the goal is for the input to be that was that was that was the goal yes and what's
interesting is uh we probably should show what it was just this that we had wrong right yeah so there were there were
three possible values and we only tried two of them we were so close we were we were so close it was it's kind of funny
but I when I realized what happened I'm like oh we were so close but we were looking at another area because text area
is different so unlike um a lot of the other uh places where we replace text through the time Leaf attributes um
normally we do do a th text for non- inputs like hey replace the contents of this H1 right with this value uh or we do
that with the messages replace each of these P's content um right we have a th text there replace failure message with
the actual message uh text areas turn out to be the same kind of thing because the content goes in between the open and
close tag unlike every other input type so every other input type has a value attribute and that's where the actual
content that's input goes um and so text area that's then that's why I was really confused because text area is
different one every other one well every other one except for paragraph uh every other input type ah text area I mean
it's also its own own element so maybe I I shouldn't be surprised that it's different from all the other input types um
yeah yeah yeah input that's a good point wow yeah yeah so hey astd and yeah Indonesia I mean there's certainly countries
where single names and I mean we could talk more about names but we've got stuff to do and we don't really it's artists
so let's see what's left nir yeah yeah well actually we got to check something off now um oh yeah J 58 yeah we need like
an air horn every time we get that you know so so we were according to our little right only Parts The Columns we want
must have at least eight columns other ignored failing test decide whether to use tested parse or parse Song level right
so I think we should in a in a sense do a little bit of outside in even though it's two methods on the same class
thinking about it sort of outside in I think what we should require is that um somewhere in in the header are those
eight columns we don't we don't want to we shouldn't care about order right even though artists will likely be first and
song title likely be second we shouldn't care about that but somewhere in the in somewhere in the number of columns that
we get from the header uh there should be those those eight columns right um so we can do that at the parse level uh and
then we can worry about parsing an individual song and we realize we'll have to pass in that that header um but in a
sense we can we can maybe create some kind of object that represents the mapping of columns to to those things something
like that and just for folks who so in the tsv song parser class there's a parse method which calls which gets all the
songs that are coming from the bulk import right and then it calls for each song right this method down below called par
songs right and that's the one that actually singular right that's the one that actually parses the the individual
columns using the split for the tab which is these are all tab separated um but right now as you can see in 61 and on uh
all those columns are hardcoded yeah and that's really we knew that was that was not gonna not going to work for for too
long somewhere and so XPR yes you you what happens with validation and this is always an interesting thing like uh I
mean I have an entire hour plus long presentation on on validation is you are going to have multiple places uh you're
going to validate the same thing perhaps in in multiple places you're certainly going to have multiple places for
validation but you're probably also going to have validating the same thing because uh you don't want to necessarily
trust the inputs but this is where converting to to domain value objects can help because then you don't have to
validate it again so if the outer layer converts the the the dates to an actual date but of a date of a specific kind
right so not just that it's a date but it's you know for example start date and you know that start date must be in the
future um then you don't have to validate it anymore because you know that that start date is already in the future
that's already been validated by the value object itself but there is going to be duplication and what you mean by that
is not using a raw date time date class but build another class maybe call it start date exactly yes um and that class
does the validation and once it's instantiated it's copesthetic exactly yeah you make immutable so then it doesn't get
munged right and you can just rely on it safely domain Leo yeah and and that's and and that's something that's I think
under under used that that idea of let me create a specific type for start date and I will call it like like Mike said I
will call it start date and let me create a specific type nude class probably record if you're doing Java um called end
date uh and if you don't care and and you might even likely will create a pair of dates because they go together and
create actually that as a record and so call it you know start and end date if you can't come up with a better name but
there probably a domain a domain a term from your domain that would that would classify and be a good name for for both
of those yeah could be duration it could be trip length right the domain that names yeah so exactly right so you'd
create your your your your you know trip dates uh and you would not be able to instantiate it if the dates are invalid
in any way on their own or in relation to one another yeah date range is is a little generic I'd want something from the
domain like what what do these dates mean um so trip date plane you know some usually trip but maybe it's it's uh
booking date or something like that I guess I guess it would depend if there was duplication but if you had the need for
two different date ranges that had the exact same validation you could have an abstract class date range where the two
you know like right you know Future travel date Future travel dates right versus past travel dates I don't know why you
would have it but you know again the domain would drive the need and then if you had that need then an implementation
detail name like date range could come into play yeah yeah but that one's yeah I agree I think wouldn't start with date
range I would use that as a potential abstraction exactly yeah yeah and and and and people might say well isn't that
wasteful you just created new types like types are cheap they don't cost you anything uh all they all they do is is is
contribute to un better understanding of the codes like wait which date range was this is this the the you know this for
the for the car or for the flight or for the hotel um and those are different so all right even if they're exactly the
same even if they they have the exact same information they are different yeah conceptually yeah yeah so um yeah we
talking about starting out outside in at parse is that what you were riffing on exactly so let's uh go to our parser
test plural parer parser tests I was thinking the name of the class F12 so I think we test go to the bottom or do you
think there's a I don't know since we're doing the header it feels like it should go at the uh and we might if there are
enough of them we might Nest them but for now we'll leave it so what do we what is our be so I guess we could start with
something it's where we pass in just else would that be helpful I'm trying to think the smallest step that move this
forward a little bit what would we look for so so would we even bother looking at the header rows if if there's no
actual data would we just say there's no data here yeah maybe that's a first step okay you know like yeah just make sure
there's at least two rows do we even do that I don't think so well we know we didn't because when we ran the run time
and I put in two rows without a hair it just said right but that had that wasn't so there's there's two issues one is is
is the first row the header row right um the other is is there any data after the header row maybe that's a two test at
first is there a row right so what I was asking is do we have a test that says there must be two rows oh I don't minimum
let's go look I don't think so either because all of our tests are doing create with header um that's a two is wrong
this one yeah because that test is is not putting a header on even though the the the songs are invalid there's no
header right and what you're referring to is last I was say last week but two days ago right we created this Factory
method to stuff a header before each test so this is actually a test that's we somehow missed this one too well let's um
yeah I think we sort of assumed that since these were invalid we didn't need the heter row but now we're about to write
a test that requires it that requires a header row um so Preparatory refactoring to change these to have no but then
they'll fail well they're gonna fail anyway because right we wouldn't there wouldn't be a situation where we'd pass in
let's say headers right because presumably you're you know we're we're simulating that you're copying and pasting from a
spreadsheet with the header row so it'll have a header row it'll just have have two columns in the header row I mean
there's there's another so there's another validation we could do which is does the number of row of columns in the
header match the number of row that so yeah maybe let's make a little list because it's now exceeded my working size
exactly in header match number um yeah and what was the other one we're looking at we were the other one was that there
is at least one song in addition to the heter line um and then it's does the have the eight columns that we're looking
for or eight required columns yeah it's a better way of putting it the eight required because we're requiring them right
now what's interesting is we do have a different concept of and I don't know where we we probably documented that in our
man it's been a long time um ubiquitous language let me drag that in see what we wrote about that could have sworn we
had the concept of required actors not I haven't done mirror in a while like how do you move stuff around um I don't
know that we documented much about required here maybe we didn't so I think in our in our test F work in this world
let's see I guess NOP we didn't use the word required okay well let's move that out here no that's it yeah so so what's
interesting is is we require a columns we don't necessarily require content for all songs in all columns yeah wow that's
like obscure like yeah the little asterik required yes so let's fix that maybe let's fix that yeah yeah right so right
so that's right uh so release title and release type are are optional as well um right you might uh so themes are theme
is required but themes uh is is not required so like maybe an annotation after line 160 because that's where you have
themes oh there is themes okay yeah for some reason it first uh at at least one yeah so our requirements for the data
are are going to be a little more uh interesting yes maybe step this one yeah yeah question for sure so uh but I think
we can I think we have enough to to go on for now though so let's go back to our little test list me get back up to the
jira location good thing I saved some of those conversational notes that we were yeah having okay let's go back to
parser test yeah so I think if we wanted we could put four as being um required something like required song data or
data song has required Fields has has yeah something like that I don't know fields are like better than data yeah you
can these are actually all separate tests yes yes yeah let's pull that out there yeah so which one should we do first
because no I'm thinking two is the simplest yeah yeah so uh I don't think we need to say bulk import here I think
because we know what we're testing against I think we just need to say rows and then we can sort of Ratched up the um
the criteria yeah ratchet up the insertions and so then we just while technically it'll be multiple tests one will build
on the other so we won't tests yeah I don't know I we won't know till we get there yeah we won't know till we get there
yeah yeah yeah okay so and we're doing this at the parse songs layer uh oh no the pars layer pars layer yeah it is a
little confusing that we've got a par method um I think which is parse multiple is basically parse all the data uh but
yeah should we rename parse I I wonder if we should we've got pars song and parse songs is awfully subtle difference um
yeah plural is valuable I don't know what you think about that one um going back to the production code here we've got
parse and then down the song we could call it parse all I could do I could work with that so let's try that on for size
oh it actually kind of reads nicely parse all songs from the from the calling perspective yeah yeah let's look at it
from a a test usage yeah yeah yeah I like it all right so then we can go back to our our tests that we're writing um
yeah that's good and you were talking about I'm wondering if we should separate into subclasses areas where we're
testing parse all versus parse song no not subclasses um what do you call it uh nested yeah no actually you went you
know what I meant yeah I just Ed the wrong word yeah um or is that a um I think our test names might have to shift a bit
uh actually actually that one that one we thought actually we would have to add the header rrow but actually no that's
par uh single song so maybe um that might be the only is that the only one where we're calling parong check I like this
pinging back and forth yeah only one yeah um it might be worth it to to segregate that one you want to segregate as a
separate um no I I think put it basically like put it at the bottom put it in a nested to like really segregate it yeah
nope yeah uh you can just say at nested really uh well not only but but uh that's required um that's it it's just it's
just an annotation okay but I was I was suggesting writing it first because I thought uh intellig would would auto
complete that for us but maybe try no I'm not seeing anything uh that's a bummer oh I know why because I actually have a
live template that that does that Ah that's why I was thinking that uh I don't think that's a built-in one though you
could try it you could just say nested and see what happens oh just just on its own yeah lowercase yeah no you yeah it's
it's a it's a custom one oh well all right so um yeah so just go ahead and and uh nesa doesn't take any parameters so
you don't need the PRS we can call this parse single song or song y um one thing you can do is is then uh we can rename
the test since we sort of have the prefix of par single song then we can uh basically say just returns failure result
and so take out the duplicate part yeah makes it more shorter yeah so then when we run it um yeah all right let's rerun
everything um I was yeah I was going to say don't I'm not even sure numbering it is useful yeah we think that's the
order but the order of operation may change yep so we're doing real tdd according to Kent backck right because Kent
backck uh reaffirmed that you need um uh a test list so we now have a written test list now we're doing real real
canonical tdd it's official uh so let's do the simplest I'm looking at a test we could steal from possibly I'm wondering
uh it's pretty much that test except song so so instead of the actual song we yeah but wait a second this is gonna yeah
fail because we want to make right so we didn't kind of say is this is this our failure uh failure path um so I think we
have to maybe change our our test name to make that a little more clear second no will pass because we gave it will pass
because we're right now we're just skipping past the first row we're totally skipping okay validate that and run it yeah
um because we got that Skip One in our right lines okay so yeah that that's not so helpful from a negative test
perspective yeah so I think we in in a sense have covered the positive aspect of that at least for having the row um
with the the test on 32 so I think we can make this a failure one which is is uh since we said must have two or more
rows I think uh we can exception uh if if does not I don't know rows fewer oh that's an interesting countable I don't
grocket can you explain so um my playground has uh uh less sand than yours does we're not counting the grains of sand um
but my playground has fewer swings than yours does because I have three and or I have two and you have three so if you
can count them so I have less money than than somebody else because we're not counting dollars but I have fewer dollars
than somebody else because dollars is something we'd count got it it's almost like you should be writing technical
document Ted it's almost like I care about that oh my God I I I got into it felt like a little bit of of an argument and
and I hope my my my friend wasn't wasn't upset about about the HDMX documentation about not calling certain things out
um I sometimes feel like I have almost too much empathy for the for the reader and it causes causes some problems but
yeah so accountable is is a even though a lot of folks um just use less and they don't use fewer uh you know that's like
but if you're gonna if you're G if you want if you want to know why their their difference is basically is accountable
or right sorry I'm just making a little notes in my notebook um so here we want to throw an exception uh so here we we
just want to create the songs having without the header we could try without the header yeah and I forget how did we
structure that oh just a straight string okay yeah woohoo so now we need to rewrite the assert right so um since we're
returning a result this would be a failure result so we can start off with just being uh is success is false because I
don't method yeah we just have sucess yeah oh um don't want to do it now but uh we need to no I need to I'll Make a note
because soon I saw failure message singular pop up and we need to get rid of that okay uh and we can delete 27 28
because we're not going to get that far right now if we're throwing an exception how are we asserting well we're not
right because we're returning a result so we don't throw exceptions right we we'll eventually uh uh test the failure
message saying not enough rows oh so is our test method already yes so I realized when I I was thinking throws exception
but then uh we're not actually throwing exception we're just so parcel uh returns failure yeah is is that good enough or
do you think returns failure is is yeah I think fails is UN un like what does fails mean whereas return failure we are
literally returning a failure result it's more precise right yeah yep convinced um soul to the highest bidder happen
we'd have to look at the code to figure it out because I don't know what parcel does is if it because it skips the first
one it ends up with empty um so it skips it does a map and a we have no failures because there there no individual songs
that fail um so we're going to have a success that's empty that's gonna that's going to be interesting that's that's my
guess is is it's gonna the test is going to fail because it actually is GNA be considered successful um so should we add
another resar to see about your s your suspicion about how it'll behave sure yeah we can say assert that uh the result
songs is empty it won't get that far so we probably want to do that first if we want to assert my uh you have individual
song it should right and we're checking that first well if we check because false that's gonna fail right there yeah and
this way we want to determine whether the suspicion that that'll be is true that's that's my yep yep so songs was empty
and songs should never be empty if it's yeah uh so that was a hypothesis assertion but we actually don't want to assert
that so we can take it out but now right we've confirmed both that the test fails as expected and that it it succeeded
or did what it was was what we we will we need a test that says hey if no because we're going to take care of at this
never mind I was going to say something on the is what if we have dealing with the scen this scenario as it currently is
is passing or sorry no it failed um but we expected yeah yeah never mind I thought you gonna say like do we have do we
want to always make sure songs or always make sure songs is never empty or something like that but right I'm not sure um
maybe put that at the top of the list and and see so that we don't forget list uh when success is true because by
definition success means we've parsed at least one song successfully all yes we need to change pars all so what's the
simplest thing we could do just make sure there's more than there's at least two rows yeah can we do that within this
one stream or we have a guard Clause ahead of uh because if we do the stream it start it'll consume the stream right um
well we can regenerate the stream because it's just a method on I mean it's slightly inefficient so we could do that we
could create a guard Clause out of tsv song. lines do is after we do the the that uh that the that's kind of ugly that
the partitions is Success yeah I don't like that as much because we we now have to so right now we have a method uh map
map to songs from partition so we'd have to pull out the partition we'd have to get from the partition for empty that
feels less obvious unless do it it would be confusing I think from a readability standpoint yeah I I think it's going to
be better to to do the guard Clause even though it repar yeah I mean we could always uh save off um we could always
convert it to a list and then um create turn it back partitioning yeah asra that's what I was uh basically 26 and a half
like maybe it was 27 and a half when you said it we could check see that's empty here that that's then a nested check
that feels even worse um I really feel like have it must have two lines is is sort of a has very much the feel of a
guard Clause like we should be checking that up front so I think unless you feel differently Mike I think that's no I'm
totally down with it uh actually you were saying we should save something off first so we should do an extra well uh we
can do that for a refracting let's do the the easiest it which uh so we just say tsv songs. lines uh if it's less than
or equal to result and we'll leave the message empty for now we'll ratchet up our test to include that um I think we
need to say size or length uh oh maybe it's do count because it's a stream yeah it's like wait is it size length no it's
count because I forgot lines returns a yeah yeah uh so I does so let's ratchet up our our expectations interesting what
I've always been doing control shift F12 to close windows so I'm going to run the test okay and I normally do control
shift F12 to close the um the test Window M but I didn't do control that time and I just did shift F12 and it still
closed it that's the difference is because restore layout restore current layout which is not a straightforward thing
and it may not always do what you want it to do right I'm have to go look out what up uh uh there's also shift escape on
uh shift Escape which which Clos which hides the active tool window so if you run it and then you do shift Escape oh
right that used to be the my that used to be my normal way of closing right but it doesn't work when you o have yes if
you have two open it's only going to close the one that was that basically had the Focus right so if I do shift Escape
now just close project what if I do it again if we do it will yeah yeah because the tool the other tool window then
becomes sort of the active window got it yeah I used to use that but then I switched to control shift F12 because it's
always yeah always does the right thing yes now we have right right because arrays have dot length so we got do size as
a method Dot length as a method. length as a property of arrays and now we have count for uh streams awesome so uh let's
define the failure message we that actually I just read it from scratch yeah was as as you were like messing around it's
like oh yeah and we wanted to write a nicer uh result do do we want fail your message in this well yeah so this is this
is what I wrote a note about is we want to get rid of uh the ones that return individual messages because we we always
want to be returning uh that was basically just a a parallel change and we actually don't want to return um multiple
right because we're just doing get first which is ridiculous because what if there's two uh what where let's let's
actually fix that now since we have failing test let's fix that now yeah well let me actually go back to the test and so
that we compile again yeah yeah okay now back to result so we want to see who's using this yeah only one test so let's
uh so let's what's the production code that's using it I thought I saw oh oh there is parer's using it from that's not
that method I think intell is confused because that's the static Constructor right if you hit control B on on that where
does it take you there you don't think it really does uh Constructor of what though oh I see what it's doing okay no
that's true all right um so what it's doing is it's Gathering up all the failure messages um but the get verse is that I
mean it could do that and that would that would be okay so what this is this is the part where we've generated results
for each individual par song and then we're we're basically collecting all of the individual which were're so par song
is an individual method right is is parsing an individual song returns a result that may have a single failure message
um it's certainly possible though that it could have multiple failure messages although we haven't done that uh in which
case this maap to failure messages from would would be broken um I think what we actually want to do is do a flat map of
failure 39 now do we want to so this is this is this should be a refactor um so all of our tests that are currently
passing should continue to pass gonna rerun the test before we make the change actually probably should commit um or no
yeah we can commit yeah I'm okay with that I think we can just change it and see if it passes and then flat so flat map
yeah that one messages uh and I guess that has to be a stream so stream oh we we I think you can't do do it if it's a uh
the method you have to convert it first to a method call oh so do replace reference with Lambda yeah uh and then you can
say failure messages do stream yeah so what that does is is it basically uh instead of trying to put the list of failure
messages and then try to then you get like a list of List It basically flattens it out and so you just it sort of it
will will basically gather up since there's only one in this case uh it it should work is there any refactoring back to
uh um I mean you could extract it to a method reference but there's not much do okay yeah it I think I think it's okay
flat map is flat map is always a little weird yeah run it we hope we so um hey a so a asks about the use of Boolean here
on line 37 at the bottom um the only reason we're doing that is because we're pulling uh things from a map and Maps do
not store Primitives yet someday soon hopefully but right now they don't uh and so here's we have to use um so when we
did a partition it partitioned it into two parts one for Boolean true one for Boolean false um Boolean false is all all
the failures um and so the only time I actually use Boolean as the wrapper object is uh when you have to put it in
collections um that are not primitive collections so here it's a key in a map and so must use Boolean um if you're
getting a null pointer exception due to the use of of Boolean you need to to to figure out how that null got in there um
but generally I uh so for for regular Fields no I don't use Boolean the wrapper object I use Primitives um so that's
that's that yes the inlay hints this is like for streams is is the only time I actually want the the inlay hints um yeah
and Mike so I'm not sure if you know notice what was happening with the inlay hint while we were trying to figure out
the flat map is it was doing a stream of R which told us that it was not it did not know what the type of the thing we
were streaming now now it's correct so now I think we can um get rid of failure message by inlining it because the only
place we used it now is in a test and we can just uh actually just change the test maybe not even in line so how was
that used um so I think we can say failure exactly and that should still pass it and it's highlighted as as not using
used for once int does the right thing uh break uh yeah let's take a quick break and then um we'll do the song sounds
good all right um five is righty so I'm going to take a quick break and we come back we'll get rid of and clean up the
song there can you hear me bad something going on with mic setup now I can hear you no I was muted that was my problem
oh okay I rebooted my headset no that was that was a me problem not a you problem ah cool uh so I was saying um now that
we've done failure message singular uh we can do song singular and get rid of that sorry get my head back into it get
rid s uh huh all right so same thing we can do a flat map so let's convert it to map that one's the right one right yeah
yes okay and flat map flap a map flap a map so you want to do tab not enter ah let me do it again that's that's the
difference and it's it took a long time for for me to get used to that so do tab here uhuh rather than enter yes ah and
then it takes care of the wrapping okay we want now songs uh songs plural because we want the one that Returns the list
and then we can do stream yeah y I did tab that time yeah it's gonna be interesting Habit to work on yeah in fact uh I
wonder if I I sort of default to tab anyway and let's we shouldn't have broken any tests yeah I say shouldn't didn't
excellent and now we should be able to get rid of song interestingly enough song is still showing usage yeah that's why
I don't trust that indicator because if you do uh a control B it'll basically report no new usages found so there's some
indexing process that is inconsistent and so I never trust whether it's gray or not the safe delete I do trust because
it will basically internally run the usages so okay all right now let's do a commit um so I haven't watched it yet um I
assume you're referring to to Trisha's uh presentation uh I have her uh her her session queued up um because it was done
in sort of aimed towards European time uh like I wasn't going to get up at 3 A.M and watch it live U but it is luckily
it is recorded uh so I'm going to go and see if there's anything that I don't know I I will be uh surprised happily
surprised but surprised if she mentions know European time is the best time yeah I know it's really it's really
interesting I I don't I I don't understand what is wrong with the United States um specifically software developers who
are doing Java in the United States where are they and why are watching all right did we figure out what we did yeah I
was just kind of poking around we uh this is the main thing we did yeah we kind of did two things um so I wonder if you
if you want to segregate the the commits um you can uh uncheck that and check result and song Service uh so result we we
dropped song and failure message oh maybe we can segregate it so never mind because they're sort of intertwined right so
let's just let's just check them all um so we can just say uh removed the singular song and result uh and then uh yeah
added a test interesting um did we do the rename of parse to parse all in this commit we did yes we did okay yep what do
you want to say about this we're beginning down the path of um yeah I would just say uh added tests row we get rid of
the class name the method it that's interesting Jonas I I I mean I guess I follow like uh Dan vun and and Deshawn Carter
um trying to think of what other Java streamers you follow um I do follow a bunch bunch of the Java folks like Nikolai
uh I guess Billy uh kado he doesn't stream a lot he creates lot yeah I mean it's funny it's like all the people you
mentioned other than me are are uh are spring developer Advocates which is interesting um because like I I consider
myself a a yes A Java streamer but focused on I guess crafter type of type of way of you know clean code and tdd and and
uh refactoring and things like that um and there aren't very many folks who focus on that in the Java World there are in
the C World um but not not as many not any as far as I can tell in in the Java world at least is streamers all right so
what's next um so we require two rows we wanted to nail down the failure message which is how we're going to ratchet up
this test and we took a tance remove the individual message so we wouldn't get confused so now we can assert that
messages contains exactly our our and and now we get to decide what it says say now you're better you're better at
crafting English well so so it's because yes technically that's what we're asking for but from sort of a domain
perspective why are we requiring two rows right um in a sense right now that's that's actually all we can say because we
haven't validated that it's a header row yet uh we don't have a situation where we have a header row and basically have
two rows and the first one must be a header row and we can't establish that here uh so I think that's that's all we can
say here and it's really interesting because I would have I I was tempted to say oh let's say You must have you know
must have uh the header Row in addition to your song data except that's not that's not what this failure is saying
testing right yeah failure is saying exactly what you wrote It's like you must have two rows we don't know what they are
We're Not Gonna validate them just yet um we haven't gotten to these yet exactly so this is this is all we can say which
means we get rid of the first com yep then we run it they should fail yes because it won't beemp should be empty string
yeah yeah yeah and it more where was that when I bring the test back up there he is there it is actually I'm curious why
control W didn't work let me try it again oh it did work I just didn't yeah you hit control a that's what happened oh
but I mean he is nowhere near well I guess said it's kind of near close enough it's kitty corner yep okay so now it
should pass it's close enough that I would I would do that yeah all right yes i' I'd extract that to a method the if or
they yeah and and this is sort of the downside of not throwing exceptions um because normally uh a lot of the whole
thing yeah You' basically just extract the whole thing and say require and it would throw an exception if not um but
here now you can get into some this is where you can start heading down the the more functional route uh where you um
you you actually have a stream where you basically say on failure and on success and so you basically string the entire
thing we're doing in this in this method um and this is is uh what what Scott wasin I think that's I forget how you
pronounce his name so probably butchered it um talks about uh in his uh book around functional is uh Railway oriented
programming and so you basically have just this stream of function calls uh in in a in a stream like or actually using
streams um or using a stream like like structure uh and you don't have any ifs and all you do is is you end up getting a
result out of the entire sequence of of calls um I don't think we're quite there yet in in the way our result is uh is
set up to to do that but it's something that that I'd like to to play around with and so you basically replace the ifs
because what we're expecting here is a result failure but there's no reason in a sense we couldn't carry this result
failure through the entire method and then just return the result and so it's so it's result failure um but we don't
even look at the result we basically call you know like require and it returns a result and then we do the next thing
and we say on success do this stuff on failure do this other thing uh and we just keep doing that until we're done with
all our processing and um instead having yeah instead of having like two ifs um we'd end up with just a a sequence and
so uh that's that's my my my sub goal um or or a goal for for playing around with this but we're not there yet so we'll
just do what we can yes is a Boolean are you kidding me um but you don't like to use require for for for yeah because it
it's uh I we could just say if you know two few lines oh reads nice yeah yeah so it is it is similar to that kind
chaining um yeah maybe has has two few lines is is nicer uh I always go back and forth about that because um there's a
uh what about what's what's the term there's yeah I don't like having negations in in in the thing right because that
that makes it harder to read yeah so what do you think has or without the has if has two few lines versus if two few
lines I could go either way I'm not lines I kind of like that better um by itself the method name might be unclear but
it's since it's returning a Boolean I think uh and I think it it reads slightly better so at least to me so um yeah so
let's let's keep it at that okay uh so yeah so so uh sui not quite sure how to pronounce his last name but I threw the
info in in the chat so Scott lash lashen I'm gonna have to I'm gonna have to watch the video again and see how he
pronounces his name because I never get it right blash I don't know not I'm not going to try um and it's really
interesting because I I am I'm very intrigued by by fshp a a similar language that was Java Scola um because FP is is a
is very much uh a much more functional language than certainly than C uh and it has some really I've I've read some code
in it it's quite readable and it's very strongly typed um so I'm I'm intrigued by it I just wish uh it didn't require a
completely different ecosystem but anyway so this book uh that he wrote called uh domain modeling main functional um
somewhere in it he mentions I think in that book uh he's also got a Blog somewhere um mentions this Railway book I'll
find it uh so he has a website called FP for Fun and Profit um maybe he only talked did a talk so this is the link to
toh to his talk to his blog post about his talk on real ored programming so uh so the slide basically looks um where is
it it doesn't have the individual slide I'll pull it uh I'll pull it up where is it so recommend definitely watching it
I have to rewatch it I haven't watched it in a um yeah I'm just getting the spefic up so this is this is this idea of of
Railway oriented programming so you sort of each step through calling the function um you you're either sort of on the
valid track the green part right so you validate first and if it's no good right like there's not enough rows uh then
you're on the red track and you pretty much just even though you're still calling update DB and you're calling send
email or whatever you're doing um you're basically ignoring it because your all your results are are failure uh and but
if you're on the green track then then you get a successful outcome at at the end and so it's basically an alternative
and it builds on this result like thing that that we've been building um what's called an either uh and you build on
that to to to get this kind of way of doing things um he does caution though that sometimes you want to do exceptions
and so uh he's pretty specific about about that so highly right but we're not there um and that's fine so uh one go
ahead there's one more recommendation in the chat from Master oh about naming which I thought was interesting was
calling it what was it it has I've never done the it before yeah so I've seen I've seen that used um and so like cotlin
uses an implied it uh when it does a lot of the uh streaming like things or functional like things Lambda basically
Lambda like things it sort of names the parameter for you as it uh which is nice because then you could say it dot has
to few lines or something like that um so that's that's yeah I guess the advantage of that is then this if you just saw
it by itself you like two few lines right take a little bit to grocket well so the other thing we could do is is is is
put a a suffix called right then it's if too few lines in tsv songs and then that reads perhaps even more nicely that
gets that gets to some of the uh what I call sort of sugary type of things it's like it doesn't add any right should we
leave it like that yeah I'm cool with that yeah all right um next next test one of these which one of these would be a
good next one I think we have to do one on 14 before we can do the one on 13 yeah new test right viewer uh are we saying
when when uh when missing required columns in header that's better I was trying to figure out how to not do not yeah but
missing required header columns sure let me get rid of the word in it's already a pretty long name par returns failure
and missing required HCS that's not that that long well but we could have done this right it was I'm joking because i'
I've written way longer ones yeah okay can we steal steal from down here a bit well so let's let's talk about what what
what um because here that like there's multiple ways this could fail uh we could have all the columns except for one um
we could have none of the right columns uh right because we didn't include the header row at all so maybe we want to
start with basically we forgot the header row and uh and we might even want to parameterize this but I think we should
start with the header row should um so I think I I basically I think I'm getting at I think it's harder to write the
failure one because there's so many different ways it could fail versus that row should we disable this test and then
positive this yeah and I think in this one um I'm not sure if this is what what astd meant by in the wrong order uh but
one of the capabilities that we're we're wanting to implement is that it had the header row has everything we need um
but the columns are in in the wrong order or quote wrong order uh in the in the non uh in a different order than we've
now so is that what you were thinking a different test it's a positive flow it long I think so well I I I I don't I
don't know for for sure so let's let's go down this way and see where we end up okay and if we end up wrong uh we're
we're committed right we've done a commit recently yeah check uh let's commit that refactoring so just the CSV song
parser not the test class right is that only pack that one let me just double check yeah because it was over factoring
it shouldn't change shouldn't have changed any sure all right so yeah so let's go down this road and and see where where
we end up just i' probably copy that um but I'd inline it because we want to actually see the yeah yeah we could do that
I I I think we W to we're gonna end up having to do that pretty quickly so um that meaning was it something sui yeah was
something suiga said Yeah so basically something in in that just ases the but I'm not sure where that head person will
um well clearly this but that will just succeed so I want yeah I want I want our test to fail right uh to force us to to
actually do some header parsing um so what I was going to suggest is uh we move we um we drop the columns that aren't
order okay so we had release title was not required now also the tab is that what you're thinking yes or just pay it
okay so and we don't want release type I don't think the release type is required either notes yeah contributor careful
about your n there we still need it the N yeah now you lost the N oh you still need the N that's sorry backwards um I
mean this will fail too uh but I think we want to really push on the fact that order doesn't matter I mean will this
fail if we we're going to test what success yeah because right now are we even looking at the head of row or just
skipping it we've just been saying there must be at least two rows and that we skip the first row so we haven't seen the
first row as a as a header right um and that's and so we need to update uh assert we're going to do then well we we're
not finished with our setup because our Our Song data needs to match it nope it didn't work I wonder if you can uh can
you try hitting uh Alt Enter and can we say um can we say inject Choice yeah just do it just hit enter yeah t uh it
doesn't have tab separated um that's a bummer uh what I was hoping is that we can inject tab separated values as the
language and then we could edit it as a fragment um but it doesn't have that I mean there may be a way to do that but I
don't think we're set up manually uh and let's drop uh I guess now ah leave it or keep it I mean let's um so this will
so now what we want to say is this should be fine right it has the requir right it has the three one two right because
we we maybe bring up our our Jura uh yeah so are song title and theme is the only thing that's required um so the
statement in our Jura our actual Jura story is actually wrong right because we said requires eight columns but actually
we don't require eight columns so maybe we need to change that right we require we only require really three columns is
a minimum three three to uh to six right yep six off by one I'm a software engineer yes that's my fence post okay so
where we said uh must have at least these eight columns is actually must have at least the uh at least well three um and
uh maybe we want to pull the the requirements okay I don't know what this bottom stuff is I'll go look at it later I
want to get I'm just gonna copy it rather than you can probably delete the to-do right all right so um what we should
probably do is add on on 65 and a half what are the minimum need you already said must have these three columns and so
I'm basically riffing off of that so so it's artist song title theme one and then maybe indent that line and then on the
next line say uh we columns and then other columns are six right or well no we're so the Mac so three is the minimum
right that's required um and then if you have any of these we'll use them and we'll ignore others right one two three
that right um but I put the where you say on 65 other columns are ignored that actually belongs on 67 because we're
saying support these eight columns and any any other columns will be ignored that's true uh and 69 is now it yeah that's
better all right so let's go back to our test Now with uh with our new knowledge what we want to say is this should pass
so our desired Behavior right what should it do is this should pass it has um in fact we might want to just have theme
one maybe since that's what we just wrote that the required columns uh is only three then let's get rid of the other
themes yeah so we said we stated that that was our minimal required columns uh and that should be success um and this is
probably going to propagate a whole bunch of changes uh that we will certainly not get to today no um so look right so
we've got artist song title theme artist song title theme that should be success because we're saying that that's our
required column so it's going to fail because we says yep now do we want to ask it through a a a deepening assert like
why did you fail or you know have it the message well we're we're we're expecting it not to fail so there's nothing more
we can do here um other than put another assert but it's not going to get to any other asserts that we write uh so I
think mat yeah go um yeah contain and see what it said well the the proper thing that would be a valid assertion would
be is is empty because if we're expecting success we expect then the failure messages to be empty right right right um
it would still allow us to see the error messages though so if that's what you're trying to do then that's what I was
trying to do just want to see the error message yeah so we can say is empty and we'll say oh it's not empty um that we
were not doing a weird contains exactly yeah so our uh our ancient assert around must um what are you looking for oh the
ancient sorry when I said assert I meant I meant guard Clause so in our code we we liter we have hardcoded minimum
columns is nine uh right there on the line above that you scrolled away from yeah on fth um relax that expectation right
uh we can change it to three and see what fails see where El it fails so the so hopefully we have some place where it's
passing in uh an expecting failure uh for having too few columns so let's run our tests and see see a test for that well
there wouldn't be a test directly constant yeah we got a bunch of failures where um yeah so in fact our par single song
test is the is is the most interesting failure uh and so this is the difference by the way between the the red
exclamation points and the Amber or orange or whatever you want to call it X's um the exclamation points means some an
exception was thrown uh which is fine but is not a bad assertion what what we want to find is assertion um so uh the
error message is is what's wrong here um because it had it said we were expecting it to say nine and and it's saying
three um we can look at the other ones but they're all but they're all about basically the guard Clause failing these
guys when you say others I mean the exclamation yeah yeah on right so that one's out of bounds what's the one above it
handles RS with nof columns yeah yes they're all probably going to be the out of bounds yeah yeah so we're coming up
against time um so uh I think this is probably where we we'd stop um because now we got a failing test uh and the next
steps we'll figure out we'll have to figure out like how do we want to approach fixing this um because relaxing the
constraint uh causes a bunch of tests to fail so do we do a parallel change or do we see if there's maybe another way we
can we can do this um do we disable the current test and say Let's test directly against par song because that's really
where where the meat of of what we're going to do has to happen right um but it's still a bit unclear what the
parameters to par song are going to be it because it needs some kind of Header information whether it's the actual
header row itself um or a pre-parsed sort of mapper that's that's an unknown and we'll have to figure that out so I
guess if we do directly test against parong we'll be able to try those tight end rather than trying to do it from parsal
actually par hard I think we still need to do something with parsol because um I'm not sure whether par song does par
song parse the header oh who's gonna get that responsibility right right um and I I think uh I think I think parsol will
have to parse the header it doesn't have to but I my theory is we parse parel parses the header creates some kind of
mapper and then hands that into song so perhaps something around here instead of skip we yeah we would basically consume
we we take the tsv song lines we'd consume the first value as the the header go parse it and then do the rest with with
the with the parse song with the remainder yeah but that's going to be a little tricky yeah because we're gonna well
we'll take a step by step and see how it goes yeah next time we meet y all right folks that's all for today thanks so
much for joining us uh in terms of next streams um uh I might be streaming this afternoon uh so look out for that if not
um possibly this this weekend there might be some streaming so as always uh you will find information about um upcoming
streams on the Discord if you haven't already joined join the Discord where uh we'll talk about upcoming streams as well
as all other stuff that you can ask questions about and find out resources and we've got a book club as I say it's never
too late to join the book club so check it out we're reading the programmer's brain uh and that's it so we'll see you
next watching
