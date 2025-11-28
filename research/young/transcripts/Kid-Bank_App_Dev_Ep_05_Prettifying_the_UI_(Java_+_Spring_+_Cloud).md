# Kid-Bank App Dev Ep 05： Prettifying the UI (Java + Spring + Cloud)

**Video URL:** https://www.youtube.com/watch?v=j9LRuU_SXZo

---

## Transcript

hi there this is 10m young also known as jitter Ted welcome to the series of recordings from my live coding series
around developing kid bank the money to tracker for kids this is episode 5 where I focus on prettifying the user
interface by making the list of transactions nicer and that's pretty much all I do in this episode so if you're not
interested in me fumbling around with HTML and CSS then you can skip this episode and tune in next time otherwise enjoy
the plan for today from last time we have most of the features we need other than persistence and so I thought instead
of blasting through to persistence it would be a good idea to actually deploy it so Heroku is gonna be my first target
for deployment mainly because it's so darn easy then once that's up and working then we can the other thing I wanted to
do was was make the UI a little prettier so I was playing around with oh one thing I forgot to do yesterday that was
it's kind of funny I didn't drag the doing to done that's kind of like the best part of getting something complete so so
let's see so tonight on on some styling I can find my so this is what I came up with I had to fix the color because when
I was designing the color I had my so basically the background color for here there's a little too green it looked
better when I had flux flux night mode which to reduce the blue so look it looked less blue so let me play around with
that color that one so it's a bit too green let's let's drop down the green a bit now it's just gray let's switch around
add more blue yeah that's kind of nice okay so this is basically a mock-up of the layout of what I want the app which I
guess I need to run again okay so that's running there we go so this is the page so what I want to do is the balanced
stuff here and the transactions I want to replace with with this much nicer looking thing so I mocked it up in code pen
so this is fairly responsive up to a certain point where if you squeeze it too much you're gonna get some wrapping which
isn't horrible because actually we're not actually displaying these as cash deposit or interest credit but actually
deposit or payment and I've set it up so that it's right aligned for the amount so that way the decimals line up because
I think the numbers for this font that I'm using which is new Neto is the numbers are mono spaced what we want to do is
is go into our template which is currently a single monolithic template which at some point later today will will
separate out into certainly pull out the the import because that's something that you will likely do maybe once will
leave the deposit and to spend money will also prettify those those later but right now we're gonna focus on basically
the balance and the transactions so let's close the run window actually let's just stop it because that'll make it
easier so again let's take a look just at the at the app once again you use the the import for pulling in a bunch of
transactions let's pull in these transactions okay import and uh-oh did something break Oh hello I actually stopped it
alright well we know what that looks like so let's get onto this template so basically I have HTML and CSS so what I
want to do is basically take all the CSS and this goes so we're using spring boot width which is basically spring we're
using the 2.1 line of spring boot which matches with the spring 5 framework and we're using for the for the view we're
basically using time leaf I don't know of any other one that's really popular time leaf is the one and so anyway the way
the resources work so we have a count balance at a template because at runtime that's going to get replaced with with
the appropriate stuff right that's what these th things are but what we want is to load up CSS and the CSS isn't going
to be processed by time leaf it's just a static file so we're going to put it good bank and we'll just paste this and we
need to reference the CSS file so we'll do that here god I always blank on CSS I feel silly for I'm betting that so
let's do this always like treehouse okay so I'll grab that it's a link and we're I remember correctly this will stuff
that's in static will end up being at the root let's just be sure that I have that correct so let's go to localhost and
we'll actually reference the kid Bank CSS directly and there it is okay so that's basically at the root relative to the
page so even though these are in different directories when they're in resources so kid Bank is under static and the
HTML account balance template is under templates and that's under resources eventually that gets all crunched up into
basically the root of the site okay so now if we basically go just to this we'll see actually we're and let's paste this
import and unknown well it looks like we've got a bug so unknown transaction type deposit Oh so it's possible I have
something that was just called deposit rather than cash deposit so let's take a look what did I have here so this one so
I had a one of the entries had just the word deposit instead of the word cash deposit so what we can do is just add
another case statement now first we need a failing test so let's do let's go and do a so these are all working ones so
what I'll do is when I do multiple deposits I'm going to call one of these just deposit and so right now so before I do
that this will do these Mazal run all the unit tests they run so quickly there's no point in not running all right they
all pass so now I'll basically change this to just be deposit and now I expect it to fail because it doesn't didn't
recognize deposit as a transaction type one thing I'm going to do is I'm going to prove this Aramis is just a bit
because what's unclear is it's an unknown transaction type deposit what I'm reading this I'm not sure is that somewhere
it was trying to do a crate deposit method call and it didn't work or was I mean we see it's in the Stephens yes the
importer but it'd be useful to have a slightly better error message so during CSV import it's not expected so that seems
kind of better so let's find that I run out now so you forget a better error message good error messages will save you
hours of debugging ok so during CSV import transaction type was not expected the other thing we can do is actually
display the whole transaction type one thing you might have to be careful of in terms of errors if you're ever throwing
it and logging it is that be careful that you're not exposing any dangerous or private information these are just
deposit I mean I don't think that's a problem for our application but it would be something that you might have to
consider like the actual transaction that failed somebody could get into the logs they might be able to figure but if
they get in to see the logs in this case then I'm hosed anyway so one thing that's interesting is right now we're we
could be throwing our own exception the other thing we can do because what I really want to do when I have this error is
not just say that hey deposit wasn't known but give me more of information about which transaction was not understood I
get most of that in anyway because it just parsed it but it might be really nice to see the actual full line of the CSV
that was that was problematic so we would have to catch the exception here I think for now I'm gonna put that as it to
do then we are add more error reporting during CSV import failure show the original line of CSV that failed to provide
more context okay so let's go back to our CC importer for a transaction dated and then we can throw in the local
big-time okay so if we run our tests we should see the better error message also telling us the the date of the
transaction that failed and there it is so that's all cool all right so now let's go fix this so we can handle all case
deposits and that should boom okay so let's go ahead and commit that fixed bug next problem not handling next not
handling is the transaction type from CSV important I want to make sure not to check these things in because that's not
actually part of this commit so I'll leave those okay and I say it committed there we go alright now let's restart the
app so let's go here control option R is a awesome pop-up that lets me select what I want to run so it restarted the app
because I had set the configuration remember from last time I'd set the configuration for the application that had
single instance only and that's this thing in the upper right here so that way it makes sure that I'm only running one
of them because I never want to run more than one at least certainly not locally all right so now that that's up and
running if I do import now so we've got most of the styling that we wanted so remember we wanted to look something like
this although I guess whiter so that looks good I don't even know if we need the word transactions but I'll leave it
there and now we want the balance to be to be formatted like this so the way that is is basically the word account
balance is just in an h3 and then the balance itself is inside of of an h1 so and that's inside of a header so basically
copy that go over to our template I'm going to just change the title give back balance okay so here we now have header
so we want to take away the word balance here we don't need it this is a span so technically we could just fit the span
in here like that yeah the shorter way would to be actually just put it as part of the h1 like this so let's just do
that no need to have extra tags if we don't need them do that it changes to h3 just see what that looks like okay well
well we'll do a sudo recompile to get timely to to reload the thing yeah so transactions now that's sitting here is kind
of not okay well so that worked really well because the CSS that I created was specifically designed for a table with
TRS and ths and so on I change this to description yeah well refresh the page and so that looks much better the blue is
a bit on the dark side so let's just do a slight cleanup on the CSS and make that a bit a bit lighter because when
there's so much of it it didn't look as bad when it was just less of it let's let's make it a bit lighter so 1.4 let's
try point 4 so that's the header background that's point 4 go back here reload yeah that's nice okay and looks like oh I
didn't notice this before we've got date action amount description we actually want to reverse these these columns
because we want the amount all the way to the right the other thing is we probably want to set a maximum width on this
because it's just too wide so first let's fix the actual problem which is that the columns are in the wrong order so
let's move and reload that and there we go so that looks much better yeah so let's take a look at what the width is for
so we set the body basically 75 and we want I should probably have at least a bit of margin because I know on my iPad
I'm not having a margin at all looks looks really weird okay that looks pretty good so we've got nice striping on the
table reverse chronological order we still have our funky huge form down here but we'll fix that later so let's say we
wanted to deposit $200 because he just got that as it as a birthday gift plus holiday gifts and his birthdays around the
holiday we deposit it and boom it has the right amount cool all right let's go back to our story um I haven't checked oh
I guess I should check to see if it how it looks on the phone so let's go into so responsive it's probably not very
responsive because I set the width to 60% and so if I have like an iPhone 6 that's gonna be a little hard to read maybe
I'll just leave the width and a hundred percent cuz probably most of the time I'm gonna be accessing it on on the phone
so let's make sure it works well on the phone yeah so that's better and what does it look like on my iPad looks good on
the iPad and if I happen to she's looking out on his phone which is about the equivalent of an iPhone 5 probably have to
play around with the fonts so I don't know how I have the font set up we have to do some offline research on some some
recommendations here but I think it's okay for now so it's pretty wide on a desktop but but I think that's okay not
terribly experienced at doing responsive without doing some googling so well I will spare you the googling and we're
going to call this story done I feel like I need a little sound effect to say hey you done alright so the next thing is
to where is it Soto deploy to the cloud all right let's be specific here we're going to be lips make few balanced
prettier so there's additional stuff that I want to do to make view balance prettier like there's some mock-ups that I'
ve got that I want to do a bit more because what I'd like about this is basically instead of having four columns it sort
of combines those four columns into two segments one on the left and one on the right and sort of emphasizes the
description or name of thing it's the way I was picturing it is that this would be the equivalent of four columns in the
table the amount would be as you see it in this mock-up this would be the date of the transaction this would be the type
of the transactions a deposit or payment and this would be what it was for there's another mock-up where they color this
instead of having it black it's green for income and red for spending so I'd probably do that as well that's this
mock-up so this one strangely enough this mock-up which is supposedly for like finance stuff has no decimals so the
other thing I can figure is they the designer is in a country where currencies don't have decimals so like you know
Japanese yen you don't have decimals because everything is rolling whole numbers anyway so this is this is the one where
basically it uses green and red to indicate whether it's a payment it's basically spending money or income income or
expense so I kind of like that coloring I'm I am one of those is unpopular opinion that I don't like dark mode so I like
white mode in especially in my phone apps so that may make the balance prettier is basically talking about that this was
sort of minimal styling just to make it to make it nice what else or on deploy app to Heroku so unfortunately there's no
audio for the part of the episode here where I deploy to Heroku and do some of the initial setup stuff for the
persistence so if there's enough demand then I may redo the deployment part but to be honest it was actually really
straightforward and this part of the episode was only about 10 minutes so you didn't really miss much okay thanks for
watching
