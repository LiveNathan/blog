# ＂Song Themes＂ Episode 17： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=cngjYV5oR1w

---

## Transcript

all right hello folks welcome to episode 17 of Mike and I pairing on on his song themes app how's it going Mike good and
you all right doing well yeah I was looking at uh cleaning up the playl list making sure everything was in there and it'
s like uh wow 40 42 some OD hours so basically almost a little more than a full weeks of work although I don't know
anybody who would well I I do know a lot of people who would um pair for 40 hours in a week uh but that would not be a
typical work week for for me even in a full-time role you're going to have time for although I was reading about um so
uh Nat Bennett who's a who was a pivot who worked at pivotal Labs been writing this um email sequence just sort of
reflecting and and retrospecting on on time at uh pivotal um and one of the recent ones was was the work hours were
pretty pretty strict um you pretty much were working nine nine to six uh and I remember that was one that was one of the
primary reasons I I got an offer but I didn't join because I'm like I gotta drive my son to school in the morning and I
can't get here by you know to the San Francisco office by by 906 um and even more so one of the things that that struck
me was here we have one of the most productive ways of doing development pairing but we're still going to work you 40
hours a week and like no benefits acre to the employees for were being way more productive than a typical everybody
working on their own and and not really collaborating kind of thing and it struck me as really like not in the spirit in
my mind of of agile like to me it was just like we're going to get more out of you and you're not going to get any of
the benefit and I'm like so that you know that that was like you know yes you get the hour off for lunch um but you're
working three and a half four hours of pairing you know in the morning session and then the afternoon session and that's
rough like I know people who who burned out from that um but again it's for me it's like we are so much more productive
when do we get the benefits right and this is you know very much the the uh the the Rebel in me that that bristles at at
basically being exploited right and you know people say like you know we're not uh you know we're highend knowledge
workers and we get paid well like doesn't mean we're not still being exploited great because I think if you're pairing
consistently and as as the dominant way of of of as the primary way of doing things um you shouldn't have to work 40
hours a week 30 would be actually as 30 hours consistently pairing and doing all the XP practices that they do did um 30
hours should be fine and so maybe even like take a day off right like get you know okay maybe that's hard to coordinate
but fine so let's work 10 to four like allow people who have families to spend more time with their families and so it's
it's I don't know it it it so upset um about about the fact that I couldn't join a company that worked exactly the way I
wanted to work um because of this arbitrary uh limit and ex and exploitation well it's interesting because a lot of the
um you know they have those lists of companies that um get more so much productivity per what is it Revenue divided by
oh Revenue per employee yeah per employee right or profit per employee depending on how you want to look at it yeah
right right and it's like almost all of those are software companies well yeah I mean yeah many of them are because you
know what what has the the absolute most Leverage is is soft is is Tech right I mean we you know it it you know yeah
it's that goes to you know the the typical thing that that you know goo and I and others say it's like you know it's
despite the fact that most software is terrible um because it The Leverage is so incredibly big it doesn't matter and
that's why there's no pressure to to there's no real pressure to become better because it's so incredibly profitable
that why bother right 100 times we're making 10 to 100 times of what we're paying you why should we bother making you
more efficient or happier I was coming at it more from the angle good point um but I was coming at it from the angle of
you know why not throw the developer a bone for doing things like agile or you know pairing or ensembling because
they're profit per employee is so high exactly yeah like why you know money is you know certainly during the height of
of the the pay scales you know a few years ago um you know you could get five six 700k as as a reasonably high-end
developer working for for a big tech company um especially if you incorporate you know those high price stocks um but uh
but the but flexibility there there's there's definitely value in that there there's value to the employee and and
absolutely no value and it's in fact looked down America uh and so so Jeff says uh yeah like why can't we take a long
lunch why can't we work six hour day 6our days why not we're we're not only are you getting more than than I mean I don'
t know to me this this was the whole the whole point of of becoming more efficient and more effective um more free time
was yeah like but you know that stuff I mean and let alone 40 hours like most people you know some of these companies
you know many of them were working 45 50 60 hours um and I just think that's that's exploitative but anyway good evening
Master good evening hello tokes welcome all right with uh with with that rant out of out of the way um should we get
back into song themes sure let me make my screen right uh did you want to zoom in again yes right because we were pulled
out for um ensembling was it 125 or 150 that you all liked uh I'm fine with 125 okay but if any anyone needs the font
size bumped up let us know yeah as you can see it's really easy people so uh last time we left off we had some
difficulties because we uh added security and got all that working except one of the things that we didn't properly set
up are the um requests being authorized for things like errors and forwards um and that's where we were like why isn't
this working it should be working and realized we were actually getting an error uh because our input was wrong um but
we weren't seeing that because the error Pages didn't have the right permission so I recently so I did some research
after I like oh there's this really cool nice way to do it which I don't know this is one of those what are good
defaults um so not having permission right not having default permissions for error pages okay maybe um but not having
default permissions open to everyone for forwards uh which is part of the the cycle that that uh that spring MBC will do
seems not like a great default um so let's let's go add add that in uh so you got that that uh that line the dispatcher
type mattress so what's nice about this is I used to in in fact I got to know now go back to uh some by code and add
this in um unlike specifying an actual path so let's go to our uh yeah or security config so unlike specifying an actual
path like we're doing here in the request matchers what we can do is we can actually um because we could add a request
match for slash error like we did and and then actually it's slash error slash star star or something and then for
something else but um it's a lot easier to just say we'd like these types to just fall through uh so you want to put
that above the request matchers okay not that that's required it's just generally you do that first yeah you can you can
go ahead and import those the second one I assume the second one yes yeah oh interesting uh unless it was the first ones
so this is this is my pet peeve with with the spring doc mentation is especially for things like this um and this is
even worse in in some of the other static Imports it's like could you tell me which package this is because it might be
another package um I assume it's that but maybe it's not it only two actually what did I just delete did I delete yeah
so then the other one is Tom Cat the other one is I thought the other one was Jakarta oh oh right J Carter um I mean
it's it's coming from the the Tom Cat thing which is why I'm I'm leaning towards it not being uh unless the author
authorized H let's go look at the at the docs for dispatcher type matchers do you want to share screen on your end uh
let me look for it first and then I'll come say interestingly the the docks that uh don't even have the dispatcher type
in it um let's see so that's that that's um the there there sort of two different competing document documentations like
there's there's a documentation for um that's uh under Spring Security and then there's stuff that's that's under uh
spring framework and and other stuff but let's take a look at dispatcher type yeah that's an enum it includes forward um
so let's let's import that again because yeah that's that's web serlet dispatcher type and then let's look at the error
maybe we're misreading the error so it's the the first one spr can't it can't understand that which is weird because
that's exactly what dispatcher type matchers right that's what we're saying so one thing I recommend that you do is uh
if you go open up the maven um where's your M it's so weird I don't know why why stuff seems to disappear for you that's
I know it's a weirdest thing yeah um just uh use the act action to find it yeah yeah is there a pin they should
automatically stay until like you do something to make them go away and what am I looking for and Maven um if you click
on the thing that has that little down arrow the third icon over from the left and you say downloaded sources and
documentation the last one um that way it won't try to decompile the code you'll actually get the actual source which is
going to be much more useful than than the decompiled source right oh as found the celebrate we don't have anything to
celebrate yet I'm going to reject your your your celebration as can't celebrate anything until we've actually figured
this out then we'll celebrate oh you're celebrating the celebrate redeem well you'll have to try it again um so let's
see so why why might that so we're doing authorize HTTP requests we get an authorize and we say authorize uh. dispatcher
type matchers um I don't understand why it's not accessing the second one which is basically dispatcher dot I wonder if
intellig is compile you can just say re build project yeah because intell basically is implementing its own compiler um
so what's it saying so no suitable method found for dispatcher type matchers uh why is it not applicable we literally
are passing in multiple dispatcher types dispatcher type cannot be mismatch oh interesting so um it actually looks like
the the first method that that it's trying to match against that uh it takes a so actually it is the Jakarta servet
dispatcher type weird because we appear it's saying the framework well it's saying it's no you can't find that right so
can't find dispatcher type matches that take web serlet dispatcher type um it did find dispatcher type uh vogs the
second one one down there meth with the second method one that's no the next one that one hi this one so that one is
Jakarta serlet okay didn't we try that and that didn't work either thought we did um so let's try that so delete the
import for the I can't believe this is I don't understand why um Alt Enter there we go Jakarta yeah okay so that does
work maybe we didn't try it I thought we did but that's that's really annoying and and and this this has happened
several times in in different places in Spring um where sometimes it's building on the standards the Jakarta standards
what used to be called J2 e and then was whatever or j2e um but in the docs it really needs to call this out uh because
if there's multiple choices and especially if there's one that's I think is quite reasonable which is the web serlet
stuff I don't understand what those are for um maybe they're they're used for something else all right anyway so so now
we've got uh we're specifying that we're okay with um any forward or any error all so um I think that's all we wanted to
add that took way longer than it should have so rerun the server and test uh yes okay uh oh there it is uh you can also
pull out the slash error in line 19 for the because we're not yeah I was gonna ask you about that that's so that's
that's now that's as oh my curse is in the wrong and I need to document I got the weirdest problem with chrome is
whenever I open a new one it leaves my book Mark toolbar visible even though it's set to not show the toolbar of course
and when I change it it only changes it on the streamyard others software quality yeah I guess particularly problematic
with that so Local Host and we'll do song import uh let's just go to stra yeah let's just try things out okay um let's
go uh yeah now now let's go to the to the import we do a quick theme search defaults yep now you gotta log I have to add
to my prep checklist no I did take I did wanted to make sure I was logged out of computer it doesn't handle well it does
it just makes it read only kind yeah one thing that's that that's interesting is uh if you create the user like we did
um there doesn't seem to be a way to specify how they log in and how they authenticate um because I don't I don't like
the email me a code thing right what's interesting working one more time invalid legit it's not trying to use my kind
work interesting so it's using my password for my kind account because I have a separate one for just as a user let me
look at the time stamps on those ah okay I see what's wrong this one's old oh okay I'm gonna edit that it okay cool I'm
back all right so let's uh let's paste in what we tried to paste in last time where we actually got uh the error well I
know what I did wrong but let me close off the columns I deliberately opened them because I was taking a look at
something and there's also these two and I forget were we including contributor or not I think not no but what I want is
I want is I want for you to paste something in that causes the error that we saw well the error we had was actually a
user error on my part right and that's how I want you to create that okay so that's the question I have so let me go
back to the code what are how many columns are we looking for so we're looking for nine and I think you were pacting an
eight yeah so okay three four five six seven eight yeah so I was left out contributor yeah so so leave out contributor
all right so we are now uh seeing seven columns but must have at least nine so um now we're at least seeing the error
page uh and what's interesting about this error page is that it's showing up because um we we threw an exception uh but
it doesn't because we did this on a post and the exception was thrown during the post um it looks like the URL hasn't
changed because the error page that gets generated was returned as a response to the post and that was what was
confusing um that was what was confusing me last time because generally what I see is is uh there'll be some kind of uh
if there's an error then it will actually you'll see you're on the error URL and technically this is returning the
endpoint sort of information from from the default error that gets that's bring creates um but we're not seeing the URL
change because it was done in post um so um let's pay the right amount but then I think we need to to better handle the
yeah 5G technician uh do you use authorization annotations of put that in the security config I'm not sure what you're
saying I've put that are you saying are we using authorization annotations on the post mapping or you saying something
else so perhaps rephrase your question so I could better okay all right nine Columns of data all right interesting uh so
you had a blank one two three four five six seven eight so you had a blank song title right so oh I see I no see what I
did wrong here yeah it was so wide that I didn't yeah uh so by Spring DSL if you mean the configuration authorized
requests um you may have missed it but we were just working with that when we'll show that bit so it went through it
went back to the uh the homepage right which is what we what we programmed it to do y yeah um I suspect though that if
we try to do a song search for any of those will that will work uh so let's look for something that was actually in a
theme protest yeah as you were yeah as as I more no Okay so we've got two issues which do we want to handle first we've
got the terrible validation for bad user input um and we've got uh what's a deeper issue which is um when we add songs
they we're not able to find them at at from from the from the UI I think I would go it deeper first because I already
did write down over here in jira handle incorrect number of columns okay all right since we last spoke okay um let's
check out our tests so what what are our our um what test are are we missing this here so it' be theme Searcher test is
having is missing something um well it wouldn't be a test from the level of the adapter right so this would be um
because the the adapter is just passing it along um but it's passing it along to the application layer so this is an
application layer test um that we we might be missing because we've got uh so it' be a song service here right multiple
songs added are found by theme yeah so this is this is um if we look at the application startup class how does how does
it startup so again I recommend not looking at the project oh yeah yeah startup yep so we're stuffing yeah so so we're
basically creating a new song Searcher from scratch without involving anything else um and this is this is basically
more of a configuration problem than anything wrong in our in our code um and typically when I find problems of this
kind it's usually because uh because of of this now we could write a spring boot test um that would be kind of a an end
to end like test to make sure that that our configuration is is set up properly uh or but it's it's it's a little
awkward um or we could just or we could just fix it oops um it's awkward um in what way is it awkward I guess is my
question uh like is it so awkward that it's not worth the effort and just fix it or um we can we can for it some value
we can okay so let's go into so you'll probably have a startup test in fact not probably I know you have a startup test
so let's that test uh you know end end to found can you reformat that file I uh by default for whatever reason I think
uh the spring starter defaults the two two space indents I've noticed that there's some files that are like yeah so
reformat with the letter L that's pretty much all I remember let's see ah there it is control all2 all right and this
one this one is like looks empty but test connections or wiring would that be a right way of saying that uh I'd either
use the term Auto wiring or application context setup but Auto wiring is probably easier yep I could just totally see
someone like oh that's empty let's just delete it yeah yeah uh so let's um speaking of Auto wirring let's uh create a
couple of them so create one field which is the uh song service if you say at autowired uh and I usually put the
definition on a new line yep then declare the variable yep for uh the song searcher it's the downside of all these
things yeah I think that's good enough uh so let's so what we want to do is is basically do what we do without the UI
involved so import a song through via the song service and then assert that it searcher it just um yeah just tsv yeah y
now do we have a tsv we can steal do uh so it's not finding anything because you got capitalization and words on yeah
yeah oh interesting so that actually I was using PHP storm you the day it looks like intellig moves it between the two
oh interesting the setting the setting sticks across sticks across it looks like I'm gonna check that out later but yeah
I'm I'm I'm dubious that it does that but um because I don't recall Us in this project I don't know whe we found files
very much but anyway that's true um go that was that yeah so we in in our book club we were talking about using
flashcards for for learning um and uh because uh and yeah I think uh asra do you need a flash card that tells you that
flash card is the word you want for this um shortcuts are interesting because initially you have to know them sort of
explicitly in the sense of okay this is alt you know control L for this thing um but eventually you you want your
fingers to form the Habit without consciously thinking about what keys you're pressing which is why when everybody says
what keystroke was that I have to look down at the keyboard and see what I'm pressing because I no longer uh because now
it's um you know people use the term mus muscle memory yeah um which of course the muscle itself doesn't have memory but
there's there's aspects of but it is a different kind of memory that that's being used and and um but I guess flash
cards would be useful if you if you want to start that process of what's format okay it's you know control Al L um and
so if you know that right away then you can translate that to your fingers and then you can stop using the flash cards
the other thing is you could have the flash card just say okay press the right keystrokes which is what of typing tutor
like things do is they'll they'll um then then that's more realistic uh and I wonder if there's an explicit typing tutor
like thing that will allow you to say okay press the right keystrokes for auto format press the right keystrokes for
extract variable and see if you you've pressed the right thing if not I might develop one because of course I need more
projects to work on so now I'm looking at this oh sorry we got to yes well of course well you're seeing tests and code
but you're always seeing tests yes absolutely welcome uh so yeah so let's um so I scr I grabbed that from the other test
great now it's interesting though now my brain is like wait a second I thought we were looking for nine columns this has
got one two three five six seven eight nine 10 yeah because remember we ignore everything after after right right right
so looks like we still but we still are expecting it which maybe we don't want to maybe we want to be more flexible
about that actually I think we're gonna have an issue because I was importing with notes missing well this is the other
problem we got to fix well yeah I mean and we talk we we've talked about sort of more flexible understanding based on
the column headers and that that might be something we do sooner rather than later I think very quickly if if that we
will probably see a bug because if we're pulling in 10 columns it's going to be off by one so if we have something with
only one theme and there's nothing in it it won't find it right yeah right okay and that's extra new problem okay but
let's make this one correct actually I don't know we'll just okay this is really set up um and then we're importing the
songs and the goal is to make them visible yeah technically actually there is no setup that actually is what we're
executing and then we're going to assert so um the setup is done by Spring boot uh so I'd put a blank line at up top
even though that might look weird uh we could put a setup which is so foreign to at least to me to have like no setup um
but is fairly typical for a lot of tests that I see in the wild because they put all their stuff in a setup method or
even service there there we go oh no no song song uh the song Searcher Searcher but is is Searcher exposed or do we go
to Searcher through the service we're going directly to the the Searcher okay I think well let's go look and see what is
what does the front end the think I forgot the name of it that's no results import no it's well we want the controller
class and this is the downside of of not calling it necessarily controller um but we know it's going to be in the
inbound adapter so at least we know where to look so it is a song theme Searcher do yeah that has access to the song
Searcher okay yeah so song Searcher doest by theme wait a second song titles by theme are there two methods there it
looks like there are um that one's that one's in the wrong place and we I think we we we knew about that going in that
that that was going to have to move uh to somewhere else which which that song titles by theme or yeah because we you
know and and this is one of those well it depends um this might be reasonable uh but I see whenever I see string as a
return value from a from a domain object um I always get concerned that maybe that really should be presentation right
which would then be in the adapter right yeah yeah got it yes but for now so if we were doing it a little cleaner we
would have what the servers have something called song titles by theme that Returns the string or the adapter well it
wouldn't be it wouldn't be the service that does that right because the service is still inside the hexagon so it still
doesn't know right so any anything about converting domain objects to the outside world is is adapter adapter which is
right so we would use by theme and then convert and transform whatever whatever we want um while we're here uh or while
we're thinking about it uh can we jump over to to let's make an entry in in Jura um that we want to uh move song adapter
I me we had just done that temporarily just to get something going in in the UI but we'll we'll also need to explore
what you know how we want the UI to look right um but for now we can one should just be a string oh reest theme right
right yeah we have there might be a little bit of of obsession there but we haven't gotten yeah yeah so I guess our
theme is thank you that's what it looks like okay actually this might show up the problem that we're just just I'm
expect I'm I'm hoping it does yeah I think it will I'm hoping it create reproduces the problem yeah okay so the by theme
returns a list of strings so it should be well this returns a list of songs but right now let's just say that it has one
one yeah and let's run just this uh I don't know if you have uh a specific one for for this but let's just run this test
directly just this test directly yeah okay yep yep so this tells us that our our configuration is is uh misconfigured
that the fact that it failed yes because that should work I don't think so why don't you think so because there's only
one theme and we have an off by one error one two three four five six I'd have to look at what word I thought you copied
this from a test I did that worked oh right that's true I did copy it from test yeah because we want this to be valid
correct data because what we're testing is if we import do we find it and it's broken because we've misconfigured the
application I see got it right right right if this was what I had copied and pasted into the edit box that's that would
failed that would have failed that would have well depending on which one you pasted yeah yeah but this is what we want
we want to actually recreate the the the bug right which shows us that uh in our uh song theme Startup configuration
we've we've messed up so yeah okay so what did we do configuration wise so let's go to our startup and uh what we want
is our s Searcher needs to be created properly right because right now it's yeah hey there Joy be welcome thank you so
um let's basically delete that code because it's all IR relevant or at least it's irrelevant now it'll be interesting to
see what test that breaks if any I expect it to not break anything uh so let's just instantiate a Searcher uh it's
probably a create method right yeah um H is this the right way for us to to create the song Searcher yeah let's jump it
we got oh this is private and then this is the factory right we've got two stream oh nope there's more than two yeah
there's a couple I think uh is that that one for for tests so this is this was um a design problem that uh that at some
point I figured we'd address um is that who is who who holds the data because right now song Searcher is acting as an
inmemory repository that is searchable in a very specific way um and that we load songs when the system starts up from
the repository but in well if you say repository it really map repository repository yeah this is not the repository I'm
talking about ah so the way the way the system is currently set up is song Searcher is an in-memory uh cache searchable
cache of our songs right right but there's no connection between this song Searcher and the song repository not directly
so let's go look service right so when we create it the first thing it Searcher so um this is kind of bad because uh
well from one point of view it's kind of bad from another point of view it's exactly what we want so song Searcher is
not something that actually should be publicly accessible and it shouldn't be injected into anything and so um the
question is is is uh is song Searcher being injected into something yeah it's being injected into into our into our our
Searcher controller so it could actually do the search but really that's incorrect right a song Searcher what package is
it in let's scroll up right it's in domain and it really shouldn't be direct so domain object in fact we if we're not
running Arc unit test we probably want to domain objects should never be injected into anything right that's that's the
rule they can be accessed they can be found they can be instantiated um but they should never be injected should pull
this up is adapters shouldn't shouldn't hold on to them because their content can change and they're really not uh
they're they're supposed to be more temporary this one is again this weird thing um and you think it would be valuable
to throw up the hexagon diagram to look at it in that context no I think there's a there's a deeper issue here and and
we need to to make a decision on on what do we want to do but I think right now we have to we it so um we need to stop
exposing this as a bean so just immediately take off the beam for well so if we do that then we can see what what breaks
so um just this being right yeah okay uh just delete the whole thing typing is cheap um I expect I think it should still
compile I expect though when we run uh run the application that it will fail because it can't find yeah it can't find so
I ran the application test only not yeah the yeah any any spring boot test would basically try to bring up the
application using the the configuration the full configuration and it can't find it because the um the song themed
Searcher so this is the awkwardness you were alluding to earlier um no I Wasing to a different awkwardness a different
awkward okay but this is but the the problem we saw before of of getting a a list of songs by their title as a string
this is sort of a symptom of of all the same thing uh so let's go to our our song theme Searcher and I think you're
going to want to start learning the control n and not control shift n oh because otherwise it tends to find all files
and they probably aren't the ones right you generally want you said yeah aning thing about the shortcuts is all the rest
of them are control shift like so all the other ones up here so here this is control in this is control shift in all
control in other words they're all no so the pattern the pattern is the m you probably want is just contrl n if you want
also files and it's control shift n if you want also symbols and it's Control Alt shift n right so it's added the way
they think thought about it was adding on more meta keys to to expand your search but generally that mostly what you
want is control n the other thing is from this dialogue if you if you type uppercase instead of lowercase you have the
advantage of you can type STS and then a lowercase e and it'll narrow down much more searcher yeah I think for me the
two I use the most um is action and unfortunately files so that and that's why I think I had the little mental
disconnect yeah yeah between the two okay so we're at so let's uh can we service you want at the bottom maybe um also or
split right uh yeah maybe split it right actually okay so if you drag to the center of the screen drag drag that tab to
the center of the screen that's not the center of the screen center ver Center and now go to the right now right so you
can see the background blue changing as changing right yeah far as sweet uh so what methods do we have what actual
methods do we have we've got search by theme and that gives us a list of songs great because that's what we should be
talking to right so uh so let's let's fix our song Searcher um not this one the controller the s song song theme
Searcher oh guess we lost that one uh command e is your friend in this case yeah or control so we should be injecting is
the song service not the song Searcher so let's change the the top of the file let's scroll up a bit more just so we can
see the yeah so we basically want to delete the the field and then uh we can change the Constructor right B It Off in
fact I might just delete the whole Constructor and start all over because want so let's create a final field I think
it's easier if we create the final field and then create the Constructor to to do that service y declare the variable
and then Alt Enter on it now on the red got it quick fix add Constructor parameter nice right so it generates the
Constructor and assigns the variable all at once got it um and so now what we want is uh we want to fix the compile 25
so on song server and whatever it it does whatever method theme uh and then we'll need to to stream it and and map it so
that we get we get out a list of songs oh right because the left- hand side is a list of strings yeah do it all in one
line no okay do it on new line it's okay I was well I didn't mean line um statement oh okay yes we definitely I mean we
could split it out but there's no point to that uh so we'll we'll do a map uh and we'll just do uh song colon colon
title because that's what we're originally getting song title S list uh and actually we could if we wanted uh inline
found songs there on 29 so it's all one big map oh good lord that actually would reduce a little bit of the redundancy
so let's let's actually do that okay so so just inline inline here yeah oh wait there two references why are there two
references it's referring to the first one on 25 that's weird if you select the all popup oh there's something that
we're we're that's out of sight so Let's Escape out of this and scroll down a bit Ah okay so it's using found songs to
see if if they're if it found any or not is we could switch it to using yeah let's switch it to using song views because
that's more technically correct songs y uh and now we can delete 28 and 29 it's unfortunate that that it didn't realize
yeah all right so basically we we find the songs by their theme but we're getting a list of songs from that then we
stream it then we map from song to string and then we map from string to song View and so that's a nice nice clean uh
stream pipe there and song view new yeah that's the Constructor ah okay because it's a record that uh I mean we could
make a static method but it's it's the only parameter to the record right right right should we run yes the stream API
is nice tests assuming we've configured things properly and I haven't forgotten here oh right because we changed the The
Constructor type so this should take the the um this should take a song uh like that or no take a song we need in we
want to create null or yeah in this case because we're in a test we can do a create statement so this is going to break
because we said create null but clearly we're passing in songs that we want to add so we'll have to we'll have to
welcome hello hello so I expect this to fail for the songs theme Searcher tests yeah so those fail because uh we still
have some issues with auto wiring that we'll have to clean up um but the song let's let's Attack the song theme Searcher
test because that's more an actual problem that we bottom uh so what we want is um when we create the song themes
controller our expectation is is that we're going to add uh uh songs instead of um uh basically instead of ignoring them
doing so you're saying this go to this yeah so right now we need to fix this because this is not okay so I think song
service might have some other convenience methods for us so instead of crate null maybe it has convenience no I think we
can just uh right no this it's used in a couple places yeah what are you looking for I was just trying to understand
what okay so we just but this is a generic one you know creating no sorry wrong term it's creating an empty song service
correct um this is we want to create the controller do we want to just add and now we adding the ones from the parameter
oh yeah uh so we can't add multiple songs because that's an array uh so we need to it and you could use a for Loop or
you could use uh an arrays uh stream but we can let's start with a for Loop so what I would do is say songs. four that's
what I was heading towards yeah just a straight up one just a straight up one and then just call add song and you can
ask it to what would the uh stream version look like if you click on the four on the four Ah that's where that comes in
um so you could replace it with a four each and that's what it looks like there on the right it's basically AR raise.
Stream So now run the test again now let's run the test again yeah yeah so suige uh the history of song view is is um it
only ever we only ever had strings but we're basically getting rid of that uh so that's why we haven't created a factory
method for it um but agreed that we will want song view to to actually take song and not just the title but we'll get
there yeah all right so um now it's Bean problem right so uh let's go find out who's still wanting message so whoop stop
so what we're looking for is is the whenever I'm scanning these kinds of Stack traces I'm I'm sort of hopping to right
my beacons right to use the term from the programmer's brain is the caus by right because we're looking for one of these
one of these cause buys is gonna have the right information in the in the right uh amount of text that doesn't um this
is just saying that that song Searcher is not available so who's did we just miss it in the top exception so let's
scroll back up to the original throws so generally you can skip past all this at stuff because we don't care about that
we care about the exception message and that's so so we want to jump from Beacon to Beacon and oh uh are we doing some
Auto wirring in our song theme startup tests we might be yes that's why it's our it's our actually test that's wrong uh
so let's get rid of 19 and anymore oh this is an older test no this is the test that we've been but we we don't need to
we still need the song service we don't want song Searcher anymore because that's not something that should be autowired
ah and is this St that stays autowire now we're using it so we need to fix our test because we shouldn't be using it um
service no just the variable the field method all right now let's run it again I think it should work this time well we'
ll certainly not get the dependency both probably because this one was looking for so any test in this test class
because the test itself is annotated with um spring boot test will always do the full configuration that the application
would do uh it is slow why we had two errors that's why we had two errors that's right because both were trying to do
the same thing create an application context and wire things up so yes woohoo yeah awesome so that makes me feel much
better that we've now uh we're not accessing the domain from our from our we're not injecting our domain into our
adapter think we're overdue for committing what do you think uh well I did say commit but you might have missed it so I
said oh no I didn't hear it okay okay this yeah so what I would what I would probably do is we probably probably should
have done a commit after that one is is uncheck all of them and then just check that one because that one's independent
uh and then just say uh all uh sorry not forwards and redirects commit um what did we Chang in the song import HTM that
was actually last week we didn't do a commit at the end of oh right because stuff was still broken um so just added yeah
we'll just add that to the current commit okay um so we want to do is check all check changes uh Y and imports them and
we fixed configuration sort of fixed architectural configuration Searcher well it's so song Searcher is adapter yeah we
added a jur for that swegi yeah because like oh we shouldn't we shouldn't do that we actually have had that J for like
weeks and weeks um but you know it could push down as that enough or is there anything else uh I think that's it okay
cool uh so stupendous follow 65 said shouldn't It Be song service imple I'm not sure if you were joking or if you're
trolling or if that was a genuine question so you'll have to let us know if it's genuine we'll definitely answer it so
don't yes if yeah if if this is a genuine question let let me know if it's just haha um then then we'll we'll laugh you
all right so um now we can go uh yeah we can certainly check off jur 57 there so close close J 57 um uh would now be the
time actually did we actually did 66 right in order to fix that we actually had to had to do that oh right um I think
it's time to take a break oh goodness yeah it is so we come back from the Break um I think we can now focus on improving
error messages uh I think the arc unit checking oh maybe we could do that too but definitely want to want to get some
better better uh validation than yeah and are there any questions we have to we can answer after the break uh so astd
have a good night I know it's late for you oh yeah good night um and we'll definitely address this because I think this
this is you're right this it's very common to see uh imple at the end of stuff so so we'll definitely uh talk about that
after the break yeah all right so we'll take a five minute break and then when we come back we'll answer that question
and uh continue from where we left off great me five all right so um reminder for folks uh per that uh tomorrow I'll be
on uh Mark's Angel lunch and learn uh it's lunch for in in my host's time zone uh 12 pm I guess it's central time um but
it'll be 10 a.m Pacific and 6 PM uh UTC and if you go to this link SL td- game- lunch uh I'll basically be talking about
uh my tdd game it's history where it came from why I think it's important uh at least the process that I use and that we
use here on on the stream for doing predictive test driven development uh and then I'll run through the game sort of
show the different different cards and different things uh and how you can use it uh in your team or organization to um
talk about tdd even even if you're not doing it to talk about maybe what are the benefits or what are the things you you
run into when you're not doing uh test driven development so join me tomorrow for code I was muted of course um uh the
bit.ly you were just showing does that uh selectable from twitch and YouTube no okay got the link into the comments that
way it's easier to copy and paste yeah so just a reminder um that is not a link to join some live stream you have to
register first so don't wait until two minutes before the time starts to go and register you will not be happy uh it
will be recorded but if you want to join live and I'll be taking questions and and having discussions um later all right
so there was uh before um our break we had we did have the question about um shouldn't shouldn't song Ser shouldn't
there be a song service imple I don't know if you want me to answer that or do you want um I can I can start um it's
sort of like um if you're familiar with uh Hungarian notation it's kind of like sort of a somewhat Hungarian notation
kind of approach where it's saying oh there's definitely an interface called song service maybe even horrifically called
I song service um well and C they got to do that but whatever yeah c yeah C++ though did that as well um I remember
doing that in C++ having eyes saw and service imple and you'd have imple for everything the one of the downsides of that
is what if you want to um what I always think of it is I don't like to call my interfaces a name with the word interface
anymore because it lets me refactor easily to it going from being an interface to a concrete class or vice versa yeah
without having to change names all of a creation and then the codebase have tons of files being changed right so that's
the one that jumps to my mind probably and the the way I look at it is is if you can't come up with a specific name for
your concrete implementation um why do you have why do you why have you defined an interface at all um so so typically
my rule is is is is the you know you got to have at least two concrete implementations one of those might be in tests um
before you know you create an interface now that's a general rule there are times when I'll just create an interface
because uh I think it's useful to capture an essence or capture an aspect of of an implementation uh so I might have a
very large class well large large for me would be like you know 10 methods um I might have a class that doing a couple
of different things but only want to expose some of that behavior to a certain client uh and actually just did this in
my ensembl when I'm working on uh The Ensemble timer uh there's a place where uh I only need to handle ticks that are
coming in from the outside um and so I expose that as a very small uh interface actually say the way around starting and
stopping a timer um it's either stop and start it does other things um and that's accessible to other places but the
interface is is showing just a a slice of what it's capable of um and uh yeah you couldn't do that if you had you know
interface name and then imple for the exact thing yeah because now you're constrained to being onetoone mapping yeah
versus a concrete class could have multiple interfaces exactly exactly and so to Me song service imple means somebody is
not aware of what they're doing uh and that's fine for for you know when you're just starting out you know what what do
we do we copy examples the problem is that's a bad example um and uh what we want is even if you're going to have one
interface and one concrete implementation let's say that that's you've determined that that's okay there should be a
name and a and sort of a reason for that concrete implementation to exist it's Concrete in some way so for example I
might have have you know timer as my interface and it has stop and start and then I might have my uh spring schedule
timer as my concrete implementation what's special about it what's concrete about it it's using Springs at scheduled
annotation then I might decide oh actually that's not great uh that's overkill for what I need let me go just create my
own thing that happens to use um an Executor surfice and so then I'd have an EXE service timer and so the idea is that
the timer captures the essence of what this thing needs to do and then the concrete implementation captures in what way
was it implemented yeah so sui's example of of clock and system clock or right there's there's a system clock there's a
a um uh what is it a manual clock where you manually Advance time if if that's something that's useful um so I often
like if you if you can't think of a good name other than like just tacking on imple um rethink of of what you're what
you're trying to do maybe the interface name is not is not a good a good name but finally like why if if you're only G
to have one concrete implementation do you need the interface what is the purpose of that interface and that's to me the
the main problem that I see is is all of these you know especially spring boot examples um but lots of other examples is
why have why have an interface create a concrete class and use that if you're only going to have one interface and one
concrete implementation what's the point of the interface again there may be a need for it you wanted to really provide
a narrow view um but if it's going to have the same methods in both then there's really like what's the point and if
later on you need oh actually now I need uh you know I do need my system clock and my manual clock for for for testing
purposes well then you can extract an interface that's really easy to do and it's automated yeah so easy it's automated
yeah as as swegi just says it's one in so um it's important once you sort of get Beyond Nova stage and you start
thinking about how you name these things and what roles do they play uh that's when you want to really pay attention to
naming of of classes am I just tacking on controller because everybody else does am I just tacking on imple because
everybody else does am I just tacking on service because everybody else does without really thinking about what is and
you know we always know that names are hard and names are important uh but you really want to to understand why are
these things named that way and it goes to to packaging as well why is there a package for exceptions that makes no
sense to me yet I see it in Project after project I see projects that have uh packages for dto and that makes no sense
to me either packaging is a way of of putting things together that are cohesive for a use Point not from a what role
they play right we are not organizing our kitchen drawer where all the forks go here and all the knives go here and all
the spoons go here in fact that's a terrible layout if you're constantly always laying out fork knife spoon fork knife
spoon fork knife spoon it' be much better to bundle L up as fork knife spoon so you just grab one and now you're done
instead of having to go here here and here and here so um when you're learning we copy uh but once you start to get a
little comfortable really explore why things are that way question why am I organizing things that way why am I naming
things that way so hopefully that question yeah absolutely pleasure yeah thanks for asking all right so we were going to
do the non-arc unit get we didn't really test this bother no let's yeah let's let's actually test it so I need to rerun
yes the application but it is kind of funny right it's like that you know I I talk about this where it's like I don't
run my application that much because I'm just you know writing tests writing code writing tests writing code and
everything then just works most of the time 99% of the time until unless you haven't tested certain areas like
configuration or UI and then that's failures why you make sure this is the right number of columns yep all right sui
imported and then we don't want new years's we want I'm gonna pick protest got the song but for some reason it Gaz
zillion of them yeah so this is uh this is an untested area that uh we probably want to deal with so this is the we must
have done something wrong with the stream or did we because I'm pretty sure we're not returning multiple values for uh
an individual song um so I wonder let's try just as a debugging politics and America to see what we get actually let's
try one that's got two death interesting that's not helping yeah so I think uh let's this one I think might pay no
didn't tell yeah same there okay that's an interesting failure failure mode it is um Let's um at our first suspect which
is so as I mentioned like it it it always works almost except for the untested areas so we first want to focus on what
are the untested areas and the untested area is the code that we wrote where we didn't have a test which was in our uh
song uh happen uh do a reformat because it'll probably align everything where where is yeah so um what I'd want to do is
uh have the song view class do this work and this is something that suige mentioned before and I think it's it's it's
actually time to do it um so generally what I like is for my uh data transfer objects to do the conversion to and and
sometimes from but in this case uh from uh the domain to itself so let's um let's do that so let's so would we put this
into a a method and then move the method into the song view yes class yep so we would extract so we want to figure out
what what do we want to to be ending up right so the first thing I think about especially when I have a very long stream
call is do we want this entire call to be in view right because this is doing a the answer is no because this is doing
all of the songs not a single song well that's not the the part I have a problem with the part I have a problem with is
this is calling song service theme so what I want uh is I want my dto to take domain dto so that's so what we' want to
do is want to split this into the sort of the two things we had before although in a slightly different way because now
we're song is there a way to say um take the rest of this and put it into a I should be using W to take all this and put
it into a you could but uh I find that to be much harder than just extract variable thing extract variable on what part
I think I'm not cracking so extract variable on song service. search by theme songs I feel like we Del did that didn't
we yes we did but now I know it's different I'm just but now it's yeah sometimes goes around comes around um so then we
can take the end okay working on my muscle memory there we um to there yeah and so I would call this uh either from
something like that is is probably what I would start with yeah song views from found songs yeah it works yep and then
we move it over into uh yeah so you have to make it static first and then we can move it really oh is it because because
right now it's instance method and you can't move instance methods in the way we want okay just no I can't manually do
it uh this yeah this the make a static is hard to get to on Windows because you have to do Control Alt shift T right to
get to it which again I re I recommend mapping to somewhere else um but I also have I I do static enough that I've
actually manually mapped that to uh to control alt s although I don't know if that's a valid mapping on your end control
alts yeah I'll check it out later yeah I just made a to-do for myself and so now now you can move it yeah and want move
it to song view right right and escalate yeah all right so now we can write a test for our dto to make sure that it's
doing the right thing do we want to inline this now or do you think it's no I don't I don't feel the need to inline that
okay so say sorry you were saying we should write a test for uh we should write a test for the method that we just right
looks like we don't have a song view test class yet would you test this tight end or should we do it no we want test
this directly right so so um and this is something that's that's different from how a lot of people do it is I don't
want to test through anything else I don't want I don't want any intermediat areas I want to know if I give it a list of
song is it going to give me a list of song views that are correctly structured um and especially once we get to uh
actually an a proper song for you because right now it just has the title uh then this this we'll need to do some good
yeah oh Wally um I don't use jpa so I don't use intell's jpa I don't use jpa because I think most projects don't need
jpa uh and this goes back to people do what they copy what they see without understanding why They're copying what
they're seeing um so I see lots and lots of projects to do spring data jpa which is hibernate underneath and don't
understand the immense complexity uh that that brings in and don't think about whether they actually need that
complexity um but basically I don't I don't use jpa you're saying most projects don't need that complexity they don't
need it yeah yeah that's like let's you know uh create 10 microservices when we've got got one team of five people load
there's two things involved there's fashion which is the microservices and then there's copy what everybody else is
doing without thinking uh which is a fashion okay so we want to test so what we want to think about is is how easy is it
going to be to to test this do we want to test this directly or do we want to further refactor um I think this one is
probably probably reasonable so we want to test is given a list of songs does it does it pull out the title right even
though it's saying it's right I guess it is a title it's putting into the view that the title only right uh Dr twitch
easy says do you still use at entity uh yeah so I'll still use um orms um because I find them mostly mostly convenient
uh but I'll use something like spring data jdbc because it does just the right me um what are we doing why does it keep
popping up that build output uh because you're did I type something I was typing in the other screen by the monitor it
was weird Okay so we're working on the name for this test so this is taking found songs um yeah converts found songs to
song views and so I think we can copy the the creation of a couple of songs from so what I tend to do is I basically
just open up the project window and find a test that I think might have the approprate I've been so like focused on like
and if I were to use find and files then I might um look for uh a list of song it's like where there where is there a
list of song because that probably is going to find um the right thing and we want it to be in a test right you can tell
because it a green find this is a parser so we need an input list oh wait a second yeah so like that song service test
so that first test okay yep so it's creating a couple songs from the song song Factory so we can those so here's where I
might get fancy with the with the multi okay off J yeah yeah oops not control J off J then you can use the the widen to
get the whole expression yep I somehow you switch to early yeah oh I know what I did so then the control W for widening
it right well this oh interesting and then you can copy it and then paste uh so I'm not sure I put this into a song I
basically would just add a comment at the end and then just do list thing one second okay thank you sorry Ted I'm back
um so basically uh in between the two lines I'd put a comma so at the end of line 13 oh and then do list uh and then do
list. of yep variable y yep a list of View no so what I would do is is just call the method and then we can assign it to
a variable so we made it a static method oh we did right I forgot about that yeah y frommed frommed that's really funny
that's I want to go with song views yes that's the better that's the better word simple so tkes I'm not sure if you're
here um after we took the break uh we had a whole discussion about interfaces um so if you missed that part uh go back
and watch it um but if you have more questions about it uh feel free feel uh so alw mentions yeah I dislike lumbo I
think um so I have no problem with creating methods like we've we've done I have I always talk about sort of the
hierarchy of uh test data helpers um so so I start with extracting something common into another private method or just
method inside of a test class uh when I want to start using it across tests um then I'll pull it out into like we did
for a song Factory here uh and then when I need more complex configuration where sometimes I want it with this and
sometimes I want it with that uh then I will go and and create a a test data Builder um I see far too many folks though
again copy pasting what they see without understanding the benefits and drawbacks um and use Builders when they're
always specifying the same values the whole idea of test data Builders is you want generally to use the defaults and
maybe override one or two properties if you're always specifying everything then you're pointlessly creating a builder
and you may as well just have a single method that takes all those parameters so so a test data Builders solve is I have
a method that just takes the song title now I have another method that takes the title and the artist now I have another
method where I don't care about the title I don't care about the artist but I do care about the themes well I don't care
about right and so now you've got all this variety of different possibilities and instead of having 10 different
overridden sorry overloaded methods uh with with eight you know with different combinations of parameters you create a
builder uh to to handle that situation um and side note it is not the gang of four pattern Builder it is a it is
actually a separate pattern what I call block Builders uh named after uh Josh block who wrote about it in Effective Java
but they are not to be confused with the gang of four Builder the gang of four Builder is a a different pattern um once
again semantic diffusion causes people to use the term that actually uh the same term to mean two different things so I
always sort of I always sort of have this ladder of of complex of my test creation stuff yeah never mind I was just
doing it to yep I'll do it later all right um let's run um all of our IO free tests so we can get back in the swing of
doing that totally all right that gloriously fast so after running this slow such a relief that was beautiful um so that
worked we can do a little bit more uh introspection into uh the the song views um so it has two let's just make sure
make sure it has the right content which I'm pretty sure it does uh so instead of has size two let's just say contains
exactly and then let's give it a couple of song view objects remember they're only gonna have they're only gonna have
the title great pass all right I actually want to write like a a custom format I don't know if intellig has the right
settings for this but like where if I say autof format it will go into all my test methods and if there's a blank line
before the close because somehow they always end up there um that it would automatically get rid of it because I never
want it but somehow Auto completes and other things somehow they they they they get they get yeah it doesn't get rid of
it no because it's not it's not doesn't have that kind of yeah yeah yeah there is I think there is some more advanced
formatting but I'm not sure if that one would be covered so all right well so uh to a certain extent that's that's good
but that's also disappointing uh but but it is a good commit what we do what did we yeah we just basically um pulled out
conversion of song transformation of song to song views yeah we don't need to say where it came from do we no test all
right they're running in in the background because of the Comm come on go away little hover you can just hit go so we
haven't discovered where our problem is right um because this is well this is in the whole from right so we know that
the transformation is correct so if we go back uh on the top if we go back to Searcher um do we have a test directly
against this yeah got two I can go look at them see if they're yeah let's look at them although it's really delegating
so it shouldn't be that big of a deal but we do have where we got we got two songs we added those two songs uh whoa why
did it go from having two test mind so um let's go back to that other test that this is testing via the service but is
no no so it's not using the Importer um in this case can we go back to our our um our end to end is test back in in the
start song theme startups test okay thanks that's like where is that one uh let's um let's create our tsv songs to have
multiple right like let's actually use what you pasted in oh I see that that that caused us to be bewildered got because
at this level I like to use realistic data uh because it is endtoend is um and we're just in a sense sanity checking and
I can do the convert to well what I might do is um undo the paste and then put three three of those for the text blocks
yeah and now now paste uh you want to paste it on the next line yep yep uh interesting there was yeah and I want you to
leave that yeah I'm not gonna change that um all right so let's uh let's run that test we expect it to fail because we
expect it to have no songs well no songs so let's let's make it actually uh so let's search for for protest because that
was one of the searches we test right because it's a slow test so yeah slower make this big so um expected one gut nine
that's fascinating interesting uh well that's good so now we've got a a failing test here um and the artist is correct
the song title is correct it's just we get lots of them instead of yeah it's exact now what's interesting uh so what's
unclear um so let's close this I think we we got it I'm trying to actually I've never made this oh there we go oh I made
it a floater I see oh that's why okay back maybe grab it at the Run uh I don't think you can just drop it back I think
you have to on the right yeah so let's um we can close the bottom what I'm what I'm curious so so I have I always I
always think of hypotheses like what what could possibly be going wrong here um one thing is uh are there actually nine
copies of the song is that possible or are they just the same song is returned multiple times um we can't tell uh by
just obser by just sort of looking at it um can we write a test closer in to figure out which of those two it is well
what we can do um I second so what we do yeah we're parsing we're putting in a local variable right and then for each of
those we're we're doing an ad oh so uh if we go into the song I don't know if it's a I forget if it's a record or not it
is a um let's let's actually override the two string so if you go to the bottom and o and want the two string actually
is you can also do it this way right where you say oh this will then bring you to control o or you could implement it
but actually yeah you could generate a new two string um but I actually want to override it ah okay because I want it to
do whatever it currently does and then do something yeah um so what I want to do is return string and then plus hash
code uh yeah hash code oh does it not like it because record it's not really saying why so um intelligate doesn't tell
you why uh there it tells you why in the status bar and it's not that's was obvious so if you if you hover over it
you'll see abstract meod two string cannot be accessed um that's interesting so they private interesting let's uh then
let's let's generate one do wait this and go back to generation uh and on line 28 let's say plus hash code plus comma at
the again yeah so it's returning the well depends on how it's calculating code because it could be calculating it based
on content so it would be the same yeah even if it was right that's what that's I just realized yeah H um I was about to
say that's cool the that I still like it just didn't solve our problem so what we can do is we can uh we can actually
ask for um uh in the test uh we can basically ask are these are these the same is the first and the second one the same
let's do that in our test so uh above the assert you currently have so let's assert that uh so let's save off the the
search by theme we'll save that off into a variable because it no no not that oh search by theme yeah no nope there we
go songs songs um I forget if a search a has uh different doesn't what I was hoping for is um assert that none of these
are the same uh which we could do with a predicate but I think we'll just make it easier on ourselves so let's uh back
up a bit uh so instead of found songs we'll say found songs. getet Subzero or just get first uh and then we'll say
assert that uh is expected not the same so it's returning bizarre all right well now we now we gotta now we now that we
so my my hypothesis was um that uh it was actually adding the same song multiple times but if it did that we would have
ended up with ones that were new instances with the same data and that's not what's happening uh because otherwise the
objects wouldn't be the same so let's um let's go let's let's find a test that is closer to our our theme got uh one
this one here uh and I think I I I saw something um so yeah so let's look at tests that are directly calling this method
I think it's just the one oh really it's just the one yeah this one here at the bottom song with multiple themes is
found by theme so we didn't actually have any tests that returned multiple that were testing for returning multiple
songs doesn't look like it there's only one test of by theme total wow okay well see most of them are up here song and
right we just moved from using song Searcher to Now theme okay so we wonder if we should convert all those other tests
to by them well we got a failing test though yeah we've got we we let's fix the failure and then we can then we can uh I
was GNA scroll up a bit if that's okay yeah so uh so let's create a test that's um not like any of the one let's scroll
up a couple yeah let's take that one line test uh let's call it search by theme even though that sounds the same yeah uh
and let's change the one above it to titles sorry finds multi I just wanted the last part changed yeah just change songs
to song it okay um and let's change this to uh instead of the song titles by theme that it's the by theme everything
else should be fine and maybe stick in a space between about 57 um okay so we wanted to test right whoops and that'll
obviously need to change to list of song you can autofix that or not I'm gonna Auto fix it yeah now we got to do we deal
from here tests and sort of my hope is that this one fails no but something is different though right we are create song
tests service is using song parser adding it to the song service which is adding it to the yeah yeah I Su I suspect um
the repository thing is is is causing some problems uh so after the import songs um we were in theme test right yeah but
let's go let's go to the bottom of what you have open and after we do the import songs uh so we can get rid of that
assertion about the first song and last song Get rid of that right um what I'd like is access to the song repository and
assert against that so what we'll need to do is uh in our repository oh um is that not Auto wireable could not overw no
be of some repository type ofan um yeah so I have a strong suspicion that that our that and we mentioned it before that
sort of this relationship between the song repository and the song Service uh and the song Searcher is all is all messed
up yeah um are you thinking of temporarily making song repository a bean so it can be autowired no I'm thinking of uh
Our Song repository uh is kind of useless and might be actually causing some problems so um I'd like to try ripping it
out well or disconnect it I yeah so I'd like to I'd like to test the theory of of disconnecting it so let's undo the
autowired part that that you just wrote Because that's not not oh so let's go to the to the song Searcher there um and
let's go to the yeah I see what the problem is oh you yeah let's let's let's keep going so method uh sorry not here in
the song service oh um let's comment out 27 and then run all IO free test and see what happens so that disconnected
repository at least from being added to yeah so um that's a different test though yeah so that's the song importer test
which was tracking what was in the what was imported by looking at the Repository uh also looking at uh basically Our
Song save to the repository but what I was noticing um so let's put that back so we don't and I know there's some
questions in chat we we'll get to those uh we can close the Bottom now or yeah you can rerun the tests um so scroll down
uh so let's go into song Searcher no sorry where we are at the bottom of that top part uh that's not where it was no I
yeah so there's something very wrong with this method and I'm sure we had a good reason for it but now it just looks
weird we have tests for it nope yeah so we don't have any direct tests for it which um isn't by itself a problem um but
uh who calls it song do you want to see who calls that right right yeah one production and the rest tests so I I uh so
let's so sorry go back to so who was calling that what test was calling that oh what test was calling it what test was
calling this ad song no no sorry one just yeah this one this this method who's call which test are calling that uh
service song theme Searcher test and song service test so let's go to song Service Test um is this the one we just
cloned uh we cloned one like it yeah so down that's the third test or the second test that's using it yeah so um let's
let's bit so that test is save songs added songs or save to repository what I'm looking for is uh tests where we're we'
re testing that that stuff is retrieved so can you scroll up on the bottom no sorry scroll up top yep no that's my fault
um let's uh let's do this so my hypothesis is we don't have tests for songs that with multiple themes that we count
right so if we look at uh if we look at the startup tests the one that reproduces the problem one thing that's uh
Halloween and death uh like that song is is is the one that's that's that seems to be uh repeated multiple times versus
the protest one right and curiously yeah if we did if we ran the we ran it for Halloween I'm pretty sure the we got
three results whereas protest got nine I think it's your other way around I think protest got like nine I don't think
it's running anymore okay it might be between runs might not be valid anymore so what I want to do is test so command is
your friend here oh I mean a different class sorry so that uh so this no not that one that's where we are the one above
it no no one down one down yes okay this one um let's add more themes to uh those H add more songs or just more themes
uh more themes is it a vars uh it is not so we will have to oh interesting create a song what is this Factory method the
Quake oh it's we have create song that takes a list of so we can use that one is create good so let's change New Year to
be list of inste and then we'll add in another yeah oh I guess I didn't need the protest do it for the other one as well
or no uh let's not do it for the other one let's run run the test see what see see if that makes any difference I have a
feeling it has to be in the other order but we'll see yeah so note what happened there's more of them there's there's
there's more of them in fact there's two of them fact there's one for every theme let's add one more theme to that one
and see how get so for each theme it's probably making a record so let's let's see yeah so what's happening is and I and
I suspect it's because of the weird way or not weird but sort of non-idiomatic way we're we're creating new song
Searchers every time um there's something that uh uh either it's there or it is um so Dr ttes says some flat hat may may
yeah there may be some some some there's something where when we're adding multiple themes sorry adding songs with
multiple themes they get added once per theme um which makes sense right because when we're when we're uh they are
ending up in three separate lists right um so we've got a problem with the way we're we're actually indexing our our
songs because it's not returning three different songs with the same content it is returning the same song three times
so uh there's something wrong at the level of of of Our Song Searcher so we can we can now um we can now dive in closer
uh and see what our tests are that are directly against um the song Searcher turns out add in particular yes so so it
turns out um right we've got this flat map and that may be causing the issues so the question the question is is are we
adding it incorrectly because of our flat map and and the fact that this is kind of under tested uh would would lead
lead me to the the same had do we want to take a a break since we're well over um yeah let's take a quick five so let's
take a break and we'll come back uh we'll answer some some of the questions that have queued up and then we'll we'll fix
the bug right so just a reminder that tomorrow I'll be appearing on the agile lunch and learn um link is in the comments
and I'll be talking about uh my tdd game talking about predictive test driven development uh stuff that we've been doing
here on stream and talking about the game and why it's both fun and uh as they used to say if you're not something all
right uh so there were a couple of questions um so that might have left but Dr Twitches asked is there a way to view
what was stored and so there's a we could have dropped into the debugger and probably my guess is at least seeing what
we're seeing now more readily right we could have taken the the test that we had failing put in the debugger and then
you know at the uh song Searcher and see see what's going on um I tend to to to avoid that uh mainly because I think it'
s really useful to be more methodical like what you know coming up with hypothesis and then seeing how can wew write a
test that actually fails um because then eventually we'll get to a test like we just did uh and we still have closer to
to go is is tests that reproduce the problem and that's what I really want because then I know that when I finally fix
it and my test pass I don't have to go back to the debugger and double check and and do things like that so I always
want to really and I you know sometimes feel like maybe I go too far uh but I really want a a test that fails as opposed
to just finding out the the problem that buger it also in addition to not having to go back into debugger to check
afterwards is you now have a test in I don't want to say in perpetuity but a long long live test that keeps your guard
rails up yeah and that's I mean that was you know what regression means is is to is we found a problem we fixed it and
we want to test to make sure we don't accidentally break that again so uh yeah um Al had mentioned something about uh
when do I think it's necessary to have a before all method um and I think it's never never um now I won't say never
because actually there are some cases where where it's useful uh when you're writing tests that have some complex setup
that have nothing to do with what the test is testing for example getting a schema set up in a database that you're
about to test if May if doesn't happen for you as part of the test you're doing then then that's fine as long as you're
not testing is the schema there and the way I think about this is if I just look at this test by itself and I couldn't
scroll around and look anywhere else would I understand why it's asserting what it's asserting or is there missing
information um so a before all that sets up some test data that says hey this song thingy is going to have these songs
in it and then I'm looking my test and saying hey I assert that those songs are there now I don't have a test that's
readable in isolation and that's important because we look at tests and and we'd like to be able to read them by
themselves and understand them fully um so the real symptom is I had a lot of initialization and the test was hard to
read notice what we've been doing in our tests right this is where you get encapsulated setup you encapsulate into a
single method the stuff that is noisy and unimportant but you leave the stuff that is important and so you know instead
of stuffing the information in an unnamed almost invisible area like a before or each or before all we give it a name
method like we do in our code and and for me it it's sort of strange that we don't treat our our code in the same way uh
our test code in the same way as as our production code like we refactor stuff and give stuff names so that it's stuff
is readable why do we not do the same thing with our tests well we should um so if the test is hard to read because it's
got a lot of noise then extract and usually in my experience it's the setup that is often has lines and lines and lines
and lines of of of ini ization setting things up wiring things up pre-filling some some information uh and I generally
find those at at the outer layers um against the application layer um well that's what refactoring is for extract to a
method uh and then reintroduce make sure you haven't extracted out all the information otherwise you have the same
problem um and then make the method uh parameterize the method so that you're passing in just just what we need so um
putting them in before all to me makes it invisible and makes it really hard to find EX encapsulating in a method where
that method calls right there at the top of the test it means I can jump right to it if I need to see exactly what it's
doing but most of the time I don't need to right same oh sorry keep go ahead the other problem with before all is now
that setup is being called for every single test yes so you really need that I mean a lot of times each test needs
different setup right right right or and and uh then it gets just ugly and then it then yeah then tests start breaking
or you start making a change to the before and now you've broken a bunch of tests um and so it's sort of this All or
Nothing which I think is is you know if it's something that that you know you're creating the connection to the database
great that's fine but in almost every other case you don't want setup to apply to every test Point all right so let's
Let's uh let's write a closer in test want we were here right well we want to test directly against that method that's
at the top the ad method there the ad do we have a test for it well we don't yeah no I was just saying there was a test
class uh you can go to see if there's a test class command shift t control shift T sorry control shift T we want to use
the existing one well that's not that's not the right right test we wanted to do it against we want we want a new test
but in the goes so that's really interesting that we never ended up creating uh so probably what happened and this
happens when when uh when you extract classes and things like that is you end up not uh retargeting tests um and not
perhaps writing more tests to test boundary yep oh why doesn't intellig know the Tesco on the bottom geez I don't know
although test technically should go at the top and code at the bottom but I can switch we've it's fine yeah as long as
it's consistent it's been did we just naturally gravitate away from that I don't remember I don't know yeah but they're
all they're all they're all green at the bottom so we'll stick with it yeah um I can switch it later so let's see okay
so we want to test ad song themes correctly added correctly is always a bit of a red flag but we can tweak it once we
get the assert yeah I'm not I I know there's some better but for now it's it's yeah yeah no I'm that way I tend to um
have my names not good enough at first so this is better than better than that okay so we need a song Searcher um so I
would say what I would say is it's actually add song let's let's start with adding one song with with multiple themes uh
and then we'll go to add multiple songs with right so we can just grab you know the test probably not that right okay uh
but we want to have multiple AR so one thing that uh might want to do is is add another postfix that does list of oh
yeah is that another swegi I don't know if I don't know if he's he's got one we'd have to I'd have that I like how
you're making a l sign of a protest song that's great yeah now we can just that's awesome totally should be a protest
song I protest against singing it as what I do um all right so let's let's add it find we need a song Searcher we do
need a song Searcher yes is there a factory for it and we pass in the song so I don't want to do it that way ah I want
to I want to go through the ad s the the ad method as we as we've done it okay so we're GNA do I'm laughing because sui'
s we must have said his name a few times uh what is it now that I forgot what it's called so we don't have a create we
could just do a just new it up uh I don't think we can can't there's no so if we want to do we need a new no you just
call that one with with no parameters because it's a VAR AR's last true uh what am I doing wrong I usually do EST and
that usually does what I go um no or do you want to do no well add is a command so we we would never command but there
is an issue there already okay yeah so this this is this is because we were treating uh the song Searcher as an
immutable thing and when we ever wanted to add it we would return an uh basically a copy of it um so let's let's hold
hold on to this one let's variable meaning this yeah nopes yeah and then we want to know that there's only well by theme
protest and that should only have a size yeah did you run the right test I don't think you're running it run the right
test oh wait uh oh no because that that test is still failing um let's disable that other yeah because I don't want to
get yeah right so now let's uh write the next test which is add multiple songs with correctly uh yes we have not um
pushed uh the latest to the GitHub repository yet um song I don't like doing that but do this fine you can grab it from
your clipboard buffer if you want Oh another song you mean yeah I should me grab one that's we haven't done at all now
do we want any of these to have overlapping so so this should be two do we still want to just against protest or one
yeah that's not gonna matter that I think that's fine so that should have size of two meaning that t this test we're
hoping to three irrelevant artist yeah because the song Factor right right so so this so uh note what's What's Happening
Here is the one that's duplicated was the one that there so that's why when we add one song it's fine it's when we add
the song fine it's almost like no I don't really know I was going to say something but it's not true um so it's adding
this song Twice yes so when we do the ad of the song to um when it's stream there are now two copies of this of the
first song in that because the first song was indexed by two themes so allang sign is in the map twice under indexed
under two different themes so I think we can still reproduce this by having only a single and overlapping is irrelevant
uh for the second song so if you change the second song to just have Halloween I predict that that will still fail oh
okay so that is not it um so it does require the second song to uh to have multiple themes so let's change the the the
next one to add another theme that's not one of the two we already have meaning so oh I see right right meaning you know
arbitrary so it may have to do with with overlapping yeah so it looks like it is it is having to do with overlapping so
let's change that to to protest and now let's see what uh all right so now now that we see that let's let's close the
the bottom and let let's um let's look at our codes what is our code doing in this case so so the first time it grabbed
the songs um should we do a saf squeeze a what a saf squeeze I don't know what that is so the saf squeeze is basically
crap I have no idea even though this is only basically three or seven lines of code I have no idea which part's broken
um so let's in line oh uh the ad method online we may not be able to do that um because it has access to the map this
this might be tricky uh let's let's do this um let's make theme to songs map let's make it package access instead of
private so just jump to it yeah um so let's just so you just delete private and that makes it package right that makes a
package it's called also called default access or default 30 huh in in our test on line 30 sorry method and sogg just
the one and keep the method yep okay great um so now we can do is now we can do assertions on Why move two ahead of mean
so am I inlining the second one only correct and not the first one the first one is not broken no I know but I'm Looks
Like It reversed the order but I mean I might have just misread it no in line this one right yeah now the song Two is
mentioned on line 34 but the original one the first one is on line 30 and that's still there oh way up there okay yeah
yeah yeah sorry I didn't see that yeah so now we can do is we can say all right what do we expect the song stream to
have well we expect that there's only want uh this is going to be tricky so first uh yeah so let's so we're gonna have
to do a little bit of of saving off what's there um is it what you're saying yeah so that uh let's call it that so that'
ll have consumed song stream so we'll have to recreate song stream um so sorry before we finish writing the assert let's
let's make Stream So after the concat uh we call that before adding a second song uh let's let's do this a different way
so sorry let's undo a bunch of a bunch before we do the stream that keep going yep keep going I could have just had you
delete all that uh let's extract let's extract song SC song stream from line variable no just the song stream yeah I
don't know why it was because it gives you options and it assumes you want the whole thing but you have to tell no I
don't want that I want that one right yeah um so we'll call this uh uh uh before add original song stream uh fine um now
instead of song stream what we're going to do is because the the annoying part of streams is once you use them up uh you
basically can't do anything with them without using them up and we don't want to use it up um so what we're going to do
uh is um do song stream on on the right of 35 I wonder can we do a copy of that to I don't know what that would do no
there's no copy method I'm just wondering if there's a a copy of so we can convert it to a list and then convert that
back to a stream so let's do stream so that's basically a do nothing it's just adding some intermediate operations so
the test should still fail does all right and so now we can extract the songstream do2 list to a new variable uh and
this is uh list of songs before ad all right um now what we can do is now we can assert uh after 35 without being
worried about um using up this using up the stream and not having it available for for line 40 so what we want to do is
we want to assert that well we've added one song what's our expectation of how many songs are in the map I hope only one
yeah this is probably gonna we we wish yeah well did you want to test what we wanted to do or no no I want to test what
what what what we kind of thought it should have done right okay let's run it we are theorizing it's gonna fail yeah
yeah which of course makes sense given that uh theme songs. values gives Keys uh um so since that's wrong let's let's
let's fix it um in fact we could we we could go even further and say well is that a values problem or is that a flat map
problem right because right now we can't tell the difference so let's extract out the values into a variable and assert
on that so that would be how far up to there or to there well you need the whole thing because you're calling calling a
method oh right to there variable oh right okay yeah now it'll be interesting to see uh what um are are you waiting on
something no keep going I'm listening oh because I don't oh okay um so let's after 32 let's assert that the values has a
size of one up I actually honestly I I wasn't quite sure until we actually pulled the code in it wasn't clear where
where the problem might have been but I'm actually still not 100% convinced uh so now like so this is what's interesting
to me about this s squeeze is on the one hand it makes stuff more accessible so we can can start doing more tiny asserts
um but the other thing is it also makes you think about think about each of the steps more clearly so this one um we're
actually G to get we we've added the song once but it's keys right New Year's in protest now what I find interesting is
maybe that's not the problem because we we we saw that it only happened when we had overlapping so now I'm now I'm not
two and so that's that's wrong kind of right off is that wrong it's wrong because we basically it um yeah that's just
wrong well what do we want we want it uh it's not quite wrong because it depends on what we want the song is keys but
when we yeah so in a sense what we do is we we pull everything out of the everything it's not that we pull the map and
copy the map and then add the new song which is really I think what we should be can you scroll the the add method into
view on the top on the top oh oh sorry top top pane scroll yeah yeah I was us saying top of yeah yeah so um it's so we'
re we're basically taking all the the songs out of the map even though they were there multiple times uh and then
reindexing them and when we index them what we're storing is a map of the theme to a list not a theme to a set is that
correct because if it were a set that okay because sets can't have multiple copies of the same thing lists don't care
whatever you add it'll it'll add it um so is there a two set well I mean that would change the structure so so the map
would would have structure so uh sui is correct that we would still have duplicates which in a sense really I think is
wrong um but at least we would we would paper over the problem by using Set uh so that could solve it but it doesn't
solve the the core problem which is uh that what we're trying to do with ad is return a copy of song Searcher with the
new song added the problem is that the interface uh the Constructor to song Searcher doesn't have here's here's an index
go just use this because we have to to so basically reexes all all the stuff so yeah so one possibility is is we could
basically say when we pull stuff out um and flatmap it uh and then make it unique um then that would that would problem
uh the other is yeah like like like suig mentions we could also um just hold on to the list thing uh hey there uh how
are we whatever AA 48 sorry unpronouncable um to me uh is there harm to harm to to make duplicated code in tests uh
certainly i' ra I agree I would rather have duplication anywhere not just in tests um rather than unclear code or um
well the behavior of song Searcher is searching is able to find songs by theme it happens to index them in in a specific
way but that's an implementation detail uh we could store just in a list and and linearly search through it um so the
fact that it indexes it is an implementation detail so that's why I wouldn't call it song index if it were just some
kind of index internal thing that were not sort of exposed then then I might I might do that but it's basically song
song Searcher you add songs and then you can find them the real question I think is from a design standpoint how do we
feel about feels kind of janky to me but I'm don't fully grock streams so well it's not so much a stream issue it's no I
know I mean it's the it's the immutability of song Searcher right because that's that's causing the problem we could fix
oh we've got symptom right we could fix the the symptom which is uh let's just make sure that when we pull the values
back out of the map we get a unique set right um so we could start there and then we could talk about design so let's do
that uh so test the failing test which is this one uh that's not the failing test oh failing class uh so let's make the
bottom window bigger yeah because all the code's there um so we now know that the values coming out of the map in a
sense are not what we'd like um but there's nothing there's nothing we can do at this level because what we're getting
out is a is basically uh a collection of lists so the do unique wouldn't have papered it over enough to go to we can't
we can't do a do unique here because what we're getting our lists and lists are awkward to deal with from an equality
standpoint so we have to basically say all right it's going to return two so we can say it has size two expect um and
now if we run it it'll Now 42 and here's where that precise prediction of line 42 is useful because that's because we've
got multiple tests that have assertions about size um and indeed it failed on that one so now what we can do is we can
say Okay so we're getting a collection of lists so we're getting two lists but we only want one song so um after the
flat half we'll do dot um is there do unique no uh we might have to do uh distinct yes thank thank you sui I knew that I
knew it wasn't unique and I okay if not then we are missing something in our understanding okay great so this um this
repairs the problem of getting this a song that was indexed multiple times but we only want to really end up with one
copy of it and we only fix the test we didn't fix the production code right but now what we can do is we can we can uh
basically take our our our new found knowledge and now apply it to our production code and say well we know if we add
distinct that will fix it or that's our current hypothesis um and so now we can undo the saf squeeze in our test at the
bottom and actually before I forget how do you pron spell sap squeeze uh sff and is it an acronym no it's person's that
oh it's from Jr uh no he just talks about it um s squeez has been around around quite some time I don't actually know
how old uh so 32 all the way down till before the assert before the last assert so so keep going keep going keep going
keep going stop delete all that except for line 47 sorry guys say didn't we need to delete that one yeah uh but that one
should just be actually a duplicate of the line above it so you can actually delete it and just duplicate 31 so yeah so
duplicate line what's great about is if you don't select anything it duplicates the current line if you do select then
it duplicates whatever's selected right all right so assuming we did the right thing um yeah that's probably a good
point sui it's like yeah do do a commit before you do a SAS squeeze although SAS squeeze tends to be very local to a
test so um it's usually not too difficult to to revert but if you have to make multiple changes then then yeah it's good
to very it's very spiky Spike feeling so all right let's run the test uh oh that's true we did change visibilities and
we would have forgotten that yeah all right so that fixed it uh let's go restore the visibility of private on our map so
you can close the test yeah we'll go fix we'll turn the disabled off in a second we do that now or uh you can do it now
okay that's what I thought we were doing so yeah so we can run that pass uh oh um I want to do the oh we might have
another issue uh so does like it so we go a we got some some cleanup to do so let's first um put the disabled back uh
yeah yeah so put the disabled back let's go um to song Searcher let's map uh let's also go to song and remove string um
because we don't need that anymore you can just revert it by clicking the gutter oh I want to just try this one just
because oh interesting okay y so so um I in the back of my head I I thought about that and then then it got dropped
songs it appears that we modify the song is that right can you reenable the test that we just disabled and and run it
because um look let me know if you want to see click difference yeah so notice that um oh our test is wrong because the
actual is correct but wrong because we added multiple themes expectation oh right yeah so basically duplicate the that
list of the whole thing oh including list of because you'll need the list of yeah and Su IGI promised he'd create a
postfix for us and we're gonna put that on this one yeah so this is again where where it's really important to
understand what failed um because uh the the it we looked it showed what the actual results were and it's like that
looks fine what did what did what were we expecting oh our wrong excellent got bit by the test magic all right well what
we did was we we' uh we don't have any more disabled tests right no okay so we fixed a a problem Searcher and you can
say song Searcher to be more precise about what class about all right um failed to start P oh we didn't run all the
tests so there might be uh as a as a repercussion we configuration or intellig just got interrupted because of the amend
that might have been it everything looks everything looks good all right so now uh we should be able to try the app and
it and it should it should work should work better than it did guarantee yep all right and then we should be able uh
death voila sweet three songs yep woohoo that's a good all right good way to end I yeah we've been going for a while y
um so yeah so we didn't get to uh improving our era so let's go make see I think you can check off 62 because we
basically have done that and now it's actually um yeah so next time uh I think um we can work on the the error on uh we
could probably also add the arc straightforward improve isn't the right word just having error messages yeah having
having userfriendly yeah um yeah and then we can we can decide uh do we want to persist the to the database or do we
want to make it easier to to skip over columns we don't care about so a bit pasting and that's the one that would need
we would need header we would need header header rows yeah and I think we have a an entry for for skip header rows they
at 52 says skip header rows but I think for importing yeah we would we would actually need the header rows right so then
that one just would be something we would ignore yeah right now we're skipping no we're not skipping we're not we're not
we're not expecting head R yeah this would be a feature that would just go away or not a feature but um we would just
delete that if we end up doing skipping over yeah I mean I I I mean I personally think we should we should be looking at
header rows to to do our import and not be one yes and I would drop the word consider I think it's actually pretty
important that's fine you can say responsibility so I might have some duplication I would I would just clarify this skip
over uh unused columns yeah did I have another thing down here that was similar well you had 68 I'm not quite sure what
that meant oh so yeah right now that I guess would be the same right now there are some columns that I have hidden here
right and so if you unhide them uh and we only pay attention to the to that then that would solve that then that right
no no assignment that's what's great about this jury you can't assign it to anybody swegi um yeah so we can do that
stuff so basically make the import nicer um and we probably want to rethink our Our Song Searcher immutability um once
we get into to uh to persistence I think and we start thinking more about that I think that will become clear about what
what we'd want yeah that makes yay so that's all for this time um I think there were there were some really interesting
uh aspects of of running into a problem that we noticed and and slowly uh writing tests that sort of you know kept kept
trying to say can you know is it at this layer is it this level or is it at the lower level um and continually pushing
on that um and then the saf squeeze made it uh helped us confirm what what we might have suspected as the problem uh and
then um I really like the the the sap squeeze like it's it's uh because what I see some sometimes what I like about it
is you're not touching the production code because what I see yeah and you're avoiding going the debugger well yes in a
way it's a technique for to answer the person earlier about you know you know well what if we just looked at what was in
there right yeah because what what but um what I like about it is is because one of the things that that people uh often
do is oh let's make this method public uh let's make this method public you know and then start testing against it's
like if it's hard to test or or it's doing too much then and and instead of trying to modify the production code bring
it into the test so you can do whatever you want and you know it's the right thing because you literally did an inline
um and then you can do sort of more micro testing as it were uh and essentially we we did look at what's in there but we
were doing it through the test which meant that what we ended up with is a test that finally passed um and so now that
test is there forever and we'll protect against any future regressions that we that we might unintentionally yeah so
it's a great technique for for situations like this where where the code is is still just doing too much or or we're no
longer sure what it's doing um in addition uh it's unsurprising that that we sort of ran into this because for whatever
reason again tdd doesn't guarantee anything uh we didn't test the ad method directly um enough or really at all uh we
had always been testing it indirectly um and so this is sort of tdd won't help you um code coverage won't help you um
mutation testing might help you uh but mut mutation testing is is not a very subtle uh it doesn't do very subtle
mutations and and so it may or may not have helped us um find find the problem but now that you know but because we had
uh all of our other tests we were able to to quickly write those and and sort of put up more um good supports to to help
us figure out when when things go wrong yeah it was all triggered by the end to end test that made us go huh yeah yeah
or no a second did we write the end the end test first or did we observe the application we observed yeah we observed it
and we said you know sort of uh I said you know it'll work except where where we don't have testing and right it's true
to a certain extent uh it didn't work because we didn't have kind of an endtoend test so I thought that was useful uh
because then from there we we sort of um dialed it in you know level by level getting closer and closer to to the one
method that was causing the problem and then from there getting down to the one line of code that was causing the
problem yeah so um anything else you want to add um no I think I'm good all right all right so as a reminder folks uh
tomorrow I'll be on the agile lunch and learn talking about my tdd uh you can go ahead and register I recommend
registering um and not waiting till the last minute because I don't know if that would even be possible uh it will be
recorded um so that'll happen tomorrow at 10: a.m. Pacific 6 PM UTC uh in terms of next stream I'll I'll probably also
stream after and it might be pairing might can have to hook up and and figure out what our next pairing schedule is um
other than that thanks for thanks for joining thanks for time
