# TDD & Hexagonal Architecture Exercise： Supermarket Checkout Pricer - Part 5

**Video URL:** https://www.youtube.com/watch?v=9gQ1CoJdJf4

---

## Transcript

all right hello folks it is wednesday although for some reason it feels like thursday or friday but it's only wednesday
so still two more days in the week whether that's a good thing for you or not i'm not sure um for me it's not because
i'm running out of time to do stuff this week um but that's okay hey dude tattooed uh so yesterday i didn't stream
because i wanted to watch the all-star game i usually don't watch the baseball all-star game um but i was really
interested this year uh it's actually been quite a few years since i've watched it um and i they did uh they had sort of
uh some of the players miked up so you could hear them they could talk and the announcers could talk to them that was
kind of cool um but of course the my league which is the national league because that's where my the two teams that i
follow uh san francisco giants and new york mets um their national league and so i only care about the national league
winning but once again for the ninth year in a row uh the american league won so not sure what that says not very much
the only one by three to two uh it was really nice to see a lot of the the pitching it was just such good pitching which
worries me as a mets fan because there's such good pitching but anyway um what are we doing on the stream today uh hey
yadav it must be really early for you in the morning i'm guessing uh so today um yeah isd yeah i figured your isd that's
what it's i don't want to think about what time it is um so uh part five i guess the continuing saga of the supermarket
price checkout pricer um again sort of the background on this is uh i took what is normally sort of an exercise to do
some uh for people to do tdd and i highly recommend using this one i really i i like it i think any exercise that you do
um and then start over and do again tic-tac-toe is still a good option i will do tic-tac-toe one of these days on the
stream uh just to show how i might do it um anyway so i built the supermarket checkout pricer uh and we've already
started formulating it according to hexagonal architecture so all test driven and now we're basically um fleshing out
the the core functionality which is just this cart that is able to produce a receipt as well as uh total so all that uh
is in cart there's still a bunch of refactoring to most of this stuff but we'll we'll get back to that at some point
right now what i want to do where is it we've got our inbound adapter which is our product scanner controller and it
basically expects a upc um then it redirects to an error page which currently doesn't exist i'll we'll create that but
sort of the you know the most minimal front-end input adapter that we can get it's all it's basically an api so you do a
post and the currently get uh sorry so this is the this is the web ui adapting adapter the rest controllers on on the
surfaces that we need so uh taking a high level view of what we're doing is is this so we've got um our product scanner
right we're simulating that uh with basically a single input field that takes you know the the upc uh and then we've got
um basically our discount fetcher that will go fetch information we've got our product price fetcher eventually we'll
have our receipt display we don't currently have that but we basically got our two fetchers they're currently stubbed
that's what this little uh little ticket symbol means is that last time we left off creating those as actual real nano
services like you would not normally create these as separate services but i'm doing it just to demonstrate uh the
connections to external services so we've got everything we've got our ports we've got our tests for tests we know use
these stubs correctly and so now we want to hook them up to the real thing and so that's where we are today so let's get
to it let me open up the other services i gotta find them uh there they are it's that one okay so we've got our price uh
our price nano service so it's job is uh when we make a request and this is a rest controller so we're not uh we're
expecting another machine to call it um and the get map is basically path oriented so we're expecting the upc to be on
the path so if we as in our test here if we do a get against slash prices with 0.987 then we expect the json that gets
returned uh to be 097 for the upc and the price to be 10. and that's uh and that's our test initially when i wrote this
test last time i didn't write it as json path but i converted to json path because and i always forget how to use it and
so i created a live edit a live template for those so for example i can say uh jsonpath and it basically something like
that very easily um all right so um is that all we need well right now it's always going to return 10. that's fine for
now let's wire up the let's wire this up um check out pricer right now we've got a um i just realized the background
music wasn't playing let me uh so what we want to do is have our implementation of the port so our application port is
here so we've got our price fetcher and our discount fetcher and we're basically wanting to implement a real concrete
adapter uh and it has to implement this interface um we've got some dummies set up for our tests uh we've got a
full-fledged stub which can hold on to some things it's it's actually a bit more of a f no not not quite a fake because
it this this but it's basically a programmable stub because we can send in information and it's in its constructors and
so now but that's test code what we want is we want a real implementation of this let's let's go write one uh you'd have
what is my view on coding to interfaces um yeah so uh in terms of hexagonal um all of your outbound stuff right your
discount fetcher your product price fetcher your sending information to a printer for receipt all those are going to
have ports and all ports in the way i most people do hexagonal architectures they're they're interfaces and in java they
are java interfaces um so that's sort of creating interfaces here in this case the interfaces are for the dependency
inversion right runtime it supplies an implementation of that but at compile time i don't know what i'm i'm hooking up
to in terms of interfaces elsewhere that does depend on do i need an abstraction do i need more than two implementations
of this even if there's only one implementation in sort of production do i need to test it do i need to stub it out is
it something that is either hard to control or is it unpredictable unreliable so generally if it's talking to io i have
an interface which hexagonal sort of tells you as well right anytime i need to access anything infrastructure or
external or hardware or any kind of i o i have to go through a port so by definition there they're all interfaces do i
have interfaces in my domain possibly if they're if they are needed um so for example if i have a bunch of products but
there are specific implementations of those products uh then i might have some polymorphism and i might have an
interface more likely i'd have an abstract base class but it's possible to have it have an interface and so i always
think about is there for testing reasons or for other reasons do i need two two more implementations and do i uh and if
so then i'll then i'll extract an interface um at the service layer there's lots of interfaces uh not necessarily the
services themselves but we might inject things into the services although in hexagonal architecture those tend to be
ports um that i inject because that's all the card services is concerned about um yeah pretty pretty much that's it uh
dota 2 attitude asks is there just the single port in the service layer um just the single port there's one port per
outbound type of communication whether it's a fetcher getting information from external service or it's outputting it
and there's one port for for each uh the way i do hexagonal so there's if you look back at aleister's aleister coburn
who came up with hexagonal architecture he talks about ports also here um i don't i don't do that because to me um a lot
of people then say oh well then i need an interface there and i'm like no you don't necessarily need an interface unless
you need it for testing purposes and a lot of times you actually just you uh so between the database and the uh so for
persistence for each aggregate there may only be one database but ports especially repository ports are one per
aggregate so you may have multiple oops you may have multiple ports each one is a separate repository and you will have
different adapters but they'll all be talking to the same database um uh right so there's no por so the only ports are
basically to protect and uh allow for dependency inversion right so the application layers talk to ports and ports or
interfaces and that's the so the service never talks to the adapter directly it always talks to the port which is in a
sense talking to the adapter it just doesn't at compile time we don't know which adapter it's going to it's going to
talk to right because that's supplied at runtime so the port is an interface this is an implementation of that interface
and so that's exactly what we're going to do here is we've got this interface this is our port and we're going to
implement this with a real concrete one that's going to talk to that external service right it just calls some method
some fetcher that uh exactly yada the idea of creating interfaces just because is is actually an anti-pattern um so
often less so today i think five ten years ago i saw it a lot more maybe even five but i still see it occasionally where
you'll have an interface and then an impul why abs you have not clearly you have not defined an abstraction if you need
to attack the word impul onto the name of the implementation that's usually a message that the and this is why i don't
talk about best practices there are no best practices there are practices that tend to work in a specific context which
is what design patterns are about design patterns are not best practices they are here if you're in this situation you'
ve got this problem this is what we found works except for when it doesn't work in these cases and most people don't
read the design patterns and so they don't realize that there's actually a whole lot of writing that says and don't do
it in this situation here are the consequences some good some bad um and they often don't read the context which is like
when to use this but um so there are no best practices or just practices that uh are yeah i guess i just don't see it
anymore um maybe because the people who are hiring me have gotten past that i don't know all right so we we know what um
what the interface is and so now we can go ahead and actually implement this so let's go ahead and implement this
interface before we do that let's run our test just to make sure everything's working all right everything's working um
actually let's do a commit what did i change uh i think i just added a comment and so uh let's go ahead and implement
this we will implement this interface um external it is not an application port it is an adapter out and in this case
that all looks good and so what we want to do here is we want to do a basically a get request against that service so
when i'm implementing these concrete ones um i tend to either test it manually um or not really test it much at all if i
feel like there's not much to go wrong because writing an automated test for something like this i started when i when i
first start i don't need much from it there may be all sorts of things i need to implement but it's very difficult to to
write an automated test and i'm not always convinced it's worth it because what am i what am i really testing here am i
testing i'm going to use spring here am i testing spring's use of rest template really but i do a manual test did i like
put the parameters in the right place right that i'm sending the request that i put on the path or did i put it in a
query string that's all i care about um you can do more if like the service is harder to work with uh but in this case
i'm not going to do very much so my implementation um what i'm going to do though is is write a test but i'm going to
mark it as manual because i don't want it to run all the time because it's um it's almost a type of end-to-end test like
i'm using a real implementation of the the product price server so let's go ahead and write a test create a new test for
this that's where it'll go flip that over to the other side we'll tag it with manual so i don't basically something like
that price 4 returns 10 from external service so we're going to directly instantiate and um i always forget to change
those in the dialog because i'm so used to not having and so our expectation is we do product uh so upc's must have 12
digits so at least give a correct one we'll hold on to the response which is the price and our expectation is that price
so uh this one i'll run explicitly i normally run all my tests but this one i'll just run explicitly because i'm just
targeting this implementation and of course it fails because we're returning null uh i'm not going to do the typical tdd
thing of returning 10 here that doesn't that doesn't help us here uh what we want to start doing is and then what we
want to do is we'd like to do um i shall do a get for object because actually that's all we need right now and um what
we now what we need to create for this is we need a dto because what we're getting back remember or maybe you don't
remember so from our price service what we send back which is basically a record like this so we can actually uh we can
actually so there's our record um and but from this side actually it's still a price response because where it's the
response to our request so it's named correctly but notice that it's part of this adapter right it's in our it's on our
outbound adapter it's specific this price service not even big enough to be a micro service all right so we're going to
get for object so the first parameter here is our um our uri or url whatever uh and that's going to what do we say the
where it was that's the discount service price service we said it was going to be 8003 i forgot the end point what was
the end point so not that one so that's the url uri whatever you want our response type and so that's going to be our
price response class and then um our uri variables in this case it's just going to be the upc that'll get filled in here
and so that just should generate the yeah exactly do it attitude um just because the sender sends json doesn't mean we
will a use all of it shared libraries among microservices is really a bad generally bad unless you all right so we'll
hold on to this this and we'll return price response price now what's it complaining about uh i may reduce null pointer
yeah no it probably all right so we'll run our test now we expect it to fail because the service isn't running so let's
see what happens oh i actually forgot the http part see this is why we run the test so now uh this fails because
connection refused perfect so this fail so when doing it's not quite tdd um but we still are writing tests having a
certain expectation about how it's gonna fail and then i run the service and i should get some kind of a response um
change to price response on which end so uh on either end it shouldn't cause any problems because again it is local to
the specific adapter right if i wanted to write price response to a database then i'd have a different object i'd but it
is correct that if i change it on the server side then then it will propagate to anybody who's using it and they better
where's my application there it is yeah die depression exactly this is this is and this is why i like the code
organization structure that favors which is separate adapters for every external way to communicate and then each
adapter or the dto is local to that adapter and if you have the adapters handling multiple scenarios then well you may
want to think about are there two different adapters here or subdivide the adapter into two parts and then have dtos
that are specific to that all right so this is running on 8003 uh so that looks good logging no vlogging um what is it i
want uh logging level uh web that's what i want equals what's debug all right so now we see the reason why i turned on
the debug is i would just want to see more details um about when it starts up uh so i actually wanted different details
yeah whatever okay so we got this this is our get mapping it's on our wrist control we already tested this um because we
tested it so that's all um so now let's go back to here uh so now the service is running so we expect if it doesn't
succeed we'll gets a different kind of error but i think i and it succeeded so we see the get request um by default we'
re accepting application anything or json we got a 200 we read the price response and all is all is good so now we know
yes this is not the most bulletproof implementation but it does work we can refactor it a bit we can say well we don't
need to instantiate this every time and we can even make it final and then we can run our test again what wait a second
why did you leave this in here i think i selected the wrong thing there we go okay uh so we get for object i mean we
might want to make the rest template injectable but i'm not going to worry about that um no insert many rest template is
not obsolete it is not that is spring folks's fault for initially when they first came out with web client that said we'
re going to deprecate rest template there wasn't i don't know if it was an uproar but there was some pushback and people
said no we like rest template it works and so they basically rolled that back and they said no it is not obsolete no we
are not deprecating it um we will continue to maintain it uh some people like web client um but i blame i blame them for
for the miscommunication way back when when they all right um anything else i want to factor maybe i can convert this to
a constant eventually this will get become configuration uh because clearly i'm not always going to want to go to
localhost um yeah no problems in surveying price fetcher maybe i should make it a constant let me and this is uh price
fetcher url i'll declare it what what are you complaining about now no i don't want it to con er go away okay um what i'
m not checking for is what happens if it's a upc that the sir the tiny service doesn't know uh that's not a problem
because it knows it doesn't care right the price service um the price service basically returns 10 no matter what it is
which is fine i'm just doing it because i want to have something that's not uh basically an extra basically as an
external service hey there my salsa welcome all right um so we've got our concrete implementation working so let's go
ahead and do a commit uh insert many you switch to typescript oh that's a big switch i've done typescript i i like
typescript um but i love java too much yeah and i liked i i like the refactorings that are offered to me by my ide all
right so got our concrete implementation but right now um the only thing it's using is this test and okay uh let me
remember my unit test make cool yeah so eventually this will become configurable but i'll um now we need to sort of
install this to make it uh used in at least when we run it from when we kind of run it as if it were in production so
first of all we need to this is an adapter so this can use spring and so here we want to make this um we can make this a
service as long as we make it some kind of component i'm just going to call it a component it'll get picked up by spring
um and then we can go ahead and in our application class replace this thing with the fetcher and then we can whoa that's
a weird so now this will be injected by spring uh and we'll pass that into cart service and so now if we run the
application we so here we basically see the requests come in and so let's clear this run we're running what are we
running on so here we've got our upc it doesn't basically it added 10 and did it actually call the service let's yes we
see that the get request was done against that and so everything works fine and so when you're writing a new like the
hardest part if you've test driven everything else you're using hexagonal architecture the hardest part then is just
getting it to talk to the service in the way you want it or the external whatever service and the way you want to talk
to it um so that's all working uh now of course um we're not handling errors so for example um if i bring down the
pricing service let's stop it and then here let's go back to our ui and say that we get a 500 right not surprising um
mainly because we get a connection refused so this means we need a little bit more work a little bit more protection in
our implementation our concrete implementation this is the responsibility of the concrete adapter to handle this
situation at least in a way that the rest of the application is aware of and so um it's one thing if we got an error
from the remote system saying i don't know what this upc is i don't know what what product this is it's another that
it's completely down now we could add in some automated retries here we're trying isn't going to help if the service is
just completely down so what do we do here um we basically have to to communicate back to our uh system that something's
wrong is this something that basically the um here the is it something that the the caller in cart service is this
something it can recover from well no um nothing i can do so this would be where what do we want to happen if the
external service isn't available right now it's sort of a requirement for the way add product works right because in
order to add product that has to create a product object which requires knowing the price and the discount rule because
what if those this requires now both services to be up to be able to build the cart now we could say well there's no
point in running the system if we can't get to the pricer which is totally valid right i mean you might go i've gone to
the supermarket and like you know the self-checkout's not working because none of them are working because it's a
communication problem right sometimes a machine or two doesn't work but then that's machine specific but if it's like we
can't even connect you know yeah there's a communication problem and they're all not working that's likely external and
there's no point in trying to use the machine right so we'd have to say that that's probably an exception that is not
going to be handled inside of this cart service that would be a you know service unavailable exception that gets thrown
and somewhere would bubble up and basically would just bring the whole system down and then somewhere on this page it
would say system unavailable try again later right that's the best it now for the discount fetcher which we'll hook up
we could say if we can't communicate we return no discounts and maybe people complain we can say yeah we know and we'll
give you credit or something like that later but at least that all right so let's um let's go implement the discount
feature but let's uh see is there anything we need to commit yes um so um application uh the real before i do that i
want to make sure no tests are unintentionally using the real thing so let's run all our tests i think there so these
tests are failing why um because it can't find an implementation of a product price fetcher so here's where we need to
help spring oh right because it's not actually checking anything all right so what we can do here is in we could just
provide a mock one so what this does is it basically creates a mock using maquito underneath create a bean that fulfills
this interface puts it in the application when you have one of these this is okay but once you really and once you're
doing it either among multiple different more adapters right more ports you're probably going to want to pull all this
out into a test configuration and then provide the mocks from there or maybe you want to provide stubs here we don't
care about the values that because we're just checking really endpoints so we've updated our product mock bean for
fetcher all right go ahead and actually commit and push that all right so that's the price fetcher now we got to do the
discount fetcher which is going to be pretty much uh it's going to be fairly similar let's go to it discount service did
we even implement it yet we didn't implement it yet so let's go to our so what do we want we want um something that
looks like this price controller here uh but it's basically discounts and what we want to return where it's going to be
a little tricky is what do we return for the discount so prices was just a number basically a big decimal for the
discount service what we eventually want in our product so one of these two things so we need some way of mapping what
that service is going to provide so we've got to figure out what is going um i think i'll just use like a single so here
what we want to do is we're going to need whereas in our product price fetcher we didn't have to translate anything
right the stuff that came in is exactly what we needed we peeled off the price and just returned that for our uh
discount fetcher we are going to have to do that mapping so let's see what that looks like so let's go to our port for
our discount fetcher all right so basically by definition so let's go ahead and implement this this is our external
discount picture and this goes into adapter out and we'll implement that uh and so now we'll do the same thing we'll
write tests for this and this will force us to to write some of the mapping code but at least it'll be under test so uh
let's go ahead and and write a test flip it over to the other side tag it as manual so we don't run it other times patch
returns and um let's say for this one it returns none discount rule is none so we'll run this test of course it's going
to fail because it returned so that's fine we could return none directly that'll make it pass um actually let's um let's
let's let's refactor first so we want to want to refactor this where we're going to get some something here that's going
to be needed to be so we'd like to to extract that mapping part into something that is more directly testable so what we
want to do here is one of the refactoring maneuvers that i really like called expose hidden operations or expose hidden
details so eventually we want a method that given some piece of information right whatever code we get from the remote
system returns none so we don't extract this to a value we and what we're going to do is we're actually going to
eventually then add a parameter so let's we want this to be static move it to a separate class so we could put the
mapping translation in this class but then it makes it really kind of awkward from a from a testing point of view so
this is discount rule mapper not mapped to her but mapper some people like translator or transformer i kind of like
translator mapping is such an overloaded term so let's uh refactor that uh and yes it goes in source main java except we
need to give it so it's going to go in the same class as our disk as our external discount fetcher should make no
difference to the test but now we can start to write tests for for this how do so let's go ahead and write tests for
this and so we want is a test um um trying to correct role so this test is probably going to be parameterized because
i'm going to want to do it for all of my all of my rules but we'll start with just discount rule none so we'll um we
don't need to instantiate discount and so whether we're okay with this being static or not is sort of a separate issue
but for now we'll just test it directly so we're going to say is given this string what do we want for none um sure why
not and so basically given that when we call discount rule translator to rule we expect that to be equal to none now
this looks weird because we're not so that passes that makes me nervous so let's go and change this uh no the the string
is the remote code that we get that represents the discount roll all right so we're now talking about we're in the
discount fetcher and so what we want is we're going to send the upc but we expect back is something that we can
translate into a discount roll all right so that didn't work so let's actually right now parameterize test because uh
well you know what let's let's just and let's say this is t so this test will fail because the none doesn't work we swap
it to none it'll fail because the 10 off doesn't work and so that will now force us to make this more complicated and
wrap um although switch will probably switch expression will probably be better um but now we have nothing to compare on
and so now we have to pass in the string as a parameter all right so now we have something to the key off of so we'll
wrap this in an if else n equals remote 10 off which is a horrible name if it's n oh this one should actually be t
that's t then we'll turn that else return that um doing a parameterized test almost feels like as much work as to just
split this into two tasks so let's list this split this into two tests so this is going to be our uh translates remote
uh remote translate remote rule code to this one is translate remote rule code p to 10 percent that'll still work it
does uh and then we can write one more test which is um if we pass in something that's unknown some kind of code that's
not known we should actually translate that um switch yeah it's saying that that it's too few it's saying that that it
should be an if statement i actually think the switch is more readable but actually our default uh is going to need to
be is it going to need to be null none right so to nun rule so it's basically this this will fail because currently its
default is 10 off so we'll just um oops this is why we write tests that should work there we go uh so due to attitude
says um the common spot i end up with mid-asserts is when i have to create something to do something else if i have a
character named thor i want to change his name to oda first out to create thor to make assert that he was created uh no
you never assert on the initial creation that's set up you don't assert on setup set up a range given you do not assert
on on on the context you're setting up hey london rogue welcome um so apply discount uh not sure if you're referring to
the current code or something else but in fact it's a code smell if you somehow had to create an object and you weren't
sure was it created correctly right so so to your example right if i had some test where you know thor becomes odin i
think it's od i am that's the way i've seen it spelled and look intellij agrees with me and if i said you know character
equals you know new character and i know this is a java character um or i would not do an assertion here to make sure
that character yeah this is setup this is set up you don't assert on setups if you were however if you thought that that
felt like you needed to do that pull it out and it becomes a separate test can i create thor and does thor look like
what he should look like can i query him information about him so you never want to assert on the setup you can assert
you assert on right you create thor you maybe have to you know give him give him his hammer but that's all set up if
you're unsure what thought would have you know what capabilities thor has with the hammer you would write a test
specifically for that then that becomes set up you must be able to right all this is about you must be able to trust
your setup this setup works let's actually go to cart test this is why you always start out with a zero case you must be
able to trust what is the value of a cart what is the total value of a cart when i start if i'm not sure right if i
thought i this right here this is telling me i'm missing a test because why would i write this assert unless i was
unsure about what this did if i'm sure unsure about that then i should write a separate test explicitly to do that and
so if you do zero one many you generally end up doing the zero case first but sometimes you don't realize it and then
you're you're about to write a test like this and you're like wait a second how do i know what the receipt's gonna turns
out that throws an exception but i'd write i'd probably have a missing test for that right so when you start adding more
queries you have to make sure did you handle the case where the thing is empty or new then you can trust the query and
build all right um we're going to leave it as a switch and i'm going to tell intellij to take a hike all right um let's
go back to here uh so now we've got our discount rule translated now we can go back to our fetcher um uh and so now but
now we don't have to test the conversion right whatever code we get back and we pass in here we know it's gonna work and
so now we can flesh out the rest of this code um in this case it's a lot like other fet whoops our other fetcher which
is this one so we can copy this code and by the way are you all aware of command shift v or control shift v shows you
the hit clipboard history within intellij uh so let's paste that and that one's going to be and what are we returning
did i even write i don't think i wrote the service oh right because i was trying to decide i'm going to pretty much copy
and paste um so we'll need a discount response so we'll copy those and we'll rename these to be discount fetcher sorry
discount controller this is discounts and this will be a discount response and then what we want to return is t so we'll
need to go to discount response string i have no issue doing what i'm doing but i'm basically copying everything so let'
s call this uh discount controller test price with discount multi-card at work import that and this should be fee and
this is discounts and we expect it not to be price but i have no idea what was a discount rule uh whoops i didn't do a
rename there we go so let's um run all our so this failed because there's no rule um did it tell us what the content was
it's rule code okay perfect what's the extract okay um so our controller looks good response no idea why it now thinks
it's unused it's used right here holiday's a little all right intellij is just confused okay when am i gonna send this
should be asking the question of when am i going to send this sellers to whole foods yeah that's right well you know it
is not open source it is source available technically i don't think i've put a license in it so technically it's
copyrighted so i'll i'll see you live coding i actually need to add the open source license to it just because it's on
github does not mean it is open source it is copyrighted and there are licenses where you cannot do that there are very
limited licenses um there's a source available license that i use uh where you can't take the code and do whatever you
want with it you can look at it uh but you can't do what you want with it this one is technically yeah don't get me
started on github co-pilot because i know for sure they have scanned that code and if i had an infinite number of
dollars i would sue them just on principle not because i expect any money no we are not going to spend any time
discussing which license is best um all right so uh we've got our discount service we do not have our implementation uh
let's go and implement it so i've got our test um we're gonna expect it to return none um let's have it return uh 10 off
10 off everything that's the name of my store we'll go out of business very quickly so let's go back to our uh discount
service in our implementation um oh that's where we're returning we're yeah said we weren't going to discuss licenses
but i'll say one thing um i want a license that precludes usage by any cryptocurrency software that's what i want all
right so this is uh somebody i saw on twitter said hey how about an mit license with an emission uh call out or whatever
you call it and so it'd be the emit license and i thought that was really great all right so it's up and running um we
should now be able to um so first we want what do we want uh same response object so let's go grab that and let's go
over here and we will drop it in the love it i love how intellij when you paste what looks like a complete class you
paste it into a specific that's what i did here i pasted it here it actually changes the package from that's true yeah
they don't none of those crypto folks use use java or at least not a lot okay so we've got our discount response object
and so what we want is our rest template uh get for object our url and and our variables is the upc and then we will
pull that into a variable which we will call discount response where'd it go what are you doing there and now we can do
discount response dot okay so if we run this test so now we can go while you're on that side uh and now we replace this
with our uh discount uh discount fetcher except we didn't mark the service as something that spring is aware of now it
is um so that means there's 10 percent off everything uh load and rogue have i ever used the vim key bindings in
intellij why would i uh one of the folks in in one of the ensembles i run uses the vim key bindings um and i can see the
appeal if like you're you're a vim user um and your fingers know vim i've been using intellij for over 20 years and so
anything else is a step backwards or sideways or anything else my fingers do not know that's why so like i was trying to
use vs code and this is now probably a couple years ago and they had somebody wrote a plug-in like thing to um to allow
you to use intellij key bindings with vs code so that way i wouldn't have to re-learn a whole bunch of things didn't
work probably works today you he max evil more than my news yeah i just from notes i use apple's notes because it's
available on all of my devices but i do most of my writing in intellij like all the stuff that's up on my all right uh
we've plugged it in so let's run the application let's run both servers uh so let's switch over to so discount service
is running let's start so now if we run our application we've got ten dollars as the price fetched from the price
fetcher from the price service and everything is 10 off so we got the 10 off discount from our discount fetcher and now
our total is nine dollars and i'm gonna be annoyed by the fact that so i see single decimals in the context of money on
so many websites and it bugs the heck out of me it is like this is currencies and in us dollars and in many currencies
not all but many two decimals is common sometimes four sometimes none but it's never one like fix your formatting we can
see the price changing as appropriate um added uh external discount fetcher adapter uh anything else before i commit no
that thanks logan wrong uh hey muhu droid uh one of the most used intellij stopped working when i switched to linux
control i know that that when i um was using linux for a while um i was really annoyed because it was they were
constantly all these different things that would steal my intellij shortcuts so i'd be and i'm in an ensemble where um
i've got some folks who are using who are on the mac uh their external keyboard is not letting them hit um for me as i
said it's like i pretty much live or where i'm in my discord um i'm or maybe in a in a document but like probably 80 of
of my time is either in in intellij working on code or writing uh in my discord it was interesting because in another
ensemble uh somebody um one of the shortcuts to move to move certain things around um it was like control alt left arrow
or something and it would rotate the screen one way because one of the drivers had had overtaken that shortcut so it's
not just linux that has those problems oh is that you dota i know that happened to more than just you so let's see where
we are in our architecture uh so discount fetcher uh product price fetcher uh should we do our receipt display at least
we can get started on that unless there's anything i'm very much liking my my little icons to represent stubs and this
one represents a spy so we're going to use a spy uh for this basically notification like thing or we could implement
some more discount rules but i think i think i don't want to do that the other slides are from my hexagonal architecture
course sign up for my email lists course is opening very very soon a self-paced course with weekly office hours and
special help channels and all sorts of good stuff it's a course i've taught live now um i basically say 40 times because
it's somewhere around there uh over the past couple years and i'm now but it's all been live teaching so finally on my
way to converting it to a self-paced version oh you want me to reveal the price um so normally it's it's uh because it's
an early release it's 297 dollars u.s for just the course i'm still adjusting some of the add-on coaching coaching stuff
that'll probably be a few dollars for for a few months you need that discount fetcher well if you're in my discord there
there but honestly it's it's a totally unless you're in a country that has a poor exchange rate and then i do i do power
parity purchase power purchase all right um so we know that works and we've got our two outbound adapters for discount
and price now please do not buy try to buy it with with twitch subs i get i get only half of of the sub which is great i
so appreciate it but not a very efficient way to transfer money um they're people who make the living off of twitch subs
i am not one of them not even close um and that's that's fine okay um what we want is this receipt display so the
current behavior is not is basically you can finalize the order this technically isn't the receipt display so i think
the name here is slightly off hold on this is annoying me so let me so when you rotate shapes in in uh in powerpoint you
can also rotate which direction the text is going so for some reason though the text is going in a weird direction so i
want to fix that rotate all text no um oh because the shape has rotated wrong what is this one uh so we want um three
three twenty six no three thirty four i cannot wait now it looks like it needs to be rotated slightly less there we go i
cannot wait until and this is a project i'm going to start in a couple weeks creating these diagrams by hand as you can
tell is painful painful um and so one of the things that uh because like you know getting it to line up and look right
and get the spacing all good and the rotation um so painful so i have a project that i'm going to start in a couple a
couple of few weeks where i'll be able to describe these in sort of a mini dsl right so like plant uml you can describe
sequence right right you can define your objects and then you can do that and it creates a nice diagram and then this is
really easy to create if you want to rename something you just change some text you want to change the way the order
that it's in you just change the text and so i want to yeah exactly so very much like like mermaid or plant uml um
plenum l is built on top of graph whiz um but i don't even need anything that sophisticated because all i need is to
generate an svg and i can do that in java there's great libraries for that i've been around forever so i just want
something that generates and where i'll probably do a job do it in java fx because there's tools for that as well and so
i can get basically have an editor window and then have it translate to an svg and then i can basically just dump that
right into my powerpoint this is the the plant uml plugin which if you do not have uh for intellij you should get it it'
s one of one of my uh commonly recommended intellij plugins i think i have an article about which ones i recommend
remind me remind me and i'll take a look um yeah so anyway so i'm looking forward to being able to create these using
text a text-based language instead of spending an hour on a single diagram um so stay tuned for that once i get the
course launched uh and and off the ground uh then i'll be um well there's nothing to say that i couldn't take the
diagram language that i would use to describe this and create a skeleton for the classes and put them in the now i
wouldn't write the actual code uh but it could write and it wouldn't create the tests but it could create the test
classes that have the right um because that's just that's just generating code from a well-defined syntax that's easy
enough to do and then you can the problem with all of those is it's a one-way thing right because if you try to do
two-way your life is over this is why case tools never succeeded this two-way modeling tools just never worked because
it's that coming back from given the code now go create the diagram or textual representation doesn't work in most like
in very limited cases it works but yeah but for a one-way generation like hey i want to create this thing create me the
skeleton um given a textual description that i have in my head for this it would totally work yeah i mean you could
probably apply certain machine learning stuff to do certain things but yeah i don't know i don't know that i'd want that
but somebody else can go do that funny machine learn like as much as machine learning pays as a software developer who
worked for companies and could have gotten twice what i was paid if i just wanted to do machine learning i i just it's
not it's one of those things i'm just like just not interested in just not interested in i know how it i wish i liked it
more so that i could have gotten paid better but i got paid well enough that's fine all right um so what we want where
was i oh yeah i was talking about receipt display and i was going to change the text here so this is um not receipt
display but um how do we want this to work what do we want this to represent this sort of represents the screen at your
self-checkout kiosk um is it the receipt log i mean it's sort of showing a log an ever-growing log of oh cool you wrote
a paper on it well good then you can write that part i'm more than happy to to to hand off my my models my my text
models and and have you uh go do the rest of it and ieee nice impressive um so this receipt log it's not really a
receipt yet until you're finished it's really uh a product the price what do we want to call it oh i know so one of the
things i do even though this is like it's never good like nobody's ever going to use this for real but i like to use
real domain terms and so i end up doing and going down the the rat hole of researching domains like oh what are the
terminal what's the terminology used in self checkout approximate weight self-checkout scans so i want something that
what is the what do we call the visual display part so yeah i'm looking for a word in the domain that would represent
the the screen that's displaying the stuff as kiosk i feel like is the whole thing um terminal is a bit ambiguous touch
screen monitor display and then i end up down the rat hole of like oh how what companies make these things um checkout
screen or check out we like terminal or screen better i feel like it's screen i mean i'm i'm very big on like using like
the correct domain terms especially in a yeah and i'll spend more than um i think checkout screen's good enough great so
that's our our port so now not that that's what we want so now we want to define is um as a result of scanning right so
carts so what we're saying is is as we scans basically as we submit right as we add a product um it can it's going to
call cart and so it fetches the price stuff adds the product to the cart and so what we want this to do is then notify
yeah six of one half dozen of the other all right so obviously i'm not going to write code here i'm just writing
comments that's fine um so let's now go uh to our to another cart service test um yeah i like that i'll i'll go with
that that's what it felt like display felt a little bit more abstract part service so let's see so what do we want sent
to basically the product because the product has well we don't want to display the whole product because that has the
discount rule we don't want to display that uh i mean i could send product but but i'm actually specifically want to
send something else and let's actually write a test added then uh check out let's play notified that's our setup um i
haven't added the description yet i'll probably add that at some point um but yeah definitely the amount uh if there's
um now they won't do usually they won't do quantitatively so multiple entries not onto the receipt so this is
interesting um and so this will be something i add the display is shorting sort of is not sort of it's showing sort of a
rolling log um the receipt sort of consolidates things and adds some stuff that you don't see on yeah exactly wrong
exactly let's go grab a real let's start using some real upc's let's this one not a brand i use but whatever uh and at
some point we'll we'll i'm going to provide an alternate implementation of the product pricer to actually use something
like this because this one you can actually it has an api and actually can ask it for hey what is target selling it at
but not yet um let's make this more interesting uh that's what i want okay oops there we go and our cart service is
going to say no discounts and so when we add the product our expectation well now how we gonna write this expectation is
nothing to expect there's nobody there's nobody to assert against so this from hexagonally and this is why i have sort
of this this stub out fetchers so we have stubs for our fetchers but notifiers that are outbound only right because this
the display is not going to communicate back to our system it's just a receiver so we need to create a spy for this
which means we need to figure out what the thing is that we're going to for now just the upc and the product price so um
i could hey there uh your a is over case c arnie carney fps so we want our checkout display um what's our what what
method do we want display but that's the implementation uh our product hey friedrich oh welcome welcome from brazil yeah
there aren't a lot of us java streamers i think is going to have something like um product added and it'll have the upc
and the now normally i wouldn't use my keto um so what we want is uh we'll basically create a spy of and this is our
cart notifier buy so now we have something to basically assert against and so now we can say cart uh notifier spy uh god
i forget about how to do this every yeah i actually don't have any spies there oh it is some method because it assumes
and product added um what i expect it to be called with um yeah it is basically toothpaste upc right and that it's
called once all right now i can run this test which will most assuredly fail because this cart notifier spy is not used
by so that failed as expected because they were they were uh there were zero interactions so perfect uh so two things um
one is you're welcome to look at the code directly but also i organize the code according to hexagon architecture so the
adapter stuff is out here this is all in inputs and outputs which is basically this so everything inside the hexagon is
pure application and domain logic uh then the things that are out on the periphery are interactions with the so in our
application i've got the cart service here that's part of the application layer and then the domain if you're interested
in more you can sign up for my email list i've got a course coming out on this exact topic but that's not all i have on
the i have also other articles uh so it's not just the sales list all right so our test failed it failed in the expected
way so now let's in inject our cart notifier um is it like a presenter uh i guess i feel like presenter has very
specifically uh it's going to be connotation here it is going to be displayed on whoops on a checkout display but it
doesn't have to be it could be a third-party system right that's updating inventory as products get scanned so it
doesn't have to be specifically presenting that information anywhere it's just being notified and that's why this is
called a cart notifier the implementation might be a presenter but the interface itself is uh is just a notifier and
somebody may use that information okay so uh so it fails we want to now inject it into so i'm going to create a private
final oh okay well first i'm going to move this so it's available so let's move this to an upper level um and it goes in
main because this is a uh ultra70w um hexagon architecture is a layered architecture uh you if you've heard of clean or
onion or those are the two other names i know if it's similar to that basically it's this so you have your domain um as
the internal part that is only domain logic business logic game logic whatever your domain is surrounded by an
application layer that deals with the domain and the outside world and then you've got the outside world and what are
called adapters and so if you sort of tilt your head it looks like a layered architecture right you've got your pres you
know sort of your your input web ui you've got your service layer you've got your domain but i like hexagonal because it
makes so uh all right so now we've externalized that so let's say private final cart notifier current notifier this will
force us to add a constructor parameter but i don't want to do that i and right now it's fine for it to be that's what i
want why did it give me two parentheses so i've got a now a null implementation a no op implementation it's not null
right no um and so now what i can do is uh because i want for for all tests that are currently using cart service i don'
t want them to have to deal with the notifier so by pushing this out and now everywhere that was using this cart service
that no null object implementation got pushed we could probably replace this with null and so everywhere it's it's got
pushed out now in our application application why does it keep throwing that stuff over there um we'll eventually want
to replace this with uh something real and we have to decide what that looks like but for now it's basically still an
implementation of our interface all right so now in our in this test we can now replace so now um and during all this
time no test should be broken except for the one we're working on and so i really like this refactoring because then it
makes it easy to to push what i want sort of as a default implementation of this thing into all the mostly the test
callers all right so now that it's in there now that we've injected it now we can do the notification so we'll do cart
notifier product added upc and and it does awesome and just in time too all right so we now have add product fetches
discounts and price creates a product holds on to it and yes good i'm glad it gives you a dopamine rush because um like
for card service i don't like service here but most people are used to that but certainly for um my external things
there there are two kinds of outbound adapters you're either fetching information or you're sending information
sometimes you're doing both like a database repository is actually doing both but those are generally then called
repositories uh i think that's all for today added port for product added notifications to part notifier added partner
for product added notifications um so next time on my next stream uh we'll implement the checkout display that i'll
actually push to railway so that it can be up on the internet so i'll be able to sort of you know scan products here on
my machine and you all would be able to see it on on the so because i pushed out the the null object when i introduced
this parameter because i did as introduce parameters as opposed to just changing the constructor i knew it would work
because i pushed out a no op version of it versus doing a change signature on the constructor would have would have you
could still of do the same thing but it's a little bit more awkward so you can do a change signature and i could add
another parameter but then you have to for the default value it can get which is why i like the the introduce parameter
because then i know it works and then i can push it out and sometimes you'll pull actually push out behavior that exists
in here right hard-coded behavior uh and i show this in the course um and i think i've done it on on stream a bunch of
times uh you extract it to a field initialized in the constructor and then you then you uh hey the g3 oh is that
guessing um is there a reason to call the notifier method with just the epc in price and not the entire product yeah so
um i don't want to send the discount rule because the cart notifier doesn't need it uh if there's anything more than two
of these i'd probably create a value object to hold on to those um i couldn't send out the whole product and then leave
it to the notifier what it needs and so it it's one of those where it kind of depends but i'm totally allowed to hand
domain objects right product is a domain object and i'm totally allowed to hand those to to the port and then it's up to
the implementation of this to then translate that into am i sending an api am i displaying on the screen what am i doing
yep no i didn't commit uh so let's see so we add that i've followed by the part service brand product is on it all right
uh yadav am i going to enhance the discount application logic yes um there uh i need to externalize the sort of two for
one rule um the discount fetcher this is not good enough um because it just takes the upc it doesn't take into account
quantity so we'll have to uh we'll have to expand on that um so um so for notifiers notifiers should not be referencing
anything inside the hexagon right they're given stuff basically information is pushed on them so notifiers shouldn't be
calling back fetchers will be creating uh often they're creating value objects if anything but they generally don't
create full domain objects although they could repositories absolutely will create domain objects because they have to
in order to restore a domain object from the database we've got to create it back in memory so it and that's fine
because the rule about dependencies and again i talk about this in my course but the rule about dependencies is
dependencies must point inward so as long as you're pointing inward so your notifiers could access stuff internally they
just generally don't fetchers sometimes do and repositories absolutely do but as long as your dependencies are inward
right domain is completely unaware of the existence of anything else it's living in this pure platonic world nothing
else exists application service that's what talks and coordinates with with the outbound adapters um and the in inbound
adapter absolutely needs to talk to the cart surface to kick things off so you'll sometimes see inbound referred to as
primary or as driving but i prefer inbound i do like driving the problem is is then outbound becomes driven and then
they're too similar um so i've gone with inbound and outbound but uh aleister coburn who came up with hexagon
architecture calls these driving uh and driven or primary and secondary and i don't like either of those pairs all right
as i say that's all folks my next stream or friday not sure yet um if you're not a member of my discord uh if you don't
want to jump right into the discord you want to know what the heck it's all about before you jump in you can click uh on
that link which takes you to my website i've got lots of articles there um reason i mentioned the discord is i don't
always announce anywhere else so that i'm going live you could follow on twitch those sometimes are unreliable uh those
notifications so um i always try to give at least at least five minutes notice hopefully more than that but at least
five minutes notice that i'm going live on on the discord plus there's lots of great discussion and questions and
answers and thoughts and so on on the discord um i created the discord because i wanted a community where i could talk
about this stuff um and so i couldn't find one so i created one and so uh you're welcome you're certainly welcome to
join all right thanks everyone for hanging out i appreciate it and all all the chatting and all the questions it's all
great that's why i do this so i will see you next time have a great rest of whatever day is you
