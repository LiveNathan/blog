# ＂Song Themes＂ Episode 39： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=ujb_O6myknY

---

## Transcript

all right hello everyone welcome to another pairing stream how's it going Mike doing well doing well I now have to go un
mute my office phone I don't know if you can hear it but um ah yes so many devices to mute in this world yes too many
well good uh um so yesterday uh we the auto complete uh so we'll basically pick it up from there sounds good I think we
left off on when you pick a a suggestion it initiates a search maybe we should run it just too yeah so let's let's run
it to see where D or C has multiple entries right if I pick one it searches well ignoring duplicates right um it's
searching on America because that's the first thing in the search box it's not actually based on our selection from the
edit box so that's I think where we left off was we want to stop using this as the input to the search and using that
instead well I mean I think we have to fix the fact that clicking on one of the items should not submit anything uh at
least not submit a search true yes um it does bring up the an interesting point though of uh because we're using htx um
who who holds the state of which autoc completions have been selected so we haven't discussed that yet um right but it's
it's a very like I think my even my natural reaction uh is oh of course the front end holds that and then at some point
it'll submit all those entries to the back end except that won't work that won't work why just to know what you're
thinking uh because when we fill in the options for autocomplete one of the things we said we wanted to do is not
include the ones that have already right so we already have to you know yeah list yeah so so it's really interesting
because this is what I would term UI State um but it's still State and therefore uh if we're going to have Supply the
the list of autocomp completions from the back end we have to supply the list of selected items as well and communicate
that to the back end um so I think uh using a but button is actually a good an okay Choice um we just have to make sure
when you click on one of the items it it it does the correct thing it doesn't do a search it just says you've now
selected right uh you've now selected this one right which gets us set up for multi- select right now we're doing single
yes right um so it's kind of like a prepare for that yeah and and this came up yesterday where it was like you know do
we just do the single move on to the to the multiple I sort of wasn't sure but it seems like we have to do this
regardless uh and it's a it would be a natural next step to to go from one to to many right yeah of course makes sense
hey tkes welcome Tes nice to see you oh you know nice to see you you know what tkes um we realized after the stream
closed that we didn't answer one of your questions yesterday oh yeah and I don't remember what the question was yeah if
you do so if you remember it ask again yeah I think it was something about HTM X and not reloading the page that was it
um and so yeah so so again this this is sort of a like we could do this you know as the actual component that I'm sort
of cripping from uh do this all with JavaScript on the front end and then you know basically when the page loads it gets
the list of all possible themes and then all the interaction and and UI stateus held in in the browser itself um that
would be okay if we wanted to do JavaScript uh and you know that gets away you know that would that would improve
certain sort of latency um on the other hand uh it it does mean we'd have to write JavaScript and we'd have to figure
out how to test that and so on whereas using HTM X as you type um one of the things HDMX provides is is doesn't reload
the page so we can do a selection and basically Target uh refreshing parts of the page um there's a term that that uh is
used called islands of interactivity so this idea that you have a whole page that might have a bunch of stuff on it um
but really it's only these sections like are autocomplete in the drop down uh and in fact you could sort of do even a
live search as you do the autocom completed displays below the results and you can then modify your your search and it's
constantly updating the the results instead of going to a different page um so that that's something that you know if we
decide to do that is totally in the in the remit of of of HTM X and this is the target thing you were talking about
right and there is if you've watched my streams on on HDMX there's multiple ways to Target you can Target um uh on the
response you can actually have the response do what's called an out of band Swap and Target different elements uh so
that's how you would do something like the as you're as you've selected your your themes it would refresh the the search
and you can do that um with response but we're not there yet uh so um I think then our next step is I guess one other
thought I had was yeah sorry just go back to is that um it seems like a lot of the stuff is done in JavaScript in the
browser that the the way we're working my sense correct me if I'm wrong is less common oh yeah well well these days it
is this used to be how you did it 10 12 years ago um and then people got I think I think you know an entire generation
got caught up in the uh you know Spa framework more of comp you know uh of of increasing complexity and it's been I
think generally not not a not a great place to be um and we've forgotten that like no instead of trying to sync up State
between the front end and back end just keep all the state on the back yeah so why don't we add a step before there yeah
so there um I think we have send or or do a do a post of the to to the server yeah to the back end back to the back end
back to the back end um that's fine uh if you're going to if you're going to quible then it should be select excellent
qu I agree with that um and probably put a note that uh this the end maintained on the back end sure is back end one
word or hyphenated I yeah I think it's a software engineering word um yeah it's not even hyphenated interesting an
Oxford dictionary has two words well yeah so we wouldn't hide hyphenated unless it was it was it was describing
something else like the backend framework right um if it's if it's the subject of the sentence then we hyphen although
it does look weird without it but it does um do we get a pedantic gold star now yes we do uh so let's think about this
step um we want each individual button to right we're dynamically stuffing buttons into this div yeah post uh so we'll
need a post and we'll some way of figuring out what what values we want to get so um first yeah turn off the current
selecting kicking off this button search actually that's what that's what we're gonna fix okay I'm just trying to figure
out like is there a way to turn the well we're GNA we're gonna fix that so what we're going to do is we're going to add
a a uh an option to the button that won't do the default post got it so that fixes fixes that problem and implements
what what we need um but it's not here it's in our our HTML Transformer right yeah so what we need to add is um well the
the the first thing we want URL the button to a post or have an HX so there's gonna be an HX Dash post on on it on it
okay yeah now we should drive that from yes the test actually we got oh yeah this is the only one yeah yeah now that we
we pulled it out uh we can we can dive right into that yeah yeah um so let's add a test and we'll only do a single
button uh so we'll add a test oh I guess we modifi just modify this test otherwise that this test will yeah yeah yeah
yeah yeah yeah uh so what we want is um actually will this work if you do it so it's a double tap and and on a second
press you you hold it down oh I was trying to that way okay no not double tap on shift no control control or is it
actually I don't know what it is on Windows let me search my cheat sheet the word double yeah it's control it's a double
tap on control so tap press let but you have to do it you have to do it tap tap uh I don't know why run anything is
coming up for you uh so it's tap tap a second time but hold or is it tap a third time and hold no it's it's press and
let go press hold arrow no I remember we had this issue before we tried yeah and you were not pressing it you were
waiting too long between key presses there we go got it yeah yeah I was moving it too slow yeah okay so now here we want
you Gotta Be You gotta be quick enough so it the text it as a double tap and not just you hanging around and doing
something else dpost uh and that's going to equal and then in double quote um this is going to be our endpoint URL so
this is going to be new endpoint um I don't I don't know what that endo's going to be so some endpoint we we'll figure
it out in a second um let actually see what what what do we points uh right here so this would be this will be under
themes so themes uh I don't think it would be a post I think it's going to be a new endpoint so um and then what we need
uh is the values so when we do the post we need to also thing it so uh so HX Val so it's uh HX Das vals vals interesting
yeah okay and and that is going to be equal to um so let's see it says by default the value of this attribute is a list
of Json what we want to submit is basically that string you want to show what you're looking at no I'm I'm just I'm just
thinking of what what do we we want to send I think we just want to send one name value pair so it's going to be um uh
uh an open curly brace because we're going to basically write some Json um really like that se yeah selection because
it's Json so it's all quoted selection then close the quote in a colon then a colon yeah because remember this is so
Json is double quoted thing col value so what we want here is and this is going to be different for for these two going
to want to uh take off I'll do it then I'll do it and then just change it okay so it's got basically it's going to be
cats and dogs as as the value um but that has to be quoted as uh and then before the uh and then closing curly here yeah
and for the so since we're using double quoted strings in the Json we need to use single quoted strings for uh for the
HX vs yeah so change that to single quote and then you'll need a closing single quote after the curly yep so that's our
that's our Json in I think that'll come in as as what we want is there anything else we need so this is basically saying
we've we've selected this item so anything else we need to pass and right now we're just doing single selection so well
you can only click on one button um so then the search button will initiate the search based on the the single or
multiple selections that are right uh how do we feel about selection as the key do we want that or do we want theme or
well the endpoint is called selected themes it's actually selected theme or will we make it well it's opposed to to an
endpoint so so selected themes is is the idea of we're creating another resource under this endpoint so that's why it's
plural okay so then I guess it would be theme what do you think yeah I was thinking I was thinking because I was
thinking ahead to when you're going to remove a selection um we're basically going to do a delete to this endpoint uh so
I think I think theme because that's actually what's being selected yeah so good um so I'm just double from yeah that's
that's weird um oh there it is so let's see so I'm going to switch to my screen because we're GNA so by default an
element that causes a request will include its value if it has one if the element is a form it's not a form um the name
attribute of the input is request um so maybe we actually don't want to use a the the vowels because that's for for
sending Json but I think it's easier if we send uh sort of standard form input which is easier yeah I think we want to
do that so what we can do is instead we can just send set the the name and value um attributes of the element directly
so let's that's certainly cleaner let's that okay so change this to name HX valves to name uh I would just delete it and
let's let's start over with something else okay because uh so it's so it's going to be theme you can put that in double
quotes it and then value equals and then the value selection yeah so I think that's that's what we want um what I like
to do is validate that that's what we're gonna get yeah uh so um you want to just create a a dummy button somewhere
outside of this we can inspect versus the uh yes uh we just need to have some endpoint that it's going to hit so we know
what what being sent oh um that's fine we can create a test endpoint and then delete it okay so what do you think just
uh so I'd stick it where it ends up going anyway which is in the autocomplete box okay and then um dummy endpoint what
do you want to call it uh well let's do that let's create the that endpoint since we've already got it uh or yeah or
actually it doesn't matter you can just say dummy maybe that's better your choice let's let's make it dummy so it for so
it forces us to recognize that gotcha uh and so let's create a uh let's just create an endpoint in one of the
controllers as well put in and it's a well first we'll just mapping um and actually let's let's do it to to slash themes
because otherwise we're gonna have security issues and we'll change the dummy to to themes ah right because I don't want
to then go go and change the security to add dummy uh so this is going to be public void um dummy and what we want is
values uh and then let's just do a a system out of print line of the values so you can do that um yeah that's it on the
on the on the back end and so let's just go into the HTML and change it to themes and then let's try it out can we try
it out just by no we have to no because you gotta have the server running right right re restart the server go grab the
actually where did they put it there it uh okay so this is this is this is why um so let's scroll up I have a feeling I
know what what this is all about oh wow that's a huge amount really big uh template themes error resolving template
themes understand I don't understand why why it's trying to resolve a template called themes up so what you want to do
is you want to jump to the top of top of the stack tray like all that other stuff like when I'm looking through stack
traces like all the stuff you were scrolling slowly through like is is is irrelevant so what you want for the the base
yeah oh that's what I was looking for but I was just doing it slower um but here's the initial initialization so here's
where we started yeah so here's here's what I want to want here's here's what I do so it often starts at the end right
and what I do is I'm looking for I'm scrolling quickly because what I'm looking for uh in this area is when I see the
most out dented thing so I can scroll quickly and say ah right so right here is is sort of to the top I wish there was a
a way to jump to that um like intellig will automatically fold some of the stuff but it doesn't it doesn't make it easy
to jump to that uh and then so of continue quickly scrolling find the next um it's interesting that it happened and then
we can sort of then we find we're here interesting oops sorry about that why does it um song theme Searcher dummy here I
thought we get rid of the word dummy that's the the method so basically it's saying that the post to slash themes um it
ended up uh oh right there's the name it ended up mapping it to this class this um this method I forgot we still called
the method dummy even though we yeah right right so um I guess it doesn't matter I'm just why bother trying to to
resolve a template called themes because we're not um anyway that aside uh uh it says that the map is empty which like I
wonder I wonder if it's automatically um encoding it in Json meaning the signature is wrong for what not sure why it's
not passing anything so we clearly clicked on the right oh we may not have told it that that we want the request I don't
think that's necessary uh we didn't tell it that there what um so when we yeah I think we need to to tack on in the
controller we didn't tell spring that uh we want that map to be generated from the request parameter so let's stick in
an annotation in front of it which is at request parameters and let's restart and try again and we'll ignore the errors
I'm not sure what those what those are coming from all right so let's let's scroll all the way to the top now that we
know that here's the initialization yeah so there it is uh theme- query equals oh that's interesting uh requested so it
looks like it's actually uh treating do we have did we create a form because it it's now basically passing all the
parameters I think we might have created a form and that's why we're getting more parameters expected yeah yes it's
inside a form and that's why um uh we probably don't want to do that so let's change the HTML so I'm glad we
experimented let's change form down yeah yeah uh let's try it again so now I'm expecting that we'll just get name uh
name value yeah name yeah and there it is all right that's what we want great it's doing but it's not doing name equals
cat it's doing oh right no never mind because we set name to theme right and value to cats yeah yes so it's doing that
yeah cool what's this other time Lea stuff we're not sure what's going on with that uh I'm not gonna worry about that
just yet um because I wonder I'm not sure because we're actually going to return something from the post um so let's do
one more dummy uh now that we know that it's returning a single value let's make sure that we're recognizing that so
instead of a map of string to string we're just going to have a string and we're going to call it parameter uh now we
can give it a par uh a parameter where it's uh you don't need to specify value you can theme that's it okay so that's
saying is find me in that list of name value pairs find me the one called theme oh gotcha and put it in this variable
which happens to have the same name but I don't and spring can rely on the parameter name but sometimes that gets lost
in certain compilation situations so I always put it and as a specific string to our request param would it should we
consider changing the name here to selected theme so that it is different from the Pam name so that this is different
than this or is it better to keep well it's it's usually you want to keep those aligned um if we want to change it to to
to select a theme uh I I'm not opposed to that although it might be redundant when we have the post mapping name select
them themes yeah that's fine I wasn't sure the meth yeah and the method will likely be called select theme right not
dummy yeah uh let's run this and make sure we get cats cats so before you switch away what I usually do at this point
when I'm doing this kind of uh console monitoring is I hit the trash can to clear what's there and then it makes it easy
to go to the I like how that's a like a really old style garbage can these fancy new ones okay clicking the so by doing
that we've basically parsed because before it said theme equals cats now it just says cats right we don't have to do the
parsing manually that's the idea yes yeah the way it comes in is usually it's it's it's form URL encoded or uh or Json
but we don't care um I think it's it's in the body spring is is parsing it the way we expect uh and so that's we've
we've finished our Spike and now we can toss out our our Spike and uh be confident that we know what we're doing got it
so we gonna um delete this end point or uh yeah so let's delete the uh the entirely good evening astred hey AST oh you
gifted uh a month to to uh tkes astred nice hey there uh Tatia um what's setup I'm not sure what you mean by setup if
you mean framework and language Java spring boot welcome and if it's than framework then clarify the question yes so if
that didn't answer your question ask again um all right so what else do we want to delete let's delete that that that
cat's button right uh and that's all we did right yeah we did move the form down here but that but that's we need to do
anyway yeah yeah um so let's let's do a uh a commit on on HTML uh just say uh move the move the auto complete outside
the form all right and now let's make that what's likely failing test uh we'll make it pass should we make it fail first
uh did we did we not see it fail I guess we didn't see it fail okay let's see it fail yeah excellent and it failed
because it's you could just actually yeah you can certainly grab the hardco stuff yeah up to there well actually I'll
take out the cats in a second so well I'd leave the cats I'd leave the cats in and so now it'll fail just on the dogs ah
good point and and we'll generalize that yep y much easier to see on that yeah yeah click to see the difference oh yeah
totally all right uh let's generalize what's the Syntax for adding in I think you have a bigger problem how do you know
what you're G to put in there oh because it's it's a list of themes yes oh oh oh oh oh and then again so it's doing this
part correctly both and that's coming from oh because the joining is taking right oh we have to somehow yeah I think we'
re gonna have to go move away from Jo the using joining and just map each one individually ah so in other words you not
use streams or still use a stream no you still use a streams but not use joining use map got it okay so what I would say
is um since this is a refactoring that we're about to do essentially you know we're red oh I see well I was gonna say
let's let's get back to green and do the refactor meaning which way to getting back to uh whatever basically revert
stuff until we're we're back at Green oh I see so take this stuff out yep probably want to save it off somewhere like
com slly thinking that so what I would have done is is commented those two lines duplicate even better so so duplicate
duplicate the entire lines and then control D I think will duplicate by the way oh yeah I forgot about that one and then
uh and then revert those lines oh actually you're right I can revert them manually well that'll revert the entire and
you'll have to revert the change you did at the bottom right so it's gonna fail but now differently yes okay as says
when failing test disturb deployment just comment them out guess you want to avoid somebody finding out that you have
you knowen all right uh so let's let's refactor our our joining to to just map one by one can I uh I think we'll still
need the joining but we'll only want the new line separator uh we won't we won't want to pref we won't want we won't
need the prefix and suffix because we'll generate those yep and so what we get is a string and string like this no no I'
m my remember my map my streaming skills are okay so uh when we when we do a map it's basically it's we want to define a
lampda that takes a parameter and produces a parameter so our incoming parameter we will call theme and then we have an
arrow and then what do we do to that theme to get the string that we want so what we want is we want to turn the theme
into a button got it so it would be well what does it say in the test copy and paste from the test oh from the test just
copy a button copy the whole thing the whole thing yep and paste it in double quotes doesn't say right so we have
basically said right now we're mapping all themes to cats that's fine that's a good first step um and then we want to
collect uh we don't need the prefix and suffix what we want is just a new line As the delimiter so what I would do is
delete everything inside of joining and and basically kind of start over Okay because you're gonna get the wrong help
because it's it's the wrong wrong version of it cut it just go there right now there's going to show multiple versions
right and so the one we want is going to take a single thing sln and if you ask for help it'll show now the help on just
that because I guess it shows them all well anyway I just want to check that it was a character sequence so that's fine
right um so now we expect uh this to fail because cats are not dogs um but it but we should that should fails and it is
and so generalize so theme can we put can we do like a um while we get quotes here you can do a a percent s and then do
do formatted ah okay cool so then here dot formatted percent s not X I know what just making sure you were paying pass
something curious what it's suggesting that you do with with that I suspect it's gonna suggest uh a method reference
yeah yeah so what does that look like does it do string colon colon format what I'm curious what it what it'll do it do
it interesting uh fat f really an interesting way of doing it it totally makes sense um but that's that's hilarious but
how does it but it's not clear that it's doing theme in the is it because no it's it's more it's definitely implicit
rather than explicit it's I I don't know that I would ever do this but it's interesting um I think we should revert that
yeah thank you um I mean it it it yeah I think it's it's it's non obvious like you say it's like we're we're that you
know the percent s isn't G to stick out or anything so right um we can get rid of uh line eight and nine because we're
not using that anymore oh yeah right so it's funny I'm not sure that this is this I'm not sure the the joining was
actually better than this I think this is actually more clear than what we had with the joining so this was this was a
good refactoring regardless true I agree yeah all right so now it should pass yeah yeah um it passed before but now now
we know passes now we go back now we can now we can move forward we've done right sure yep actually I could even but now
we should be yeah now we should be able can we convert to um that's what I was thinking to yeah is it gonna allow us to
do a quick fix to to a text block that let's see uh no I wouldn't select anything because it's the whole string that we
want oh right all the way out to here so that's why wouldn't select anything ah so just do Alt Enter uh yes second to
last option excellent yeah that's much easier with now we go back here uh you can just paste it's already in your
clipboard oh you're right um right there and I would put dot the dot formatted on a new line no you don't want to
replace that um and the Orange is bugging me I don't know if it's bugging you uh so let's tell it to stop suggesting
that how do you tell it stop actually um so hit Alt arrow and now uh disable inspection or suppress for let's suppress
it for the method no let's press it for the method okay right arrow that's a good one yeah so so when whenever so often
um intell when you especially when you do Quick Fix um hitting selecting the item and hitting the right arrow gives you
options for that item uh and so especially for things like when it's suggesting to to Quick Fix um you basically do the
right arrow and and tell it not to do that um but it's not always disabling it's always options all right uh let's make
a pass yep now since we're reusing the percent s that's not going to work because it ah so what's the um the way to say
to reuse that same parameter oh I see never mind you don't need to tell me it's this right well that's one way to do it
oh I mean and that work um works yeah we keep going what's the better way uh you can put a positional parameter inside
the percent s oh like um curly zero no uh it uh uh uh now I'm taking I think it's just percent Z I think it's just zero
for the zeroth parameter oh just do that for both and then and then uh no it still has an S but it's zero in front of it
um is it that hold on now I gotta look at the docs because now I don't remember let's look well no let's look let's look
at the docs because I think that's wrong yeah so bigger uh and uh click on here let's go to format string uh and it is
argument index oh sign ah so it's percent and if you're going to use an argument index it's the argument index dollar
sign um and the first argument it's one based not zerob based wow of course why not be different so it's yeah yes thank
you ASD that's cool I didn't know they had uh ah yeah yeah yeah I've used that and so it's one of those like I know it's
there I just syntax yeah I think in C it's like something like this I'll just type it out in space um I think it's just
that for the replacement pretty what percent one dollar sign s is less well because the percent you need anyway so so
having an open and a closed brace is one character more than having sign that's true but then you've got the well the
percent I'm just saying when when this was when this was created bites mattered I guess now who the heck cares J on for
everything yes uh can we reformat this because this looks really yeah uh yeah that's fine yeah took me a bit but I think
it's okay um all right that control K selects all looks like it remembers from the last time um control K should select
again interesting I wonder why it didn't that one time I don't know sometimes it'll open up the commit window and won't
change anything and then another control K does the check check everything I'll try that next time it happens yeah next
next time it happens we'll we'll we'll one uh we pretty much just updated our our HTML to add uh the oh the HX post it's
supressed yeah sorry you were saying we should type in uh what um added uh HX post or added HDMX buttons yes I forgot to
check jir how are we doing post of no we're still working on that we're still working on that because we we've got the
we've now defined what the HTML should look like uh and so since we're at our hour mark probably take a break sounds
good uh and then when we come back we'll Implement uh we'll test drive the post mapping endpoint um and then next so
after the post mapped endpoint we will then need um that post mapped endpoint to basically do a uh send the HTML to
display the with selected themes well it's HTML uh of or for the selected theme well we'll do one and so the HTML will
send it back and then we'll do many and the HTML will send all those back yes right so the way we'll start mixing up
these two JS which is fine right asard mentions that message format on the other hand uses uh index based things because
message format is newer or uses newer syntax who the heck knows inconsistencies bound thanks as I feel Vindicated and
then there's logging where it's just an open close brace that says you just give me the next string so we've got our
choices um once we get string interpolation then finally we will have one way of doing things and all the other ways
should be deprecated but unfortunately we're at least a year away from that because they had two previews of string
interpolation and they pulled it because they wanted to do a redesign uh so there's nothing in jdk 23 no string
interpolation at all so we probably won't see a preview until jdk 24 which will be in nine months all right let's take
our break and when we come back we'll continue with with our uh Auto auto autocomplete selection cool sounds good all
right see n uh so just a reminder that um our next book for our book club our next season for our book club uh is
happening very soon uh Sunday this coming Sunday uh we will be starting with chapter one of uh Martin Fowler's
refactoring book so make sure you uh if you have not already joined there is uh very easy way to get into the book club
you basically go to this link join the Discord if you're not already member um if you are a member uh or after you join
send me a a direct message to jittered just let me know your name and I'll I'll get you all hooked up uh so we meet on
Sundays uh from 10: am to 12: noon Pacific time which is 5: to 7 PM UTC uh and we meet on zoom and uh so our first
session we'll we'll just get introduced and the first and discuss the first 20 or so pages of of the book so that's that
um I also have my TD game as you can see up here tdd game I also have uh you can't see the the the game here because
it's green so the green screen is overlaying it but just got a sample of of some hats and and this actually came out
really nice this is embroidered um Jitter teds tdd game so if you want if you want a tdd game hat uh they'll be code
what's embroider this code what's that let's embroider this code yes since the Hat's embroidered finally crafted I was
actually impressed with like it basically took a raster um image and and turned it into an embroider uh uh pattern and
it's actually quite impressive and it did a good job on the colors too I was I was just very impressed well that's cool
um all right so let's now that we know what are what the post is going to do and what it's going to look like and what
it's going to send um now we can probably write uh um what is it B no what do you want to do I was gonna go to the test
for this this one yeah control shift t uh we want the MVC test first oh right right right right then no contr n yeah
then it would be themes yes and actually it's a post right selected uh yes themes returns 200 for a post also um let's
see we are going to return content from that 200 I'm just gonna steal here and change it to post I have this funny
feeling same so you can do Alt Enter to import that when you're ready plural do we do a query parameter for this uh so
we do want to put in uh a pram so outside the PR so not as a query pram though ah because it gets sent along as part of
the body so if you hit enter and type dot you'll get prams or pram actually and then this is the name value pair so you
can say theme comic cats or something yeah like that and then it still expect is okay yes now this will fail because we
haven't created the end point correct now will it be a four the wrong test I want the wrong test or will it be a 401 or
will be a 403 that remains to be csrf is it o in the name is um no we'll get to that in a second we need to add the uh
in the test after the post we need to tell it that token oh um that I don't know how to do do we do that uh so we do
that elsewhere if you do a a search you can find it but basically um as part of the post so after the dopram so this
will be a search not a C srf cross site request one watch out for your PRS so the csrf is another one off of post so if
you do yeah I see so it's after yeah got it y so if we run this uh what Happ I haven't put it in yet but it go oh no it'
s now you had it right you just had too many closing PRS ah so if you're gonna do a paste which I probably wouldn't do
but if you're do G to do a paste you got to delete that closing PR PR Y and import that and then close the pen there
okay all right let's run it again I expect it still to fail um a different but hopefully a different okay um now why
have we even created the endpoint we haven't yet no we haven't that's why it's a 404 yeah yeah um can we go to yeah that
shouldn't that shouldn't be allowed that's fine we'll we'll take a look at that oh because uh we're not right uh we need
to go to our test security config oh we go to the top of the test that we're yeah uh if you go to the song themes okay
yeah so that's a so we don't have we're not overriding security so we haven't specified any security for our endpoints
that's why we didn't get a security error we just got a 404 so that's fine we'll just need to we should probably go and
add it to our security right now because uh otherwise otherwise we'll forget yeah okay so do what where uh so in the a
security config uh after the themes will add that new endpoint now run again I mean you can run it again it's not what
we just wrote won't change anything it'll still be a 404 oh right because we haven't we haven't yeah uh all right so
let's uh let's go pass does it matter where we put it I guess we would autoc complete then theme search yeah I'd
probably stick it in the uh I think you I don't know how that happened yeah you can do control shift J um undo didn't do
it all right never mind no it's weird okay it's probably because it's not attached to a I think you you hit it at the at
the wrong time doesn't matter okay okay um response body yeah actually we are going body and yeah let's write the method
this is a void because it's a post right no it's no we're we're we're going to return content right we're GNA return
HTML that will update what looks want so I think we want to call this not select dead but just select theme it's sort of
oh because it's called for each yeah right it's for each individual one right right right and Prem any values or leave
it just straight up yeah we want theme and as name you don't need to specify value it's the only value oh right like we
did in another example yep got it all right and then uh doesn't matter what we return we're going to string all right
that should get the cool what are you thinking um us yeah because we're run out of tabs that's fine right I think I
wonder uh there a way to pin and say keep yeah I think there is a yeah I think when you pin it it automatically moves it
but uh oh to left yeah I think yeah try yeah move it over here and then do pin yeah yeah it does move left that makes
sense totally makes sense to me um so we did we we can Clos J 26 we just did that and now we have to decide what do so
we currently don't display that anywhere so we'll have to figure out what we want to display um but I think we'll need a
new div as the container for that that we can Target so above the I think we can put it above the autocomplete box so
above here okay no sorry above the input sorry yeah uh we'll create a div for um actually we create this as a a UL by
the way if you if you had changed the div to UL it would have changed the closing tag for you automatically oh both of
them oh that's pretty sweet yeah um oh that's cool yeah because it recognizes that that's probably what you want yeah
yeah uh so let's give the UL ID uh let's call it uh what else do we want there we'll also want a uh some HTML s some CSS
just to visualize a little bit better what we're is yes this box here the one that has Dallas and Delhi in it yeah okay
so that's what that that's what the new UL is going to contain correct the UL is the contain uh because these are list
items and then you can just decorate them however you want so it's a bit of it's a bit of semantic uh uh markup because
you could put it just I mean you could put it as a div but it isn't it is a list and it is an unordered list um although
technically it's an ordered list but uh yeah say it's ordered but we don't want the number number well we don't want
other stuff anyway uh so unordered list would would give us bullet points um which uh we could do ordered lists because
technically that's more semantic opinion um so let's add some CSS I think we can go directly to adding a class and we'll
Define the CSS up upstairs as it were uh we can just call it selected use control W to do that another Y and so what we
want for this uh you don't want new lines or you know style and say none so that'll turn off uh the list style options
uh let's turn off margin so let's set margin to zero and want not sure what the padding we want uh we want this to grid
so we're not exactly copying the Styles because I don't like some of the way whoever did this did some of the styling
you want display colon Flex uh it uh if we want to sort of preview it we can scroll down and and manually add some some
list items to35 yeah let's just create a couple list preview good enough we'll we'll have to style the individual list
items um I we'll right uh so you don't need to do that because what we're going to do is we're going to style all list
items inside of we're going to let CSS Cascade for US ah so we'll do it at this level or within this class yeah yeah so
we want is um uh no no so it's not inside this it's going to be another CSS box and then uh a greater than sign this
around it really I've never seen and then uh and then Li so what this says is this style that we're about to establish
is for list items contained within selected themes box and why does the um help do the greater less than and greater
than uh that less than greater than is is not syntax it's just saying that this is It's way of indicating these are HTML
things options I see gotcha so it's saying for any Lis contained within selected theme box yes the cascading part right
oh so uh let's do um let's do some some uh uh want yeah let's let's let's style it the way that that they styled it um I
think it's a reasonable Style mean here to um sort of in the middle this one yeah that one they don't there oh that's
interesting uh why would that am I wrong in the in the containment well let's um let's grab um we grab all of it then we
can chop out what we don't want yeah let's yeah let's grab all of it uh I don't think I want the font size ear uh I'll
get to this question in a minute Charles welcome so um why does the preview now before it was showing an a I know
sometimes it's like it it doesn't split at the screens it it does weird stuff I don't know why uh that's I wish it was
on the left left aligned that Gap in here is confusing to me oh where is that Gap coming from that's weird oh I wonder
if that's the internal padding of the unordered list yes that's probably it so let's set the zero let's try that so you
can just hit uh controls that was it there we go yeah yeah because when you do a an unordered list the list items are
indented uh have a default padding on their left right shows is indented yes yeah yeah yeah uh you would have think of
list style none would have well it it's that that says what you want to show before each one but even the list style
thing itself is indented um then there's padding around the the list style item yeah makes sense um uh I presume we'll
punt on adding the X for removing yeah because that's going to be stuff around how do we delete um so we'll get to that
when we get to the delete functionality all right uh that's close now do we get rid of these hardcoded uh yeah since we
since we now selector I'm just looking at at the um my understanding of of not having the is I'm I'm not sure but you
can also say Li you can put the LI in front so you can say Li do selected themes box like that yeah and so that says uh
all Li elements with that class um and I think that's pretty much equivalent to having an Li uh as as a space Oh okay so
Charles says uh only first children so the um the gr L sign means only the immediate child child apply it to if it
happen to' be further nesting then you would not apply it to that okay um for us I think that's for us we're only gonna
have one level deep so I think that's fine okay so leaving it as is is fine or go back to the greater then uh no we can
we can leave it as is um I'm just looking at like uh that's uh okay so technically the greater than sign is referred to
as combinator um so as as Charles mentioned that that means only the immediate child uh not to be confused with uh and
so what we're doing is is what's called The Descendant combinator oh actually doesn't really work uh so dot yeah so
let's put the Li s huh um wait why you say it's not working we have a list item of cats yeah but it would looked
different before it had all of these it had was like gray uh but you lost the dot that's why at the front ah go yeah so
so the dot says this is a class um uh without anything it's basically some kind of element so you basically have and you
can actually Define your own elements in in modern HTML browsers so now we can get rid of the um yeah now you can get
rid of second duplicate or dummy hey okay yeah so that that's yeah so we're we're we're what we want thanks Charles um
so in terms of site mesh I've never used site mesh is it still maintained uh because I remember site set mesh is is
pretty I guess it's still maintained for for templates these days what I'm looking for is um that it does less rather
than more uh so I want like super minimal compilable testable stuff uh I'll take another look at site mesh I haven't
looked at it in in since it was like site mesh one um but uh my my tendency these days is is most of them are just kind
to do much more than I want and so it's a level of sort of coupling that that I'm but I'll take I'll take another look I
actually while um with time Leaf can you make it work on HTML pag I'm not sure what you mean time lift is HTML Pages
which is uh so we've got our Target is our selected themes box um and yeah I think now we can we can drive our test so
what we want is uh we can now drop down to to our IO free test this one no no control out shift T right yeah yeah
navigate Go to No Worries Charles yeah and and that's one of the things I really like about time Leaf uh is that it is
an HTML it is an HTML page so there are other more modern ones the so there's jte and there's the a mustache version of
a Java version of the mustache I think it's the Jasio um the problem I have with those is the problem I have with jsps
is that you you basically are it makes it two easy to write code and my current way of going is I want to have zero
decision logic and therefore zero code in my templates which is why I think most of the templating systems do too much
uh especially if especially doing HTM X all right um we want a test for our selected themes that basically selects
themes so I think those are against the auto complete compl themes this this the news I think this is different this is
uh submitting this is more about submitting the auto complete would it be another nested test class or just start at the
base level for now uh let's start at the base level and see where we go end where's nested there it is okay oh I was
going to say put it after that but before it makes oh at the end end well before it actually makes more sense because
you do this before you do the right uh I'm tempted to say actually and so this is uh I don't know something about
selected I'm losing yeah sure actually what happens if I do no BR Alto yes Alto okay do you want to typo typo in the
class name no I think them no selected them yeah we selected them all right uh so do where's our endpoint here selected
themes for a single theme so it's the LI right and we want it to to to uh post I think we'll do it uh uh an out of band
swap for for this so yeah so we want what so post of the theme returns HTML with saying how can we and I feel like I
want to I feel like we also want to say something about uh with no themes selected oh do the zero case first well there
is no zero case but want to make it clear that we're doing see so it's sort of the you know it's sort of the given no
selected themes when we select a theme then we expect the HTML do you want to do a given to have that selected theme
naming no I don't I'm just sort of thinking out loud what the whole thing is um so what we want to return is uh uh HTML
for selected theme returned something like that HTML for selected theme when theme is posted or when yeah when posted do
we want to move some of the name up into the class name I don't know yet too early to we I don't yeah until unless we
write another test I don't know what what what the common stuff will be true it likely will be HTML with or HTML for or
um that would probably be my test so what are we testing we're Searcher and call theme search on it can ER n service St
theme finder themes way we don't even care about the selecting yeah so we kind of well we don't care about the existing
themes just yet but I think we will um stick with that um Factory method yeah okay so so it would be steal these two and
then I'll change that one in a second why are you stealing the autocomplete I'm going to change the method name oh this
sure but then you have to also change the variable yeah didn't buy as much okay yeah that's why I was wondering why you
were copying because it's like I'm going to copy it and then okay so this takes uh theme so it should themes and yeah
and so this is going to HTML y because that's what we're going to get back as HTML right and so we can assert that the
HTML that's funny um not even close actually was I got the Halloween right we got the Halloween right but nothing else
uh so what do we want the HTML to be we want to do the LI right um was there more than that we actually deleted it didn'
t we so we don't um it was a straight it was just Li right for now there will be other stuff but for now that's that's
all we need now it got it yes thank you uh so HTML for select the theme return theme is posted so we post that theme and
that should be the HTML we get uh oh we are going to need additional stuff because we're going to need to do an at
Advance swap Target do we need that for this test or for the next test um we need that for this test because this is
what we want the HTML to be uh because there's nothing else that's going to force us to create the out ofand swap Target
okay I've not done autoband swap so you'll have to walk me through that all right so what we want is um on the LI uh we
want um uh we want HX Das swap d oob quotes uh we probably need to switch to yeah so Al enter yeah Al enter I repl the
text box always is the second to the last option it seems uh and so now we can put the quotes after that uh and that's
going to be uh we're going to Target be want this to be uh where do we want this to be we want when we get another Li
okay so this is this is interesting do we want so we have two choices uh we can have this Li get stuck in at at the end
of the the unordered list so every time you post it'll just stick it at the end um I me so and I I think from a UI You'
put it the front I'd put it the back the new one yeah the new one at the back yeah yeah yeah the OR at the at the
trailing Edge yes yeah know um you so you can do uh you can do before uh before end and so the question is is do we do
we want to just stick in Lis every time we do a post or do we want to re generate all the post which means the server
keep track keeps track of what well the server has to keep track anyway it's just do we sort of how much do we refresh
think I think let's just try before end because if when get to delete we'll be deleting by uh a specific identifier and
we'll have to figure it out then but I think for now we can say before end so literally before yeah literally before end
all one word all lowercase two e like that well yes I know that's what you said just looks funky I don't I don't
disagree it's it's it's uh it's not TMX so what I learned oh is that these are the the values for this come from HTML um
and so there's before end uh after end before and in HTML and all kinds of things those are all from the standard Dom um
we also need to specify uh a Target and what we're going to Target is uh the UN the identifier for the unordered list so
what is that what did we have this want so I think that's what we want yeah so the outof band is saying hey just swap
literally at this Target and nothing else yeah so yeah so it's saying uh and put it before the end of the list of
children of this targeted item I'm pretty sure I guess we'll find out well not for this test this test is just gonna
show their yeah this yeah right right HTML yeah and yes anel we do test everything or at least everything that we think
is not not completely 100% obvious but more way HX is is the prefix yep sorry go ahead oh I just say for um anel uh XYZ
um what was I gonna say yeah it it took me some moving towards testing almost everything which is what we're doing um
and I think part of it is like well how else do you know that it works um and a lot of times for me when we've skipped
testing something like oh this is so obvious this will work and then it doesn't then we don't know why and then we're
going back to writing the test anyways the number of times I've been bit by oh it seems like this is obvious and it'll
just work and it doesn't doesn't have to be that high it could be like 10% of the time and it's but it's still enough to
go you know I'm just going to write tests all the time um because writing tests as you can see doesn't take much time
well this one took time because it's well Arena tests are really easy but but I think the important thing is what took
the time in writing this test wasn't writing those four lines of code right right it was understanding what we wanted to
do right which is something that I think think is not recognized by folks who are not familiar with tdd I think what
what lots of folks think tdd is is somehow um here's a bunch of stuff you need to do here's specifications write a bunch
of tests go do it or even if you do it one test at a time that there's no thought involved you just write stuff it's
like no actually what you do is figure out what it should do in clear enough terms that you could actually then codify
that into a test right so like for example we spent a lot of time figuring out what this should actually be right and I
actually realiz really Ted yeah um and and I got it wrong the HX Target should be ID uh HX ID no no just ID oh really
yeah um the ID becomes the target uh that it that it will that will will modify so either this will work or it'll
replace the UR but I don't think it will replace the UL um I think this will work correctly it's what's really
interesting is is uh whenever I do this I feel the need for like a a not quite a making app but like a a playground um
because one of the things that that that makes this difficult for me is like we're sort of trying to understand two
parts one is what gets sent into the server and the other part is sort of what comes back and and how does that then
change the Dom um and you sort of need a need a playground for that like I want to basically have on on like I imagine a
UI and I'll probably end up creating this is on the on the you know on one side it'll say here's what you're going to
send and submit and then on this side you define what it's going to return and then sort of in the middle it's like and
then here's the result and I think this is this is a huge failure of the HDMX docs to have something like that is it
makes it very difficult to understand which way is going what is going which way and and what happens as a as a result
they have the there's just a lot of either un you know assuming you you know how this should work and basically you're
if you're already familiar with manipulating the Dom through through JavaScript then then this is all like of course
this is the way it works um but for anybody coming from a different language which actually is the target market for htx
uh there's there's still a lot of work to be done I think in terms of documenting it yeah maybe they have the uh what is
it the cursive expertise yeah def definitely cursive expertise cursive knowledge y yep the the the hardest part is often
that first part is is what should it do and then how how do we know it did it yes I 100% clearly agree I think we're
both aka the fast ones right yep because we returning empty string so let's uh let's return the hardcoded y excellent
passing not generalized but passing yeah so let's let's actually try it out because now I want to make sure that we've
got our HX annotations correct so you're saying he and what do you when you say try it out what do you mean I mean run
the application oh run the app okay I like really try it out is there another way to try it out that I'm unfamiliar with
I wasn't sure we're gonna do something with the um uh in the HTML and and mimic it with oh putting an li no again this
is this is the thing this is the issue it's like we need to have the server thing the request response in order to
figure out does this does this work correctly yeah okay let's garbage dump refresh so now we are if I type anything
it'll say Halloween right so uh it won't until you click one options did now The Styling isn't happening yeah the sty
that's what I was we lost the styling uh The Styling does the swapping have something with uh can we go back to the
browser yeah oh sure want me to inspect yeah so let's make it full screen full width yeah otherwise it's gonna be hard
to inspect ah so this was what I was afraid of um so what happened was uh the list item got booted so you can see it's
just strings right there's no Li yeah and so this is uh this is the part that I was I was like wait we actually need a
swap container uh so um what we actually want and by the way I I love this as a demonstration of of why you want to
verify things in in small steps even if they're hardcoded um because if we started generalizing the return string we
would been generalizing the wrong the wrong thing yeah yeah uh so what we actually want is we want that Li to to not be
an Li um or more precisely uh uh here I think it's gonna be easier if I just do it yeah Do It um so what we want is we
want uh so that this so that has a swap Y and then we've got our Li and swap so so that uh so let's run the test so
that'll fail and then we'll copy that into our whoops wrong test well it ran just that for I've lost control go
interesting I've lost my Spinning Wheel on my mouse that stopped working uh I've got disconnected from tup so I'll have
to connect oh okay let me connect you back now oh it died on my side oh interesting all right well let's not worry about
it right now okay so basically we want to make it pass yeah let's make it pass and then we'll TR we'll we'll test out
the app again okay so we want so I wouldn't copy it this way um because it's a text block I test oh man I'm so bummed
the mouse we stop working on my mouse I do a lot of scroll with the most odd hello there we go so I'm gon to grab let's
see this is the why don't you close the test window yeah that could be and then we want the song them song theme searer
on the bottom whoa sorry it's totally up it might think there's a there's a key pressed because when I got disconnected
I was holding down a key so what I tend to do is hit all the meta things that was it yeah that's that nobody ever hit
the key nobody ever released the key and so it must still be pressed even though I'm no longer connected gotcha okay so
the goal is to changed this to be this right up to here uh no so what what I what I would do is use control W to select
the entire text block to there one more the entire text block yes all the way to there yeah okay thing yep boom yep now
it should pass let me go back to IO free yeah all right and let's try the okay garbage can grab that browser window oh
go there we go that yeah why is it doing that I mean that's desired but we didn't do that I'm confused why it's doing
that yeah uh because this box oh the input noit second no that's box so it's triggering on the on the on the change to
the input triggered doing a get I mean our our filtering is not affected by that uh can we do an inspect yeah it was
already there and can we see what's inside that div oh interesting so it's uh uh it's all there oh I know what it is I
know what it is yes and this is another annoying thing that if you don't know you don't know what's going on so what's
happening is the button is doing a post and what HTM X does is it takes the result of the post and replaces it whatever
comes back gets replaced so every time you click string oh but why are we still buttton in the div here uh there's
probably some interaction uh uh sorry because notice that the first button has the word cats in it but none of the other
buttons do buttons are lost the text and that would be displayed is gone is gone because as you as I move it along you
can see it's actually moving yeah the button's still there but there's no longer a label on the button got it because
what was inside the button tag got replaced with an empty okay um so we want is on uh the so let's see where is this
going to be um this is going to be on what's returned no it's going to be on the po um right okay so let's uh let's
change our test we want to add one more uh the test we've been working on yeah uh so want to add one more thing to it uh
at the end of the swap um after the swap you mean sorry uh the tag um what we want is so no at at the open swap tag oh I
see still within it yeah so we want to add uh HX HX D none H Within quot results I think that's what we want okay let's
try it uh let's oh the test is gonna fail sorry let's let's actually put it in in the okay did we blow brass our break I
think we did uh we did yes um how much longer uh were you scheduled 12:30 I can go till okay um do you want to take a
quick break and then pick it up from here that'll be good all right let's do that give our brains a break yeah all right
a all right and uh as a reminder folks in addition to to the book club we've got the Discord where we discuss things
like we do on stream and uh have further conversations about things we we do on the stream and so best way to uh get
involved is go to the Discord so go to ted. Discord um I also do coaching and training so if that's something you're
interested in uh you can contact me you can find out more about me and go to ted. deev about um as mentioned this this
game over here tdd game uh you can go ahead and purchase a copy of that uh on my solo streams I've been working on the
online version of this game and so if you purchase the physical copy at td. cards uh you'll get early access to the
coding all right figure out what yeah so we got the HX swap none on the wrong thing uh so let's fix that um so let's
code uh uh let's run that yeah let's run good okay looking up how how to how to do this no I'm just uh looking at at uh
make sure that I I was going to put this in the right place so what we want HTML uh the the time Leaf templates let's go
to that oh the HTML file got it um and on the unordered list here um no it's the buttons that are pro are the problems
we want to go to the autocomplete box yes and what are we swapping the post uh no it's the button that's the problem
sorry uh let's go back to the song theme Searcher actually it might even be the HTML Transformer let's go to the HTML
Transformer yeah okay so what's happening is the post is being initiated here from the button and so what post says is
whatever I get back from the call I'm going to replace inside the the the element that I'm in so button says post
whatever I get back becomes the content of itself um we don't want that uh so let's let's go to our test actually let's
just make do this before we write before we add it to the test uh so right before um name in in none and let's rerun the
app and try it out and if that works then we'll we'll it and it's this kind of stuff that I want to try and codify in uh
some kind of component Library uh still haven't figured but so now press on one go yeah it's no longer filtering okay
awesome and now we got lots of Halloweens that's a separate that's a that's an expected problem right yay celebrate
let's go celebrate and then later we're going to want to not celebrate sorry ironically later later we're gonna want
want this list to reduce yes uh but we we actually want the entire but also we want the entire button to disappear not
just the the text on the button because the button was still there it's just its text label disappeared was disappearing
yeah yeah which we soften the inspection uh so let's go fix our tests because right now our Test's broken is broken this
is sort of a weird weird sort of the the opposite way of of doing it it's it's our production code it yeah actually I
could grab it here could I yeah could have used that double tap control thing but by the time I got it working right all
right so this should pass and this is now working the way we want it um yeah it's basically the we now add We us so now
um now we need to generalize perhaps what were you thinking yeah it's a good point because we did time because we've
hardcoded the return and that works and that's great uh but now we need to to be a little bit more sophisticated we hard
code the return was it in Searcher yes here must that's this one right there Y and yeah we're only testing it for one so
if we change it two new years it would break so so let's change it to news and have it break we'll generalize that far
and then we'll do the many yeah don't run it yet because you haven't changed the fail yes asterid correct you see a
patch Legacy untested code don't let it grow weeds hey s hey IGI all right uh let's make the test pass so sweet so now
we've got the single yeah cele celebrating that swegi arrived yeah uh so now that works if we pretend that that's the
only one that ever that we ever care about but it works for a single theme it works for it works going from zero to one
right does not work from going from one to two because we will not have the right results well I guess technically it
would work for multiple uh yeah actually that this doesn't work for for many what what doesn't work is the actual search
but the UI and and the fact that that the back end actually does not store the state so that's I think the next thing is
we have to I like because now right it should be clicked not always Halloween right and right it's showing it's
displaying multiple yes the backend doesn't know all of them yet the back end has no idea what you've done yeah it has
it has no memory of what we've done right um so is that the next thing we want to do uh so the endpoint is sending HTML
of selected theme uh we don't we're not we're never selecting more we're never generating HTML from more them mon theme
um so now we need something around is the back end actually having that state is that the next step is it the next step
or should we have it actually initiate the search well I guess we would want it the initiated search to happen after we'
ve selected one or more um uh yeah then that might be the next step is I mean and that's really the only way we can
verify that that it remembers anything is because when we initiate the search it uses what has been selected right so um
yeah I think suggest not sure what's oh it's not a suggestion button it's selecting the search button right before this
is the old text yeah so let's change suggestion yeah but the search button actually appropriate but on top of it you
can't click it until you've selected something I guess you could but I think that's a that's a a Corner case to deal
with that's that's a UI thing um meaning if nothing's been select don't enable the search button yeah exactly I mean we
should do that but I think we can do that after yeah because that's the that's the something like that so I think there'
s a a a an edge transition issue with the with the words you used it's not once at least one theme selected it's when
one or more themes are selected right because once because yeah well it's also when you transition from0 to one it
should be enabled when you disabled is that now correct NE One selected yeah okay so we're going to go work on this one
now yeah just says nothing selected could also mean all themes no because what does that mean I mean I guess you could
but right but we don't want to just do it D we yeah um no I never why would I remove the search button so H removing the
search button I think there's a certain set of folks who like I want to remove things from the UI and make them implicit
like that you have to hit enter or know some magical incantation um I don't like that style I things you're saying so
that mode would be something along the lines of once you selected these two I hit the enter key and it does something
that yeah okay that's a bit obscure yeah I mean enter should work but there should also be a search button that's that's
labeled search that works if you click on it so the idea would be if you hit enter it clicks the button yeah it clicks
the button because the default right where or where the focus is Right would be yeah on the search button so if you hit
enter it would the focus well during the interaction with the screen the focus would be on the this where the input box
right and the idea would be uh so then the I mean it brings up an issue of what if you type in enter now in that input
box that that would to me would would be the keyboard because it would be enter hitting enter where the cursor is right
now is a shortcut to clicking that search button interesting I wouldn't have thought that I would have thought I need to
have the focus and then enter well that would work too but if but if you think about it um that would make sense like
you select it and you hit the the thing after it autocompletes it should should erase the input field right right uh and
actually that's something we we need to make sure we do yeah uh so let's add that to our list we might want to do it
next I'm not sure yeah I think you're probably right I don't want to because it's more fun to do the search but um I
think you're right um so we're saying clear clear when uh when an item has been selected what is actually the name name
input this is what one of my pet peeves is what sui said it's like let's hide stuff because oh we don't want to clutter
the UI and then you only know about it if you happen to hover over the right area terrible apple is notorious for I
think Apple was one of the ones that I first became aware that they were doing that I think it's they're a big fan of
that aren't they yeah CL box when a yep okay so uh how do we do that how do we do y so how do we do that is when we do
the post do we want to use like an htx swap do we want to do a trigger docks so when the button is triggered uh oh we
could do a the let's see the trigger uh trigger filter then I want to do sync feels like we want to do some kind of
event oh or we could just do a TW Target like there's there's a bunch of different ways we could do it we could either
have the front end and HTM X sort of kick off an event that you've clicked the button and then that clears the input
field but I think it's actually better and safer if the back end just clears the input field so that's what we'll do
okay and we G remember to leave time for retro at the end yes uh so we'll give it what 10 minutes and then we'll retro I
would say I would say five minutes okay uh so let's switch back to you give me a second to clear my d uh so let's go
look at so the input type theme query uh that's the name we probably want to too I tells me you want the ID before what
do you want to call it I think we well and thank you that was bugging me yeah me too uh no we don't do dark mode on when
we're pairing because it makes it makes it harder for me to to see for the time boxing talk mode for the time boxing
because uh I have uh redemptions for dark mode for for 10 minutes oh I see but even that would be too long um so what we
want to do is uh when we return uh so let's do this as as a little bit of a spike and then we'll um if we have time
we'll we'll write we'll write a test for it so let's go into our um and what we a no it's not this one it's in the song
theme song theme Searcher when we respond with the the swap uh so we want to add another swap uh tag H sorry swap
element we can swap I just wanted to emphasize the swap yes HTML all lowercase no uh the HT ml is all uppercase oh
really yes okay I know I was surprised to too but that's the standard that's the that's the JavaScript API property
whatever uh so what that's going to do is it's gonna say swap the inner HTML of the thing we're going to Target so the
our our ID is going to and yes astred it is case sensitive which is a separate discussion um and I think that's it so uh
close it close it right away on the same line can we do this no you can't do it self closing I mean I don't think you
can but it's safer it's safer not to yeah yeah it's also I think a little bit more clear so if this works correctly and
we're gonna have to run the application to find out um it should empty out the contents of that if not we'll have to
figure out okay run darn it darn all right well we'll figure that figure that out next time yeah let's do a a commit so
we can well it doesn't work if you do on a chrome why uh so I think we we're we working on the clear input box when them
is commit and push yes okay yeah we haven't run all tests in a little while well they've been running every time we did
a commit oh that's yeah so why don't we create a new file for our our retrospective so I think would use your tool but
you want to use that oh I was just going to have it as a text file I wasn't going to it so for those of you who are uh
who have not been watching my solo stream one of the things I've started doing uh at the end of my streams is doing
another take 10 minutes or so to do a little bit of a retrospective where do you keep them typically at uh at that level
basically yep so I usually do this as markdown so let's I should Mark Mark down extension um how can you change just
refactor F6 oh shift F6 shift F6 I always get yep uh so let's put today's front and a space pound sign it's not a pound
sign it's an Octor go talk to anybody yeah anybody anybody will go what's an Octor right yeah uh so what's what do we
think uh what do we want to know and so what I'm generally thinking about is um things that went well things that didn't
go well things missed M mistakes that maybe we from learned we tab so when I do this uh as markdown I usually uh format
it as like a bulleted list so a blank line above that line and then a a star or an asterisk if you want to be technical
like that yes not OCT star no there's not eight things it's an asterisk that that has too many syllables so it's a start
um I know for me uh doing more spikes with HTM driving would would save nice correction there from time to effort would
save wasted effort or would reduce wasted effort or something like that yeah no point in test driving something that's h
yeah learn about the percent um and I think under HTM X we could certainly sort of some of the the things we learned is
or have forgotten about that I learned and forgot about is um the empty buttons the empty button text because of the HX
swap else what else did we struggle with yeah cuz the button um basically is an HX post and the HX post will take
whatever is returned and put it inside the thing that had the post so with since our buttons had the HX post because we
didn't specify HX swap equals none it took the return returned HTML which was essentially empty and replace empty I add
want finish that sentence you can say because we didn't have HX yeah good what do you call those uh it's sort of a a
stuck key scenario a stuck stuck it's funny it happens to me often enough which is why I you knew pretty quickly
suspected that that was the problem at least I I don't know if it's once a week but often enough I'm like all right let
me tap all my keys because sometimes they get stuck for some reason but you didn't tap all keys I just tapped control
shift alt well it was it was one of the meta keys that would have gotten stuck and so those are the only meta keys that
would right and so I'm not sure which which key was essentially stuck but that was what was preventing yeah the
scrolling and all sorts of other stuff because it s um what else what else uh let's look at uh why don't you do an ALT
nine to bring up our git window so oh yeah so the um the autocomplete uh the the form when we we were discovering the um
the autocomplete post was inside the form so it was submitting the rest of shoes for some reason I have like a fat
finger on the S key and the number of times I I enter a big pile of s's like I'm not paying attention right and my
finger is gotten heavy and the number of times I see a big line of mes on my screen is so frequent pretty funny um what
else anything else I think uh yeah I can't think of anything else yeah I can't either uh I mean one thing that I noticed
that's pretty clear is we we had many fewer commits today yeah yeah that was interesting and I think that's because we
were doing a lot more HTM X stuff so experimenting y I think that's it cool so um and let's let's double check jira that
uh uh that's got it has all of what we want so that's yes we're still working on that what was this about uh so that's
dropping filtering which we could do before the actual search or we could leave where it is um but I'd probably move it
up at least one uppercase well I always do uppercase yeah I don't know why I guess we've been doing a mix or I guess
it's mostly me yeah that's typing yeah it's all you it's all me man I will fix the casing later oh that's uh so yeah so
what's interesting is is one of the ways we can observe that the back end is holding on to the selected items um one way
is you do a search and see if the search is correct uh but probably a more obvious way is um filtering it out of the of
the autocomplete because it the only way it could drop the ones you've already selected is if it knows which ones you've
selected that it right so I feel like we want to do that one before the search makes sense and then this whole multiple
is going to go away well this part yeah but we'll have to we still have to answer the question of what do we do right so
30 oh I moved it up you agreed but you didn't you didn't then move it I moved it too far or not far enough yeah because
see this was on 32 I just moved it up didn't move it up far enough okay now it's good all right I think that's it it uh
because we were trying to fix it and we didn't oh right um although we did do some generalization but we didn't fix the
field right was one big Kaboom well actually I think we should back off of the change we made that had no effect ah so
that would be in the song theme Searcher basically delete line and now let's on uh sure or did you want to amend the
previous one no that's fine okay commit said oh that must have been from the previous committed push yeah because it
hasn't finished yeah actually they by using that line we may have fixed it because we remember we're doing a spike so
there's a test that was checking that HTML and there is a test checking that HTML y yeah now they all passed yep all
right o all right well that's it for for another stream thanks folks for for hanging out and for helping out and for
celebrating our wins appreciate it um I will have a solo stream tomorrow is my current plan uh I also um will reschedule
my askme anything stream uh for probably a week from Friday uh so stay tuned for that as always um join us on the
Discord and uh ask questions there discuss things lots of good discussion going on so join us there and uh otherwise
we'll see you
