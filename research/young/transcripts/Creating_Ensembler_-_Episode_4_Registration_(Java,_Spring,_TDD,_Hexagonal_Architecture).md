# Creating Ensembler - Episode 4： ＂Registration＂ (Java, Spring, TDD, Hexagonal Architecture)

**Video URL:** https://www.youtube.com/watch?v=2ESC6MEw3ic

---

## Transcript

hello everyone uh but I did want to try and see if I can get this application that I'm working on uh just enough so that
I can start using it uh so I do a weekly I have a um weekly mob mob programming group that I run for people who've taken
my classes which I'll be at some point opening up to more than just the people who've taken my uh my classes but right
now it's quite enough to keep me busy um and so managing that uh is it's a lot it's a lot of just annoying little things
um so I have to check like uh have I filled the class who signed up I have to send them zoom zoom links um and then
afterwards I basically uh want to send them links to the recording uh I need to figure out if they've already if they've
been a part of the group before then there's no no additional setup that you need to do unless we're switching to a
different uh code repository that we're going to work on uh so all that kind of stuff um is a bit of just half a dozen
little details and it's just annoying uh and so why not create a little app that that sets the stuff up so that's the
app that uh we'll be all right um so one of the things I did offline because uh it's one of those I'm worried about
doxing myself as well as worried about revealing secret keys and things like that um so one of the requirements for this
application is like any application um you're gonna have to uh log in and I was thinking well what am I going to use for
logging for login authentication and I realized well everybody who is part of a mob needs to have a GitHub account
because uh that's how we we use a tool called mob sh um and that tool uh is um for basically doing Handover in remote
mobs uh and it uses basically git and GitHub so it pushes stuff you sort of the stuff people are working on into a
branch and then pushes that to GitHub and then the next person then whose paternity is basically does a pull down in mob
sh sort of wraps that in a nice thing hey forests off yes well thanks appreciate that yeah it's nice to be streaming a
little bit a little bit more I'm trying to get into a um so mob sh uh since it relies on git and GitHub uh although I
guess you could use it with gitlab but I use GitHub um since I'm gonna require people to have uh access to GitHub um I'm
gonna use GitHub oauth oauth 2 uh to authenticate people so sort of kill tubers with one stone because eventually I'll
be I want to automatically people who sign up for a mod programming session I want to automatically make sure they're
linked up and have access to uh be able to push to the repository that we'll work on um but right now again I'm like
trying to do what is the minimal I can Implement that gets me something that starts uh being useful to me so anyway so I
did the oauth stuff uh in the application uh offline yesterday and I love how easy it is uh I remember the days when
this stuff was non-trivial but now um all that I have to do in order to uh allow uh people to log in through oauth is
basically add this dependency the spring boot starter oauth 2 client once you've got that then it's a matter of just
doing some configuration so um I've got my uh client ID and client secret that the oauth2 needs um and I had to figure
out where to put uh my uh client ID and client secret so um that used to be uh and I forget which version it changed was
it 2.2 or 2.3 so it used to be that it would read a file called dot spring boot application devtools application
Properties or something like that in your home directory uh they move that so now it has to be in a DOT config spring
boot directory so finally figured out where that goes and uh that way when I'm running locally on my machine I don't
have to accidentally uh or I won't accidentally or much less likely accidentally reveal my client ID and client secret
stuff um because now that's in a file that is not part of the project uh so it won't get accidentally committed um but
then when I deploy this on something like Heroku I can go in and set the the environment variables directly there so
basically the client ID and client secret or are kept are kept secret um so once I set that up then uh that's pretty
much it like everything else is just handled by the spring boot uh Spring Security libraries uh which is really nice so
um what I've been just playing around with otherwise is just making sure the application uh uh works so I'm already
logged into um GitHub so it already basically knows who yeah so environment variables are used when I deploy onto
something like Heroku I can set those uh but the nice thing about having the the spring boot Dev tools um file is like
it's it's much easier for me for me to manage so so that combinations worked worked really well yeah everybody always
falls back to environment variables yep yeah and and secrets getting like I worked when I was working at Apple um we
were working on a next-gen cloud platform which was not using kubernetes at the time uh I was using a homegrown thing
and basically how we injected Secrets was we injected injected into environment variables because yeah everybody's reads
those uh so let me close this tab hold on I want to make sure that I pulled I when I was testing this out I had a
display like uh information that I got from GitHub um which included my email address um I don't want to even though my
email address isn't terribly private I don't want to docs myself so hold on a second let me check something okay uh so
this is the uh I it's it's not been too bad I don't think I've I mean at worst I could always rotate the the client
secret it's not the end of the world my email address I'm not terribly concerned about either yeah there's all sorts of
sorts of great secret stuff using Vault or kubernetes Secrets or kubernetes can use Vault and and all sorts of stuff um
I generally deploy onto Heroku because I don't want to deal with all that crap and so it's just easy yeah exactly
exactly for ourselves not not terribly easy I mean honestly my I've had this email at you know email what 15 years I get
a tremendous amount of spam so a little bit more spam is all right so what I'm displaying uh here is just more sort of
some debugging information I'm I'm planning on doing some music this weekend assuming I'm not too put um so what this is
showing is uh so this 3382660 comes from GitHub um I believe it's an identifier that would not change whereas for
example the username uh you could change in fact one of these days I will swap it with Ted am young but whatever um and
these principal authorities come from the security stuff so I'm just a user uh and and not not much there foreign yeah
so like it it was other than just making sure I had the the all the things I needed it was basically add the
dependencies of the Palm file set it set up on GitHub that um this is this app mob org is is registered and everything
else just worked uh so what it looks like if you sort of logging for the first time let's open a uh basically it takes
you to GitHub to to sign in I'm not going to sign in because that'll be annoying and require me to go get my phone for
second Factor authentication but basically that's what that's what it does and then eventually it'll redirect um I guess
I could log log out so I can uh by default log out is an endpoint that is provided by Spring Security so I can go there
and I and and I can and then basically I can log back in um that redirection I have to fix uh uh because I don't have a
formal login page but now I'm back logged in because I'm still logged into GitHub the logout doesn't quite do what you
think it might do uh so but honestly this is that's this is fine for this application this this is totally fine um why
am I zoomed in though that's better so this is what the application looks like when when there when it's empty and so
this is tracking my uh the mob programming sessions what I'm calling huddles uh that I lead on a weekly basis so call
this one mob number five which at 9 00 am so if I schedule it now it appears in the schedule and then I can click
through to it and see the the detail that current size is just a lie uh but yeah so the reason why I used the word
huddle um is because the word session was was the other possibility create a mob programming session uh and session is
such an overloaded term um in so many ways that I wanted to find another term uh and the grumpy Game Dev suggested
huddle it's like Oh I like that so huddle is like once you know what it means there's no confusion as to as to what
you're talking about and so in the code I've basically shifted all all things over to use the term huddle uh and in fact
um I've started to create a little ubiquitous language uh here program teacher teaches German words well that that's a
that's a good way to go um so huddle uh schedule we don't we don't say create an event we say schedule an event uh and
the stuff I need to figure out is this which is user versus participant so now that I've got the login stuff and
authentication now I can sort of focus on on thinking about that oh and by the way in case you're interested uh so this
project is is open source uh as well as you can use a flu bits so you can actually look at the code while I'm editing it
uh live here on the Stream yeah there's German is is a is probably a great language for that excuse me all right so
where we are is um that's where we are probably need to provide a link back to the to the dashboard but that's fine so
huddles exist they get identifiers they have some attributes uh I can schedule new ones uh so one of the things I was
thinking of is sort of again sort of this idea of I want to get to you know what what they off off kids call these days
and you know uh MVP right minimal viable product and so I thought well I could sidestep having to figure out how to
handle users that are not me um by allowing me to just add participants manually so I thought I um so these are sort of
participant uh stories features I hate using the word stories when these so um and I so I need to figure out the
language for this um so I think I'm reserving I'm going to reserve the word user for a logged in authenticated user
mainly because that's what I get from Spring so if we look at why the heck is this um so what I get is I basically get
the authentication principle which is a no auth2 user and um since that's a user that's what I'm going to use as a user
so I've been using the word participant to refer to someone who uh uh is participating so let's go update our ubiquitous
um and so where it gets a little is someone um some random person off the street uh Regis basically logging into the
system using their GitHub uh credentials um do I do I refer to someone who has logged it authenticated with the system
right so I have a user for them um but has not registered uh for any particular mob so they've never participated in a
mob I think I'm just going to treat them as a participant participant who's never participated I don't I don't know yet
if I need somebody if I need sort of some term referencing a non-participant so registered in some data and it's the
registration so yeah but it is different from user yes um because mainly from an object point of view and a naming point
of view I need to have some other name than user because I'm not going to be storing users in the database that can be
storing participants participants belong to huddles well actually I don't belong to they're they there's a one-to-many
relationship between particip one to many which could be zero um and now I feel like I should be drawing this yeah
language is really important the whole idea of ubiquitous language comes from domain-driven design um and if you're
going to have any anything especially especially this kind of stuff because so many terms are are so overloaded and
unless you're really clear about what do we mean by this term in the context that we're working in uh people can come in
with their own assumptions that may lead people to write code that's not great that make certain assumptions that are
simply wrong so let's see if my visualization tool works yeah exactly for us off it's it's once I mean heck even for
sometimes you know small projects what do you mean by by rule what do you mean by user what do you mean by session right
all right um so um so a participant is one two uh zero or or many huddles um one of the things that participants there's
probably something around uh uh yeah so the user is is is the oauth user I'm gonna I'm gonna continue to use the word uh
user because that's the name of the object that I that I'm dealing with um I can always change it later the I don't at
this point need to get sidetracked by me as the admin um so I'm the admin or mob manager I have some relationship to the
principal because everything the way you log into the system is through principle uh but I'll deal with that later I
don't need to I don't need to figure that out right now because again right now I am focused on uh uh just getting
people getting using their yeah I already have their Okay so uh holes not a manager all right so let's go take a look at
huddle for a second let's see what we got there um so we got uh the name of the Huddle which has turned out to be
somewhat confusing um but I'll worry about that later right now it's just a label for what which mob it is um the the
date and time is much more important because only one of those can occur at any time um so I think what I wanted what I
then want to do next is add participants do I have a participant yet uh no I do not so I currently have ways of of
creating uh huddles I have an in-memory huddle repository that I'm gonna pretty soon want to turn into a real thing to
sort um the Huddle ID is currently not final because uh the ID is assigned from the database um I I tend towards having
the database assign IDs even though I know that uh there's reasons and good reasons to do it where you basically create
an ID before you create the object um but there you go and this is primitive Obsession eventually this will be something
else but for now it's an INT although I guess I could put in now the Huddle ID is a value object so yeah what I want to
be able to do from the UI is when I am looking at a huddle uh I want to be able to well display the participants so I
want this stuff to be real and not fake so let's do that so from a test standpoint what I want this page to do is to
show participants let's do commit which was uh added Spring Security and uh uh to support for uh authenticating by uh
GitHub okay so now so this is a huddle service schedule test pedal service fine test uh so we want um huddle uh huddle
participants participants uh so let's go make a live template for that create uh Imports so that's what I want um all
right it was one of those anyway okay um so the test I want to write is um I guess I can use zombies here so uh zombies
is the zero one mini uh boundary interface uh exceptions acronym is it an acronym yeah it's an acronym because we
pronounce it uh and so this one is basically when a huddle do I need to test this through the service what is the
service the service is just going to uh uh eventually I'll need a factory for huddles I'll have to think about what the
um what the aggregate is here that'll be interesting all right because it's a one-to-many mapping but the mapping is
sort of reversed is the Huddle so okay so uh huddle new um that I like how it took the name from from the from the name
but I'm just gonna call it huddle well we can say two things one is number uh I think that's really participant count or
participant number number of participants that uh that is zero um and puddle participants uh this will return right now
I'll just return a list of participant and that should be empty all right so this will fail because uh this will return
zero but this will return um a null and that will fail so let's run our tests and it fails as expected so we'll go fix
that we'll just return empty list for now so now um puddle as I'm always having trouble spelling this word because it's
got that icip which is just throwing me uh huddles one something like that huddle and uh we'll need to create a
participant no I probably should refactor this uh GitHub username now record uh false I should I'll probably need to um
uh dedicated class to make it easier to so huddle register I'm having one of those moments where you know you think
about a word a lot focus on it and now it just seems wrong that's where I am the only other term I can think of is sign
up but I think register is sufficient let's go ahead and we'll create that uh that's going to be a void so it's not uh
and now what we can assert is that um number registered is one and huddle participants uh is contains only participant
um us to implement an equals method on participant currently participant is a record so this fault equals is created uh
I have a feeling I'm gonna be switching away from records oh wait a second this is oh crap I've goofed is a participant
View wait is this even in the right package who's using this uh so let's do this uh and now we've got five problems um
so we'll need to create a class because now huddle doesn't work all right so let's go create this this goes in the
domain and this will be a full-fledged class uh um foreign why are you putting it in test I don't okay um so uh GitHub
username email this chord username um yeah because I I'm I'm I'm on the bleeding edge on on this app I'm using Java 16
and and 2.5.0 release candidate foreign uh mom organization um yeah mainly because I'm using records um so yeah okay
what's going on here I don't need that uh this foreign okay good so that's failing uh so let's go to number registered
this should no longer track it this way uh uh actually leave it that way for a second participants add participant
create that field it's hilarious sometimes what what IntelliJ suggests why did it suggest that all right and so then
this is participants uh size so now the test will fail because we're not returning uh the list of participants and it
does um oh right and I was going to go to participant because I need to implement uh uh and eventually these will not be
strings anymore uh and they won't all be final but for now that's fine an equals based on GitHub user name sure that's
that'll that'll definitely be unique um but I shouldn't use that as an ID eventually I'll need an ID on participant but
for now this will do fine so let's create an equals is that that um and yes it will not be no okay all right so this
test will still fail because participants isn't including anything a copy of participants I don't feel the need to add a
mini test if I add one uh there's probably some tests where I can't add multiple uh but I think I've got a um to do for
that so let's go that make sure I have that foreign so I'll need a test for this precondition um I guess I could that
feels like a little bit of bike shedding so I'll skip that all right let's do a commit uh added domain participant and
renamed view to view of it to participant foreign ers silly meetings what issues have you found nitpicky yeah okay fine
I don't really care I know they're unused um all right so uh we can now uh add participants to a huddle um so now I'd
like to display them uh first off if you just run uh the mob uh that assuming uh all your tests pass that should just
work I was just thinking would the security be a problem no as long as you authenticate with because right now I have
the application is defined that it returns to localhost uh so we're localhost is Wherever You Are all right so we got
this we've got participants um I'm gonna turn off Tailwind just because I'm not I don't wanna Tailwind uh when you use
Tailwind like I'm using it here it basically does a let me turn off basically all of the default uh all the defaults you
get because it assumes you're going to add those all back so I lose anything around H3 versus H1 and all that kind of
stuff so uh what I want to add here is I want to add the participants tomorrow I want to write for a test for that so
this is from the Huddle detail view so let's go to dashboard right so uh huddle detail oh I was gonna look at the Huddle
detail page just to see what I can just preview it yeah so that's it in all its ugliness so um let's all right because I
turned out the Tailwind that's what I wanted to see okay great so what I want here uh for the list of participants name
GitHub username that's it maybe so we want a list of participants how do we want to display that you just want to
iterate through and display it as a bunch of paragraphs that's fine for now so I want to iterate through participants so
I basically just want a list of participants all right let's play as it oops I know how to do radio buttons one of my
many back burner projects uh is basically creating a Time Leaf cookbook for exactly the situation I'm in right now it's
like how the heck do I Loop through a list to display something again because unless you're doing it like all the time
um you forget right we forget because we don't access the information and when you access it then you remember it for a
while but then you forget it again so it is a I just started my first job I'm feeling terrible terribly overwhelmed you
know even for someone like me who's been doing this for a long time whenever you're in a new especially a new job you're
having to you're exposed to so much and you're having to learn so much it can it can definitely feel overwhelming um uh
so hang yeah hang in there it it will get better um you'll still have the feelings of try not to stress too much about
it because you're there's just no way to absorb it all at once so this dude so one of the things I look at when I'm
looking at documentation for spring and spring Boot and things like that is I try to as much as possible go to the
spring i o right the primary source their guides though sometimes are like a little bit off Target and this is something
I hope that I will eventually do differently once I get to my spring courses my course is on Spring not my spring
courses uh is sort of different sort of Plug and Play kind of thing so one of the examples they use I I went to this
when I was trying to figure out the GitHub oauth is that using like jQuery and JavaScript on the front end I'm like why
are you confusing things with that like I get it um but like it it adds confusion and adds more complexity than just
like how do I use this with just sort of straightforward front end um participants and it's like this I don't know why I
can't remember that so this will create a div for participant name and this is going to be participants if I say name
and GitHub username GitHub username that looks right let's go fix it uh this is this test is going too large so let's uh
let's split out the detail view because I'm probably going to split the controller too so let's move the detail view
detail View yeah let's move the detail View to a new test see I I really wish intelligent and I keep me into following
issue I wish I told you I had a way to like say these are test methods they're fairly independent if not completely
independent from the class they're contained in can I just move this because I have to make it static move it you know
can I do this five refactoring not a cut and paste that's what I would like because I do this a lot all right so let's
create a new um uh huddle and uh wise name okay uh so let's run all oh why do those fail 403 right I should have run
those tests earlier uh those are going to require a mock user um Chris I forget how to do it foreign oh and this can go
on the test class well that's what I thought do I not get that as part of I wonder if I just haven't pulled in the whole
Spring Security because I only pulled in the oauth so I wonder if I need to pull that in separately all right hold on
was that a was that an uh for something you're dealing with lexlers or uh in oh sympathy yeah so I think this will bring
in the tests stuff that's interesting that's I that I that this I guess it has a dependency on security spring security
test I'll have to clean that up all right so now let's see if these um yeah there's probably something special all right
so put the security stuff aside from from uh the integration test point of view um we'll go ahead and uh go back to our
I'm gonna stick and ignore ignore disable disabled uh figure out password to based security Authentication okay now the
mock MVC is is auto is already Auto configured through the webmbc test there's something else uh that I need to do and
I'm not gonna waste time on it because it's not right now it's not important all right so other than those everything
else passes which is fine um okay so what we want to do uh was display all the participants so we have the uh uh Dash
puddle detail right so I want to do is we want to put participants into the model um so let's go to our dashboard huddle
view test um so I've got huddle what we also want to uh is or should that just be in the Huddle make sure that should
just be in the Huddle detail view itself so be huddle participants yeah that's what we want okay so from a huddle uh we
need to create a uh um let's just do list of participant View oh yeah it's totally tempting to just hey let me just put
all the code in the controller why not um and that's where the refactoring really has to be a an ingrained habit uh
otherwise you will leave it at sort of the wherever it's convenient yeah uh go ahead and create a not a field increase
local variable topic that's interesting so it's either saying create a field I don't want to create a field I want to
create a local variable why is it not giving me that option now introduce local variable will be for the whole return
but that's not what I want I had to force it and I still don't get quite what I want uh so I want is huddle participants
map stream map and what I want to map it to is uh uh from us it should have known that it's why wouldn't it figure that
out it's a list of participant views why wouldn't it figured foreign participants oh it might not have known the return
value from that all right but then we just want to do it uh when was this added was this added in 16 yes was that in 16.
okay Echo strike so I was just reading how much is relevant to me and how much is Just y'all conversing uh if you're
doing tdd you need to add a method to a service would I mock the call to the repository or could you just call the
service method and put the mock in during the refactoring step you're going to need to add a method to a service would I
mock uh so this method to the services I'm assuming uses the Repository I mean it depends on the method that I'm adding
I mean I tend not to use um I tend to use fakes for my repositories so I basically create a uh like a fake or an
in-memory Repository add the item directly to that uh and then that's referenced in the in the test yeah so I'm always
almost always passing in some kind of fake or similar into my services when the service gets created so in fact it's not
the view test uh where's my service test so for example um I've got my in-memory version of the repository uh and the
service takes a reference to that in memory version I added an item directly into the repository and then I test my
service method which uses my in-memory version of the Repository so here I could stub the repository or I could provide
a fake but I already need an in-memory version because uh I want to be able to use and interact with the application um
so I don't and I don't want to involve a database just yet because I'm still trying to figure things out so I tend this
is what I tend to do is create an in-memory version that's actually kind of production it's in the production code side
not not on the test side if I already had a real database and hooked up then in here I'd be replacing the in-memory
version with a fake um because it's really easy to work with all right so we've mapped our participants to participant
views we put that in here that's all in there uh and then here uh we assert that that and we can also assert that the
huddle participant views um in this case it should have none I would want a separate test the tests to see that it has
yeah actually this isn't the wrong test I need a new test okay uh detail view uh existing huddle with one participant uh
returns Theory this test name is too long but yeah I need both of those all right I can't refactor that I probably have
to move to a builder pattern but I'm not ready to do that just yet and on the Huddle we'll register a new participant
this is a bit annoying uh GitHub the uh okay is a plan to deprecate in-memory huddle repository eventually um probably
or certainly it would not be the the default one at startup but I might choose to use that one if I'm if I'm doing some
sort of more work where I don't want to get the database involved I'm not worried about drifting because both the in
memory and the real one will still have to implement the uh huddle Repository uh interface and so I'm not I'm not
concerned about that uh student I had an interesting discussion today with a colleague uh using a fake versus a stub
when testing the service that calls the repo one of the points phrase when we need the natural behavior the repo
shouldn't we just move on to integration testing um it depends on what you're testing yeah if you're testing database
interactions then you wouldn't be testing the service you'd be testing the repository information implementation
directly you can't just provide us stub because usually what I'm testing requires something that uh has read write
capability so that's the difference between a fake and a stub a stub you only read from the code the the code under test
only reads from it uh with a fake it can write to it and read from it and so repository needs to implement that full
interface I generally so like in this test I'm sort of treating the in-memory repository in a very stub-like fashion
because I'm pre-populating it with with something um so I prefer to to do it that way so that the code that uses it uses
it in the in the normal fashion if there is anything deeper I probably would be writing a test against the service uh
what is it called when you don't actually run the save but you just verify the correct stuff is passed through save that
would be um that would be a spy so spy looks at the methods that are called and what parameters are sent which I
generally do not do I don't I don't like behavioral tests like that uh okay so we've got our huddle we've registered a
participant we've saved it on the Huddle detail View and I might be convinced that I could merge this with the prior
test uh uh I don't need the save title I just and now I can just assert at the Huddle View participant views I don't
feel like I need to do much else than that I I tend to use test doubles that are basically mocks written by hand yeah so
I don't use the word mock except in a very very specific case uh which is something that can self-verify the things that
a spy might verify so what methods were called and what parameters otherwise I use generically test doubles um and then
if I'm going to use a test double it's one of the three types that I talked about in my class um a dummy which is not
the case a stub which only returns information and a fake which can store and return information so in this case this uh
huddle repository is serving as a fake and then these are just actually real objects um and so I'm using a a fake
repository to store the information that gets returned through the through the controller uh and so test double may be
as simple as a stub where it just returns a hard-coded value and you program it that way or it might be somewhat more
sophisticated as in a fake all right so let's see if this test passes I think it uh I think I shouldn't be thinking I
should be knowing so here when we create the Huddle detail View uh we do convert it um let's not do that and now then
this test should fail got that test this test right because we weren't adding it so we expected one but was Zero so now
we can go ahead and um uh okay so let's go back no not there to The View and let's undo this so now that test should
work and it does okay so now we are loading uh participant views um in our huddle detail uh we're no longer getting it
from participants right we're now getting it from huddle and it's and the participant View foreign but I didn't have a
test for this I should have had a test for this all right IntelliJ doesn't recognize records as used in inside a Time
Leaf yeah stubs are stubs are fine if if the code under test doesn't have to write to it um and you just want to control
what it returns so like stacking the deck in in a card game uh so new participant View do I need to write a test for
this this is almost direct translation uh oh participant doesn't have any uh uh has a name so public and eventually some
of these will become uh types instead of Primitives but for now uh this Discord username I'm not even sure so I'll leave
it for now just code username and okay foreign name email uh Discord okay uh size it seems to be problematic um let's
make that easy so in our huddle okay so I realized that a bunch of the stuff I just wrote was not test driven because
it's pretty much just copying information from one class to another if I was concerned that I wouldn't see that easily
through the UI then I would write a test for it but it's not even manipulating them it's just copying them so I am
comfortable not test driving that because there's no logic to test all right so that all works let's run what do I
expect I still expect the because I don't have any way of registering the participants uh I could register one somewhere
um maybe I should have written the ad or just register a participant first so let's do that let's do that and here all
right so that's good and we don't see any participants so that's good uh need on this page and add purchase a register
participant button but um at the end of my time block I still got a few minutes let's see how much I can get through so
let's do a commit um for a huddle view detail View now shows participants oh yeah I need to figure out uh testing uh
integration testing and I lost to involved and I guess I could put this on a on its own page but it seems kind of
convenient to have it here uh so what we'll need is we'll need to form and the th action will go to where is that going
to go to uh no I think that's fine we'll just put it uh action equals that method is post and th object is uh
registration uh the th is the time lift time Leaf template so I'm using spring boot uh MVC with the time Leaf templating
engine all right so we'll need an object and uh what information do we need for a participant um it's a teenage field uh
and there's an up a member of that so we got name we've got GitHub username and I think everything else I'm just empty
that's interesting that I think name is valid um margin top three type of Schmidt and it's uh so this tells us what we
need from the back end uh and so now in the back end this will need a new endpoint though and so I can write it I can
sort of do middle in I can write it and then worry about the the configuration test so let's do that let's pretend
there's a method uh what I'll do is it will take a registration form and what we expect it to do is uh uh add it in so
what do we need we'll need oh it's going to need the ID of the huddle hidden uh type equals number and the th field uh
huddle ID value is a th value that means I'll need to add that onto the Huddle so this way when they submit the form and
they say register this participant we know which huddle they're registering for I think this is a good stopping place so
but I'll do on my on the next stream uh uh which might be tomorrow I'm not sure I've got a bunch of things I need to do
before next week um but whenever we resume this uh we'll continue uh hopefully I'll have figured out the security test
stuff and then we'll be able to write a test for this endpoint register uh and then we'll be able to add some of this
stuff and make sure that when it's submitted with the right information uh that participant gets both in this case
created new and added to the Huddle um sort of participant management if there's if they already exist and that kind of
stuff that that's going to wait yeah uh so let me yeah let me at least do a commit um added form for uh register
registering a participants with a huddle apparently as soon as a new hey new participant actually it doesn't uh oh good
question um so participant is part of my domain and I do not use Getters and setters I do not use Getters and Setters
for um methods on a domain object there's only one place where I do that and that's for an ID um but anything else uh
the information is owned by the object and uh if you wanna find out that information you do a query and so these look
like Getters um but uh putting get and set in front of it means something very different it means I'm gonna uh access
information that that you're storing and I'm getting back at internal information that's usually what people think about
when they do development in Java uh and I wanna make sure that you're thinking about these names as queries um and not
as uh Getters so Getters and Setters are very invasive whereas queries and commands are much more in not just in the way
I think about it but folks other folks too that you want to think about queries and commands uh you have an object and
if you want information that it has you query it if you want to ask it to do something you you give it a command so it's
a little bit more than just just noise it for me is is very much names are uh names influence how we think about things
and so by not having Getters and Setters it hopefully uh has people think about them differently that's just nice it is
it is a bit of noise yes um mainly Getters and Setters were are a misuse of something that was not meant for humans to
use but as I say that uh that horse has left the barn many many many years ago uh yeah so um yeah kotlin avoid the noise
yeah Getters and Setters were meant to be used by tools so Getters and Setters started with um the Java Bean
specification which came out in 1997 and were meant to be used by uh at that point GUI editing tools um to figure out
what properties were on components that you'd drag and drop onto the onto the the screen uh just to create a UI um at
some point and one of these days I'll do the research and figure out when it happened uh but probably around the
Enterprise Java Bean days people started using Getters and Setters by default in their code um but they were never meant
for us to write they were meant for tools to be able to use the naming patterns of get and set to figure out what
information uh a data only object had so Getters and Setters are still used I have them in in um but uh uh they shouldn'
t be used anywhere else because we should be thinking about what are the commands and queries we want to use against an
object and leave Getters and Setters for things that are just data and have no no Behavior if you do a search for um
Getters and Setters are evil uh you'll find an article written by Alan Holo in 2003 uh where he talks about
