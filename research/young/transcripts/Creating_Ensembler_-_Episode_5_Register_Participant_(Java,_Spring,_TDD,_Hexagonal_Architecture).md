# Creating Ensembler - Episode 5： ＂Register Participant＂ (Java, Spring, TDD, Hexagonal Architecture)

**Video URL:** https://www.youtube.com/watch?v=_UVD4fZzOFw

---

## Transcript

advertised is uh Mob org which is tool that I'm creating to help me organize um mob programming huddles mob programming
sessions that I'm running uh because I'd like to run more than just the one a week but even the one a week is a bit of
overhead detail tracking that uh is annoying so what do we do we build tools uh so actually hit project as well as blue
bits so you can follow along all righty it should be yep okay so you can follow along with flu bits um the repo is is
public open source uh there's a starting of a readme file uh that I was basically creating because I was testing out
this tool called read me.so uh that I found and was like oh that's pretty cool um let's go do so this is the overall
project um for managing the huddles basically I have uh I can schedule I can schedule a new huddle um I can see the
huddles um the next thing is basically details so again for for those of you new to to this project um my goal is to
make this thing is usable usable as quickly as possible hey there tram Stars welcome I want to make this usable as
quickly as possible which means right now I'm only worrying about me logging in and being able to do whatever I need to
do um and not worrying about participants sort of self-service just yet just so that uh if I ask who wants to be in the
next mob and I get people saying yes I want to be able to uh just enter them into the tool manually um I just realized
it' be cool to integrate with Discord um Service uh inter fun Z I wonder if it makes sense to make the participant
details a value object um some of the details will be value objects yeah hey there pinku welcome um so let's see so
where are we the next thing we're going to do is basically add uh add a user as a participant so what we we mostly me
but with help from y'all uh figured out that we've got um the user is is our oo 2 user because I'm using oo 2 through
GitHub uh to to manage authentication so um user is an authenticated user uh participant is sort of the main the main
thing they have a one to many relationship with huddles and the participant has a bunch of information the minimal
amount of information I need uh Center fun Z says you meant uh oh you wonder if it ever makes sense to make the
participant details a value object even though yeah even though I won't sanitize them just for right so the reason I
make value objects or new types in general is not always for sort of Behavioral boundaries um but names uh yes name and
well if I'm thinking truly minimal I I just need names uh eventually like the next tiny feature I want is just names
eventually it'll be have they been hooked up to having access uh as a collaborator to uh to the repository I think right
now just kind of name um but I guess I do need I will have their GitHub username um so I'm going to assume that I've
that they've already been hooked up uh or I've done that manually at least right now that's that's reasonable well let's
see how far this goes um so where participant is only name and hi Hub username uh tram Stars uh is it a is it good
design to have details have abstract class of details like username for o uh I tend not to like abstract classes for
stuff that links to things that are not in my control um but that's sort of a general thing so I'm not sure uh not sure
I fully get what what you're think about the bound the domain boundary uh for for this I think all of these are in my
domain is oo2 user in my domain it's technically part of the security subdomain but because it does TI me yeah I'm think
about that because it does tie me to a specific implementation it does time me to technically yeah I'll have to Fig I'll
okay uh uh so yeah so if we look at par participant right now these are strings um I have not why does it think
participant is misspelled oh it saying class can be a record really no well yes because because that's what it was
originally uh thank you intell um so yes these are uh these are definitely things that could be replaced with value
objects um and eventually I'll I'll do that um I'm not sure if that's what you were getting at so there is a setting I'm
tempted to like comment out some of these until I until I need them because they're going to sort of get in the way or I
could provide just a nicer convenient participant creation yet yeah I think that's that's fine okay um so what I need
then is a is is basically some way to trigger adding um adding a participant to an existing huddle and some point pretty
soon I'm going to want to actually persist uh the the huddles because constantly recreating them uh actually I could do
that application load let's actually do that uh so what we can do is we can create a class um and this is a spring
specific which where would that go oh that would go it so this is going to be Runner and we'll need to repository and
we'll create a okay and so then here I can say huddle repository uh save and I'll create a huddle oops it was snowing
now it's really hot yeah weather is weird yeah that's weird to switch that that melting uh says the name of the Huddle
number six uh Zone day time of let's see so when is my next huddle plan s of did it put the parentheses in the right
place I think so all right so that should preload so what'll happen is um if I annotate it correctly which is why it's
complaining what is it properly yeah component is fine uh so um now why is it having trouble oh because my in memory oh
right so I need to bridge that how did that work before oh because it used the Huddle service no I just need the
repository so let's pull this out into a method all right now it should be fine yes okay good so if we run it then we
should be able to see uh the loaded too many tabs open so there's my mob click into it uh did I expect this to fail did
I something oh yeah so registration right that's because I was creating that be last time okay and I was ignoring these
oh I forgot to figure out security make a note for f integration test and also okay I don't want to do those online
because those are those are boring and tedious and not as much fun um you spent a lot of time security yeah it's a it's
a whole I mean there's still stuff that I always have to look up because I'm constantly like well I haven't done this
since the last time I set this up and the last time I set this up was the last of the during a project and I even have
to like go to my own training materials it's like how do I do this again yeah I want to mock loged in user but because
it's oo it works slightly differently and I and I didn't want to deal with that right now all right so we did that we
did that all our test pass so our huddle detail page um this is the registration object we want to create so let's go
into our uh troller which I do I want to split yet getting there um so when we do a get for this form yeah I added that
annotation it didn't work and I didn't want to troubleshoot it at the time so um I'm not sure what it was but but it it
was that's what I that that much I remembered uh that and I have to dig dig in in troubleshoot that some more hey rivan
welcome oh good welcome to board um feel free to ask questions by the way don't don't feel that you're interrupting me
if I want it to be stream uh so what I need to add is I need to not add I actually need to create a form that has the
name and oh look I had already figured out what I needed name a GitHub username look at me username and so we need to do
is reg I can already feel like even though this this package has what five classes I already feel like there's there's
stuff around participants that should be maybe even in a sub package um because this package is already starting to feel
like the reason I'm feeling this way is I'm I'm like this isn't just registration form this is sort of uh huddle
participation registration form and I feel like when I'm adding on too many of the the nouns too many of the classes it
feels like it needs to be in a sub package so I'm just going to call it registration form right now um this cannot be a
record so we need string for the name and sorry oops yeah and this just a dto annotation can just refactor to that so
we'll just do model add attribute H registration form so uh yeah it needs to be mutable sure I'm forgetting the details
now but for using it to pull information out uh records were fine but pushing information in seemed to not work not sure
why um so going with a more class yeah I don't I don't remember the working we got the detail view we got that form I
don't like the word form in understand that's weird so it picked up registration um which int does it picked up username
intellig is very sort of inconsistent about getting getting this stuff in time LEF correct uh so pulls that out of there
add huddle do I have huddle ID in the in there uh I need to make sure I have that um so when we load the Huddle detail
view do we grab the ID yes we do do we have does it know how to pull it out no because it's just called ID it's so weird
what it knows like so so it knows all about the Huddle um but participant that doesn't know from participant views
doesn't know this stuff but from registration it knows get whatever okay um ecse that's right let's let's flip the table
and switch to Eclipse because that's worth it yes um so we got our registration form so now the page should work so let'
s do app actually I should be able to go right here and look at that so we've got no participants we have registered
participant would help I guess if I label the fields I know I'm not going to be making it pretty but I should at least
have this is the username so when they submit where do we redirect them back to I don't even think we we don't have this
endpoint do we I don't think I've implemented that endpoint yet so this is a huddle schedule this is a huddle detail
okay right and so this is where I was going to write the test the configuration test uh which I I can't because I've got
the security stuff working so I'm going to I'm going to wing it which I would not normally do um where is that going to
register uh TR remember the first time I found the stream just learning job my goal is to get a job as a Dev also look
for like SP yeah isn't that so interesting it's like it's like you know when when we first encounter stuff we just don't
know which way is up even we don't know you know what's important what what's not important um and that's that's
honestly you know as a trainer that's the hardest part for me is is like what you know trying to remember what I didn't
understand uh and that's actually been one of the really great things about streaming all this stuff is I can see if I
go back because I I save everything I've got drives filled with just video recordings over the past what two plus years
um and being able to go back uh and just look and say what was I puzzled over when I was learning X like one of the
things I'll do is um I work on my uh spring course later in the year uh I'll be going back and looking at like what
didn't I understand when I oh and then we like get used to like the complexity and it's like oh that's you know what the
why is it so why does this hard uh lusi why do I initiate the Zone daytime in the controller instead of the service um
referring Oh you mean here um mainly because uh the service is in the domain um and so this is part of sort of the
influenced by hexagonal architecture so services in the domain and speaks in sort of domain terms whereas um this
information is coming from the browser and so the controller is responsible for translating uh things coming in is like
text and numbers and and and well basically in this case text and numbers uh and it's responsible for converting that uh
at least initially into some kind of domain type uh thing um I could push this some of this stuff into uh uh basically a
something call application service um I think those terms get confusing but basically I could put this in in somewhere
else but right now it it's it's fine where it is uh but this service specifically is speaking in the language of the
domain so I don't want it responsible for converting something from a browser uh that's very specific to this controller
um because there may be getting input from another place like text messaging or command line or something where uh this
conversion would different yeah good question I'm probably missing I think I've got some tests on that so uh so we're
going to do string this and we're going to grab we're going to so uh first thing we need to do is get a ID and so it
looks like we're going to need some kind of huddle register participant for that huddle um with their name and GitHub
username so now that I know what I need here uh I'm going to sort of put this on pause so I can actually write some
tests for it so I'm going to create the method just so I can compile and uh I is going to redirect back that so now I
know what this now I know what the so what I'm doing is sort of this outside in development I'm trying to figure out
what is the what is the web UI need from from the service and then now I can start uh testing driving participant so if
we go so what we need this to do is um basically grab the Huddle from the repository so do a look up on that and on that
huddle um ask it to register the new participant and then uh save it back so I think I can actually go one more level
huddle and start test driving um register which I already had tested okay so there we go so now I just need to test the
service uh transy start this app only for you or you uh the eventually um the goal is to have uh participants register
themselves and eventually eventually to have them when they register themselves and of course I'd have to have some kind
of you know I don't want just arbitary people to register I have to know who they are uh and so they get some kind of I
haven't figured that part out but but I can't just let arbitrary people register um but once the self I want to push as
much onto the self-service as possible so uh however they they become known to the system they register they
authenticate through GitHub so it knows who they are and then we'll give them access to the repository automatically
because they're apis that do that um and a whole bunch of and then send them follow-up information send them an email
saying hey welcome to the Mob here's some reading material all that kind of stuff so all that stuff that I currently
sending them a the zoom call link um sending them calendar invites all all sorts of stuff but right now I just need it
for me that's that's why it's like what is the minimal I need in order to make my life a little Pap all right so this
already Works adding a participant to the h remembers it um so then I can just go to yeah the scraps are paper ended up
to being easier than like an Excel spreadsheet so yeah scraps of paper and lots of copy and paste um so do I need to
test anything here it's going to retrieve from the need I don't feel a strong need to to test this but I'll I'll write a
test anyway so let's go figure out where we this um did I use the language consistently yes okay that's not where I want
to be that's um this is sort of a weird test because I feel like I'm almost writing it after the implementation but what
I expect is participant are the reason why I'm I'm I'm not feeling very strongly about these kinds of tests is these are
mostly just delegation right so like schedule huddle it just takes the information creates the correct object and saves
it and these are totally passed through to the repository so I don't have any tests for those and this one is going to
be fairly similar um so this is more almost more of a sanity test than than anything really driving Repository um we do
need to schedule a huddle so test be time now uh I want to do it that way or directly push I I need the ID so I need to
put this directly in the repository no method so though uh and really all I care about actually is the ID so let's do
this long huddle ID good I all right um now on the Huddle service we're saying when we register a participants oh it
takes the actual ID okay uh and so if that works then I I ask the Huddle participants extract so we're that contains all
but that should be good right yeah I don't want to get hung up on on sort of equals stuff I need I need make sure I'm
testing that separately um but I'll get to that once I get to to persistence so let's run our tests stop the application
all right oh I forgot to to predict see I'm out of practice uh I fail and I expect it to fail because I have no
implementation for register participants so I expect it to basically this to be empty so that's why this failed all
right um now we can go here um we can repository I guess we could say find by uh so or else get um no I don't want I
want to I else throw that's what I want what's it throw by exception so let's go create that let's see if it'll create
it in the right place no of course not why would it put it in the directory hello I am white knife oh I can just use a
method yeah I need the cast though that's kind of annoying do I really need that if not why did it add it all right so
now I've got a huddle I've got a valid huddle uh on that participant uh name GitHub go uh I'm white knife no I have not
worked on Android apps and I probably never will I I I always like I I every time I I think oh maybe I'll I'll write an
Android app I look at what's involved and I'm like I'm not going down that yeah there's only so much I can do oh hydrate
all right uh so now I expect pass now there is technically something missing so I'm going to of like the the only thing
where you can get into trouble with using non sort of transactionally oriented storage systems yeah but then I got to
look learn cotlin and I've resigned myself to the fact that I'm I'm I'm just not going um I think I think that's right
do I not have an participant name I was fooled by the fact that it's called name here uh but it's full name here and so
that's why it was complaining here uh you know what I'm going to rename this to participant view because that's what I
call in my code oh thanks for that rename that was horrible that was not at all name and oh interesting casing uh
technically this is correct cuz the H and GitHub is is uppercase um is this a personal project uh reason why I'm having
to think about that is technically it's for my business but it's just my business is just me so business uh is this
going to be confusing in the future um clearly I am inconsistent um I'm not gonna all right let's let's not do that uh
and let's not do this either did I just rename it without let's rename this because even though it's correct I just
think it's going to cause me heartache want capitalization right uh I mean the project is open source um but I need it
for eventually uh I run private mob programming sessions and eventually I'll be charging for those and so I need a tool
to to manage that but it's open source so anybody could could use it um all right so now GitHub username is name which
it still thinks is wrong but I think it thinks it's wrong here because participant view is uh uh a record and so
intellig is not quite caught up to records in processing time Lea here though um I don't know why it's not recognizing
this unless I got a capitalization wrong there as well no there it's correct the H is lowercase and the H's lower case
so I think it's just intell is confused possibly I'm confused but it looks okay to me uh where do I learn design
patterns from I learn I mean I'm old I've been around for a while I I learned I learned design pattern from the book uh
discussing it group I think it's just study group yeah um but how do I recommend people learn design patterns um uh one
way is is is implementing them I I think you know there's always the stage that I think you sort of invariably go
through when you're learning anything new is is you tend to see everything through that lens and so when you learn a
design pattern you tend to look at everything through through that thing um there are a couple of sites uh that I
usually recommend I don't have them off hand but if you ask me in the Discord um uh I can I can dig them up um but it
really it's it's just a matter just a matter it's not just a matter of anything uh it's something that you just have to
be careful that when you start learning them you're going to see them everywhere or see application for them everywhere
and you just have to and you have to be careful not to overdo it um but you will and so I think I think like anything
else you have to implement and see what are the implications you know if I use uh a strategy pattern versus adapter what
does that mean what does that do for me why would I choose strategy over decorator and and I find discussing it in a
group or with with other folks is and not just sort of by yourself I personally I think design patterns are useful I
think being able to do refactoring uh and test driven development is much more important now with that said when you're
doing refactoring sometimes you'll be refactoring to a pattern so knowing the patterns um but I think knowing just
getting really good at at the basic refactorings extract method rename um move methods things like that uh patterns yeah
um UB no five levels inher you're doing it right yeah refactoring g is one of the one of the sites I recommend um good
materials on there this still not quite enough examples um and one of my sort of many back burner projects is to provide
deeper examples um but I'll probably cover that kind of stuff um sometime it when I pull together my uh the follow on to
my uh maker code more testable class which is basically thing um qu qu chrona sorry I'm reading your name incorrectly is
spring better than react um that's yeah it's not Apples to Apples spring is a framework for there don't now there's a
spring thing for react um but that's not at all what I'm doing here what I'm doing here is spring framework spring boot
for Java uh and that's not at all something you can compare to react totally totally completely different things one is
a front-end technology and the other is a backend technology uh one is for JavaScript typescript the other one is
different uh hey T Chan yes learning them in context um I very much believe learning about what the problem is that they
solve because without knowing that you're just going to randomly refactor to to patterns or you're going to randomly use
so I I really do like the idea of refactoring towards Pattern because that's that's what I do I don't necessarily start
out I'm going to use a strategy pattern here it's often because of some constraint or some need that I have that's like
oh I want to be able to swap out these interest calculation algorithms so I will then refactor it to um to strategy
pattern sudden uh Cur for advanced patterns if you're not developing a general purpose framework yeah and that's that's
a good point that a lot of them are not very useful in sort of day-to-day development um like the last time I used proxy
or prototype or I mean even decorator I mean for at least at least on the back end I don't I've used a couple of times
uh adapter I tend to use a lot um Factory method maybe sometimes factories those I use somewhat somewhat frequently um I
don't know if I ever finished writing it uh but I had an article sort of like here are the common patterns that you're
probably going to encounter on sort of a week a weekly basis um and then there are the ones that you're probably not
going to encounter except yeah um well I would say spring is primarily dependency injection framework I mean usually
when we think of spring we think of all the the modules it has although I guess you could look at just its core as
having dependency injection and some other things uh I believe yeah larl or and Django I think are probably to um oh
lexler is the followup um mainly so I think of both parts as being part of the make your code more testable um and there
actually is is stuff in in between those two classes because there's some folks where it's like I'm not going to be
changing my my architectural design I need to know how to better refactor more at the code level and so there is sort of
this this this area in between those two classes that's like let's do more refactoring towards sort of design patterns
how do we how do we refactor some classes um not concerning with how do we test stuff outside so there's some stuff
that's in that's sort of in the middle and that's of uh hey jabba MJ is it possible to make a backend Java project that
goes into react front end yes absolutely and yeah I mean you right now I'm creating my HTML front end server side
generated so spring MBC is generating the HTML using this template um here uh what's called time Leaf um but we could
totally switch this to being a rest restful API sorry about the eye roll because nothing very few people are actually
doing rest but whatever um basically an HTTP API that would support react or view or something from the front end so
that's really what for I mean if you're yeah if you're a JavaScript a typescript developer you're not going to use this
because you're going to be programming using some other framework uh with with no JS but since I'm a Java guy I use
spring because it's pretty much does what I needed to do and it's pretty use trar asks so rest um if you look at the
original definition and the original discussions around and what it's supposed to be um the aspect that that's normally
ignored is the hyper media aspect this idea that um you sort of provide uh instead of being this very tight connection
between a frontend between a client of an API and and the API provider um you loosen it up a bit by the API provider
providing links um saying you know here are the possible things you can do based on on this input um I not describing it
very well but but there's a whole area of of more client driven um sort of instead of hardcoding stuff in the client
that it that pays more attention to what the back endend is is supplying so if you look up hyper media and rest um
you'll probably find more than you want to look at it these days for worse I won't say for better for worse um rest has
become a synonym for Jon uh and apis over HTTP yeah the whole hados stuff yeah yeah I don't I don't I don't have a
strong opinion about whether hyperdia is is good or bad um I can see some places for it and Heist strer uh but um I mean
there's got to be there's got to be a reason why why it's just not as used much not used as much although I know there's
there's there's folks who do use it quite heavily uh and spring has full support for it with spring rest but uh sorry
going back on chat here uh you asked because you so many jws are spring hibernate Java um if you're doing Java back ends
spring is the standard I mean it's not an official standard in the sense of governmental but it's what we call deao
Standard which means it's super super popular everybody's using it other Frameworks that compete against it uh there are
a few quarkus um Micronaut and some other things but right now from a market share point of view and a mind share point
of view spring winner uh R my project I'm working on as app yeah I'd like to call them web apis 2 uh strager um but a
lot of people call them rest apis uh I call them HTTP apis but but that maybe I'll just call them web apis HT HTTP takes
too long to say say uh I am white knife what kind of side project should I work on to learn design patterns um I'm going
to give you the same recommendation I give whenever somebody says what should I work on which is find a project that is
personally meaningful to you because you're going to be the one deciding on what it's going to do and you will then be
instead of trying to find artificial things that you could do um creating something useful for yourself uh will sort of
stretch you in ways that that sort of normal here do this tutorial project won't because you'll have to implement Things
based on what you want it to do um and you want to start out with something that's that's small and then grow it over
time and uh you'll find I think that's more useful because you'll find sort of it'll it'll be more realistic you'll have
to solve problems um that you'll encounter uh and I think that's you know and if you do it in ways where you're doing
test driven development if if that's something you're comfortable with or at least writing lots of good tests um doing
lots of refactoring I think that is uh uh and then you can start you know as the project gets more sophisticated because
it's personal and has personal meaning you will you know sort of be more motivated to to work through some of the
encounter yeah dub dub dub and and I used to say that too and then I just stop because it's just annoying uh there's
also Spring hados right yeah yeah the uh I've used I used this the play framework back in the back in the in the sort of
drop wizard days but I decided at that point drop wizard was better this was in 2017 2016 um and then uh I did some
spring stuff and wasn't happy because it hadn't fully gotten rid of the XML um but after that once they got rid of that
then then spring is where I've been time yeah uh TR Stars makes a good point which is if you one of the hard one of the
things we often create our projects that are almost just data entry projects I mean like this one is is somewhat like
that but you have to sort of grow it past a certain point where now you've started to add actual Behavior so things like
constraints things like rules um once you start getting to to something at that level where there's there's some
behavior and not just sort of editing stuff that's in the database that's where you'll really counter uh some of the
important things around patterns yeah I haven't played with AOL a lot um but it's pretty cool oh and NightLight all
right I think I'm caught up on chat awesome um this is still bugging the hell out of registration all right so let's uh
I think I fixed everything now that we've got all capitalized all right there we go not not pretty but I'm not going for
for for beauty here um so now I've added that participant they're in there uh and hey look current size actually says
how how big the the current huddle is so commit now specific did that looks commit yes it works it works thank you for
the pass emotes all right uh so let's see what next next uh so this is done could uh I could add constraints but if I'm
being honest really the next thing I persistence because having to type this in every time would defeat the purpose so I
think other than looking for some refactoring opportunities uh I test um so this probably will need to be a factory
method of some sort but I'm going to skip that for now because uh I need to sort of stretch the code in it in a
different direction but yes I sometimes ask myself that question leex have uh not sure what code to test uh I could
write an implementation of hey there Simon yeah I could youo the whole persistance part there's not much to it uh other
than I mean the mapping between huddle and participants is going to be the Thing um how do I want to do I want to go
down the whole database route or do I want to just file even file stuff is just annoy just annoys me and I try to avoid
it because it's um I'm just trying to like I could I could uh to Json and not write it to anything and just copy and
paste it that seems file uh yeah I mean I could write it just to just to to do it and then then migrate my over migrate
my way over to something testable yeah I'm probably going to use postgress just because um where I'm going to deploy it
which is Heroku uh has great support for that very straightforward I've done it before so that's eventually what I'll do
but um do we think we can do this without tests yes do I think we can do it easily I'm not sure um all right well let's
do it so uh we'll need to create an implementation of a huddle into uh adapter file um uh you know I'm binker that's a
good question I I still haven't quite figured fully figured out naming conventions um for packages uh for packages in
the adapter out because sort of by definition there's a port somewhere you've never seen me this lost you haven't watch
been watching enough then I get lost like this all the time all right so if we want to save a huddle like do I want to
just write it to Json and delegate to the to the Jackson lifting I don't know why there's a part of me that feels like
that's cheating but topit uh can I get an object mapper I can just new one up right let's mapper all right so we got an
object mapper um so that means to save uh I'll just use the object mapper uh oh look at that I forgot see I don't use
these aspects of of object mapper very file let's do that um where am I going uh I don't know where the current
directory is but wherever it is that's where it'll store it pudles on and then basically it's it's huddle except I can't
do that uh because uh by definition domain objects are not what get persistent so I need to first yeah no I this this is
this is this will be the most straightforward I do need to though conver I can't write the Huddle directly I need to
create some huddle a huddle dto and a huddle and a participant dto yeah so it'll it'll put in the Target directory what
does it put in the root of the Target or is it honestly it doesn't matter as long as it's reading and writing this from
the same place thank you for the hydrate uh so good I don't have to deal with the file stuff directly but I can't store
huddle um why is it complaining though oh because I need to return something uh so somebody needs to sign an ID that I
that inmemory huddles so saving means I need to huddles so every time I do a save it has to rewrite the entire list
that's gonna unless I write each yeah I could just re rewrite the whole time yes we're about to find out uh so sequence
that's going to be interesting this is not going to be as straight photo as I thought which of course um because it can'
t start just at Zero it has to start at uh I actually so I this since I can't delete I can just of sorry I'm just having
flashbacks what uh there was a course I taught um which basically PE had people write this kind of not a file based
version but an inmemory based version of the repository and uh it was really interesting to see what students and these
were you know people just out of school um what they would write for this part of the save where it basically had to
assign an ID um you saw this typical stuff of like random um which for what we were doing would probably work but not
safe certainly uh because and they some people did uuid which was fine but I had a requirement that to had to store it
in a long uh and so that that didn't really work um some folks would basically scan through the entire list that they
were storing looking for the max ID that existed except once I added in delete that went out the window uh so anyway so
it was so it was really interesting to see what people came up with yeah I'm not going to use a a GD uh I'm going to do
the Let's scan the the Max uh so I'm to am I going to load it every time I time so we're going from so basically it's
findall I might have to write find all huddle all huddles equals this is going to be so inefficient but what who cares
right um and then uh but I only need to do this if the ID is not assigned because otherwise it's already got one so if
this is um find the max ID uberX is getting their money's worth for for the right code without a test because I'm
writing way more code without a test than than even I generally do for for this kind of Channel Redemption uh I prefer
long over ID mainly because um uh it's U eventually I'll be storing it in postgress and I let it assign the ID there is
the other way to go which is create a a GD or a u ID um and sort of separate the two but it's more straightforward that
way yeah I don't want to use the object's hash code I'm I'm fine with with doing with doing it this way because
otherwise I just use should I just use a random number I could just use a random number that would probably be fine we
just have to make sure the seed is is not uh predictable no let's do it this way um hey con schoney what does object
mapper do so object mapper is the Jackson um uh uh Json uh library that Maps Json text into objects and vice versa take
objects and write this some out as as Json yeah and hash hash codes I'd have to make sure I'm just going to use G gonna
assign IDs this way um hey Alex amam can I teach this Kafka elastic search nope uh I don't I haven't used Kafka in five
years so and I haven't used elastic search ever I used to be a solar expert um I no longer a solar expert all that all
that knowledge has been ejected from Jas all right um yeah I've written so right uh what the hell was I doing oh yeah um
uh so let's map to int I was about to write a loop and I'm like why the hell am I writing a why would I write a loop I
can use stream so let's map to int for the huddles uh huddle ID oh uh so first I need to huddle right uh which ID is on
wait a second I'm getting confused what id this is this is a huddle ID so why do it giv me why does it giv me me such
here boy H is in uppercase I'm really having complaining um before I can save I have to sign an ID if it needs one so
that's what I'm doing right now oh dark mode oh boy we're going for here uh hold on let's see so we'll map to to that
and then from there we want to map uh huddle ID that's what I want comparator I'm I'm I'm insulted that um I'm insulted
intellig didn't compare that uh didn't compare that didn't recommend that uh okay and so now this is long I'm confused
what is is it complaining optional so it's uh so it's or else uh or else get uh I just forgot this how to write that do
I need the yeah I don't need that yeah okay uh that's Max ID and then all this to set freaking little ID of uh Max ID
plus one assigned uh let me let me do um dark mode because Kanani redeemed redeemed hilarious all right hold on I guess
got minutes okay yeah all all you dark mode fans are now like oh my God thank God oh my God you mean he can do it and
he's been to don't follow all right so we' we've gotten the idea sign uh in case in case it didn't uh take now we need
to map all of the huddles into huddle dto that we can use convert uh yeah you know if I used U ID it only would have
saved me what nine lines of code so um but it would have required me then to change the type of the ID everywhere so
actually not everywhere well in enough places anyway so now I need to map uh so I want a list of huddle dto so let me go
create that and that goes in along um that's that zone daytime I hope it knows what it's doing with that and then these
are going to be participant toos so we'll go create participants we'll just grab setters this lumbo uh maybe we can
start IDs from one by default it'll start from one did you not see what the code is doing basically what happens is uh
if there are none so it'll do a stream of the existing ones and if it if it doesn't find one it'll generate zero but
since one unfollow wow I've got some really demanding viewers here it no I don't have it I'm not about to add it so too
bad all right uh so now we want to basically uh huddle dto we're going to do do I need all the huddles anyway yes I do
okay because I'm adding to that list so we're going to do that um and then in uh this is like not only writing without a
test it's also writing without any of the intermediate refactoring that I'd normally be doing uh stream of stream of
Consciousness coding huddle dto so we're going to take all the all the huddles we're going to map them uh I need a
mapping method on my dto so I want to map from so huddle huddle method uh so it's going to huddle youle dto uh could you
use records in there yeah I could um honestly I'm going like the the path of least resistance so whatever I have to do
not a lot of thinking thinking about um was catching up on chat lumb does bite code injection yeah immutables I should
actually take I keep having my list to take a look at immutables bad never look at learn guitar if I had to do first
luckily top hit this is not required to learn how to play guitar yeah I know Jackson's record records compatible I'm
just going path going um okay so we need to create a new huddle BTO Huddle and Huddle and we'll set Huddle and last but
not least uh we need participants so I was thinking it's like huh I might have been able to use map struct here but
never mind all right so dto uh empery you need me to recommend books all right top hit I I I might see you later enjoy
uh so participant D I also need um a map method so we'll do uh huddle dto set stream map uh so we want to map puddle dto
no participant dto from and let's go create this participant this feels so weird to be writing code like this um so I
want to return a new participant dto oh right I don't have any uh I just have Getters and Setters so put that in dto oh
I don't want to copy all that it email set set geub username at least int is making pretty good suggestions and dto and
then return pudle dto so what was it complaining about here uh participants stream two list all by itself one thing I
just realized is in dark mode um the rainbow brackets plugin I use is a lot more noticeable in terms of the colors it
uses for the parenthesis because we see sort of the shift between the the green and the yellow um all right so we've
done that what else have we got uh this then we need to okay now we can finally uh write the Huddle dto uh and we'll
return about yeah to me I I I find it harder to to see errors in dark mode that's why I don't use it well one of the
reasons I don't use it oh dark hydrate oh I I'm very sensitive to code say goodbye uh put your sunglasses oh wow it's
much faster than it used to be you should I us I used to have to actually say okay or apply before it apply the the
light theme now it's like k um now what is it complaining about here file can I just do that is or is that too easy okay
uh now write values okay fine that's an exception um what do we do with exceptions we just catch I'll just throw a
runtime exception what do we do we just catch runtime hey lien they're your channel points um I don't know if I have a
cool though easier um but we got way so uh object mapper read value um mute move move dojon uh and it needs to know the
type be oh it's going to be that awkward one to use a list uh I don't want to do that um this okay so that'll be much
easier to work with uh so we want to write that we are writing that huddles D huddles confusing oh my gosh okay uh and
the dto um this going to give us the type that we want yeah so I can just puddle um uh Ur says uh for every of white
mode use a household in India doesn't get power for a whole day I'm sorry mining Bitcoin far out ways any waste of that
causing yeah you know the right code without a test probably could use a timer um but it's basically write write write a
file based version without tests we we'll see I'm I think I'm almost there uh the find by ID that'll be easy because
I'll just read them all in and search uh this one I got to do the conversion the other way so I've got to do here uh
create a sufficient yeah that should be sufficient and so now here huddles dto map uh then we'll map uh what are we
getting out of those we're those why am I not hitting the right file control uh so we want so we're getting that's a
list we list of huddle dto and so we're want to do huddle dto method uh no static I mean what's funny is I'm going to
have to write some of these conversion things anyway when I store in the database so I don't feel too bad about writing
all this code um I won't I won't actually be throwing uh Throwing It All Away uh long method alert oh we've got many
many many code smells going on here uh s if I don't say bye later it's because it's almost 1:00 a yeah go to sleep oh no
weat l 25 I'm not going to be streaming for oh basically till the stream ends so this is dark mode stream all right I I
kirite I'm actually really amazed that that they were able to finally get that appearance change to be instant although
I'm not happy that it does it that instantly um like I I would prefer wait for me to hit the apply button that's like
all right so we got to convert do do the same thing here we know we're going to need in the participant dto we know we'
re going to need a method that's going to be uh participant uh as participant and this doesn't take a huddle dto because
it's on a huddle dto and so hle so from the Huddle name and of and then uh for all the participants so participants map
stream map uh participant as participant and then to gets come on you didn't really need to put the this in there did
you I guess you did huddle oh I don't have an uh that uh or I could provide a Constructor an overloaded Constructor for
easier Recreation oh my hold on I'm way behind on chat uh Mr kir life says um run through basic instructions before oop
Etc um yeah I'll leave I'll leave other folks to to reply in chat you can always join our Discord um that's a bit more
of an involved question Dev yeah so I don't lead code um I think that's not at all interested in that if it if you're
using it in the way that I think you're using it which is uh very much not the types of of coding that I do all right um
got 20 minutes do we think we can finish this so we got our participants converted and now I think then uh and then they
do huddle and did I do participant dto no I didn't so let's do that um so participants um name it's so weird sometimes
intelly will will autocomplete the entire set of parameters comma separated and I never quite know when it when it gets
triggered um and so I'm always like how do I how do I trigger that on purpose but oh well so email Discord username and
then M Lobby is that right those all the same yeah they are okay cool so that's done that's wanted um Okay so we've got
our dto we map them to huddles to convert those to a that oops there we go oh my gosh so much ID is just find all uh
filter find no find first find any find first find any uh where uh so this is going to be a stream of huddles wait it's
not the find this is what always confuses me about the streams it's filter um yeah pretty much I agree with what y uh
even even for jobs at at those companies I don't the kinds of questions they ask and ster knows this as well is is not
those um and I don't know this I'm not going to get into that you stagger honestly in terms of algorithms I I algorithms
uh all right so we're filtering so we're filtering where uh the Huddle huddle. ID is equal to May finding it does what I
think it does right returns an optional short circuiting result okay and filters inclusive right okay and I can just
return that because uh all right 46 minutes later I've um well what do you know we have time to actually see if it works
no I'm not writing it there's no more code to write there's no more code to write yeah when I got a job at Google there
was the only kind of competitive programming I knew of was like with the ACM Association of computing Machinery job I
still haven't renamed the class all right uh I'll call this one file huddle huddle that's as far as I'll go and rename
dead um should I I just totally YOLO it like it uh so let's see so what else what I need to do to wire it up is uh in
the momor repository um I'll just this one out and what we're going to recreate is the exception oh right um the findall
will fail because the pile doesn't exist no I'm not I'm not no I'm rejecting that I'm rejecting I'm rejecting both of
these you can have your you can have your points rename um so uh yes so the startup case of uh find exception um I will
magic puddle puddle I'll think about it consideration so is it like because it's um now we have some other problem but
hold on I will I will store that uh unsupported operation so failed to execute the command so the huddle oh because I
returned an empty list and you can't add to an empty list so let's just list I think it was Uber X who initially did
that some um oh uh Zone day time is not supported 310 okay so included module all right oh you know what I wonder if it'
s there and I haven't register it because I basically did not have that injected so uh let's move it That Into The then
yeah so that's that's the problem is is I was creating my own uh object mapper that didn't have this mapped do I have
something like a road map on what to learn on Spring uh I think it go sort of goes back to my same advice of like pick
an application pick a little project you want to create and then learn about the parts of spring that will let you
create that um and I think you will naturally find the pieces that you need uh you're likely going to need like cord
course Spring stuff all the auto wiring and and and concepts of bean scanning and stuff like that um so your basic
spring boot stuff MV spring MVC because that's how you're going to implement web apis and then beyond that it's you know
database modules depends on the database you want to use uh then you're then you're off into whatever else you need and
there's not a lot that you need um I mean I pretty much get Java developers up to speed in three days with my spring
training because once you're there then now it's just a matter of figuring out what you need to correctly um still can't
Constructor oh and that means it needs a Setter all right that uh all programming now didn't I fixed part of it I didn't
completely fix it yeah crash file see now I don't know what the hell on um yeah so I think it basically created an file
right because when it fail when it failed that it couldn't write the date time it just basically crashed all right so
let's just remove that um at least um yeah in general when I interview people it started up successfully when I
interview people I like to pair with them that's what I like to do uh or even better if we're doing mob programming pull
them into the mob uh K I have written rest Apon work with angular ready um yeah I mean once you're beyond there there it
in terms of what to learn next honestly for me it would be get better at at testing because spring has a lot of
capabilities there but they're not documented developers yeah so I I um I did the yacht dice game which is like yatsi uh
I did that all test driven that's you'll find that on my YouTube uh that's also nice because you know anything with with
like sort of like games like that are really nice because they have lots of rules that are very testable um and usually
the user interactions are not very sophisticated so you don't get hung up on that uh so I I definitely do a lot of game
stuff in uh in when I'm teaching we use Blackjack yacht YSI that kind of stuff all right um so it's up and running uh
let's let's see if we can actually see stuff all right so there's a mob there and it has ID of one a not have what did I
Implement wrong so not found probably means when it was there got no participants but that's fine but it's there that's
interesting what did it what did it fail on um roller oh I'm today dashboard controller so this was the Huddle detail ID
which is one so it should have been if oh I never implemented equals here uh and although the default equals what would
the default equals for a record be that should would would it use the hash code of a long no that wouldn't work uh but
it won't be equal equal oh duh uh so let's let's do that I will not enumerate in all the ways that test would have
caught all this stuff all right um but hey we persisted stuff which means we're going to end up mobs when it starts up
it adds a new one that'll be somebody all immutable right uh yeah too well it's a list and I mean I could create a new
list and then add it um idea so that one is fine because we're writing that one returning so that's interesting so two
list puts it in an unmodifiable one but H yeah I know dark mode ended I'm aware of this uh I'm also aware that my stream
should be ending but now I'm at like that point at which it's like can I just get it to work so now we see two mobs
that's fine uh this should be one and this should be two I should be able to go to this one and look at register will
that work no of course found um I have don't did it add it and not save it no it did not save it correctly ruined yeah
normally just just for those of you who who haven't seen me redeem the right code I usually do not write this much code
without tests um the reason why I was okay with doing it uh is because this is temporary anyway um and the dto stuff I
actually will use when I store it in the database so that's that stuff isn't a waste um but let this let this be a
negative example for for you if you were thinking that you know you don't always need to write lesson um how much more
do I want to so it failed it do I dare debug so should be able to go to uh the dashboard and look there's an Ever sixes
so wrong yeah I'm not even sure where to look for that so I think we'll we'll here yes I'm clearly capable of writing
bugs with yes this is the first time in and I can't remember when that I've had to page uh the hidden value is zero and
I said I would stop but but now that this is this is the danger zone of like oh let me just do a little bit more and I'
ll be able to figure it out that because that huddle correct yeah I'm guessing it's it's not retrieving it properly but
um I will I
