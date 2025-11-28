# ＂Song Themes＂ Episode 13： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=qTJzOlVebdw

---

## Transcript

all right welcome back to uh pair streaming here with with Mike Rizzy good morning Mike morning Ted how you doing I
think we're both a little little tired yeah so uh so it will be interesting to say the least and and I haven't done
anything in this regard for a a couple weeks so I'm I have to get my head back in the game yep yeah I haven't looked at
I certainly haven't looked at this Cod either I've been doing my own streaming but um yeah we have to get our heads back
in the game I've been having fun with taxes oh oh joy yeah I'm not sure I'm not sure I so so for those of you who uh
haven't either have completely forgotten what we were working on or haven't uh seen our stuff before um Mike do you want
to give a little intro about what what this app is all about sure um I volunteer at a radio station and I've been
collecting uh songs of various themes you know like Halloween Christmas New Year's it's raining out um you know all
kinds of things and they're collected on posted notes um handwritten notes text files and lately spreadsheets woohoo
getting modern um and it's always spreadsheets yeah it's always spreadsheets um and so I thought it would be fun to
share these lists with folks in particular with Folks at my radio station but also with the world why not um and I
couldn't find much in the way of interesting theme song theme websites they're mostly the top 10 songs about a
particular theme and it's usually Laden with a the website and it's usually very mainstream stuff whereas Community
radio stations tend to little be a little bit outside the norm um so I thought it'd be fun to build a website to share
it but hey let's make it more interesting just from a technical perspective how about we build it such that we can have
contributors and we can have people log in and people who become members have special benefits like building their own
playlists that kind of thing so uh that's what got us started on this road plus I got to pair with Ted so that's cool
yeah and so we have been uh so if you so this is episode 13 so we have a a we've been going for a while we have a
playlist um on YouTube uh and you'll find the link in the description uh if you're on YouTube if not um I'll pop it up
somewhere uh and we started out with uh some domain driven design stuff uh event storming to figure stuff out learn some
stuff there uh and then basically we've been test driving along the way and uh luckily last time we left ourselves with
a failing test uh so so hopefully that will help us figure out where where we need to go from here sounds good all right
should I bring up your screen sure all right and I I ran the test while we were talking we got the failing test and look
our jira says work on skipped empty Rose and literally that's the failing test so all sync so what we got here is it
looks like we were created a test you can tell it's been a while because I'm saying it looked like it looks like um we
had a test called skip blank rows rows and just to give you some context this was we were implementing um a parser for
uh bulk import of text that somebody would copy from a spreadsheet that's turns out in Excel if you copy from that you
get tab Del limited uh columns in the clipboard yeah in the clipboard yeah if you copy from clipboard and we're we're
going with the simpl thing that would work at first which is just a giant edit box where we can throw in the paste what
we got from the clipboard from Excel and so we've been coding that and we're now at the what if you have a blank row uh
Corner case and we wrote a test for it which is not fully shown on the screen there it is where we give it three rows
but we're expecting two songs and it failed right so and and I remember last time we were were like why isn't this
failing and it turned out we weren't running the test so always be careful which test you're running um even experts
like us make mistakes like that and it it's it's always tempting to run some subset of tests but in general it's really
a good idea to just always run all the tests and if they run fast then there's there's there not a it's not an issue
which is another reason to have running fast tests yeah so that you don't take shortcuts yeah so this oh sorry go I was
gonna say so in terms of running tests and tests run fast um I was doing something where uh there was some random you
random number or something else um and I'm like let me throw this in a parameterized test uh and have it run a thousand
times and just to show that that it is not the tests that take any time to run it took no longer to basically run that
test plus some plus a bunch of others than it did without the parameterized test so it was it was like oh wait it
already ran all of them wow that was quick um but it's all in you know if they're all in memory then the stuff just runs
really fast and most of the time waiting for test to run is is all the comp compilation and and jvm start up so y true
so we've got this test failing where um should we Dive In by the way yeah let's do it okay um and it fails because it's
saying it actually throws an exception from require we're getting the not of columns exception which is this code which
checks the number of colums we want it to be least nine yep so that's our own exception not enough our own exception so
now it begs the question interestingly enough here in the production code we parse the S this is a song um so now it's
like well if if there's less than Max columns is it really an exception case or do we do if there's one column we ignore
and anything from one 2 to nine is an exception like hey something's janky with your spreadsheet if you get like two
columns of data yeah I mean I think I I think for parsing so parse song is is basically parse a line one line single
line one line into into a song object um and I think if it's not valid we throw an exception it it needs to have you we
we sort of I think we agreed that that's got it's got to have have nine columns um right and so I think we need to look
out one level to detect whether there's actually any content at all um because I think what we're saying I mean so our
our test is giving us our intention what do we want right I'll bring up my my tdd game right the the what should it do
um what should do is is if we hit a blank line that that's actually not an error we just want to ignore it uh and so
that's that's what the test says we do it doesn't expect an exception so that's what we should do so I think if we if we
get a blank line there um and we can basically modify our uh our stream I think we can use a stream function to to skip
blank lines um that that should fix it got it so then what we'll do is um let me go back to the so this gets called by
parong right what we're gonna say is just don't let parong called get called exactly if it's empty right right so
basically don't bother even trying to parse a blank line because that's just we're gonna basically just ignore it yeah
yeah yeah so yeah my idea was one too low right makes sense y so we want to go but I think it's I think it's really
interesting like we are expressing the desired Behavior we're we wrote this test saying we want a blank line to be
allowed as input we're just going to ignore it uh and that's like literally what the test is is saying it the behavior
we want um and and I think it's it's under under estimated how powerful thinking about this in this precise way how
powerful that is like even if you don't do you know very short cycle tdd even just doing test first and really thinking
about what is it I actually want um just continues to to amaze me that I that I could have coded any other way it is a
hard to go back yeah because I you know I just I just know when I'm doing spikes or other stuff where I'm not doing test
first uh you're just writing it feels like I'm just writing piling on more and more code without because you you're
almost stream of Consciousness just piling on more code without really any justification um so a so uh so we got a
failing test it fails for the right reason um should we make it pass yeah so streams as you know is uh one of my
weaknesses so what's the what's the magic incantation to uh to tell the stream to say if this song If this line is empty
just skip it so uh stream has a uh a poorly named method called filter um and the reason why it's poorly named is are
you filtering out or filtering in oh interesting uh I wish they'd called it keep because that's what it's doing um and
so so filter takes a predicate uh so if you go on to half okay and then dot keep uh so it's not keep filter it's filter
yeah you already got me TR yeah um and so filter takes a predicate and basically a predicate is something that returns a
true or false so we want to say which ones do we want to keep are those that um where the string is not empty empty not
empty not empty yeah so we can do empty and just see the test fail uh so if you do a a Lambda or just string colon colon
we can go right to the um right to the capital or lower upper s okay second colon empty col double colon empty oh yeah
my bad is empty sorry lowercase i because it's a method that's all right you're Rusty I am uh so this basically say fa
this should this should make things even worse because now we're saying let's only keep blank lines right so let's run
oh yeah so uh what we can do is we can um invert that by wrapping it in a in a knot so there isn't a knot empty there's
not a knot empty which kind of sucks so we have to wrap the entire method call so you can do a AR I think oh if you want
yeah oh my case oh it worked anyways not yeah or yeah because it's GNA be there so this basically inverts it and so I
expect that it will fix all the other tests as well as fixing our current test yes all right uh weat La has an
interesting suggestion if you really like your your bangs then um uh then this is your your method otherwise I ier our
filter predicate oh my God I I feel I feel like I just need to like just delete all the knots and hey there wasn't a I
do like this predicate not that's pretty cool yeah so that's um and and often for that kind of thing I'll actually uh
make it uh I'll import the predicate directly so if you ask intellig it'll it'll not qualify the oh I see did you want
me to do that or best leave it for now we can just leave it for now but if you hit all Alt Enter you can see what it
suggests so we would do uh yeah add the static import so that would just get rid of the predicate dot that's cool I
think that's more readable I I tend to not use a lot of static Imports but I think in this case this is one of those
where I where I do it um what's nice is this is this is like super when learning probably good to have this for a little
while yeah and then like yeah okay now I know what that is I did undo the wrong way what's redo control shift Z there go
uh now you might want to give it a reformat because indentation got off oh yeah that one I don't remember um altol alt L
see if I see yeah Control Alt L well the cursor on the appen not in my notepad y that helps just to make sure I didn't
break yeah uh so brov you you can certainly ask um we may decide though that it's ask indentation still broken I think
he's pulling pulling your leg that's you bang ceremony all right so let's uh let's let's close this jira done then I
guess we got to figure out if there any other the- negative cases test do we what else might we yeah what else cover I'm
just going to do it a shortcut that I think is right but it's probably wrong nope I wanted to see the list of methods oh
uh oh no that's not it I have all these posted notes right in front of me but that's not one that I have I think uh
control F12 control F12 really that doesn't sound right oh that is structure I don't know why it comes up as it is it is
structure and it is a structure of the file um it is sensitive to what kind of file you're in so like if you were in a a
different kind of file then it would show you a different different structure um you can also make that window permanent
with uh alt 7 and that pops in as a tool window while it's in not Al not alt F7 alt in the number seven oh alt seven
yeah so so that's a tool windows that pops in and and stays there um so there's often a popup for for a lot of the the
tool windows yeah so what was talking about in terms of the indentations it's true it's like if we renamed on on the
bottom right the the tsv songs to something else then all the indentation would be would now be wrong oh but but that's
why I I ought to reformat every time I do a commit so it's not a big deal and actually that is an incorrect name uh
parsing a single song right no that's parsing all of them oh oh right right right it's the other one this one just a
single song yeah yeah oh hey you Alex I know the feeling I often watch videos in you know 1.5 two two times speed and
then it's slow and hey there 127 AKA Local Host nice um so what do we want to do next uh are there any other negative
cases that we of so we handled blank lines we handled lines with not enough columns empty row interesting empty Row test
how is that different than skip blank rows so that's parsing uh so that one we probably want to rename the method is
basically uh if we try to row then uh then it throws an exception ah right that one okay parse single parse empty single
row throws okay row exception exception just straight up exception yeah or do you want to name it I I usually don't put
the name of the exception in the in the test method because it's Crystal Clear on line 49 what what exception right plus
if you did want to change this then you have to remember to change the name method yeah yeah yeah that I'm not thinking
of any others but well so one thing we currently are not handling at least I don't think we are is what if one of the
columns exists but is empty so for example oh kind of if we left out the song or the artist was empty right any of
basically any of any of the columns columns that we're actually pulling out what if they're empty yeah I think we even
had it somewhere around here in our thing what was required I think I even used a star there it is yeah so the things
that were required with the themes theme or themes artist song title right so yeah that's probably something we could
add yeah um so an interesting question then is where do we where do we add that um we could add it in the in the parsing
in the code that's showing on the screen at the bottom uh or we could force um uh or we could basically make sure
integrity and basically validate in the Constructor do we validate do we do any validation in the song Constructor noord
yeah can check for uh for empty strings in in our par song or we can check for empty for basically clear sure each s hat
must have I would say not at least but um non-empty and is there any other validation we want around those does it
length I don't see a reason to have middle there's certainly bands that have one letter names song titles themes not but
you know yeah heck there could be a theme about you know Sesame Street the Letter A right so right I mean I would
probably call that the letter a rather than just a right but all right so then uh song um so then uh I think that's
probably the only other negative case I can think of um so let's let's do it okay so actually the doing it part we still
didn't decide whether we want to do it in the Constructor Constructor validation or in yeah so I think this is this is
Constructor validation um that's where I was heading to because same page yeah because and you want the object to
protect itself from having invalid data so it must check the incoming data to make sure it's otherwise it'd be feature
Envy right where it would be feature EnV yeah yeah because if par song was doing it then it was doing the work that the
song object should be and we could also do it in par song but I don't see much of a benefit um other than it has more
information uh and it's always an interesting trade-off of um so parong could tell you hey uh and actually even parong
couldn't tell you um we don't know what row it is we don't know what row it is yeah it could tell you what the whole
line is which makes it easier um because all song is going to tell you is like hey one of these was blank and it's hard
to find a you know it might be hard to find a blank artist um but yeah you'd want you'd want the be value in telling
parong what row they're working on for an error reporting perspective I I I sometimes do that but I I I really try not
to because I feel like cringy to me but I wanted to say it know um yeah so there is this there is an idea uh and and we
could do this at the at the parse uh at the top level parse thing is is basically um hold on to you know basically run
through the entire thing not fail at the first problem uh and and we talked about this before not fail the first problem
but basically then generate a list of hey couldn't parse parse these these lines and I generally think for this type of
thing um that's what that's what you want because it's sort of like you don't want to say oh great I fixed it and now it
shows you the next one that's broken and then you fix that and then you find the next one that's broken which is banging
your head against the wall which is very annoying uh so we probably want to do that uh so let's add a jur for that yeah
I was just going to say sounds like one I want to word this uh I think we can just say then uh to return all at right so
what do we do for parse problems what are what are our tests so that's a happy scenario yeah scenario uh that's a happy
scenario is yeah interesting one because what if I mean I wouldn't do this but what if the First theme was empty and
then the second one I guess that could happen I'm going to bring up the spreadsheet uh let me get one with here what if
um so like this song Heartbreak has heartbreak and sunglasses what if later on I determine you know it's not and I
delete it but I mean really this is gonna be a one bulk load I mean I guess it could happen but I think the odds are
screamingly low um I'm not sure we want to code for that weird scenario yeah I mean we could but you know I I agree it's
probably not not not high on our list yeah um so that one that one's fine that's basically saying we only pay attention
to those columns yeah uh so this one is basically saying if exception and rows with not enough columns empty row is sort
of the degenerate case of not enough columns right and this is only if it's the first row because is that right well so
one issue skiing empty rows well one issue we have in in this test is we're actually calling two different methods right
we're calling the one that takes multiple lines and we're calling the the par single line one directly right should we
be doing that maybe not uh that's like the the pars and a single line perhaps should not be public um because that is
somewhat of of an because really the entry in really the thing um so yeah it's a good point how many do we have any how
many tests we have testing that one just that one oh no two 20 no just one one test oh one test yeah so we could convert
that that test that's testing that directly um we should be able to convert actually so this is interesting since we're
now skipping blank lines that's what I was get heading with this is I think this one yeah does this test make any sense
if we if we made if we made par song private then there's no way this could happen correct um let's make sure of that so
let's change this test to call parse directly with an empty string and we expect it to just successfully so it won't
throw the exception and that's what the the error will go on yeah um what if we put a space in there or sorry uh what if
we put a a uh a back slash n for a new line oh I expect that to still be fine because it's just going to be now two
blank lines fine meaning still fail yeah because it's still not going to throw an exception um what if we put a space in
different area yeah so we basically said is empty not blank and I wonder uh if if uh we probably want detect that as
well so when we wrote there on line 19 we wrote is empty but really we probably mean is blank and if you're gonna change
that without a test I'm gonna be upset no we have a test well we have a test uh well but this is this test failing for
the right reason um perhaps we convert it well let's see this is the test we're calling parse now instead of a single
song so I think what we can do is we can for the most part I mean the name of the test should change yes well I was
going to say we should just delete this test and write one specifically about um uh space basically a non basically a
line right but I think I think I think so I think what we've done let's before we do that let's delete this test let's
change pars to commit yeah so I think is blank does handle all whites space we'll find out we'll find out um what do we
do we got working yeah so we have skip blank row us yep hey so now if we run the test everything should be green because
we deleted yeah rows and I think what no a bit too obscure to like put in a a space here because it' be interesting you
mind if we do that I'm gonna put a space here and just run it what happens because right now it's checking yes blocks uh
trim spaces at the end oh uh if you don't want it to do so one thing we you could do is is put in the space that one I
do not have memorized but I'll uh that would basically be back slash u0020 uh don't forget the U to tell it that Unicode
yeah lowercase you I think upper I don't know upper case would work but it's lower it yeah even because that happens at
the compile level so it probably doesn't doesn't matter um interesting uh so then how are we going to test this or we
have to do a non we'd have to do a non uh text block version got it let's put that back the way it was after ski empty
grow is that too subtle a naming wait second no this one says skip blank rows but it's really skipping empty rows that's
true so let's let's yeah and but I just feel that skip blank versus skip empty is very subtle well we could convert back
from the we could change the earlier one and just convert the text block to non- text block and that and then we can add
uh White space spaces more easily is that a um I don't know if intelligy will do that for us you can try with an Alt
yeah replace with regular string literal I think that's what you want so go and so now you can put a space before N I
was thinking doing is it 200 or 2,000 no zero it's z0 20 the reason that is having a I was thinking just having this is
really yes uh and then we can add another row we know we'll detect any white space but um that what you're thinking or
yeah and then back yeah yeah what is it complaining about at the end of line oh oh saying it can be replaced with a can'
t uh so if we run this we expect it to fail because the tab is not going to be detect actually neither one of those
lines is going to be detected and yeah that so let's go make the the the easy change columns oh interesting so if we
wanted to use the text block we could use a space if we specify it as an octal character as opposed to a Unicode what
octal yeah so if you do if you do back sl040 which is the unit octal for for space that will work because that gets
translated at a different time than the stuff fun knowledge about compilers good Lord um uh so we that's actually not
quite true um the the backslash at the end of a line does does something does something different so uh yeah so we
change that the blank sweet now we can get rid of this the beginning of a test we're jir Y and so just to just to
clarify uh so we l mentions adding a a backs slash at the end of a text block what a backslash does is it actually um
prevents a new line Terminator from being inserted into the string so that's useful if you wanted to create a long
string on multiple lines that's actually not what we want we actually want new lines right so the the back sl040 trick
is is is what you want if you want to actually space all right uh so we ski empty rows we ski blank rows uh and now we
can do some tests against song to ensure that songs don't have empty stuff yep um let's do a commit since we just
changed some code what did we end up calling that test uh fix empty rows actually we need to do one now it's black um so
I was going to say we should we should have a BL an actual empty then a blank uh and then a different blank and then uh
another row oh a separate test or all within this test we we basically had taken out the one that's empty so let's put
the empty one back so this should be skip empty and blank rows okay because I'm fine with having the spe in one test
cool is that what you were thinking yes it yeah uh so so we all asked a good good question I was I'm actually curious to
like what does it do with that space does it does it do it correctly if if we convert it to a multi-line now what does
64 that's broken wow that's broken that's a bug that because that that won't work do you hey we just found a bu yeah or
do you think there's actually no but that it'll we tried that and the specification says Nope that won't work um what it
should really do is it is the only thing I can do is is put a back sl040 but that's like a that's a corner case but
still that's a bug that's that's an incorrect replacement are you gonna file that bug uh I will note to file that bug so
hey weat you just found a bug uh text block with my right so um let's do a commit again we sorry what did you say uh
let's do yeah so now it's well oh it looks like you you can use backs also instead of back sl040 does that mean space
that does mean space okay let me commit you want it um or do you want to move on I'm yeah I'm curious so let's change
the the the Unicode 20 yeah so um and now if and now if we and now if we ask intelly what would this look like as a text
block would it do the right thing this time probably because it just takes the backslash s so does that work Let's do
let's let's replace it and see if that works that I think will work because that doesn't get replaced during parse time
yeah it's it's cleaner um if I didn't know what SLS was I would go and look it up go look it up yeah you know I think I
yeah cool let's check that one in now thanks for the caffeinate as um yes and this is this is why you can't use the the
Unicode because it happens during basically parsing your source code that's replaced at that point whereas the back
slash S and the backs slash 040 those are parsed later uh and so they remain um so compilers so new test uh yes new test
um and this will be in our song do we have a song test we probably don't have a song test don't believe we right because
probably a record because it's a record and it has no Behavior so we implement so constraint yeah sorry what did you say
I was saying we're we're about to implement some test get sh alt shift t no no oh I mean you could generate a test uh
that'll work too what were you thinking with the all shift t uh that that is a more direct way to get to the test class
the same thing yeah yeah yeah I just do this one for a change change of above you want to do one per or do them all in
one like empty uh let's do one and then we can decide what we want to do after that first one because I'm thinking we
could do them all if if the error message we can figure out what kind of error message we want um or if we want uh we
could also do a parameterized test but let's start with the simplest okay we don't care about that one just read blank
blank so I would say to to be clear about this test what um I'd want the only thing to be blank is the is the artist ah
yeah right because y otherwise blank um yeah it's fine it is right okay although my my code OCD is going to complain
that your theme has an uppercase te at the beginning and no none the others do it's funny when I was typing it my part
of my brain was going something's wrong there but I just was so focused on the a song well so the question is what do we
want if we try to create a song with that we're likely gonna need to throw an exception yeah it's the wrong yeah so I
think what we can do is we can say uh uh assert that um we can start with illegal argument exception yeah that one first
one uh then hit then hit uh enter and then dot uh is thrown by uh and now um no no we now we want a and then you can
copy the the call to the new song so we don't need the variable song we just need the the new song to The End Of The
Line got it so what we're saying is if we call a Constructor with this with these parameters we expect it to throw a
legal argument exception like that yep semicolon Yes that helps okay now this delete delete 14 because we don't want it
to throw the exception there so the entire test is is basically is in is just the assertion yeah got it so now this will
fail because it's not gonna throw this will fail because it's not gonna throw anything yeah or it better okay uh so Alex
asks uh will we in general have validations inside the domain model yes that's where they belong um so invariance which
means things that the object should not be allowed what State Should beow like basically this is an invariant we're
saying artists cannot be empty uh so you should not be able to create an object with an empty artist that's an invariant
right it can it it must must have a non-blank artist must have a non-blank title and so on um there are validations that
you might do in the adapter such as may as well check it at the at the front end if there's uh an empty artist you could
probably even push that into the browser so that you could never even submit something so my my goal in there's always
two different kinds of validations there's what I kind of consider syntactic like something something's empty it
shouldn't be something has a character that's not allowed uh or is missing a character that it needs like an email
address I'm going to check for an at sign and a DOT and that's it I'm not going to do anything else um and that I want
sort of as close as possible to the to where it came in so that I can provide the most useful error kind of response um
but then there are domain invariance which can only be done uh in inside of inside of the domain like you know you can't
have more than a 100 songs with this theme or something like that not that you'd Implement that but that would be kind
of invariant that could only be detected in in the domain or inside the application so so would um so for example the
email thing looking for a at and a DOT um you check that you know as close to the the you know input whether it's a UI
or rest call um but does that mean you would not check it at the Domain level no what I'd be checking at the Domain
level um is did the user confirm it because to me there's there's there's no point in even having some complex regular
expression I've seen seen this happen over and over again where people use some complex regular expression to say
whether an email is correct and really it doesn't matter because it may still pass the regular expression but they typed
it wrong or it's not their email and so there's no point in doing any other checking other than minimal like you forgot
a DOT or you forgot the at sign um but anything else you should just basically then send him an email and then when they
click a button you can now say it's confirmed and that's that's do that's in in the domain okay I guess I let me choose
a different example um the one where that no what you said is great um but I'm thinking so for example this right this
where we want song to be not empty like you said I could imagine us wanting to have that checked at the front end yes
but I can also Imagine The Domain object going yes I want to make sure this is yes and so this so so Alex is right here
you generally have to duplicate your syntactic rules your syntactic validation rules because you definitely want to
protect your domain from having invalid data you don't know where the data came from but the adapter also wants to be
responsive and friendly um as well as you know maybe there's no point in even forwarding it on when you know it's it
can't possibly be right like this should have been this ID should have been a number and it's got letters in it there's
no point in trying to create an ID out of it because it can't possibly work uh and you can respond better because you
have more information like one thing we notice with the parsing the songs is when we're down at parsing an individual
line we don't have the the larger context right and it's the same idea with the UI with the UI we know exactly which
field you type this in and we can basically in the controller saying this this field is invalid and in fact we can push
some of that validation onto the framework so you generally have um and I have like a an hour and a half long
presentation on on exactly this topic of validation in hexagonal architecture uh and you end up having to to duplicate
these rules which I've seen time and time again um people trying to shortcut that and say let's create the rules on the
back end and then we'll translate it into something that can be done on the front end uh so they'll basically take some
kind of domain specific language of defining validation rules and then having a way to translate that into the front end
in in JavaScript and things like that and that can work but it feels like um now you're maintaining multiple things but
if you have a lot of that kind of stuff then it then it can definitely be worth it man there a reaction it sounds
extreme dry and you you you have to make sure yeah yeah great question Alex yeah um we're at the do you want to take a
break now yeah that'd be good and then we'll let's make it six or seven minutes sounds good so I'll set my timer let me
get my you do your magic off all right see you in see you in six to seven minutes all right and um before we get back
into it just a reminder that uh I have a Discord and so uh if you have further questions on this app or other stuff um
Discord so the link so ted. deev Discord gives you the link to the Discord if you're not already there if you are um
great ask questions get in discussions uh as you probably know if you're already in Discord um I run a book club and uh
we finished our last book a few weeks ago and we're coming up on Sunday to start our next book which is the programmer's
brain so go check out on the Discord the book club Channel you see the details and hit me up uh if you want to join it's
not too late in fact like uh as I say it's it's never too late right if you missed the first week no big deal you'll
just catch up on the on the next weeks if you can't make it every time don't worry about that either make the ones you
can um but it's a great way to uh really read something more closely and get confusion resolved and questions answered
uh and just uh sort of share experiences with other folks so go ahead and do that coding I think there was a question
from lyrics I think what Ash is asking is like will we have lyrics in a future version of the site did I miss that
question it's right above Alex uh 951 oh I thought that was asking about lyrics for a song named song test but oh maybe
maybe I misunderstood it but we we are it is on our on our jera very far down yeah but uh including a link to lyrics
yeah I think including the lyrics itself might be interesting down yeah that probably some legal legal issues we can
certainly provide a link to lyrics yeah yeah I think she was playing with words but that but even uh even if not that's
that that's a that's a future we might have at some point yeah all right yep so if we're going to tackle this does this
switch from a record back to a class no you can still Implement methods uh you just don't have to implement all the
boiler plate oh interesting that's sweet so we'll in basically Implement a Constructor uh in indeed we will so um uh we
basically create a con so you can go ahead and generate a Constructor so if you're record um it Al to insert yeah yeah
there it is alt to insert and then Constructor Constructor and so that's that's the benefit of the record is you don't
have to specify all the parameters they're still available but you don't have to specify them so we have access to
artist song title and so on just straight up or you have to do like this dot artist Noe ah I mean you could do this dot
it's it's it basically is the same thing great oh sweet there jennice welcome nice to see you so let's uh let's make the
test pass to just straight up we want to put some text in there well would that well we're probably going to convert to
a custom one right probably and also uh we don't have a test for that right Point well taken I like the smirk well
deserved on my end okay let's run this test do we think it'll uh that looks like it'll fail fail or pass I mean pass
okay sorry I'm like what what what type mod did I right so what do you think grow this test to um check other fields or
have one per so now now we can talk about what do we want um to happen if both the song and both the artist and the song
title are empty do we want it to just immediately throw on artist or do we want it to to basically spe say that hey now
both are missing right well both are missing would be much uh I think in that case a new test yeah yeah I mean these
tests are are not long so right um although if we do want to convert the exception before we copy the existing test now
would be a good time to do that right so if we want a custom test sorry custom exception what would we want to call it
uh song Missing song attribute that's a generic one or would you want I was thinking it would be per like missing artist
but I guess the downside of that is well you can only throw one of them if you do it that way that's why I was thinking
more generic right so want to go where if artist and song are missing then it's G to go in the body of it or yeah uh yes
so James Boon brings up can the artists be null we didn't actually do a null check so uh we will have to we get yeah so
so that that's that's um that's actually a really interesting question do we need to protect against nulls it's because
generally the only way it through uh through the parse and the only and and you can't parse and and get so it's one of
those is like how paranoid are you um and I'm I'm fine not checking for nulls at at the song level uh it's kind of where
I'm at at this point because of the structure of it where yeah and just not to think too much about the future but like
okay coming in from a bulk import yes we're clearly dealing with it at the parse level right so then if we had a UI be
kind of somewhat similar where it wouldn't be null it would be empty it would be empty yeah yeah because any any nulls
we would have um yeah so for me I generally and this goes back to sort of the validation level uh areas like to me I'd
be validating around null at the edge of the system and assuming by the time you get to The Domain we've eliminating any
POS any possibility of of nulls um so as brings up again like do empty uh and we again sort of have to say do we protect
so is empty just means a zero length string is blank means has only white space um but at the song level do we test I
mean we already protected it well we're not protecting against individual I'd probably say we probably do want to check
for should not be should not be blank so here this is is blank yeah so if we're gonna want that to be as blank then we
need to add uh a test one I think I think we like I would be fine with one test that basically said blank but so two
assertions within okay or do you want to do the SLS to make it really clear I like I like the backslash s yeah me too
okay so now well we were currently in failing test mode weren't we uh it passed it passed for that and now it'll fail
again because we've got a a blank not an empty right so and then we can make it pass uh so Jonas we're we're in the
domain so we're not allowed to use anything from Spring um and there's really no reason to use spring in this case but
even so uh we're in our application layer and inside we're doing hexagonal so inside um we're not allowed to use
framework even though that's a library uh I would not be using I would not be way I think if you have a song title that'
s just white spaces you're gonna have problems in the modern world oh man that's a very Kian question though don't you
think man what a awesome comment James um tangent did you hear that they're playing long oh really yeah it's like you
know you play a note now and then another note a year from now right you know nice somewhere in Europe I can't remember
what it was are there song with blank spaces that's I I think we can safely assume that if they are they're gonna be
expressed using actual words yeah know it's the music geek and me that's going it wouldn't surprise me if somebody had
that but yeah because artists yes CA artists exactly as as a music librarian a volunteer music librarian I've seen some
crazy Co cases so okay so making this is blank them sweet so we could turn this into a parameterized test that might
make it a little bit easier to read and easier to difference I can go look for the I know we did it before uh what is it
is it is it at param uh it's at parameterized test it replaces it at test ah got values yeah so we have to figure out
want uh if we do a value Source what we want yeah value source is uh is good um so sorry uh value source is another
annotation so it's parameterized test with no PRS uh and then value source and then inside there we're going to say
strings lowercase strings equals and then open curly brace and then we have our two parameters blank and then if you uh
do an extract parameter on one of ones and then just replace this one we'll we'll delete the other one that's fine
assert uh and that's it that should do it test there you go and just to prove that parameterized test is working let's
add fail yep um and so since that failed but it didn't tell us why uh let's go to parameterize test and what we can do
is we can create uh so equals um and then and then a string in quotes will say uh oh this is going to be weird name and
then put like a single quote so space single quote so so sorry backup you want uh and then inside the single quote we
want a curly brace zero curly brace so what that does is that runtime it'll replace that curly brace zero with a
parameter but we're putting single quotes around it because we don't know in double quotes because we're in double
quotes we could Escape it but basically want to want to say that uh so now if it fails it'll should tell us why it
failed the parameter that failed yeah so it actually is the name of the test on the left oh interesting uh why didn't
actually you know what I don't can we undo this for a sec sure because if you look at what the default did I actually
think it was nicer see it says three artist oh that's true um okay then actually let's leave it I forgot that that's
where it shows up so yep so you can delete the Parn from the parameterized test then oh just straight them and then we
get rid of not playing baby right and then that should go back to wrong I think we just I'm starting to to like the idea
of just not saying much in the comments yeah you oh so if you click on amend the check box there above the then you can
just fix it yeah so I've on my stream I've been using um the AI to to write the comments and it's just so wordy and
verbose as you would expect from an llm it's just like it just it just writes stuff I'm duh uh sometimes it's useful um
but I I generally do not accept what it what it writes for me because it's just it basic say and so we've added a test
with to check for this exception to make sure that this is what we want and that makes you know and then it's like and
then it's just crap like you know to make the code better or something like that and it's like is it um yeah is it luell
that does the just Single Character commit messages uh for ref Factor that's Arlo B's commit notation yeah yeah yeah I
try sometimes to use it I just it's I don't do I don't use it enough um and since I'm not working in a team it almost
doesn't really matter that much as well so right uh so James is it good I have not found it very helpful um the chat
part so you can basically just chat with it has been what you'd expect I mean it doesn't feel like it's any it's maybe a
little bit more con it's more convenient than switching over to chat GPT um but I find the code that it useless yeah
somebody wanted the GitHub link uh I forget did you make that public I did we did it a while ago okay I'll put it in but
you'll have to repost it to um oh I'll I'll grab it that's fine you got it I'll find it here I'll so what's the what's
the next test that we want um right so now we want to do another another test for um oh did we want to change the
exception did we want to change the exception first we it right yes I sent the link to you via private okay so did we
come up with a name we didn't um we were starting to then it got attribute missing just attribute straight up or missing
song attribute because I could see we might have some other object where we're checking well it could be generified but
I guess we could cross that Vision I get to it yeah I'm I'm I'm good with missing Sol attribute just create a class yeah
just create a class it doesn't have a create exception uh not test that part of intell J drives me cre crazy yeah it's
one of those I I understand why it does that I just don't like it uh I think we just want to extend yeah and even though
for me it's technically ahead of what we need I generally uh override uh the empty and and single argument Constructor
because I know we're going to use it I think it's control two yep yep then you can close it we're not going to need it
again yeah run test it's gonna fail gonna fail because y uh so now do we want to get more detailed in what we're sending
with I believe we do yeah I guess we could make a new test for that or make it part of this I think we can make so I
generally have the message as part of the the test that throws the test for throwing the exception so we can say is
thrown by and then we can say has uh with has message with message I think it's with missing the artist has left the
building argument yeah so this should pass this should pass yes okay and so now um now we need to test for here uh end
of functor zero which which test method because we haven't done a whole exist uh so you you have test and parameterized
test you just need parameterized test they're mutually exclusive that was a bad which I actually think is kind of
annoying I actually would like it to be at test and then at parameterized right it's an attribute of the test to yeah to
me it's it's it's like oh now I want it to be parameterized it's like now I gotta change The annotation but I guess
differently so you think um uh Constructor parameter name or uh more English human readable song title towards this but
I think that's fine because that's really what it is now let's double check do this look fail all right uh so I just
want to um end ofun zero asked about something since he's looking at the project obviously uh let's just jump over to
the test go controller uh song theme control chest yeah and where within down scroll just scroll down um so the first
first test there's no results so there's not going to be any results uh the Line 39 is where we're testing for the
search results and all we care is that it's not empty right so in this case that's all we need to test we don't need to
test the actual song results because we already have tests against that and so this is where you don't want redundant uh
tests that are testing the same thing uh and and in general this is something that that can be a little bit hard to get
used to but this idea of um uh so James Shore calls it overlapping sociable tests I call them chain tests here the only
thing we need to check is that there's something in the search results the actual search results we are testing directly
against where that behavior is of actually getting the search results and so we're chaining together different pieces of
behavior um and this is always for me the the annoying memes about you know you know you always see these memes where
it's like you know uh unit tested but not integrated tested and to me that's just a complete misunder understanding of
how to write tests um like oh it's broken because you only wrote unit tests like well nobody said to only write unit
tests it's a STW Aon that makes no sense um but if you write unit tests you don't have to write end to end tests the
whole point is you write unit tests that overlap so we know that here we're going to get search results we know that at
the next uh layer when we ask the song Searcher for search results we get the correct ones therefore we know that if we
ask for that from the front end we're going to get the correct ones and then it's well how do you know they're
transformed correctly from song objects to what we see in the UI well it's like we've got a test for the the
transformation and so unit tests are all about making these very strong links that are linked together um and you get
all right so back to our song test so this fails um because we don't get anything right they're not pass oh there's not
a DOT throw oh there is okay cool so end of fun zero right now there isn't a transformation test because literally it's
the title um when we get to if when we get to more complex transformations of a song uh then we will have tests against
the song view object um but right now we don't have any tests trivial if it's trivial and it's easy to inspect then
there's no reason to write a test for it if there's no logic or very little logic then there's then there's no need to
to test for it tdd does not mean test every single possible thing right and if we had Getters and Setters which we don't
you don't write tests for Getters and Setters right so this is pass um but it'll be interesting when we start having
okay what do we want the message to be if both happen right but we'll cross that bridge we get to it I think we should I
think we should make that I think we should do that now because yeah because it's only gonna be point so now in this
case that would be another new test for sure that would be another new test yes yeah we want to d uh so it be artist and
right and I think here we can um not bother with the parameterize right because we've already tested the individual ones
now we're testing that they're that two two are blank however they're blank it doesn't matter yeah good point and it
doesn't like the name uh because it is a parameter that we're not using oh right um but there's also probably something
else wrong like curly what is it not happy about oh it parameter what yeah so intell when you select something if you
have the option turned on and by default it's on when you select something and then you type a double quote it's like oh
you want me to put double quotes around what you selected it does so it doesn't replace it and then let you start typing
which is what you might expect yeah um I gone back and forth about that option I I think I turned it off so what do we
want our go ahead yeah I'm at some point I want to speaking of options I want to turn this visual noise off to throw a b
yes can you can you right click on it I don't know if it'll let yeah so you can turn off the inlays so it's what's
called an inlay the problem so what you could what I generally do is I I have it turned on because for streams it's
useful uh but for these chain methods it's it's really for for assertion chain messages it's really annoying um and so
you can tell at how many lines to do it I don't know if there's a setting yet to change it for he only turn it on for
like streams I'm not sure was it called inlay yeah but you don't want to search for it there you want to search for it
where your cursor hints method change uh so no it's under code Vision um no sorry it's not code Vision it's method
chains yeah so you turn we turned it off for Java right and so there's no further options for like can you only show it
for streams and not for search oh it doesn't have that okay I thought I thought there is another place somewhere where
you can say it must be chained a certain number of times uh click on click on Java in in the checkbox tree click there
yeah there is on the right there's the minimum yeah so you can so I generally set that to three and then turn it on yeah
so I turn it on and I set it to three what do I have grab my Snipping Tool big um I mean I would just say artist and
song title are blank um but I don't like that sorry what were you laughing about I was laughing because you said R and
it's like oh then we'd have to have logic to convert from is to R and I don't want to do that yeah um I think we can we
can make it more programmatic and just say uh these attributes were blank attributes and if somebody says but you said
these attributes you you had one somebody's gonna complain about grammar I'm gonna just ignore I'll just ignore them
we'll them well interesting so comma artist Comm yeah so we have to build up the message and then do that's luckily
that's easier yeah so the string collectors join the string joining stuff makes that easy variable oh no oh right I know
what I enough h well the context is such that you can um so what I would what I would do is uh change message to be
attribute and message and we start building it so what I want to do this is is kind of as a refactoring so um let's uh
you're saying rename this attribute yeah so rename this to attribute but let's go back and and disable the current
failing it just to make sure it's still yeah actually it's probably gonna break because we're no no it's fine yeah yeah
yeah because you just extracted the string right um so let's now build the string the way we we want it to so let's
change that first test to be right so sort of go back to to the one case um where it's going to be these attributes were
blank colon and change that for both of them or we could do one at a time yeah okay so that one will fail and then we
can build the message in the Constructor call to nine right so so attribute should just be artist then I'm just brute
forcing it here I think something along those lines yeah in Java is this a legit uh syntax oh well I'm I'm not sure why
that like instead of using a builder no no no just say message plus plus attribute oh here ah yeah so that should make
one of the test yeah we haven't changed the expectation for the other one so they should all pass now they're all
passing right yeah so now let's do the same thing for the song title change our expectation in the test similar and then
do do the similar thing to well it should fail first right so I gotta that it fails yeah then we'll do the similar this
I think that's right let's ask to test yep sweet so now we can do a little pull um up well let's do this uh no so we
could do that that doesn't get us much where we want to go so I think where we want to be is um basically a list
problematic start collecting them basically yeah so this is this is basically a prepare factoring we're not changing any
existing behavior um but then once once we do that the uh the other test should should pass so would this be is there a
way to do what I'm just did instead of in a non-manual way um no but um uh but let yeah so let's I mean that should
still work yeah I hope collecting so we just do it like a you said array but would you just do a collection um well we
want to do a list I me we could do a set but a list has name attributes i' probably say something like uh invalid
attributes oh that's even better yep um so we can say is just invalid attributes just straight up well this will
probably fail because it's probably going to format it as a list with like square brackets but let's let's see if yeah
right yeah um so what we want to do a we could either do it uh a stream and then collect or we could just use uh a
string Joiner let's do a stream to collect so stream and then do collect uh and then uh collectors. joining jooin want
me to change it um that's that's available we can see if join well that works so let's try see if there's a do join
there's joining yeah that's what we just did oh yeah so that's what that's what we need okay uh what is uh intelligence
probably suggesting a better way to do the collect uh but yeah fix what what did I do place I was just going to undo to
go go so uh UNH highlight it's interesting look at what's at the bottom here it says can be replaced with string. jooin
yeah so it's string. jooin um so let's try that so you need to UNH highlight and it so UNH highlight like that yes oh
and go here yeah yeah join uh it worked are you I heard a hesitation in your tone Oh I see what it did okay yeah that's
that's fine um what is the first parameter no no I'm just wondering what the first par what's the first parameter to
join message can you put the cursor inside of join yeah ah so that delimiter is is we're going to want to change okay
but we don't need it yet but when we do the when we do when we do for multiple then that'll change right so let's do the
same thing for the same refactoring for title one plus sign too many so that should that should still first all right
and so now what we can do um is uh we we could do one more preparation but then that would make the other test pass and
I'd kind of like to see it fail and then for us to do uh the right test so it should fail because it's only going to
have one of those I guess artist first refactor uh now we can refactor this out so 13 and then we can move 16 out and we
could run it and this will fail in a different way and probably break a whole bunch of tests it did yeah um but that's
fine uh and so statement uh if invalid attributes is not empty not there is no is not there is no not empty yeah
actually I guess I could I could do this AR and then not uh no you can't do that that's only for predicate ah so just
bang it y That's the only thing you can do I mean you could say equals false um I don't know that that's necessarily
better uh also make sure you put curlies y so this should fail because we don't have a comma but otherwise the other
after the join yeah but the other test should pass so it should still only be then the one failing test and yeah yep and
let's make the awesome so we've got song title get Artisan song title what was the other one artist song title and then
themes okay so they me to do a single one for blank and then this one would be three uh sure um I at this point I would
want to um par basically well I'm tempted to Pro to to extract and parameterize our assertion for the well for for so
for all the tests oh right because uh because we're constantly doing the same uh the same um this this is one of those
where I'd be fine not writing an individual test and just changing that third test to themes but then but you wanted to
parameterize this or just change this one uh because it will then definitely check all three because it would have to
statement yeah we could parameterize it yeah uh or I I was wondering if do we need to parameterize it I think is where
my head was going well this one's empty um well I guess I I don't know this this is one of those like are we being
pedantic or do we just want to get real work done because yeah you know if if I was if I was teaching this then I might
say yes let's write that third test to test both kinds of blanks um and then put one here but I feel like we know what
we're doing we're always using do is blank and so let's just add a third one so let's just let's just change the the
theme to be blank in this test uh and then change the message so would it be a list of or would it be a blank would it
be like that yeah it still has to be a list right because yeah yeah now yeah I guess it would it' be just theme it's not
I I don't know that it's worth reporting that you know you've got two two blank themes because I because we pretty much
stop processing them once we hit a blank anyway fail yep this one's going to be a bit trickier I um huh if themes is
empty but there's probably no way is blank yes we probably need a separate something very we need a separate error empty
so that's not the test we're trying to solve right yeah the test we're trying to solve is that there's an empty uh
string yeah let's try oh wait a second oops Yeah me to change y now this will only work for contains that which is not
quite what we want so uh when you say contains that so contain so that's an empty string um so it might make this test
pass but it won't satisfy the blank right so then do we write a separate test for blank no let's let's put a let's just
make the list have an empty and a blank test or I guess we could parameterize that we could we could parameterize this
whole test so let's let's actually do that I think that's probably a good way to currencies oh yeah we're gonna do that
let's parameterize it all okay because that's what we said should be empty or blank so let's do what it says on the rute
I don't know what else to call it that's fine I was going to say just copy what's what we yeah oops so this will Now
fail because theme space yep so now we need to write another test well no what we can do is we change what we can do is
we can change that to to themes uh convert it to a stream and then find blank so you're saying um it's actually the
opposite of it's basically all match okay yeah so so stream all match uh and our predicate is uh uppercase string colon
colon yeah so you can have the predicate not and then it's blank is that g to fix it or is it just going to change the
to when it goes to the parameterization isn't it going to make one pass and the other one fail no we're saying is blank
and none of the match is blank uh but we're saying not so we're basically saying all are not blank I think that's right
okay let's see what it says our Tes tell us oh unhappy H so it's parameterized test it's going sending first empty
string can we just double check that first failing test I want to make sure that uh in our tsv song that we're that we
we actually have there so match well shape to run the test and find out yeah no interestingly it's the same error
message oh the predicate shouldn't be not we're basically saying if it has any problem and it should be all uh I mean
any or all it doesn't matter prefer all no in this case it should be any when it was not it all made sense sort of uh
but basically now we're saying do any of them match yeah so James Boon was right except James you didn't tell us wrong
right because what we're saying is is we want we want to to throw an exception if any of the entries in the done yeah so
this I think somebody asked I think it was James what if one's blank and the other isn't yeah I'm not terribly worried
about that because in a way that's covered I mean we don't technically have that cover it I don't feel like I I I need
to I mean if we really want to then we can copy one of the the tests above and pass in both values for pass in two two
different blanks to list to to the list yeah so have the list have two separate blanks um I'm okay with moving on um I'm
fine with with moving on I mean if we end up having a quote production yeah okay uh jir yeah yep actually yeah I guess
it's done we we're sort of the exception but we don't do anything with it at the moment nobody's catching it but I guess
it would go all the way to the well yeah I mean we didn't we we didn't say handle this at specific levels we just said
that make sure song is is is has abides by its invariant right um yeah so if somehow uh we weren't checking our
validation at the adapter um then an exception would be thrown yeah when we try toate this yeah uh so end functor zero
asked this question earlier I don't know if you're still hanging around um when I do mappings from domain entities to
any kind of dto uh I'm always testing it um that's the cost of mapping but it's also the benefit of mapping uh if you're
always doing onetoone mappings I'd be questioning whether you actually have domain objects because to me it's IND
indicative of your domain objects are just data if it's always a onetoone mapping to a view not that that's a bad thing
just that it's something to to be aware of and if you have a lot of those then you might want to look at Auto mapping
tools um but uh I'm going to want to test that because honestly I see a lot of commit uh do you have reformat on Commit
because I noticed there's some Tech code that's not formatted can you hit the commit uh let's do reformat code the top
one ah there it tests but no we learned that run all test happens after I know it happens after yeah I have to check on
what on that issue annoying all right we can close that um it's pretty much just the I'm sure 55 exactly I will laugh at
that for a really long time so now it's running all the tests which is great except ex great but late all right cool I
mean I guess it's better than nothing because you'd find out like all of a sudden it would pop up with it with saying oh
a test failed you'd be like what um and then you can go amend your commit but yeah all right um what do we want to do
next oh we've got this hold on to parsers to return all at once so I presume that was for this test the parser um here
we'd have we'd want to look at uh where would we want to collect those problems um this gets us back back to I think we'
ve had this discussion at least once which is uh ARS currently returns a Lissa's song because there's a an assumption
that it's going to return a list of valid songs and that there's no problem and that if there is a problem uh we throw
an exception which means all we know about is that one of the songs was right right then if the next one's not right
then we don't know about that um so the question is do we want to do that now uh or do we want to move on to more
feature Behavior yeah I'm kind of jonesing to move forward a little bit I must say yeah so let's um let's clarify jur 56
uh to say that um return them all at once from the song parser parse parer that good um and you can put in parenthesis
uh using result result yeah yeah that makes sense all right um we already getting close to our end time but it' be good
to kind of think a so do we would we want what would I mean different next steps we could do is we could have it so that
we build the UI in but then we won't be saving it persisting it in any real way it'll go away once we shut it down um we
could then right but it's so but it's so easy to import that you could just reimport it every time the server goes down
this is true I mean could do that for short perod of time I mean part of me is more interested in doing the um you know
getting the doing the authentication because we we need authentication before we can do the database right was that one
of our decisions uh well if we're going to make it public yes we need we need authentication before we can persist it to
a database right can you fix the spelling of authentication oh my God who did that yeah um did we do 3.2.2 no because I
I didn't I didn't do that I'll do that after so um so are we saying we want to do database or we want to do
authentication I guess we could do database without nobody it's not accessible on the website right does that seem like
the right approach is to do that first then do authentication then the UI or will the UI need the the authentication
need the UI Skin uh well one I mean I would say the authent we yeah we can do the authentication with basically a no op
UI that's fine so we can yeah so we can do it in that order we can do database authentication UI um or we could do
database any advantages of choosing one over the other depends what you want NE us to do next ah no I don't have a I I
meant from a implementation perspective not from a perspective I don't think I don't have a strong opinion Frank yeah I
don't think um I don't think there's any difference from an implementation perspective I guess let's do the DB first
then authentication than UI is well I mean we do have an inmemory database so it might make sense to to move to the UI
next um and so it's it's saved in memory and it only goes away when the server restarts right so from that point of view
we might just want to go to the authentication UI uh and then persistence later okay and so we have to figure out what
want what is this grouping here okay load sorry you had a question I was thinking about trying to um how how do you want
to authenticate do you want to use um username password do you want to use social like Google login what do you what do
you want to use I um imagine something like Google login um but because it seems like the more we Implement I mean I'd
rather not reinvent it right so yeah I wasn't well I was so wasn't going to suggest that we're going to invent
authentication I just want to know what are you okay with the Google login versus um us username password where somebody
else manages username password oh yeah I'm and from that perspective yeah then I'd prefer it not be necessarily Google
just username password yeah because there's there's a um there's a bunch of thirdparty services that will do that for
you okay that at our free yeah because not everybody has Google and I'm fine with that I mean we could all you know one
of the nice things is you can let you you're basically delegating all all authentication to them and then you could you
could through them if they want use Google that would be an option so that way you leave it up up to the user how they
want to authenticate that works for me okay so basically next time which will be tomorrow we will um add authentication
and then uh and then we can build the UI yeah so we'll do that Under the Skin at first and then build the UI the
authentication part uh well or will it or do they need to be well the Authentication a layer on top of of the UI so once
we configure that the UI will all you UI Pages we'll say we we'll be able to specify which ones are open and which ones
are require authentication got it okay sounds like I'll be learning about that tomorrow yes maybe I can find some time
and do a little reading up on it beforehand and are we already yeah we're almost at the end of yeah we're pretty much at
time um yeah so that's our our next step yeah uh so we'll add the authentication um we'll delegate the authentication
get that to work uh and then then we can add our bulk import page and that'll be protected for admin so we'll um we'll
actually belonging to one Ro all which is admin and then it's basically because what you can say is you can say like the
search pages are permit all basically allow anybody even unauthenticated people to access it but that the import page
will be protected that you must be role cool all right I did have one comment on endofunctor last uh chat uhuh um the
whole you know using story numbers as a conversation um I've had teams where you weren't allowed to do that where there
was like a working agreement in the team was you had to use the title which then encourages your titles to be short and
we used to strive for five words or less yeah for every title because then you're actually having a human conversation
right versus what's us 5344 I gotta go look that up right right whereas if you just have a five-word title you know
five-word or less you can be like oh I know what you're talking about I don't need to go look at a system right right we
can just yeah on that positive note on that human note yeah there you go all right so that's all for today folks thanks
for thanks for hanging out thanks for joining us um we will be streaming same time tomorrow um so tune in then and uh
tell your friends don't forget to join the Discord if you're not already a member because we've got our weekly book club
coming up don't miss out yeah it'll be fun and uh that's it we'll see you next everyone
