# ＂Song Themes＂ Episode 34： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=p0cS11A5qrQ

---

## Transcript

all right hello folks and welcome to another pairing stream with uh me tedm young and Mike Rizzy how you doing Mike good
um been a little bit frenzied but that's uh sometimes the nature of Life mine in good yeah I had uh the opportunity to
um play my tdd game that's this thing uh remotely this morning over Zoom um and and it worked out pretty well uh but
there's a reason why I'm developing the online version because managing uh even three players was was kind of rough so
um but those streams have been going well uh making progress on that um but today uh what are we doing today what's on
what's on the agenda for today song themes um well should we look at jira let's look at jera never gets does not um let'
s see looks like we left off with the failing test let's see if that's true no I just oh free and by the way hello jodis
hey jodis it's too bad the um streamyard chat doesn't doesn't show the the these are little animated dinosaurs they are
dino dance yeah dino dance hey oh well well nothing uh two ignored tests nothing failing what is our note here we're
working on bulk import failing test show number of songs imported will be will be in song importer test might require
yes so we didn't finish with a failing test we basically start wanted to write a failing test uh to do some additional
assertions um for what we want on our success page uh Mike would you mind hiding the little streamyard thing at the
bottom oh I had moved it over but then I realized I shared the wrong monitor so I had to unshare and reshare no worries
does that show by the way it does show and it and it shows in front of the uh whatever whatever you're sharing so it was
showing right in front of the the presentation assistant so it's perfectly placed uh so what is in song importer look so
we've got uh single failure message when missing header song import adds failure messages plural for failed import song
so this is um so we basically had a uh we wrote the test to page that was the last thing we did visible and so what we W
to do what do we want to do what number of songs imported okay so do well at the moment it just says it redirects to
song import success and adjust at the bottom oh it's already there great okay so right now it just displays a success
message uh do we even know what that success message is I don't think we have any assertions against that no we don't uh
so we could look at the the code and see what does it do in the response to import it looks like it just returns that
page it doesn't actually put anything in the success message so that looks like the the the zero step before we can or
maybe that is the that is the message that we want to test again so we need to start writing a test against that yeah
that's what it seems like yeah we need we need some kind of as so write a assert that asserts for a message that's not
there and then have it failed yes uh so we can look at at the failure mode as um uh so actually I think we talked about
this last time um there's sort of two possibilities of how we do attributes um and then those get displayed on the
success page that requires uh or that is not resilient in the face problem because if you do the post and it succeeds
but then you never but then the the return message is dropped you'll you never know if it succeeded or not uh and you
may try again and then end up with with duplicates unless we do duplicate checking uh and so that's that's basically the
the lack of separation between commands and because what that's saying is the the import command returns in useful
information that we have no other way to obtain right which we could say that's fine uh or we could do something else
which is do command query separation um and that would be that the somewhere persists information about the most recent
um or possibly all uh song Imports and whether they were successful or it what are some thr away number two is kind of
like um we've separated the two and then we say yo were there any errors basically sort of that old um what was that in
Unix decades ago like error info where you would query the object after the fact like how did it go proba wasn't an
object it was probably a before Evena process yeah yeah um something along those lines is that what you're thinking for
number two yeah so we could uh either say we'll just store the state of the last thing that happened um or and this is
where you get into a little bit of event uh oriented stuff whereas we just save every single command and it's State uh
which would also make the failure mode a uh possibly easier um or at least it would make the failure mode problems but
either way um yeah way we we would we would be able to see what was the last thing that happened the downside of I've
only failed so the songs you were trying to import never got to the server and then of course you of course don't
anything because you never got a redirect um so either it never got to the server or the server F fell over uh now you'
re not sure do I retry it um and there's no way to check uh and if you try to check the state the last state is like I
haven't gotten anything from you so what are you talking about versus well the last successful the last thing we did was
two days ago and here's the status um uh that would tell you something something uh and so it depends on where we
persist that info do we just persist it in memory so if you ask for it again or do we persist it somewhere more uh uh
persistable persistent persistent uh somewhere more permanent um and then we then then we don't have to to worry about
that and these are you know what's interesting about all these choices is these are actual choices these are trade-offs
we can say you know what I'm really not concerned about losing a a post message or item potency or anything like that
where it's like if something fails I'll just deal with it um which is completely a valid option uh because it's all
return on investment uh you know what's what's the investment what's the payback what's the sort of if it does fail how
much does that hurt that sorry yeah that's so at says uh let's just use the last ID in the table and and assume that
that's what we want yeah don't do that yeah yeah one yeah um we're breaking the idea of separations and commands and
query which is fine we're allowed to yeah that's you know I know yeah there's there's certain situations where it's
worth it and it's or it's just we're breaking that but we're doing it intentionally versus exactly exactly so that so as
opposed to I don't know any better or I just don't care or I'm being lazy um we're we're making an intentional choice
and uh you know if we doing uh architecture decision records this would be ADR and we say here's why we did it this way
I mean I must admit well it would be fun to do to go through all the the work of two it seems like an awful lot of work
for what is a system that doesn't require that kind of resiliency yeah at this point exactly that's my take on it but I'
m curious um uh I'm on that as as well um I I I mentioned the other options uh because we're that we could explicitly
decide that they're not worth it yes yeah yeah um all right so we have we have decided yes uh that we're willing to give
up a little bit of resiliency uh because it is likely overkill for certainly for our use case of this only one person
who's importing songs sorry I'm just I'm just filling out our ADR here okay yeah I was actually going to go and find the
template um and and use that but we'll okay do that I was decision so you basically made a than yeah I wouldn't go so
far as decision I was more like I'm blurting this out and then I was like oh wait a second this could be the cheapest
ADR ever written but no we could do templates too I'm I'm not married to the idea uh I think perhaps um it doesn't have
to be a full template on its own for each one I think we we uh might want to create a separate file though that is our
series of adrs good idea so so it's a it's it's our ad database um because it's our architecture decision database of
Records because something I don't know I mean I don't like using acronyms unless I have to so what we just call it
architecture decisions oh no I was not suggesting using an acronym so yes great and did you have um a a rough idea of
template otherwise I would just start winging it um I mean I I I don't think we need a template um we're not that formal
uh so I put I put into the um into the chat uh Michael nygard's uh from 2011 which is as early as I remember adrs uh so
how how he does it and there's a bunch of different variants um but I think we just you know we put the date and that's
fine yeah and maybe a number in case we make in case today I'm thinking about that if we had more than one decision
wouldn't we just have um I mean we could give it like a title context decision that's fine so then if the title changes
sure we can actually even do it this way that's fine I feel like i' get confused by the one one and then one again and
then one you know what I mean oh I wasn't saying one per per day I was saying also increment the number but I really
don't care a full sequential number got it so the first one would be one other words a unique number for the whole thing
yes this is this is not a decision I wantan to I want to spend much Budget on time on yeah yeah yeah cool since you're
typing it whatever whatever you want okay because we've made other decisions that we I I know true that we've regretted
or at least I've regretted uh not writing down like that set versus list generics thing right down what do we want to
call for a title on this better I don't know something about uh s import success you say fix import success uh no no
just import uh import success user information yeah inform you know response information response something like that
something about how well it's more about how uh we how the the browser finds how the browser success oh would failure go
to another page failure go to the same page but failure is actually kind of covered under this as well because it's it's
sort of a more General thing although this this decision applied specifically to the success so include failure in the
parenthetical or no uh no because we're not making a decision about that I think we already decided that that was fine
we didn't record that but we're not going to record that now so I think uh there's the there's context and then there's
the choices and then there's what we what we selected so you've got the choices so you want to call it choices sure or
options alerts I mean it's it's it's explicitly the the things we can choose from so options is is right on okay I just
bessan is that a typo ASD uh no I'm not sure uh so options that or that decision option one yep sounds good to me so I
might uh rename the file so it's a markdown file and then you can use some of the markdown formatting to to help divide
things up is it shift F6 no yeah oh it's not working uh so for this case you have to be in the project window ah because
otherwise it thinks you're trying to rename in a text file work so now what you can do is you can um I would put like a
a double Octor in front of that and put a space yep so now that's treated as a second heading if you uh Mouse over in
the upper right of that client uh a little to the up is there a setting you have on your computer yeah there should be a
showing the preview of this file um maybe close it and reopen it because maybe it didn't yeah there it goes there you go
that's what I was looking for uh oh interesting oh because it's MD it doesn't count that as a break right so you want to
put a new line before that and then three in front of that there you go okay you probably want a blank line uh after
after two so after up uh 12 and a half line 12 and a after really a no no it's a 12 and a half line 12 and a half tab uh
that's what you want the level of indent for those next two items got it so you want that so that three goes away oh it
gets converted to that yeah so that that number is sort of irrelevant um but that's the tab level you want for get rid
of the number three will that go away so you don't want to get rid of the number three uh oh why because that's the
that's the level of tab that you want so what I would what I would do is erase all the white space to to the left of the
A and just join just basically join the lines like that go to line 13 indent and join the lines where is it Alt J uh
it's control shift control shift J right yeah uh but not not twice right because those are two separate entries so we
want those on two separate lines and they need to be at the same level of indent otherwise it doesn't know that they're
two separate B and now the move the the B to the left so it's aligned with yep put a number in front of that like four
doesn't matter but it has three there you go so generally when you're doing markdown um so I take it you're not familiar
with markdown no okay so when you're doing markdown uh when you indent it it does the numbering automatically so you're
putting numbers there just tells it um hey I want these numbered uh you have a little bit of control over how those
things get get numbered but you could basically put ones in front of all of them and it would number it automatically uh
I'm not sure why it picked no Roman numerals for for those um yeah if I remove the three in the four what would happen
it wouldn't know that those are uh ordered line items ah but did one and two no doesn't really I was two here yeah so
you have to put something so that it recognizes that that is not a continuation of the previous line got it and that
that it is part of the the same list so you're just not sure why it's doing Roman numeral or the yeah I think if you put
a and b it would probably b um but then you need to put a uh you need to put a blank line yeah I'm not sure it's
recognizing that so there's different markdown variants I don't want no all right so we got our decision record uh so
let's get to it okay should we commit that we've got this or wait till we write the code for commit I'm always in favor
of committing okay all right so then um we're going to want to then structure this in the same way as we did for the
failure messages which is use the redirect attributes um to provide the information about the success message so so you
could probably change yeah maybe it's not worth copying any of it because it's already been refactored to uh be useful
for the failure coding um so what we'll want to do is is extract the redirect attributes model map into a variable that
we'll have access to because what we want this method to do is to put stuff in there basically put the success message
in there and then we'll evaluate that it was put in there gotcha so I'm just going to look back down here so here we've
put it to a local variable right so we then could reuse check things here correct y got it so it's very much like the
model concurrent model stuff we've done before uh it's just because we we're want spring to hold it hold on to it over a
attributes so we've got that part just looking at the other one this has got a special function that we wrote yeah was
just a convenience method so you could grab the line of code in that method because that's we'll do something very much
like the yep NOP not that one no it is that one I think you extracted the varable you're right revert no no not
breakpoint this oh I know what I'm doing wrong there we go all right and then we can put it right there and we said it
was success message is what we're looking for as the the key map uh and then let's assign that to a string because
that's we're expecting it to be a single string ah okay and you'll need to cast it right was that again if you just do
an you oh assert probably assert that uh we can start out with it being not null and then we can ratch up our assertion
something all right so if we ran this test what would our expectation be um that it would fail because we haven't put
anything into success that I'm aware of right so that's our quick question there you go now we just want to run now the
song importer yeah we just want to run the I card all right so let's make it this would be on the import redirect
attributes. addattribute oh interesting why do you have an extra PR there that's what I was wondering huh and at this
point we just want it to have something so we could just yep basically we want you just want something that's not no so
I wouldn't even put just go with empty I just go in an and how redirect at one second I'm just this okay yeah my
prediction is it right nope oopsie did you see something yes and I was wondering if you were going to catch it before if
not then we would have had a failing test that's fine so uh so not as predicted you have to stay in the current hex tile
so you are in the game mode we're setting success message oh I yeah and this one to get flast plural because it's a map
okay but we're only getting one and so we don't have to cast it to whereas for these guys those failure message is
plural so it's a map that that Maps strings to objects so a list is an object the string is an object that's why we have
to cast it because we don't know what we're going to get are we going to get are we gonna get an array are we going to
get a list are we going to get a string we don't know right so it's up to us the programmer who book The Other Side of
this equation to make sure they match got it so now Hing succeed unless there's something else I missed Noe excellent so
now we can ramp up uh expectation I think we can be precise here so it's a single message what do we want that message
to say oh is exactly uh is equal right we're just saying what is this what is this what was what do we want to display
if we successfully imported well I don't want to say successfully imported song but I would say songs that's a that's a
place to start and then of course we'll have to add the number in a bit right now we'll just run fail it'll say got a
blank string not songs me run that again you mean run expected that's why control W is your friend Mike took the words
right out of my mouth let's run this and see if it uh should pass yep all right so now ratchet up some more and have the
number of songs yes so here so I don't know if I want to deal with the pl singular plural thing oh I'm fine for taking a
taking the easy route okay so so I usually put the pen around the S so it's s that way it applies it applies both ways
gotcha okay the easy that's always the easy way out yeah yeah I'm totally fine with thatth so now this should fail and
let's see where is our success message so do songs import songs what does that do that's the parser parcel parcel
indicate anything result success so we just stuffed the number of songs in the list so I guess we could do the count on
the so I think there's something wrong here uh types and which part portion where are you thinking so what's the return
value of the method that you're currently in uh it is result of song uh who's calling this or checking it so this is
because um uh can we look at the result success method the implementation of of results success oh interesting uh that's
why it works so we've defined success as it must have list of whatever you've defined the success type as got it which
is and that's a very inflexible way of defining the success because it always has to be a list of something no matter
what well yes that plus it's not obvious that that's the case which because it wasn't obvious to me right right and uh
it's not super self-documenting yeah so so it's not intentional revealing at all um and it doesn't allow us to use
anything other than a list of those values so if we wanted just a single value or if we wanted a set of values uh or we
wanted basically anything other than a list of those values we would not be able to do it um since obviously we haven't
needed I think what I would say is let's continue but um there is a task of J we need to to dump uh this result class
and use a more proper one um I think we have a j for that we just have to decide when we're going to do that so I think
there's another entry about there's yeah let's see if it wraps around no I guess I think I think we we we probably want
to put that one 23 under a bigger one which is library because we could continue to refactor it but there's there's an
implementation that's that's good enough that solves that problem plus this other problem that we ran into should we put
the reason for it here uh yeah I think we should document that there's an implied list of yeah we could do an ADR the
reason why we're we're skipping it right now is because it works or at least it works right now um yeah I don't think we
need to do that okay so uh so that that resolves my confusion um so if we go back explains your confusion I sure it
resolves it well it resolves it for now true true uh it may not resol it won't you know the next time we run into it we
might be confused again um then in our code uh I think we know what to do so let's go then back over here yeah uh no
here yeah so my my confusion was how can we where do we get the result how could we possibly know how many songs there
are for only getting list what is it do formatted right no the um sorry size gets us every time yes okay so in theory
this should work yes and if it does we probably should add one more song to make sure it works songs look like a test
that was awfully fast nope that was all of them no wait no default package that wasn't that fast it wasn't I mean I mean
it was fast so what do you think of the idea adding yeah so I might differentiate it differently to make it more obvious
that it's different um I might just put one and two in front of at the end of each each one do you does it matter about
one and 33 just add two in this one that's fine I'm like it's just the eye the eye at the beginning was not no I know I
I didn't like it either i't started yeah partially as me Acre now this should fail but it's the number how is it gonna
39 let's make this let's crank this one up first mhm now it should fail in 41 or 42 actually yep well actually not 42 oh
right yeah 46 yeah but the but the other one yeah yeah now now it should pass excellent cool so that's an interesting
idea that as that as has is basically put a put a little how often were you confused by this line and basically you add
one every time you were confused by it and when it hits a certain value then it's like okay you really must per factor
that I like the r of three angle on it yeah where would we put if we wanted to do that let's let's do it just for for
fun so put it where I was confused um was in the bottom code when uh basically because I was confused by that right I
was confused by the fact that result was containing song which meant that it could only hold one song um but I'd
probably put it at the end of the line saying yeah confused confused One Time by result song really being uh and so I I
said one time because uh I wanted the digit one uh so that that would be incremented oh I see yeah yeah I was thinking
of here at the end doing you know as had the idea of putting a question mark can you put a question mark after the the
double slash what does that look like tied into it or the space uh right right after it so you could use that as the
counter but I think that's not obvious as to how it's counting um but it might be good to to have that as sort of the
the confusion all right see we hit it again Amit yep we got a passing test for this little mini feature returns import T
now provides browser with number of songs imported now we're not displaying any of that actually we are are we the HTML
has oh because it's text right it's just the text that we're yeah ah knew I was gonna do that wrong so given this since
we have the ADR yeah you can delete probably delete that do we need this framework test no com and you can just and you
delete the failing test Parts what we achieved was not the failing test but actually that piece of functionality yeah uh
AST makes a good point of of we've confusion so we could uh to be more useful as a confusion indicator we could
basically drop the everything after the word really do we that you're saying yeah in other words not explain the
confusion well if you explain the confused so if we're if we're basically running being confused here and then being
confused then look at the comment you're saying don't give the leading question I I I I think if if we want to run this
as a as an actual experiment of will we be confused by this again I think we need to not uh not all right uh we can run
the app and and then do the import and we should login yep good thing I had my password VA open so let's see what do we
want um well we're gonna have duplicates now so this should songs the problem with the width of the screen is the wrap
makes it hard to count out I'm to pick a smaller number test I'm not concerned about that we have that that's pretty
well covered with tests um we could make the uh the text area wider if that's if you think that's a problem in the
future okay you can also drag the lower right to increase the size of the text area oh sweet so one two three four five
six songs and we let a rip pressing import yeah did we not set up the authorization for the new isn't that uh a new page
well we got uh we got an error page oh do we not have a an endpoint for the success we may not have actually implemented
the success uh but I'm concerned that uh that the error is not being passed through can we go to the uh um we have
dispatcher type error permit all uh oh we don't we didn't ex oh we did not explicitly add that page mean like um well we
want we would want that also as authenticated because it you shouldn't be able to go to the song import success page
unless you're authenticated ah this yeah except we don't want to do it that way okay uh what you want to do is just like
we did on the line above you can comma separate the the end points oh I see gotcha um but this does mean we might want
to think about putting them under their own path so we don't have to do this every single time um let's do it now and
then we'll we'll fix it okay what was it called again I might have to relog in or not we'll no interesting exiting from
error dispatch up that's because it it tried to refresh the page um oh so go back go back to to the home oh I see yeah
yeah yeah I was I go hey Benny so Benny mentions uh why not do any request authenticated uh because that's really
dangerous um it's fine if you if you never will have any kind of different authorization for different aspects uh but we
will definitely have different authorization ability for different aspects of the application um so doing that if
somebody's authenticated they may not have be authorized to do the thing and you may not notice uh so I'm always very
careful about doing any any anything if if it's any kind of uh permitted or anything like that I'd rather eror I'd
rather air on the side of not allowing somebody to do something when they should be able to versus letting somebody do
something that they should not be allowed to so all right that a rip yeah yay there we go cool now didn't we have I
guess let's look at jir but I thought we we had a j we had a j for showing the result the actual stuff that got imported
yeah um but let's do so what I would say is before we do that um let's uh refactor our end points a Mark Ure which it
turned out it wasn't working brows okay you were gonna say something yeah so uh let's put um admin or contributor level
uh endpoints under their own path to uh but as Jonah suggests let's do a commit since we fixed that oh yeah I was gonna
say commit and then take a break yeah commit and take a break and then that yes the secret to productivity just clone
your jur tickets and and what you do is is you do it fractally right so you take the the Jura ticket you slice things
down into small pieces anyway and then you get look at all the tickets I've closed and you break it down really really
into super tiny pieces and then you get lots of little tickets but since tickets are apparently equivalent in value you
get lots of tickets done this well look we've doubled our velocity we've tripled it we've CL yeah there's that joke
right like um you know you sneeze and it's two more story points right I and you create a ticket by saying uh uh I've
created a ticket for this thing so I'll close that because now the ticket's created okay all right uh so we'll take our
break and when we come back from our break uh we will uh refactor our end points and then we'll move on to the next step
which is display the data that was actually imported um and not just the count of songs so we'll do that so we'll see
you after our coffee breaks he than he uh so just a reminder that I have uh a game called Jitter Tad's tdd game you can
see uh I've got a game in progress here um that I've been playing uh with some folks astd being one of them um but you
can get your own copy uh all you have to do is go to td. cards and you can get a copy and uh on my solo stream uh what
I'm working on is putting this game online and so uh currently that mockup looks like this uh so this is the the online
mockup that I'm working on um and so if you purchase the uh if you purchase the physical version then you will uh get
early access to to the online game so go to td. cards one of the things that that's really nice about this game besides
um being fun to play it's it works as just a game um I actually given it to my son for him to play with his friends I
have to check in to see how how that went uh so it works as just a game but it also is perfect for fostering discussions
around test driven development especially uh the predictive model and writing less code at each step which I feel are
are really critical uh and often underemphasized parts of doing test driven development so dd. cards you can order get a
copy I still got a few in stock and you'll get early access to the online version and now themes uh Mike I think there
you go yeah all right so let's um let's change our end points can we actually yeah I'm gonna ask you how do we do that
do we just actually make a path or do we need to so the the where the templates are located is not at all important uh
for where they end up appearing and this is often confusing I still get sometimes confused about it um the controllers
the get mapping and the post mapping Define where uh so these even though we name them similarly it's actually the
mappings that matter here not where the files are so this is basically Behavior provided by the the controllers uh
themselves oh did I forget the confetti hold on there's the confetti what was that for uh because uh Astra did a
celebrate oh cool um so what we want to do is we want to change some tests because we are changing system Behavior so
we've got some tests against endpoints so what I would I would say is we want to find where the song import and song
import success mappings are and then change the tests for those I'll here's song import right here yep so find the the
test for this which are all surprisingly song and Porter test so what we want to do is we want to look for the tests
that are asserting against redirect page string one so would we basically add a subpath and what would be a name that
would make sense uh you tell me so usually what I I do is I um prefix it with a role that I believe will be applied to
users who can access it um this isn't strictly admin which which is why I said contributor so we could say either
contributor or contrib I don't mind the full name but up to you I'm a full name person so like that looks good to me so
now we run the test and it fails and we of course just run this one or run all of them I guess we know it's an IO free
wait a second pass all right ones this one does song import so be same fail and so there might be multiple tests that
redirect the same things so uh when we fix it we might find that another test fails but that'll be okay right because
probably could be that one too which test was this this was n yeah so actually I fixed the wrong one yeah it's well run
it and let's make sure that you fixed the wrong tests yes very good okay so now back here you want to undo the other one
now one and this one is this test wait you're going to fix the the test by oh I'll do it backwards yeah you're right yep
I mean I'm I'm okay with that like yeah I I would I would not have you uh well I just did so that's fine now we got it
failed for real yeah it wasn't it order okay so what else do we have in this file that's checking redirect that's it so
what other song import song import success so now we need to change our MVC tests because they also hit end points that
we want to update because what we did was now they redirect to the right place except the place where they need to
redirect to are wrong so now we got to do all tests and we get should get some failures uh actually I don't expect any
failures because we haven't changed the you can go ahead and run it see okay MVC tests they're slow so they run yes so
slow oh my God it's actually the jdpc tests that that are the slowest because they have to bring up the test container
okay sorry uh Jonas is saying how dare you write production code first yes we should not be sloppy we should not de
demonstrate sloppiness yeah just imagine the ruler came and wrist I don't know that's a us only so these are the two
tests that are hitting song import and import success three tests there actually three because there are three in a
sense there are three separate endpoints there's uh a get to the song import uh and a post to the song import and a get
to the song import success so there's basically three mappings that we need to update so we just need to go through one
by one change it have the it what am I missing yes what are you missing so I see the test where is the I guess I need to
find the code that this test is running against yes so where would that be is way to navigate to it directly uh not
really if you're using the ultimate version tell you it should have a way to link to that if you hit uh control click
there it should take you right to the thing yep right there song importer but didn't we just no we only changed the
redirects we did not change the mappings there are two parts there's right hey go here and then there's oh you came here
right there's the response which we've fixed and now we need to requests got it okay so we want to change the B the
expectation first so in this case it's still in my buffer or not I'm actually gonna just see if it is yeah it is okay so
now this one should consider slow I'm just gonna run this one yeah I was gonna suggest just run that just run each test
yeah because we don't want to run the jtbc test you could just run all the MVC but you may as well just run this single
test because that's all that's changed so we pass all right and then we can move on to the next what you Chang
production first oh right thank you so again we expect I ran no I ran the wrong test right so our expectation failed we
expected a failing test with a 404 and we got passing yeah so ran that's okay so can you not scroll all the way to the
top I want to make sure I want to see that 404 so it's right above the stack Trace there it is there it is so we see a
404 code now I can do shift F10 because it's the exact same test now that should pass okay and now this next one Let Me
Wait yep that passed now this one I'm going to change the test not the production code run this exact task yeah fail
failed predictions so you turn oh no well Jonas if you if you want to write sloppy code you can just say well Ted and
Mike did that on stream so I can do that blame us we'll be happy to accept the blame or at least I will all right so
that failed interesting now the jump doesn't work um the now it should pass let's okay so I would say let's run uh all
the MVC tests I don't think we need to run all all tests um it just iio based actually do you have a configuration for
MBC oh we tag these as just IO let's tag these as MBC instead or also instead instead because the way the way I tend to
do it is is tend to have IO free um MVC database and then just everything is this the only MVC test class uh I believe
not no there's this one song So if you look for MVC test because we always end it with MVC test and if you look for
names of files files I no so not finding files yes that one yeah I was just working on my keyboard shortcuts yep so we
just did this one right so then it's this one yeah oh look that one's already tagged correctly so we must have tag the
other one incorrectly so let's go to our run configuration wait I'm not sure about that this is or maybe we maybe we
only oh this I got them backwards okay yeah I something wasn't right okay good okay uh so let's go to our run
configurations and edit configurations uh let's let's rename the io based tests or would you make this upper case
because it's no longer oh I don't and then apply uh and then yeah then clone this one you can hit the little copy icon
at the top database and I guess we'll tag it as DB prefer do we we must have some yeah they're currently tagged as IO so
we'll go change that I got to fix the spelling of datab yes uh and can you click store as project file on this one and
on I think the other one is fine because we already saved that one yeah yeah they all are they all were except for this
one yep and then now we have to find the database tests yep are they already tagged or no they're probably already
tagged with IO so you there you can do a find in all they weren't they clearly were not tagged at all because when you
started typing tag only two of them container maybe we don't have database tests uh oh you're you're you're looking in
directory we W want to look in directory want to look in project project maybe that's why we weren't finding them go
back to tag yeah there you go so we did tag we did tag them as database uh startup the startup test though uh you want
to go to this one what do we want to call that one well we disabled It Anyway let's just and I think we need to go to um
go back configurations uh and update our IO free test because I think they're now tests oops that's fine let that run I
was going to have that run anyway so that's fine uh let's run the MBC tests so they should only run tests that are NBC
yep and then uh run the database if you want oh did you have a different thing you wanted to run no I was just going to
say I wasn't going to bother running that at all ah we definitely do it for commit once running yeah could could just do
H all right let's commit okay what I gon to call this um we moved what was the terminology we endpoint so we prepared it
and now we can change our security in the next commit to anything else oh I guess we added um all right approved run
configs uh yeah I I don't know that I bother you saying that it's now we're going to update the um security yep so will
we just do one request matcher for SL contributor yes how do you do a path so I would take yeah so we do is um yeah so
take take that one out uh and then instead of song import we'll say SL contributor since you've already got in your
buffer uh and then a double star so SL double star yeah so what that does is anything underneath this this path sweet so
let's stop it and rerun is that right uh yes we don't have uh we could run all the tests uh because our MVC tests uh use
the security um so we could run those since they set up a fake user they should have access to that ah so we don't need
to necessarily do the manual running of the app we could just a double check but um those tests should uh and we can
prove that by taking out the double star so we didn't actually see it fail so maybe we want to do that uh so let's take
out the double star um let's run just the MBC tests because we don't want want to spend time tests we should have these
fail Ur because we have Haven set up permission those denied uh but no we haven't explicitly um what do the can we go
look at the NBC test so we said with mock user that are we using the right m match we are using request matcher let's
matcher uh we're we're not applying roll so it should be anybody with a mock user but config no ant uh ant matchers have
been deprecated uh since like 5 point so 5.8 changed a bunch of the way the matchers work uh and you're supposed to the
request matchers uh you can use the NBC matchers um but it's recommended that use the that uh so to me I'm I'm I'm I'm
curious if we have to explicitly deny I front because all we all we know is that you're authenticated or not so we may
any request I mean what I'm wondering about is how does don't we have to Define what the role of fake username is no
because all we all we said in our security setup is that you're authenticated so that makes you authenticated we have
not done has we have not applied roles yet um all we said is that anyone can access slash or theme search uh but nobody
can um and right now nobody has authentication but me well any any logged in user uh is considered authenticated so that
fake user that mock user is considered authenticated yeah so let's let's add at the end of that on a new line at the end
of line 20 on on a new line uh say do any all right I don't want to Rat Hole on on this uh let's just put the the the
double star back and leave the denial yeah let's leave the denial just to make it explicit that that um any other
request is is denied run all the tests all the MF MVC tests again just to make sure double star doesn't should be fine
right should we add a jir to look into this offline Spring Security is one of the Arcane um has it's very brittle and
it's very hard to use correctly which is unfortunate for it being security because there's a lot of stuff going on under
the covers that's not obvious which means you could think you have it secure but you don't uh yes which may be the case
we have right now yeah which is unfortunate um because I don't understand there's clearly I'm I'm missing understanding
something uh and and the Jon asks about the forward and the forward is about um forwarding to a template which is
supposed to be separate from the requests that are being made um so these are not redirects because there's a separate
redirect dispatcher type all right so let's um let's let's run the app to check uh okay ah now I need to give A New Path
yes so all your all your autocompletes and and history is is now useless dang okay all right let's uh if you want you
change Commit This yeah let's commit it's well if you're not logged in uh if you open up like an incognito or private to
you should be able to get to the the root endpoint but you should not be able to get to the contributor endpoint okay oh
gota log in well the idea is you don't want to log in so you should be able to go to rout right so that's a and now if
you contributor now it should force you to authenticate right which it does yep need all right so let's commit okay what
do we want to say um well this we just changed the the security to uh require authentication for yep okay all right ASD
have a good night thanks for joining us good night um I'm not sure what your asking full n question hello uh is that
steel stey how welcome uh Mar this one done this's done no I mean we check there there might be some interaction with
the way the tests are working uh there might be some interaction but we checked our browser required you to authenticate
and that's all our test all our security config says is you must be authenticated to access those uh but you don't have
to be authenticated to access the route so we works you want to look at full lles claric uh summary of the logic uh yeah
do you want to go through just go through what what this method's doing yeah so we'll we'll get a songs if it's null we
consider it um an error actually contributor yeah we go back to the original page saying right can't do anything um
although in that case we don't show an error message we're assuming that something went wrong because it's uh uh very
unlikely that spring will give us a null here this come this comes in as as a request from uh from the the form and this
is just sort of protecting that that um but I don't feel the need to put anything else in okay um so then we call the
song service which gets past the songs then instantiate a parser I don't think you need to go this this level just this
L and and fulln can ask any additional questions I don't want us to go deep deep deep okay de birs so let's just so we
basically parse it yep and back uh if success we say hey hey these are the songs or not these are the number of songs we
successfully imported right if it fails we throw some failure messages uh back to the browser and it's failure message
is plural so say we pass five songs and three fail we'll get right yep interesting and oh sorry uh line 44 basically
puts whatever you had entered back into the text area so you if if you know if it's just a minor fix you can fix it um
because what's always annoying is if you submit something and there's an error and then the thing is empty and you got
to start all over is always annoying so we put basically put it back uh so it's there when the page re sort of refreshes
yeah go one thing I realized is so if we have five songs and three fail do the two success we don't actually report that
two succeeded well cuz they didn't oh if any fail the whole thing fails right is that true I don't know that that's what
I think is true we can check um what do okay so I probably wouldn't look for a test at this level that that does that I
probably would be looking at a test directly against the um song service import songs because if we don't have a test
that says that then we should we should write do so you're still at the song importer test do we not have any test
directly against the song service Oh I thought we um okay so we have a a whole bunch of so we can check the malformed
one uh we just look to see if the result is failure so we actually don't are not explicitly testing that um a mixture of
passing and a su successful because I would say that the behavior that we want uh is that if any of them fail we don't
want any to succeed because otherwise then it becomes really hard to to fix it you got to go and like yeah yeah
especially if you're a bulk importing like 200 songs and and one of them fails now you got to go find that one song and
go fix it and then delete all the others and what if like half of them I mean I I just think that it it's should sort of
be all or success all or um but you're right we don't actually have a test for it so now actually I don't know what the
behavior is uh we could look but I think we level okay um mixture what was the new structure we're using with names uh
so outcome first right so I would say what are we going to repository so we can say something like when uh so full no
full transactions are uh already implied by the jdbc implementation so one thing that you may not have notice is that
this test class is an abstract class um because it's testing against the application use case layer um we want one set
of tests to run using our fake repository uh but then we want the other to use the same code in the same test but use
the real test container database uh so when it's using the real spring data jdbc and the test container then applied hey
DOTA attitude um is that actual song data in the test uh I mean we Mike's been picking stuff from actual song data that
so those are actual songs if if that's what you're no so I'm it's a really verbose title uh no s repository yeah I might
I might minimize it by saying uh when at least one failed song or one failed song import but we're so we could say when
at least one song one song import how about malformed because we've been using the term malformed in the previous yep
okay yeah we've been trying to use realistic scenarios like uh oh I forgot to copy this column or I didn't copy enough
columns or I copied the wrong columns um or I copied things in the right way so you trying to use generally right let's
get one that's real how many columns we get one two uh what's the multi- select is it J uh alt Alt J all J but you got
to select the thing first window then next time we don't care second oh do we want to put don't cares in there no I
think if it's real data it's real data so if if that would work then that's fine yeah so that should work so actually
should success uh negative no I think we should Express what we want and then are you saying you're not sure if that
data is going to be good uh right to prove that this data is good sure so we do that now it should fail right that's not
at all these are IO confusing right yep okay good so now put this back go so now this should pass again and yeah how did
we check the repository last go well if it's failure this should be empty yeah so I think what we'd the behavior we want
is all songs is empty that's what I was thinking happens yep yep okay cool all right um uh yeah I'm glad we wrote that
yeah because that was my suspected Behavior but we didn't have a test to make sure that that was to not only documented
but also ensure that that's actually the case so that's good okay let's all right check this so I might make that more I
make that more clear um I'm fine with so add a test to make songs uh and then I'd put a comma there after songs uh where
some are correct and others malformed causes uh no songs to be saved into the Repository and uh just to be sure we
should run the database tests as well okay sorry that wasn't something to type I didn't think it was but I thought it
was yeah be uh because this is the the version of the same code uh but running with the database as the repository as
opposed to an inmemory version and sometimes there are differences but not this time oh good sweet so that's I didn't
think there were but they say better better safe and sorry yeah and it's good to call it out too be explicit that's what
we're doing okay all right what does jir say for us uh so now we said we wanted uh to show the actual data that was
imported yeah so how do we make it tabular so it's readable instead of the the crappy way it looks when we paste it in
uh we use the magic of HTML I've heard about that um so this is popular data so we use a table yeah even though uh divs
and CSS grid and so on uh still for tabular data I think table is the best way to go so um let's create our table in the
HTML and then we'll have to put the right stuff place are we doing it for Success yes for Success that would be because
we just demonstrated that if you if it's not success we haven't imported anything oh can you just try something uh can
you minim minimize that bottom window again a little bit and now double click on the tab was that a double click it was
some me do it again yeah huh I thought you had the uh tab switcher plugin I do I believe it might not be configured
correctly because some of the other tab switches stuff I was looking at were plugins have it installed that's weird uh I
wonder if it just works differently on Windows huh OSX shortcuts other OS shortcuts because what a double click does on
the Mac is basically an Al uh uh an Al alt shift M um which is maximize that window temporarily but maybe that doesn't
translate on Windows okay never mind Sandro is that the the guy in Sardinia uh I don't know where he's located he's he's
associated with codurance I'll go look him up later yep all right so never mind let's let's cancel out of this okay now
make it bigger um there is a keyboard shortcut to what it does is it maximizes that and then if you do it again it's a
toggle and then it basically puts it back the way it was and so it's very handy for like what you end up doing a lot of
which is drag it Up drag it down drag it Up drag it down right um there's a shortcut for that I'll have to look for that
um but it's it's already a lot of shortcuts on top of a lot more shortcuts so uh all right so let's um let's put a a
header that something like you know imported songs table so table just straight up or do you want just close it and then
uh we want our headers and now we want uh so I usually put the table headers on a single row and then just it makes it
easy to to duplicate that meaning like this yeah control shift J would have yeah been your friend there um so now we
just basically put in a column this is the the header that will appear at the top the table so you just want one of each
of these for each I forget are certain columns uh well you want to look at whatever is in song um but I put each th as a
separate uh basically stacking up the th's Oh I thought you were saying you want SE on one line sorry uh I want the th
and the closing th on one line you had them as two separate things each th element on one line but stacking stacking
them because then it's easier to read got it I let me go look at song again yeah because the only data we have is what's
in song artist song title release title release type and themes okay don't know why I did that artist song title release
themes or theme one theme two theme three you tell me I don't know which is better um I think just grouping them
together and having them separated maybe like comma space square bracket thing which sort of Auto we can do the the
comma separated that's that's easy enough with a string Joiner I know we do I'm pretty sure we yeah um all right so that
that defines the header row you can preview that if you want yep okay and since you have no uh Styles we get a pretty
boring table but we can make that nicer later uh so let's go ahead and after the closing TR we want TR um this one is
going to be the one we're going to Loop over so we're gonna do it four uh th each you think it would be four except it's
not because four is applying labels to input fields which I always get confused about uh so want th each uh and we
pretty much want just want to pull some kind of song view out of a list of song views do we I forget how we did that so
you can just say song view colon and then uh so I usually name these like Vari these are variable names they start with
a lowercase and I put spaces around my colon just to make it easier to curly and then inside there would be song views
basically that will be the list that we'll put into our model like that yep you can close the TR and line uh and then
you want basically uh similar TDS because these are cells so they're TD um so you can copy and paste those wrong okay oh
I missed one now what happened was you selected too much and so it did Auto completes for you I was going to say only
select just the the the letters not the bangle brackets but it's fine oh I see easy enough to fix uh so now what we want
to do stick in uh after each TD text um so what I usually do is I do the uh I do a uh multi I do a multi multicar
vertical but that uh I don't know what it is on Windows is it a double tap on the I don't know what the keystroke it so
there's a on on on Mac it's dble you double tap the option key and you move the arrow down I don't know what it is on
Windows try because won't help me because uh oh it looks like it's a double tap of control okay so if you hit control
twice if you say control control down arrow no no control down up control down arrow but you have to be uh does that
trigger run everything so double tap of control does run any all right well then yeah uh the intell is wrong because it
says double tap of the control so you have to so you do control up and down and then control hold down and then arrow
but you have to do it quick enough so that it recognizes it as a double thing this is why this keystroke is really hard
to to learn got it there you go and now every time you do down it it duplicates it uh but if you wait too long then ah
then you lose it this is one of the harder ones because it's that it's that that you right you got to hold it down while
you press the arrow the second time and you got to keep going otherwise it it goes out of that mode ah damnn it so I'm
gonna say don't don't bother andless okay I was so close what you can do is um if you want you can do the select the
entire TD element including the angle brackets and then just do the all J and now you can move right and then left and
now you've got basically what equals and then brace uh and now that that's G so that's that's all that's the same for
each one and now you can just put in the uh the individual names we're just calling them I think they're just straight
up right yeah why not we we can call them whatever we want oh at this point they're not already in there well we haven't
defined song view so we uh what did I think we did yeah Jonas is correct you we're probably lifting up the control key
too soon so you don't lift up the control key the second time until you've selected all the ones you want but again it
does take a little practice okay and yeah it is game it wouldn't surprise me if there is a hidden snake game somewhere
in intellig I would I would not be at all surprised uh so we can we can do a preview of this just to make sure that
everything's laid out at least in some way uh oh great then is it used so there there's a bug in well okay so I
encountered a bug yesterday where it was saying oh this record is not used when in fact it actually was um which caused
all sorts of problems for refactoring uh now just because it says it's not used doesn't mean it's not um let's I'm
convinced it is used so let's look for a new song view in if you're going to do a search it's a new at space in your
search yep yeah um three places so we are using it there's a bug in intellig uh so Jenice asks have I have I followed it
yet no because I um because I wasn't sure if I it would be easy to recreate but now that we've I've seen it twice in two
different projects uh now I'm going to file I'll file the issue today because that's um that's pretty awful and what I
what I ended up having to do is convert to a class do the refactoring and then convert it back to a record which was
really annoying um but in this case we can just reuse it because it does exactly what we want right uh although it is
missing something this part might be different but that's fine uh but it's missing release type ah do we do we care
about release type at this point we don't because we haven't release type is that one column that we still haven't dealt
with as far as it could have the word compilation could have the word collection or soundtrack and then that has some
verification implications like if it's a yeah remember there compilation or soundtrack it has to have a release title
whereas nor don't considered having a release title right so the question is is um for now do you expect to be importing
data with that because right now we're not showing it we're not showing it we're not showing it but we are taking it in
so I don't like I don't like that asymmetry yeah me neither I would rather show everything we got um so let's uh so I
suggest we actually I don't want to show everything we have um because I haven't decided like contributor oh is that
just ignored it's not yeah it's not a column importing I mean if you look at song it's not in song right song is our our
domain object we don't have contributor anywhere ah okay so that stuff is so it's one two three so those items and that'
s it so everything else is ignored yeah so that means when we start real at that point we'll have to decide what to do
whether to clear the database and start over again oh no that's a migration that's what migrations are for that's true
that's true the presumption is that the only person who's importing that the minute we care about that there's more than
you just importing it that's when we'll do the migration and then we'll in the column as a default with you because you
were the only one who imported right so so that's that's a that's certainly a yagy but that's not the only column we're
ignoring the other column I have but right now we're not displaying uh both when you find songs and if we try to use
reuse the song view we're not displaying the release type so if it's in the song I think we should display it regardless
of anything else got it so we'll just display everything that's in the song yeah all right J good luck tomorrow with
your uh and good luck with your on call week oh wow so I hope you to sleep hope called all right so uh so what I would
view other words add in release type yeah but if you do this um we're the refactor is not going to work because it think
there are no usages should we do the same thing swi it to a class um it's only used in a couple places so I think we can
uh just manually do it I mean let's try to do uh uh a change signature I just think it's not going to fix anything and
then we'll just fix the compilers change signature okay like that yeah and so wherever release type was is what we
spreadsheet after release title where is it now well you just moved it up so now it's in the right place okay and you
can see see the preview in the bottom yeah gotcha okay let refactor fingers crossed and my guess is if you try to run
the io free test it's going to fail to compile because you think it didn't because I think it didn't whoa oh that's
interesting okay that was oh that was me yeah uh so you need to fix that by putting in song a new because we've now
changed it uh so looks like it did work it looks like it actually did change at least view so the question is did it
change the other references because it changed this one yeah so it did not um but that's fine we can just manually data
now just yeah now it thinks it's used except we'll see I'm not convinced that that will that will stay that way what was
really weird is like it was clearly used because it was used inside the record in a static method uh so I wonder if a
minimal re reproduceable example it can be done record no yeah that's I don't know I don't know what you did but you've
got too many double quotes there we go yeah but this is now wrong because you got too many double quotes here we go uh
and you probably want to copy I mean too because it's missing now irrelevant release type actually want the quotes too
uh no you don't want the quotes because you're pasting it into something pass excellent commit I presume y yeah before
you commit actually uh suiga brings up a good point okay that it's no longer irrelevant because now it's actually used
in the song view yeah well if we actually go to valid yes but that's not the current behavior this that's fine because
that's the relevant release night is actually not a if you think of it as a if you want to keep it valid that's fine
yeah keep it valid it's either empty or four other strings none of all right let's finish that commit and then take a
break and then we'll take a break yeah we shot past our break commit all right so uh we updated our HTML to show at
least uh will show the correct stuff um you can do a quick preview just to see uh and I think you 25 totally now you've
got an extra T there you go uh if we preview it we should see that that's fine um and when we come back from our break
we'll actually uh update the controller to put that data into the model so we can grab it n a he hey folks uh so as you
may know uh in my Discord Community one of the things we do is we have a book club and so we're just about finishing up
the book uh the programmer's brains we've basically got one more session and then uh we're going to select another book
so if you would like to participate it's free um what we do is we pick a book uh once we pick a book then every pretty
much every Sunday uh from 10:00 a.m. to 12:00 noon Pacific time which is currently 5 PM UTC uh we spend two hours over
zoom and we try to make sure that we understand what the book is saying and we uh discuss things we share experiences uh
get clarity on things and so uh we've done gosh I don't know six eight books uh since we started doing this um so our
next book we're currently selecting and so if you want to uh help select and participate in that join the Discord go to
the book club Channel um there's This Thread about uh up what book you know you would like us to cover uh and I have a
few little guidelines about the kinds of books we're looking at so we're trying to stay away from very specific language
or framework kinds of things so uh not going to read anything on Spring Security as much as I feel like I need to uh
we're not going to read anything on react which is totally fine with me um so we're looking for sort of more General
books of more General appeal because lots of you know not everybody in the community even though I do Java mostly uh
lots of C Lots of PHP python all sorts of languages and Frameworks uh folks use and so try to have a book that is at
least applicable to those we've covered books where they use c as the source code or Java as the source code um but
generally it's things like unit testing or design that are more generally applicable so um if you are interested in in
putting forth your uh idea for a book go into the book club Chanel look at the thread for uh the next book and make your
case um even if you haven't read the programers Bane uh but you're interested in lobbying for a book uh you might want
to join our next book club session because after we finish the chapter I don't expect it to take the entire two hours uh
we will spend the rest of the available time talking about the the books we might like to cover um but either way join
join the Discord if you're not already a member uh if you are join the book club if you're not already a member of that
you might have to send me a direct message if you don't have access to the book club private Channel um but if you've
been in past book clubs then you already have access uh and we will be making a decision soon um and then if you weren't
interested in lobbying for any book you can still of course join us uh once we select the book all right so um I think
we were going to connect it to we were going to write a a test that makes sure uh we put the right stuff in the model so
that our our view which now is it the HTML view is looking for song view so do we have any tests for song view the
question so may not be we have to do the old school approach right um You probably want to look for access to the from
method and not song view guess because the only non-test usage is actually from line n the from method so we can just
look for usages of that oh because that seems to work you think it's because of the record is that the issue there is a
bug yeah I mean it's it's like line eight is saying song view is not used and it's 11 so there's all right there's uh
and if you click from there if you go from song view on line 11 at the bottom and you do a control B yeah so it takes
you to the record but if you try there uh oh it does take you so now it seems like it's recognized that it's used it's
just not updating the sort of coloring of it and it's not showing the test because it is used uh the test so that's
interesting all right anyway there's clearly some bugs there I will be filing an issue later today so uh we want a test
where do we be so what are we testing again I just want to be clear um we're testing that this HTML got The Right Stuff
MH yep okay so that is that like a guey test or a UI test no we're talking subcutanous okay so where does song from now
in the HTML who's in charge of so where does that song views reference come from comes from a very similar place to the
success message oh from the it importer test the redirect the um the model the redirects so this isn't a redirect
attributes so how would you how would you figure this out so song import success is the page that we want to basically
modify so what would you look for if you want to figure out who's who's page well since this was already working I would
see who's referring to this yeah you could do that and that may or may not work because it's not always reliable because
intell has sometimes has trouble parsing route but that's only for redirect messages right so that tells you what puts
it in what actually displays this page so what would you what would you look for to figure out what something like that
right so it has nothing to do with the get mapping it has to do with that right there return because that's what is
returning view so this is what displays it um but it doesn't give us 100% telling us what uh what gets put in here so so
um what's interesting is is we get some of the stuff from uh we're currently getting the information through redirect so
this isn't going to tell us everything that that we want to know because we don't we just came here from a redirect so
again we have no idea what just happened the only way we know what happened the earlier ADR right and so um so that
means it's going to be another type of of redirect and so that's where you can say okay well clearly it's going to be a
redirect you could follow the trail of the success message um or you could find where does it redirect to this mapping
so one of the most confusing things in Spring MBC is that get mapping on line 28 can be 100% completely different than
the name of the template that you're 30 so the name of the template could be XY y z and as long as you're returning XYZ
on line 30 it works the redirect would not change because it's a redirect to a URL so the get mapping is URL based the
redirect on line 41 is URL based same for 36 but the template name is just the name of a file and so that's something
that that's like oh looks like they always need to be the same and they do they don't they don't people just tend to
make them the same I tend to make them the same um although I do wonder sometimes if that makes things more confusing uh
but they don't have to be I remember way back with struts and struts to it's like a whole bunch of things had to be the
same and I was never sure which ones it was okay to be different so I just made everything the same uh but it can be
confusing because they don't have to be and so sometimes they're not but that's where it's like is this the name of a
basically an HTML file or is this a URL uh and so redirects are always about URLs get mappings are always about URLs uh
this just happens to be the name of a template right because there's no redirect on this one where it is here yeah and
some people don't use string some people use model and view as as a more typed parameter for these and then it make it
becomes a little bit more clear um I just find those harder to so because we only have the information about what was
imported in line 40 we have to basically do the work there uh in terms of where we're going to do the work and then the
test will be similar for the one we did message so we'll add an additional attribute here so we we will add a new
attribute there okay and what will the name of that attribute be uh songs oh do we call it song view nope it's always
inside the curries so the Cur the dollar curly brace is saying pull in from the model from the from the map whether it's
a redirect attributes map or a model map it it turns out to be the same thing find me the the the attribute with that
string gotcha so this would be something of um right comma stuff right which would be your song song views objects or
BAS the list which you songs so we know how that's going to go songs so T not tsv songs but from the result from the
result yeah so just like we pulled out the result values we basically do the same thing but we'd have to convert them
because that's views but we're running ahead of ourselves because we haven't written the failing test okay so the test
would be off of handle song import which is all in the song importer right so should we reuse well this talks about
putting in repository so should we that the attribute has all of the songs well so this test is saying repository but
that's not really what this test is testing so I think the test name is wrong okay because notice we don't reference
repository ever uh well we do actually do it on Line 39 uh I wonder though if we shouldn't do that there anymore I
actually think we should have lead that because we actually have that now covered with the success message oh so do it
this way yeah and then do we need we do need the repository still Yes although uh I don't remember if we have a uh a
nullable for that but we will no longer need reference to that um so what we want to say is song import results in
success page containing songs imported and again I might sort of flip shows yeah I don't know what happened there with
the name sucess test page it uh so suiga mentioned something about a custom assertion uh I don't think I have the out um
so given this uh it's basically um we might want to just like we refactored before for um looking at the flash
attributes uh we might want to also do a similar refactoring so like do it um success um maybe maybe I've just gotten
into the habit of of not using model and view I'll have to out so this would be well what I would what I might do is is
uh extract that but in in the idea that we're going to reuse it for oh I see uh yes yes I was mimicking this yeah yeah
yeah I was thinking that we might re reuse it but we can't because uh we're going to ask we're actually going to get a
different type a different flash anymore is that what you were thinking yes I might name it a success message from to
make it clear that that it's actually pulling out the success message from that what uh it's asking you to rename a test
method we don't want to rename the test method so just hit okay yeah now does should also add from uh let's look at is
this used outside of this no it's basically asking if you want to rename mes uh method names and we asking uh SOI asks
will the redirect attributes translate into query parameters I have no idea um move this to the so I have I haven't
answered to sui's question since they're flash since they're flash attributes uh the documentation is explicit about
saying um unlike other redirect attributes Flash attri attributes are saved in the HTTP session um so they don't appear
in the URL so if your concern was which I had a concern about is if we import a thousand songs is that going to appear
not um which is comforting so all right sorry I interrupted you so we WR failing test now for yes yes um I guess
actually I want to steal or part but not actually is the list of no yeah so I wouldn't copy that part and I would just
uh I'm not sure why you're oh shoot whoops so I would copy just from redirect attributes to the end of the line and then
we'll let intellig uh here so what I would first do is pull that out into a variable to make it easier on us to do that
W there you go nope it so song views is the correct variable name but the type is wrong right because it doesn't know so
here would be a list of song okay of song View and now complaints and now you can autofix it quick fix to cast method
and you don't have to select yeah unable to extract contains syntax errors oh it doesn't like it because you got a
syntax error on line 48 which is weird because that's unrelated to what you're doing it's weird that it had that problem
um I would basically comment out 47 and 48 do the refactor and then we can uncomment it you don't have to select just do
is that weird oh we can do from yeah there we go that's better inline well will let me inline with the partially oh let
me do that it's like yeah I don't know why it had a problem with the other thing uh interesting because it didn't have a
problem here so who knows all right so now we've got our song views uh what do we expect those like well I guess the
first thing would be there should be so many of there and and how many should they be two memory you're going to need a
I know that's what I'm looking for oh you're looking for the Finish statement yeah what is the Finish again it's not on
my cheat sheet the control control shift enter there we go oh there it is literally the top of my cheat sheet the number
one I wrote it as code completion what did you call it uh so intellig calls it uh complete all it all right so um what
do we think this is gonna do fail because we're not stuffing anything in there yet so what's did we wa a second h no we
didn't so I want a more precise failure prediction um well we've got two songs here before these two were passing did we
change anything that could affect those no so it's only this new assertion so how is this assertion gonna fail it's
gonna fail saying on the get it doesn't know what get is which means it'll return a null object which will then try to D
reference so no well it's just it's just gonna be saying expect actual to not be null but I wanted to get to the point
that that what we get is a null not just zero right so right which would which could have been a reasonable expectation
um but that's why I drilling down to like what is precisely going to happen to uh to think about oh we're doing a get
that attribute is never added and so therefore we'll get a we'll right look at that actual expecting actual not to be n
exactly what we said differently oh make it feel differently oh right what you mean is get the attribute but not have it
right yep ah look at that um and let's make it actually it's expecting a list of songs right yes so you could just put
empty list if you'd like that's what I was going to do is empty list really you got typ it oh I'm not sure why it doesn'
t complete for you but you can yeah collections do I could have swon that that autocomplete work before so now it'll f
saying it's zero not MH not two yep now we can make it I mean we could put in two entries uh but that kind of gets
pointless so let's do the right now we're importing the songs they're in dots values that's a list of songs so let's run
this and see how it fails or will it so it's gonna you think it's gonna fail because what is uh so I think it's gonna
fail um because it's GNA try to cast it to a list of song view so it'll fail it'll fail on the oh did not fail on the
cast and the reason generics but that's good to here now well no no no no it has nothing to do with that it has to do
with the fact that our cast um in our on our is is not really concerned about list of song view because it doesn't
really at at runtime it doesn't know the underlying containing type so it just sees it as a list in yeah which the fact
that the empty list was passing should have been a a a warning that that's was going to happen oh because it did we
didn't say what kind of mty list right and there was nothing that it it could infer because the add flash attribute says
object so which is actually good because what we want to do now is say uh not just has size of exactly and then
basically song views of above so here's where we could manufacture the song views directly um but I'd say that's kind of
pointless uh let's just call um well what this we we could uh we could pull them out of the repository and convert them
ourselves so that so we could do repository uh we findall so uppercase song views Al so all songs gives us a stream so
list a oh this is all songs not song views second from is expecting yeah sorry I'm the can we put it so I think aarch a
also might be confused uh so let's um let's extract the entire yeah let's songs from solista stong view so why oh we
can't say contains exactly with the list we have to say cont contains exactly what's in this list uh I forget what it is
uh so can you hit the autocomplete elements of yeah H that's why because we weren't we what we want to say is contains
elements of this other list not this list contains sense got it so now yes collaborator based isolation is is is what
we're kind of doing we're basically saying we know that the song view from method works because we've got tests against
it so there's no point and not relying on that the fact that we're going to the repository we could go directly to the
parser six of one half do the other we know it's in the repository so that's fine if we really didn't want to have a
dependency on the repository well then we'd have a dependency on the song parser so I don't know six of one half doesn't
the other so what we're saying is um we expect what we get in there is basically a bunch of song views to a certain we
don't care how they're ordered how uh well we care how they're ordered actually because we're saying contains exactly
elements of we didn't say in any order we presume it's in this order um but we basically don't care about the details of
the conversion because otherwise what we'd have to do is do new song View and then basically write a bunch of code that
duplicates the text in lines annoying and prone to error and we don't really we're not really testing that anyway
prediction might work that's not a prediction should work that's not a prediction either uh um I mean you could say pass
we'll pass I think it'll pass and we'll find out okay so I think it's going to fail views so remember we put songs in
there and but we're what we're expecting are song views oh so what we're saying is and what's interesting is like yes
they're very close because of the way that song and song viewer are closely related wrong so let's go fix it so that
should these values are songs we want song views right so funny enough we just wrote in all right suige have a good
night thanks for thanks for your swegi all right so now we now I think it okay and voila cool so now we can run it run
the app uh I might need to restart the app because I think it's already running there is that shortcut that I is go what
is that control shift semicolon what are you working on so there's a bit of an annoyance at least I find it annoying
that um particular uh note what you had to do was we had the Run configuration selected for running IO free tests and
because most of the time we can then just press shift F10 or controlr to run those right to run the app then you got to
select a different run configuration and then when you go back you have to switch it back to to run uh iof free tests
you can keep the Run configuration set to the startup um and then you invoke a different keystroke to run recent tests
and so that will basically always offer you iof free tests and other tests that you've run uh and so you can always run
recent tests without having to configuration but I won I would throw more keystrokes at you okay oh it's a keystroke
only thing got it uh I mean it's on a menu somewhere but there's a the shortcut is uh control shift semicolon oh my yeah
so not at all and I and it was one of those I actually I actually came across it accidentally uh because I was actually
trying to press the um tab shifter to move uh to split the window uh top bottom uh and I hit the wrong key and it's like
oh what's that run recent tests yeah I'm still gonna add it to my little checklist here all test all right so let's uh
misspelled I misspelled shift and you probably can guess which letter I left import a displaying because how is the view
connected again um huh uh that's surprising singular versus that's the test though where's the production importer song
list H do we need to tell it which values no they are by definition and we know that it's the correct number because
we're displaying that that it imported six songs so we know that there's six entries in them um so we do add flash
attribute we're seeing that message um and are there any errors in the oh okay um so what I was going to suggest is what
what are we displaying no TRS or are we um uh or is something else wrong so let's go look at the browser and this is
again where sort of uh HTML tests would would help us here uh and do an inspect and I think we'll find we've got empty
so we are displaying and I bet them yep okay so we are displaying so my first thought which probably was yours as well
is that somehow song views was empty or not being transferred across the redirect we actually know that there are six
TRS so that is so the the each is iterating through all them um so there's a problem with our our our th cells so we're
saying artist song title but we're not prefixing it with song view because these are properties of song view ah so here'
s where you can practice your control down aror if you yeah yep and then just start yep hey bdsl yeah I don't use that
generally unless I'm trying to figure out sort of layout stuff I like to just inspect so I can see the data um because
it's a lot easier to look at the the elements in this case uh especially since they're empty um I'm not actually sure
how much space they'd be taking and good evening rerun and at some point you'll delete line 27 there yes so you could do
a Refresh on this page which will show us that failure of our resiliency um but we we made that second oh we were
running right so what is that error stack Trace I'm I'm gonna guess it what that is that the names we used in rth texts
are not quite down stop uh song title does not view we call it title ah artist title so on song itself it's called song
title on song view it's called title uh how do we feel about that I don't like that yeah um we can rename this view of
I'm good try wh stop and try again or she want to rerun the uh well let's run the tests all are just IO free um let's
run all yeah I'm not sure how I feel about the redundancy either consistency I like this control shift semicolon M must
okay all right uh so I expect because we're not testing HTML um wherever we were using song view uh other than this file
is now wrong so we were using it in one other place so let's look for where else were view uh I wouldn't look there
because that's not gonna find you want to look for the actual string song view right yeah because it's h but not that
string what you want to look for is a is an actual quoted uh you want to look in HTML files and there's not that many
for for song view oh I see so search in files uh somewhere song title release title yeah so that that must have gotten
renamed so looks like we're okay and I was wondering because I think that one so I wasn't sure if intellig would do that
uh it's not it's not always reliable to to renaming into references inside of time what but those are what we did yeah
this is the one that the automated tool did right got it oh interesting so it did actually do it all right cool run the
app again yeah let's we want to see a table with with with our stuff totally and then we're then I think we can we can
say we're done for the day yeah actually I could just reuse it you just import it click the import again look at that
wow not great but okay well I mean it has the correct data we may not like the layout and The Styling uh but it
certainly got the so yay success ship it or at least commit and push yeah let's do that actually let's go to jira first
if I didn't close it I think I style oh we can mark this one is done jir nine that's the thing about our new system is
the jir numbers move around are G are going to be changing and moving around bad all right uh so next time we can
improve the style a bit um we get to this yeah I was hoping we'd get to this too but um what else we get we've got so
was either going to be uh autocomplete or deploy to production um what do we want to do first next time I would
definitely I think I'd rather have auto complete ready before we go live with it okay might even want to remember that
going live doesn't do anything because isn't it still turned off at the production site yeah it just says coming soon
yeah so I mean unless somebody knew the the actual endpoint right which I'm okay with the obscurity yeah but um that's
fine either way so in that case yeah we should it'd be good to get up to production I I think we should get it on
production because that will uh get us to um setting up the database and then setting up our continuous integration you
want do that before autocomplete I'd like to do that before autocomplete because the way things have been going is is
features take a while um and I'd like to be able to I'd like to be able to see it yeah so set up database what else were
you saying uh GitHub actions for build it yeah I'm thinking I might like these yep all right so we've got our plan for
good enough yep anything else you wanted to add nope hit to commit and push we keep forgetting to push at the end of the
session that's why yeah we've been like saying it out loud commit and push uh it's running all the tests I think we just
have and then dis tests and then have to say push considers uh disabled tests as failing in this regard ignored tests so
they're ignored does that mean it actually didn't this well this is got to go to yeah see now it says commit anyway and
push uh can we change a what is the what does the circles the refresh icon do there oh reruns commit checks can we check
the the settings on that and the right um I think that's wrong I mean I under I can understand it but I think it's wrong
for it to consider that uh preventing pushing um so just say commit any way and push I guess even though do you think
there's a setting to say uh ignore ignore because basically I don't is this more no all that does is basically which run
configuration do you want um that I don't see anything else off hand I'd have to look a little deeper unless it's in
Project settings um I honestly think and and and bdsl is alluding to this is that once we have the GitHub stuff set up
it's going to run all the tests and then we can stop doing that at every commit because then what'll happen is we'll
just run the tests as we normally do and if we forget to run all the tests oh well when we push all the tests will run
anyway uh and then this will stop being a problem or we yeah see but right now we don't have I mean we're not pushing to
production anyway so the sort of doesn't matter so we could turn it off anyway all right so thanks folks for hanging out
uh and uh giving us uh assistance when when we needed it and asking good questions we always appreciate it uh and so we
will see you next time so have a great whatever rest of day is left for you
