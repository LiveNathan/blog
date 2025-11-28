# ＂Song Themes＂ Episode 31： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=Seic6zld9Fs

---

## Transcript

all right hello folks and welcome to episode 31 uh uh a rare Friday stream morning Mike how you doing morning good good
still waking up even though I've been up am sometimes that happens yeah I haven't I haven't had enough coffee yet to
remedy that situation do you know the cartoonist too much coffee man ah rings a bell you know the character is a coffee
cup right with eyes and yeah I'll have to share with you later they started at UC Berkeley they were UC Berkeley student
and then oh okay and places all right um so last time we finished our persistence we got all the database stuff did all
the the FlyAway the schema the testing the um all that all that uh fairly straightforward because we don't really have
much in the way of of data to save but it's our main aggregate the song so we're we're now able to to find it um by
theme and uh so what have we got next I think we were gonna look at adding search to the UI and the homepage right
because we have the the search endpoint working uh we don't have an actual right UI page for it so yeah so let's let's
probably should put some data in there as well in the produ did we put data in the production one or only in no well we
didn't have a production database so um that's something we can also do if we want um I also have the mirror board uh
available for us uh that we can look at when because adding the search page is is uh will not take very long um and we'
ll probably have to figure out what our next what our next big feature is okay sounds good want me to clear the okay and
actually you know what I remember seeing I was just scanning jira and I think uh we can mark this when it's done it was
done a while ago yeah that was had had some overlapping issues exactly so but yeah that's it's nice to yeah and then
custom reducer got what that was about um oh we we may not need to do that um I don't think we I don't think we need
that do we still have that partition buy I forget where we had that because there's um that we've removed right so all
the stuff around uh the searching um I'm not oh so we do that in the in the parser oh there yeah um I think there's a
larger issue and and we will have to decide when we want to sort of take that on is expanding our results class uh to be
a bit more more fluent there is um an open source result for j class uh that I found that was actually pretty pretty
reasonable that we might want to just adopt uh at some point oh that'd be cool um so I would say uh and I think we have
a a jir for that do we have a jir for yeah so that's basically I think 83 is basically it yeah not a great word to
search on uh yes that's true I was like what oh yeah of course that's like that's like calling your programming language
go it's like yeah smart move M Mr search engine or C yeah well that was that was a pre-search engine so I'll I'll give
from that pre internet not even pre web but pre internet so yeah so that's covered by this one so that means I can
probably obsolute the other one or should yeah you can say obsoleted by um need for obsolet by uh using better result
now we decided to punt on these two for now right and so yeah we are here up to jir woohoo so uh what what pages do we
have in our yeah I know what do inbound web adapter uh we've got the result what so that's just a view class for the the
song theme Shure which at some point I think we need to to improve the results page because right now we only so show
the song title right yeah the results Pages yeah we we probably want to do some work there um do we have anything that
responds to the root page or is that just the the static uh coming soon yeah it's in it's in uh um the homepage level
why am I because you're thinking top as in it's a top of the list but top level meaning it's it's uh just above
resources there on the left got it so those three classes homepage controller the config and startup those are in the
base package the top so those are top level oh I see right right right right and they do it after the packages and yeah
I've always I I've always thought that that was wrong um it's like those should be up top because those are in the song
themes package uh but they the way they order things is if you collapse it you really can can sort of tell but also kind
of looks like it's part of domain even though I mean as a quick glance right even there may be some some ways to to
reorder to reorder stuff but that's sort of the default way so I try not to change move away from defaults too much um
so uh where do we want to put um the search page do we want to put that as as the homepage or do we want to have the
else well it depends I mean if we put on the homepage then it's totally publicly a ailable um I feel like we're not
ready for that yet okay um so maybe we do put it at a a hidden or URL that well we'll put under URL that we can protect
yeah yeah um so uh what is the endpoint that we use to submit the search so that's going to adapter that'll be under
yeah song theme Searcher so that uh so we could um I mean this is this is sort of a a UI layout layout question uh we
could have a search bar at the top of the search results page so when you first come in you get the search bar and there
are results then you enter your search and you see the results but you still have the search bar available right to
further refine or whatever yeah or do another search or refine yeah I think that's the way to go okay um then this will
be our endpoint so we've already got that uh and what we'll want to do is um we currently redirect to two different
pages depending on if they're so we can use uh a timely fragment for for the search part so let's take a look at the um
like the yeah either one of those the no results is probably simpler yeah so here there's there's basically nothing um
right though it does show the text temp if nothing's found uh right which I did a little test a few minutes ago which we
probably yeah um I think we should just have a uh you know try your search again or something and you can delete the th
Tech oh that's not where the songs will go well this is the no results page oh this is the no result page duh so I'm not
sure when or why we added that temp but we don't we could just get rid of this yeah entirely and then just put sure um
let's see is there anything else we want uh okay so then uh we so we can either use a a a Time Leaf fragment that then
makes it easy to reuse the search portion of the page into both Pages yeah um although but what would the initial page
the initial one would it be one of these two um that's a good question it would probably be it would probably be a third
one which is just the first time here kind of thing yeah I don't know another option I mean another options we could we
could repurpose this page to uh so it starts out saying no songs found search for a different theme above that might be
a little confusing then right I probably think with like I mean I think we should treat it like you know like if you go
to any search engine the first thing you see is just you know what do you want to search for you know whether whether
it's Google or whatever it's like here's here's the search box um and that's the entry point and then when you search
then uh the search box is at the top I think we should go with what people know copy you know copy ideas reuse ideas
when when they're they're welcome welcome um so let's do that so so let's page where if there's file um I think you can
just I would just copy the current file because it's gonna be very similar yeah it's oops ah nice so we call this one
theme search Point name is that going to be well the endpoint is theme search but the page is doesn't have to be it can
be whatever we want right um maybe we just call it search themes just to make it different well I I wouldn't make it
different just I I would actually call It theme search uh um and the title will just want and our H1 will be and so now
let's let's create what our search form will be okay so what do you want the heading I think we should start off with
just one theme at first okay you know do a one than many kind of approach um all right and so we'll need uh a form okay
uh so you want to get rid of the P we don't need that yeah I'll get uh basically two pieces of information for the form
so what the endpoint tag uh so the method is going to be get method y get uh and then action is is going to be the end
point um and this will want just to to be sure um so put put a a an Octor here or a hash symbol Octor is Octor yes that'
s the technical pound I call it pound Octor that's Octor is the the is the is is a technical term um wow uh and then we'
ll do a th colon action after Octor okay uh and then after that a th did you say service action or action uh just action
okay uh and here we're going to use the Syntax for referencing a URL um which is the at symbol and then open close curly
braces and then inside there um what is the endpoint where was it uh controller no yeah so theme that stick that in
there all right um and then inside the text uh be field uh so we'll we'll just say uh um field uh so what is the what is
the the um what's the parameter name that that expecting requested theme requested that yep y so that's it uh we could
make it larger but I think that's that's probably fine yeah for now yeah deal with styling another time um that's it
that should work so if we so we just need something to serve up this page uh so we want this page to be served up if we
get so if we go back to the Searcher um what we want to do is is the behavior we want is if the requested theme is empty
or null uh then we want to show that page so what should we do next so would this be sort of a um this is before we even
get to this stuff so it would be something along the is blank or is null well you'd probably want to check for null
first um but we're right but but this is implementation detail so we need to write our test first before we do this
right oops do we have so the behavior the behavior we want is on theme search uh that if we give it an empty string we
expect to get back back the correct and we do have a test class yeah which I will move to the hey there 5G technician
yeah so exactly we want to we actually want to handle a situation where uh uh it doesn't exist because that would be the
first time hitting the page and we want to show the initial search screen so yep um we don't want to redirect we just
want to return a specific uh uh view so I would say this is probably like something very close to that first test um but
much easier in fact yeah because a we don't have to create anything right so search like empty search navigates sure go
at this point I think don't care uh well interesting where're creating a song Oh this is the controller yeah we need to
create the controller um but but with no songs yeah uh I mean we can just this was back when we were injecting songs in
through the tests well here we don't care we don't care so we don't need to inject any songs so we can just create the
the song themes controller directly oh right without even having to use that uh actually would so we want to do song we
need to create a song service like we do in 57 but I think uh we can just do that and then just directly pass that into
about so if you want you could you could you could just inline that and delete the yeah be careful you're deleting I
know I deleted the wrong way uh and you also changed it so fix go that's what happens when we do this on our Friday um
so why don't you in in line the call to create song themes yeah uh and I'd probably inline uh the the concurrent model
into the parameter because we don't care about that either yeah do we even care this is a we inline this one as well I
think that's too chatty um yeah uh and then we want probably a space before 21 because that's the that's the action
we're doing right um and now we can assert on that who yes Full Line Auto completion um close so 5G technician asks uh
do we think it's worth it to test the rendered HTML um in this case no because it is literally returning an HTML page
that has like 10 lines of HTML um at some point when we have more complex HTML we we might want to do that but this is
one of those where the return on investment of setting it up so we can use something like HTML unit or playright um
vastly exceeds the the the return because we can easily examine complicated all right so um no slash uh I'm going to be
pedantic and ask you to swap the test to the top and the bottom because you got the the test class at the bottom and uh
um test class you have song theme Searcher test in the bottom Pane and I'd like it to be in the top pane oh I've got him
oh I did get him backwards wait a second yeah Bottom's yeah uh so what's our uh what's our prediction this should fail
and how should it fail ah so what are we gonna get instead yeah let's see if we we will get the theme search result
theme search no results because it's empty we're passing that's what I think okay I I think that or yeah I don't think
we'll get an error or anything so I think uh I agree think did the whole IO free or uh yeah I free all right no results
excellent as predicted all right uh let's fix it now this one we're checking the test is looking okay fine is that what
it suggested yeah no well I mean yes technically that's what we want but uh you'd rather do the uh I'd rather do the is
I always forget the difference between is empty and blank um I do too so what you can do is is hit uh control q q yeah
um so basically if it's has uh White space that's considered blank so if it has basically non-meaningful characters so I
think blank is is actually more appropriate but our test is only testing for empty right so we'll start off with and see
it does when you say will'll see I'm like oh you see something I don't no I mean that one really was a will see no that
was like yeah we'll see um so now should we crank rank up this test and or have a for so this one actually is empty we
have another test called blank search navigates the search home I guess we could start parameterizing the test if you
wanted to do that um I would say let's parameterize the test yeah yeah actually you replace that don't you uh I always
forget that was my memory looks like yeah um and for this one we probably want to forget um in 511 that's coming out
soon there's a a field source that would make this a bit easier uh but um I think I think we should just use the CSV
source which is probably what we use elsewhere well here we had value Source oh right we're not we're not uh passing in
we're always comparing against the same thing in terms of the assertion so value source is what we want yeah I was I was
thinking CSV Source because we want it in in and out to test against but actually the out is always the same right so
that's perfect yeah and do we need the pars uh not if there are no parameters we don't need the parets okay and so then
this would be blank second one sorry first one's empty second one's blank and then third one would be null well let's
just crank it up one at a time well so 5G technician asks can spring ever give us null I don't believe it ever does um I
believe it will always give you uh an object that object may be empty um but I don't I don't believe it will ever give
it will ever bind uh uh something that is null does it throw an exception for spring or does it well since we said
string since by default this request pram is not required you can actually say required equals true and then I don't
know what it does uh but since we don't say that um if it doesn't find it will it will I believe will give you an empty
string um we can try it if if you want to do that before we we finish writing the test we can go ahead and run the
application and see what happens if we hit that endpoint without anything so let's do that let's let's okay let's see
because I was looking at the spring oh Docker your Docker demon is not running no should add that to your checklist I a
excellent do okay so that's so now we we rerun this should be successful okay okay and then we're search with no
parameters with no parameters so like with the question or mark oh it's automatically required oh then we want optional
equals false so there we go that's what happens uh it basically um fails to bind it so uh let's add in I'm glad we did
this yeah uh because I for some reason I thought required was optional was was uh the default so uh inside of request
pram um put a comma and we're going to say something I don't know ask auto complete see if it's if it suggests anything
where is it control space yeah so we want require oh we want required equals false and if we do that um then we can say
the default is empty string um but let's try it with just this I don't know what the default would be um is it going to
give us null or is it going to give us an empty string so let's try it now okay so we're going to restart the um yeah
yep this interesting all right so I guess it does return null well color color me you're wrong this is why I don't rely
on on for this kind of stuff where I just don't do it very often it's good not to rely on memory um so so in this case
uh we we never want null so we can basically say um default value equals empty string and then we don't have to deal
cool so I guess uh spring mbc's viewpoint on this is if you specify request Prem that is optional then I guess it can be
null to indicate that it wasn't there at all um I think for what are called Model values where you're binding it to an
object right a dto as opposed to a direct primitive um the object itself I think will be created but but its contents
will will be null but we don't need to worry about that so okay so that's what we want um and this this is the case
where if we we could have written uh a spring MVC test to test what happens if you don't pass in a parameter um but we
verified it manually and then so uh yeah so we don't need null we just need to have a a space in that will we change
this name to yes so now it's parameterized to do empty and something with a blank now this will fail because we only
coded for empty correct and I should stop the server we're not using it those and it failed as we expected well I didn't
actually say which what was the um what the string was expected so I didn't fully predict that's right yeah uh the only
downside is um the display value for the value source is kind of not not terribly helpful so you noticed when it was
running we knew that that that's how it execution like looking at this without have without going to the test there's no
way to tell why what what exactly failed because left side we see request to theme equals but since it's a space we
space is there any techniques for fixing that fixing it from the perspective of making it more useful visually I think
with uh sorry not in the assert um well we could do that but I think we can also in the dis in The annotation on the
test itself we oh no actually it's a parameter to parameterized test so never mind about the display annotation oh here
yeah one if you hit uh control Q gotta get the cursor on the um actually no what I want you to do parameters uh which is
control quotes um so this is uh basically each the parameter becomes the curly zero curly and so we can put that in
double quotes like that yeah that'll give us the value but that's by itself is not very useful so let's surround it by
by double quotes we need to do you'll need to escape it that like that um and we probably want to say something more
because otherwise we'll just have a display name that is yes much better where is it where are you seeing it um in the
test names on the left oh on the left I'm looking over on the right hand side ah yeah because what we've done is we've
we've overridden the default name that gets generated for parameterized technique all right so uh We've improved our
test failure output so it's easier pass oh wait second was it no we don't need to we're not handling no we're just
handling blank right we already handled that yeah so it would be this well blank is a super set of of empty oh so if you
okay right because blank checks for empty and basically you can think about blank is doing a trim remove remove white
space before it does is empty interesting that for the passing test it's not parameters uh that's a different test so if
we want to do the same thing display name wise we can go and copy that uh to to that test so that that one um so you're
not in the right test I know I'm getting this here so we just need this part uh no no no this part right and then the
other one was song test I believe parameterized that was this one so we change it to that and the parameter in this case
is not requested theme yeah because we're using attribute for sort of all three right all three optional pieces or all
three required pieces yeah right so maybe we should change it to attribute interesting what did I miss because that's a
different you you modified not the test wrong test I mean that's good we should probably do that in general um but that'
s not the test you're seeing yeah so I find oh there's you wna that you so there it did work it picks it for that one
yeah um should we rename while we're here attribute to required attribute or should not be empty nor blank well the
require doesn't really matter the test is testing that there are missing song attributes um I think it's fine okay and
let's me see if my buffer got it yep now this one his song title should not be empty or blank and it would be artist
well that's not what the test method says so I'm title oops my brain today tit there should not be empty nor one that's
this one okay so that one's working so the remaining one is the artist should not be yeah by the way you can hit F4 to
jump from the test uh that you here yeah so if you hit F4 it jumps right to that test it's funny when it's a failing
test you can double click on the name well you can't double click on a on parameterized test the at this level but I
would think you could double click at this point here no because if you double click there what happens nothing doesn't
go anywhere yeah opens and cl thee node right that's why that's why I don't double click because F4 will always work F4
I want to write down excellent point uh jump to test from test run F4 it's funny that that keystroke is is is the the
one that's noted for Windows Linux um Mac there's a separate keystroke but actually have4 on the Mac still works really
yeah so it's it's command down uh on the Mac um but also F4 works as well on on both platforms so F4 and is that a
platform thing or is it intellig specific um no it's intellig specific got it yeah now all of these have that nice yep
great annotation cool all right yes um navigate search guess we would call it requested blank is empty or blank plus uh
improved test output for some parameterized uh so let's try it our test pass okay I'm gonna close some of these windows
kind one we'll just refresh um can you how do you do um a blank or a space well I don't know why why you're doing that
just type A Space in in the true so basically it it came back to this page right so note that it put a plus there
because a plus is the URL encoded version of a space of a space that's what I was noticing so if you put two spaces in
what yep you tell I used to be a C++ programmer so uh I don't know about you but it feels like we're missing a button
like yes enter enter worked um because it doesn't submit on the form when you hit enter uh but it'd be nice I think it
might be comforting to people submit and then you can close the the element and now what do you want the button to say
um yes enter what are the what is I would just I would just say search oh button weird there it is ah there it is it was
like a hiccup of some sort uh you have to explicitly save the file for it to update the preview that's what it was cool
should we commit that just to or just move on to the next task um is there anything else we want to do page I mean we
could put a little placeholder inside the text box we could make the the text box bigger but I think it's probably fine
for now yeah you say placeholder like sort of like a a grade out text yeah like saying put your yep but I think that's
probably pretty obvious uh no they just have a little um um magnifying glass icon to the left yeah um uh how about we
add some songs and BG s yeah yeah oh going to ask for my kind login go take care of that oh and we probably want to
protect is you said we want to protect our our search page so probably need to go into that okay I'm back to song
importer so this is going to go into your local database so put some real stuff in there okay let's see is this a legit
let me just grab oh I know what the problem is I forgot to grab the header column so hold on a second um can we look at
this this output here yeah so can you scroll this not so helpful I thought we had I don't recall us working on failure
output if the header row is missing I mean as far as the UI perspective well maybe we didn't um so you forgot the heter
row yeah so really should just have one message that says header row missing yes I think that that would be a good idea
so what's going on that path before we okay oh there we are uh I think we can though well we added the search page we
haven't tested that it works yet have we um we just said that it works from a sense of giving it a blank for a space
well I'm personally confident that it works but uh okay if you want to actually do a real import and try it out I'm fine
with that one second I got an incoming call that might be okay one for so as a a side note um note that we discovered
something by using the application that we didn't realize before uh you will never know everything that you need to know
upfront and this is why when you're doing projects to learn um you want to make them something that you're going to use
sort of for real because that will guide you to using it for real and wanting it wanting the behavior to to be different
so here's a case where we didn't think about that scenario where we forget you know we we check for it we make sure we
don't import stuff that doesn't have header columns um but we didn't really establish what we wanted if the header row
is missing and so this is a case where if you're just writing stuff following tutorial or maybe creating an application
that you don't really care about you're not going to really use it and then you're not going to encounter these kinds of
situations that will then say Oh I now need to do this because this is what happens in real life this is what happen
happens in real software development you discover things by creating functionality you create functionality you discover
things that it doesn't do or interactions with existing or other functionality that is something that you may or may not
want um and so this is why I always encourage folks when they're learning to work on projects that will be used whether
it's just by you personally or by someone CL to you uh where you'll get feedback because if you don't get that feedback
you'll never encounter these things and you'll just sort of you know this is where tutorials sort of guide you along
this um perfect path but that's not software development software development is you trip over things you bump into
things you you find that this other way is better um and that's software development uh and and that's what what makes
software development so so difficult hey suiga and yes absolutely um real software development is not just learning like
how to code it's learning what is needed it's learning uh about options it's learning about um things that you thought
would work well that turned out not to work well or vice versa something that you thought ah that that may not you know
that may be a simple way to deal with this but oh look it's good enough uh and so really software development done well
is all about learning um learning about the the thing you're building uh and and these are things that you know disco
and and I almost like the term discover in in in some ways because you discover things before yeah I think most software
developers enjoy learning um sometimes that learning is like oh crap this doesn't do at all what I thought well now I
know like for example the request pram uh by default is is not optional and if you make it optional it is null uh I will
probably forget that again for next time because I just don't do that very often um but yeah um not all the learning is
is is positive but uh but yeah not not so you know this was a a a debate we were having uh in our um book club around
like not all developers are interested in learning they're just interested in doing um and that's fine they're going to
be folks like that uh and there you know you're you're not going to change them um but they're going to uh fall behind
and they're going to potentially CA cause some issues um which is why when I'm interviewing uh one of the things I I'm
really looking for are people who are who are who are curious who who want who want to learn um but not necessarily
learning to the exclusion of doing right so there there yeah and you know and and that's fine there's there's always
going to you know sort of be a need for people who who get stuff done they may not be interested in in learning the
latest and greatest or or you know but I think there's a difference between learning about new techniques in coding and
learning about the product that you're building um I think it's actually very important uh most software developers I
think are are mostly seem to be interested in in the the coding aspect this is why we have an infinite number of
JavaScript Frameworks um and less so in in the the domain of the product that that they're building and I think that
that uh to be the most effective software developer right because remember our job is not to write code our job is to
solve problems um and we don't get to define the problem usually the problem is handed to us sometimes the solution is
handed to us which isn't great either um but uh our job is to solve the problem it might be with code but it might also
be with not code um it might be suggesting we can use the existing thing in a in a different way uh since is around the
time that we take a break anyway um and uh while Mike is is busy on on an important thing uh now and so we'll uh we'll
see you shortly a he uh sort of taking a a Break um having a set time to take a break I think it's really important uh
because I know that I have a tendency see uh especially when I stream to just go on for like hours and hours uh and I
think it's really important to to take breaks um give your brain a break give your body a Break um I know sitting for a
while it's like it's comfortable when I'm sitting and then I stand up and I go like oh ouch oh ow I need to stretch um
so take breaks folks take them at least once an hour if not twice an hour uh one other sorry keep going um yeah take
breaks another benefit beside just giving your body a second to chill almost every time I take a break I didn't this
time because I was on the phone um but almost every time I take a break I think of something that I hadn't thought of
either if I'm problem solving a new approach or like wait a second we're in the weeds maybe we should step back and do
blah blah blah Y and so it actually is don't feel like you're slacking or not working right yes exactly yeah um yeah and
that's why I say you know give your give your brain a Break um give your brain a break from from actively working uh
it'll it'll often um yeah invariably you you come back from a break and it's like oh yeah we do this instead or oh this
is the way we should do it or oh you know like like Mike says like we've been doing this for a while how about we back
up and and try something else and it's it's very much the N you know sort of the nature is like you keep sort of
pressing and pressing and sometimes you just got to let go for a bit and then uh yeah yeah yeah my my watch reminds me
only only every hour um but when I'm doing uh usually if I'm doing doing work and I'm not streaming um I've got my PO
Pomodoro timers so every 25 minutes I'm break yes if if if uh so many problems are definitely solved you know in the
shower or when you're doing something that is not requiring you to do much thinking and sort of let your mind wander um
yeah another advantage of working from home is you can take a shower for for lunch it's like oh this I've come up with a
solution that will save us time or or fix this problem y or walk around the yeah okay we something and I had to peel off
where were we uh we were we you were not satisfied with you were not convinced that the search page works so let's do an
actual import uh a work import um and then try it page this time with the header row oh nope that doesn't look right
either nope it didn't but import it see what happens okay we do let me just finish that one will should give you should
give us yeah missing missing so this time it's not missing the header row but it is missing required columns um and
that's why I thought we' fix that that it would only do that once once but clearly we we've we've missed something so
here in theory this should be a clean import nope what did I miss this time you again really pushing and testing the yep
artist that's the problem when the spreadsheet is wider 2 this one should work yeah that's what you said the last two
times I know all right so where it redirects to is probably not where we want it to redirect to yeah um but otherwise
it's it's likely the import worked um so let's let's add another redirect okay be a bit more explicit because fix
doesn't tell us what yeah uh we can say redirect to import currently goes to slash but we probably want it to so
something like you know 25 row 25 songs imported cool all and Don't Fear the Reaper I think it's two different so do we
want to fix the view page to show more than just titles do we want to fix that now yeah I mean there's so many things we
got to fix now it's um but yeah let's get the artist in there because this you might think it's a duplicate but it's not
yeah so okay so let's go back to the view but I think we can check off that the search page to UI uh the search page
does work so I think we can actually check that off let's get credit where where credit's due yep yep and play artists
um I guess artist and well we haven't no we could do release title release type and notes we'll have to wait for scoping
well whatever the required columns are we can certainly display those right or required is what artist song theme so to
add it to be required it would just be artist okay yeah I mean do we want to show the themes as well Oh you mean other
themes for that song If there's multiple themes or you saying show the theme that we just searched uh show basically all
of the themes for that song whether it's just the one or all of them so play artist that's that's a product question
song title I know I'm picking out that I mean artist song title I would say I would like this show release title even um
yeah it could be interesting right to see oh what other themes is it connected to yeah decided all right uh so which one
of these do we want to do first I think let's do the artist theme one because that's yeah the current one in our that
sounds good memory buffer and then we'll decide which of these other two do next at that point all right so let's uh
let's go to the to the class responsible There You Go song view test or the song well the song view is the thing
responsible so going to the test step so there are two parts to this um and this is where uh goes back to do we want to
test the HTML um because we can right now if we add stuff to song view it doesn't mean it's going to get displayed
because our uh time LEF template if we look at that doesn't I don't think show anything other than um release yeah now
testing UI I always feel is um doesn't yeah so the sort of again the way I look at it is how easy you know uh how easy
is it to verify manually that we've got the right thing um and I think this is right now it's pretty easy pretty easy um
but I do do uh even if I'm not going to write a test even if I'm going to test this manual I still want to start here
because I want to make sure I don't forget about it so I start here sort of at the outside edge of it this is the most
outside edge of the system because this the HTML oh interesting so you wouldn't start from the T song view test you
would start here no and there are two reasons one is to make sure I don't forget but also two uh often this will then
Define help us Define what we want our view model to look like here it's pretty straightforward but you know what's the
capitalization of release title and and those kinds of things um since we Define it here uh then we know what it'll be
when we write the test and I think this is an important aspect is it's very easy to jump into the the sort of test you
know test at the at the view model but if you then do that and then go back to your template and you realize oh actually
it needs to be a different name or a different structure then you have to go back so this is very much outside what is
strong view oh it's a record I see yes and so that made it easy for us to to do uh and so we can um so let's uh let's
let's change our do well I think we probably want to go to a table layout I don't think we want graph I'm not a fan of
table views frankly um oh okay well then you tell me what you want it to look like yeah it's I I mean they're fine
because in spreadsheets but I find them hard to read I actually kind of prefer things to look kind of like this all
right you're the boss um so in which case if we go back to has results so this would be for each basically so if you
want basically one big concatenated string um then what I would say and this is this goes against what I what probably
most people would do uh what most people would do is is create um is Du to the concatenation here in the template and
I'm going to say no to me the temple job is pretty much play what it's handed and don't manipulate it in any way yeah
make the template as dumb as possible and and really super dumb um and I've been this is this has been something that
that has shifted for me over the past year um and very much influenced by by rest and HTM X and things like that is um I
want my templates to be the most most dumbest thing and in fact so dumb that uh it would be easy to actually replace the
template with a simpler technology um but I haven't found one that's that's any better um there are some like jte but
then they uh don't result in in what are called natural templates right so one of the nice things about time Leaf was we
could preview this template because it's just HTML um jte adds a bunch of stuff just like JSP did that is not HTML and
therefore can't be previewed but I'd actually like a a slim down time Leaf which does what time Leaf does for things
like iteration um but doesn't allow you to do things like concatenation or if blocks uh or things like that because I
think those those are very dangerous um because it leads that it's a very slippery slope down to right logic in yeah I
mean there's gooey logic but like can we get away with even even that so um I'm gonna throw a um monkey wrench into that
approach one I agree with that approach um but it gets interesting is what if I want that to be font and that's a that's
a good question because we would then have to decide who's responsible for that um in that case since uh that really is
a formatting visual display then that is something i' I'd put in the template and so then i' I'd keep them separate um
so if that's at all possible uh in terms of likelihood um then let's let's put them as as separate and then create uh
spans to to for for each segment got it so still be on inside of a a p a paragraph um but we'll use spans for each in a
sense yeah for each element yeah yeah each each chunk whatever term you want to use so let's do that okay so if we're
gonna drive it from the test be actually how do you do with this so what I what I tend to do is is do the HTML first
ignoring forgetting span what do you want inside that span and then do we do the space hyphen space independent of the
span I guess it would have to be yes it would have to be be something like that so it's GNA take well white space will
always get eliminated right so wh space will be collapsed do I to do this uh no it'll put white space but it won't
collapse it completely but it'll collapse extra uh White space extra okay um nbsp is basically I want a no break space
but I don't think that's gonna matter here yeah okay so we got and will it put a space if I do this something like that
all right and then let's get rid of the other stuff that's used so let's preview that does that and so now what we can
do is we can now start putting in uh th texts um so you can get rid of the one from the P because we're gonna put it uh
somewhere else so I could do this careful here careful oh I see what I did I wonder if I control W graph it does and
then basically the same thing for all of them it's just going to be a different uh right property or method technically
yeah so this would be artist and so this is where what we put here drives right what we're going to do how we're going
to modify Our Song view now this part are we GNA have to do another uh th each we could or we could or we could assume
that the view is gonna The View class is going to do that Ah that's cool because that one we don't need I would probably
say let the let the view the song view class figure out be y um if that's the case then that means I do or would we um
yeah we'll let the square brackets be done by the view as right okay cool let's preview it I guess did you want by the
way did you want to bold one of these did you want to change formatting for any of these yeah I definitely want to bold
the first one italic second everything else normal um so then let's let's do that okay would we want to do the CSS
approach or just do inline um within the span uh I tend to use classes uh CSS uh I mean I tend to use Tailwind but we
can do a we can do a style so we wouldn't do a class because you don't have any classes defined right um unless you want
to do that unless you want to I mean how do you want to do it we could do an an inline style here or we could create a
CSS section at the top I guess it start with inline style now and then as it starts to grow we'll start so let's to CSS
yeah let's do a and what did you want artist to be bold what is the uh it's font weight font weight that's it wow
there's a lot yeah that's why I usually type DW and let bold oh interesting so did you want this what did you want this
oh that's not a weight yeah emphasis ah there you go y cool and then everything else just de now you can preview that
and see if it want cool all right so now we know what we need um and we know the method literally the the components of
the record that we need so now uh now we can test drive VI so now we're going to have to change parameters yes is that
well I guess we'll see where it is yeah so that's so you got the one that takes the full okay um but that also includes
release type so that might have too many uh well we could ignore this one right yes um oh interesting goes up to theme
too this time um now we could say well now we're going to have another variant that means we should go to a test data
Builder on the other hand thongs are really trivial to instantiate and so the fact that we're using a song Factory it
doesn't re the only thing it really helps with uh is we don't have to create a list of themes um so I I I probably would
say just instantiate the song directly oh and not use the factory at all well so if we want to use the factory I
probably would convert it to to a test data Builder um I'm I might be let like I might be willing to to abide by
creating one more variant um but we've already got one two three four and now we're going to create a Fifth Fifth the
fifth would be with all the themes well the one you're you're proposing is that we don't have release type so that's the
fifth but if we want multiple themes then that's that's even another variant well I was going to say ignoring on The
View side we could just ignore the release type oh you still have to specify it I see what you're saying good I mean you
know so there's what we could do and there's what we should do um and right I mean you know just because we've got
another variant doesn't mean we yet have to go to test data Builder and so we feel like that's really more work than
then the return on investment then we can just make another another variant it's not like it's hard I guess we could do
a variant that would be so we can do the variant of of exactly what do we want for this test so basically I'm going to
copy this but know that I'm going to be hacking so it would theme list of themes no release type so why a list of themes
to deal with multiple themes but test oh you're saying build theme one theme two three four I I don't know what do you
what were you thinking of of I I don't know what your test needs so I don't know what we should be doing here so you're
you're you're you're going you know inside out as it were got it and I mean and I I I tend to go outside in because I
don't want to build something that is not what I'm going to need if you want a variable number of arguments for themes
we could convert we can accept variable Arguments for themes and then convert that to a list so if you know you're going
to want one or more themes but no release okay so a ver ARS so a version of right so a version of 19 removing removing
relise type and then making it vars at the end right theme one and then possibly more right okay is that still inside
out it is but at least we're we're we're stating what we what we believe we need the danger is is that what we believe
we need is is once we actually write it don't we actually are our belief was wrong wrong so how about we just so do it
from the test side the out yeah so if we do from the test side instantiate the song directly with what we want um then
we can refactor out to what we need right so this will be a new test anyway right well actually no it's the same convert
found songs to song view I think we since we are literally changing what song view is yeah uh this test would is is
gonna need to change this in line so it inlined one because that one calls yeah there we go okay which is we're in Stane
in the song directly yeah which as okay so let me grab some stuff from my and then we would just keep a relevant release
type or Would we not um I would uh sure yeah yeah because we're doing the new song here not a just gonna pop it in the
comment here with that's one get something totally different that has title sure this will work actually this one's even
better oh no I'm not gonna use that one the Ripper and it really is a JY tune it's um kind of almost of a pop bubbly
kind to so this is the setup is now correct manually done but it's correct all right wax actually which of course the
Constructor can't handle and then we talked about doing VAR arcs here uh no this is the song view so this is what we
wanted to produce so that's correct and then we want the themes formatted as as you with yeah all right now this
Constructor now we want to change the signature in this case because we want to be real not yeah so what I do in this
situation is because I'm always nervous of like how many other things am I going to affect by this change you create a
new one um in in this case what I do is uh I I might create a new Constructor but I might just be curious like so you
there three in production code well now the first one is not using the Constructor the second Constructor the second
one's not using the Constructor the third one is using the Constructor um because that's the from method itself right um
so uh that one's not that one isn't that test we're currently working on currently working on this one and that's the
test we're currently working on so uh so I'd probably be comfortable in changing the Constructor and not create a new
one because the only thing so we're in a sense we're we we're protected by the fact that uh all the usages outside of
song view are going through the from static method so we change the Constructor and then we can just change that one
from method and everything else is good got it and what's the difference between the first and second selection so it's
does it add the ones before or after so you can see sort of uh in the first option in the drop down the last three
strings are bold and that's where it's going to add the new parameters so the existing one is the first one and then it
adds them at the end the second option is let's add the new parameters at the beginning and the old one stays at the end
so we want the first one interesting and you you can you you can actually see it in the preview so you can see right now
it's previewing the title is still first and then the and if you select the second option now it says our new options
and then titles at the end actually well I don't like either frankly it it's yeah so if it doesn't matter it doesn't
matter pick one and then we'll we're gonna have to rename and reorder things anyway anyway okay I'll just pick this one
because I know sorry you were gonna say what um so it means though that uh we we might want to move the title to the
beginning before we do this refactoring so that at least that parameter is correct not title artist would be I would no
artist to be first right now you you want artist to be first but right now title is the only one that's available so in
line 20 swap the first two right so now when you do the refactoring at least one of them will be correct so that one
will be correct that would be the one we want okay so take that and now you can go ahead and start um I don't want a
default variable well you do um we're going to replace it anyway but at least it it it means that we won't lose
compilation got it okay so now that's artist themes and then I want to move this one so you said I can do the move up
and down the signature order and at this point and it'll take it uh or should I change signature after we do the um and
also you should not check use any of our because we're specifying the variable to use to get rid of that okay yeah and
then I could do this reorder now to do that yes crossed and we suspected that that that did what's nice is is that it
said this is going to be a problem and it basically fixed it anyway oh what did it do to fix it it converted it from a
method method reference to to a Lambda so I should put in the second set of parameters or the second view all right
second reversed artist title P title yeah I think because we did the reorder at the same time I I was I was worried that
it it wouldn't do it right yeah I was wondering whether we should do one then reorder yeah but the song view is correct
artist title release title themes so I guess we should look at the else that's from that's the one we got to fix yeah
but our test should should now uh fail io3 should fail gloriously though well there's only one test that's testing it
and so it should fail because one of correct so the first one was completely correct which is what I expected because
the hardcoded stuff got moved over into the pr method right um and then the second one the title is correct because
that's the only variable that it's looking at and everything else is wrong because of the map because the map is using
hardcoded strings got it so if we if we replace the hardcoded strings with the variables that should get our so in other
words convert actually I'm this so uh we're going to have to change our uh we're going to have to drop the the map to
song title because we're not right so we just want to drop that drop that all together oh this whole line and now what
we're mapping is song to song view so change title to uhuh and then change song is that just giving him names like this
or is it more this no it's so given a song object how do we get the arest out of it got it given the song object how do
we get the title given the song object how do we get the release title on that last one's going to be tricky um yeah but
not terribly me and is there sort of a no there's not going to be a I mean we could do a a collect the joining but we
should just use the string Joiner okay um so if we wrap uh I don't know if we can do that in one can we do that in one
line uh let's try it so before song themes Joiner um and then the parameters that we want to pass in are not the themes
so we so don't pass that in as the parameter uh let's hold off on adding the parameters just yet um on string Joiner
available uh so it is ADD um okay so we can't use string Joiner in the way that I that I wanted uh is that because the
square brackets on the outside um no it's because there's no one method on string Joiner that takes multiple objects uh
so let's switch over to to to themes uh we'll do a uh a map should we start doing this on its own um actually we don't
even need need to do a map uh after stream then we do uh collect and joining uh what are the parameters to to join
joining okay great so we get this the delimeter our delimeter is what Comm comma space comma space and then uh and then
the prefixes sare whatever yep open Square and then the suffix that's pretty sweet yeah kind of method you'd want for
exactly this situation yeah should we move this to a new line it's getting to be pretty uh well you c yeah you can move
it to a new line like that yeah yeah not the middle of the and if I were gonna do that I might move line good evening
astd welcome hey right do we think this will pass the test maybe I think so it feels like a big step but uh let's let it
rip I think so too yeah we go back to if not the test will tell us right so um let's uh let's run the app and see what
what right so the songs already there so now and I added yeah so we do this one so just re yeah just redo that search
boom so I'm not familiar with uh beautiful souths is that a cover of the the same song yeah I am not familiar with that
cover that's part of the reason I put it in because I know you knew blue Easter cult yeah um so all right there you go
uh let's put um uh well let's commit and then we probably want to update our yeah uh cooking will always win out over
watching a stream absolutely 100% agree uh plus the yes so actually song View and well I would just I mean I would just
say the the results page shows yeah the fact that we use song V to do that as a implementation detail yeah result
displays yes flat made is one word just like roommate which has two M's in it which always annoys me there's a great
band called the flat mates really yeah sort of a all all women power pop from oh interesting I think they're from
Edinburgh they're pretty sure somewhere one word the flatmates yes yes part of the mid1 1980s British Indie pop huh yeah
what's my now now you get me one oh they they uh disbanded it in ' 89 before releasing a proper studio album all right
really all the stuff is like they're all all these stuff are apparently just yeah singles yeah I'll have to check them
out let's see which ah of course gota say band Yes um oh I guess I was wrong they weren't all all women two women
vocalists um yeah Shimmer is great Shimmer's really good um and Heaven Knows another one that rings a bell are they on
band camp so it's easy to listen to uh apparently there's some YouTubes yeah there's some YouTubes for sure um oh band
camp and they're on band camp cool well this might be nope someone else some else Georgia that's a different band yeah I
hate the i i i it's it's it's too bad you can't copyright the the name of a band that would make life so much easier but
I guess yeah that n this is this is Bristol okay we're going on a rabbit hole yes but we're allowed to do that on on on
on this stream because this is all themes cool um jir check or X actually we're close to break time again and we are
close to break time let's decide what to do next first uh oh we wanted to protect right the surch so let's go to our our
config is that uh in kind or no no no that's that's in our uh web config web security config how what are we calling it
again protect what page so that's a top level class and you know where top level classes are now they're not at the top
they are at the bottom they are top level classes but they at the bottom that's the one um so we're currently saying
that theme searches permit all and we're saying or you're saying right now you don't want that so you can basically move
move that to song import if you want that to be authenticated do I but the only way anyone could get there is to know
that it's slash theme hyphen search true security by security is not reliable um since on stream we we've announced it
so right right no I know but I mean it's not like import where people can change the data this is true I'm less
concerned about that one that was my that was my thinking but you're the boss so yeah no I was thinking more just not
put it on the homepage right the homepage right I mean there there's no link to the homeage the H page yeah the homepage
says coming say coming soon and that's it so um I am fine with the obscurity approach okay so only a select few those
who are are paying attention to the stream will know how to how to do a search yeah of course it's not push to
production with a database so it doesn't work anyway but step yeah I mean I don't there's nothing bad you can do by
having it it's more yeah there's no it's not a there there's only a get request so that so there's nothing anybody could
do yeah exactly so I don't think we need to do that yeah yeah um so we got single error message when bul import is
missing and then redirect after import right I think the error message we should tackle next what do you think I think
so too so should we take our break and then tackle that yeah sounds good all right cool so we'll see you after a a all
right and we're back what's funny about that video and and I chose the segments per on purpose is that's um I I I make
my coffee using the pourover method which I just literally did during coffee um if I got more coffee I'd be in big what
did I miss anything uh so even if I don't poish heritance law yes well there's not much API here and again even if uh
you know I mean if you tell people it's fine right now it's not going to work anyway because we haven't pushed we haven'
t set up a database in production anyway so but uh absolutely um if you don't want people to see it secure it yeah don't
um effective yeah something it this a startup or something definitely yeah yes absolutely uh admin admin there actually
is a uh I think it's a law that that's a bill that's being discussed about um there's something some regulation or some
some Bill that's being discussed I think it's more than just routers uh not allowing them to have a default password
because there that's been a vector for lots and lots of security uh problems I I just can't imagine the the customer
support mechanisms for for that you got a router and it has basically a random password and then people are going to
forget it or not understand how but maybe that'll force force the vendors to focus on making security actually easier
instead of just horrible which is how most of them are anyway uh so we said we we're GNA handle jir 102 yes so let's um
let's go figure out what's going on with that because we import iot to remember where that was songs failure message is
additive or it yeah so we're returning it once uh even if we're returning it once per song I thought we would um only
return one we may not be um uh what's the word combining merging the the failure all right Jonas lurk away have a good
rest of your day evening cool so let's I mean what I what I typically do in these scenarios is look at our tests what
are our tests doing right no test test at the top because test drive test drive the code test drive the code it's got
kind of polluted up here no not that either there imin or is it imin you'll have to let me know is it a long eye or a
short eye is it is it an IR Mazin or is it an IM Mazin but hello either way or I'm a s I don't know usernames are hard
um so it's probably uh so what failure modes do we have here song import adds failure messages for failed import well
that one looks let's look at this is a very long complicated test um well if if it's long and complicated that's
checking the original text area got it okay then we're just checking that there's two failure messages we're not
checking the content of them so here it looks like it's saying song do we have a situ do we have um oh the situation
that we encountered which was no header row at all right let's see if we have another test for no header row think we
did because I don't think at this level if we we had very much s in points do you think it might be lower level I guess
we could well the thing is this is the level that we care about because this is what we're observing because this is
what the controller the search Searcher uh UI directly accesses um but I noticed that you said that this was hard to
read and I don't disagree so we might want to First focus hey grome thanks for their driveby have a happy Friday
yourself in case you're by so what makes this this hard to read well it's testing two areas actually and there's just a
lot of lines um need well this name to Mal form song is not so helpful um I was like if we could hide that does that
help us much I'm thinking no so let me let me let me say what what sort of stands out for me as as being hard to read um
I don't think the setup is hard to read uh the direct attributes maybe a little bit but but not much I actually didn't
look at the variable name too hard I just saw it was that and that's what's passed in to the to the handle song import
right um and so I I think that that's actually okay the way it is I think that part that you've highlighted um
especially uh where we have to grab the flash attributes yeah that's a lot of noise that that um I would probably want
to push aside um I also kind of feel like in like 64 um it it would kind of be nicer to have a higher level assert
basically assert that redirects too um might make it a little easier to read but I think the the main culprits for me
are are line 66 and line 69 um those are yeah those are hard to read because of the way we get information out um and
since they have some common ities um could be one helper method yeah although I think need two because they're different
types yeah so let's let's do that let's let's fix our our expression of what we want um the other option is we
completely wrap the assertion and the obtaining of the the contents of The Flash attributes into a single method would
you make it a assert or just a method um for now I would just make it a method in this class uh later on if we find that
we're using a similar thing frequently we might want a specialized asserter for uh for Flash attributes so one option is
make that into a method and then have that method just be called on 67 instead of failure messages that's one option and
then the other option is convert 66 to 68 into a method right like with the name something like aert um number of
failure messages yeah that might that might be taken too far because I think we're also actually GNA want to look at the
the content so I'd probably start with with just um pulling out this that part into into into a method yeah that was my
original Incarnation okay right all right suiga care um extract failure messages just okay and then we would want to
inline that one um what's different um oh I see it's covered uh extract uh original songs well I think it should be
whatever the variable name is right because we're we don't care that that it's under the name tsv songs we care that
it's referring to the original text area content because that's what we're we're saying is that not only you know does
it redirect and we have failures but also the content of the text area is the same right and the advantage of that is
when we inline it that variable name will go away and then we're screwed ex not screwed but we've lost lost that we've
lost that information yes yeah so now when we do inline it's still human readable right yeah I think that's a lot better
and now I'm wondering if we want to extract as a different verb you mean I I think I think reading it now extract is is
Oher that yeah so now so now I think we can take out the word extract because now I think it's uh more meaningful to
when you read it it says when we read it yeah original yeah oops what didn't that like there that's fine did it take
what was that popup I don't know you this you disappeared it yeah let's see what happens if you do it to the other enter
oh it's wanting to rename the the test method the test you mean the pr you're gonna have to expand the dialogue because
I can't see the whole thing this is like a consistent problem with intelligy it's like the dialogues are never wide
enough I don't understand like everybody has 13inch monitors it should scale to like be you know 80% of the width um I
don't understand what it's saying method and it's not a test method it's a private I think intelligent is confused so
just hit ignore well you're gonna have to click okay but I'm not sure yeah I think it's confused because it did the
right thing name yeah the right thing is here and here but I I think it sees it I I don't understand it I think it's it'
s just confused all right so how do so I think now because we've gotten rid of some of the some of the noise so assert
that failure messages has size of two assert that original text array content is equal to yeah I think that's that's
much better okay cool um let's make sure it still talk test takes so long to run to I know oh they're done I barely had
time to sit my coffee yeah I know that's why we want long tests you need more time that's right that's right improved
asserts okay now the original reing we here was not to fix that test or not to make test easier to read but to modify it
right deal with header rows what are the other tests again I just want to quickly see handles null repository okay so
you think just modifying this one or should we have a new one saying something like I feel like we row is there I I I
feel like we should have another test that's dedicated to just what failure messages preference my thinking was below
but it's not a strong preference I don't have it either if I Didu would have done it um okay what do we want to call
this um so how so what would we what how many failure messages would we like one per row right well even though that's
too much if the header's missing so there's to me there's multiple things if there's if the header is missing one
message and done all right so let's let's put some comments so we can have all those all the cases yeah so one is
missing completely missing heter so what were the other scenarios the other scenarios we were row is that what we want
because it could just be for that and say for that row we're missing required column X and Y because it could be the
other the other rows are fine so it would import everything but the problematic rows I don't think we're going to be
able to tell the difference between the first one and the second one so I think oh because what tells us that we're
missing a header row is that it's missing all required column names versus one required column name and I think that
might be hard to detect and I think it sort of doesn't matter I think we're looking at two different I still think it's
two different things though because if you have the required headers but if that cell is missing an entry in a required
column for that row yeah I guess we I guess I I guess I I uh need an example for what you mean by missing required
column okay um so assume the header is correct so this this one is checks the assuming header if header row is correct
then so there might be something like you know the required let's just say it's artist um title what was it theme one
yeah yeah um uh you can just say FU and bar I'll I'll understand bar or actually empty then that row would fail correct
okay agreed um and why I was asking for an example is you said missing required columns that's not a missing column
that's a missing C cell yes yeah that's why I want an example because I didn't think we were talking about the same
thing right we missed yeah um but then there is maybe one B which is missing you know having like title and column so
missing missing literally missing an entire column that is required I think it require get its own number I think
they're the same thing is I think one and two are the same thing really missing required oh because right because then
the required header row I mean having having a header row doesn't it's it's about does it have the required yeah because
what the finds ah head of row it's not like it looks any different from any other row it just happens to have special
words in it yeah yeah exactly you're saying one B but it's not really a separate days test I think so um but you're the
you're the boss so you might want different different I I think if we try it I think we well um I mean let let's let's
actually try it let's go through the UI and say what happens if we have an empty cell what what what error message do we
get it uh I don't think it's still running is it the stop button here oh okay I guess it is still running to as saying
you've got one b and you I think that qualifies as pant of the day award as someone who's pedantic um this is a hard one
I guess this oh yeah me do okay so here's a single row and we're doing two right to prove that two is works so yeah I
would actually minimize minimize the header columns meaning just only to have the required ones just so we can be clear
about what we're testing okay um so let me two this is why is release title required I thought release TI was not
required no it's not okay so so the tabs right so artist song title it's um so let's drop song title but let's make sure
the other one so you should have one tab there Y and then cats should be the theme so one tab yeah um and so now let's
put let's remove green eyes and a tab no leave the tab we want we want the we want the column to exist but be empty but
be empty the cell to be yeah attributes for blank song title so that's the right error message failure that's
interesting so somewhere in our code so we're we're um so looks like we bug yeah so we found a a bug that we need to so
we're not handling uh situation two I thought I we are at the bottommost level right but not we are protecting song
against being to uh I thought we did that too but I guess we didn't all right well tdd does not guarantee you have no
bugs it just guarantees what you think you want what you intended to have you have but we clearly didn't didn't have
that said it was parong uh and then we look at um extract column oh well we're not checking for situation uh H because
we're saying that if the header column's there which it is um then we grab it uh and we never check to see is that cell
empty so we grab the cell it's there and then we return success with an empty cell which is not good so we're not doing
that validation okay well that's a missing missing scenario yeah let's see if we got a test for extract column or or do
we test I guess we could test tight end well so typically what I would do is the same way I would implement this
functionality so we see that it's not there um I would basically start outside in start at the song importer write a
failing test um and then we'll end up having to implement it at this level but hey at least it's good that you know we
protected our our the okay so were there other scenarios that that we need to since we're writing down our scenarios and
we might want to jira I thought we already checked to make sure that there was at least one one for artist one for title
one for theme or is extract column that was just actually one I would say there we can treat artist title and theme one
basically since they're all required I can I think we can treat them the same from the test point of view right because
basically is the columns test yeah no it's only the required because we're allowed to return an empty string for an
optional right but where do we check that it's required uh index of we never check we don't check here if it's required
all we're saying is that there is a colum with this name give me the cell contents we check for the required columns
when we when we analyze the if it even contains that column that log me if you asked for release title and that column's
not there that's not an error right so that's why we have that logic there so what is the definition of is optional but
do we ever check whether something is a required column you say we do it somewhere else yeah so we do that up front
because row up front where when we when we create when we create the column mapper match no that's um no that's
different that's different no when we create the column mapper yeah right there ah here's the required columns yeah we
def right so we Define the required columns if we end up getting to something right so if we extract a column if a
request comes into extract column for let's say artist it's not a header column so we don't find it in 21 it's not an
optional colum so we don't go into 25 26 we end up at column which is why we we I thought we had this differently but
this is why we're getting all those missing required columns when we drop the entire header row because we're actually
not validating that the header row has the minimum required columns in the first place so we're not validating the
header row at all right that's what getting at yeah I thought I thought we were I thought we were doing that at at when
we created the column map or I think we may have maybe in my head planned to do that but we didn't right I mean this was
the hint to me it's like is optional column but there's nothing else columns other than that is optional so right we're
never making sure that the three required columns right and that's and that's why we're in this situation yeah okay I
don't know why my brain spinning with that might be because we've for a while um so a test at this level yeah so we
should do a test where we don't passing ahead a row at all and we expect and we would we desire a single failure message
um then another example where we have some columns for a header row but not all but but we're 1B okay three test yeah I
think I think uh uh I'm gonna I'm gonna add the a for AST well what I think we should do is move this to jira um and
start writing one a and that's probably as far as we want to get because it's really 1 a and 1B are under that J 10 102
yeah I think two is is a separate J yeah that work nope well let's turn them into check um we probably want a few
different yeah I was just going to specify them because they're basically to so you can duplicate 107 um but put uh a
theme for the second one one get the bar all right I was gonna do one right sounds theme like so we want is even though
two technically has two missing cells um we would like to combine that into one one yeah I think that's going to be a
little harder and so we'll have to decide whether that's worth it right um I think ODS of it I think the bigger yeah I
think the the bigger problem is is the tremendous number of error messages which is you know three per row of import uh
all because we left out the header yeah because we should pretty much we shouldn't even be processing anything else
because and that's why I I thought we did this because this makes no sense to doint any further but I guess we didn't
yeah can we look didn't so would we check it at this level we would say after this we'd be like hey is the first row a
legit header row well pretty much line 22 is where we want to do the check um and uh column mapper is responsible for
that right so um yeah we Define them but we don't them yeah we Define them and then we actually parse the column headers
uh but then we don't do anything we don't do any validation right yeah um and so the question is is uh that will have to
answer the Constructor yeah we don't want the yeah so do we have it populate and then we have like a validate method no
that's terrible I I know but I'm like I'm trying to figure out what to deal how to deal with uh so I mean it's it it's
so this is where I I I move to um Factory methods oh factory um because the nice thing about and this is the the this is
why I think like Constructors are are really problematic if if uh if you want to do validation because other than
exception there's no way to signal that it's that it's wrong right um well not there's no way but the other ways are
ugly yeah I mean one way having error object right the old school well that I mean you know like you query the object
and go do you have an error yeah and then it's horrible that yeah that that's not great because now you have an object
that's basically in an invalid state right um and you have to know to check validate first um exactly and yeah yeah I
think Factory is the only way to go I agree and and and it's it's it's fine because um like factories are used for
creating sort of you know complex objects the other option is we pull that behavior out um but then sort of you know and
this is sort of an a cohesion thing like who's responsible for knowing what the required columns are um one could say
that column mapper knows too much like it should just map blindly and not be responsible for checking them right yeah so
basically like hey just map stuff and then somebody else checks to see if if they're required or not however uh I think
this currently feels like it makes more sense because the extract column we want different validation errors depending
on whether it's not true so we've we've sort of given it enough smarts to say these are the required columns so that way
it knows whether you've asked for something or or I think it's it's fine fine the way it the way it is um so why don't
we write uh a failing test and then we'll call it a day sounds good and we'll do it at the song importer test level yep
and we're GNA do onea right I think we're gonna do one a yeah s import fails no well just write this first and errow we
want to mention that it's one failure message yeah so so my tendency these days for naming tests is what's the
expectation message when row and so you were saying you do expectation uh test naming format uh yeah I guess it's
context and there's no action here right because what's the action is we're doing song import except that's the name of
that yeah right and the reason why is is uh I've been starting to to shift towards this is when we were looking for hey
did do we already have a test for this we were looking for our our you know the result we were looking for a result we
were looking for hey when do we get failure messages and if we look at the test names right now that we have if if names
we see that like for the last four the first two words are irrelevant it's always going to be song import and so it
makes it much harder to find we ended up having to to search through the the the ends of the test names instead of the
beginnings right and so this is Benny asks uh you don't like given when then it's for exactly this reason given when
then is a great way to think about the test but it's a terrible test name because I when I've been really trying to be
aware of what happens when I'm looking for tests I'm almost always looking for the then part and the then's at the end
it's really hard to so you're channeling the book club basically where we're about how cognition um yeah works and you'
re optimizing for that yeah in this scenario right right because then it's like hey why aren't we getting a single
failure message oh look there's a test single failure message when well when when that oh well that doesn't cover the
situation that I care about so that we're missing a test um this doesn't always apply uh but it's been working for me so
far when I've been when over the past month or so that it so let's write it and then uh then uh yeah I think we could
just call it missing hetero and I don't even think we need the tsv yeah I was wondering about that I saying header row
should have done F6 on that one or shift away and I've intending to put the opening triple quotes on the same line as
the assignment yeah control shift J would have been your friend there yeah I know that one was not on my radar let me go
back to it control shift J there we go which I want to go to to this one because that's part of the noise of hindsight
so back here so what are we doing for Sears we're checking whether it's redirect yeah so we don't care about the
redirect in this test no we just care about the we just care about the failure so you can copy 65 yeah and you can get
rid of now the variable assignment on 89 because we it contains exactly yeah we want contains exactly um we can start
out with uh a lightweight which is has size uh I meant as the actual assertion Oh I thought you meant a test right
should fail this will fail let's predict how how it will fail uh it'll so I have a number in mind yeah it's a big number
right it's like nine um there's three required no so it's it's it's six right because there are two rows and each one of
them causes three failures right so three * two is six yeah yeah so let's oh ah that's interesting well it's but it's
missing the head oh I know why because it it treats the first uh row as the header ah where's the test here it is so
because it treats the Row the first row as the header uh there's only really one song that it thinks is being sense that
could cause some weird really weird error messages if you happen to have an artist called artist or a song title called
song title yeah um that seems unlikely enough that I'm not going to worry about that um and once we fix this problem
then that will go away as well so all right um should it make this our breadcrumb or did you want to I was gonna say I
think we're make it pass no I think we're we're we're good we can stop here yeah leave leave with a expensive I'm not I'
m not going to trademark predictive test room development I didn't invent it I mean I think I came up with it
independently but I know other people um like I know yep and then we get to say push anyway no that's a whole different
kind of business oh my as all right cool guess we should uh clean up Jer a bit yeah leave us yep or no have top yeah
yeah all right well that's all for for today folks thanks for thanks for hanging out thanks for all all the good chats
nice to see all of you uh so um we'll figure out our upcoming streaming schedule um over the weekend uh so as always the
Discord is where you want to be um if you're not already member of the Discord join the Discord uh and then if you're
new to the Discord make sure you go to the rolls channel so you can click on the little alert button that uh will notify
you when I do announcements about uh streaming scheduling uh and things like that um and there's dedicated channels to
discussing what we do on on the stream so feel free to ask questions or make comments there uh any final thoughts Mike
no happy week good weekend everyone yeah so have a good weekend and uh we'll see time oh astd mentions starting a new
book soon uh we are getting uh we have a few chapters left in our current book so we are going to start think in the
next couple of weeks we are going to start thinking about what next book to choose um I have some thoughts on that but
uh uh let us know your thoughts in the book club Channel um and uh once we go through start going through that process
I'll I'll definitely announce that so all right thanks
