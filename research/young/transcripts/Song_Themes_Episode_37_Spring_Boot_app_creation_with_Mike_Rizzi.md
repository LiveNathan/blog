# ＂Song Themes＂ Episode 37： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=57r0Y8tkpBg

---

## Transcript

all right hello folks welcome welcome to another episode of working on song themes how you doing Mike doing well doing
well thank you I think I'm awake I am yeah I don't know about you but but when it gets to around this time of year when
the days are really long and the sun like Rises at 6 I'm I'm usually up at like 6:30 which is way earlier than I'm and
then I'm otherwise up explain it for me you it's it's very strange to be like oh it's it's like 9:30 and I've already
been up for like three hours got my run in because it's gonna be hot today so yeah yeah I get up early in general but I
was shooting for 6:30 that's why my alarm said I was up at 5:30 I like damn it I want more sleep but I can't because
there's Sun yeah so last time we had started working on on our uh autocomplete component uh so let me know when I can
bring up your can I ran the tests all tests so we're good great so let's see we were up in here right so we we had a
drop down where it showed all the themes that we could select one so that's all that that complete uh do we want to run
run the app and just see where see where get our heads back in the game yeah yeah think what interesting I was expecting
Halloween uh and it's an actually wow so it's State let me hit this just see what that and we know about the duplicates
that's are yeah so uh well I know we got the drop down to work I don't know that we're actually where we're at with with
the auto complete so so take a look we we didn't say we completed the autocomplete we said we did the the drop down and
we were starting on the autocomplete so I think we're we're just we'll have to take a look at at yeah we got list of
unique things alphabetical yeah show all existing things yeah only one to be selected so I think we might have we can
look I think we might have harded hardcoded the the response does seem like it doesn't wow hey there Deon um always open
for questions doesn't necessarily mean we'll be able to answer it uh but we're here it aha okay so we did hardcode it
that's great all right so that that that confirms that we didn't break anything but I think we we basically were saying
we we just started and so one of the things we we did on this was we put the the response body because we wanted this um
this request maybe scroll up just a line or two yeah nope too much one bring just bring yeah there we go so that's the
get mapping uh and if you pull up the uh the HTML we'll see that it does that get I'm trying to remember the name of the
file this one right yeah yes home yeah and so we'll see above that select because that's just the the single drop down
right so we've got the the trigger um so basically Triggers on input when the input's changed uh and it delays every 500
milliseconds it doesn't HX get that was the thing we fixed at the end of last time um and the target goes into search
results so with the hardcoded stuff we know that that that's working um and we're just thr in the div for now yeah yeah
that's why we were seeing the cats and dogs there so I think um so if we look above V jira uh to a certain extent 21 is
is kind of done I mean we don't get the correct HTML auto complete but we do get that it puts it in the right place does
it well it certainly puts it in the right place for now like it puts it in the intended location which is search results
which is right uh oh that location yeah so we haven't gotten to like making the component nice yet but we were basically
like do we know how to you so for me this was did we use HTM X correctly so that it made the request and put the the
HTML in the right place so I think the thing that confusing is what is put in the right place we were vague and now the
vague the vagaries no the vagueness vagueness is is getting us though vories is fun too fun word um good evening astred
hey astred so let's clarify this just so we're on the same page so to speak returns HTML that is temporarily put in the
div because ultimately it's not going to go in that div well ultimately I'm not 100% sure where it will go wouldn't okay
from a drop down perspective we wanted to narrow this list down to whatever's a filtration of the type yeah so I think
typed yeah so I think for now targeting just the div is sufficient um and we'll we'll have but what we want is uh that
it actually pays attention to what we type we know that the the right so so here again we were sort of doing things a
tiny step at a time right the first step was like did htx do the right thing and make the request and then take the
requests take the response and put it in the right in the place where we intended right it did that so now we can say
okay now let's have it actually pay attention to uh the the actual request whatever you've actually typed um right
that'll be an interesting uh it will so that will mean that um so actually start typing returns so start typing it
doesn't it just doesn't pay attention to what we're typing right so start typing returns hardcoded sure HTML that gets
put into a tab yes then the next step would be we want start typing to actually yeah we want the tighted oh um I had one
of those um shower moments where you're thinking about something in the shower yeah remember how we were talking about
um um whether we're going to do search basing starts with versus anywhere within right so the theme that I thought of
where it would be a two-word theme because it's pride month here in the US and I could see somebody wanting to type the
word pride sure um and want gay pride to come up doesn't mean we have to solve that right away I think starts with it
first would be a good one but I now have a real example of where yeah so it's really more I I snagged an example for
future talk right future conversations right which I'll just throw down here for now yeah they're Pro yeah so any so you
may want to look at the the first word in in a multi-word phrase yeah I I can definitely see that yeah search um so it's
still not within the word it's it's just but it's but within the the theme phrase yeah right versus starts with first
beginning of any GG cool I just wanted to throw that down in my head y so okay back to where we were um so we want to do
22 next so given that 21 jir 21 is completed yes we 21 um is 22 enough and not figure out if there's any more steps
between 22 and 23 just intent of as we Implement we'll learn things approach I think that that's good enough yeah I
agree I just wanted to partially because we're streaming I wanted to say it out loud what we were thinking like yeah
yeah that's good enough to move forward yeah so uh dpan asks a quite a long question but I think the gist of it is um
there's so much to learn uh and you can't master it all like other professions so let me preface by saying other
professions I mean you look at other professions so for example uh you know law accounting medicine any profession like
that and and software is perhaps different in that there's just so much new that because it's so malleable and flexible
and there's so many people doing different things um but in any any non trival profession I mean even you know being an
electrician they're like what kind of electrician are you you know sort of a household electrician and you're putting in
you know wall sockets or are you like working in a in a in a factory and you're you know hooking together very large
machines so electricity but very very different knowledge uh that that you need so I think the hardest part um at least
I I know this is for for me is the more you learn the more you realize you don't know and that you will never know at
all and uh you know and this is why with with you know I was actually coaching someone someone yesterday um we talk
about learning projects so there's there's katas which is about practicing very very specific techniques like I want to
learn how to uh use extract method in various different ways um or I want to take you know this messy huge if if Spock
gilded Rose is sort of the prototypical example and clean and clean it up versus a learning project which is I want to
create something that's realistic um and it has to be realistic in the sense there there have to be some kind of
constraints uh because if you don't have constraints then you can't make decisions right and a lot of what we do is make
decisions and assumptions but we also make decisions uh and decisions based on assumptions and if you don't have any
real world constraints even if they're completely made up then you're never going to do anything because you're going to
be like oh I can do anything right because anything will work if I have no no actual requirements and so for learning
projects I think it's really important that you have uh sort of a boundary and a scope and the reason why I talk about
learning projects is because then you will learn what you need as opposed to saying oh my God there's 10,000 things I
could learn you know just the Java ecosystem you know spring I mean spring is huge you know there's lots of stuff in
there you know you just look at the modules that you can select as a starter and there's you know 30 40 50 modules I
don't know the half of them um and so uh it's very easy to like look at that and be like oh my God I'll never know it
and that's why I really encourage folks to do learning projects because it starts constraining that puts puts a puts a a
boundary around it so it's like I only need to know and learn just enough to get this this thing done because that's
what we're doing here on stream and that's what you do in software is you if you don't know something you learn just
enough to do it you don't you know it's like oh we need to learn how to how to do um you know what yeah o yeah so let's
go take a two-day course on oath it's like that's like maybe if there's a lot of people and you're about to do some
heavy duty stuff you might do that but if it's just like we need to to add you know oh we go look it up we go figure it
out and and then we move on and that's that's the reality um and imposter syndrome is is interesting I think uh you know
many of us suffer from V from this sort of varying degrees of of being like not confident or not feeling like we we um
that I think there's there's a lot of good materials out there to to to talk about that but I think again it's it's don'
t worry about what you don't know focus on on what you do know um and you know working on these small learning projects
I think can really help build up you know it's like oh look I got this thing done I I was able to to to do to to do this
thing and I think um deep also the fact that you know you don't know is actually a huge step um because a lot of people
don't know they don't know right and those are the folks that are kind of stuck and when you and we all will work work
with folks like that where they they just know what they know they don't feel like they need to learn more um so the
fact that you're aware that there's more to learn and you want to learn that's that's already put you higher up in the
game than the average engineer yeah yeah software engineer the other thing I was going to say regarding that was um the
thing about software engineering software development whichever term you want to use it's one of the few professions
this is slightly a rant but it's one of the few professions where there isn't the idea of uh continuing education units
right right my partner is an interpreter uh and she has to do a certain number of cus every year and it's not like oh wo
is me I have to do this thing to keep doing my profession it's more like this is great it gives me time and space to
learn more about what I need to do to be better at my profession and that's sort of one of the sad things about our
particular chosen profession is it doesn't have that kind of thing that doctors and lawyers and um maybe even
accountants I don't know interpr certain kinds accountants yeah absolutely yeah they have to keep refreshing yeah so um
so part of it is it makes us have to be more self self-motivated which can be hard yeah you know so yeah and you know we
all can feel like imposters or or um you know feeling like we don't know enough in in different contexts because it it
also depends on who you're surrounded by um you know they that there are always going to be people who know more about
something or who are better at something than you are um and I think you know the the important thing is to realize that
you do know something um and you know comparing yourself to others is where where you where it starts getting
problematic and that's why I like the learning projects because you sort of compare yourself against yourself it's like
oh now I'm able to do this that I was not able to do before and you you know as you build a project then it might be
months before you get to something where you have some kind of thing you can sort of use or play with and you can say oh
wow I I created that and I didn't think I could do that um I always say don't go It Alone uh like like anything you know
difficult or challenging uh or requiring you know pushing through stuff that that's not so easy that's actually one of
the reasons I streams it gives me that that motivation to to push through it's like H this really sucks especially when
I'm dealing with CSS um and you just make it through and you you you push through and sometimes you get a little little
bit of a hand uh and this is this is why I also coach individual developers is is a lot of times it's not the coding
that's the problem it's not the technology that's the problem it's the how do I even approach this these requirements
like I want I want to you know make an app that that's does you know XY andz to-do list is sort of the prototypical
example um I don't even know where to start how do I break things down into small pieces right so it's more the the
managing and and and sight ing of of the stuffff and it's you know yes there's the technical stuff but that's the easier
stuff to learn because that's the stuff that you know chat GPT can give you an answer it may not be the right one um but
it can give you an answer or at least point you perhaps in the right direction uh but like how do I break this down and
how do I do that that sometimes is is not not as obvious and I think it's a much more important important skill and I
wanted to plus one asteroids comment about you know seeking out people um stronger than you are in particular areas
right yes like my son does that he's a musician and he whenever possible tries to play with people that are not at his
level but at people that are much higher level like he wants to be pushed to be better and being around you know great
players is a good way to do that I find that to be the case also with software development you know I I've certainly
enjoyed reaching out to people who like you know like Ted you know when I first met Ted he was um I was like wow that
there's so much I can learn from Ted and I still is right but it's like you reach out to people and um change your crowd
as uh ASD says yeah one other thing is that's the other advantage of not staying in a company for too long is that the
more at least not staying on the same team with the same people yes thank you that's even better way of putting it yeah
um is that moving around and working with different teams you get a lot more perspectives and a lot more and also even
os's right um you know moving from different operating systems different languages um you all these things give you
perspective that you wouldn't get otherwise I remember I was in a one company for a really long time and when I left it
was kind of like whoa and it was a little bit intimidating at first but it turned out to be one of the best moves I ever
made was to like stop being at that one company after four years and yeah new language new platform everything and it
was right challenging but great that's what I like about ensembling um and especially you look at fast where it's like
you're shifting up te you know quote teams like the group that's working together perhaps in a mob um you're switching
those up frequently uh and there could be some downsides but the the upside is you get to work with different people who
sort of wanted to work on that specific story or that specific task um because it's sort of that that
self-organizational aspect uh and certainly working in in in a in an ensemble I think is is exactly what you're talking
about M it's like working yeah you know with with those people um and like asra says it's like we all struggle with
different things so we have different expertise and you know if you're lucky and you're working on CSS and you have an
expert in CSS that's going to make life a lot easier uh you'll learn from them and they'll you know learn learn from you
that's actually reminds me of one team I don't want to say team building but team activity that I found to be valuable
as a coach is to do the skills Marketplace activity I don't know if you know that one Ted for those who don't tell tell
us okay yeah so everybody in the team they start writing down what are your skills right and you start writing them on
this you know sticky notes and put it on the wall if you're all physically together and you start to realize like the
diversity of experience and also that no no one person knows at all and that helps with sort of getting an understanding
of the skill of the entire team as a whole and like you know oh maybe none of us know anything about I'm just gonna use
oop again um you know maybe we the six of us should spend a a study session together on it that's not probably not the
best example but something where it's like hey none of us know this and we probably should no that's a great example it'
s like you know we we we might know like the oh just get the the ba you know the basic o off but it's like oh now we
need to do this this other kind of O off off with you know this other flow that we've never used before right um
absolutely let's let's go take some time and figure that out and it's much Social Learning and learning learning in a
group is is much easier um and more fun uh if usually uh than than trying to to to learn on your own even if none of you
know it you get the different perspectives people understand things um and pick things up in different ways because we
do have different different sort of knowledge structures in our brain and uh and that's that's you know and this is why
you know I I run a book club is because it's hard to read stuff on your own uh sometimes or maybe you read it and you
think you understand it but it's not until you talk about and explain it to somebody else or or ask questions
understanding let's say hi to some folks fnu and fnu has a question uh how to have a logical architecture that can be
partitioned into a physical architecture architecture um I'm not sure about the last part of different profiles with
different contracts I have the same question what that mean uh but I can certainly talk about the the the first part I
mean uh hex architecture hex plus DD which is the architecture that that I use because it's not pure hexagonal um as the
application gets bigger uh as you have bounded context you're probably going to want to put those into separate uh
modules um so you end up with a modular monolith and then if you need to partition it physically uh you split it along
those module lines and basically separate each one out into a separate Deployable um I always wonder though why bother
like if it's a really really huge model that that takes up a lot of memory okay I can see that but if it's not that big
just deploy multiple copies of it and shut off or only activate you know the modules that you need you don't necessarily
have to pull it out into separate repositories and code bases and Deployable artifacts um but you certainly can't this
is why you know as things get larger the nature of what we should be doing is is you know you I mean I always look you
what's that it changes yeah and so so I was gonna say is like you look at at at biology what do cells do when they grow
they don't grow infinitely large they can't what do they do they split right and it's exactly the same thing in code you
sure you can have a class that has 5,000 lines in it um that's going to be really hard to work with it and so what do we
do well we try not to let it get that far we split it before it gets that far and what do we do with with s you know
with with applications that that you know internally get too large you split them and you know you find you find the
boundaries uh this is where you know domain driven design and the and the bounded context can can help you um and and
you slice it up and you split it uh and so you know but you want to make sure that you're splitting it for a good reason
um and there there for me there there's two reasons that you go with something like like a microservices one is your
team's too big you can't you're stepping on each other's toes trying to make changes uh that happens probably when you
get to about eight people who are actually actively working on a code base probably going to want to split it um but it
doesn't necessarily mean you have to go to micros service you just have to split it in some way so you're not stepping
out each other's chice modules modules are great um microservices if you really do start needing I need to independently
deploy these and usually that's that pressure comes from then scal scalability which most people overestimate their
their need for um so uh so maybe a herisa could be um go to microservices when you have no choice when you're backed
into the corner and have to versus prematurely going to microservices yeah seems to be the current theme in our industry
and it's causing us the industry Untold pain and is very painful um because people do not understand and I've said I've
had this around you know before which is the main reason you split stuff into microservices is because you have too many
people working on the same areas of the product and you want to split them up that's you know you talked to James Lewis
who talked you know who who I first learned it from back in 2011 right 13 years ago uh it was all about the people the
people structure and I was actually experiencing this we had a team of 20 people and we were stepping on each other's
toes uh and it made it very difficult to work with and had we split it up into microservice which is which I proposed
but was not the right time it would have been a lot easier um and so we basically sort of had to had to start
segregating the code a bit uh it was difficult but that's what we wanted to do is is split the code but microservices
aren't the only only answer modules are a great answer uh and it's much better and much easier to do refactorings if all
the code is in a single code base and it's modularized so that you do have independent pieces that can be worked on
independently and modular is could be a step towards microservices if ultimately value yes you absolutely want the want
the it regardless of what of whether you're going to actually split it out into separate Deployable things um because if
you do have it modular like you say it's like you then have that choice you can then say you know monolith to
microservices well how do you go to microservices you pull out a module and make it stand on its own and if you really
did it as a modular monolith that would be relatively straightforward right you know what used to be inter inter method
calls is now you basically stick in some adapters in between the two and now you can deploy them separately um perhaps
not that simple but it should be close to close simple so full aul it's probably going to require a lot more detail
about your domain so you're talking about dentist doctors so so appointments of of some sort um you gener really want
modules split along bounded context I encourage you with whoever you're working with who are the the subject matter
experts figure out what those bounded contexts are um for example uh you know if you were thinking about running a
doctor's office there'd be the scheduling aspect that's bound to context there'd be a specific doctor's um notes that
they're taking on on patients I mean that gets into whole you know medical record stuff but like you know what are what
are what's my view of of today and and versus sort of the the office as a whole um and then there's other things that
that that have to be done it's like uh uh letting letting somebody know that you know so actually sort of running the
office okay you know this person's ready for for the next appointment um right so there are different functions that
that that need to happen you want to figure out what those bounded contexts are because you generally you want to split
along at least bounded contexts if not uh subdomains and if you're not sure what those bounded contexts and subdomains
are that's your first task you can't figure out what the good lines to split things across until you figure that out and
that's not always easy and that's why we have all sorts of techniques like event storming event modeling um and various
other techniques which mostly involve getting everybody in the room virtual or or physical to talk about what are all
these things that we we need this thing to do and of course preferably you do that before you embark on creating the
system but if the system's already there that's fine too you figure out what should the boundaries be because it's all
all about boundaries it's all about what are the boundaries how big are the things and are they too big should we split
them or are they too small to granular we've got 200 microservices when we don't need 200 let's pull some of those back
together as some companies have done and say let's let's just end up with five instead of 200 uh so you have to find the
sort of the right level of of granularity for for those boundaries but you gotta you got to figure that out you can't
just look at it from a you know or you can't just pick something up and and say oh we we'll you know cut along these
lines you have to really spend time to figure out what those bounded contexts all right back to code yes sure on about
code we were still in jira oh right we weren't even in code all right let's switch there uh so I think the is so is the
next thing uh yes that's the that's that's the next thing so there are two parts what um we have to figure out how to
get what was typed uh sent across on the get request right so if you look at the HTML maybe scroll up a bit to bring
that in view yeah so we've got a text input um does it send I don't even know what it sends uh do we want to bring up
maybe move that to the to the top and let's bring up the actual Searcher that responds to that endpoint yeah do with um
like does it handle get I mean request parameters I imagine it must yeah so let's me look at the docs um do you want to
this so so we're doing a get request which I think is fine we're doing basically a that's installing I don't want
installing I want triggers uh so form is triggered everything triggered DeLay So this is so basically this is what we're
doing we're basically only issuing a Crest if it changes we've got our delay um and uh so do we have the changes thing
implemented again can you go scroll back up to that yeah we' got that input change right um do not see it oh no there it
is I see it I found it it's within the trigger yes so so the trigger is is multiple pieces it's got the input so that's
saying when the input changed um basically trigger but Del lay don't do it more than than every or basically do it every
500 milliseconds to look for for changes yeah got uh are we back to your screen so I can switch back yeah okay I
basically use tle to to view your screen um so these are trigger modifiers trigger filters we don't care retr filters uh
request indicators we don't care about request indicators what we want to know is what made um that's a single page what
about request what a smart idea so htx respects responses to be HTML um it doesn't really tell us anything no it doesn't
really doesn't talk about request prms huh was that the only hit for request so here is the request so let's see so
here's what happens request this is this is exactly the place of an example as as mer would say an example would be
useful right about now um so values are gathered so my assumption is based on uh this and a little bit of of guessing
about or assuming about how it works is that whatever is currently in the input field will be sent as a query parameter
um I think what we can do is experiment yeah we could test that right uh by adding um just looking to see if there's
anything else yeah there's nothing nothing else here um unless there's something in examples that example it doesn't
post but that's uh yeah we need to see those what's what's happening on on the server side like we know that that's
going to happen I'm assuming based on what this is doing whatever since this input field this is pretty much what we're
doing that there'll be a a request parameter so I think um let me switch back to your screen we can basically start
start coding up a little bit of an side so what we can do is uh on the autocomplete themes method at the bottom uh what
we can add as a parameter is uh an HTT TP chain signature no no no just just start typing HTTP yeah but uh it's going to
be some class name so it's probably going to be servlet uh so it's going to be lowercase seret request uh yes because we
just want to see the seret requests we don't care about the response you can hit Tab and we can eras the rest yeah I
would say we just do that because what we want to do is basically want to sort of dump the request and and examine it um
I don't know if we want to do that in statement I don't have a preference uh uh let's let's do let's use a debugger so
this is these are the times when I'm like what the heck is going on underneath with the framework or the library and I
don't understand it and so that's like when I go into debugger it's 95% of the time because it's something not my code
that I don't matter uh so let's put a breakpoint on this like get so crowded over here uh but that's not L3 oh true
there you go there you go and uh let's stop the current running and then hit the little bug icon to run the the did or
did it no it's no it didn't break yet didn't break yet okay so type yeah okay so now let's uh let's open up the and what
we want uh might have to do some some tricky stuff here um under this yeah so let's uh or which this the this dollar
sign zero or the higher level this so what what I usually do at this point is I start doing uh request dot uh get so
let's get um options uh body that's a request to get prams get parameter get parameter map let's see what that looks
like so there's something in the parameter map there it is theme query and there's the B so U my my suspicion was
correct that basically it submits the input field which we named as we can see on line 15 on the top we named it theme-
query uh and since the input type is text basically submitted as if we had done a submit on a form that contained that
after we typed the letter B so that's perfect so now what we can do is we can uh we can stop we can get out of debugger
we've we've discovered and and out and uh what we can do is um let's uh before we forget let's turn off the the
breakpoint and uh now we can actually put a query parameter here request parameter so replace that argument with uh
request brm yeah replace the and so uh yeah the value is is basically the name of our yeah um do we do required or
default uh required I think we'll leave because it's always going to be there um but we should do a default value of an
empty sure and now you now we need to actually string and we can call theme query that's fine we're eventually gonna
need we're eventually gonna need the model so you may as well leave that in there okay yeah so that's that's all we need
to Define you know sort of to put down in code what we think it's going to be and now we need to switch gears and start
test driving it if we wanted to we could return what you type just to prove that that that's what's happening uh that
might be a useful experiment what I just typed you mean this part yeah so instead of so instead of in addition to
returning that hard-coded stuff we want to return the theme query that came in so we can see but you probably want to
put it put some yeah what do you think just a paragraph back now this is where you're saying no no you'll have to you'll
have to either do string concatenation or do a string format so replace theme cury with a format yeah exactly that is it
formatted or yeah it's formatted yeah but I got that wrong what's up about that why is it thinking get that no got that
right it did yeah oh because it's this one right right right right yeah yeah yeah yeah because that's the variable right
uh so let's run it and see we should basically see our search echoed back to that for those of you watching that is a
predict even though we're we're not writing automated tests it was it's what we're daely doing is we wrote is we have a
prediction of how something is going to work and if that prediction succeeds then we know that we're on the right track
and confirms what we want to do type the letter H excellent so it's triggering every half second and it's sending
whatever you've typed so far uh and so we know we're receiving that we know that's that's what we need so now we we we
uh we're done with our experiment and so now we can say okay we've got the HTML HTM X we've understood how it's going to
talk to our our what what kind of HTP request is going to send and now we can uh uh uh yes we can now move to the next
the next step so now we're gonna have to right now we're just sending back what the user is typing but what we want is
to query the repository MH for which themes do you have this start with what's been right so would this be a theme
finder test that's kind of tied in or is it more Searcher test or even farther out well we want to we don't we're not
creating a new endpoint so we don't need to create a new MVC task because the endpoint already exists um so then we test
still going to work since we added parameters to it uh well right now it won't break at some point it might not work I
don't know that we have much of a test other than I mean we could look if we have a test it's probably only that it
returns response it's that one yeah so it's basically does the endpoint exist we don't have uh the request parameters
required so doesn't matter right um we could add it on basically just just to to make sure that it doesn't doesn't fail
in the future uh in case we do model require it um that might be the modify at that point in time or now right now let's
just do it so this is the the outermost test so let's just modify this test to to send along uh the the query string the
perform on this one on 41 so um yeah so just like we did on 30 line 35 we're here now this would be theme query theme-
query because that's the request parameter yeah and it likes pants that's hilarious that's really funny uh make
something different actually what's pants is fine I don't care okay I pass since it's MVC I'm just running yep excellent
we're all good uh so let's do a commit since we change stuff and we still have Test passing yep I noticed we're we're a
bit inconsistent in how we named our request parameters ah should I do we fix that before we commit yeah I think I'd
like to fix that so on 29 we have a hyphen separating it uh on 34 we've got the Pascal case request parameters are
normally Kebab case ever uh are they always I think it depends um yeah I think we have to decide what what what we want
I I I think I tend to to go with Kebab case so rename this one yeah now well this this because it's string refactoring
won't necessarily catch it all right I would probably do a global a global search uh a global search and replace for
that oh but not all the yeah not all of these are gonna yeah yeah uh I would basically look so the other approach is we
could just change this one and see what breaks yeah I'm not 100% sure that that's going to catch it because we do not
have UI HTML tests um so what we can do is is search for that there not that that many occurrences of it and just uh so
for example we can pretty quickly go to um the HTML one which is this one and fix that uh and then anywhere else it
appears it's going to appear as part of a string so the only other two places that actually matter are are basically
this one and this one so we can change our test then have it have the test fail and then change the yeah okay so let's
now in this case we just want to run this passed uh mainly because uh at this level we're not actually forced to to
basically because it's required is false there's no reason for to to to do anything so should we create a failing test
and then rename it I don't feel like I don't feel like we need to do that I just wanted to start with a test and and
then we fix that yeah okay that covers everything now yeah so let's um let's run uh even though it shouldn't matter let'
s run um I don't know we need to run all the tests let's run the io free because we ran the MVC ones and those are fine
I only ran one MVC this particular one yeah that and that's the only one that tests against that endpoint so that's fine
gotcha yeah we're all passed all commit good uh I would add a statement of of aligned n uh uh naming now I want kebabs
for lunch man a good Kebab my favorite Kebab place closed down a year ago oh no I'm still sad about it all right so we
have our MVC tests doing what they need to do with they're passing and so now we can drop down uh a layer into our
controller test that tests the song theme Searcher directly um one yep uh do we have a test that tests against that
endpoint Auto on against autocomplete themes I do not know let's see no usage found all right good then let's write a
new test okay and that's a good place for it it what do we want to name this um the goal right do we want this to go all
the way to the repository or to a test double or is it uh too early for that conversation it's gonna have to go to
something um and will have to be a test double because otherwise we'll have no way of well it doesn't have to be a test
double but that will be the most efficient way to do it right um I don't I don't know what test dou we uh yeah I guess
it's a little bit of a tangent so as far as the goal of this test so what's nice about this test is it returns a string
with the exact content that we that we could then inspect right so if we say that you know we've sent in h um and we
expect it to be one paragraph of containing Halloween then want I'm just trying to think of how to test with request and
we don't need to talk about sub substring in the sense of as long as it matches we're good then yeah I mean I was
thinking do we want to put autocomplete in the test method name or do we want to create uh a nested autocomplete well it
certainly make this test name because that test name will get long if we don't put it in the Ed in true I mean I guess
my inclination is not to go to the class until we've got multiple tests that that was my thinking as well because I'm
not sure how I don't think we're going to need all that many so I would I basically prepend it uh yeah we could steal
this sure actually we need the yeah we've already got the model in the so we need to create a model because we added it
to the request actually we don't need the model I don't know what I was thinking oh I know what I was thinking but we
don't need the bottle so we can take it out of there yeah we can take it out of there so the reason we don't the model
is we're not returning something that will get combined with a template we're just directly what the you're the the code
Code full line code completed want still wanted to put the model in there and I'm fine well you want to hold on to the
you no it's not how it is actually what it is um could be autocom completed themes the last option I like how put that
in the past yeah H like it okay so assert that autocomp completed themes contains this will be here it's this is gonna
be is exactly is equal right this is a string and we're saying that it's I think you want to string around that no
control shift enter control shift enter why did I think it was J or all Shi J's for combining lines the the enter one is
basically complete control shift enter yeah yeah completing complete complete the statement um so now theoretically that
should work oh because we're returning no it shouldn't work it it won't work yet but I mean it it it could sorry I didn'
t mean should I meant could work um because we have uh the song themes controller can we see the what what creates song
themes controll is doing the one that that calls what is that doing so it creates the the null song Service uh and then
does an add song uh oh it passes in a stub theme finder what does the sub what does the ah uh I think we probably want
to make that programmable um because right now it's not obvious what what stubbed values it's going to return right can
we take a break first I was about to say let's take a break and then we'll we'll do that sounds good all right see you
after the coffee break folks he hey folks so uh as I've been talking about on stream uh I run a book club and we just
decided on our next book for the book club which is going to be Martin Fowler's Infamous refactoring book uh Second
Edition so I've read the first edition um very long time ago basically pretty much not long after it came out I've not
really read the second edition in in depth so I'm actually looking forward to this and uh our first session will be uh
in less than two weeks so um you can go to uh the website to find out uh and get links to uh the Discord so basically
we're going to use the Discord again to coordinate the book club no charge all you got to do is send me a direct message
with your full name so I know you're a real person and uh this page has all the information so you can go look at that
that's this link so T.D book-club Kebab case there and uh has the schedule for the first session what we're going to be
reading um which is basically pretty much the first 20 or so Pages uh and we'll talk about that um the second edition
uses JavaScript uh but what probably I and perhaps others will do is provide uh Java or other language implementations
of what Martin shows in in the book so join us for that it's always uh good discussions and right rock and roll so let's
get back to go uh so we wanted to make our stub theme finder programmable so let's do that what do you in what way are
you thinking like um through Constructor parameters yeah I think so who's using it right now just that one test or that
oh that one helper within that test right so what do you think introduce parameter um so let's see we probably yeah so
let's yeah so let's field um what do we want people to pass in I think we do we want them to pass a list that's kind of
annoying let's let's do VAR yeah so uh we can make that list a field but I think we'll make the Constructor uh vars now
varargs of themes correct not of songs right right um but let's make that a field first yeah is it f for field f for
field is that right yeah yes uh except uh when you extracted it uh we want to uh I don't know if it let us yeah we'd
like to initialize it in the Constructor if possible I don't know if that was an option I forget I don't well let me do
undo we'll try it again I don't remember seeing that as an option oh it is OB yeah so the the the non-modal is it's not
as obvious yeah yeah and then the name we want to be themes I'm disappointed that it didn't suggest that like as a
default it's in the method name Why didn't it apply that I don't know okay so that's uh did you want to run the test
just to be sure yeah I did okay but you were talking mid sentence I I saw you poking around up there so it's like oh
well I turned the um it did break uh well the test that we're currently writing is broken uh which is unsurprising yeah
yeah because because it yet uh so let's let's go to where we were the St theme finder and let's push out those as
variables um can we uh what would be nice is if we took both of those and extracted both of those can we extract that
well let us extract that to a variable no no um because what I want is I want to extract it to an array variable because
then it'll be easier to to move to the VAR args right so let's do that uh we'll have to do that as a manual refactoring
oh my God okay so would we do it by just creating an array so we don't uh so we want a string array yeah so string or
when you say string array do you mean that array not an array list ah because what we want is we want the parameter the
parameter for um no no old oh like that no no remember I didn't do old school Java I'm new Java uh so it's string open
open Square Brack oh oh I said I was saying in Old School really old school okay yeah got array and then we can do uh
the curly brace for the yeah for the and then you and then we want themes to be uh I think we can say arrays. of I don't
think we can pass in a theme array here I think we have to say arrays. of so we don't want list of think could also see
if Auto uh so delete the semicolon because I might get there it is raise as list right that's what we want so this is
this is so this is um what I talk about a lot in in this idea of composite refactorings right so our our our larger goal
is we'd like to make this Constructor be VAR ARS we could have just gone right there um created the VAR ARs and then
have to figure out oh wait how do we take vogs and turn that into a list but we're taking smaller steps um and so this
should still be the same result the one test failing but this will help us verify that otherwise we did the conversion
of a string array into a list correctly correctly right and so now what we can do is we can like that yep whoa oh it
went out to the collar right so that just still work right because that was automated y while that's running we go look
at the test see how it change the collar yeah so we'll want to get rid of having to pass it as a string array so back in
the stub uh theme finder uh change the dots that's exactly equivalent because underneath all right and now we can go to
the caller and they don't need the new string anymore in fact intellig suggesting that you can just have intellig do the
right thing if you do um Alt Enter remove explicit creation yeah so got rid of the new and got rid of the curly braces
and now it's just vogs and that should still work yeah or work in the same way yep and now preparation is now ready for
this to accept themes coming in such that they so now this test currently it's hard-coded for hallowe in New Year right
which uh is probably um like we actually want a version where uh we specify the themes directly and we don't care about
songs right and I'm actually so the songs are added to I see the songs right to the service right but what's interesting
is we're not looking at those songs themes right yes we're using this sub theme finder interesting right which perhaps
is not correct yeah so should we make a new helper that just does what we want yes want to refactor this towards it uh
well this one this one's still this one's being used for other purposes so what I would want to do is have one that's
dedicated to creating the song themes controller with a list of themes as opposed to a list of extract this method into
a method that would be the I'd probably do a copy instead of an extract ah because we we want what this method does we
just don't want line 92 basically right but we don't want but we want to leave this one alone that's why okay so now VAR
ARS are not if this is themes VAR ARS is that still the same signature yes yes it's not like lists where in Java it can'
t tell the a list strs because arrays it arrays are types that are not we don't lose the those types yeah got it okay so
then we don't need this correct okay so now we go back to the test that's using the vers is that calling the method we
just created wait a second yeah yeah yeah what's up with that no yeah so who's calling this method because they're doing
it they're they're may be doing it in a way that we don't to Auto that's the that's the one so this is testing the um
that one could use the new method too so whatever so the the so we basically need to not use that method because we don'
t need to either should we put that deprecated on this to help us uh no I would basically delegate it to the new method
we just created and then we can just inline it ah under no it's in the same place was it in the same file yeah ah it's
just is that right looks right to me let's try it so everything but the one oh something else broke ah one ah I was I
was thinking that that was gonna happen um so let's go to our sub theme finder uh and make sure that when it says all
unique themes alphabetically that's actually sorted right because we what was it we're saying we're saying that theme
finder that's his job is that when it Returns the themes they are they are sorted so let's right see we had list up
right got it now we can emulate that behavior and this is this is sort of one of the downsides of or one of the
potential dangers of of mock or stubs is that you don't prop properly fake the behavior and so you get into into sort um
but we'll actually need to do that on the line before because it ah yep get rid of that extra space so now that should
fix the broken test but the other one's still broken yeah it should fix the the model model yeah model excellent cool so
then actually I shouldn't have closed that so then the remaining one is this one which is broken right but let's do
commit because we we we made some modifications and improvements to the stub commit all of it or just the improvements
to no let's commit all of it because we did improvements both on the stub and on the the Searcher test yeah but we also
did create the new Searcher test that's fine okay I mean not gonna try to chunky it I don't think that's worth it right
yeah hey D attitude hey went through that invent storming exercise yeah chat GPT I find those the the llms to be useful
sort of for for brainstorming some of the things when you're trying to figure out um you know especially if you don't
have a real subject matter expert like I was saying earlier if you have a learning project uh sometimes you can uh
brainstorm and bounce things off of chat GPT and I find useful oh vacation nice hey there tkes um no we're not going to
make estimates released it's especially harder like if we were working a regular number of hours a week we might be able
to provide some range um but since even the amount of time we spend on it is pseudo random um there like for example the
first hour we spent a lot of time talking about things that have nothing to do with this app well there's that and there
but there's also like you know are we going to stream one day with this week three days this week we have no idea um so
uh it'll be you'll it'll be ready when when it's ready yeah is it done yet yeah that's a fine question is it done yet um
when is it going to be done is is a different question that that I'm not gonna answer are we there yet are we there yeah
exactly are we there yet okay you you can come on every stream and ask are you there yet um and that question we'll
answer you can also always hit Refresh on the live website um through and see if anything happens that's useful if it
doesn't say coming soon right then you my streamyard there you are okay uh what thing do we do we care about that that
test got added or not till it's yeah okay I'm proba one I find I don't think terribly hard about my commit messages
because at least in a non-team environment I almost never look at I don't really yeah I don't really look at them and if
I do it's usually good enough or I can just look at the diffs pretty easily so all right we want to get this failing
pass so we're creating a controller with things I'm going to look at the path yeah we calling and we wanted to inline
that because that was a useless delegation the uh I like the with themes to be yeah it should because it's only used
yeah yeah so it did keep it so now we don't to the other benefit is we don't need to worry about the um the fact the
overloading of names one which take songs which now then begs the question yeah should we make this one with songs no
because I think they're because so the reason why I like with themes is because the types are just string right here the
type is song song so it's obvious so it's this is not VAR args so the sub theme finder is VAR args the incoming thing to
this method is not VAR ARS uh we could because uh we could just make it VAR ARS it would be really easy to do yeah so if
we just did I wonder will it you suggest will it suggest Enter no it won't that's a bummer oh well so yeah so you can
just doing NOP okay I'm just seeing if if it right I presume like that will work okay so now if we rerun this the one
test using this is the broken test so it should break but should break in the same way yep okay all right oh it's used
in two places right was that model tests that oh right failed for a minute and now it's and then our new test okay so
back to the new test we're autocomplete returns with expecting with those two Halloween so that means this change right
right now it's just returning what it's getting right back yeah so so there's no so for so I think there's no need to to
do a a constant return because we know we're gonna have to look in something to to get that because we already have sort
of a constant return value so I think we can now jump to well where do how do we do how do we do that how do we search
ask so this is the so who has the information about various ways to search for themes looks like Searcher no well oh uh
sorry back to because that's the song Searcher yeah yeah I went circular logic um it's the theme Finder right because
the theme finder is all about finding themes oh right right now finder and we're not using the theme finder yet so we'd
like to use the theme finder since it's all about finding themes it may not have the exact method we want so it had the
method where it's like hey we want to create a drop down give me everything but now we want to do a more sophisticated
search which is the theme finder we'd like to find find themes starting with right so that means we need to add to the
interface probably we don't know that 100% for sure right yet so where where what code do we what code is currently
hardcoded that we need to that's the end point yeah the this one here right so this will have to use the Finder right
and so here's where we Define what method would would we like theme finder to have that would make our lives easy of
starts with something like that yeah not sure I like the name but you can start with starts with right we gotta start
somewhere so we can start popping into a VAR oh it won't tell us what the VAR is because it doesn't know it's a string
yet yeah well so you'll have to do that manually yeah I know it's terrible well so are we so what are we expecting a
list of themes probably list subset it could be zero than one right it could be zero it could be one it could be many so
that that usually to me list I'm mixed about the ter the variable name themes what were we gonna say yeah I was gonna
say I I I think that's too General we I think we can say a little bit more about what those themes are um my first
thought was this which I don't like found themes um filtered I like uh matching ah matching that's even better welcome
uh is vertex worth looking into needs you you should have known I was going to respond to that question with the
question so let's create starts with let's create it yep what oh yeah there we go now that's creating it in the
interface it automatically created it there that's fine we'll we'll end up with some compile broken so here yeah so we
need to figure um what do we what do we want uh so let's implement the method I think control o will do it sufficient so
we've got the themes we them well is there any other place that's not um so we want this to take the themes in the field
right and filter them or reduce them down to yeah and so here probably are um we could do that we could just say return
themes not list of themes themes is already a list right and so this will certainly break because it'll be we'll be
returning too anyway but now I have a different failing message oh interesting right so we did that and I wanted to do
that because we now need to at least format the themes that we get query so if you look at the implementation we're not
paying attention to the themes we found implementation of which of of the controller right because we're we're finding
the matching themes we're just ignoring it so we need to now format it properly right this is what you mean yes wait a
second that's going to stuff all if there's more than one it's GNA stuff all of them between p and p well right now our
test is only asking for one true so we'll see what happens it probably will closer yep oh interesting so not quite what
we want right right right correctly you mean here on 29 yeah we're gonna need to throw that away and and different so
what we want to do is we'll want to do a a stream and then map and then the map will actually do the do the formatting
for Joiner actually let's let's try string Joiner so I don't think we need to necessarily do map because we've already
it's already it's already as a class so what it says at least yeah I'll do that but then we want to just replace this
with so string Joiner takes takes multiple arguments what so what do we want we want um when we concatenate the strings
we want uh a a prefix of the opening paragraph tag suffix of the closing paragraph tag uh and then maybe a new line
separating each one right so it takes three three arguments so the limiter the things that separate each item uh the
prefix what to put before each item and then the suffix what to put after okay so it' be like this but the thing that
I'm let me get first so like that right no okay because we don't want P Halloween P comma P New Year's P comma we don't
want that oh we want the separator to be a new line oh that's a gotcha and now we need to actually use the joyer right
and we got to figure out how to get rid of the the square brackets no we don't we don't okay no so Joiner what do we got
so we could do using the the ad um but since we've already got a list this is actually not going to be the the way we
want so we actually are going to need to to use a stream just to to collect things so that we can iterate over it so if
we do matching themes uh do. stream. collect so get rid of Joiner we're actually not going to use Joiner but that helped
us figure out what we need the Joiner to be lowercase oh so I want to do a get a stream on that and then we want to
collect and we are going to do joining and it's basically going to parameters and that returns a string so that's
basically what we're going to return I don't know that you necessarily need to VAR it up at all just direct return oh
return sweet get rid of this that yep get rid of that yep now let's try it so now I expect it to be broken but uh that's
actually not the way I expected it uh I think I think I conf I think I confused the suffix and the and the delimiter so
our delimiter uh is actually not a new line it's actually a open I think that's what we want close new line so close the
paragraph tag New Line open a new paragraph tag because the prefix and suffix are for the entire thing not per item
which of do you want me to say again what I frozen so while waiting for Mike to come back um yep we lost mik uh so
vertex is known for high performing like if you really really need very high performance uh servers um and it's all
about sort of reactive um I think kind of stuff uh it is it does have its place um and so it really depends on on what
you want but unless you have a specific need that around performance that vertex could B yeah not looking into good into
new Frameworks is is a good idea unless unless there's something need uh G to check in with mic see what's uh we seem to
have lost connection because uh let's see if I can bring him check uh so me to Let's since we're almost at another break
anyway let's take a break nature let me take a break and then then all right so while uh while we're trying to so Mike's
internet did go out um so while we're trying to figure out how to that's not much I can do um not sure how much he can
do uh but I can talk about um so Astra was there something specific you had in terms of fractal nature that's very
interesting statement and not not quite sure what that would be um but I thought it might be useful to take another look
at the um at the architecture of what we're we're building and what and sort of where we are and and and sort of how I'm
mentally tracking what kinds of tests we're we're writing and sort of what the test is actually testing against um so uh
so let's let's grab this and we'll grab that let's duplicate that and move it and I'm G to have to Center that because
that's the way I is basically what I what I've been now calling um hex so it's hexagonal plus domain driven design uh
and the reason why I no longer call it just hexagonal on its own because hexagonal and alist Cobra and the inventor of
it has made it very clear um that he is uh agnostic to what you put inside the hexagon in terms of do you split it into
application and domain layers or is it just one big application code um and so uh so there's basically I I use the the
domain driven part and two layers um and this is what clean architecture gets at I just don't uh I think clean AR
architecture and I've said this before clean architecture and onion and hexagonal they're all separation of concerns
architectures um I just don't like the diagrams that that that clean gives you because it to me I think the separation
or or split uh and Clarity around what happens on this end uh and sort of what happens over here um I think in terms of
inbound outbound are triggering uh and and responding um I think is actually really nice to have that that that symmetry
or a actually a symmetry um and that the left side here is very much these are triggering events that cause the
application to do something and that these then are requests or notifying uh either notifying or fetching information
from an external service for so it can get its job done and that everything inside of here is your domain and it has
absolutely no knowledge of what's going on or that even the outside world exists and I think uh but it's really this
this asymmetry that that I really like from uh you don't get these diagrams um what what's I'm curious what what you're
what you're not getting um so let me uh get rid of now and so what we just started working on is um and we started with
with the outside right so we had uh we can stick browser oops really it's it's the HTM X part of the browser the
JavaScript that's running in the browser that's going to do it right so it basically uh is out here and it makes a
request then and it hits our adapter or triggering adapter depending and so this adapter this is our song theme Searcher
right so the endpoint that they're hitting is basically the um the theme query that what the endpoint was that was the
parameter I think it was I forget what the the name was it's basically them query the browser sends the request to um
and uh then this is the code that's going to do right that's the mediator that's the adapter between the outside world
so we get the request we get a string and we need to basically figure out who who do we call to get that information um
and that's going to be an application use case service which in in our case is actually a port um because there's no uh
there's actually not a use case per se so use cases are almost not not always but a lot of use cases are around change
of state uh but here we're actually just searching for things and so there's no State change and so we can directly use
um a port so I'm going to grab one of these finder and so the theme finder then we have our our concrete dictionary move
this down the arrow go and so what we want then is our adapter our adapters never talk to The Domain directly here we
don't actually care about the domain they're actually isn't much of a domain involved in in the theme searching so we're
pretty much going to have uh this talk directly to uh the theme finder let me color these appropriately and so when we'
re testing there is sort of multiple layers that we can we can test against um so the MVC test was basically testing did
this work right did did we acknowledge that hitting this endpoint did the right thing um and that was our MVC test that
was really just does spring Did we tell spring the right thing does it map to to the right thing uh then um we want to
test the the controller directly and so that's a unit test so this testing here was basically a framework test right so
we're sort of testing the Leading Edge or the thing that connects to the outside world so that was our MVC test um and
actually I themes uh I think mik didn't push so I code yeah so it doesn't have a latest but um but basically we were we
were writing a test directly against this method so we had our MVC test which just which basically was testing this part
the get mapping um and now uh we're writing tests directly against this that takes a query uh and hopefully Returns the
right um so this is the MPC thing and then we've got our controller test which is IO free right so there's no spring
involved in it we can call it directly and so that's you can sort of think of it as as uh being at a layer below so here
we're sort of checking the outside edge did we configure the the mappings correctly and this test is now we're testing
the the class directly we're instantiating the class as we saw we were handing it the stub theme Finder right basically
handing in instead of well because what we want to check is when we make a request here and then it calls whatever theme
finder is in play uh that we then actually get the results back that we expect and so that's what that's what we're
doing here and what's nice about about this is we can take this same test um that's IO free and actually stub in the
real jdbc theme finder uh and it expected so uh this requires all themes to be already persisted ASD uh so when we're
using the stub it's whatever the stub reports um which is just testing right it's not testing the theme finder
capability the concrete theme finder capability it's just testing that the controller here is actually calling the theme
finder and formatting the results so here what we're checking here is one finder and two that it formatted the HTML as
desired now could split out the formatting of the HTML we could extract that and put that in a separate class and that
is what we would probably want point oh hey suige yes we lost Mike his internet went down um surprising that it's still
down give me a few more minutes if not then we'll right so this is uh let's do that so those are basically the two
things that this test is testing and the fact that it's testing both of those is actually a little concerning um because
we want to we want our test to really try to test only one thing at at a time um and so this is actually testing a bit
more uh than than I would like but it's a place to start um really the main thing we want is that it got themes from the
theme theme Finder right that everything is wired up correctly that it calls the right method on the theme finder and
that we get what what we expect the formatting the results as HTML right tacking on the paragraph uh elements um that's
really separate and that we I generally pull out into into separate code that's then directly testable given these
themes I expect this HTML right so again sort of breaking things down into pieces uh so let's see when there are themes
that are not yet pers persisted I'm not I'm not quite understanding that that scenario so when during typical operation
when songs are added right because you don't add we don't actually add themes we add songs um concurrent us so if you're
talking about M users trying to search um still not understanding what they wouldn't find so if the songs aren't in
there and the songs have themes themes until we persist those they wouldn't be found but once we um once we persist them
then they're found because remember the theme finder is not a database it's not its own thing right so if we look at
this diagram it it like our jdbc theme finder is actually there's no separate database for this it's going directly I'll
what shape can I use h no database shape all right I'll pick that so this database is used both by the jdbc theme finder
as well as the song Finder right because there's one table so you can't add themes without adding songs so it's always
you're adding songs to the database that have themes and then we just find the unique themes for database I'm not seeing
no when you add songs they get written to the database so that's not this this part of the hexagon this view of the
hexagon is just showing the theme finder for songs right we basically import the database so if I add songs that have
new themes when they get persisted you'll be able to find those themes and you will be songs if I don't persist them
they don't exist right because there's there's no point where they exist in the inner hexagon right in memory and do not
exist in the database the way because you have to import them and the only way you import them is you import them and
then we pretty much immediately write it out to the database so I feel like this something I'm I'm not getting from a
scenario you're you're proposing there is no there is no point in time where where songs exist in here in terms of
production code there's no there's no point at which songs exist here and don't exist in the database they must be in
the database otherwise we couldn't have loaded them into memory so if they're in the database then when we do the theme
search um we will find those themes because we're router so because now this is not this is to a certain extent you
could say this is cqrs right because we're basically you've got um sort of a use cases where we're adding songs so we're
importing the songs and we're writing to the database and then there's a separate view a read view of of just the themes
but it's still looking at the same database so we don't have to worry about consistency between sort of two tables or
even two databases um it's all one one database we could optimize like every time you insert it all also updates a
separate themes thing but right now we're not we're not doing that we're we're searching uh and collecting all themes
from all rows which you know if we had a million songs then that might be something we' we'd look at optimizing but for
a few thousand songs is not something we probably need to optimize now from a test standpoint um we're stubbing out the
theme finder which means we're having to configure it to to act correctly and as I was talking about earlier this can be
a little bit dangerous because what if the concrete implementation does things in a way that's different from how you
programmed the stub to work and that's where uh and that's why I like running this controller test IO basically IO free
against a stud but also uh IO dependent against the real thing to make sure that the real thing is working uh that my
code is expecting the works and this is where um uh you know you want you might want to think think about is is this
stub the you know what are we using this stub for um and I see similar problems Much More Much More prevalent in uh in
code that uses a lot of uh makito mocks with the when this then return this other thing um you're bypassing a whole
bunch of code that may actually be doing different Behavior than what you're programming it to return um I think with
stubs it's it it can be a similar problem and you just uh it's not an assumption it's the way it works we persist songs
and you can't find songs unless they are persisted and you can't find themes unless those themes are for songs that have
been persisted there's no way that songs and themes get out of sync because we are searching for themes based on the
songs if there was an implementation that modified State around songs in memory not yet persisted I don't want to find
those either because those are a separate transaction so if for example we did need to do some manipulation when we do
the import and that for some reason took a non-trivial amount of time that's fine when I'm doing a search I'm not going
to see the stuff that was in memory because that's somebody else's trans action let's say there's a review in progress
and and we have to wait that's fine I don't want to find those because those are in a separate transaction um but theme
finder will always find themes that have been transactionally completed so yes it's true if we had an implementation
where songs in memory had you know there were songs and themes in memory that were not persisted I absolutely do not
want to find those because they're not done yet the minute they're done and done meaning they're written to the database
then you'll be them so this is where it can be a little confu a little bit confusing um where we are bypassing you might
be considering that we're actually bypassing our service layer but if we're doing it for reads that's fine because
that's no different than than anything else we only need to have our our sort of use case layer use cases only get
involved when state is changing if you're not changing state right and a search by definition is not changing State uh
you don't need a use case Handler if you are changing State like I am modifying I'm fixing repairing uh this thing why
am I not be able to make this yeah right so for saying oh I need to um before the songs can be officially published I
need to approve them and they're in memory and I'm working on them um then that must go through the use case but the
idea of Aggregates comes into play in that what I'm modifying while I'm modifying it should not be seen by anybody else
right I want transactions so yes in this for this data it must state must always be persisted um that's very different
from certain kinds of transient uh types of things so for example in ensembl I have my Ensemble timer that's not
persisted anywhere um but then there's only one and so if the machine crashes oh well it's not a big deal uh but the the
way this the way this system works um and the way any system works is if there are State changes at least if you're
doing this architecture if there are State changes state changes must go through a use case because it's the thing
that's going to load stuff into memory right to basically load stuff into here call methods on that and now this state
changes and so it's going to have to then persist it back out otherwise nobody else can see it memory this area is
transient this area only exists while you're executing case um I can't think of a case where song themes would not want
to if we imported songs I I want people to find them um there may be a case where I have to approve songs before they're
available right so we do have uh that functionality in in our in our in our backlog as it were where contributors can
contribute songs but they're not published yet um but we have to still persist them somewhere they're just not persisted
in the searchable database so it'll be a separate table for proposed well not sure why why you're unhappy what in I'm
having trouble coming up with with with there's some aspect of what what you're what you're driving at that I'm that I'm
not getting I'm sorry and I know the asynchronous nature of sorry not asynchronous the the uh asymmetric nature of of
this stream and frustrating but use cases are all about State change if you're not changing State you don't need to go
through the use cases right you look at any use case definition and it's all about the customer the user wanting to
change something they're wanting some state to change and we must persist State otherwise it's not state state means it
has to remember it if if we forget about it then it's not state or at least it's so uh so it looks like um there's a
problem with Mike's um router uh so we're going to call it for today and we'll pick it up next time um so thanks for
hanging out uh and AST maybe we'll we'll get on a a zoom and you'll you'll explain more your your uh what what you're
thinking of because page all right uh well thank you everyone sorry about uh the glitch that's computers for you um so
uh I will do be doing a solo stream either tomorrow or Thursday probably not both uh I will try not to delete my in the
future honestly it wasn't my fault I blame blame the router company um and so uh we'll pick it up from here next time
and um that's it so thanks thanks for hanging out and uh we will will see you next time um as always join the Discord if
you'd like to know uh about future upcoming streams um don't forget we've got our book club check it out go to ted.
book-club and uh and join in for for that has all the information you need uh if you're in the book club go get the book
um and read it uh and we'll talk about it on on the 23rd and uh what else oh tdd game yes uh game um so the the solo
streams that I'm doing are basically taking this TD tdd here um and and putting it online so if you go to td. cards you
can look there's a video here um this video basically I walk through the same process of of doing test d development
that we've been doing on stream here and that I do on my solo stream we do in the game and uh basically the the video
talks about the process and then then walks through the game a bit um you if you buy the game you will um get early
access to the online version so not everybody's in the same physical location so it's not easy to play a physical game
remotely although you can I do it uh but but it's a lot easier if if it's online uh and that's what I'm working on on my
solo stream and so if you buy the game you will get early access to the the online version um and uh I still have a few
copies left in stock so um go ahead and buy them before before I run today hey Jenice sorry you joined us just as we're
ending we lost mik due to a router malfunction on his part um so we're gonna have to end here um join the Discord check
out the tdd game join the book club uh and stay tuned uh for uh schedule information about the the upcoming streams and
I will see you later have a great rest of your day whatever day is left for you and I'll
