# Trying out FusionAuth (sponsored stream) with Java & Spring Boot

**Video URL:** https://www.youtube.com/watch?v=2VAsQpflZqM

---

## Transcript

foreign hello folks welcome to today's stream uh it's been a while since I've streamed um so I'm hoping to get back on
the streaming wagon as it were today's uh is going to be a bit different from normal stream you've probably seen me do
uh some sponsored streams before so today's another one a company called Fusion off and um while I've sort of looked at
it a little bit um this is me sort of seeing how it works and trying to integrate it with a couple of my applications
and we got uh one of the folks from Fusion off uh developer Advocate uh the infusion office is his name so he's here um
so as I mentioned uh my plan is to to basically take some spring boot apps um as you can probably guess by their name
it's about off uh so let me start by sort of introducing the applications let me switch over to about that one let's go
for this one let's push the right button this time um so this I just realized so laughing because like uh I have renamed
the application I finally after far too long renamed it it used to be called mob reg uh because it's a registration
system for uh basically mod programming sessions that I that I run um but I renamed it if not mentally uh in the code
and elsewhere as ensembler except I almost never see this page because um I'm usually already logged in uh and so
usually I go directly to the URL and and and I'm already logged in um so it's rare that I actually see my own home page
uh so I should probably fix that um right now the application let's say Loosely integrated with with GitHub I decided to
when I designed the application to use GitHub as my auth because I didn't at the time really need anything General so
you can either sign in with GitHub or register with GitHub and this uses um basically oauth uh to to do the the login
work so one thing that I continually say if you've ever watched me on the stream like I see so many application
tutorials for spring Boot and security and like they're starting off with let me you know use the in-memory version of
the authentication I'm like why bother like just just go directly to use somebody else uh for for authentication you
know whether it's a GitHub you know uh or or Google or Twitter um or something like uh the ones you might already be
familiar with um or Fusion off like don't don't do authens by yourself like I I I I still see that and like I guess it's
useful there's there's aspects that are useful to learn right so there's the stuff where you're basically um you're
doing the security config which by the way uh sort of a separate note the web security configure adapter right what a
name right um has actually been deprecated in recent releases of spring boot uh ensembler is still on 268. uh I
eventually need to upgrade it to two seven what do we got two seven three um so they deprecated this because uh it's
really annoying to have to do these ands to connect sort of different pieces together um so they they basically made it
more sort of componentized and from what I've seen there's a video from Dan Vega that he just he just put up on YouTube
that that goes through this uh and it's it's you know not much um yeah what version am I on uh what's my palm saying I
think I'm on two six eight yeah so I need to get off 268 pretty not like it's urgent but I like to keep stuff generally
up to date you can tell how long it's been since I've worked on this on stream um it's it's been a while uh one thing
against sort of side note since we're going to be talking about security uh use MVC matchers if you're using spring MVC
use MBC matchers actually um uh wrote Dan a comment on on his video saying shouldn't you be using NBC matchers because
he was using Ant matchers and the reason why is if you're using spring MVC um you want sort of the matching logic like
how does it match against for example invite an MVC matcher could match against slash invite or slash invite slash or
slash invite.html that will all go to the same place ant matches don't do that so in fact there's a cve out that
basically says use NPC matchers uh so again like I see a lot of tutorials that basically cop like I'm not going to go on
a rant about tutorials but there's there's sort of this um everybody copying each other and not really thinking about
what they're doing um in terms of what's the most modern um yeah it's is it slash invite star star um well there's the
slash user slash starts R which is basically anything that's underneath that um right so it's a path wild card um I
guess that you could think of it that way I probably wouldn't if I was going to do that I'd use a single star because
the double star indicates uh uh um a path right hierarchy uh wildcard as opposed to a string Wild Card although that's
probably not true either because if you had invites plural that probably wouldn't match so um but anyway so when I first
set this up I set up um the oauth2 login to basically delegate all of all the login stuff to to GitHub and I currently
have an invite system which I need to at some point need to upgrade um because right now it's not at all like this
application is tdd hexagonal and the invite part uh I wrote really quickly directly to database stuff and I need to sort
of um rewrite it but it's one of those like well it works so you know hasn't been urgent uh so the invite system one of
the things it does is basically I can link uh when somebody wants to sign up for The Ensemble which I'll show in a
second uh they um I I need to start somewhere so one of the things I I don't have is a system where somebody who just
has a GitHub username can can just authenticate uh and and become a member you can actually authenticate so you can
basically say sign in with GitHub and if you sign in with one that is not recognized by the system then you won't see
very much so this application has has basically I guess you'd say three levels of authorization right so authentication
is who are you and and are you who you say you are an authorization is okay now that I know who you are what can you do
uh so the three levels of of authorization are you log in through GitHub but I never heard from you I don't know who you
are so you're just a plain old user and you pretty much have access to nothing um you're a member which means I've added
you to the system explicitly which means you can join uh one of the ensembles and then there's me the admin uh so let me
actually go to uh so this is the admin screen so I get to see both admin views and and member views up here I'm going to
add a few ensembles just just so we can see what what the app is all about we'll skip the zoom link um so uh so what it
did besides just you know writing some records to a database that actually went out and fetched information um uh well
it actually initiated creation of a zoo meeting from from zoom using their using their API and that's something else I
need to fix talk about auth like they've deprecated using uh certain kinds of apps that use jwts um I know people
pronounce those jots but that doesn't work for me um and so uh so it goes and I have to decide to fix that because now
now they want you to be a server to server oauth and I swear like my head spins with with all this stuff just because I
don't I don't I don't do it all the time um so fetch basically requests a meeting to be created and one gets created uh
and then uh it creates creates the event so from the members standpoint what they see is just hey there's an event and
they can either accept or decline so if I accept then I would see the zoom and otherwise I can add it to my calendar so
the zoom link was automatically created I can also decline if I decide you know I can't go uh so diffusion says RFC 759
7519 uh the suggested pronunciation of David G is as what English word that would be jute and then there's the the um uh
James Webb Space Telescope and so every time I see those four letters the jwst I'm I'm always thinking of of wait what
yeah yeah I know that's not what they say I don't I don't pronounce it shot all right um so that's basically what the
application does this is from the members standpoint so if I'm I'm a member okay yeah uh copy paste and chat is
sometimes hard uh and from an admin I have different permissions so you can see that the URL all right so everything
under admin I need to have admin roles and so the way I have this structure then of course is all this stuff um and I
wish I could hide some of these inlay hints because like I don't need these enlightants sometimes you want them but
sometimes I'm like I really don't care about some of these anyway uh so you can see here that um there's uh permit all
four slash and for error roll user for the user one and to access the invite anything under admin needs roll admin um
and uh if you want to see member uh the member stuff which is basically uh this page this is under member uh you can
also edit your profile that's also under member so you have access to to that but you'll notice that there is a user and
this is what you see if you've been authenticated like okay GitHub says this is who you are but I don't know my system
doesn't know who you are you basically see this uh uh and right as you can see it's a placeholder for onboarding that I
just I haven't had the need to implement yet so but there are those those levels the other thing is um those who've
authenticated if they did get an invite they would go to a link that is invite and it has a token that gets generated uh
and then I know who they are uh I know that they've gotten it and then they can then it basically upgrades them to um
roll member so I'm storing this in uh basically this information in a database so uh let's go look at our database let's
let's refresh oh the other thing I need to do is you may have heard Heroku is stopping their uh free plan um I have a
couple of projects that I pay for uh but ensembler actually gets used like a total of maybe an hour a week at most so I
haven't use their pay plan but I'm probably going to have to either decide to upgrade or more likely move to something
like Railway so if we look at um a database see a bunch of tables yeah and I totally understand why they would do that
um I mean I would you know I I it's always interesting to see companies new companies and old companies when they offer
something where there's a potential for some kind of compute right the obvious ones are something like a Heroku but then
you have something like replit which allows you to run applications in a sandbox then you have things like build systems
which clearly have to run code in order to build your thing and any of those people are just going to abuse and
Salesforce yeah they I would totally understand they don't want to really compete in that market it's too bad but um it
is what it is so uh the the information basically I store the the roles for each uh yeah it's all it's all um and I
guess spam and fishing and and stuff like that um so what it does is uh when I authenticate right it goes and goes to
GitHub um we didn't see a login page because I'm already logged in the browser so that information is saved so basically
I goes to ask GitHub who is this person who's accessing the system it returns Ted Young because that's my GitHub
username and that goes to the database and says well what roles do they have and loads loads that information in uh this
is actually uh in the code we look at member dbo which is the database object it's actually a set of strings but I
happen to store it as a single uh column because it's just a set of strings comma separated why not why I have Separate
Tables so that's how it figures out all right so that was a very long Preamble uh to what the application does what it
needs from both authentication and authorization uh and so let's take a look so um Fusion off is apparently so there's
another acronym see I like like there's so there's so many and in any sort of new area there's always a lot of acronyms
um ciam is is not one I had heard of uh I'd heard of like identity providers but I had not heard of uh This Acronym so
um and so it has the typical things uh that you'd need from from any kind of auth system um so users that's what I'm
interested in applications that's going to be uh yeah it's not a TLA it's an F or letters uh so I'll probably need um to
to Define application um fusionoff has provided me with with a cloud-based one you just like uh something like key cloak
you can basically go in and download it and run it on your own um so they've got a bunch of different ways to download
that uh it's really nice to see sort of um I'm a Homebrew fan but I'm also a Dodger fan because I don't like to install
stuff I don't have to uh and so the the docker setup is is nice it's got a Docker compose set up um and that takes care
of uh everything you need with the fusion off itself in the database and I guess elastic searches for searching stuff I
don't know I haven't actually looked at that um but I'm going to be using the the cloud-based one just so I didn't set
it up um where to start I guess is what we want to do so what I'd like to do yeah for searching for users so what I'd
like to do and before I forget because I've done this before uh I'm going to go and create a branch let me just make
sure I'm all pushed yeah okay I'm going to create a branch for this um all right I won't worry about that uh well no I
don't want that so we'll all right good so now I'm going to Branch so now I can sort of screw up all I I'll I'll uh I
want to and and I won't affect my actual production app um so I'm already uh in terms of let's see where'd it go there
it is in terms of the fusion off itself it's already here um in terms of uh set up the admin um so I'll have to go
through some setup here uh so let's see um oh I think it's that's already set up for me that's already set up for me
that's already set up for me so let's create an application and configure the settings let's go do that uh let's set up
an application and this is this is pretty typical for yeah so luckily uh Dan set up my dashboard for me so I didn't go
through a bunch of other steps so here is the the application and this so then there's uh I'm going to move these
windows around um yeah I'll just use the 10 theme so let's see so rolls uh so let's add our rolls so we've got um admin
um that is not the default um assuming that that's my super roll I guess I could go right to the to the oauth but we'll
add we'll add this role I'm not sure what super roll is just yet um so we want uh I use the word I use the name user um
for non for basically people who are authenticated but have no other powers so we'll just add that uh and then we'll
have uh member all right so let's go to bowass and I'll have to regenerate the client secret I guess it doesn't really
matter user is a default role okay what happens if you don't have a default role what does it do uh let's see this so
client ID client secret I'll regenerate that um refresh tokens debug enabled so one thing I remember about um uh hooking
up oauth to Applications some providers do this and some don't wear um like I want to test this locally so my redirect
URLs are going to have uh and some don't allow multiple um URLs I forget who doesn't I think GitHub doesn't and that's
really annoying because then you have to set up two completely separate applications that are basically the same thing
just now yes that's a good question if if you get assigned member do do you get used anything else with it or do you
just it's if you if you don't like I would assume that if you got member you wouldn't automatically get this this just
means it's the uh uh so let's see what um what's our redirect URL gonna be that's a good question uh because I'm going
to rely on um I'm gonna rely on uh spring to to do that for me just looking at Fusion so it's just relying on the
standard oauth 2. pulling in the fusion auth Java client and yeah so we we basically want to specify um we're gonna
pretty much do this to configure the open uh uh the open ID or basically the oauth uh those well I guess we'll find out
how how old it is um well I should be able to transfer translate this so we're going to have a um oh so this is actually
going to be the call out so right so we want the redirect URL to be whatever we want which is going to be um we're fine
with all Origins log out um so our log out is pretty much going to be the same thing okay I guess that one of course
wait so I have to say I have a um dislike for uis that do auto save um there's another product that I use where uh you
change fields and sometimes they get saved and there's an occasion where they don't get saved and there's no uh yeah I
think I I think I did go back let's see so enable grants it looks like there's a save button up here so I naturally
expect save buttons to be in the lower right not on the top but whatever um sort of uh reviewing the UI I really dislike
icons or these kinds of things like yeah there's a bunch of things here but these icons especially this one does not
remind me of you um I think the UI would be much better served having uh actual words here instead of instead somewhere
here is my client secret yeah okay so let's go and um what I wonder is how the roles let's let's see if we finish this
okay so we did this that's our authorized and so we'll need well I'll have to configure spring for this we can skip um
foreign so all that stuff is is set up so we can uh so I'm already in there as the admin um and um and I don't think I
oh time zone let's put in time zone just for the heck uh actually there we go because that's who we said it was okay
yeah so right now I'm not using sort of self-service registration and and here we get to select the roles um so I'm
going to make jittertet a member actually let's just make jittertet a user and then we'll upgrade them to uh all right
so we've got um oh so this is just a marker for a super roll and in my case uh I don't treat the roles that way I
basically have separate roles for each one 1.38 that's way above this 1.7 so one thing I recommend to people who are
documenting this kind of thing is unless this is automatically updated don't put in the version because you know what
people are going to do because I do this is they're just going to copy this and they're going to get a version that's
out of date if this is left as sort of placeholder then it's clear that you got to look somewhere else my preference is
auto update but sometimes the documentation tools don't make that easy I like the Click of the link to the search so
that way I can see the latest that's much more helpful than going to to the GitHub and saying uh what's the latest
release because it sometimes they have releases and sometimes they don't and sometimes they're tagged and sometimes
they're not so um but I do recommend also on the GitHub having a one of the tags marked as a release I that way it shows
up here as so again I'm going to assume that um spring is going to handle all this so let's uh we can close that and uh
yes this is I forgot the name of the Chrome extension octo tree that's what it is yeah very handy all right so let's go
back to our example uh so we should just be able to pull in into the palm um yeah this is quite old hopefully it'll so
let's see uh that's the Java client we don't need that uh I have I have a recent version of the spring oauth um I assume
I still need or is it gonna or do or is or is this completely unnecessary because it's just oauth which is what I would
expect so I think I don't even need any of this yeah okay so that um yeah that that uh example needs to to be updated
then that's really it so let's go then and and make sure we configure this correctly um so let's go into our so here's
the um the GitHub a lot stuff and it feel because it's one of the known providers uh Spring Security you sort of already
knows about it so it fills in all the rest of the stuff in terms of URLs we'll have to specify those uh specifically uh
so let's go ahead and do that um I'm gonna throw that down here at the end uh so uh uh whatever I think whatever I want
and then the client ID that's interesting the autocomplete is uses the dash version of it uh so let's check our um uh R2
login uh I wonder if I should convert my other stuff to be the lowercase version all right um so here are the property
mappings this does Fusion off auth provide a because I know I can manually do this but uh there is ability to sort of
Auto configure it um so let's grab when the client ID client Secret redirect URI let's do this this way because I don't
know the other way uh so let's go back to our applications by the way and this is only for for those who stream um but I
notice also a lot of uh uh places that have the secrets are hidden unless you click something or and and or have a way
to copy it to clipboard without having it shown um so that would be I know that's specific but there's a lot of times
people are are sort of showing screens uh and I and it's one of those where it's like I don't actually care what it is
just copy it to my clipboard of course wherever I paste it is I have to be aware of it that's something that uh is is
convenient to have the client secrets a client secret did I copy that uh the um let's go back to the so we want custom
provider properties uh uh ah authorization URI why are these are these not listed up there oh it's the provider ones
right so let's so we want uh this has to start with provide client provider I don't like ammo all right uh and then let'
s change IO so oh it's just all off two so there's so that's introspect that's token user info these are probably all
standard and authorized um I think that's probably something let's go ahead delete that so is that uh that's that's it
so what I'm gonna do oh should I add the the jwk sure oops two colons there yeah definitely having a clipboard I
recently added that to oh to my invite thing because I have to copy and paste a link that I send via email manually of
course because why automate things if you don't need to automate them all right so um let's um and what do we expect to
happen I don't know what's going to happen uh oh into the admin UI itself okay um so oh right we didn't finish that so
let's I guess that's our API key um so it's in the dock somewhere because I didn't remember seeing this what what this
where is where is this in the process because I can just do it I just want to um yeah if you can point to a page that at
least describes what I just did that you're eating waffles did you bring that uh so is that an ID that I need somewhere
okay so if I hadn't because I'm actually not yeah so I actually didn't need that but let's go ahead and save it yeah let
me let's see what happens um because I expect something to go wrong uh because this was a lot of I think this will work
I think this will work so let's go now um the authentication route it's going to go uh uh might not work because it's
specific so let's go into our GitHub Grant authorities mapper um let's turn this off and then that will be fine and then
we want the welcome controller so this might not work either yeah so this um this granted authorities mapper is what
what I what I was using with the GitHub authentication to look at um sort of as the um as the the oauth2 user sort of
comes by I get to do my own my own mapping uh and this is where I sign the attributes it says I'm going to get those
directly from Fusion off then uh Then I then I won't need this so let's ah well because I turned that off the web
security config couldn't find it so ah right well I need to do something here anyway so um uh I forget how to configure
this let me go look um but I don't need the manual um let's just look at their setup for their sample and we'll probably
actually want to turn on in addition some logging levels let's do and let's turn on logging level no button level uh
what do we want we want org spring framework security got the whole thing debug yeah Dr toshizzi uh yeah I was talking
about the the goodbye Heroku free tier yeah I'm moving over to railway um railway.app uh I think they have a tier
without the credit card I know they changed some things recently for a similar reason um because the problem is is they
need some way to check that you're a real person uh and not trying to do fraud and so that's where the credit card comes
in I know fly dot IO um yeah so uh fly is really is really nice um and in fact both fly and Railway um I haven't used it
yet but I'm going to use it they have a a page that you explicitly um basically authenticate Heroku presumably using
oauth uh and they'll basically slurp all of the configuration for an app and then set it up on on that platform yeah
it's not like they're going to charge anything uh it's not gonna they just sort of you need the card for an identifier
um let's see what was I doing oh yeah web I wonder if they changed the so that's the application itself um so what does
the controller look like yeah it's just got foreign all right um okay that's interesting a new template that's just
their template okay there's token endpoint there is no JWT um but these were all defined in I don't think I need to do
anything else that's it I think I just say oh it's your login uh configures authentication support using oauth2 um you
must register a client with a provider client registrations are composed uh the um yeah so I don't actually need
anything because it pulls it all from the um from the setup if I wanted to build it manually I would do all that stuff
but I don't need to do that all right uh Dr for cheesy is is gcp available alternative I don't think gcp is a viable
alternative mainly because I honestly I don't trust Google to keep anything the same ever um plus they're going to be
much more expensive I think Railway fly um as I think render was mentioned if your stuff supports it but I think for
like spring boot stuff um Railway I've used already and it's really straightforward uh I have not deployed anything yet
for for uh for fly all right let's run the application see oh right I forgot to take that out that was what I forgot to
do before um let's see right because it's a lot of wired I totally missed that okay uh uh I um oh I've got the provider
name like I don't know what provider you're um all right so this was not unexpected uh uh so let's go figure out what am
I um oh uh I wonder I wonder if I need all this stuff um it's amazing how much of this stuff is just like copy and paste
the right things uh I don't think I need the profile I would have thought some of this stuff was all right so whatever
do I need all this other stuff um am I mixing up my equals with my Dash that's problem I want I forget that does do the
hey look at that all right so at least no no errors uh and thank you howling arctic fox appreciate that appreciate the
assist all right um now that's interesting that GitHub is still showing up as a login possibility I thought I didn't
have that oh I wonder you know I I bet that that still works but did I not fix those let's fix those thank you good eyes
um I wonder why it thinks GitHub is config oh I know why I think I've got a separate yeah let's comment those out uh and
let's rerun it just to make sure that that see I kind of made the mistake in in this stream that that I've made before
which is which I should have done um but that's all right we can always go back to a simple App instead of trying aha uh
uh let's see uh invalid redirect oh so this is I think this is wrong I think I actually uh first of all let's say
localhost is it that I bet it's because it doesn't match like that if you want the nerdy explanation um I wonder and I
don't know if like this it's always interesting like errors in security um oh detailing arctic fox just redeem it was
out of stock no that it shouldn't have been out of stock wow 25 minutes oh man uh huh out of stock you have enough
points and it's saying you can't redeem it that's weird I don't have any of the dark modes on pause well even he
redeemed it or they redeemed it so I'll have to do that um so one of the things I was saying is about this this nerdy
explanation and um in errors that when it comes to security that might not be like something that somebody could
leverage and and like is what's the reason for this being invalid is this invalid because it wasn't one of the ones that
I specified in my setup which is what I suspect that 127.0.0.1 does not match uh this should just be um localhost uh uh
so let's um let's restart and while that's well so dark mode was already I think there's a limit to the number of dark
modes that can be ordered um and that's one at a time um but that's weird I'll have to block the twitch folks and find
out oh some of the messages are dictated by all right so we restarted uh let's go back to localhost oh because that's
not what I had I had login um which is actually not what I wanted so this is actually the correct URL that I should have
in the in the application uh let's go switch the right thing to do um uh this is the wrong URL why did you all even let
me type that in Oh weird there's a little scrolly like this there's some I don't know this input is weird okay so I
think that's correct let's save it okay um um we want to go back here okay so let's log in hey look at that which is
basically Chrome just without the Google or without as much Google as I can I can stop um now oh so it was using the JWT
all right uh yeah I probably do want an incognito window that's true um I guess when it was getting the user info it was
getting the JWT but let's let's make sure and let's try it in an incognito window oh I've got to switch to dark mode uh
I'll do that in a second I'm not counting this towards the dark but I guess that doesn't matter so um let's go you have
to say I'm a bit confused why it was fetching the JWT and this again shows my uh lack of right okay uh okay so now we
could do the trial and error but all right let's uh let's go back here um hmm foreign oh huh that's interesting spring
is a assuming gotcha boy a button on the fusion auth like you'll get a lot of customers if you have a if you have like a
one-click configure for spring and it just does all this through a wizard or something a one-time thing oh yeah dark
mode uh let me switch to dark mode stop the server let me start my dark yes you're all going blind because it's I do get
it like some of you are in time zones where it is nighttime uh let's go here appearance um there we go foreign that oh
would help have the thing started uh oh and I want to set the timer so let's go here there we go I hear you homeless
yeah nice try transfers okay uh let's go back here and ah this is what I expected so um we've got uh our granted
authorities uh uh stuff here um but I'm pulling out specific stuff for for GitHub so this is not not surprising so hey
look at that we got we got um and I dumped the whole I dumped the whole principle uh so we can go ahead and grab what we
want um I'm actually kind of assuming role all those error other errors were not wanted uh so let's go let's see what we
got so user attributes uh oh preferred username so um I I don't last time I looked at this stuff there was like no
standard for what these properties are and I wish there was some kind of standard uh but let's go ahead and block this
so um so let's uh let's go to the GitHub username multiple extractor this thing is actually used from the Welcome
controller um yeah I could I'm not going to so I was looking for login and that's why um that's why I couldn't find it
so let's uh no because like it's it's login for for GitHub it's um what is it like everyone is different everyone's
different be consistent uh so that's your username is there like a not preferred username you're all special in your own
way um can grab the email I don't think I uh uh will I use fusion and product you know I don't know if I'll use it for
this application although I might um I'm not I'm not sure this there's uh some features for ensembler that I need for um
dealing with multiple groups because right now I run one two three I run four weekly ensembles for four different groups
well three different groups um and I don't want to manage the groups like I'm I'd be happy to let Fusion off um so uh
this Branch specifically is for me to just test it and and and get it to work um but I could certainly see uh using this
mainly to associate specific people with um groups that I can manage from somewhere outside of my application I don't
really want to Implement group stuff myself I mean I could do it but I'd rather not um for what was the other
application I was yeah there's another application that I'm working on that uh that this uh would be very handy and
again it's like I don't want to deal with auth I want to offload all that to somebody else I'm more than happy to do
that all right uh so we've got our preferred username um scope I wonder if so what about what do I get if I ask for the
profile I guess all right there we go I am logged in as as user um ah I love that these are all three letter identifiers
like is there a reason these are three letters are they trying to save space in the in the JWT I remember I was working
at a large company that has fruit a fruit in their name um and they were passing around jwts that were so big that they
were getting clobbered and causing major hey sweetie yeah it's that it's like they were putting in all sorts like every
single thing uh it was so and I didn't I was like hey this was broken I don't know why and I don't know um oh yeah it
says right there duh yes so I guessed right representation should be compact um because you're sending them all over the
place all the time all right so we are welcomed uh let's sign out um this is a lie uh but let's see what happens it's
gonna go to member um but I'm not a member so it redirects me to user so that's an automatic uh feature I have um if I
try to go to admin it's basically going to say I'm forbidden I don't have a good page for that because yeah it's clear I
did not set up log out um but let's should we do should we should we do logout or should I add more uh uh uh rolls uh
let's close that yeah close our I wasn't just asking you Dan I was actually asking everybody but I'm I've already
decided I'm gonna go into the users um so let's go um well it's funny because like I actually never want to log out of
that application like why would I want to other than what I'm testing it in which case that's when I use the the um the
private window but yeah I don't want to log out uh yeah that's right it's not verifying it through email so let's go
ahead and create another user um oh here's the button I'm going to say it again for for emphasis like this is not
obvious where it should be uh you know I really dislike remember me because it seems like on every site that I care
about it never remembers me there's this one app that um that I used to to monitor the the laundry machines to see when
they're available and it always has the checkbox for remember me and it never ever remembers me even if it's like an
hour later like then just don't put the check box there um hey there Lord caffeine uh any websites ready to use or Java
projects um I have a whole you know that reminds me I have a draft of uh an article on pretty much that topic that I
really should publish um I generally recommend people Define it for themselves uh like what do you what do you want or
if you're looking for for topics then there's these um exercises are sometimes called katas k-a-t-a uh where there are
all sorts of different applications like one I'm working on that I'll get back to probably this week or next week is the
supermarket checkout pricer and it's just like you know think of features add them think like discounts and stuff like
that um but uh if you want some more concrete things go ahead and join the Discord um the Discord my Discord uh and feel
free to ask um and if nobody else I will certainly um what was I gonna do I was gonna add another user uh uh for the
login page does it always require an email or does it also allow username I assumed it was email because that was uh uh
password I'm gonna have a bunch of bogus passwords that I'm gonna have to erase uh uh so that's his full name languages
this one's letters for oh that's probably for the form display um it's nice that it has time zone uh because that's
something I use in my application uh Han so high uh most modern way to you can do it with swing 2 but Java FX is pretty
much the way most people start out these days I do have on my on my list of things to work on stream the um the
supermarket checkout price for that I've been working on so I basically have another another UI but yeah Java FX is it I
Dr I dread doing it because like there's there's a certain amount of just getting the project off the ground that uh
let's see I just was I'm I'm in the middle of re-watching The Simpsons and so there's the episode where Homer uh try
goes on a search for what is his middle name because all he knows about is it's the letter J and it turns out it's
actually the entire name Jay so there I've just ruined that episode so it's interesting that this says username but in
the payload its uh yesuigi he does have um actually he not only has a kotlin tornado FX bootstrap project but actually
he's been working on a Java FX1 I think he has one that's that's that works pretty well oh is this part oh really that's
part of um well they what will those RFC or spec writers think of uh is that everything I want I think so uh so so
there's two usernames so that so there's the username for the user for uh that one looks a little bit outdated uh
although it may he may not have updated it uh CG um I could always ask him so is this username then which one am I gonna
which one am I gonna get when I've logged in I guess I get this username when I log into the app and not the one that's
associated with this is this is like fractal like nested usernames um all right so let's call this one Homer J or I
guess Homer ass homewards uh times I will skip so we said we wanted this one to be a member um go where'd it go oh I
closed it right did I stop the application I stopped the application uh all right um so that's running so let's go ahead
log in uh we don't want that one we want this one now here this again was expected uh because when I had the GitHub
version I was specifically looking up in my own database but now I actually want to get um from Fusion off so let's see
principal that's an name yeah so the role user is automatically added um by my uh Grant by um I think it's it's the one
that's just by merely uh being authenticated so now I have to remember um scope that's the word I was looking for and
this is where it gets to uh that's yeah so how so I guess uh uh what do I need to ask for additional scope or does it
because I don't actually know what the open ID scope gives me um so I've got the open ID scope here uh the question is
how do I get the because the granted ones are are the um but here I'm showing my my ignorance of uh the username is
Homer J for Fusion auth the username and the context this is what I was joking about before or laughing at before the
user um the username in the context of this application though is I'm a member right so if we look at and this is where
right you can it's gonna you can really like so um but yeah that's that's true it's like I would have expected in the
context of so that's a an interesting thought transtars so uh yeah so this is the username inside I would yeah I'm
confused why I would have oh so this is this is only for display purpose that uh oh it's tied to the user not to right
so now I gotta retrieve the registration stuff and so this is um this is where I think I'd have to look let me see so
this mapper is not used um but let me actually turn it on because maybe there's something in my code yeah let's set a
breakpoint here let's and did I close the window let's open up right uh darn that shows the breakpoint here yeah so
these are the this is these are the ones I get in yeah so this um ah so I'm doing it the hard way because for the
incorporating with GitHub um so let's turn that off turns out there was an additional parameter needed for uh the web so
uh so the docs that um um but I still need to have this this user authorities mapper um so what does this do if the
authority is an IDC user Authority uh then it pulls so user attributes yeah so that's that's what I want so um uh and
it'll basically iterate through all of them so let's go grab uh this this is one of those things that um almost feels
like it should be boilerplate oh right that's right we're in uh we're in Java modern land we can just use instance of
and then we oh yeah I don't take advantage of this very much because I don't generally you work with inheritance
hierarchies but wow so much better um so let's uh let's set a break point here and here let's make this public and we'll
make it a bean so spring will find it cool all right uh I didn't import them at all so if you have this Adam and I'm big
add unambiguous Imports on the Fly and and this is important uh you can figure exclude from Auto Import all the crap
that is in various parts of the GDK and various other libraries then it will automatically import without you having to
manually select each one there's there's about five percent of the time where it's annoying where it keeps fighting you
but the other 95 of eventually I'm going to put all these tips together in a in a um becoming an expert IntelliJ
developer there's all these little settings in IntelliJ that I'm like this should uh where do I press now if I provide
only user info endpoint do I have did I Define the user info endpoint um hmm I already went past that that was not good
of me really remove the the Jason Webb key set thing sounds like you know more than I do where do I press now what uh
what will and yeah I'll stop on the ID token oh if I if I don't want local introspection this is why my head hurts after
doing this stuff there's so there's you know like any area like security is its own area of expertise and uh there's so
much I've forgotten because I just don't do um oh why did I have a and why did I have a foreign yeah I would have
thought it would hit this endpoint to to get that information um but it's clear it needed this otherwise it had an error
unless there's something else I'm missing uh let's so my config is incomplete what I'm what foreign user info I mean
I've got the four that that they if you have us if if it's a config that that I'm missing uh let me know what that is
otherwise I'm gonna so uh so this user has both member and user roles so we should be seeing which we then map to
granted authorities uh so the authorities I get are these two um oidc user Authority that I would expect because this
one um and I think spring automatically creates uh well trampstars I'm assuming that spring has already done that and
that's what these attributes are grab the the JWT but I'm gonna see what Dan is talking about oh let's um let's go ahead
and okay right so if I wanted to manually retrieve it I could go here but the idea customizations lambdas hey Dot
attitude wow one one whole year ah so this is the default open ID connect um so many types uh is it an open ID connect
reconcile or client credentials JWT population okay uh I assume I'll leave the leave that there um uh uh that's
interesting didn't I select looks like once I've modified this it so add and we want just jwd populate there we go
there's a registration that's what rolls uh you may add or modify anything in the GWT object however you may not modify
uh uh so it says prior to the version 114 the following claims were reserved does because yeah that's what it looks like
I'd want is is that okay that should be more clear because to me I could read the other way around all right uh so JWT
dot rolls equals I guess it wants semicolons okay I'm used to doing JavaScript without setting semicolons these um so I
guess that's it oh I need to give it a name uh stupid Lambda settings uh so due to attitude populates called after
someone registers no so the idea is populate um yeah it is it doesn't need the functionality my assumption is is that it
calls that Lambda when on the Fly does it call it on the fly or is all right I'm assuming that's it yeah so just yeah so
it does it on the fly during the authentication when it's creating the JWT that totally makes sense that it really is
neat um it's like the escape hatch that you always want oh look dark mode is over and nobody warned me foreign and let's
go open up I should learn the shortcut for this shifts command n I'll let I'll let Darko and go a little longer all
right um member and user voila so now I need to write mappings for these um uh I can do that I know how to write
mappings um or I could just change yeah I'll map them uh so uh actually I'm just gonna copy this one so all I need to do
is out of those out of these things I need to convert them to um a simple granted Authority so let's do that uh let's
close you so many tabs open release and close that okay foreign so when you're creating so when you're creating these
lambdas uh customizations lambdas uh so when you're creating these customizations lambdas uh no I didn't so I could be I
could basically emulate GitHub in terms of what I expect presumably I could as long as it's not a reserved um as long as
I'm not using something reserved I can do whatever I want is that correct like I could add that's pretty neat that would
be that that would be really nice all right but right now let's go uh what was I doing oh yeah I was writing the code
quickly I forget so we've got our mapped authorities and what we want to do um that's set our breakpoint here because I
forgot what they look like so I think that's right um those are going to be Springs I don't know why it did final uh yes
let's cast rules Supreme oh it's not a it's actually not that it's actually I don't know what type it is is it a list
let's see oh oh it's a Json array sure I never would have guessed that um but of course that totally makes sense uh uh
so I can't what um nope that's not what I wanted uh ah okay oh geez um so let's let's do VAR will that work so let's do
VAR rolls equals oh but it's going to just treat as an yeah that's a good point does it does it Implement something
something better well let's do this let's um all right so then this is a list um the list of I say list of string it's a
list of uh and then rolls stream map um so I'm gonna get the roll uh this is the horrible way to do this by the way I
would not I would not do this in production uh new simple granted Authority this is the string so this is uh roll number
actually I can do this even simpler what am I doing um I can basically just do uh uh return new um and then it's
basically roll to uppercase uh and then I want that prefix with with roll oops you want that that and then I don't need
the return it's an expression Lambda uh and then this is uh to uh collect wait what am I missing here that's what I'm
missing authorities all right let's format this a little nicer this is this is um bike code I'm allowed to I'm allowed
to do this uh so we want not to uh we don't want this final and we just want to sign it um uh I forget how to do that
all right so uh so we're doing is we are uh I can take that off and put that here so we're doing is we're getting um the
rolls claims they come in as strings with title case for the names so I'm just converting them to uppercase because it's
user and member uh and then prefixing roll underscore because these are roles and then for each one that I've mapped in
that way I'm adding it to the mapped authorities uh yeah totally like we could totally uh inline the the roles let's do
it this cast is sort of annoying but hey as I said I've not I would actually I might write this as production code but
I'd be test driving it actually let's oh right since um I could just do the Oh you mean he up here um but not all
authorities are gonna be this one that's why but yeah I mean I this I don't I wonder what what so I probably don't need
the user info mapped authorities hey look at that um now here's where um the other expected place where where uh where
I'd expect it to break is in my member service I'm expecting a GitHub username but we've got the authorities map
properly otherwise we wouldn't run into that yeah so technically we CA um and so one thing that's interesting about this
this process um is it's showing me where I've I've been too tightly coupled to to GitHub which uh is great for when you'
re starting out but eventually I'd want to have a much clearer separation so that if I do add in different auth for
different reasons I don't run into these issues um so I think we only do this to basically just grab their name uh but I
think I can actually get that uh uh oh I do I actually do need a member so what do I have in the database that I so
let's go back here uh let's skip out of this let's go back to our users so let's um so it's pulling the username out of
the authentication but I don't have that in let's go add one now here's where there'd be redundancies so this is an
interesting question would I probably still want uh a member object it's just I don't need I would not need to store the
rolls but I still want to associate them with um with a GitHub username because they're reasons why I have a GitHub
because it's connected to GitHub repositories uh so I'd probably instead of having um so their primary username would be
the username I would get from Fusion auth and then I would have a map to the GitHub username for when I needed to talk
to GitHub um so for now now the roles are are going to be ignored because these roles are are um are local but I'm no
longer using them because I'm now looking to to Fusion off for that uh DOTA attitude you said something about another
option besides uh open connect ID go localhost we want and hey Hallelujah I must have wiped the database bam so um again
this is this is sort of where uh uh Fusion off as my authorization provider um I probably I need to make sure that the
roles are sort of normalized uh but then then I could drop the roles from my database and then have a mapping from
authentication username to uh basically honestly I would just basically replace this column with with the authentication
the authenticated um and then everything else stays the same uh and I wouldn't even have to store the email because I
could get that it'd be handy in a database because they might want a different yeah I'm sure Dan knows all the RCs
involved do I want my data denormalized yes I mean there's there's sort of like what data do I want um what data would I
want in the application that sort of it owns versus what data do I want to store in Fusion off so um I still would I
still would want the GitHub username because I need that uh the first name though all the name stuff I could get because
I've I've always got um I don't know like I certainly could store the GitHub username but I need to auth against GitHub
anyway to get access to uh not yet at some point I might because I might need access to um it would be handy to not have
to store the time zone and just grab that from Fusion off and I use Fusion to talk to GitHub no I mean I'd want I don't
know that that makes any sense the reason why I'd want to talk to GitHub is for example in The Ensemble if uh you were
an ensemble host I could give you access but then you'd because that's not quite what I was thinking so I'd have to yeah
I'd have to create another app and another right right and then I'd copy the the githubs using the Lambda which boy
that's really handy um copy the login with to to the username um so that would actually that would actually be really
because then I would just not have to worry about if I wanted to add another provider I because foreign yes exactly tram
Stars well said fusion fusion would be my my security adapter um which would be really which would be kind of nice
because then I could offload the manual mapping stuff that I do currently um because I actually don't there may be some
cases where the admin needs I need the oauth for for admin stuff like if I want my application ensembler basically will
uh this is a future feature that that it's going to do is when you sign up for an ensemble each Ensemble has a GitHub
repo and so what it needs to make sure is that if you haven't already been added as a collaborator because for you need
push access so I need to add you as a collaborator right now I do that manually um which is fine because I add one or
two people a month but uh if I automate that that's really oauth for me personally because I own the repo unless
somebody else hosts it um in which case I would still need the the auth there uh but for 98 of the users and then if you
want to go and store your credentials there that's fine if you want to use GitHub that's fine it probably could add all
the other adapters for Twitter and so on that would be that would be really nice but yeah definitely definitely uh not
right and once once you're there then I could add all of them right yes if although I don't I don't know if I want to
support Google um I don't see Discord though I mean oh there's Discord yeah I mean Discord is just another oauth it
should be yeah I guess once you offer you could offer a there's Xbox right there this is a weird alphabetical order it's
like uh uh this one because these have icons but it's alphabetical so saml doesn't have no no icons for saml foreign you
all need to add an icon to like uh some of these to line it up oh I guess that's right um yeah I mean I guess it I mean
it's it literally is like an adapter for all the other ones so I can uh use hyper what is hyper what I feel like I know
that hyper I don't think I've heard of hyper okay so I remember this question going by up earlier in the chat uh about
Fido or Fido I don't know how you pronounce it whether it's a long Irish short I Fido um then there's all the the
current new stuff um what is it pass keys there's so much going on that that I but apple apple would if you provide the
Apple would you get the would you get the pass keys I don't know I'll let Dan answer that yes that's exactly how I
imagined it yeah yeah because I mean the nice thing about Spring Security oauth is it makes it connecting to these easy
um but there's still like not having to modify my code and redeploy to add a provider would be would be nice uh oh so
the web authen and Vito stuff is coming real soon now great yeah that was one nice thing um when I was at that fruit
company uh we had uh the little little adapters you you plug into your laptop and of course we weren't supposed to carry
around our laptops with that in there um but of course we did uh and so Dan is there anything else I should I should
look at that you want me to call out because otherwise I think we're we're at time oh I gotta do the giveaway oh my gosh
all right so what'd you get for the giveaway um there are two items you get the modern guide to oauth which explains all
the stuff that that I was some of the concepts I was struggling with I actually uh read through part of it um so uh
we're gonna give away a free copy of that um and uh a free t-shirt so you can get the T-shirt If you sign up somewhere
where to go uh so if you download and install Fusion off yourself and you're in the United States and Canada you can get
the shirt but I know a lot of you are not in the United States and Canada so the shirt that I'm giving away will be sent
anywhere um and yeah use that link so I get credit uh and uh the way I'm going to do the giveaway is I am uh going to
have you just guess a number I'm going to write it down so that way uh so if you want one of the two items if you have a
I'll give you a preference foreign so what I'd like you to do is is in chat um pick a number between uh 1 and 20. so
while you're tight if you so if you want the shirt or the book um and and the first one who who hits the the number uh
we'll get their first choice uh tram Stars I think it's a bad idea to roll your own money class period just use Joe to
money it's so easy to use I use it in um I'll use it in my portfolio application Tawny um uh it's just it's it's Joda
it's even Colburn's stuff um the the guy behind jsr 310 the daytime stuff so just use jota money um now one number per
person hold on uh so MVD Dev got got one of the numbers um so MBD Dev you get to choose whether you shirt or book that's
the book and tram star is also one so those are the numbers I wrote fifteen so mvdw you get the book it's a tram Stars
you get the T-shirt uh you know how to contact me on the Discord send me send me a private message and I'll forward that
information over to the uh to Dan over um if you want the book anyway there's there's also a coupon uh the lean Pub
monthly sale so you can always get that as well um so yeah so MPD Dev uh uh make sure to uh so mvdw wanted the book so
just give um or you can whisper directly to Dan Fusion that's fine uh and tramstar is uh uh make sure to provide your
shirt in the book and tram Stars um and that's it that's all for for today uh let me switch so uh thanks to to Dan for
hanging out and providing support while I struggle with some of the stuff um it was nice to finally get that working and
uh I now have a some of this information about authentication has been reloaded into my memory but it will be lost
probably soon if I don't if I don't use it again soon um so uh if this was interesting and useful and you want to see
more about this stuff let me know in the Discord as always um otherwise uh my next stream uh not tomorrow uh so Thursday
is probably gonna be the next stream if I'm gonna do it this week uh and I'll probably get back to um uh either there's
some stuff on ensembler I want to work on not all stuff uh or I'll finish up the so thanks everyone uh and I will see
you next time have a good rest of your day and uh if it's night time then then have a have a good evening hi
