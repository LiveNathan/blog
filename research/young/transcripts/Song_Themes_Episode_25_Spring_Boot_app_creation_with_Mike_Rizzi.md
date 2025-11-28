# ＂Song Themes＂ Episode 25： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=9bqKSeqCtSg

---

## Transcript

e all right hello folks and welcome to episode 25 of our pairing stream how's it going Mike good good morning good
afternoon good evening wherever yall are right I was just looking at skimming of our notes from last time it was
actually a couple weeks ago since we last did this yes yes whoa because you were you were out of town and I was uh you
and I was out of town at the agile open Northwest conference which was uh a lot of lot of stuff hey it's the grumpy Game
Dev welcome nice to see you again yeah um how was the conference how was the conference it was uh um uh extremely
intense um it was basically three the conference was two and 2/3 of of days um but it's an open space conference so for
those of you not familiar with that style of conference it is um you come there's no set agenda other than time slots
and uh wish it was intense I've been in conferences that that were in a tent in a very large tent but this one no this
one was inside uh and there are spaces set aside um in this case there were I think let's see eight n there were 10 10
spaces so that meant um what like five or six time slots each day so like basically room for up to 60 to 80 different
sessions every day um and I like the way they they did it at this one sometimes uh so what you do in in the conference
is you basically come and then there's the period of great propose a session and as a session proposer what they call
session host you don't have to know the answer you don't have to present anything um but you can uh so you can either
say hey here's some cool stuff I've been doing here's some stuff I want to talk about or I have a question I have a
problem I would love to hear some some solutions some ideas um and so it is if you've never been to an to an open space
conference uh I I highly highly encourage uh folks to go and if you do go um I highly encourage you to suggest a session
uh because again like you you don't have to be the expert in fact likely what happens is you become the one that draws
in the experts and then you get a bunch of experts in the room and So speaking of experts in the room so people like
Woody Zu of mob programming Fame and luell and Steve quo and paig Watson and and all these folks from the crafter
Community uh were were all there uh James Shore um talking about fast and Quenton cortell who basically came up with it
so like you know all the the the kind of quote luminaries of of um of agile but really of of sort of extreme program in
the crafter Community were were there uh and you will have the feeling of like darn there there's like four different
sessions I want to go to in this time slot uh which is you just have to get over um but the nice thing is is one of the
the principles of of of an open space conference is if you're not actively contributing or learning or getting something
out of a session you get up and you go to another one um hence the the O you know the other part of the openness of an
open space and it's it's interesting because um Mike you and I have been to to Open Spaces in in Northern California uh
and it's interesting how the space itself affects that sort of openness of people drifting in and out um I remember I
was at one uh open space conference on on the east coast and the spaces were in rooms with doors that closed and it felt
like it it closed off the the conference a bit because it made it harder to to move around to sort of overhear things um
there sort there's this interesting tension of of that kind of openness of being able to overhear oh that sounds
interesting let me go there versus being noisy and I can't focus on on the on the one I'm in um so there's there's
always there's always that tension uh but yeah it was it was it was great I I um uh I basically ran my my tdd game uh
with three sessions and got some uh amazing amazing ideas for expanding it uh so I've been furiously like taking notes
and and writing up my instructions for for the folks who already own the game to say hey here's a new way to play it uh
and uh so I'll be be hopefully getting that out to to folks soon so yeah it was it was definitely um and we were mob mob
programming ensembling uh late into the evening uh until like 10 10:30 at night and so did not get a lot of sleep so
that also contributed to brain brain fry I just want to tag on to what you were saying about um don't be shy about well
one definitely go to an open space highly recommended pretty much my favorite conferences in general um and then the
second thing is dive into hosting even if you don't know squat yeah um and you know that was hard for me to do I
remember the first time I did it I was just like I don't know intimidating yeah it is intimidating and it's like you
don't have to have a presentation a lot of people just have conversations yeah I think the first one I had was something
along the lines of like what are your favorite technical practices um that that work in an XP environment kind of right
and so some people came showed up and we just talked about it like there was no presentation no whiteboard yeah people
just riffed um and then the one I usually do that I'm pretty much every time I'm at an open space is a session on what
books have blown you away and you want to share with other people yes and it's a it's kind of a brutal because your to
read list becomes massive um but it is really fun to hear people round robin talk about books that they're they've
discovered or they rediscovered or whatever yeah yeah that's great I always remember so you don't need to know anything
to post that right you can just say all you're you're facilitator that's it right you know just have to have a good
question yep um I was going to say something else uh and I forgot open space related um maybe maybe I was trying to
nudge there uh it'll it'll come to me yeah yeah or not um so speak uh speaking speaking of books um one of one of my uh
favorite books uh Thinking Fast and Slow the author Daniel Conan apparently passed away today at the age at the age of
90 wow um so I'm a little a little emotional about it because um I read a lot of his work and and heard a lot of him and
saw him speak uh I forget where I saw him speak but uh he gave a just a wonderful talk and just a wonderful um person um
but you know he really did a lot to to push forward and some of the stuff in that book has been sort of not quite sort
of disproved but hard to replicate and some of the things are not some of the factors and things like priming and so and
were have found to be not as strong but still it um really set you know some of the language that I know you and I use
and other folks use for system one and system two and uh discussing how people think and and that book is very popular
in sort of you know the communities that we're we in in terms of crafter and agile and XP and so on um so just just
thinking of thinking of him W yeah I remember when I read that book I mean it's a brick Thinking Fast and Slow um the
one thing I remember about that book is that afterwards I felt sort of maybe depressed isn't the right word but it's
kind of like well damn what can we do now right right right and then I think there was a heath Brothers book that kind
of answered that question like here's how to fight or how to counteract some of your cognitive biases right right I
think it was called decisive but I'm not 100% certain that that sounds right but yeah but it's decision- making so that
would sort of if you read Thinking Fast and Slow you might want to read decisive afterwards so that you don't come out
of it going well damn you know how do I fight these biases yeah I remember I listened to it as an audio book the first
time I actually encountered it wow yeah that was I I I think I did that pretty much when it came out because um I felt
like I was one of the the early adopters of of some of the stuff in that book nice um but let's uh let's talk about what
what we're gonna work on so what um where did we leave off so for those of you who who are uh are new and haven't
watched the previous 24 episodes uh what what we're working on is is an application called uh song themes uh and maybe
Mike you want to give us the the quick The quick summary sure um so the it's basically we're developing a website where
um we're collecting so I'm a DJ um as a volunteer DJ Community radio station and I've been collecting themes of song you
know songs associated with a certain theme like you know Halloween or Christmas or you know antisocial Behavior or you
know um songs about rain whatever and one I've always wanted to collect it in one place and so this sort of helps force
me on that the other thing is it's interesting how there's not much out in the world where you can say you know I want
to see a list of theme songs for a particular theme they're either listing like the top 10 and usually they're very
popular songs right versus this the idea is to be more comprehensive it's not necessarily to be like a comprehensive
website but it's you know partially to have a project to work on to practice some of these techniques um and also I
think what would be fun to have out in the world and I know um my fellow DJs at the radio station when they get this I
think they're G to be like oh yeah they're gonna start entering more songs I hope and and I think it's really key so so
one of the things that that I get asked not quite every stream but sometimes it feels that way is how do I learn X where
X is Java spring boot whatever whatever the the the thing is and I say come up with a project that you care about that
provides some some some value to you um whether it does to others is is great um that's that's an addition but at least
it has to be something that you will use um so if you need a to-do app because none of the to-do apps out there fit your
way of thinking or your your your you know how you want to do things great go write it to do that um find something
there's something in your life in your world that likely can be made a tiny bit better by writing a custom application
for you um and I think that uh or something that that you do and and maybe it's for work but I always say um often the
people who are asking or looking for jobs or or new developers uh something that you will use because one of the things
that following tutorials and doing following and and doing what the tutorial says is is great um but you really learn by
by solving problems by figuring out oh I need to do x uh so I was um playing uh the agile fluency game and one of the
things that that it does is it does some calculations and I'm like okay this would make a great little app because it's
it's a little bit of math every single round and it's kind of uh you can do it but but it's not it's like this should be
a little spreadsheet or this should be a little app um and so you know even for for like board games there might be
things where it's like oh I I wish it scored this stuff more easily or something uh um one of the things I was thinking
is is uh a a phone app that would use sort of computer vision to you take a snapshot of the board and it would be able
to figure out who won right so if you're playing like ticket to ride or something like that instead of manually counting
things up have have the app do it so any of these any of these things creating an app that you will use that because
then you will provide feedback to yourself and you will have to then learn how to do things um that's the that's the
that's the best there's there's nothing like it has so many uh you know you get all this positive feedback of like hey
this does things that I want to do plus you're you're learning what you need as opposed to somebody telling you what
what you should learn um and that's that's always great all right so uh should we share your screen and take a look at
jira and see where what what we're up to interesting that um on streamyard it shows an old version of my desktop does it
do a Snapchat uh I don't know because I actually have um I do not have streamyard on that monitor I have intell yeah I'm
sharing the right monitor uh let's see we'll find out nope you must have shared a browser window I don't normally do
that let me un share but not leave Studio there it is stop sharing that is weird share screen share window oh entire
screen ah yeah yep I did window can now there like that yeah yeah I always I I was like wait no it's not window it's
screen it's screen yeah it's like why why is it the third option too okay my bad hopefully nothing hor don't want to
share their full screen yeah all right there we go there we go now we're sane so uh jir let's see according to our
breadcrumb jira 72 is next I ran the passes oh and if I didn't say hi astd hi astd uh and yes the grumpy game that was
like uh what do we do how do we do this it is also it's not like it's early early it's just I know my brain hasn't
hasn't fully woken up so yes so one of the um and this this is interesting because this actually came up I forget where
I think I was talking to a coaching client um and uh this is sort of the the the the danger of of learning um is as a
novice so one of the issues that novices have and it's not their fault it's it's simply the level of experience and
expertise is you see something and you're like oh that's useful let me do that and this is how sort of design patterns
get out of hand it's like oh let me use the command pattern here and the strategy pattern here and the adapter pattern
here and actually they didn't really need any of those um and you end up with code that's more complicated than than
than expected and so the the situation here with the illegal argument exception is kind of the the the way I think about
it now is um if you're if you're validating user input then you probably want something like the result class that we
created to provide messages back to the user uh otherwise you probably want to lean towards throwing an exception
because that means you you need to wrong so if you are not processing user input if you're doing things like reading
information from a database and there's some IO exception don't wrap it and and return some kind of result class there
you actually want to throw an exception uh but if you're handling input and you're validating it and the validation says
there's something wrong then that's a good opportunity to use a and so what we've done here is um when we started doing
the the parsing of the header um maybe let's go to the the that last one the assert that illegal argument yeah this is
got to be the one yeah yeah so basically we uh exception thrown when header column count does not match data column
count uh um so the idea is that the data needs to match the number of of column headers because we're we're paying
attention now to to column headers and um we're throwing an illegal argument exception which was actually a mistake
because we uh already have a result class and we should actually be returning a failure result as opposed to throwing
throw an exception so that's change and this is the header with four columns and we're passing in six Columns of data
right so looking at this test fresh um it took me a little while to orient myself as to what uh what was being passed
into the column mapper and so I wonder if we should pull that out into a string and call it header or header row I was
thinking the same thing hey bny welcome uh header or header row what do you row that I also feel like uh even though 29
is throwing an exception um the column we're asking for we should ask for a column that actually exists in row oh
instead of song title yeah yeah I'm sure we copied and pasted that from somewhere but's it should it should at least
appear valid do three yeah and then let's rerun the test make sure that should still fail still should No it should
still pass I mean it should still pass because we are throwing the the yes yeah um um it'll pass by failing um right and
then I'm said a similar thing like reading this I think I just wonder if name so since we're doing tddd we should say
what Behavior do we actually want right right so what what should it do this is what it does um but what should it do uh
is is basically our uh and and I and I want to highlight this I I I do this all the time when you're doing tdd there are
times when you are going to change existing Behavior with any you know non-trivial piece of code you're that you're
building upon you're going to change Behavior Uh and in this case the test already exists which means you change the
test to say here's the new behavior that I want so um that's yeah so we basically instead of asserting that it's going
to throw an exception uh we want it to return some kind of result and we can say what what we want and then make it
happen great so just start changing yeah let's just start changing okay there oh interesting does it even return a
result well it doesn't return a result because it th exception right right right so it's not even we're not even at the
point yet where well let me rephrase it the the code is not such that it can even right and so we might have to do some
refactoring uh to to get it to to what we want so we'd like uh is is it to return a result sorry go ahead yeah I was
going to say would we well change signature first I guess depends how many people are using whether it's being used in
other tests or just yeah so we we we sort of have two ways so whenever we change it whenever we want a different result
no punen intended uh not that result whenever we want a different return value a different return type um we generally
have have have two options we can change the existing method uh or we can create a new one that does that and then uh it
and then basically wrap it and then inline everywhere so that uh it it the callers get the right result so we probably
do want to look at what what are uh who is who is calling yeah there's only one uh ah a bunch of tests too many oh and
production code well I would hope production code um so then we would do something like this it's a horrible name but
we're not it's not going to live for long something like that create that method have that method call extract column
right and then it would oh I can't accept this phone call right now um yeah yeah so then the other tests the tests that
are calling extract column string keep working and then when we get to the point where we need to inline it will auto
inline but but it won't we probably don't want to inline it uh I think in some cases that that will work but I think in
this case um we'll just have to to change change some code line by line because the song parser is using it a lot um and
uh that that process is those lines of code are going to need to change yeah significantly to um so there are a couple
of ways we we could do this uh one way is um just write a new method uh another way is write uh write the code that we
want in it let's try that approach for a change yeah because we've done the other one so many times so um let's revert
yeah let's revert all that string yeah um and since we know that that is going to throw an exception we can wrap that
code uh I think we you can get rid get rid of I know I know I'm gonna go back okay we can get rid of this uh we'll
probably want to keep the message because the message is going to come from the result failure um so let's let's delete
just the 3132 and then let's do that for now and then blow it all the way at once yeah we can probably get rid of 3132
at this point and just leave the message um and then we can wrap that line of code 29 with a tri T catch and so we know
which exception y oops close this window so I get a bit um so if we do throw the exception what do we want in this case
we want to package object right that we can then test against right so there's a couple of static see ah it's a single
message actually will it always be I guess we will test for that when we it oh yeah go ahead well scoping yes is my o
yes um that's fine uh why don't we call instead of failure call it result because that's eventually what we're going to
want and we can now sketch out assertion I forgot you gota be patient yeah I never wait oh the scope right the scope is
yeah dot really there's no method oh because of the scope because it's not in scope so if you want uh before we write
the the assert we can pull it we can pull it into scope yeah is there a automatic no uh you can split into declaration
then move the Declaration up yeah oh yeah I was looking for a one step yeah there there would be a one step if you were
trying to reference it or if it was already referenced and then I could say bring it into scope but it right right so
that's that's what we'd like why is because it's not definitively assigned ah so what we want is um 31 we want to
convert that to a result right because we want this block of code to always return a result because this is eventually
going to be move oh interesting so the song yeah so hav gener because our result the only time we've used it is for
songs and we have not generified it to return arbitrary information so we might uh have to put this on hold and go fix
result of could you know we could have done a bit more planning and a little more design work um and maybe realized
earlier that we needed to have a more flexible result class we knew we were going to need a more flexible one at some
point um and so we could have thought a little bit more ahead and said oh before we even bother with this let's result
uh I I I would just comment it out comment out the the uh the whole the whole whole set there when you say whole set
what do you mean I mean I mean basically line 30 32 if we do 32 then oh I guess it's just a warning yeah it won't will
it compile yeah it will compile H maybe well we can run the tests if not we can just assign it to to to something yeah
so we can basically just uh do equals null there that'll just be a runtime exception yeah so that so well hey it worked
yeah uh that that doesn't make me comfortable no no no uh uh because we're not we're not checking the message let's um
I'm uncomfortable in making this well actually let's disable it um because it's not really a valid test yet yeah uh and
then we'll pay get just that one it looks like uh we've got a bunch of others which we will have to look at ah yeah they
um we have a couple where it says enable once we return result failure for mismatch column count we should add that
comment to to our current disable because I think there there are several that are uh basically the the same the same
right uh I would say let's do a commit even though I think we've only just modified this test it's probably good to make
sure we have a clean slate to go back to if we if we go wrong on on this next refactor I think we could just say we
started something yeah I thinking started um second to Fan van welcome from YouTube good okay uh you want to do a PA
factoring to modify um we want to see how much intelligence is going help us in generif Ying the result you can probably
like make that if you double click on the the editor interesting double clicking doesn't expand it no double clicking
that's as far as it goes that's weird that's different than on the Mac really yeah on the Mac double click um basically
expands it to the maximum the maximum size yeah I'm double clicking it might be can you right click and say uh huh I
don't see anything off hand there not a make full screen now I'm gonna have to go look all right well let's just
maximize it manually yeah maximize minus one so um let's let's let's see if if it gives us any options if we click on on
the result class uh uh we actually want to bring up the refactor menu nope the other one it's it's all the keys it's all
the keys plus T really annoying one right right but this only is a subset of what's in the menu yeah and I was just
seeing if if it offered that um I don't know if it has it has that kind of refactoring let me look at the menu the more
generics convert raw types to generics what does that do that might do it I don't know where it is on the menu um
there's a generics so you might have to bring up the actions yeah I thought I did but it didn't come up uh convert yeah
so the full so say convert raw types why is that not showing up for you you think this include disabled actions that's
fine it's going to include ones uh I don't know why that's not available for you um are you uh Let's Escape out uh what'
s the latest am I far behind oh you know what I think this is actually part of a plug-in so there's some plugins that uh
jet brains offers uh for more refactorings and I think this one is coming from from that plugin um do want to install
that plugin sure so um these are these are uh if you go to the plugins um where is it uh tools no uh no plugins under
under your settings oh Jesus brain for some reason I thought it was part of tools okay here so if you click on
Marketplace because you want to search plugins and you search for uh Java refactorings and there's the first one cool
install yep provides convert raw types to generics remove middleman replace temp with query and WP method return value
nice yes so wrap method return value might be something we also try looks so these are basically the more sort of uh
experimental I guess refactorings here why is it not did you restart the IDE no uh it should have offered an option uh
oh that may may may not require additional it may not require a restart okay okay so um what's weird is looks like it
got it got confused about uh let's open up the maven menu I don't know why it keeps hiding it for you it keeps hiding it
for me that's try I don't understand that um action I presume uh it's going to be under uh well yeah you can bring it up
that way and then let's check the settings maybe say says looks like it's there because it's got removed from sidebar as
if it's going to always be yeah maybe right can you right click on that does it give you the same menu not there but on
the on the all the way on the sidebar oh over here right mode it's pinned understand that all right uh if we click the
the refresh arrows there we go clean it up yeah there all these little little uh little problems that that intell J has
where where often that that fixes it all right we can minimize it um and so let's go to the refactor menu again option
so we want to drop obsolete casts yeah I don't think we have any uh preserve raw ways who cares leave object um I I don'
t know if this is going to do what we want uh we can just try but I just grabbed this um I think we'll we'll okay did it
do anything nope anything um let's try it again it it may only be suitable it may only be set up for certain types of
things like the this is this is where intell's documentation falls down it's like it doesn't give us the full parameters
of what it's going to consider right um because it basically says transform existing code that does not use generics um
but that's like okay what are things considers not using generics and what is generics aware uh let's try perform exhaus
of search about that you want try preview just that for no let's let's just do a factor it'll either do something or it
won't believe nothing yeah yeah all because what it's supposed to do if you look at the example that it's applies which
is insufficient uh basically if you had a list with that was not um so it I guess it's it's taking usages of things that
aren't generic uh and so yeah this a this is a refactoring that that would be nice to have but we'll just have to do it
manually all right so what we want then is let's um let's let's just generif it so the result class has two types it has
the type um although I guess really it only has one we could consider the failure messages another type but they're
always going to be strings at least in in our usage so we pretty much want to generif it based on right now it's h a
song so we'd like to to promote song to to be the generic um so meaning here uh well everywhere song exists in this
class we're going to have to change to to basically a t or some other named uh generic type looks like it's the well
there's song and then there's list of songs right but that's still that would still be list of T sist of T right so
those are the two places it would be from what see so um let's uh would you mind might move the two successes next to
each okay and you're gonna say something before I cut you uh so wherever we currently use the static type so our static
types are going to have to um change slightly uh but I think right now what we'll do is we'll focus on just making
everything everything backwards compatible um so let's let's go ahead and and add uh the uh the type parameter to our
public class result so on line 10 oh online 10 10 ah got it uh let's put um what do we want to call the type um for now
let's call it t I can't think of a better name okay we'll come up with a better name so that's still backwards
compatible and you we now see that intellig is complaining about all those results being generic um and uh what we'd
like to do uh is change the return types um and let's see if intellig will help us on that well it's just a that yeah no
it's not going to do anything like that uh so let's just change it so that this is um so this success will take a song
and therefore song like that yeah although actually we'd like T like that yes and then we'll want to and since we have
generics here we're going to need to add uh one more one more type parameter to the static method so uh in between
static and results on both 26 and 30 we're going to add T what's the multi select don't tell me alj so could I do okay
here oh no it's not going to grab okay what am I again you'd have to include static but there's only two so we can just
just type it uh so you want one and we're not dealing with failure at the moment just success right because failure
technically we don't really need to generif even though it's complaining about it um we probably will at at some point
um so this should not uh affect our our tests this should have something um right because in this case it it's relying
on on the type uh so what we can um we can uh cast 33 so let's make um instead of just Y and now there's sort of an
implicit loss or cast and so on that's why it's complaining about parcel but now at songs what do you think about
running all tests um we can I I'm mostly concerned about compile errors than than anything else I don't think I don't we
need to yeah so let's um let's yeah let's go back to result and uh we probably want to change now uh line 13 so
basically want to now start changing anywhere we have song to change it to T right uh you can make that final if you
want it's well it's complaining that it may be final yeah it's basically saying you could make this final if you want
have to um but I wouldn't do that because I would I I think that's off that it's a tangent tangent yeah okay so we got
that one so basically anywhere there's a song reference a song object reference uh or type song type reference T um
right now you'll pretty much just find any any compil errors in this code we'll do that we'll we'll show up because now
truly is a compile eror because we changed the internal type tests and again mainly I'm I'm saying run tests in in lie
of compiling because uh so we probably want to change our internal name of songs to be more more generic so right now
right now this will hold either songs or anything or strings or strings well strings yeah because the column data is
also going to use result so and that St just as a string so like you said basically anything um so when it's songs it's
songs when it's not songs what is it it's just going to be some success message I mean for me it's like it seems like
it's just value or values values well values for the for 13 so the idea of this result is that when it's successful it's
a container for what what is it that we actually want as a result of whatever we're doing so when we're saying parse all
songs it's a container for songs when we say parse this column it's a container for the column data and if we said parse
something else it would be the the else and we're going to want to change yeah which unfortunately doesn't extend to all
the static methods that are basically uh Factory methods so um right whereas this has to be value right but that's oh
you're saying you're thinking this one yeah it it it's unfortunate that it didn't pick up that one but um so yeah now
we'll just change them one by one so anywhere that song exists we want to change it to to value and then this we will
have to rename that but not just yet let's let's change everything internally first got it so then either internal was
value there anything internally so what does it offer to fix that uh and you'll basically do that for about oh wait this
is failure so failure though is still a generic type because we're going to it's going to hold only the failure messages
but it's still of the same type because it's still a container for whatever it is so we still need to generif those okay
but we have to do that by going turning this into a t no no no no it's still holding on to string it's just the result
object that gets returned is a generified type so we do the same thing we to the other static methods it's still T
result T even though it's not containing T's um it's still that's its type and this one's the manual one we have to do
yeah and you'll need the the T in front of it as right and then you'll you'll you can autofix those or just add the
brackets to the 33 and now it'll now it'll give that as a suggestion y whereas before I wouldn't right yeah that makes
sense so we should have gotten rid of all the um all those warnings so now I think we are fully generified um other than
the query method songs everything else is tests and everything still works y um I would say let's do a commit and songs
is that a yep okay all right um I think we could it I just want to see one of the tests this are we gonna make the test
harder to read so right now it's we're only putting songs into it and that's why it's called songs but because we're yes
yeah I guess there's no way to make it we have to change it from songs to values yeah it just means it it becomes a more
generic container just like a list right so then rename this guy to values right is that gonna have a collision well
one's method one's field be amazing we're already at the one hour point do you want to take a break or do you want to
finish uh generif Ying the code are we close um I don't know how many usages there are of result so how many usages are
there of of result yeah we're not we're not near done we gota basically change all those right now here is where
actually the generif might help because now we've actually generified results and so now the usages of it might be
available so we could could take a crack at uh the refactor uh from a usage point in prod or test no I think we just do
um we try from here from here okay uh and if not then we can go to a use a call site but let's see what happens said no
occurrence is found so let's go to um wait a second wait a second that's the values we changed oh the songs to values
right maybe we should oh too late now uh we can do a commit and then and then try this next step because we're going to
do a commit anyway yeah make sure you check uh so control K I know yeah control k um what did we change oh we changed
yeah instead of gentrification yes that would be a very different very different thing so let's go to a call site our
usage site and see if it can help us generif from there test how about that one sure or a column mapper no let's go that
let's go with that that you have to bring down the refactor menu yeah and then from here do convert rot types yes
where's the is it so in the status it said raw use of parameterized class result um but it didn't actually do anything
yeah um I had the selection on here what if this found yeah it still might not have enough information I'm I'm not sure
and this is again sort of what's frustrating is it it it doesn't tell you enough about what um because I would expect
that uh if you were on the result where you are now and you invoked it um that it would it would do something but us
yeah just the expect in expect inspection all right we'll have to we'll have to do it manually uh and this might require
us to simply just do a search a global search and replace but we can do that after the break if you'd like yeah let's do
a break that's a good point all right so we'll take a a f minute break when we come back we will do some search and
replace um and fall back to that uh to get our result object to respect uh the concrete type that we want uh and then um
and we'll continue from there stick respect the concrete type right all right so we'll see you see you five e so as a
reminder folks uh I run a Discord Community where we have a bunch of folks who are uh interested in and talking about
all the stuff that we do here on stream and that I do on my stream um so the best way to find out about that is to go to
ted. deev Discord and uh you'll find a link to the disc some information about it and a link to the Discord and you are
welcome to join um we also run a weekly book club we're currently reading the programmer's brain and as I say it's never
too late to join uh so if you join the Discord uh and you're interested in uh joining us for our Sunday discussions
where we do it over Zoom uh just send me a direct message and I will give you access to the private channel that has all
the past recordings and transcripts and chats and things like that uh and that uh available also free no charge so join
us um if you're not interested in the current book uh when we're done with this book we move on to another one and right
yeah sorry keep going no I was gonna say go ahead do we just start saying which one we want well I think we can I think
we can use search and replace to to do this so we don't have to do it manually every single place we do it ah uh so
asked how far we long in the current book we are in chapter six um I don't know how far away that that is through the
book uh feels like halfway probably close to half yeah um but you can join it anytime there's no uh even if you haven't
read it even if you haven't you don't feel like you have to catch up um even if you just want to fine we want to do this
to all files one so replacing files control shift R yep now all of these will be song because we haven't done anything
else yet correct um I would relax your search I think that might not find all instances uh that assumes that we yeah
relaxing that way because we also actually do want to change at least right now um uh I think we think we want to change
all of the method return values as well like uh replace all is not going to work we have to do it one at a time why is
replace all not going to work well I don't think we want to change jir well so you can change the file mask in the upper
right so that we're only looking at Java files PHP uh and you want to drop the result replacement and I don't know if I
don't know if you have a space at the end of resting yeah I we so you want that and then you want to replace it with a
space SP but this one but the thing is we got something here called song result which we don't want to change we want
the this one you want this one not this one right so if you uh click on the W in in the upper right next to the CC yeah
go now other than the comment which is fine I think we're good to go just turn scan you agree um I think the uh the
comment the first one that's in green if you click on one uh I think you just need to hit the delete key really yeah
nope that's interesting that's what Mac uh well that one's that one's harmless it doesn't matter it's a test with just
the middle of writing anyway so we can I'm feeling like it's okay so yeah let's do a replace all and see see what
happens let's compile eror that's fine I kind of expected that we'd get at least one um so here this is now it will work
uh if you uh oh run it well you need to click on the Red tsv song parser um and let's take a look at F2 uh what's it
complaining about cannot infer functional interface type uh yeah because it didn't generif because we did the W um
there's some places where it didn't generif the the list of results so we'll need to replace those separately manually
or uh with a search and replace so you uh no we don't want to change that we want so the problem is is you see on line
63 where it's a where it's list result that hasn't been generified and we want to generif that so we want to replace
list of song of song like this no no sorry I'm not correct so uh bring up no yep and did you copy it to the buffer I
wasn't sure what to copy my copy copy list of result so when I say of in this context I mean angle bracket it's a list
of result so result of song is a result angle bracket song but we want to do a search and rep place of that with
basically list of what what you've got in the in the in the two in the second there so put list in front of go so list
Ang open angle bracket and at space right so what we're saying is is it's a list it's not a list of gen General results
it's a list of results of this specific type right got it uh and you'll want to uncheck the the W because it's not a all
so now it can infer right so the problem is is is it's like it was a map of Boolean to list of result and I don't know
what result holds so I can't infer was so now rerun the test see if there there is let's jump to that one because that
was the one that we ran into before one oh this is our new test right uh so what's it saying the problem was rerun yeah
so that's a that's a a problem where uh it required an import because that class had not imported song previously right
all right all our tests pass um we've uh I believe we've generified all of our uh or at least most of our code perhaps
not all of it of Y let's should we enable this one and make this one work or um do we have more prep preparation to do I
think that's it so yeah let's let's shot so in this case it's not going to be song 30 right right because we either get
we failure what are you stuck on I want to look at results again to make sure I understand what you're saying string if
success in this case yes because extract column if we look at what happens on line 32 currently it returns a string
right and it also uh throws an exception if there's something wrong with the mapper right um if it can't find it it
actually returns an empty string so there's a case where there's basically two different cases where we're going to want
to return a failure message where the things didn't match or I couldn't column but let's start with making the test work
and then fail yeah so the thing I'm confused about is isn't the type of this different depending on whether it's here or
this part of the path or this part no no why so why do you think it's different well you were saying this one will
return a string well it will return a result of string a result of string so then right so instead of result of song
it's going to return a result of string other words the type that we're defining here is if get if it's a failure then
it doesn't matter what what what the container holds because it doesn't it's failed so it can't hold anything right oh
wait a second can't hold anything but I thought we were as far as values go it will not hold any it will not hold any
success values if it fails right but it's still of the type right it's B like saying it's an empty optional right an
optional string but it right think about an optional no no no I know but I thought we had a didn't we have a point where
it's like here it failed and here's what you gave us or is it here what you gave us not coming from the result it's not
coming from the results it's coming from something else okay messages so this is this is what's sometimes uh referred to
as an either uh in more functional languages it either has the successful results in which case the failures will be
empty or it returns failures in which case the success stuff is empty got it so whereas an optional holds either one or
zero or a list holds a bunch or nothing um this holds either right it has to be true that either you have the successful
results or you have any value in calling this either result or either um either presumes that you can uh specify the
types of of both options here we're basically saying it's always failure messages are always going to be strings got it
and then if we if we wanted a true either I would pull in a library got it and for us the result the failure case it's
just a string type so the typ or specifying is the success type um and so now that might provide us uh an indication
that we want to change so let's let's let's try that out for size so in the result class um rename the T this T that t
and let's call it success uppercase all uppercase all uppercase all uppercase is the uh convention for generified types
yeah got it okay yeah I don't think I've ever used anything other than a single letter for generified Tes before this is
yeah there's nothing I mean it basically says it just has to be an identifier uh tradition says uppercase although I've
seen places where people don't do it uppercase um but this this sort of uppercase tells you that it's not a variable or
it's not a class name name it's it's a in this context we want to refer to the same thing interesting okay so it's
interesting that it didn't t's interesting and I don't and uh I find that uh uh I think that's a bug in intellig that it
didn't rename all the t's so there's the static methods that where it didn't rename those t's now you could say well it
could return a different generif fi type for those static methods so all right um let's methods manually or uh no use
use shic okay because it at least renames all the ones in that method call in that context yeah this one yeah those as
well oh but success for success got it yeah this is where generics get often we we only are are are we're we're mostly
only consumers of generics um where it gets difficult is creating uh classes that are generic enter uh let's run it
again that should problem oh oh that's okay because oh this is the one we were we're not done with with that with that
uh so let's um let just comment that out just to make sure that all the other tests pass okay great and they do um so
yeah so let's let's get back to what we're doing so we have so our type in this context it's a list of results uh sorry
it's a result of string uh which means when we create our result with a success we need to pass it in the correct type
which in this case string you mean here well we already have the string we just got it on the line above right so
writing code that if it extracted Y what are you what's what's going on I was just saying it was it was a red thing I
was just curious what it was oh complain it was only read for a second it wasn't actually red ah so this is uh we can
now if we want assignment and I don't think we need to comment anymore so this is the code that um will'll eventually
want to push into our uh column mapper right because this continues to pass and that's what this is doing now is it's
translating the exception into a huh okay so then would we extract this into a method push the method into the column
mapper yep okay so give name again this is shortterm name right so the what I tend to do the temporary name that I often
use is is I basically say whatever the old method was um and then then I say with whatever the new return value is so in
this case result yeah that makes sense all right um move now we should be able to do a move yeah do we keep the not null
there tests and doesn't just just run it again so the problem is is sometimes when it moves stuff around uh it doesn't
do an import oh so when it brought over not null it didn't do an import import previously when it introduced song it
didn't do an import but because we have Auto Import on uh as soon as you open up the file it does the import and
everything works got it do we want to keep that not no uh sure why not okay it actually uh tells intell that this will
never return a null uh which can help it with with some analysis all right um we uh we probably want to and maybe we
should have done this before we did the move we probably want to parameterize the the method a bit yeah I was just
wondering about that so should we re should we inline it and then no I think we can introduce parameter here that's fine
it's just in place so what are we in line what are we what are we introducing as a parameter column actually we want to
yeah we want to introduce that as our parameter because that's what extract column actually takes is that parameter so
we need to push that parameter uhhuh all right and so where do we get the failure message from we're not testing for it
at the moment we get it from result oh we should actually be testing for that so that change exactly it should just
contain the one actually would we um do characterization test no this case we're trying to we know exactly what it it's
it's hardcoded back so that it still pass it does and it does yep um so now we can uh generalize our code and say from
oh it's coming from the exception that okay any potential refactorings here I'm not well there's no point in refactoring
this because because a bunch of this is oh right because because right now what we're doing is um change maybe we want
to move this method closer to the method did it not move no it hasn't been moved you've just been scrolling interesting
it's oh control shift Arrow darn down I can't so what you doing I was just thinking about what the next step was okay so
what is the next step well we have to we can't do inline because I remember we talked earlier about that about how this
won't autofix we're gonna have to manually do it right right so I guess we just start manually doing it actually I think
yeah I think we just basically start manually fixing the callers uh and then we can that we that we can get rid of then
we can inline the other way um we can inline the current extract column into our the one that returns result and then
we'll be able to get rid of the and then rename extract column back to with result back to extract column y got it start
with the test first you think uh I think we should start with the commit oh Ying that's a horrible word generif Ying
maybe yeah is that good that's committed ready to roll all right so let's start let's start fixing our tests do you
think start with the test first or does it not matter I was leaning towards starting with the test first but uh yeah
let's start with with with a one and only test really there's only one test to extract column interesting so now we want
this one to be with yep and it's going to need a string now the name column so this is interesting uh uh for now um I
mean I'd probably rename yeah and then it's the result. values because we got to pull the pull it out container um I
don't think it's going to be empty I think it's uh going to consist of an empty string because that's our current
behavior and this behavior is going to change because we're going to want to return a a failure result for this one as
well right because we're not even testing for failure result yeah we're basically saying if you ask for a column that
doesn't exist you get an empty string um because that that's what we decided but I think we'll now that we have a result
class I think we're probably going to want to return a failure but for now let's just remain backwards compatible okay
so if we run the test this should fail because it's no longer empty right and one has to run you the helps yes so it
failed at expected and now we can make it pass uh contains exactly yeah contains okay okay all right great one down so I
think when we were writing these column mapper tests we were mainly doing it to uh uh deal with the edge cases should we
make a note that we might want to do more testing on this front or um so or do we wait till it rear its head I I think
we should should I think we should I don't want to disable it but I think we should make it we should definitely make a
note that um when we ask for col when column mapper when we ask column mapper for a column that doesn't exist uh issue
result let me just get the wording right again all right okay so let's go fix all the other usages okay interesting what
happens if I yeah it's going to replace it that's so yeah tab replaces inserts so now if we do here values have
something's wrong probably my comprehension why are you thinking that something's wrong why do you why do you think
something oh the red underline is making me well right because values many so depending on what you're trying to do um
right if we're extracting a column har song this is supposed to be just one song in this case it's never return the
result is a generic container right so like get first if we want to be Backward for or be like do I want to keep doing
time this is going to start getting a little hard to read mode not sure where I hit to jump oh there we go hey there
bash uh we're programming in Java so we don't use um we don't use the wrong way to capitalize stuff and now I want to go
methods methods started start uh methods uh uh start with lowercase letters as it should be what's the language that
does do that is it c as the main one yeah they basically wanted to differentiate themselves a bit from java so we're
it's like we're gonna do things differently for no reason and so that way you're going to get always confused class um
just goes to show people can get used to anything no matter how is so I didn't run all the tests maybe run the test um I
think that was the last one we'll go check in a to I assume you realize I'm not actually bassing bashing name oh what's
there Bash 1750 yeah so now here there should be only one two did we handle the themes I don't parer extract themes
right well I guess I'll just start typing here and see what it complains about so what that does is it means instead of
getting a stream of strings uh we basically get a stream of results um and so what we want to do is change our filter to
say we only want to pass through if it's uh if it's success so before we were looking for empty strings to to ignore ah
right and now we want to look for we only want to keep um uh is Success so yeah you can delete that and we can replace
it with result to success that one yep now that's mapped results um so what we and I don't know why intellig is not
showing that uh it should be showing that after we get a stream of results we still have a stream of results uh so we
can't convert that to a to a stream of strings so we need to to now pull out the values and flatmap them so what here do
a flat map uh no after after we've filtered for is Success uh now we map uh and we want to pull out the the the values
um a little bit more detail uh so results colon colon values ah and it's not happy um what type is it it's not showing
the type here which ISD yeah I don't understand why it's not showing the type there it knows exactly what the type is
which is a stream of result know uh what's it so what's it 59 uh cannot convert oh we have to say uh uh uh dot stream
after the values so we have we I don't think we can use um no we can't you that's a method Handler you can't call a
method on that oh so I have Lambda uh and then now you can say dot go I don't reformat that often and I don't remember
that shortcut let me see it's oh ah so now rerun the test I expect this to fail oh baby it did yep because we were
depending on it being blanks so we see we need to we need to ref filter that to Behavior meaning change this filter uh
no we need to add a filter after we've converted it back to Strings ah right because where we're getting an empty is
right here and so now we want to empty yep now uh as yeah as as to be expected so we rename this back to um yeah so now
we column everything should work but running test is cheap all righty so let's do a commit and then we've got some
disabled tests to enable yeah uh yes bash there's uh it's somewhat similar to link uh the stream API is uh definitely of
a of a similar idea of having a specifying a pipeline of thing um although I think link is is much more powerful because
it's basically a different in a sense a language all right so let's start re-enabling some of those tests let's um the
ones that are labeled enabled once we return result failure those are with want to start with song importer or lower
down yeah I feel like lower down is is probably where we should start start with this happens I was doing the starting
to read the test I'm glad you just said just for it you work uh I thought it should work um but we may see ah so what
happened was we basically um changed our failure Behavior so um we are ignoring failures because our TS our par song
does not return a result uh or it does not sorry it does not propagate the failures that we get from from our column
mapper to the result song but that's good so this test is failing in a sense for the right reason because we don't have
the correct column so extract column I want to just try and Gus you can close the bottom window yeah and you can close
the little dialogue there so keep in mind what it used to do when it encountered a problem it threw an exception right
so it throws an exception right now we're just grabbing the message M well we are stuffing it into the result failure
yes but is anybody paying attention to the result failures from extract column so column right so if any of those fail
it's it's not it's ignoring yeah yeah yeah it's funny I had in the back of my brain when we changed the first one like
hey shouldn't we be checking for failure and then I moved on with my these we're g to need to test the result the result
of string so what do we want to do if if they fail so this is a single failure message but there is the whole Paradigm
that we set up of having a collection of failure messages so we kind of want to mimic that and not just fail immediately
and just start collecting them right and where are we currently level importer so we're doing it at two places it looks
them right but I think I think what we want to do is we want parser right so we are returning a result um but right now
we're we're no longer only doing success we're only right so we'll have to do some sort of everything actually wait a
second yeah well there's also extract themes that one that one we're also ignoring failures we're ignoring I guess let
start with artist song title release title release type first we want to basically if guess we need to collect failures
well so so yeah sorry let's go one step at a time how do we make the currently pass where is it failing again four so
where would where would we like it to fail what is what is what is at a high level in English how is this failing what
are we asking for and why do we expect that it that that it should not work sorry I'm just getting my head wrapped
around something give me a second I I would I would say don't look at the stack Trad that's going to confuse you I I
want I want you to think at a higher level What in English what do we what's the inputs and what do why do we expect it
to fail right we're passing in two columns we're saying there should be three four that's not quite what we're asking
for we're saying row and what are we asking for we're asking for which is which is the request in to column mapper um
that's actually causing the failure and I want you to close the stack Trace oh I was even looking at it but yeah Works
what are we a what are we asking fail we're at asking it I feel like I'm going to come back and say the same thing we're
asking it to parse a song that has four columns two right and so how does it know how many that that it needs to to do
through the Constructor here it says right we need these four well three oh right the space confused me yeah Le three so
where does that um where does that check right here exception does it though so let's run again right that's why the
stack Trace was confusing yeah so but I wanted us to be clear about what our expectation was so we expected it to
internally throw an exception because the column counts shouldn't match um but we got something else right right so so
tsv song when it's parsed has two elements in it uh and column Meer when it's parsed has three columns in it uh uh and
now look um when does uh that requirement established it's not am I get I'm just well when does when does it get when
does when does column mapper enforce right it enforces it the first column right but the current usages are always one
column at a time so let's run this test again so now that we have uh a better understanding is so at this point it
thinks for Success because it's doing the success problem right so somewhere in here we have to make sure whether we're
actually succeeding or not right so basically artists returned a right so we could add in a check for not I hate to use
bang um well it's either that or you wrap the return yeah in and so now we'll move the error right so now now we're only
returning if artist is Success what do we want to do if artist is a failure right so we probably should change it to is
failure is is failure a no I I think C all right so now let's put in the else because we have to return something right
or we can just say return we don't need an else true now we haven't collected the messages yet well we're only doing
artist so there's only one possible ah place to from yep so bash mentions can't we keep you know can't we put on break
points in check um and that is against the entire philosophy of test driven development so what I find when people start
going into breakpoints is you've is you don't have a good is is folks end up not having a good theory or really
hypothesis of what's going on um so when I find people jump right into the debugger uh even if they have tests they're
doing that without a clear understanding of what is what is our expectation what should it be doing why do we think it
should be doing that and what do where where is it then actually going wrong there should be no reason to go into the to
the debugger to figure that out um it's harder because we have to think it's very easy to jump into the debugger and
start debugging and start looking and I find people then spend a lot of time because they're not clear what they're
looking for it's very much like something's wrong I'm just going to look around and hope something pops out yeah that's
why that can end up being yep so the failure is now a little bit more specific so it's close the question is is is this
now the was our expectation correct in the in terms of so we definitely got a failure we expected a failure um but want
so right now it's returning this yes and if that's what we want I mean guess the one thing that's missing is what is the
row currently contain right and is that valuable right so I guess we could but I mean I think the interesting so the
number of this format exists somewhere in some code or maybe it doesn't anymore uh in other words we could just change
the expectation to be this yeah it feels a little bit blind well so this again goes back to the question is is what we'
re asserting in line 169 at the top is that what we want I don't care what it does is that what we want do I kind of
like the current assert frankly yeah the current assert is want and so if that's what we want then we're going to have
to change more code but again this this process of we specify in our test when we're doing test driven development what
do we want regardless of what it currently does what do we want because we should want things and we should want good
things and I think that having it specified this is the row that we have a mismatch that should be in the output so our
test is correct the thing I'm wondering is where is this message coming did and we want to do eventually and this is
probably the time to do is we we'd like to stop throwing the exception because we're throwing it and then immediately
catching it and pulling out the message which makes no sense right because originally it was an exception it's
interesting I forgot about this yeah this I mean this this is the entire reason we we are moving to result is because
this is a validation error and we want to not throw exceptions for validation errors yeah so we're throwing it
internally because we've just done refactorings and so we've encapsulated that behavior now inside of here but now it's
kind of ridiculous we're basically we're literally throwing an exception on 21 that we catch on 29 right when I think we
can do that a little bit nicer but perhaps we should take a break first is it that time already wow it is okay so let's
take a break um and when we come back from the break we'll uh get rid of this ridiculous catch and exception uh yeah so
so this is the result of a refactoring we basically had done some work and we've done some inlining and we end up with
this thing which technically is is returning a result instead of throwing an exception but that's not what we what we
actually want we we want to stop throwing the exception so we can stop catching it and we can basically clean up clean
up this method and this is yeah this is all about validation all right so let's take a great e so folks uh you may uh be
aware that um I have uh a game that helps you learn some of the principles of test driven development so it's called
Jitter Ted's tdd game um as I mentioned at top of the the stream uh I played it uh at a conference with a total of about
20 people everybody had fun um Everybody learned something and uh so if you want to especially with your team play a
game that helps you discuss and and Foster discussion around test driven development uh and also have fun as as a as a
both not just a learning tool but also it's fun um so go ahead and and you can go to uh a website that's dedicated to
this and you can actually watch um a video so the video on on the site um over here is a presentation I gave a few weeks
ago to the uh agile lunch and learn group where um I talk about predictive test driven development basically the process
that we've been doing here on stream and that I do on on all our streams and uh then run through the game and show you
what the the game is all about um so go ahead and check that out go to td. cards and you'll uh see the the video and you
can always come to the Discord and ask any questions uh so take a look at that and think all right Mike there we go no
now um the double mute is over double mute yes double secret mute is over right so this is interesting we want to have
this message we're currently throwing that acquires we want to convert that to returning a failure point so we're
currently we're currently in Red so we either if we want to do any kind of refactoring we need to get back to green true
um which is an important feature of my game as well because there are only certain places where you can play the yeah so
we can either disable test again so the test is this it's not meeting our right getting back quickly to Green is there a
way to do that with a hack and then refractor well we could try the the the steel right lie cheater steel so we can lie
and steel and basically just return that hardcoded and see what it we know that's not going to work but we can also see
then what what else breaks right or if it does work then we know we're missing perhaps some some tests and but where
would we return it from because this is throwing an exception oh I guess we could change this to that then the failure
will get caught right then that message will get sent back yes so out no no don't copy what okay paste that test so this
is good because this tells us wh which test was expecting the stuff we got that we actually don't like so now we can go
to our column mapper test and say right and I think it's not so this should be something of the form well but then
change it to yeah one two three four actually this going to be different uh so the number of columns is how much six
then row contains I would just say run it and and characterize t uh although we can't characterize it because it's not
going to be characterized correctly so because yeah yeah yeah yeah but it's basically every it's basically just one
comma two comma 3 comma four comma five Etc yeah because there's no quotes or anything within the squares yeah so that's
what we want right now it should fail but it's going to fail in the way we want it to fail yeah right so now we can now
we can generalize that's here and the requires matching so actually was that in my pce buffer I want to see something no
I I forgotten what the syntax is is it basically percent s yeah it's percent s yeah okay um no we want to do a do
formatted because we're using the string formatter oh right uh tradition and Java to make that a new line like that or
no uh that's that's fine number of columns was so actually which one is it uh hitter column size columns length number
of right and had you hadn't if you didn't notice we would have noticed that when we ran the test size um and then the
third thing actually at this point can we yeah columns now how do we so I notice you hesitated uh and that might
indicate that our variable our argument name is not quite uh true specific enough however ref now well this kind of
refractor for for that where we noticed that we we stumbled um and it's a local name refractor I'd be fine with with
refactoring it um but let's get the uh yes so we want to be each of problem separ so it's not it's not uh compiling
because you're missing a closed br oh oh it's compiling but it's still not going to work though well it's not going to
work but I wanted to get us to it yeah shift rename yeah you want no this one yes within all all occurrences would would
rename any text that happen to use that it so is it rows requ well it's a single row row or row as columns or we might
just say it's columns and we just have to deal with it or columns for row colums either one but row columns sounds like
header in a way to me I'm I'm fine with with this and uh yeah let's stick with it yeah now because the other thing that
it might indicate as as well is there might even be a missing abstraction right okay so if you run this it's going to
fail because it hasn't dealt with the commas and the well it has but not in the way that you expected right yeah so
we've seen this we've seen this before um and what we wanted to use arrays but which method on arrays oh is it like like
literally like arrays dot kind of thing yeah and then two tab so it's either tab or enter enter go does that just comma
separated all by itself we'll find out so you're missing a Clos print yeah right so that's where uh your control shift
control shift enter will will be useful right so close um it it the two string already provides the square brackets so
we need to drop that from the string voila sweet I don't know if you noticed it was two tests that were broken uh
because for the last one yes because we we had add the extra bracket square brackets okay so we generified it but we're
still throwing an exception we want it to not right but we're back at Green so I right basically fixed interesting it's
only for artists that's the only test we have enable gotcha as they say tdd means whatever you intend is working um
works I don't remember the name of that test um well that's not the test that triggered our is it the it was the song
parsed one right it's a horrible sentence so this is a case where um my preference for commit uh messages are what did
we do not what can I figure out by looking at diffs right so this is um doesn't matter that we reenable the test it's we
handle uh column differences between the header data did we improve the error message or maintain the original one no we
actually improve the failure message oh right this for the required exception not the right okay sound good yep so bash
asks about code coverage I expect to be pretty much at at at uh 100% there's no reason you should be at anything less
than 100% putting aside things that are not Behavior like Setters and Getters that you might have on dto and things like
that but if you're doing tdd you're going to get um all all coverage of everything that covered now with that said code
coverage is a terrible metric and you should not have that as a Target goal for any of your work if you work in a place
that requires a code coverage percent you really want to have a discussion about why you're doing that because it does
not provide the information that you think it provides it does not say anything about the quality of your tests all it
says is that code was executed I actually think the word coverage is misleading and I wish people would stop using it
because it is not covered it means it was just executed as a side effect of your tests does not tell you if that code
was checked to see if it did the right thing which is what you want from tests if you want that use mutation testing if
you do tdd your mutation tests will will pass if you did tdd correctly if you're not doing tdd you're going to have a
hard time uh and it's likely your mutation tests are going to find code that wasn't verified all right now let's
refactor this mess we can start by inlining requiring matching count because we don't want to yep now our method's even
bigger that's to get bigger before it gets smaller yep exactly to at this point return a failure be yep and that should
be sufficient let me run it could still be green yep okay sweet so now are we ever going to get an illegal argument
exception anymore because the only time we were getting it was because other oh that was the only you inline the only
place it was thrown got it and so it's no longer thrown so we can get rid of the tri block is there a um you're gonna
have to delete the the catch Clause oh really in order to get it to um which means it's almost not worth it because then
you could just delete the try line there's no automatic I don't think there's an automatic way to do it there's not an
un there's not a there's not a remove yeah and you can just you don't need to select anything if you want to reformat
right that's true L but now we get this double oh we can just inline that oh um well that you can inline right there and
that got rid of the local variable because we actually weren't using it anymore right so that's better what else can we
block uh no it's actually used um oh out here yeah never mind but we can uh we can move it true and so this should look
familiar this pattern we have a a a basically a validation guard Clause that returns a failure if something doesn't
match um otherwise if it's successful then uh we do this part of me wants to give this a name turn into a method but
sure I I definitely love the require approach but that only works for exceptions that only works for exceptions that's
that's the downside of of using failure is is uh it it's a little bit harder to extract yeah what do we I forgot what we
called it originally uh require well here you have to rephrase it as not as required not as required as you usually use
is as your verb I don't really like that no not in this case if oh just like this number of columns match yeah if number
of columns match yeah so I'm again sort of like you got to tweet for it name it and then and then see does this read
correctly is there anything yeah uh yeah and is that the correct Direction so is is that is that truly saying number of
columns match header oh they don't match if they don't match yeah number of match of course I messed up but I'll fix
second made a mess there so bash we we'll get to your question in a second but we're we're going to do some naming stuff
here let's see my buffer did I have the right name I did okay so we probably don't don't no pun intended want the word
don't in here yeah I know I'm trying to figure out how to flip that so that um mismatched if header columns columns
great aing is hard so we're passing in the row columns name I don't know I'm still uncomfortable what the word mismatch
that to to and we can well we can expand any any any contractions we can expand so we can say header columns true and
then if we did that we probably yeah y okay can we make this even name I guess this could be extracted into a method yes
uh but I think we're going to be playing around with this because we're going to instead of returning uh an empty string
we're going to want to return a failure so I I I would probably uh I'd probably leave it for now but it may be prime
let's run our test make sure we didn't yeah so bash asks the question uh are we method is that is the meaning of time
complexity meaning is bashes in meaning like is it going to be too slow is that that's my uh that's interpretation
that's my interpretation bash if you're you're saying something else um but I'm assuming you mean do we have to care
about the time complexity the performance of of a method the answer is no now until well so the snarky answer is no not
snarky well with our coaches or Consultants head on is what's our answer there is it depends it depends so if you know
you are working in a context where runtime and time complexity are vital to the success of your project then you're
going to worry a lot about that stuff and you're going to do things upfront um that fulfill that need that means you're
working on something like a game that require a real-time game that requires uh sufficient performance and response time
um you're working on some kind of realtime or near realtime system General business applications and online SAS tools
and things like that uh for the most part there's no point in worrying about that because you're going to find out when
you actually do some measurements there is unless you are an expert there's almost no way you can predict the runtime
performance of code especially in Java it does two levels of of really more than that right it compiles code and then
that code is run in a a runtime that does all sorts of crazy optimizations uh that might be non-intuitive or go against
your intuition my favorite is um won't creating more smaller methods slow your code down and it turns out that actually
it can speed your code up which might seem totally like wait aren't you doing all these jumps or whatever because that's
might be the mental model you have about how code is executed but in fact that is not the way the runtime Works um so
the short answer is no I'm generally not worried about it because I will do um profiling of of it and then find out
where the actual bottle decks are and then and then fix those yeah pre what do they call it pre premature premature
optimization is usually a failing yeah so premature optimization is the is is the root of all evil um yeah that's it but
it depends on the situation whether it's premature or not right in this application and again in sort of most
applications that most people work on um this is performance is not a consideration and if you focus on performance
which is what people tend to do especially more Junior people because they were just taught in school about bigo
notation and it leads them to believe that that performance is really important uh when it's not it's understandability
and readability of code that is of primary concern which goes Q up rant about yes education system yeah that's I'm not
gonna cue that up no I know but it low you all can qu Quee it up on your own I'm sure you can find at least at least a
few in past uh I'll rerun the test I can't remember if so what do we want to do what do we want to do in the last 10
minutes or so oh time flies um do we have any some more disabled tests that we want to so we could tackle the ones that
stay yep and let's work bottom up again sure what's the deal with you well nope I'm not going to look at it I'm going to
do a Ted approach just delete disabled and rerun the test and false sorry it got a true or expected a false right and so
we have a nice error succeeded right we've only Built it for a single sense is this so and by Mak sense I mean is this
the behavior we want from our system so right now parcel the title is all returns multiple failure messages we have two
malform songs meaning the first one's the header is three columns so if we look at the failure messages the failure
messages no longer make sense given our our current context of parsing the header row right there is no minimum of five
anymore there's no minimum of anything right but we can repurposes test to we can change the header row to be five
elements and then that want do you want to give them real names or I I I don't like using bogus stuff uh I I like using
realistic stuff okay so so we can say theme one and theme two since those are valid columns sure and those just rerun
let's rerun I think this should work yeah we got what we wanted cool one more yeah written return so this is another
question of do we want to have required ater columns I think we do yeah um but let's defer that because that's G to be a
longer yep now this one a quick um but let's actually add a comment and in a sense a a a message to our disabled not we
haven't implemented it yet yeah desired yep that work yep okay just GNA WR around the test just to make sure it one is
also waiting for mismatch so we'll happens all right yeah so again this is literally the same change we need to yeah
okay rerun now we're expecting this to pass which left this is the last one yep for the same model we'll rerun it passes
yeah let's take a closer look yeah it is not it is not successful because here we have a weird situation um but it's
just basically at this level right this is at our service level we're just saying if we get something like this that
means there's something wrong now do we is this still a valid test though because could we in I mean you have to do a
really you know s on your head copy and paste out of excel to get one row with two cells and another row with three
cells I don't even know enough um Excel Fu can you do that can you well you can shift you can shift it you can shift
select um but I think the the lar the larger question is is what what is this actually testing yeah so the the test
method name unfortunately doesn't give us a lot no what are uh what are some of the one added songs are save to
repository bulk add songs using tsv format so this is this is mainly checking did is the service wired up to the parser
correctly uh in terms of returning returning failures so I think if we want a um uh a more realistic failure then we can
do what we've done before uh with those other add yeah give it give it sort of a valid failure then actually there's no
header so this would be released title this would be two that's well so that's interesting so this is this is no longer
two malform songs because it's missing the header so this is this is unrealistic data so we should grab a header from
somewhere that's valid that is that is completely valid one want well we want it to fail well the variable is called two
malform songs so either we change the variable or we add another invalid song another song okay so so this is actually
artist this or should we you know what it's confusing let's get real artist names you can just grab from the one stuff
yep excellent that one passes then we want to rename it so it's not quite so funky Y what we call this what's it better
um um Mal songs all right so we should only have one ignored test correct yeah one disable test yep that's the one
that's the one that we'll we'll want y so should we go to jir let's go to jira still giggle every time internally 72
that uh that I think we'll do next time yeah we should we is that part of the test that we issue this is required maybe
we want to add this as a as a feature um that's what I'm thinking yeah require columns I'm just going to put that there
require ensure r no this is this is requiring header columns you don't want to call them required columns you want to
call them specific columns well I prefer the term require rather than Ure um because requires an upfront check a
precondition check so we're saying that that uh require that header rows have specific columns yeah specified whatever I
got to fix the spelling of require the head of rows have specific columns yeah that works so we're going to work on J 73
next time uh yes someday we'll get to persist a database yeah I I was think we might get it to it today but but nope I
was thinking today too I know Dar it took us it took us a while to to generif results that was actually an unexpected uh
I didn't actually think yeah um and it's reminded me that I need to get my my button gear and spend some time doing
stream cotas because that stuff is still like my head's not crocking it or just do some intentional learning on that
front yep deliberate practice helps yes the thing that we wanted to do for creating a custom assertion for result um and
I think would like to do that this one move this one down is it within yeah we can move it we can move it down um and
that may also requires to also have uh some concrete sub classes but I think we'll have to have to wait on that um
what's the ordering we I kind of want to do the the custom assert next um we also are are missing some some tests so we
only capture failure artist right right now we're just testing for artists yeah um the question is will we catch that
when we uh I think when we handle the empty string as being a failure um I think we'll we'll start capturing that do we
have that as a Todo because right now there's no other failures that can happen to any of the other columns right so if
artist fails uh sorry if artist succeeds the succeed right we're not testing for the rest having well nothing can go
wrong with the rest of them oh right if artist succeeds then the other then the rest of succeed you have to explain that
so uh in what ways can extract column fail what is the only time it Reserve failure the first time we check it right and
whether if if the columns mismatch they're not going to suddenly match if the columns match they're not going to
suddenly mismatch um which means we probably want to promote this error yeah I say Mo this up yeah so it's less
confusing yes um but my point of the only uh when we get to the empty string that will be the other failure mode because
right now there is no other failure mode we have empty string on our list 73 ah it doesn't exist empty string got it so
those next three are next three tickets yes I I just like ticket even more than than calling it a jir number yeah y it's
even worse all right folks thank you uh for for hanging out with us um our next pair stream is probably not going to be
until till next week unless maybe we do something this weekend but um actually that's probably not going to happen uh so
um again join the Discord if you want to be notified more than just a minute in advance um you certainly appreciate
subscribe and follow on the appropriate uh uh Channel as it were um YouTube Please Subscribe that would be great um on
on uh twitch please follow that's great uh but you'll only get notifications when we go live so if you'd like Advanced
notifications knowing uh your best bet is on the Discord uh go to the Discord join the Discord if you don't already have
uh get notified there's uh you go into the rolls Channel and you click the little alert button underneath the the be
notified when uh I announce stuff around streaming I try to do that as much in advance as know about um sometimes it is
only 10 minutes uh but often it's at least a a day or two sometimes several days in advance so uh that's the best way to
be be notified and you can also then ask questions and have discussions about the stuff that that uh you've seen on the
stream um uh oh did you want to commit what we did you want to do that that yeah yeah we did and may we enabled a bunch
of tests and get them to work yeah but that's a high level it's not it feels like a little too abstract or you say yep
that's okay um I mean we we enable tests uh and revise them uh well and in some cases they just worked right we can say
and verify behavior and I think that's a really important step um often uh we look at tests and assume that they are in
a sense correct especially if they've already been there yeah that they're sacing that we that we must not touch them
it's like no do they still describe behavior that you want or do they no longer describe behavior that you want or they
describe behavior that you've you are now in the process of of changing and so you need to change your tests so it's not
always changing right so uh I'll be doing a solo stream uh uh tomorrow um not sure uh and I am running a half marathon
on Saturday so I will not be streaming on Saturday um cross your finger that the weather holds up um it's looking like
it'll rain a little bit but that shouldn't be too bad um and uh yeah so see you all on the Discord or on the next stream
and have a day
