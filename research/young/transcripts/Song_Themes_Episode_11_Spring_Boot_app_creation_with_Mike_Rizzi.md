# ＂Song Themes＂ Episode 11： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=ud-zS5ch1eU

---

## Transcript

all right we're back hello everyone howy so it's been a couple weeks since uh since we last paired has it been that long
time flies yeah time flies I think it's been almost that long hey astred hey astred nice to see you uh but luckily we
left ourselves a uh a breadcrumb so we'll we'll pick that up um one thing I want to announce is uh in my community uh my
Discord Community we um one of the things we do is we have a weekly book club discussion and so we just finished uh the
learning domain driven design book and so now we're currently voting for the next book uh voting will take place for the
next few days and then we'll decide on a book and then we will read and discuss that book so if you're interested in
joining that uh go ahead and if you're not already part of the Discord you can join the Discord if you are a part of the
Discord uh and you're not in the book club um there's no charge uh I just need you to send me a direct message to so I
can verify that you're a real person um and then you'll have access to the book club even if you can't make the Sunday
uh live discussions that we do on Zoom so we spend two hours on Sunday mornings actually during this exact time time
slot uh so whatever time this is for you this is when the book club would would meet um if you're not uh even if you
can't always make it um I always encourage you to come anyway even if you've fallen behind the reading come anyway uh
really it's it's it's very very low uh low formality uh kind of thing um you can just chill and listen and lurk uh or
you can participate um really it's it's it's mostly about um having people figure out you know what the book says you
know we pretty much read a chapter a week so so not not a lot of reading required um but I also really want folks to to
use the book also as as f for discussion about other things that are going on uh in your in your professional life hey
dudan so again um join the Discord if you're not already part of it if you're not already part of the book club uh
there's a special channel for for that um go ahead and and send me a direct message uh and we are now currently voting
for a book there's I think 19 choices um not always easy to choose uh but as Mike can probably tell you uh but um do
your best so all right that's a little get that out of the way so um yeah so what's what's going on Mike what's what's
going on with with song themes well like you um it's been a couple weeks and I haven't looked at it at all so we're
doing this cold cold turkey if you will or whatever the inverse of cold turkey is now that I think about it um going in
cold I think is is the right term going in cold yeah so I don't remember but we looks like we left ourselves a little
breadcrumb here um and we also probably have failing test but I don't know let's run the tests and see I know since last
time you updated uh popped in and updated the spring version if I remember correctly yes so it's in fact we can we can
do it we'll we'll probably want to upgrade again nothing urgent there because 322 was just released this past week um so
we'll upgrade to that um but these are all minor upgrades so so shouldn't affect us too much but you could probably
check off uh you could either check off 39 or you could change it to upgrade to 322 um depends on if you want that
dopamine hit or not of checking something off yeah good point good point dopamine cool and I think we had a build fail
yes so we we have a uh we have two tests failing um and I think it's um so one of the things we we did and I think we
finished this off last time was uh we were adding more attributes to our song so we have artist song title release title
releasee type and then uh and then themes and so the thing we finished off was was refactoring that so I think I think
we can actually call that done because we did that because we wanted to now import from from your spreadsheets so I
think I think we can call 37 done we have an import ah here it is wait on here no but we can just move well as part of
that I mean you know whether you call it UI or not um right we we why said we're going to do the the subcutaneous part
which is because the UI is basically here's a big text box and that's it um right let's see are we adding songs via
bulkload I don't think we can check that off but the one that we can't check off 37 we can I think we can check off
because we have modified uh song to have additional attributes and this failing test is failing on the parsing not on
the adding attributes correct okay so uh and we might want to revisit uh since I think from last time I claimed that
that Excel could easily export to CSV using double quotes around field apparently that was a lie a lie and so uh I don't
think that'll make too much of a difference from our implementation um because basically um relying on on uh well
actually I don't know uh I think we're yeah we're relying on the CSV parser um Library we using it yeah yeah so we're
using that in the CSV song parser class one of the things I was thinking about is and this goes back to a question that
came up when we were figuring out what library to use this is such a uh like do you do you include a library when
libraries tend to be fairly generic um but here we're like literally using what's basically one file um and one class
and so you know it does do you copy and paste the the code into your library and um I was looking at the the code and
it's like it's not a lot of code we might just want to copy it but I figure let's let's get our let's get it to work and
then we can um then we can figure out what we what we want to do yeah I guess I would my initial reaction was like well
what kind of frequency are they updating does it matter you know is it so it's it's an you know it's an RFC so it's not
going to change like sort of the whether it has double quotes or not um if comma separated and if it does have double
quotes with an embeded comma then it'll handle it uh honestly I actually had um chaty PT write write the code for it uh
it's not it's just not a lot of code and so I think we'll probably want to do a drop in replace of of it because it's
really not that complicated um right so and do we need a full library for just one class exactly for for for a class
that that ends up we're using you know maybe 30 lines of code of of it so yeah and with one less dependency which as we
know dependency are can be deadly yes yeah hey control Dave twitch coffee oh I should open up my twitch that's the
downside of streamer is I don't see the twitch stuff look get my stream I wonder if control Dave twitch has twitch
because they're on thanks for the caffeinate I will follow through on that um I'm going to reject one of your caffeinees
I'm not going to yet grab that one reject that one all right great um oh so one thing I put in there so you can see uh
there on the top with the par um a mentions the left pad yeah don't don't have dependencies on on on like a one or two
line thing like just just copy and paste it like I you know it's really funny is like are there's guidance that that has
in our industry and this is probably true of any profession that have been interpreted by a lot of folks as these are
hard and fast rules right so you know dry at it is I think one of the most dangerous things to to to interpret strictly
as don't copy and paste code ever don't have duplication ever um you know in terms of actual you know syntax level of of
code and I think it's just wrong and I think it gets people into a lot of trouble I think it actually makes things worse
and um and that in in a lot of cases that wasn't even the intent of of of dry dry was more about what you know what
information and State uh you want to make sure not Not Duplicate and um I I think interpreting we must not you know copy
and paste code C I mean yes if you're copy and pasting you know 10 20 lines several times then maybe you want to think
about about uh sort of some kind of refactoring to reuse but I think that for me connects with this idea that one of the
benef one of the top benefits of objectoriented programming is reuse and I think that's actually a mistake um I think
reuse is great if you get there through actual use um but designing for reuse is is actually really hard as any Library
developer will tell you so I think dry and and reuse are are way over over especially those less experien over over over
index on that and and I'm here to tell you you can copy and paste code it's fine you can copy and paste code from from a
library if it's open source you can just do that uh make sure you buy by whatever license there is but copy and paste it
um maybe rewrite it yourself to to learn a little bit but if it's you know if it's one class or even like one method
just copy and paste it don't bring in a don't bring it you don't have to bring in a whole library and you don't have to
library yeah d a minut is odd just return not it's even yeah that's right B blam yeah uh single point of Truth yeah
exactly that's why yeah I don't I don't use dry I use I use spot single point of so all that's to say at some point we
might we might replace that uh what I want to say is the stuff at the top is if we wanted to you uh right now we're
Escaping The Double quotes um but I I just wanted I I sort of put in the usage of text blocks which makes it slightly
more clear although I am annoyed by the the trailing backslash at at the end of the line to prevent an actual new line
in the string um when we get to multi-line CS V's uh then we'll we'll probably go to text blocks but I feel like it's a
little I don't know how do you what do what do you think of of of that I I think 16 18 is way more readable than 13 okay
if that's what you yeah yeah so if we want to switch that that's why I put that in there so we have that option yeah
let's just dump that and then we can get rid of the comment or should we leave the comment I think uh I would say I
think we I think this yes because yeah I think leave that part of the comment last line has to be so everything through
the butt you could probably get rid of the butt get rid of the butt or leave the butt get rid of everything else uh and
yeah so um so since I lied about what Excel would would actually uh save it as um the if we think about lie you just
didn't know just I was I was I was wrongly confident and I was wrong so anyway uh do we want though to so there there's
going to be two different forms of of import presumably maybe not you tell me um one is here's the file upload it uh and
the other which we're sort of currently working on is let's copy and paste from the spreadsheet directly into a text box
um if we're copying and pasting we probably want to use as our example a literal copy and paste uh from the spreadsheet
just so we can see what it look looks like right because I don't know actually what Excel would put into the clipboard
right I can guess but I'm not sure so maybe we should try that before we sure nail down what we're actually gonna gonna
just pull out some Li here my text editor let me bring in um and and asra says can you find a song or something or band
name or or any or title that has a comma in it so we could see what that looks like right um even if you have to fake it
that might be a good idea let see this is gonna be a funny search search for comma that's in band ah yes Earth Wind and
Fire yes yeah it's not too bad and it's near the top do they use the Oxford comma oh my God is it Earth comma Wind and
Fire or is it Earth comma wind comma and fire sorry I had to do that what um I guess we want to be able to well two
things one is we would we want to be able to skip columns that we don't need right because at the moment we don't care
about contributor actually looks like I've got some hidden columns here what are they oh links to lyrics so yeah
actually interesting actually I want to do a does what does if I do a copy if it's hidden does it grab it or not I sure
hope it doesn't yeah I'm gonna go to there and worse oh that's interesting all right so worse as far as the format goes
yes yeah there's no comma can you a tab probably a tab yeah it's probably a tab it's a tab I can feels um so I wonder is
there an option under the edit menu to co to copy in a different format from Excel copy in a different format
interesting so on the menu menu menu the top menu you mean up here when you say top menu you mean this oh sorry I'm
thinking Mac um where is the menu where's well this is the menu it's a ribbon they call it this whole thing right but
there's on the Mac there's a menu in addition to the ribbon really yeah because there should be an edit menu somewhere
oh uh let's see if it's one of those hidden ones they have this quick access toolbar here new open email I'm not seeing
edit can see if it's in the edits as a you might have it turned off all right no worries in the in the left there is the
clipboard um section there's a copy button there yeah it only does copy or copy as picture so uh um so what do we want
to do do we want to assume that you're not going to copy and paste since that's not going to work for us yeah I mean we
can just say I mean at first I'm the only user right so I could just do export well not as PDF but uh where is it CSV is
in here somewhere is could do that route yeah which will you know dump to H to a CSV file so if we're gonna do that but
then it dumps the whole thing not subset bummer I mean it is so if we paste that in so if it is tab separated that's
fine too right I mean the splitter the the thing we split against doesn't have to be a comma right um as long as it's a
character that doesn't appear in the text itself that's fine I mean tab is technically better because it doesn't you're
not g to have generally tabs in your text uh one would hope if we paste this into uh Java code so just paste it into
like a a text block sure what does it look does do the do the tabs basically do the it which test were we just working
in this one right yeah actually was the other one well that's the one that has the text BL so if you if you just
duplicate or just create a new string and we'll do a multi-line string yeah and then just paste whatever's in the
clipboard so those so it feels like the tabs are there yeah um do we want so what do you want to do what's it's it's
sort of you know you're going to be the one importing the spreadsheets what what is what is it you'd like to do here
well I mean I see it as two steps one is we want to import like a subset for initial development and then ultimately
dumping the whole thing right so it seems like supporting a subset in other words a copy and paste approach versus
having to go into Excel export to CSV delete a bunch of rows that we don't need just seems screamingly tedious uh to me
so it seems like being able to copy to support copy and paste off the top of my head seems like the way to um so um what
do you think another another option is we always do tab to limited because you can export uh save as uh a tab to limited
text yes yeah you can um and so then that will think it's as and then you can select but I believe the selection there
is only down there noow oh text text tabed limited so up five up five oh there we go oh it does it as txt file
interesting right I want to see what yep hit that drop Dropbox pop up um um let's see if I available so while you're
doing that I'll answer a question from from Chad good hey remixer um you're G to have a tough time finding uh a project
to contribute to that's not the framework itself um so the issue is is that the kind of stuff you'll find that's open
source um that uses uh Java and spring boot tend to be libraries and Frameworks and things like that there aren't a lot
of sort of applications um which I think is is unfortunate but um the fact is is is there aren't a lot of them and the
ones that I've looked at because I've looked at a lot of them mainly to to find examples for uh for use in in in
presentations and training um they tend to pretty big um and not well structured and so not not very friendly to uh to
to to contribute to um so I would sort of turn the question around say why do you want to what kind of project are you
looking for and what's your purpose in in doing that because there are different kinds of projects and there would be
different reasons for for you to do it if you just want to contribute to an open source project um then I would say find
find small things whether it's little documentation improvements or or API uh documentation improvements certainly
spring Boot and spring framework could use a lot of improvements there uh because it's just so much that could always
use improvements um but if you're looking to more application as opposed to library framework uh then then that's going
to and so as mentions a resource on on finding a project in general um I think it's really kind of unfortunate that
there's just not like I've got several projects that are open source that use jav and spring boot um and certainly open
to to pull requests but but yeah it's like again sort of what's your goal right so in doing any of these things right
working on your own stuff contributing to other stuff it helps to to know sort of why you're doing it there has to be a
purpose to to doing it uh and you want to think about what is that purpose um because that will help guide the kinds of
things you can you for all right Mike what what have we got what you found well it's the big bummer is it doesn't honor
the hidden so the hidden columns so well yeah I mean I would not have expected the save as to to honor hidden yeah no I
know but it's just it's sort of the um eventually you're gonna have to so uh eventually you're going to have to if you'
re going to want to import a whole file you're going to have to export a file that um removes those columns right yeah
and that'll be you know theoretically a onetime event right so and but then the other thing is at that point hopefully
we'll built enough where all the columns are useful Le yeah and and again we can't always you know add the function I
think we've talked about this I don't remember if we talked about it on stream um we can ignore columns right we can we
can code that so that way it's less less work less manual work for you to do and less um exactly and I always look at is
is is two things one is make it easier mistakes um and so if you know for example if you're constantly having to copy
the file and then remove the columns and then you you mistakenly remove too many or or remove not enough then uh uh we'd
want that the application to um adapt to it to adapt to that yeah instead of the other way around yeah I'm thinking at
this point just straight copy and paste and and that'll grab the columns and you know we can actually have it so that we
grab a column we don't need right practice ignoring it right um because I think the whole export thing is just too
tedious um frankly error so I'm going to have to actually get the right colums that we want because I hid too many
speaking this oh now this is the txt version let me go back to the original see if the txt still open it is close that
one don't save don't care okay what do I got in here unhide oh right moment oh interesting oh bummer let me close this
for a sec I'm GNA go over another computer yeah don't save back in a sec I'll answer some chat questions H whoops uh so
remix you say I like the fal idea and philosophy I think it can help improve my skills um I'll be honest with you
contributing to open source is not a great way to improve your skills unless it's um unless you're very sure that the
project is going to provide you with useful feedback uh in my experience a lot of projects unless they're big and
well-maintained and sort of well supported the maintainers just don't have the time to give you feedback on what you
contributed um so if your purpose is to improve your skills I I don't think it's the best way to to do that I think the
best way to improve your skills is write your own code um write your own code create your own project um use op Source
stuff um maybe open source your project uh but I think Far and Away the best way to improve your skills is to create
your own thing um because it's unlikely you're going to be able to uh you know there there's a lot of projects um and
again depends on the kinds of stuff you want to work on uh and the kinds of things you want to learn um so there is a a
a an advantage to contributing to an existing project because you can get experience working on a large project and
contributing to it um but it takes a really long time of project that's of of any size is going to take a really long
time for you to to get into it enough to be able to contribute a non-trivial piece uh and then you also have to find a
pro project that exists where it's not you know it's non-trivial and where the maintainers are going to be able to
provide feedback um a lot of times again they just don't have have the bandwidth to be able to provide deep feedback and
it might just be like we we can't accept this um you know so uh you know definitely support the idea of of of I I got I
gotta say that that I that I think you're going to improve your skills much more by creating your own project and
working on things that that matter to you and I talk about this on almost every stream it comes up it's like create a
project build it yourself just like what we're doing here what Mike and I are doing build a project that's meaningful to
you that does something it doesn't have to be big um but as you approach each little problem like what we're looking at
here is like do we want to do CSV or tab Del limited how do we do that how do we parse that um those are going to be
real problems that you will then have to solve uh and then you will you will improve in in in that so building your own
projects you won't get feedback from others uh necessarily but you you can there are places where you can say hey what
do you think of this code in fact I see that uh fairly frequently on Reddit um and and some other places uh but the
feedback you'll also get is you will be using it and you will be writing it and so you will have to make it work um and
so there's a there is a certain amount of minimal feedback uh but I don't think it's any any worse and probably better
because you're going to be able to to ask for hey you know there are various communities that that can that can provide
that feedback um you know and and they're uh depending on on how much you know money you have to spare you can also pay
for for coaches to provide you feedback uh you know I do that um I don't I don't do it for free because it's it's it's
expertise but there are uh free communities that that can give you feedback But ultimately um you will also get get
feedback just by trying to to make it work yeah it's an important point because um as you're working I mean you'll make
it work but you'll also find the road bumps here the bumps in the road that make you go oh what's you know why is this
hard why is this difficult yeah so I'm gonna slightly disagree with bass blam here I think doing code and katas is
worthwhile um as long as you have a very specific goal of what you hope to achieve doing the the Kata um there is a vast
difference though and this is why uh I think it's useful as a portion of your learning there's a huge difference between
doing katas and creating a real application there's going to be stuff in a real application that you're going to have to
figure out that cotas don't cover because kotas generally don't do a lot of things like present a UI and persist to a
database and the fact is is that in most applications that's actually the hardest part um or at least integrating it
together and making it work uh the one thing that I would say is um make sure you know how to write tests learn how to
write tests and if you're going to do kadas do kadas that uh really guide you to use tests especially test driven even
if you don't like it it will give you practice on writing tests which I think is one of the most important things in
development is figuring out how to write tests because design um so you can join my Discord in case you're not already
there uh and you can get in touch with folks there um my community tends to to skew a little bit more towards more
experience but there are lots of folks who uh who who are willing to to provide um some you know answering questions um
but you can also say you know what communities and might be more appropriate for this and there yeah and so so cotters
are great as long as it's not the only thing you do is is Rel thing so definitely important part of learning um I I do
kotas when especially uh and a cotas isn't necessarily even creating you know creating something sometimes it's uh like
I do refactoring codas how what are the different ways I can refactor this code using automated refactoring Tools in in
something like intellig idea uh and practicing those and trying out different things um and that's the goal is to sort
of experiment uh try different things um with cottage you can do things like hey can I write this without any if
statements can I write this you know without any any you know decision statements at all uh no ifs and no switches what
does that look like doesn't mean you're necessarily going to do that but sort of really expanding uh the kinds of things
you look at also um one thought that comes to mind you could also if you if you feel like you need you feel like you go
too long before you check in code you could have a timer you know and when the timer goes off you have to revert to
whatever the last checking was right sort of to force you to learn that you know I think of cot is a lot for building
habits you know whether it's keyboard shortcuts or refactoring techniques yeah and there's no sour of katas um yeah
Emily has a has a whole bunch and in all sorts of different languages um and so uh you can start there I've got a I've
got a a few um and you can get lots lots more suggestions in in uh in my Discord and yes the testing and going and and
and taking the tiniest steps possible and practicing that can I take even a smaller step uh will will be invaluable uh
no matter what you what no matter what kind of code you end up doing all right let's get back to spreadsheets okay I've
got the columns I care about and I'm leaving in two columns we don't want to use uh the notes column and the contributor
column for now that'd be a future thing so this um so it seems like it would give us information we care about plus some
things we want to ignore so um what do you think just grab up true Earth Wind and Fire sure or because do you want the
contributor in there yeah I was putting in column that we're gonna ignore got it got it I was if that's okay I was
thinking of that yeah and the H column the notes is now there we go there's a clean copy let again so do we want to dump
this all into uh this test yeah well we've got we got text BLX so we can it'll be pretty readable yep let's go back here
take that out and dump oh it didn't interesting now this test we the test is currently failing so we were just doing
this to see what it looked like right off so we probably yeah so I think passing first yeah so I think that I think what
we should do though is is grab grab um one of those lines that we can use to say can we parse a single line because
that's what this this uh at least this test was at least where we are in the code was originally about was to to just
see how do we can we you know can we successfully parcel line interesting yeah keep going uh and then we can then we can
expand to to um to multiple lines and then we can expand to dropping columns Okay so grab a line with content yeah
versus a header column here there we go now it's tab delimited no longer right which means it's not gonna which which
really means it's it's going to be way easier to parse because we're not going to have to deal with uh commas that might
be embedded um because we're not using commas separated and here we don't even need to use the multi-line strings
because we don't have to escape double quotes or anything like that so we could probably just go back to well actually
there is um so in the there are some with quotes still so see here there's quotes for this one um so but that's part of
the text true oh right we're not saying quotes yeah yeah yeah so we're we're going to be slicing along the the tab which
means that'll that'll do just fine okay so we'll dump 15 so endofunctor zero asks uh would we see the CSV parser as an
adapter part of um that's a good question I think um so the question I always ask is would we expect a of in other words
are we are we parsing only because that's the way it's coming in from a specific endpoint a specific adapter so if for
example we were writing this as a command line tool also would we have the data in a different structure um and I think
here it's actually a part of the application so if it were well the web UI we're going to do CSV or or tsv tab separated
um but the command line is already gonna H is going to have a different format like a pure Excel spreadsheet or we're
going to get it in from some messaging feed where it's a completely different format then I would probably push that
parsing into the adapter but here it at least right now it feels like it's actually part of part of the application I
guess if we supported two uis one where you copy and paste into an edit box and another one where you use a file picker
to bring in let's just say an Excel spreadsheet so then they will be two different it's an analogy to what you were
saying basically yeah in in that case I think it's it's still the one that's uploading a file would eventually translate
that into here's a bunch of strings right so there is some adap one adapter there yeah yeah so there'd be some
transformation there but eventually it's it's not going to transfer all the way to the songs that it's still going to
pass here's here's a bunch of yeah and yeah I think we can assume that that Tabs are not part of any at least not
intentionally part of any of the so um so yeah so we don't need to use multi-line strings here at all is it was my uh
was my suggestion that we can just make this you can just join it so if you do control shift J and then again keep going
now you can just get rid of the triple quotes and is that space before Earth part of the yeah interesting I'm trying
actually look look together was like 24 right no there's no space there interesting can we look at the yeah going no
space there either yeah so that was yeah all right um and we're since it's no longer technically CSV we're gonna have to
do some renaming um but uh so let's at least name we're red yeah let's let's it I mean we're we're changing our red so
so let's change the the let's change all the names to to adjust at least in this class to to be uh call it you could
call it tab separated so tsv I don't know what if there's a standard I don't think there is I didn't see that uh heard
of tsv um yeah tab separated values tsv it's a Library of Congress says it's a file format so we can use tsv tab
separated values I kind of want to stick with the full word um I like only use abbreviations when I've I've used them
for a while and they're like I'd be like what's tsv oops all so IND ifter zero that's a really interesting question I'm
gonna actually disagree um the the operator the users of this actually do care about the file formats cuz they're that
is part of the business that's part of our domain um it's one thing if you have two machines exchanging files and you
don't care what format that is uh then the business doesn't care but here the business actually does care hey we want to
be able to import files of this format into this system um so it's not just arbitrary things ultimately it has to be
some specific file format and so it could be that you know if this thing were you know popular and people wanted to
import stuff and they were using a different tool that actually generated comma separated uh instead of tab they limited
um then uh that would be an additional use case so these are even though it does seem a bit technical it is a use case
it is a we want to be able to import tab to limited files we want to be able to import Excel spot Excel spreadsheets we
want be able to import from a Google spreadsheet all of those are use cases and yes part of them have a technical aspect
but that care yeah absolutely so right if if we need to process a file because we're integrating with a system um you
can bet the business cares about what those documents are you know generally their XML uh and cares a lot about the the
technical format um because we want to be able to support you know uh and there there's you know especially when you get
into to areas like uh health insurance and uh there's oh my gosh is the the the mess that is those file formats and
electronic records so so there is a lot of stuff where you're you're integrating things and even if you're um if it's
not through a UI it's still it's fetching it from another system you know maybe file uploads still happen FTP and so on
uh the business certainly cares about making sure that those file formats are correct so so it is dangerous to to sort
of assume that that business doesn't care about technical aspects there are some technical aspects that the business
cares about yeah absolutely see CSV is is a is a one of one of the more common interchange formats um it's it's a
terrible format if you if you have any control over it um but lots and lots and lots of apps use it yeah it's a it's a
really good question because because I know for me you know my my tendency is to say is this really you know is this
something that uh uh you know business person cares about and there's a lot of stuff that no no they don't care about um
but this this they definitely do all right um what you looking for I was just browsing oh okay so I renamed the test
class I renamed um actually I still got this one to do and so I'm actually doing a mix of tsv in some places and just to
sort of start the education of but not get go overboard works for me works for me cool uh so let's update our assertion
um so we actually know what those values should be in fact we can uh you're gonna say something we can actually expand
let's let's actually make this a bit simpler because it was failing before because we were creating a song that had some
default so let's actually make this a bit um um as in change line 14 no no as in change our assertion let's let's start
out with a simpler assertion let's just start out that the song uh the songs that we get um basically uh just pars the
the the artist so we can do is um on 19 and a extracting and we can say uh song colon colon so we'll get a method handle
which will basically be uh one of the attributes and let's grab yeah let's start with artist so let's just check that we
get the artist and then we can uh for that then we can just say Fire because then what we can do is we can just get that
to work and then we can expand uh more right more and more so these are the small steps we take remember we just talked
about that folks I'm G to kick off the run so this will almost certainly fail because I don't know what the heck it's
going to do yeah now was this song service test an outer test that we probably want to disable for now uh yes that's a
good point so let's go disable that um and indicate that that is uh basically we can put a comment saying disabled until
the CSV sorry T done that yes the and a half is is something um I forget who I've learned it from first uh but it's it's
common in uh especially uh any kind of remote pairing situation because it's a lot faster than saying can you go to line
19 and add another line between 19 and 20 just say 19 and a half I think I learned it from loyel andico it also works
for non- remote pairing as well you know sure although it's a lot easier to just point can you add it over there that's
true with pairing with ensembling in person yeah the monitor is a lot farther away well yeah all right so um oh the
failure we wanted to see the failure uh yeah the failures irrelevant because we're going to actually delete the code and
start over because the parsing is going to be way easier so on the code below uh Delete yeah um and uh you maybe change
the variable name and so um since it's Tab delimited and we don't care about and a tab always delimits it no matter what
where it is uh we can just use string split you start implenting at this point uh I mean I guess now we'd have to return
a list of we could return an empty list I think we we can go beyond that I don't think we have to take that tiny step I
think we can we can Implement right away uh so if you just split first one yep and then uh back SLT backslash T yeah
they're backslash Yeah so basically split on tabs right um and that returns an array oh yep actually I think we can come
up with columns um and then let's create a song Column what does this guy need again is it control parameters it control
shift p yeah that's the type info if you want parameters then it's oh it's control P okay artist song title so artist is
going to be the First Column so let's stick that in there and then the rest we can just put empty stuff I didn't count
how many columns there were needed I always hit control P to figure it list oh uh lowercase e because it's going to one
all right and then let's return a list of that song run so uh can we switch back to the test that we're actually
expecting to fail yeah um I think this will pass right yep yep sweet um did you want to take a a break at this point
yeah I could use a quick bio break okay thanks for asking all right uh so we'll take a a quick break and when we come
back we'll expand our song uh parsing so stay tuned all right n uh just a reminder um I run uh a weekly book club we
just finished a book and so we're voting on the next book if you want to participate there's no charge um what we do is
every time during this this time on Sundays from uh from 10: a.m. to noon Pacific um um so basically whatever time zone
you're in from an hour ago to an hour from now that's about when it would happen on on this day and what we do is we
discuss a book um so we're currently selecting a book generally technical oriented books sometimes more conceptual like
the learning domain driven design that we just finished uh sometimes really getting into code which uh some of the book
selections are there um so if you're already part of the Discord and you're already part of the book club make sure you
vote because the more you vote um I mean only vote once but the more y all vote I can't actually detect if you if you
vote more than once but don't do that uh but the more of you all vote the the more likely it'll be a book that you that
you're interested in uh in reading and um then we'll select the book and uh give folks time to get the book and start
reading the book and then we'll start discussing the book um and if you've never been part of a book club no pressure
you don't have to talk you can just hang out and and listen um but I find it uh one is it it really helps like oh crap I
didn't read it let me go read the next chapter and even in it's much more likely you're G to finish the book and that
you're going to read the book and understand it um much more than if you try to to read it on your own um that's mainly
selfishly part of the reason why I I do it is because I want to read some of these books and and really dig into them uh
and doing it as a group is is a great way to do that agreed it also helps with like you said with the discipline like
it's like oh I bought this book I keep meaning to read it but if it's like Gotta Have chapter nine read by Sunday yeah
so there's a little of accountability but but of sort of the good kind so right to thyself not to the group exactly yeah
often all right um you want to expand right so yes uh we probably want to do a commit since we currently have all Test
passing and we've done some non-t changes yeah that's absolutely true BS so if you don't read it I won't know and it
really doesn't matter um showing up uh is great but even if you can't show up at all um the uh the discussions are
recorded uh so you can always access them transcripts are generated so you can always search and read through them um
but even if you haven't kept up with a reading you can always join and and guilt that looks good to me lgtm as they used
to say lgtm looks good to me oh way back in the early 2000s that's what we did with Google and now it's become a very
pretty much everybody does that but I think that's the worst I don't know I don't want to get into P request reviews um
all right so uh shall we expand to do we think we can take a step to just now do the entire song I think so um or we
could do the entire song other than oh but we have to skip columns we have to skip columns yeah so that's not too hard
from what um we just ignore them yeah I guess we we just we know what they are up front uh here yeah so do we think we
can make that jump to the whole kitten Kaboodle to the whole song right so then what we would do is get rid of the
extracting uhuh and then make this a new song right okay sure I'm up for it if you are let's do it if we goof then we
can always revert and and take small steps rting what a crazy idea loss aversion is a thing we can Avo we can we can
that's another thing C is are great for is uh getting used to throwing away code I think it was mentioned before is like
you know do the Kata feel good about it and then delete it and try again and that will get uh because one of the things
that that is you're fighting against your your cognitive bias of loss aversion some cost fallacy uh is sometimes it's
easier to just delete the code and do it again I imagine we would start with just one is that right yeah I was think as
you were as you were typing that I was like um the theme seems like a bigger step like a step on its own uh so let's
yeah I think let's grab the first one and then we can should we make it list yeah it still be list of it still has to be
a list of but we can just make it the yeah so should fail should fail because it's empty for everything but the artist
yep be curious to see what it looks like oh interesting uh can you scroll up and error yeah ah there we go that's the
problem yeah scrolling problem so yep so as expected everything was empty except for the artist but we got all the other
stuff um all right pass one so colum I'm actually not digging that this is not self-explanatory so let's see uh Artist
is well we just say it's two what is the parameters Again release title yes yeah I'm wondering if we W to update our
test our test data to actually include those because it would be very easy to flip the ones that don't have any data and
we wouldn't know it from from this test right so mean put in some bogus values here yeah and you'd have to put that into
the appropriate place in the PSV right actually I want to go back and look at tsv uh so it's you know what just gonna
put this here for a second title just gonna us the brief I'll actually write yeah just write the what it is yeah like
type and then we're ignoring notes right oh interesting yeah ah so I can see a failure coming already um that's fine
good that's the way this is supposed to work um and how many Tabs are there there's one so we'll just say notes yep
interesting how many Tabs are here two we're not looking at distributor so put it uh put in theme four there because
that's that's that oh right yeah yeah good good call that's it that covers it yeah bdsl we're absolutely going to do
some refactoring um sooner or later for for those yep 100 yeah definitely yeah I might have been muttering it under my
breath I can't remember if I said it out loud or just in my head but when you're pairing onbling yeah you think out loud
as much as you can you did mutter something and I'm like yeah we'll get to that I didn't it's true it is that skill
though it's an interesting skill to start acquiring when you're pairing and mobbing it's thinking out loud rather than
just to yourself yeah I think that's actually something that's really really hard to adjust when you're um when you're
pairing I think it's more obvious when you're ensembling I think sometimes it can it can sometimes be um so uh we
probably want to update our yeah am we ignore that right we're just going to look at one for now thank you and ignoring
that yep okay so this will certainly fail yeah because the columns are wrong and right yeah actually it's pretty close
the only thing we're missing is the theme everything else is right so um right because I took a good stab at it here
yeah because the one we want to ignore actually is the one in between the the release type and the theme so right so
let's make it make it pass so here we're ret turning an empty list but instead we want can we just um now which column
is that zero one two five so it should Pass unless there's here uh all all all attributes plus First theme right yeah
that's that's uh something I don't know when or if Java will ever get sort of named in default parameters is um lots of
discussion around that uh it's not the highest priority at this point but maybe someday we'll see something like that in
the time that's where a builder might be um so skipping the columns was easy because we are very much tied to the exact
order so if that changed we would not know about that but I don't know that that's a requirement at least not yet not
yet I mean we could ultimately tie it to a header name exactly but for now I think we can just we can just hard code the
skipping of it as it were right uh so themes for get the Syntax for this just okay now here the same thing well actually
we right so um I'm actually wondering uh about that um so you punched in in your data theme four actually I actually uh
I don't know how much I want to put into this test so there is the let's put in theme four let's make it Complete
because I think we'll need a separate test for what if you would only have one theme right it shouldn't return the theme
and then three empty strings so I think that'll be a separate test right right that makes sense yeah so now this should
fail this will certainly y yeah definitely the simplest thing will work but I see where you're going with the uh once we
start having empty strings what's going on yeah run it let's run it we expect this to yeah it's funny it's like for this
one so I generally don't like um I actually don't like put and this is another sort of guideline that folks have like
you know don't have magic numbers and literals in your code like sure you can do that that's totally fine um you just
have to be careful about which ones so here I would agree that 0 one two 3 five like there's there's nothing in that
code that tells you anything about it um where where I find it not useful to replace magic quote magic numbers uh is
when you're doing a comparison and it's inside of a method uh that's very clear what that what that means but here is is
I would agree that that constants probably are are useful um do we want to uh since our tests are passing do we want to
do that refactoring yeah I was wondering do we want to um just make symbolics for the for the uh literals or is there
value in just having named instead of other um what we call it artist column for example so named variables rather than
magic numbers yeah I don't have I don't have a a strong preference yeah I don't either I just throwing it out uh in fact
I probably lean more towards a local variable with the name than than just pulling out zero as as some some magic number
right so something like this what Oh wrong one it control I always get that wrong I always get Al in that so here would
be um do you want to include artist in the name or just call it artist I think we're just say Artist Artist yeah that
yeah yeah so to me bdsl and this this goes back to sort of the the dry aspect a little bit um this idea of of use more
than once to me I don't care about usage so much as meaning somebody looking at this would they understand what the code
there on line 14 does and what all the parameters mean if not then I want to attach meaning to them so one way of
attaching meaning is by doing what we're doing which is extract them to to variables um because again we don't have
named parameters so this so we don't have that information and I I personally like uh uh so sometimes um I think even by
default intellig has uh the parameter names turned on so they'll show up as and I find that really distracting um I'd
rather and especially since you don't see that if you're using some other way of looking at the code I want the code as
if you know you were seeing it on on GitHub I want that to be as clear as possible so for me it's less about duplication
and more about uh meaning yeah yeah yeah uh Hey Clayton so Clayton says is it necessary to check the length of the
columns and use a TR catch block to um well we wouldn't use a TR catch uh but there are the non-happy scenarios such as
what if the column doesn't have all these things uh doesn't isn't is not the expected length in terms of number of
columns um we will certainly have to to test that um and again this is where when we're doing test driven development
which is what we're doing we're doing test driven development um you don't always know the tests up front that you're
going to write you may have an idea and so maybe you jot them down but you also look at right just like when we code I
mean there I feels like sometimes people even aren't even aware of how they code anymore because they've gotten fluent
in it but when you're writing code you think about the different scenarios and you write if blocks and and branches and
things like that tdd is the same way it's like oh I need to make sure that we handle there aren't always four themes so
you use that information to then write another test so instead of just going ahead and writing the code right away you
write a test for that to right I'm G to rerun just even though that work cool yeah I think I think uh we'll not quite
sure how we'll phrase this um but we'll we'll probably get to something where um we'll probably extract the theme stuff
to to its own method uh to clean up this this method but for now I think we just need to know that the next test we're
going to write is what if right I would just say with um only one theme so uh what does it mean what what do we expect
to see and observe if there's only one yeah oh zero themes do we have a are can you have zero themes or must you always
have a theme you have to have a theme okay I mean that would so that would probably be a a a good test to write a good
test for um when we get sort of our right um yeah interesting um back to naming this par song with only theme as only
one theme I I think that's yeah oh actually hey there's a dead comment oh yeah I delete that and the other one can go
away soon that's just would them two te three yeah that is the other way to do it astd um I kind of prefer this way
because it makes the line that actually creates the song A Little Less bulky in verbose but that is definitely an
alternative yeah for sure and that may come into play if it turns out we need to we have some code coming up soon where
yeah this is not clear yeah but setup can actually use the same there probably just copy the whole rest go right do we
want to be a little bit more uh evident in our data and basically since we're only caring about the theme replace the
rest of the text with just irrelevant oh so but mean up here relevant as well yeah so basically the the input and the
output so just say you know relevant artist a relevant whatever wondering no is there a uh you're want replace both at
the same time is that what you want to do yeah yeah so what you I don't want I don't want to place these up here what
you that Alt J ah and as you do it you it's added it's now you're now you're in multi multi carat mode right so irr
irrelevant arst if you don't like care that's fine then you can hit escape to again so I'm gonna try no no you got you
gotta select it both oh yeah you're right alj just selected the first one first one but not all of them y gotta they're
additive exactly got it um we get okay I'm doing both to see which I like better H don't care release title release
title actually so if I do that can I do now it replaces it uh no what you can do is uh sweet right and all J is a band
really okay funny oh yeah they are I forgot about that b there's another band right now that's charting that's C slash
oh I forget the rest of the band name but it's it's C something that's funny well I hope it's yeah NOP and one actually
uh backslash would be uh if we got that in the text it's already stored as a backslash it it's only when it appears in
code that it's an that it acts as an escape character so we'd be fine I found user that's great it was on this best of
test that's not a very not not a googleable uh searchable uh B name that's unfortunate um did you try sorry yeah I tried
it didn't with the word band it didn't find it yeah I said I said band named so um how do you feel about irrelevant
versus don't care I kind of like don't care also the cognitive um friction of having to remember how to spell irrelevant
yes yes that's why I I mentioned it yeah yeah okay so let's see can I no just do twice oops got it all right now we
should still be failing yes because we will have some empty themes that we don't actually not still failing that's our
first time running that test oh all right well then da on me still fails for yep all right uh so how do we want to fix
exract the list of on mine 20 on the bottom and it's yeah I'm just wondering if we could extract it into something that
will then start having some logic yeah I think extracting is a good first step so let's do that now the bummer isct to a
variable we did all the naming of the well we could still extract and pass it in let's extract it to a variable you don'
t have to select it oh yeah yeah we can just call it themes yeah that one that expression oh right that one so right now
it's not sure which you extracting why yeah took me a second themes did it just tack on one to themes one did it yes it
it it wrote theme 11 because it took the first variable that it found and said I'm going to add a one to it all right um
so we extract that into a method and then yeah I was thinking about that we could write some more code here but I it'd
probably be easier to to visualize it to visualize if it's in its own method so let's do that uh parse themes terrible
get to get out of it's really it's really annoying because like it's it's not even a like I know the intelligy does that
by default but it's like it's not even a g it's it's so um yeah so now we now we now uh it made it static for some
reason can we not do that interesting uh sometimes when you extract method this it checks the static oh you can just
delete it yeah okay I was debating whether to make it public at the same time yeah and then we could test spr test
directly against that if we wanted to or leave it private and just test indirectly uh I think probably leave it private
we can we'll be test we're yeah okay so we should have the same failure nothing right everything we did was automated
refractor inss so failure uh bdsl mentions arrays copy of range no we we don't want to do that um that just copies it
into another array we actually want to figure out if uh if if there are any empty yeah if they're empty um I mean we we
could do this the very clunky way uh can we do it you're thinking yeah oh what were you thinking I was thinking clunky
at first and then refactored it better yeah so the question is what's the what's the clunky way um it just seems like a
lot of if statements which sucks yes that was what that was the clunky way I was thinking uh I think we can do a little
bit better than that that um so one of the things that we can look at we can see duplication that the only thing that is
changing from those first four lines of the method is the index so let's basically let's do a refractor so let's let's
disable our currently failing test and we'll go ahead and do a prepare refractor no no which one no no no the test the
current failing test yeah sorry yeah so what we're doing now folks is we're doing a prepare refactoring what prepare
refactoring is is to make the change easier um to make the the code that we know we're going to need to write uh it's
going to be better if this is in the form of of a loop um but we want to make sure we don't break the code while we
convert it to a loop so we're basically taking a step back getting back to passing so now we can refractor so if I
wanted to switch hats I would I would put on my my refractor hat I'm not going to do that um and so now we can do this
safely uh to make sure that we we basically don't break anything so let's now that we're in safe refactoring mode let's
let's convert um those lines into yeah unless there's a refactoring way automated refracting way to do it I doubt it
intellig is that smart I mean maybe if we were using co-pilot it might have a way to do that but we're gonna have to I'm
not saying anything we're gonna have to we're have to type that code um we could use streams but that feels really much
more Awkward because we'd have have to first convert the array to a stream but we'd have to do that stream at a starting
at a certain point it's yeah what do you think going this approach um kind of ugly yeah we're all about ugly uh I yeah
uh probably less than or equal well let's leave it and and if it if if that doesn't work we have our test to save us
true um so let's uh let's create an empty list first so that we'll have themes so you just want to do a declaration of
themes and then just do list then you can delete line 32 so we can compile and what I what I usually uh in this case it
doesn't matter let's uh because it's it's um because we're not returning L of song so your 23 is actually wrong ah list
of string yeah yeah that's I know something funky fish uh so let's um let's now add the themes to the yep gone and it'll
fail oh uh well it should pass this was this was a refactoring oh right um so we're not using it any we're expecting it
to to pass and this is why we're doing it during the refractor stage is um we may not have noticed that that the the for
Loop is wrong it and so this is why we do this in the safe space of refactoring because if we goof up on our refactoring
because this was a manual refactoring we will know about it so let's go fix that uh so I prefer less than or equal to
eight because great yeah no I'm with you on that I was yeah my brain was going that's ugly but the other part of my
brain didn't go what about equals to I'm also curious what intellig is suggesting to replace that for loop with yeah oh
we a pass now we can ask oh that's even oh no H I don't think that's any better it's kind of cute but I don't know I
reason you know it's one of those like for Loops are are much more familiar and so therefore unless this were um oh
that's interesting so that was something else I was thinking and that was uh perhaps um closer to what sort of bdsl was
mentioning with the arrays copy of we that we don't even have to do a themes list the only issue is the is the five
comma 9 um but the constants don't matter themes yeah so can we can we look let's do that this one yeah just click it
yeah um inline themes 25 really okay yeah no you delet too much 24 and 25 24 and 25 I you catch it do the other round
let me ah got it and then uh drop the drop 2 drop meaning delete 25 oh delete 25 okay uh and then delete the themes. add
return and you can drop those extra parentheses yeah I kind of like that so it's much more precise um it's pretty clear
it's giving a subl list and I don't really care about the numbers so much because the name of the method is pretty clear
what what we're doing um if we felt strongly about the five and the nine we could we could make some constants uh but I
kind I kind of like that because it really is a um oh well actually that's great if this is the want the next step we're
going to remember this was a prepare factoring in order to make the next change easier so we've now made the next change
harder or we've made it no easier than what it was before so let's let's undo all that and this is why uh it's important
to remember what mode we're in that we're in prepare which means we're trying to make the next step easier this will
make it easier to detect and bail if we hit an empty theme right the Su list doesn't help us um and in fact the streams
doesn't help us either so this is actually the ideal prepare uh because it gets us where we pretty much just have to
write one line one or two lines of code so all right um let's just make passes all right great uh let's do a commit
saying we did a prepare all right now let's reenable what we for so this should still fail in the same does and so now
we pass I want to say not not empty because columns is a string yeah you can say uh it would be outside the the brace oh
yeah yeah bad curer movement is oh they don't have oh we gotta do um well we could do it just to get it to it weird was
there something I did um I didn't see what you did so I'm not sure what what happened oh okay it wasn't giving me the
matching braces so I had it this is the bang I was saying I'm not of I'm not a fan either but I also trying not to go
too far out of my way to get rid of it right right so now it should it should pass yeah so this is one way to do it um
which uh which is actually technically not the behavior that we want because we said is we said or maybe we didn't say
but I was thinking you you'd never have a theme and then a blank and then another theme right they'd always be either
theme and then some blanks or theme theme and then two blanks or theme theme theme and then then a fourth blank so it's
almost sorry keep going yeah so if that's the case we can bail out of the loop as soon as we hit an empty string ah so
that's one way of of both getting should let me do it a bit more true to what we're saying invert yeah and so instead of
continue we can just say break yeah or return themes you prefer I don't like a return embedded all the way in there yeah
that's just me I know some people do early returns but I don't I like early returns now this only solves part of what
you said right because wouldn't we this no because you said the first the first them is never going to be blank so it'll
always add oh it'll always add it right and then we'd be able to do some validation later if that list is empty then we
know something's wrong something's wrong yeah yeah um let's see if this this gets pass yep it's funny so twitch Auto mod
didn't Bang Yeah so it turned out the the continue is is is equivalent I if it were just to get rid of the the the bang
then I would say that that's not worth it um but here we actually want to break out uh and so it turns out that that
this is this is what this is not only what we want but gets rid gets rid of the mod so how we doing mic so let's where
yeah luckily we don't have the the cold weather that uh here in the Bay experiencing it's actually we're almost at at
time anyway uh but let's see if we can get him back to to say goodbye so um where is it uh so dud have been sort of
jokingly asked about uh post paay um there obviously is the the posts make your you know get to Green right that is the
the typical refactoring that people think of in the tdd process um and so even though if you look at like sort of the
the standard tdd thing which is you know red green refractor um you definitely uh don't have to sort of so if you end
with a refactor you're factoring what you've done and then you can also look at it as this is the first thing I do in
order to get to the to the next muted yeah I didn't want to cough into thanks I'll give you a quick quick up quick
update bdsl this is um an app uh that Mike um wanted to create and so instead of using his spreadsheet that we've seen
to search for songs that have a certain theme uh we want to have an that all right um so when you when you froze from
from our point of view uh we were just looking at um so all the tests pass is that true yes Che and do we feel we need
to uh write another test for two songs or do we feel like um we've covered it sufficiently God feeling as we covered it
but let me think about it a little bit more because we've got a test that that has all four themes we have a test that
catches just one theme I feel like we've we can also inspect the code and say this is General enough for for uh for what
we need I think I think we we can commit and and call call it done at least for parsing a single line right so I think
the thing we added was we can now handle various variant uh ship it yep should we check back with our with our jira and
see if see where we're at sounds good since we're pretty much good timing we we got it got it completed let's see jira
um my jir right so I think we haven't handled bulkload yet but we have handled what would probably be considered a a a
subtask of the bulkload and a subtask of yeah point in our tests we don't actually have a test so so as mentions we
should probably document the assumption that there are no gaps in theme columns I would say that's a missing test so I
like to document things if I can write a test that basically documents it um so I don't know if you have if you have
time to to to write one more test because sure I could actually um I could go for a bit more I've got energy and okay I
don't have let's let's write a test that documents this let's um basically create uh a string where it has a theme then
a blank and then another theme and that we don't see that other theme sorry um so that would document that we bail out
as blank and so we can say um something like you know stop parsing themes when we hit a blank theme yeah I'm G just grab
the whole thing yeah uh so BDS L's question I think I don't know if you if you heard us earlier but basically we're
talking about exactly that it's like uh especially for tab delimited like there's it's it was literally one line of code
to do tab tab delimited the comma SE the the comma delimited was a little bit more work and that's why we initially
pulled a parser off the shelf because uh if you have embedded commas in inside of the cell um but even there we were
considering if we were going to move forward with that we'd actually just copy and paste that or just use you know chat
GPT generated code but literally like it's it's dot split so uh so it's like there's there's no there there's no reason
to have a library for that if there was something like you know we were pulling in an Excel spreadsheet which requires
deep understanding of the file format that we'd probably pull in a yeah so um if we you know we basically been doing
mostly the happy case scenarios here is not necessarily a sad case but more this is the be the the behavior that if you
have a blank column we're going to stop scanning your themes um and so documenting that as a test and then we will have
if you basically have um I don't know maybe there's a there's something wrong with the data I'm not sure what we might
encounter in terms of a Mal form uh column um again with tab with tab delimited it actually gets a little bit easier
because uh you don't have to worry about embedded embedded stuff so yeah I don't I don't know what the what the negative
cases are we'll we'll yeah y I believe the fourth column let's see that's the First Column second third fourth four so I
put it in the fourth okay assuming that's only one tab here yep I'd probably use the word ignored um skipped IGN Noble
no ignored yes an IGN an ignal theme this would still have the same assert as the previous test yes yes and given the
way the codee's yeah it does sweet hey we did some self-documenting code so here's a case where 99 times out of 100 I
want to see a test fail before I see it pass um here I don't know uh I don't feel like I I need that um but what's nice
is now uh we have documented this the test name basically says we stop parsing themes maybe want say stop adding
whatever but this basically points out that um we we won't have multiple themes if if you've got a if you got a blank uh
and this is my preference if I can get around documenting something with some kind of comment by instead writing an
additional test that's going to be my my desire uh because then you you've got you know this the typical benefits of an
actual test that's actual code uh where if we do unintentionally change this Behavior like if we actually let's do this
let's comment out uh 26 through 28 um on the bottom actually could just 27 and let's run our test we expect this test to
fail and probably maybe the other ones that has a bunch of blanks but both both should fail so we've both seen we've
seen both fail um this one should fail because it has the ignored theme in it um so this this is how I you know so
sometimes I'll change a test to make it fail and sometimes I'll I'll sort of manually mutate the code uh to to make it
fail and so this proves that that it's doing what what we expect it to doing and sometimes it takes a little bit of of
thought um how to express something that is some kind of constraint or uh check or something like that um into into a
test uh but I think this was this was actually a really good one and what do you think um your normal usage pattern for
Java jocks is mostly don't use unless something like being customers I I so it depends on who's who's the consumer of it
um if I'm writing a library that's a totally different situation uh because I'm documenting how to use the library I'll
also want tests of course um but there I'm looking at it it's like somebody's calling this method I want to have good
docks right there because they're going to hit you know F1 or whatever to to bring up the the Java doc um for other
places I would only be documenting what I typically document with comments which is the why not the the water the how
yeah because it seems like the Java do thing can or not seems like I've seen it where it's overused yeah where there's
this huge amount of effort writing Java docs which a very quickly become out of dat and B don't provide a value ad yeah
and sometimes Dollar on nothing yeah just and just having a lot of stuff in there especially because it can go out of
date um but also a lot of times you you you just don't need it uh so so yeah and hey tokes we're actually gonna be
ending you what's your how far can you go as far as extend totally up up to you I could probably do another 45 I could
even take it to uh one our time you want let's go to let's go to 12:30 sounds good and then because I think that'll
probably be good yeah yeah yeah uh does Java do populate hover text an idea um Yes except I have that I have that turned
off because an noise I I really heavily dislike Mouse hovering um and I think it's actually uh a problem in Ensemble
pairing situations is is um since you don't have direct control over where the mouse cursor is as the person who's
driving uh sorry as the person who's navigating um it can actually be really annoying it's like can you move the mouse
no now can you move the mouse again uh because it starts covering up stuff that you might want to see um so I much
prefer basically hitting a key to bring up the Java do and the key to hit F1 is control Q for some reason on Windows
Linux I don't know why why it's not F1 is like the the worldwide Global key for help it has been that way since function
keys came about at least as far as I know uh and and why it's control Q the only thing I can guess is that Windows
perhaps is intercepting F1 for something else I don't know no F1 I did it gave me help oh that's interesting so is it uh
wait did it pop that up yeah ah so that's help on that's not what it does on on the Mac when on the Mac what it does is
it's a control if you hit control Q that's what Mac which basically brings up if there was Java DOC for this it would
bring well um so I guess F1 is is truly the global key for help but it brings up the help for the application and not
the help for for the thing you're on I guess that's acceptable so control Q is the thing that would bring up Java do for
for a method if there were any so if you click on like uh where is it um in our bottom and you hit control Q that's the
that while you talking I was playing around with changing the name of this test stop adding themes when first when how
about when hit first blank theme so drop the at and reverse the yeah so to a certain extent there's a little bit of
documentation in the sense that it's not something that is is going to break if we change Behavior which is the name of
the test method so that's kind of the only place where you could sort of say well that's really just text right nobody
nobody else cares about what that text says other than humans um but we do have the tests that uh the content of the
test that's that's testing that and that'd be true for all tests because it's human readable name exactly and if you
change the test to no longer behave like that human readable name well you let's that's thing about tests right is you
got keep checking make is that name still good yeah yeah uh let's do a commit since we added a test and it does pass
right because we broke it and we back pretty sure I ran it yep there is also a setting uh that you can select in your
commit dialogue to basically say run tests so all the way at the bottom right of that dialogue there's a little gear and
if you click that you can click on uh run tests and you can choose which configuration and we would choose the io free
you might choose the all but that might be annoying if you're doing frequent commits um right but we could do that and
just see what it looks like um I have a feeling this is going to fail so let's but let's see what happens we haven't run
all tests in a while yeah we haven't run all tests in a while yeah um just the same commit textes last time document
stop you know stop parsing it oh that's interesting it does the commit first and then runs all the runs the test that's
weird that's not what I would have expected that kind of like what the heck how is that helpful I I want to run before
com you actually commit yeah yeah you want to be more like a CI kind of thing that's a bummer interesting I I because
clearly I never used this feature before um and now I'm like that's not really useful it's like oh great I just
committed something that's broken I wonder if there's some settings gonna it's really that's oh it's not a failed test
it's actually a it's just a disabled test yes but it ran it did run it after right yes like all right I'll double check
on that because it seemed like it um but maybe maybe it's just the status was actually incorrect we'll have to play
around with that because everything else in that dialogue is before commit so i' I'd be kind of surprised if it actually
uh if it actually but it let commit true even though it was quote well it's unclear when it actually finished the commit
h so um but anyway uh so let's leave it um yeah let's leave it okay so where are we in let's check our jira where are we
in done multi line yeah so I think uh something mul line which one which one do we want because there's the skip the
headers and then there's the actually process multiple songs so let's write those both those are yeah is there anything
else I think that's it I think we have multiple songs and heter rs then the bulk load is uh is all we need uh we will
need the actual UI aspect of it which is the time Leaf template and the controller um this part down here yeah I think
that's under under brainstorm this a value I think I think we can get rid of all of that because we're no longer doing
CSV anyway and therefore all the double quote stuff doesn't matter yeah as hard as it is to stuff I do one one thing
it's in the commit history that's right yeah so that that's that's a u what what might be some um so that's the kind of
comment that uh you'd want somewhere because that would not be at all obvious why right why we did that video I think we
can still delete this yes it's old but not particularly yeah what do you think song first sure um it feels more
satisfying but that's just me um sounds good to me okay I don't know write a test is there anything else we can do no
absolutely okay um what have we called the other chest so far I guess parse multiple uh oh is there another word you'd
prefer that would be more business friendly yeah I'm just wondering um this gets back to that question of does the
business care about CSV versus tsv is like yes they do do they understand what the word parse is or would load multiple
songs be sufficient but it's not really loading him this is yeah I'm sticking with parse unless you come can't think of
a better a better term and then you were going to say something I think I interrupted you uh so one thing I was gonna
say is can we go to the disabled test oh yeah yeah in Test um does this pass what does it do it's been so long let's see
I don't know but we should check yeah I'm guessing it's not because it's got all that well first of all it's it's wrong
the data is data so okay be that then you can do uh there we go no you can uh I would not do that I would do a backlash
T ah make it more self-documenting yeah and column oh there's that right there's an extra column in in the artist s try
to release type we're skipping which is column three that's between title and themes well just go to the other test what
do we have there we have uh notes is the one we no we also skip over and then we basically have the distributor column
but we we skip over that right we're skipping over release type we're also skipping over this but this one we're not
skipping over release type it's in the song oh right right right right yeah we're skipping over notes so the only thing
we're skipping over is notes and then we just stop at the end of themes so anything after that we ignore should we call
this skip notes for now sure that help uh yeah I don't think it'll here oh who who who that's the other test that's the
other test I was goingon to say we we disabled it so I expect that right yeah yeah and skipped there uh so T tkes asks
about um Collections and so uh he tookes notes that we're declaring variables as list even though uh we're using uh
array list underneath so that's the difference between the interface list and the rete implementation array list uh and
in general what you want to do and this is general not just collections but in general you want to use the most General
interface or class type that you can when you're declaring variables um because uh unless you need something specific
from that more concrete type like you're doing something very specific to an array list you want to treat it as its most
generic type so you actually don't rely on some of those details so in general and this is idiomatic Java and other this
is the Java that that most people will write is you use the interface type for for collection so you use map not hashmap
is your declaration type so the key thing to understand is there's two things right on that line that that uh at the
bottom there that that Mike is highlighting there's two parts to that there is the first part list of string themes that
is the Declaration what is the type of the variable themes then there is the initialization or instantiation of what are
we storing in that variable and that's the new array list so those are two parts declaration right the first part is the
Declaration what is the type of the variable which defines how I'll be able to use it later and then there's what do we
actually starting off to be which is an empty array list uh and so the Declaration you always want to be as general as
possible um and that's just good idiomatic Java uh to to follow so um it's a really good question because I see a lot of
folks who are just starting to learn Java will declare this as an array list and there's no need for that um you can do
it it's fine it's just the idiomatic uh and preferred way to do it is to treat type all right um so we added the skip
notes um uh let's go back to our failing test yeah because I think there's some so we want to add in the skip notes here
as well into our data right so skip notes was theme I don't know why I copied imp that Sil you know how you do stuff and
you're like why did I do that why did I do that all the time if we do that is that going to make it pass uh well it
won't break the same way it did before where we didn't have enough columns so like it'll still fail I don't okay all
right uh index six out of bounds for length six are we missing a column in our see well technically we're expecting it
to go up to eight nine columns oo um so this test was written before so I know it's happening so there is an assumption
that if there are that there will always be the extra theme columns as blank right but here we didn't we only had the
first theme column and nothing after input and I think this is not valid input uh we might want to protect against this
but this is not typical valid input right this would be if if you selected the column only through theme one right but
typically you're going to select all the way to theme four so you will always have blank columns for two through two
through four at least for me you know if we get to the point where we allow other people to contribute then we might
want to give some more flexibility but again that's a yagy versus well I think we should have a and we don't necessarily
have to have to write it but I think we should know note um in our inera uh write some tests for um at least write a
test for uh only one theme column and maybe more generally what if columns so I should mention malform column so The
Columns themselves inside the columns aren't malformed but yes the the entire set of columns might be malformed mainly
in that you don't have enough so I don't know if I'd call that malformed but definitely not having enough columns will
currently cause our fail so make this one pass by putting in some uh so we' if we're going to have correct if we're
going to say that this is the data we pass and we want to basically have a couple of uh basically tabs does interesting
is that enough columns one two three four five nine oh wait a second well we certainly have at least six so I'm curious
why it thinks uh enough what does oh wait a second it's here what does this method do it just calls the parse that we
just wrote right I mean if we look at the ACT Trace it's it's failing on parse themes strange yeah we have more than six
columns we have more than seven columns we actually have 1 2 3 4 five 6 7 seven eight I mean uh there's certainly more
than than that um I wonder what's going on there I know um do you think split has an unusual behavior when it's an a tab
with nothing like what does it yeah so so the question yeah so I think the question is and this is what BDS man is is
what what does a blank column mean can we look at at the actual Source in Sublime whatever you had in your text like um
meaning one without with only one theme yeah so what is it this one yeah so one 2 3 4 5 6 7 eight n but those are just
consecutive tabs right right so it's not like there's a space in between the two tabs no there isn't um I wonder like so
let's write let's write a test uh or let's modify one of our existing uh tsv parser tests to use the back SLT instead of
the actual tab character ah so like anyone uh let's pick the one of the earlier ones that has all yeah so let's let's
take that one so I was going to suggest duplicate it first and then oh uh and then comment it out and then replace it
with with okay so actually this one will probably be fine because we we don't have blank columns so maybe this was the
wrong one to select uh so let's let's back off on this one cuz we actually want one that has the blanks so like the next
one is probably better yeah uh this one on 24 yeah okay future reference control D is duplicate current line oh yeah I
always forget about that one got to use my Alt J today oh look at you there we go okay so we expect the same behavior so
let's see um although this one does have the don't care contributor at the end uh let's take that off okay it looks like
it failed with the same oh this this test passed let's take out the don't care contributor and see what happens
interesting so it looks like split is bailing out if the rest of the row is is oh that so do we call the other split
method so let's call the other split method uh so click on no sor bring up the help again uh RP contrl Q right and then
click on the split highlighted in the Java doc there no inside the paragraph oh yeah that one yeah because that one will
point to the two argument split so the two argument takes a limit so if limit is positive then the pattern will be
applied at most limit minus one um yeah so if we specify the limit explicitly it will stop there it's only when it's
zero which is the default uh does it does it ignore blanks so we can call the split with um 10 yeah okay yeah that fixed
everything now let's try nine nine will probably work too because uh we're not we're never touching that last
interesting so because we're not even though we're not touching it it's GNA split oh interesting so basically it doesn't
know we're usage right it's just thing it doesn't know that we're not accessing no but look at the actual it's actually
tacking on the contributor oh whoa so it's like so it's like it stopped it basically stopped parsing at that point and
basically took the rest of the string as that last column oh which is weird interesting not what I would have expected
from from from that it's basically saying as soon as you've you've hit nine delimiters everything else the last one is
in the last column and that's why we got theme four with an embedded tab Rizzy right um yes yeah so the Java do says
exactly that which is why this is what you want in your Java do um so so but that's fine we've got tests to cover this
so we can just change it back to to 10 and and and we okay and so um this was really interesting because had input that
we wouldn't normally have but if you selected fewer columns or you didn't select the contributor column because you
thought oh I don't need that um it it would have broken uh but now I think we can revert the passes all right and then
we can go back to our song Service Test uh do we want to represent the contributor column here or do we want to just
leave it as is by putting in contributor here yeah yeah Vol ad songs using tsv this one's only triot tour and that's it
we're not we're not not using it right so that should still pass yeah and it does commit because we actually uh fix a
potential problem but also now our song Service passes good enough again all right all test pass cool so to asked about
the difference between the Primitive int and the integer wrapper uh and why collections only take wrapper classes and
the reason why is generics so if you collections are all about storing uh and being defined by the generics the things
that they can hold and generics can currently not be applied to Primitives so you can't say list of just int um at some
someday that will work maybe that's what value uh the whole idea of value classes that that's being worked on um but uh
Primitives at the beginning of Java's existence were always separate from objects because of performance issues remember
this was the early 90s so uh performance was was an issue for not treating object and so um there is a top type for
classes it's called object but Primitives are not objects Primitives have always been separate things and so int is not
an object float is not an object unless you're talking about the uppercase float which is an object and so in order to
store and support storing integers and floats in collections they had to create wrappers for them yeah so there are
types the Primitive types are not class types and therefore do not have object as its parent this will hopefully change
um I am looking forward to it I expect that maybe in the next couple years we we will we will have something like that
and they probably did that originally I mean originally you'd think well make it all object oriented out of the gate but
I imagine the reason they did it early on was the performance reason you were talking about so performance and memory so
an object version of of an INT takes up more space than the Primitive int because the primitive ENT is what four bytes
right four bytes Longs are eight so four bytes that's it four bytes an object though has other information associated
with it the object header uh and so we'll at least have a few extra bytes I think might even be four more um and so that
means you basically double the size of usage of your primitive types if you got lots of those and remember 1993 we did
not have gigabytes of RAM 1993 when Java was was being developed uh so both performance and and memory which is kind of
performance were the main issues why they decided explicitly uh unlike languages that came in before like small talk
they decided explicitly no we're not going to do that we're GNA have Primitives be their own thing completely separate
um if they you know if you could go back in time and change that then maybe Java wouldn't have been as popular who knows
uh but it is what it is and we and Java needs to be backwards are so Primitives are their own thing they do they are not
objects they are not stored as object they are not referenced as objects um and so therefore the only way to store them
in collection classes that expect objects object all right um process multip song so uh do we want to change our outer
test and start there sure I almost wonder if that's even worth it uh since it's but um it does store it in the
repository so we should we could start here um or we could start directly on the let's actually I don't know I think we
could just do an inner test seems like it to me which is what we were starting to do when we've got interrupted so I
think you already have a blank test yeah there we go um so let's do it let's let's uh why don't you take actual copy and
paste from your Sublime editor and grab something without this is an interesting one with quotes in it sure I don't know
if we want to do that today right now seems like a corner case we can deal with later um all right let's grab those
actually let me grab I'm going to grab these three all right no that's got two so now for this one we will want
multi-line right uh yeah yep and then just delete the blank line yeah like I was trying to think why is that blank line
coming in because you copied a new line at the end and then put a semicolon at the end of that one and we got our songs
uh the rest of it is yeah it's pretty much the same that'll be yeah so oh we would do this is an awfully long line so
it' be something like yeah that I'm not sure I got have the right par um what I would do is uh stick a comma uh do a
sorry go ahead and and push the the semi the close print and semicolon on new line and then duplicate that line using a
control D and now put a Comm at the end of Baseline and then we just got to make it match so to ask why the exception
for string uh I'm not sure what you mean are you talking about the exception at the end else and yeah so arrays are this
weird thing um arrays can hold primitive types um collection classes cannot they must hold objects um but arrays because
they're a very different kind of thing uh can can basically hold anything they Primitives yeah so strings are also weird
because they are objects um but they're built-in objects unlike some of the other ones that actually require
implementation string is automatically imported into your code uh unlike unlike other things we have to expli imported
so strings strings are objects they're very special they get a lot of attention but they are objects and that's
different from some other languages like um like C where strings are are sort of in a sense Primitives but C is a very
greatly we got a I gotta use control W more easier think I got it I don't know if you were probably weren't tracking
because you were talk um so you've got some don't care stuff that isn't present in your input do you w to those into the
input or do you want to leave them blank let's see what uh yeah blank right because it'll just be I think we can do
blank yeah right that should fail that should certainly fail uh the question is how is it going to fail um I think we're
just processing the first one so we should get the first one and just be missing the second one that's what I was see oh
you're running the song Service Test we want to run ah so yep we got the first one and missing right I think that's uh a
great place to stop a good breadcrumb yes and we got the breadcrumb here as though oh yeah yeah my partn speaks German
so I have a few that come through now and songs and that's it cool all all right another another good pairing session
making progress we got uh the next steps should be should be easier so we'll get the multiple songs and then we can
start maybe hooking it up to the UI sounds great uh so I'm not sure if we we don't have a specific date and time plan
for the next episode so you'll want to as always uh follow Andor subscribe that will help you um but ideally join the
Discord uh join the Discord go into the rolls Channel click on COD stream alert and you can be notified uh usually I try
to give it as much advanced notice as I have for either pairing streams or uh solo streams so that's your bet bet uh and
reminder book club if you're interested come join the Discord and find out and vote on on the book yeah and that's it so
thanks folks thanks for hanging out on a on a Sunday and uh we'll see you next time by
