# ＂Song Themes＂ Episode 35： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=jiWU5YuP74c

---

## Transcript

all right hello folks welcome to another pairing stream uh here with Mike Rizzy how's it going Mike doing well doing
astred now I'm doing pretty good mostly focusing on vegetable garden getting everything planted ah yes just enough time
to get all the dirt stream yeah and I've been uh doing a lot of streaming per uh working on the um tdd game and that's
been going well but today we're uh we're getting back to song themes so let's do it want me to oh you already got me
queued up there you are I was just looking at jira yes my partner was asking me about jir they do not work in the
software industry yeah um yeah I saw a a social media post uh asking sort of like what what software do you pay for but
hate to use every day and like jro was the popular one they own Trello now right yeah they've owned Trello for a while
did they ruin it or is it still free and halfway decent I haven't used it in um it's still free um and useful I I use it
for for for Stuff um yeah I have in the past not as much as I used to because it's it's the where did where where am I
keeping this information up to date I've switched either to jira um or uh really or GitHub Jonas oh you're out playing
board games was fun is what's important yeah we all need more fun and board games is is a great way to it's a great way
to have fun yeah so where did we leave off well um I just ran all the tests and they passed okay well I did IO free I
didn't do all um I was looking at this our little and I'm wondering if we should hold off on deploy to production until
after 21 for me I feel like the autocomplete for the themes and getting rid of duplicate entries on import possibly even
including dealing with this because then I can import once and be done with it um but then again yeah I don't know I go
back and forth so open to your perspective uh it's up up to you depends what what if you want to get it in production
and see it and and Set set set stuff up or if you want to I know we were hoping to get to this last time yeah so I think
we were kind of getting ready for that there was also this style right I know yeah I believe we wanted to start with
that because that shouldn't take too long so then we can go go to the autocomplete and we'll and then we'll put this
defer that for a little bit a little bit maybe for now we put it right here yeah and then possibly move move these two
up or plan so uh let's figure out the do you want to run all the tests just to be sure that we're in good shape and then
we were of a similar mind I was like we ignored two probably should take a peek of what those two do all right um that's
because this is the startup test okay yeah and then this one that's within yeah startup test this yeah I should actually
put myself a reminder to do that because otherwise enable Okay I'll make sure to do that today but wait a second wait a
second if it's disabled how come it doesn't have a disabled attribute oh the whole class is disabled the whole the whole
thing yep okay took me a second to and that's funny had the exact same error message or you know not error message but
informational clue cool uh so let's uh since all our tests are passing which is great um let's take a look at our uh
success import template and see what we want it so right now it's just sort of it's a raw table yeah yeah it's um let's
see I I'm trying to see if we can do this without running it or we should run the app and see what it looks like to
remind us what uh you should be able to pre well actually if you preview it you'll see uh the table with one row of data
got it that doesn't really help my sense was It was kind of jagged other words each row was well there's no styling in
terms of padding there's no styling in terms of if you want uh um the thing to be the full width there's uh stuff around
uh borders and things like that so yeah um I mean I think we can pretty quickly uh depending on what um what style and
more CSS I was doing CSS yesterday and earlier this week and it was it was okay and also not fun um uh so it's defin CSS
is definitely an attention to detail and high patience kind of thing at least I found that to be the case yeah for me
it's been mostly about how do I I know what I want it to look like how do I get it to look like that and how do I get
things to be in in the place where I want them want them to be yeah um so I don't know if we talked about uh what um how
we want to do the CSS in this project we did not okay yeah so there's a bunch of options um we could use something
opinionated uh like a a bootstrap or um what's the one I found the other day when you say opinionated what is it is that
a term or using bootstrap isn't opin something people have strong opinions about oh so an opinionated framework
basically says you want a table this is what it's going to look like we have an opinion on how tables should look versus
uh something like Tailwind that's just a convenient way to do CSS um where Tailwind itself has no opinion on how tables
should look uh there are Tailwind uh components that do have an opinion and we can look at those as well um and that
since on top of um basically it's just on top of of H uh there's another CSS framework um uh that is is called matcha um
oh that also is opinionated basically is is if you add it it will basically put CSS on all the stuff and so it would you
can basically add one line to the uh to the HTML and basically see what it looks like so we can try that um bootstrap is
a little bit uh so in terms of sort of opinionated Frameworks there's there's sort of also two kinds there is let me
style standard HTML components you don't have to do anything extra if you do it like we did with a table with TRS and
THS and TDS then it will Style pilot uh ones like bootstrap might require you to add classes uh to the elements to get
things organized and looking correct um because they have grid layouts and and column and all sorts of uh all sorts of
stuff so do um does one of them have more Advantage for being able to use the the app to sort of for lack of a better
word Auto style to computer versus tablet versus Cell uh so you're talking about responsive uh and um so responsive
means it works in both and all three of those kind of rough categories of yeah so responsive means it will it will look
appropriate for each one of those platforms each one of the there is no framework that's going to do the right thing out
of the box because the right thing is context dependent like what you know if you wanted to add you know view the
imported songs um and you had imported it from you know a phone what would the right output be probably not a a wide
table right um but then okay so what do you want how often you do the well there there's that so there's there's how
important is the import being done on a on a cell phone uh but even the the search output um you instead of having a a a
list that that is a wide table you might want the list to basically be more compact but where do you break things do you
do you have two columns do you and then other stuff is sort of hidden do you have you know two columns and and stuff
Stacks which things stack how do they stack like so it's one of those you have to figure figure out what's what's
important um the different um uh the different sort of Frameworks or whatever you want to call them for CSS um some of
them might provide more help than than others but ultimately you have to do I would personally say uh and so none of
them prevent you from doing responsive um but they won't they're not they may not they're not going to do it for you uh
so picking one or the other doesn't matter in terms of the ability to do it if maybe that answers what your intent was
because it's all CSS ultimately it's out um I think I'm working again there you go no I can't hear you Dar you can't
hear me oh that's weird usually it's the around so while you're figuring that out um so these are the Tailwind samples
uh so there's of the straightforward table um where some of the columns are are bolded some are not um there's of course
links which we won't need for for our use case um but we have uh spreadout sort of takes up the full width and stuff is
aligned left in column and it basically uh still uses tables and T head and that and so the drop in CSS that I was
looking at this matcha is uh this is what's called a semantic styling Library so it basically um styles things in a
reasonable way in so we would just drop in this link I think I'm working are you working you hear me I can hear you can
you hear me okay yes awesome all right I think I need to do a factory reset on this headset I've had it for like I don't
know seven years so I'm pushing I'm lifespan so thanks for being patient yep what you guys what do you all look at maybe
uh so um here I'll add me back uh so this is um matcha and this is basically uh so tables will have collapsed borders um
um uh table rows um there'll be possibly alternating backgrounds uh and so this is this is the semantic one where
basically you just drop it in and it will apply styles to the ones that we used got it versus uh Tailwind here for this
table um we'd have to basically add a bunch of uh put some divs around the existing thing uh and then style each of the
um style the the body of the table the T body um and the table itself and some classes on each individual column and you
were saying you could do um something like matcha on top of Tailwind is that what you were saying no you pretty much
have to choose you it's you don't want to you don't want to you don't want to mix up um you can start with tailwind and
then just convert it to CSS which is what I've been doing um because uh as you can see from this code example with
Tailwind it's like you know really both all the headers are the the same you're basically uh there's basically a lot of
duplication across similarly styled things got it so like since all of these have the same you know padding give it a
name you know yeah and so that's you know this is the the sort of the the critique against Tailwind is like well I have
to basically copy and paste this stuff and Twin's response is no you don't do that you create components um that have
these Styles attach them uh and then you you don't have duplication um but we're not using a component Library uh so
what I what I've been doing is basically styling it this way figure out what looks good once I have that then I convert
it into a regular CSS file because these are just shorthand for I mean that's tail Tailwind is is is a lot of just
shorthand for uh for CSS the convenience functions are syntactic sugar in a way where sort of yeah yeah some of the CSS
language yeah I mean it hides all the CSS language so the you know PX you know py4 would turn into a uh ver is it y or
vertical or just padding colon and then a bunch of parameters um uh pl4 would would basically expand to padding Das left
colon uh one REM um um so this is sort of the CSS what do you think between the two um I think uh let's drop in matcha
and and s so let's second need some warning on that okay uh so let's uh so if you go to the file uh so inside the head
below the title so seven and a half um actually I'll just paste it in here is that actually copy to my clipboard no I
don't know why yeah all um it's not letting me paste into your tupal so I'll just throw private chat yeah or full chat
do really matter there it is interesting one negative for Tuple we just discovered is so there is a way for me to paste
uh I think we just haven't configured it properly got it so it looks like are using Tuple means I can't get to monitor
two where I have streamyard chat the mouse stops at the border here let me I thought we figured that out thought we did
too I we can disconnect if if if that's a problem what was the trick Escape no maybe if I click in my side yeah you got
to click to to regain the cursor yep that was it click on my side okay like cool shall we run it yeah let's run it kind
is it Running Y it's running hey X proof I'll uh get to your question minute did I say hi to Sue okay didn't like it but
I think I might H I'm just G get a new browser just in case is that the right endpoint for song import isn't it I don't
remember what the the thought it so we had put it we had moved it remember because we did the right the the higher level
uh to to basically secure the contributor stuff differently so it's under the SL contributor slash uh oh that's what we
did so you can tell if you um my auto complete was oh sorry you want to have me at so here it is if we go to I'm gonna
take over for a second sure um where is it tools window tool Windows spring it's over there what's doing over um uh
that's not what I want what I want is why does that not look like mine there is a gear maybe that affects the how it use
how it displays uh no that's just um the how it's laid out seeing all right well I'm not going to worry about it I'm not
seeing what I expect so that's real what's going on all right you can take over okay so view so folks we're we're using
tupal that's how I'm taking control of the screen but it is a little bit of uh getting used to yeah playing around with
columns how do you know did you get an error no I just why not why didn't you import I would have just saying you wanted
me to I I would have just done it bad it's almost like I need something title I'm looking for one it's actually well
there's a release Title One let me one nope not that one no the other one this one oh right of course you need the
headers and I got pulling from the middle um you could undo and then leave the first let you undo that box no won't let
oh it already it already you already yeah no no okay I'm gonna do a little hack here on the side okay I'll take that go
back to the top grab the header hey arrows are still working it does lead us to like you know is this kind of thing
going to happen in sort of real life or is it just an artifact of us playing around yeah the other so from a u let me
just do this first see what it looks like yeah so that deals pretty well with multiline um one of the things I was going
to say if I go back to the importer screen is that's a long title which one Asters oh let me go check I have on that
screen oh yeah classic song thinkink Floyd that's from amagama I think right the name of the album is AST um what I'm
wondering is to facilitate this would this is like I'm not saying we do it right now or even but like what if we had a
separate field that persists that is here's the header row right y all hold on to it but it kind of defeats the purpose
was to make sure the comms match up yeah yeah yeah yeah and and also this is you know not likely a thing you would you
would do you pretty much you know be just for yeah cool well we we know that this is good enough as a UI for now so yeah
actually what'll happen if I redo it I probably just get duplicates yeah it's not we're not tracking duplicates right so
cool all right well then we can check that off on our jira yeah well we should check it in first sure or check off the J
check off the J and yeah so X proof asks uh one of the standard questions about about validation which is uh is it okay
to have the same validation in the controller and the domain objects and the answer is um not only is it okay but it's
required you cannot rely on your controller to always validate everything objects um I always sort of think of of
objects as they must be paranoid don't trust anybody calling you with anything make sure that whatever they're doing is
uh not going to leave your object in a bad State Um this can lead to duplication of validation um but that's the price
we pay for providing quick response like we do in our controller so literally song themes does exactly this right we
basically check um some things on uh in in the controller and then the rest is up to um the object we don't actually
have much domain constraints other than making sure certain things aren't blank uh we had somebody we pushed into the
database yeah so um uh but I think if we can you open can you open up song on the bottom there yeah so we do have right
a check for is uh that you have to have themes and we check for blanks for uh some attributes so we are doing validation
here um but these all throw exceptions so generally the way I think about validation is um at the controller and
application Level uh we use the result class because we expect things to go wrong but at the Domain object level we
expect you to have figured out what's correct and do the right thing and if you don't then that's a bug so generally if
we got a song where the artist was blank that would mean some outer validation failed uh one more thing specific to xb's
question uh is um what sua literally just wrote which is you want and actually in the Discord we were having a
conversation about exactly this kind of thing so uh in the Discord uh we were talking um with uh some folks around what
do you call it was mostly related to Tim related stuff which is this example is what do you what do you call these
things how do you name them um so if you've got checkout date and check-in date uh those would be you know so so check
out on and check in on uh would be it's kind of nicer than than tacking on the word date um but the more important thing
is is the checkout date should be a type right because you want to make right uh or the the pair is really a type is
that check out must come after checkin so that's a a single object because its constraint is one of those must come
before the other and so you make it so that you have a type of uh you know stay duration or stay period or something
like that where it has the two dates and makes sure that you can't possibly even create that object without the
constraint being satisfied um so IGI correctly points out you want your domain to be if possible that you can't even
express something incorrectly like the checkout and check-in date uh and if it does violate it that means the validation
on the front end has failed and you better throw an exception because you don't want to have object um so we use
exceptions in the domain and we use results error messages in uh in the controller user and yes custom exceptions are
the way to go um but again uh I don't consider these validation errors I consider so for example what's what's showing
on the screen uh line nine and line 27 uh those are constraint violations not validation errors and and I and I try to
make that really clear because constraint violations throw exceptions you've violated the Integrity of this object and
that's a bug validation errors are hey this is not valid do you want to try again or do something different and that all
right so what's next um let's see um autocomplete all right so we probably want to think about what we want from this
what do you want from this feature um what I would like is actually you want me to just grab that we F we were found
several examples I could just show if I can well I want you to describe it in English rather than uh okay visually okay
visually we we'll get to the visual stuff yeah so for me in English let me second how can I describe this um I'm just
GNA blurt and it's not going to be good English or grammar or if um matches one of matches existing themes then go
selected sorry I'm CH I'm chuckling at Astro's comment oh that's if you want to rethrow it then yes that you will throw
up a little bit if you rethrow an exception yeah I mean just the thought of it makes me yeah you know a little bit yeah
um so let's see so as far as the initial thing you start typing if it matches one of the themes then it would show
actually then them then allow one of those things to be selected okay um there's more okay um allow for selected allow
for a selected thing to be removed EG changing one's mind right H is that everything that I've got uh this is a big
feature so um how how might we break this down into smaller vertical part that we can sort of break down probably the
the it's really 13 that's one right you could start by just showing all the existing actually I don't know if it's
vertical it's just a thin slice um well I think it will need to be vertic a vertical slice right because hasit because
this is gonna pull the data from the database so this is G this so this um so I want to be very clear about what this
what our thin vertical slice is it's not just show all existing themes it is uh show all existing themes and only allow
the selection of a single one which basically translates into an and so the reason why that's important is then we don't
have to figure out how do we do autocomplete and we don't have to figure out how do we do multiple select right but we'
re still doing a vertical slice in the sense that we're going all the way to the database getting all the themes
building that infrastructure to do that we don't have thatly we don't have that right um yeah no very good point and
then leave this the air code styling which is more than the styling but but a more complicated UI to later right makes
sense yeah and that's and that's why I wanted to to push on this is because there's two big unknowns which is one is the
UI part how do we do the UI how do we do autocom complete at all and then how do we autocomplete with multiple things um
and that's just a lot of work on the front end without knowing are we getting the right data or how do where do we get
the data from yeah right now we have no way of getting that so so break down the story into smaller bits yeah so sui's
suggestion I think might be the the follow on step once we have uh there's sort of two directions we could go is once
we've got the the drop down like okay a way to get a list of themes a list of unique themes um and throw those in a drop
down the next step might be now focus on the front end a bit more about autocomplete uh the other way we could go is get
the list of dropdowns and it's just static you know basically a static HTML page and then go to multiple select and then
go to autocomplete so there there are a couple of different ways we can go but the first one definitely is um list of
unique themes yeah and would we have break that down even smaller as to having a test driving getting that information
well sub continuously okay I mean of course we're gonna test drive do we need to have a separate line item here in J I
don't I don't think so I think it's it's basically we've defined the the story um and now this this thin vertical slice
story is we want um the dropdown selection to have the list of unique themes do we want those in any care I mean
ultimately alphabetical but well should not let me rephrase that at first alphabetical is fine but if we're going to be
filtering based on what you're typing well even in that case you probably want alphabetical yeah that's that's what I
was thinking even if it's a even if you're narrowing down the stch you still want it alphabetical um so that might I
mean that might be part of this story because it's such a small thing but important yeah agreed um do we want to flush
out the the next steps or just do this one I'm kind of like let's just do this one and then rather than spending too
much time planning yeah because we have a rough sketch of it here yeah no I think I think that's we don't want we don't
need well might be interesting to have a a an HTML test but I I think we can we can skip past that and it's um basically
a test against start you know start testing against the controller right so which controller is that gonna be I was just
gonna like which controllers do we have so this would be on the theme Searcher yeah I move down to the production code
panel yeah I don't know where else to put it yeah no this is this is this is where it needs to be um because somewhere
when we dis when we display the thing you're going to fill out to search which is this page um well this is the get
request that actually does the search right so want uh uh I think we have we do have well we do have a page that I was
just taking a look at so I think if we drop this down we can uh go to declaration or usages oh and so we can so it
doesn't show for so those are the oh this is what I was looking for before these are all the endpoints so we can see
that that here it's contributor song import and song import uh for post and then contributor song import success um so
the homepage controller uh that we don't care about uh so which HTML page then so it's one of the HTML um basically has
the thing that turns it into a get request which I believe is a form right we just show a text box I think it's oh no
look in the look in the project I was just going to go here but sure yeah so where does so that theme search search so
we just jump to um sorry my cursor is there it goes uh so here's what we do we go to display oh if it's it's blank got
it right uh but we'll want so I think then what we what we want is our test if if the theme search is blank then we want
model for that page right does this page have its own model or would it be at the well it wouldn't be it so the simplest
thing we could do right now is add model to uh the um well we could return a model or we could just add model as a
parameter to this method but this is this is basically the method that we would start writing the test at because this
is just below the the HTML right we've currently got some free stream search yes yeah oh there's a model there yeah oh I
guess it's the end so maybe we want to put a new line oh well I close the close the right hand window yeah close the
right hand I'll and it was this one right yeah yes okay so there it is at the end um so we've got the model and so we So
currently we're using the model to populate the result results you want to break would you do that uh yeah I would break
it there uh sorry I would break it well I'd break it before model that may or may not be very very much help uh and then
I might also break it before the string yeah sorry interrupted you you were mident well I was going to say like but we'
ve got a wider screen so let's not do that because our vertical space is at a premium so we're optimizing for for
vertical space so um so what we have is uh we add the search results here um but what we can also do is is before we go
to uh to here uh but basically before we return the template we can put stuff in the model here and then this this
search page home can display it uh display whatever list will provide of the themes as a as a dropdown so our goal then
is is put a list of themes in the model right and that will force us to stuff so we would again go back to uh theme
search nope that's not what I wanted um I thought there was multiple yeah here we go test tests y so we want to go to go
to that test file and then move up so as asks the questions about having the mappings be Global constants uh rather than
my tendency is um I just I don't bother uh I haven't I haven't found that to be a problem and intellig is usually pretty
good about keeping sync because then you gotta basically have time Leaf pull in a constant which you can do um I just
don't probably with maybe with a larger project I might I might do that or if there were lots more usages of of
individual mappings that then I might do is initialization of the search screen so what's what's the outcome we want
that's all I that's what I start with these days yeah you're right the outcome um I'm um yeah do we need to have the
word list or we just say populated with themes I'm fine with with either okay themes is without the list is a little bit
more flexible yeah I feel like list was like we're committing to using a list it will likely be a list um because
because uh so maybe list is actually important because ordering is important oh good point um and we want to say with
with or but do we you say how it's ordered uh I would so I would say cool so I don't think you're going to copy anything
from a previous thing because this is a test not a test we've really written before right um other than maybe 50 well
well um we're certainly going to need to do some preparation some some setup part but uh we can figure out the
assertions part first so you could grab uh the model and call call the the yeah are we going to two let me I want to go
back and look at so the idea was to do it here in 23 and a half correct was to populate the themes this the only one we
so is there reason you're not copying that to start with oh yeah I was could have I was just looking at it to try and it
and then you can basically we can pull in some other themes so not just the same theme yes list is still a word that
that existed before Java existed so yes we can use the word list it is not a term interesting now we got ah okay cool so
now create song allow multiple themes not that version but we might have an overloaded version yeah let's go yeah there
is an overloaded Version Y so this one I would want to change it because see this song is about New Year Halloween do we
care so what's what's our goal for setting up the data for now this is good enough you're right you're right um so I
think what we want is we want data that has two more than one them B yeah basically two themes are more um the number of
songs is irrelevant right so what I would say is we don't need that first song and then inline the theme directly into
uh to get rid of the variable since we don't need the repeating true J there you go in mine um and in fact and maybe we
we could refactor it now we could refactor it later we actually don't care about the song names true into or we could
just make the names a relevant name well what I would do is uh what do you mean like a a helper method that abstract
yeah so what I was thinking is is a helper method where uh we basically oops we basically take this whole thing um
extract this to a method and then introduce parameter on the themes the themes great do you want to do that now test uh
either way we're going to do it okay so you're saying the whole thing so here method extract method now this one we call
it's a different it's also create song themes controller yeah and we can just say then you know create song themes
controller then yeah so you want to then extract introduce parameter on the themes yeah introduce parameter on each of
them or variables oh they would come in as one of our ars no they would come in as two separate variables and then we'd
have to do the manual work got it to make it for one did I do parameter yes you did and just select there uh you don't
want control shift it's Al ah no control alt I haven't done it yet Control Alt P yeah two yeah so before is is again you
don't need to select prior to initiating I figured that out yeah I figured that out once you set it like oh yeah okay so
now we've got that so the capitalization of New Years is is is bugging me um is that important uh I'm okay with probably
for the data entry part we want it to be when we actually search it's not Rel the case in sensitive but for correct
putting it in this is basically what what's going to right so here we we don't care about the view name and that we we
explicitly need that to be blank so that we get the search page so then we assert that well we don't want the view name
yeah so I would say don't bother even storing it as a variable since we don't right so now we get to make our first
decision what do we want to call the maybe current themes I didn't want to just call it themes by itself why not
available why not just call themes really no I'm wondering that was actually a question why so what what was your
thinking why why did you not want to use themes it's it wasn't I was thinking that in certain contexts it might not be
clear but I I guess in this context we're saying hey model what are the themes since there is nothing else in the model
I think that's that's fine right so what I would say is um uh to yeah I mean it eventually we're not GNA even have this
so it's sort of not not worth trying to figure out the the best name for it because eventually we won't be be returning
all the themes controller we won't when we start doing Auto search we won't the autocomplete will not you will not we
will not load all the themes into the front end Oh I thought we would then the front end would just them is 500 too big
for uh front end to handle like at what point does performance hit versus I guess here's the that's the trade-off which
you can only know by measuring um yeah so we we might um and it depends on how we implement the the front end but
there's there's no guarantee that that we'll do that right um since we're likely going to use HTM x uh we would then we
would not be loading uh the full themes we'd only be loading the ones that that that match search but we're still ways
away from that so if actually no not is equal to so is the attribute going to be a strings so it contains exactly
contains that's what I thought I was like what is the so what I would suggest is before you type that pull model get
attribute as a variable because we want to cast know you don't and and you don't and you can be anywhere and let it
right give you the Expressions so what are we doing yeah works for me Y and then we can change object to what we
actually want be and quick fix all right and so now we'll get the proper autocomplete on that I forget contains exactly
is in a particular order yes okay it's in the exact order so since we said we want it in exact order we have to Define
what we what we expect got it so then we would do list no just put value comma value value oh no the ual strings that
you that we expected to says so I basically we said in alphabetical order those weren't in alphabetical order oh those
are not alphabetical in English Halloween would come before New Year yeah yeah yeah sorry you Del too much there y i I
think you could have had intellig swap it but I'm not sure if it would have worked so it's a quick fix fix h no I guess
not all right no I thought it might it's one of those where it's like I wish it would have but yeah because that would
be helpful I think it only does does it on on uh parameters not not and let's see how is this going to fail it'll create
the control the Searcher create the model theme search passing and nothing will just return a model that is empty
because we haven't added the attribute right so the get attribute will fail I don't know how those failed is that for an
exception uh no return it return it returns null so we expect actual not to be null is the the outcome because when we
try to assert on themes it first checks to see if it's null and it will be null right so 69 will yeah say themes is null
got application yeah let's run our tests yeah give me a second I want to find one of those shortcuts that I've been
meaning to this the one I'm look see control shift plus no control shift plus that's expand oh no sorry control shift
semicolon ah yes ah but it only it only shows recent once you've done it then it becomes a recent one but it doesn't
show all your options so then the other way is to do and so you can start typing to narrow down so any any dialogue in
intellig you can start typing and it it Narrows down it all right fails is expected sweet so how about we take a break
and then we then we implement it have we really gone an hour uh more than an hour dang okay time flies when you're
having fun exactly so yeah a break sounds good all right so uh enjoy the coffee break and when we come back we'll get
that test to a so um wanted to remind folks that uh in we are picking our next book for our book club um and no I don't
expect you to read this list I'm just putting it there so that you know that such a list exists so we've got a list of a
bunch of books um to to choose uh today is the last day to to modify it um if you want to add a book um on the
spreadsheet and this information is in the Discord channel for the book club uh for choosing the next book there's a
specific thread for this uh basically we've got the list of books we've already read we've read quite a few uh over the
past few years and a little bit about what the best kinds of books for this book club are um and then basically a list
of of the books and the list is uh pretty long um so if you have a list that you a book that you want to add to the list
that you think uh achieves these goals which is basically is it related to software developments coding testing um maybe
process uh is it General enough to be of interest to people who are working in different languages um and also is it
sort of not an easy read like uh so I know um tidy first has been recommended but it's kind of an easy read uh there's
not much like it's useful um but it's sort of also you know for at least for folks like me fairly well known stuff that
Kent Beck has has talked about before um and so really I think the best kinds of books that really take advantage of
what a book club is um are those that you might find difficult to read by yourself or difficult to fully understand by
yourself because that's only because then it's through talking and discussing and asking questions and clarifying things
uh that we understand things better um and so for books like domain driven design or object design um unit testing
principles those kinds of things uh were really good books because we could really discuss them and understand them in
in ways that you might not be able to by yourself so that's the um book club uh question the book club yeah are all
these books newly added or were they leftovers from the previous book club then folks added to it yeah so basically it's
it's an it's uh all the books that were suggested previously plus any new books that people suggested got it um and just
because it's here does not mean it will actually be in the the poll uh so we the poll will start tomorrow um but uh as
the leader of the book club I get uh to decide what books we get to choose from um and so uh join the Discord if you're
not already member um if you're a member of the Discord uh and you're not a member of the book club then uh go ahead and
send me a direct message so send a direct message to Jitter Ted and I'll add you to the uh private book club area um so
uh starting tomorrow there'll be a a poll probably around I'll put only around 10 books in the poll uh and you can vote
and then I think the voting closes uh early next week and then June 26th is going to be our first session so we'll have
decided on a book everybody will have gotten a copy of the book and have read the first chapter of the book um whatever
that book is and then we'll we'll just we'll kick it off at the end at the end of June all right cool so I got a related
question um well tangential yet related okay so as a DJ I um one of the things I use is Spotify um you know I mixed
feelings about it but that's a whole that is a very much a tangent which I will not go down um but what's interesting is
I have this one playlist I've been using to create it's a collection of potential songs for upcoming radio shows and it
had a thousand songs in it and two days ago it had a thousand songs yesterday it has 23 only things I added starting
April 15th of this oh no and I'm like I didn't delete so that's going to be one of my like you know tech support oh if a
product like Spotify even has support right yeah some of these it's like your so you know you can post in a forum and
maybe somebody will look at it yeah I mean this one I'm paying for so it's I feel like there should be some support yeah
my I'm with you when you said yeah my brain is thinking the exact same thing so if anybody's ever heard of it anything
like that and no have any any ideas love to know but yeah that was my latest frustration last night I was like yeah it
sucks that we can't like and you can't export that data uh I thought there was ways to export the data using uh tools I
thought they had an API for that oh maybe external tools yeah that could be but yeah it's like if I can't export my data
and and I can't trust you to keep yeah all right so we got a failing test it failed as expected um should we make a
thing so we could make it fail differently uh we don't have to but there is the possibility we could make it fail
differently right now it's failing because themes is null we could make it fail by saying the list is not what we expect
it um right I offer that only to our viewers I think we could probably move uh faster but if you're not sure of even how
to get stuff in the model then this might be a good Next Step well you can probably tell that because I'm noticing yeah
h no no no steal now MH and then so you could run that it should fail differently right because now we're now it's not
going to be null so this is a good little step because it tells us did we put the stuff did we put anything in the model
correctly is it getting added to the model when we expect it yeah and then we can worry about how to get the contents
correct and so it fails exactly in that way yeah so then we MH you got an extra PR that's why we run the test to find
passes what happened oh there you go sorry I lost your My Stream yard window so I was trying to find it un monitor too
okay so that passes yep but that's just you know this hardcoded bang so now we need so we are in the controller so now I
feel like I want to look at a hexagonal hexagon diagram which I think I might still have on my screen my other monitor
let me see if I still have it or I could just switch to my h of course the movement out um you need to use keyboard
controls to do that if you hit the question mark and the lower move so zoom in zoom out is in the bottom so how do you
how do you pan on Windows I don't know how you pan on Windows I mean normally I just drag with the mouse but from a
keyboard stroke for so not is that how that works in in miror I thought I thought you have to hold down that um yeah you
hold down shift and right click so it's not going to be a right click can you do alt and then hold down the ALT key and
uh that doesn't work either no we probably shouldn't waste folks here put this back up while you're doing that I'm GNA
think about it so you need you need to get a Mac because then this stuff is much easier just kidding uh J because we
it's really easy to scroll it or you my other tools my other tools it works fine but I don't know I've so so um what did
you want to know from this this diagram so we are we just go back I'm gonna quickly look at the code we're doing theme
search from song theme Searcher which is basically we're starting with the test at this layer at that layer and so would
we again kind of like what we doing now where we go skip around the domain because really we're just saying hey
repository give us all your themes please um is there any reason to go through the domain for this well so that's that's
a that's a good question um this you're right that this is uh solely for readon purposes and so the compromise uh of
that we can make by by skipping over the domain and possibly skipping over the application layer as well or at least a
service method so we could go directly to a theme finder that is a port uh that themes so it basically be we we directly
go from let me use a different color use this color basically go out and go out this way to a port to a New Port that
doesn't exist yet that does not exist yet uh and when do you differentiate between using the word Searcher and finder I
think our current term for we have song theme serger is the class the controller that we are looking at right now at the
end point yeah so I I tend to use uh like at the repo level kind of thing I mean it basically is a is a repository and
so I tend to think of of it as as a in this case a finder um some people name it just themes because it's really all the
themes I find that a little bit too uh too easy to misinterpret um we're not searching for anything there's no criteria
that we're asking for it's basically just give give me all give me everything you got um so finder is is what I've been
tending to use where uh either I have a specific ID hey can you find by ID because that's the N sort of terminology
that's used for repositories um in this case it's gonna be a find all so um theme finder is is the name I came up um now
you say because we're returning all but we did talk earlier about returning a subset that I mean you know at that point
or is it uh or is it too much yagy because we're not there yet I yeah I don't know okay so we'll just stick with this
for now yeah works for me yeah I mean uh like Astra says it's like you know search you may or may not find it you may
not find exactly what you want um find is is generally you're getting something concrete it's either sort of there or
it's or it's not but again this is all you know whatever the common usage is and so whatever we decide is is is fine so
this case there will always be if we're basically saying find all that better not be empty yeah yeah it better not be
empty so yeah that sounds good we can switch back let me just move the uh oh one second I think I have somebody asking
me moment okay I'm back all right question all right um so should we test drive this from here or closer in so what I
tend to do is I tend to to say okay we're going to want some kind of other object that we're going to talk to um what is
that object going to return it's going to return that list that we're going to basically so so the question is is uh
right now we don't have any value objects that represent theme so uh I don't know if we need one but certainly um if we
don't have one then our uh then our interface right now for string right do we think we need a a value object trying to
think about this I know we had it as our nouns in our ubiquitous language I mean we may want to uh what sort of
constraints or validation yeah I mean it's I the only thing is you know do we require a certain minimum number of
characters do we require certainly we require it not to be blank we already have that in there as a check in the song
itself um other than that uh yeah I think again the Agy let's just stick with strings and then yeah when the type when
the need for the type shows itself we will then right refactor to it y so what I would do is then extract the list into
a method and then we can take that method and move it to a new object and then that uh or we can then uh um extract it
as a method for now and then yeah so let's extract that as a as a method yep find all yeah because that's what it's
gonna be that's what it's eventually gonna be where did it put that the bottom I'm just going to move it up close to
where we're working for now even though it's gonna move shortly it's gonna move next okay so then we're gonna move it
into a class that doesn't exist yet yeah so um what we can do is try to see if extract and we can give it our the name
that we came up with and this would not be in the be outbound it's not an outbound adapter either this is this is our
outbound Port Port so the one rule that is that you cannot must not violate is adapters must not like for me some of
these are you can relax a bit um but adapters must not call other adapters to me is is is a fundamental you must not do
that yeah yep so for whatever reason intellig annoyingly does not remove that method even though uh it's no longer used
and and I keep forgetting to file a that I sometimes feel like nobody uses extract delegates and nobody notices broken
so where did so it replaced it got it and so now the implementation on line 23 is useless it's not being used moved it
when extract the delegate and now literally delegated to it but then it actually replaced what we wanted it to replace
which is line 30 and so therefore line 23 is not used and you can just do it safe delete sa delete interesting but it's
like it it does every time I do I do extract delegate it it always does that and the method that's left behind is uh is
not needed and it never deletes it annoying so we've hit our quota for intellig bugs although I don't count one so what
should we do tests and they still pass so that's good I can hear you can you hear me yep okay clearly I cannot use the
headset mute button that seems to be the source of the problem so I have to make sure I only use the streamyard you
right which is a hard habit to break because it's automatic so I'm sorry you ran the test and and they pass so our
refactoring was was successful cool um so now we can go to theme finder and take a look at that find all method we can
sort of guess what it's going to it right yeah um and so now we uh we um before we sort of start test driving theme
finder uh we need to uh create that uh make that dependency uh available uh as as they say as an injectable dependency
right because right it's supposed to be a port but here it's a Concrete class yeah I mean that's fine because that's the
next step as we'll extract it to an interface and then of an implementation and so on but um right now uh it is not uh
an injectable dependency for the song theme okay and intelligy always adds in the delegate the empty Constructor which
is like okay that's fine I'm less concerned about that because at least it's can be somewhat useful he there full
welcome hey it's been a while no I think P na was our last stream it's been a while for me I guess because okay yeah
when was our last stream that was the 20 it was a while ago yeah yeah eight days ago okay so how do we do the injection
thing um so what we want to do is uh initialize so um do finder and move the initializer to the Constructor so this
prepares us now to yeah uh like that um Yes except not with the one at the end course does oh that didn't no no no no
that was not the you sorry you selected the wrong thing to extract yeah let me undo it you want to extract the right
hand side of the expression this part which I didn't did not need to select correct to a parameter correct and now I get
rid of the one yeah will I put the this in front once yes it will ah okay called so now in our tests we're handing a new
new theme finder which is what we want um it's complaining there because now spring doesn't know how to get a theme
finder when it needs one uh so let's make sure our test will pass and then we'll fix that all or IO uh IO free because
all will fail right because the spring Auto wire will fail yeah we could run it and see that it fails but we know fail
here we don't here here we don't need to actually run the test to see that it would fail um so let's go to our this um
where is that what kind of file is it uh we I don't we might not have set up a separate config file so it's in the
startup class uh we probably should move this um let's do that uh before you before you do um uh let's make a I think
the easiest way is if we make a copy of this class so if you hit F5 we can make a copy of the class and this will be our
uh config oh meaning like that just change that exactly yes location good yep okay uh change line 11 we're going to want
that to be just configuration as The annotation and then get rid of uh the main method we don't need that in here
actually can you just no just do it manually yeah and uh go back to the startup class and we can delete the bean method
from there because we now have it in our config does that work uh it may not work because it is I would just do it
manually okay uh let's run um oh let's go back to the config and add the the bean so we need another is there a no you
don't get to create One automatically no you could yeah not on method y uh I don't know I don't know why Cody thought we
needed to pass anything in we don't theme theme finder is currently independent of anything uh that's correct all right
if we run all the pass yes so we predict correctly you get so F asks about uh logs aspects in security can be considered
cross concerns should they be placed in the layer um if you're doing aspect uh to implement your logging um or perhaps
other kinds of things uh that is IO related the therefore it must go in the infrastructure therefore it must go inside
an adapter uh security presumably by security you mean um obtaining the security principle because security is also a
domain concept um and so uh you'll have the framework or Library specific security stuff in the the infrastructure
package because it's framework and Library specific um inside your domain you're going to have that so what went wrong
well let's see the first caused byas is error creating importer so we want to do when we see stack traces like this is
we want to uh okay yeah so we want to look at the ultimate source um so if we this the bottom right yeah this the bottom
yeah so you want to you want to line Auto wire so what is what is it saying I can't read it uh let's let's do that so no
qualifying being of type song service um okay so it can't instantiate song service um is that part of what when we moved
it over because remember this song service was under startup that's fine but it's in a configuration class so it'll it
should be picked up uh uh except in our tests it won't be so we need to explicitly add that so um and this is uh uh this
is where sort of some of this stuff gets gets a bit annoying um so but what we want to do is also just make sure what's
going on is uh here um so it's saying uh error creating Bean with song importer right and this test is about the song
that uh we we have mocked out the song jdbc importer where importer even being used uh song importer is um is actually
what we're we're testing against right oh we using importer to populate that endpoint to populate the list What will
what will be a list of themes yeah so this is a web MVC test so what happens with web MVC test is is what's called a
slice test which means it only um sort of makes available uh the controller which is the song importer um but song
importer if we look at song importer why don't you jump to song importer sure have to CLI making a note about importer
so it requires song service um and song service is no longer when it was previously defined in the spring boot
application it was always there but because we pulled it out to a separate config file the downside is it's not always
there the upside is this gives us more control when we're when we're running of what that song importer and song service
and so on look like um for now uh we're fine with that configuration but we have to explicitly import that configuration
into our test class let's go to our test uh you've got a yeah uh and let's go to the annotations at the top of the class
and so after uh at webm PC test import um and not that class that's the a stupid import because like you're importing
yourself which makes no sense uh what we want to import is the config yep and if we run that test those should pass uh
no line 20 no 23 that's just going to yeah my brain was thinking this was a second asks is song service a spring Bean um
song service itself is not a spring managed class and that's why we have the be method in our config to bridge the
framework to our uh agnostic application class um so we can basically copy that line to uh the other test class so we
can get that one to to pass the other one that was failing oh darn we didn't save that one we just rerun them all you
can just run all the NPC ones because those are uh yeah that's that's correct full enough all the anything that is a
specific concrete dependency on Spring Security um must be in an adapter must be in in the infrastructure layer cannot
be in your application your application everything inside the hexagon must be agnostic um or should be agnostic there's
cases where if it's not doing any kind of IO uh then it's fine um but in general uh especially for things like security
that you want to keep out of your your hexagon all right work looking good all right uh so let's do a yeah we did so
much I'm like how do we summarize what we did um well first we didn't we didn't actually do that much uh it's just we we
move some stuff around we never committed the finder I mean I think it's pretty much we started work themes I like the
rest is the rest is detail yeah cool committed uh so Jonas asks if I Define an adapter that retrieves the current
username from the principal would I um it depends uh so on an inbound adapter like uh with an MVC endpoint your I
usually act get basically have a parameter that's the principal and that gets passed into the method call when spring
calls it so that's on an inbound side because spring is providing it to me it is sending it to me it is sending it as a
parameter to my get map post map method um if you have somewhere in your code where you actually need to explicitly from
your application go out and grab the principal uh then that would be an outbound adapter because you'd have a port that
says hey I want to find out who the currently logged in user is so that would be an outbound port and then the
implementation would probably be one one or two lines of code of looking at the current context and returning that I
never do that because I always like to provide information and not force the application to request it if I if I can if
I have that information available so um it's a lot easier just to say hey Spring always pass me the it yeah tell don't
and ask is is the the way to think about it um if that works for you that never seems to work for me because I always
feel like it's phrased backwards to what my brain interprets it as but basically provide the information to whatever
needs it instead of so expanding on that is provide the it uh so importing song theme config solves the problem because
um the tests are trying to use the song importer the song importer has a dependency on the song Service uh but because
it is a web MVC test right it's a slice test the only thing that spring will actually instantiate and put in the
container or the application context the only thing it will put in there is the controller that you're testing um
everything else is ignored uh the point is is because it's a slice test you don't want to create more objects than than
you need uh we got it for free before because it was in Spring boot application and that's actually automatically all
that configuration is automatically included on on any web MVC test which uh is why we moved it out because we want to
have more control over when those things get created and I remember learning about this and being really confused until
it's like oh springing boot application is special and stop doing config in there because confusing yeah it's almost
always easier to be told information than to have to go and request it so if the if the caller has that information
available to it easily then just pass it in um and I find in in I can't think of a case where I've had to explicitly go
out and request hey who are who's currently logged in or who's the current user because it's always me all right um so
now all our tests work and we've committed so now uh we can now drill down a layer um because we've got our test against
the adapter that does the right thing uh test um perhaps not directly but somewhere in one of those creation Factory
methods in this test we're doing a new theme finder and eventually we're going to have to sort of promote that out a bit
but for now it's it's it's fine we can we it um just to to be clear why don't why don't we me here so if you go to the
implementation selected that one yeah and so here is the theme finder and uh we're probably going to want to introduce
that as a parameter to sort of pop it out because um well maybe not here maybe this is this is fine uh we could have a
better way to to sort of an easier way to set it up by um by basically uh instead of forcing us to create songs and then
figure out a way to to extract those we could just put it in the theme finder directly um I don't I don't think we need
to do that so I think we can we can now move on to to what what and how should theme finder work so yeah so what do you
think so we'll be talking to actually would you mind throwing up yeah there we go so we've got we've got the connection
to our theme finder so we got this that's too big but it's it's concrete but it's the uh so do we have it sorry I was
going to say so we have a choice of sort of where how we can go um what were you thinking well was like do we work with
the fake in memory adapter or with the the database directly or not directly but other words are we talking to I guess
we talk to the real thing we don't need to talk to the fake for this because the fake is only used for tests uh so we um
yeah I mean the real work is going to be in uh in in the in the real thing um for the tests we do want to provide a way
to create create a fake so we could um and we don't even need a fake it's basically just a stub because we're not adding
we're not sort of we can program it more yeah yeah um so for the test we just wrote we could basically say okay we want
our uh stub theme finder when you're asked for find all return these two songs right um and then we need to uh test
against prodction test against the right you said it was two two different approaches what were they again um it's sort
of like just which do we do first and I think extract the interface have our stub and then create the concrete one is
probably the our our next steps okay sounds good let me make it so you can switch back to me now so we just extract
interface on this class yeah the usual naming challenge let's see so the interface we want to keep it as theme Finder
right so that's why we want to do interface and we want to rename the implementation in this case it's just a stub theme
yeah everything else good and technically oh this should go to test right yeah so if you hit the three dots you can
select test from there and then we want to select the thing that we want to form the interface oh this guy otherwise it
won't do very interesting yes because now we don't have a real theme finder oh because this is the production code um we
could Implement one right in place uh for now which basically just returns nothing so just do this yep oh you're saying
return nothing oh no what you just had so this one yeah yeah I don't know why it's asking you the only one and you can
convert that to a Lambda because it's really it's a single abstract method uh you'll have to click on theme that y heck
you could even replace it with a which is not not obvious at all uh but that's fine this is this is temporary yeah
that's a little bit cryptic um so if it's to is there any value in in in doing that no I mean you could you could leave
it as an anonymous in class even if that's if that's easier to understand because this is temporary this will this will
go away once we actually have the concrete ofation okay so let's just leave it for concise but hey it's like it's a
method that returns a list and so just saying list of is is is is an implementation clearly it's a valid implementation
um let's uh let's run all the tests just to make sure we're still yeah probably break if we're doing we're doing a hard
stop yeah I was gonna suggest break all right so we'll take another break and when we come back uh we will start uh
looking at implementing the real thing you want to commit this when we come back first uh yeah let's commit uh continued
um I think we can say yeah okay all right enjoy the coffee break n all right and we're back you know the coffee just
made me think of something um like I like coffee but I'm not a connoisseur at all my my local neighborhood coffee shop
is um uh the owner is considered you know like one of the best Roasters like I think she I think she wins World
Championships kind of thing and she was telling me about these um beans she just got from Colombia MH and they do this
thing called co-fermentation which is kind of um so they literally ferment the beans with the berries still in them you
know the berry around the Coffee Bean oh in watermelon juice and added yeast H and um so she let me sniff the beans and
the beans smelled like watermelon I haven't I haven't tried the it's incred ibly expensive was like 40 bucks for a bag
oh gosh I'm hoping when she does a a tasting I can see what it tastes like but um it smelled like watermelon which is
kind of trippy so who knows what what kind of coffee it'll make or espresso it'll make but it would be interesting yeah
I don't know if I want my coffee smelling like watermelon well I mean I do know and again I'm not a connoisseur but for
some reason I do notice that for Ethiopian copies coffees it always tastes like blueberries and it turns out that's a
common yeah profile for Ethiopians yeah I mean blueberries uh yeah I'm I'm I'm I'm pretty much a Brazil uh Bean fan I'm
not much of a Colombian I mean Colombian is okay but I much prefer uh Brazil is my go is my go-to is your go-to okay
yeah so you know more than me I'm like I don't know what's I just know about Ethiopian because I like it and it does
does tastes like blueberries which is a trip compared to like wine when they say the wine tastes like leather jacket and
what okay doing so I just want to ask answer some so F ask why not use Java 21 records for persistence um I don't know
why I'm not sure if we did that intentionally what are what are uh what is our data can we go to our database
implementation stuff go where' again are you gonna click or you or you I was I was just pointing for you I was like I'm
waiting we G to click yeah uh well I'll just click then okay just do it yeah so um let's I mean there's probably no
reason couldn't do it I don't I don't remember spring data jtbc supports records yet I think that probably was why we
didn't do it um but right now there's no reason why we couldn't we couldn't store that the song dpos they be records too
as long as spring data uh supports that I don't know if it does resisting entities supported types uh I don't know I'd
have to look it because spring data jdbc is is oriented around storing Aggregates we don't really have an aggregate here
uh at least not yet um so generally your Aggregates are not going to be records because they're going to be mutable so I
don't know if spring data jtbc supports directly uh storing records I don't actually see any reference to that so I'm
assuming not unless it says it's somewhere but anyway that's why I wasn't sure if it supported all right so finder where
it go so you fall you've fallen into the Trap yep I know which is so easy to do I was looking for the actually this I
was I looked at the screen for a split second and then I Wasing what's the shortcut to get to this yeah I did files not
classes actually what is classes Control Alt n no classes is it's just plain control n control without that yeah the one
with the fewest Keys is the one that you probably usually want use the most yeah okay there we go so um what is our
actually what's our table structure uh I forget what it is um why don't we look at our uh uh DB migration scripts just
so we can remind ourselves what our table structure is now in this case we do this right is it TB uh you can probably
look for just uh V1 that one so themes are in an array so there's there's why you think it would be interesting well it'
be interesting because we could delegate all the work to the database of find all unique across all themes sorry across
all songs find unique themes and then return that uh sorted alphabetically and there a reason not to do that or uh pros
and cons what were you thinking there there are so I don't think there are any cons other than we have to have a a uh
the correct SQL um why wouldn't we have the database do so just out of curiosity if we had which we will never get big
enough to this be an issue let's say we had you know millions and millions of rows I guess at that point it would be
table well yes so that was that was sort of the the the thing that was in the back of my head uh when we started looking
at this is um do we do we want to create such a such a thing do we want to say that this really shouldn't be an array of
themes but actually should be a separate table and EV you're doing that now versus waiting uh if we do it now we don't
have to migrate yeah migrating could be kind of weird great um I mean so on the on the other hand uh uh always be
migrating um if you if you never migrate then you never know how to migrate and then you never know if that works
properly and you don't know how to right so how to do point um but you know but the question is is is is it worth it um
to to to to normalize the the data I mean certainly it would be way more efficient yeah right because we basically just
would read from the normalized table and we're done right really fast the so the only downside is it just it does make
our our uh our database objects slightly more complicated do you want to see what I my current and this is you know the
current spreadsheet um which does not have all the data by the way I still haven't gone through all my txt files and
Word Documents and everything and make flesh this out but even with this minimalist version which only has like 500
songs how many do I got here yeah almost 600 so the number of themes in theme one I don't really have a count but I 30
another 30 assuming they're 10 so yeah so that's like roughly 90 themes back of envelope right and how many and how many
songs 568 so I doubt we'd notice the the the um but let's just assume I get 10 times sorry I'm laughing normalizing a
relational database with referential Integrity sucks all the fun out of bug finding um yeah so so normalizing would mean
right now we're we're storing uh the same theme string multiple times in the database right so so as you saw from the
spreadsheet every time we've got a song that has Halloween the string Halloween appears in that row uh normalizing would
be splitting out the stuff that you you don't want multiple copies of into a separate table so you'd have your songs
table and then you'd have your themes table the themes would have basically the 5090 records whatever the number of
unique themes is uh and then you have a a join table that that joins them together and basically says for this song it
has these themes so this table's record has these other table records uh and so it's basically many to many um right
which is normalized but it does it turns out to be it's it's a little bit harder to deal with um it just makes the like
this is the object relational mismatch is that in in object world it's not as as convenient yeah and so so normalizing
uh if if you took a course in databases or or relational databases um there's different uh sort of how far you can go in
normalizing so there's first normal second normal third normal nobody really goes beyond much third third normal form so
if you want want to know more about that stuff do a search on on third normal form database and you'll get uh you'll get
stuff so let's just assume we have we ultimately have 10 times 100 number of songs well 10 times are 100 I mean even
like even like certainly on the order of thousands I to not notice any difference right um 50,000 maybe we'd start
noticing a difference but I'd have to we'd have to measure it right so are there any nonperformance reasons to normalize
now other than I'm just trying to play Devil's Advocate like sure not normalize now or normalize now um any other reason
to do it um you get to migrate earlier um from the always migrate perspective but it makes a joint then you gotta do
joins more often which is more complicated yeah so that's that's basically the the downside is uh the the table
organization and then therefore the queries are going to be a little bit more work because even just to retrieve songs
we will have to join into table Yeah I think leave it for now is where I'm leaning towards but what do you think I kind
of feel like leave it for now uh as well and just um keep keep it in mind for later so there so I mean that's that's
always the trade-off uh or or that's one of the trade-offs that you make in terms of normalizing or denormalizing
normalizing tends to to mean that um inserts are a little bit more complicated uh because you have to say is this theme
new and therefore I need to create a new entry in the themes table or is this one that already exists and I want to
reuse it um so the inserts become more complicated the selects become possibly slower because you're doing a join uh so
in a sense denormalizing is optimizing for for themes now we could do both um basically have normalized and denormalized
like a table for exactly and so so every time you do an insert you basically update that uh that normalized table which
very much has the feel of of cqrs yeah I was gonna say that definitely had that kind of vibe yeah seems like a punt at
this point I think yeah are there any more questions in the chat that we should answer before we um uh FN asks can we
use Juke we could but then we'd be completely swapping out our persistence layer we're currently using spring data jtbc
um what is Juke I don't really know that one uh so it's a different way of in a sense map basically mapping um objects
to to to your database tables it allows you to write your code in a type safe manner um and write sort of you're writing
database quer is basically an a fluent uh uh Java syntax um and so it's quite flexible especially so if you've got you
know complex database relationships table relationships uh it's really nice uh for doing that which we don't have which
we do not have yet uh I don't maybe never for this app uh so jaob asks uh W you want to retrieve all songs by given the
theme uh we currently do that with a query that looks through all of the rows um so that search would be faster with a
denormalized data because then you basically Traverse the relationship from hey what are all the songs that have
pointers into this row of this themes table it be you said denormalized would be for sorry normalized the normalized
would be faster retrieving of find me all songs for this theme right where it gets yeah and then you'd basically use a a
combination because if you're searching for multiple themes you want to find ones that match any of those but we already
have a query that works um using the postgress uh array syntax because if you look closely line eight there is that's
that themes text all right so uh we probably want to write do we um do we want to put our our do we want to implement
the theme finder in a new again song repository that's the port that's the port be in memory oh and this is the other
reason that that I that I I I'm stopping my use of repository for Port names is because it becomes very confusing
because we've got two things named repository and that one being the port and one being having the word jdbc in the
middle uh doesn't seem to help in that regard but for now let's leave it let's not worry about that so let's go to the
song jdbc repository because that's the concrete one so this one we've got our our our little query that does the select
that finds songs by theme ignoring case um so we have a custom query here that returns a list of song um oh uh this is
wait a second this is interface class though well technically it's a Concrete implementation because at runtime it's
it's actually becomes a concrete class so uh go back to the drawing again would you mind throwing that up used then
theme finder would talk directly to the same adapter yeah so it's it's okay to have two different ports talk to the same
adapter um I wouldn't use the term talk to I would say two different ports implemented by a single class is totally fine
right right yeah so it's a class that implements multiple interfaces but from a so technically from a Java perspective
that's that's legit from a hexagonal perspective it's also okay who cares okay as long as well I was thinking about that
plug-and play where you could remove one feature one aspect about hexagonal that I think is pretty cool is that if you
want to eliminate a feature you can just get rid of the ports and the adapters related to it and everything nobody's
talking yeah in that case you you'd get you delete the port interface and then you delete the implementation of that
Port interface from the class ah yeah so and then you're still not affect so as long as affects each other other words
yeah so there there's there's you have to be careful there yeah I mean you want to do it where where it makes sense
where there actually needs to be shared information um so for example in my tdd got uh I've got the situation where um
I've got an inbound adapter and an outbound adapter sharing who's connected because because both this one actually up
this one updates the contents of the shared so when you connect as as a player you connect with the websocket we need to
record that because then when I broadcast information I need to know who I'm sending it to so this is a fairly common
case where there's shared information and so there's one implementation of the the shared session that this one writes
to and this one reads from um there's some interesting symmetrical uh stuff going on but basically the there's a
concrete class that is shared by by both adapters okay uh for song themes I don't think there's actually anything shared
so probably doesn't make sense to put it in one put in this you so have a new adapter yeah okay let me get this off the
screen so we can go back to H okay oh clear oh you're going to make the drawing out that's um the is it are you pre
fixing the J okay yeah I think that at least makes it more clear that it's uh the jdbc implementation got it whereas for
our one we called we put the we stuck the jdbc in the center in the middle which is a little bit hard to see yeah got it
so we could rename that itself I think that might be a good intermediate renaming step yeah so let's just go there and
rename right now yep where go there it is probably want to rename from the implement the class side not the test side
and that you want to uh select because we want to rename the test yeah make sync and I would probably say rename all
right was that everything think so let's run our tests I just meant as far as renaming goes yeah oh yeah I think so IO
or all oh let's just do longer so full that's that's an interesting thought um these diagrams are are sort of uh by
themselves not useful so trying to make them useful on their own uh I don't think is worth the effort um these are uh
sort of on thefly in context boundary objects that are that we're we're sort of creating meaning together and that by
thems and this is this is where people I think go wrong with with artifacts is the artifact is not generally useful um
because or for anything that's that's non-trivial you can't just look at a diagram and understand it so you end up
having somebody walk through it in which case you want something that's a bit more um Dynamic uh which is why I usually
draw things from the from scratch so that we can sort of build in everybody's brain as we're explaining it you're sort
of context uh however the coloring is something that I have standardized on um and I talk about in in my talks uh so I
use the specific coloring for the different parts the inbound versus the outbound adapters uh and the the coloring on
the ports and things like that those are pretty specific we never did do the coloring on the project oh no we didn't um
I can go and Mark that as a to-do for me I wouldn't mind learning how you do that I have a video you have a video do all
right I gonna show um yeah full no is um Ted has a setup so that the adapters and each have their own color here in the
IDE so that it matches the cool but okay we do have hard stop in 21 minutes we probably should uh so we want a a test
then against um whatever the new the jdbc theme finder uh so let's write a that oh I thought we created a that's the
only theme finder yeah we didn't we didn't actually implement this the the jdbc theme finder ah okay we we just named it
in the diagram uh we hadn't implemented it got it so you can go ahead and and implement it uh to create an empty
implementation and we'll put that this will work right yeah that'll work uh and we'll name it said location's fine
because that's real not test code uh that's the wrong package though because this is our outbound now normally uh when
we have any non-trivial retrieval search or save um we create an adapter because we convert to and from our domain
objects to the database objects here since we're just returning strings we don't need such uh adapter so um so now we
want to drive this through tests um specifically a database test so here we're going to switch from our IO free test to
our database tests uh so what I would say is is let's grab our um and I it look uh let's grab the the jdbc test because
we're going to want a similar setup to that this one yeah when you say grab uh so we're gonna pretty much copy it copy
oh we're not gonna use the word repository anymore no right so this one's going to be called jdbc theme finder test out
jdbc this needs to be into the test okay so what do we change from this made um I would say Let's uh just delete the
test um so delete uh we don't want to autowire uh we'll want to autowire something else but we can delete the tests the
actual tests tests because we those guess I could have done safe delete n it's not worth it you would have to do that a
couple of times yeah okay all right um so yeah let's make a new test actually so what's our first test we may only end
up with having just one maybe two tests yeah so when we do a find all we want all how do we say that um so I think we we
can start with um find all themes returns all themes um and then I I was trying to think of how to put the return gel
themes at the front so we just we could say all themes all just thinking about that approach y so here what we're going
to do and this is why I wanted to leave the jdbc song repository there um is we're going to need to to insert repository
so actually we might want to had uh yeah let's let's grab those three y uh we don't actually need the the return value
so you can just delete the left side of the assignment and then tighten it up because we don't need the blank line um so
we can say all themes returned by find all themes and then we'll either write write another test or we'll expand the
test to have multiple songs with multiple themes yeah probably not worth parameterizing to have um it might be might be
yeah I guess we'll see when we um we'll see so that puts it in the database and so now we need to call our our uh so
we'll also need to like it says so it knows what we need um why doesn't it like it uh canot Auto finder is this in the
right um oh we haven't actually said what we Implement uh so so this interesting um Oh you mean from this perspective
yeah we didn't extend anything so we implemented but we didn't extend uh I think we want the same extends I don't know
that we'll need list crud repository but we'll put it in what's it not happy about uh you want the implements at the end
ah so order makes a difference in Java and it still doesn't like yeah because it doesn't have that's why we don't want
list crud I think we just want oh oh oh sorry um cred repository is an interface uh so we uh how do how do we do this
can we just do we just Implement both or do we create our thing as an interface I think we create our thing as an
interface so jdbc theme finder should be an interface and then it's implements and then you need uh a comma instead of
the other implements ah like that uh and it's no longer implements extends because we're now an interface go uh and yes
we are AO Auto scanning everything so um what's it complaining about on line 11 oh we have we're providing an
implementation which we shouldn't be right so get rid of this entirely uh well we need the uh we could provide a default
but we're going to write our own thing anyway so um let's delete the public let's delete the the curly braces we'll just
leave the override uh we're going to want to write our own query oh right kind of like what we did here yep in fact you
might want to borrow that because what going to look more complicated than that but that's the I want to look at that
again so we had the query as a annotation and then return to interface got it okay wait there's the param them yeah
we're not gonna have a parameter so we're not going to worry about that okay um I wonder how this is going to work uh
because we're defining our own method what is it complaining about it just thinks that you can't put a star in in um uh
is that based on the query shouldn't we no it's well it's based no it's based on the fact that we're extending crud
repository which already has a findall oh but and it's got this um so yeah so it expects to be returning an iterable of
song DPO uh for now let's do a rename of the method to be find all themes and then we'll figure out a this uh so I would
do the rename from theme finder or just do a rename here and have it to just rename this yeah rename it from here
because this will be more reliable yeah and you said find all themes um we could just say uh all name okay uh don't
think I would say I would say I think we'll leave it as is okay that's where I was heading let's go version uh so now
it's happy although the query is wrong it's at least now happy right uh F asks what's the benefit of using list crud
repository list crud repository instead of returning an iterable for things that return multiple items it returns a list
which is usually days um but we're not using any of those so doesn't really matter um so what we would like uh is
something that returns a single column uh and a single theme and it's going to be wrong uh but it's a good Next Step but
it's a good a good Next so let's do oh I missed uh asterid celebrate what were we celebrating the working it's true we
don't celebrate enough we all right it doesn't work as well here as it does on OBS um so uh let's change our query so
it's not going to be select star it's going yes uh and it's not going to be directly from song so we're gonna have a
nested uh Wonder we do something simpler first um let's see what would let's return something simpler uh yeah so let's
do this um so select themes and then using the array syntax so open close square bracket put a one in the middle uh and
then say as theme not that that matters no you no no you still want don't delete that stuff that you just deleted we
still want that uh so as theme with a colon or without NOP without there are no parameters so there's not going to be
anything uh and there's no were Clause because we're not all so this will SCT the First theme in the array and
regardless of uniqueness or anything like that so if we look at our test why top um let's add another uh that's the
wrong test um but we can grab the data from uh and you may as well grab this the save Parts too actually why don't you
just grab 53 through yeah the saves yeah because that's exactly what we want it's this test not that one and put that in
place of what we have there uh if you you have a question just ask it we're using test containers we're using um the
repository to insert our data so this gives us uh if we were to get the First theme of everyone we would expect money
money daddy right because we're not do we're not we're not we're not doing anything about trying to get all the themes
we're not trying to do uniqueness um so this will make sure that this will give us our our sort of First Step uh so
let's um let's call the the all themes method finder which is our jdbc theme finder yeah yep and we can just assert that
y it's not F all all things oh right so you probably want to undo yeah because it's going to be a different variable
type right no no just all themes no find oh we got rid of the find right yep yep and these are themes yep and then we
can uh insert that it contains exactly what we said it did easier uh so we expect three strings just three strings okay
right it's the first it's basically the First theme in every row and we want this to fail um actually it should pass uh
it may not pass because uh we don't know what the order is going to so this might fail this might pass depending on what
the order uh that we actually retrieve things are in just run this one test or this yeah do you have Docker it and
whatever happens this will wooho that it worked fast cool all right so next time uniqueness and order yes uh because
that's decidedly not in so I'm gonna do this yeah or actually we right yep so we can mark off 13 and get the dopamine
here that's right so ASD unfortunately we cannot use distinct uh at least not not in not that I'm aware of because we we
first have to sort of unwrap uh or what postgress calls unnest the array so we get basically a bunch of them um and then
uh distinct won't work because it's going to think it wants distinct across records and so we have to use a different
mechanism um but we we'll see what that is next time cool yeah I know for me same same way uh jaob is is is basically
like I'm used to normalizing stuff what's with all the data all right so That's all folks for today thanks for for
hanging out and and cele crating our successes with us uh and uh next time we will pick it up from here um changing our
query to uh to have just the unique set and then the unique Set uh alphabetized and then that will enable us to go back
to the front end um and implement the dropdown and then we can start talking about the actual autocomplete aspect and or
the the any any final words Mike no we should probably do a commit and push yeah yeah I can do that after yes so we can
do that do that after um our next stream will be sometime next week probably yeah we'll figure it out so as always if
you want to stay up to date on when uh I schedule things uh join the Discord T.D Discord if you're not already there
join um been there's some good discussions that going on there and of course the announcements channel has when uh when
we schedule the streams um that's the first place it'll broadcast all right so we'll see you next time sounds good
thanks everyone bye
