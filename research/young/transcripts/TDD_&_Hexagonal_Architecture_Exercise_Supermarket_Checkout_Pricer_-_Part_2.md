# TDD & Hexagonal Architecture Exercise： Supermarket Checkout Pricer - Part 2

**Video URL:** https://www.youtube.com/watch?v=2ESC6MEw3ic

---

## Transcript

all right hello folks uh happy fourth of july for those of you today's stream i'm going to be working on the supermarket
checkout pricer exercise that i did last time but whereas last time i started from the sort of a bit inside out sort of
starting directly with the cart and figuring out the product it was a bit awkward because there were some places there
that it was unclear where was the information coming from so uh let's take a look at where we were and then uh then we'
ll so let's go over here um let's close the project and try again tell jay i don't know why it had a problem like i
didn't change uh i think that oh the jdk in the um all right let's okay so now it works hey squeegee all right last time
uh we had gotten to the point where in our tests we had um the ability to not only price the items but also be able to
ask for the cart contents and find out uh what they what they contained and we extracted a product as base as just a
straightforward record um but what started to become unclear was when i wanted to separate the responsibilities around
this receipt printer uh basically i split out the code so that the scanner printer was responsible for printing the
receipt so we'd done that separation but was really kind of awkward and again mainly because we weren't doing outside in
we were starting with this cart thing and then expanding from there uh but the real question is where like how does this
whole application start what triggers products to be added to the cart what information comes in uh to the cart like
does it just get products added if so then where do those products come from in our tests we basically create these
products manually but those products we're instantiating each time and so anybody could you know if this were something
with uh you know type in the name of your product and the price that would be really inefficient right that's not
something we we'd want to want to deliver and so this is really um while the the sort of standard checkout pricer
exercise is mainly around just getting the product stuff to work right getting all of the different options around um uh
you know the special deals and things like that um i'm a bit more interested because i'm uh wanting to create more
examples for my hexagonal architecture course i'm really more interested in uh so you can play around with the
pre-printer extract and try renaming cart to receipt printer and extract into a good cart yeah that's interesting yeah
you could do that um and so i wanted to sort of start over and uh take it from how you know thinking a bit more about
how does the information come in uh what's interesting is that uh this then allows that um this to be more of a
hexagonal architecture application than just sort of you know uh having a cart that knows how to do special deals and
things like that i think it's actually i think it's more interesting mainly because it it has to do with hexagon
architecture which of course if you know that that's something i'm very interested in but i think it also uh is more
realistic um and there's not enough good examples of of hexagonal architected applications uh even though this will
still be a relatively toy application i think it'll have a lot of the so sorry i'm just getting my drawing tool up so
i'm experimenting with using my ipad as my drawing tool because i have my apple pencil okay um so what um what we're
doing here let me just okay so what we want is is things like cart um and product we want uh those things to be part of
our domain and have no knowledge of sort of where where information came from what we want to get to is where we're
adding products which would have sort of price we want to get those products into the cart so the question that arises
okay how does the system you know let's say we're actually writing code for a checkout scanner where does the
information come from right how do we know what product was just selected to be added to the sort of the cart even if
this weren't you know physical checkout machine the same thing applies like where does the information come from in
terms of how the person selected selected the item oh sweetie thanks for the for the sub with prime gaming appreciate
that the the answer is basically from from this adapter so the adapter is the connection to the outside world right the
stuff out here right it has not no knowledge of where the information came from is it a physical machine with a barcode
scanner um or is it uh you're shopping online and you're clicking on items that are displayed on a web page who knows
who cares that's all up to hey dota 2 attitude uh thanks for for oh you can still take that shot one zero months it's
either two months or ten months um so right yes uh and so the adapter um then becomes okay what do we want our adapter
to be uh what i think um might be interesting is that it's coming in from some barcode scanner and so uh the reason why
i sort of want to go that direction is because then there's going to be the need to to look up uh to look up apis that's
to look up upcs via an api to talk to uh some server and and i basically found one that that basically returns the name
of the product along with a bunch of other information but we won't need all that information and so um what we'll do is
we'll want to map then uh that product name to to our catalog um now we could say well why don't we just map the upc in
our catalog to the name well maybe we don't um we don't have all the information we need upc will will come in through
the adapter uh we'll have to go and fetch information from the from the external service uh and then we'll use that
information to figure out which product we need to uh and so when if if that's what we've got then uh you know what
might our first story be right so um what we want to build is uh where we get you know some some upc you know from
barcoder for from whatever translate that into a product so maybe we get that information uh from the third party
service and then we we look it up in our repository so maybe we have a product catalog so we've got some product catalog
to to find out what that information yet another way to access something externally so this gives us enough enough of
the bits and pieces for a hexagon a an application that would lend itself to hexagonal architecture right we've got our
um our sort of right and then we've got our domain it talks to the upc external service out here and then uh we'll also
want another adapter which will be the thing that so we've got an inbound adapter for the barcode we've got some uh
information requester types of things where we're fetching information from the third-party service right that's our upc
uh api we've got our catalog to retrieve information about the the product itself and then at some point we'll want to
trigger uh the receipt printer to print no there's a little lag because i'm i'm using um a shared whiteboard um so
there's a slight lag uh trying to figure out a better a better system it'd be nice if like i could literally use the
ipad as a drawing tablet um some hacky stuff that that doesn't work hey there umuz would be a good read to like most
things you will not learn by reading you will learn by doing but some guy some good guidance for tdd uh i think kenpack'
s book is is okay for for starting out but it's gonna end at a point where you're just gonna want to do more um beyond
that uh i actually don't know of uh there's a book that that um has a chapter on it i have not looked at it uh to see if
it's so i'm not sure i can recommend any books other than kenpeck's which i think is is okay as a grounding but uh i
don't think gets you to some of the more advanced stuff because i think some of the more advanced stuff is actually the
kind of things that i'm going to be walking through in terms of hexagonal architecture so i would say basically try to
follow the the the tdd things that that kemp beck talks about um i think one of the hardest parts about tdd is actually
the refactoring and that's that's under emphasized uh so getting good at refactoring i think getting the refactoring
book by martin fowler and of course if you're not already in my discord we talk a lot about edd and hexagonal
architecture and all sorts of stuff so don't hesitate to drop by and all right so we're gonna basically um go back to
our uh main branch we're gonna create a new branch um and this one's gonna be uh that was weird i'm not sure why it
opened both those up so um by the way speaking of tdd like one of the things you want to do is is exercises like the
supermarket checkout pricer so the main branch for this is just these first tests to start with and then uh the readme
has a bunch of ideas for for how to uh how to kind of kick that off so something like that is is a is a really good uh
place so we kind of established like where does where do we start here how does it know where the um product comes from
uh and so the question then is is given this you know quick and dirty architecture diagram uh where do we start well we
want to start with um basically here right with with our inbound adapter because that's going to be helping us figure
out and this is why it's often called outside in development we're starting with the outside how does information get
into the system so let's say um the upc there's all sorts of questions around uh if this is you know an online system
then we have to sort of know who's who's the customer here because it's handling you know a bunch of different customers
all at the same time right any website that is going to need to do that but if we kind of assume this is sort of a
standalone machine then we don't need to know that because the there's only one one user so we can start there and then
we could always explore what would it take to have this be sort of an online online system hey homeless 207 uh barclays
guys like yeah uh yeah i mean it may have a connection to the internet um but it doesn't you know certainly especially
the modern self-checkout ones uh where um it's also gonna do things like you know you enter your membership number so
you can get discounts and things like that uh there's all sorts of complexity that we could add in but we're gonna try
it try and keep it fairly straightforward but we are going to be connected to the internet because we are going to
basically uh call out to this third party api to get so we'll start with the adapter and we don't necessarily need to
start with so we can basically start with the upc yeah universal product code so we'll start with the upc i know we say
it like atm machine right we start with the upc that comes in as a number maybe it comes in as you know just a string
and so what do we do with that right so we're basically thinking about what comes in to the adapter but in terms of
where we might start we're really going to start at at this boundary right this is the boundary of of sort of our
application code all right so what is and and basically here this is our our application layer right so this is the
first thing that adapters connect to once they've done all their work of handling input and receiving messages and
deciphering them and so on and so this is why in hexagon architecture it's often called the use if the use case that
we're talking about is product scanned then we can start with our use case and have and start test driving yeah
sometimes it seems like deciphering the deciphering decoding so that means we're not going to start with a cart test um
or at least yeah we're not going to use that word so let's go ahead and delete this we're on the branch yeah so let's go
ahead and delete this start with an add product to cart test let's start off by putting this in in the right layer and
we'll go ahead and create and so we'll start with our first test so what would our first test be um here again we're at
the use case level so our tip my typical tdd uh sort of thought of where do i start which is zombies right zero one many
handling the zero case here it's different because we're starting at a use case so what the use case is is add a product
okay so what product are kind of doesn't matter we use toothbrush in the examples before so we'll sort of continue with
that oh just from um so so the test is really um it's add toothbrush and so then what's our expectation so uh what we
want is how do we know this worked right so the two sort of the hardest parts of test driven development uh is is
figuring out um what do we want to do okay so we want to add a product well how does that come in what sort of the api
is it were at this level what we're saying it's a string that's the upc um and so we're going to need to be able to
observe something about the system to know that it did the right thing uh typically if we're executing a command right
we're saying add product and so that's a request for the system to change state right to start tracking that product um
and so this is often where it's like so we'll have to think about maybe there's a different place to start uh homeless
207 um oh my gosh had amelia kind of cut him kettlebell yes sorry i just was actually watching you before uh working on
the minecraft stuff and like oh my gosh i know nothing about the minecraft stuff so welcome thanks for bringing your
your uh your huge party here i appreciate it what i'm working on is um starting from scratch doing test driven
development and hexagonal architecture on this supermarket checkout pricer exercise uh so we're starting we're starting
from scratch so it's a good time to join um this is sort of a quick and dirty drawing of uh what we're doing which is
basically figuring out how we implement a little supermarket checkout pricer we scan products with a upc figure out how
much they cost do receipt printers but we're doing it according to hexagonal architecture to separate concerns so thanks
for thanks for joining there's a question homeless 207 you had about uh putting test files in the same folder so in that
sort of depends on the language and the test ecosystem that you're working with in java um 99 of the people using junit
i know there's still some test ng people out there but most people are using junit uh and even with test ng the
structure is you have two separate folders you have one for your code and one for all your tests and that way when you
package things up you only ship stuff in the code package the tests don't don't get shipped um uh yeah i'm using java 18
in case you're asking about what version like how you're executing a command against me java dash free uh yeah i'm using
java 18 because why not i get to do whatever i want uh with this project so the first test that we want to write if it's
going to be add product and like okay what how do we know that worked so we have to have some way of querying the system
right there's no system yet there's no no codes we don't quite know what to do but we have to have some way of of
querying the system that the product got added now if we were doing um a more london school style mock based approach we
might write a mock and then verify that a method was called and and do something like that but i'm a classical tddr so
we're not you have x yeah every every language does things their own way um so if we're gonna say you know so really
it's right that's a horrible test name um but for now when as we're thinking as a sort of thought process that's you
know that's okay so we want to add a product um we'll start with a toothbrush because i need a neutral toothbrush uh and
so basically it's how do we know this worked what can we observe about our checkout system that the product was added
well there's several things we could do we could say we could ask the the cart right which is the thing that's going to
accumulate these products um what you got what's in you what it so treat it as a container that we can query um we could
also just say i'm right now mainly interested in getting the price functionality working i don't yet care about that it
keeps track of products right all it knows is that you've added a product and it's accumulating the the price um so
that's one possible uh way to to uh so we'll see that for for testing we're not going to actually use an h2 database so
i used to use h2 quite a bit uh but these days um with test containers using docker uh and postgres um we can do a lot
of stuff in memory so we'll we'll see some of that with with some fake uh implementations and then when we want to
actually write to a real database we'll use the real the real thing that's what i do in my my other systems and it works
really well it's it's it's a lot easier than it was just a couple of years ago in memory is definitely faster and we'll
so then cart total one dollar so we're going to say add toothbrush all right so that's what we're going to say so we're
going to say that the way we observe this the way we observe the change to the system right because we care about
changes to the system we add a product it's worth we're saying that it's going to be a dollar so that when we ask the
cart it should be a dollar well if we're going to do that we end up with with zombies again um with it which is zero one
many this is the one case but how do we know what a new cart is i don't know they charge for shopping bags so maybe a
new cart with a shopping bag is 25 cents and so we need to establish a baseline of of what it is when uh the shopping
cart is empty so that means we the way i do that is i basically put this test on hold and i start with a baseline test
of um so the total price of the cart starts at starts at zero yeah i don't want to mark it as disabled or ignored um i
want to basically for it that test to pretend like it doesn't exist so that's why i deleted the the test so now we have
to figure out okay great so we're saying that our baseline assumption is that our uh cart system when it starts out has
is when it's basically starts out assuming starts out as empty it's uh total price total cost maybe total cost is a
better term and starts at zero so what do we instantiate so now here's where we get to what is the object that we create
so remember that uh we are in our core domain in our core domain we're at this application layer so we're inside the
hexagon but we're not in our actual core domain there's actually a piece piece and let's see if i can change colors yeah
good enough oh that's a that's a weird color um this is the first thing that that gets hit uh and so that's our our
application layer or our use case layer or sometimes called our application services layer i've kind of been playing
around with the terminology and i'm even though application services layer is long it's three words um i think it gets
the idea across that it's a service layer which means it has no state by itself yeah i guess that's the unicorn color uh
um i saw dude am i making a time machine no i'm not making a time machine not sure what you mean by time machine um and
so this is the first thing so we have to figure out um and so the way i start out is i pretend it has all that it needs
uh everything that it needs so what is the method we're gonna call to ask our system what is the total price well it'll
be um we'll call it cart service i know not a great name but we'll we'll so we'll need to create one of these and so now
we're actually creating our first class so now we're going to split our screen because this is the way i really like
doing development having the test on the left and the code on the right um and so uh so we've got our cart service so
given a cart service when it's new um total cost so here side note like this is where i'm always thinking about language
ubiquitous language from domain driven design what what do we call things so products have prices um they may also have
cost but i think i'm using price what do we call the thing like the the the amount of value that the card has i'm using
cost but even that feels weird so if you've got a better name than cost i guess price i don't know it's weird uh we'll
use total cost for now total amount maybe total amounts better and with this order total and so since this is a query
method um yeah it could just be total since we're asking the card service yeah even better all right so we'll do that um
so then we'll just say total so we'll so notice that as i'm refining the language i'm also changing the method because
you want the method to match the match its contents yeah all right so we'll go and create the method uh it's not going
to return void we're going to start out with money being it's we're not going to worry about money certainly i'm not
going to be using a float or a double here uh we'll start out with ins whole dollar amounts eventually we will have to
use something like a money class um once we get into discounts and things like that yeah it's very true good names tend
to get shorter not always but they they tend to do that uh so i'm gonna return negative 1. i'll sometimes return and
throw an exception but here because i i know that sort of the expected value is zero i can purposely return something
that's yes i know i haven't used it yet intellij slow down all right so let's assign this to a variable total uh and
we're going to assert that total is zero so our first test yeah until you have three well then you need packages and
like yeah three hopefully you don't have that many in um so here's our first test uh we now want to run it we so my uh i
have a whole bunch of articles on my website about my predictive test driven development process so one of the things
that i find really valuable is to predict how is this test going to fail i know it's going to fail and in this case it's
relatively easy because there's not much code but as the application gets more functionality more code it gets a little
bit harder to predict but being able to predict why it's going to fail or that it's going to pass is is really valuable
so here it's obvious it's going to fail and in fact it fails as expected great we're going to return zero that'll get
our test to pass uh hopefully if you factor things well homeless 27 if the as the app gets bigger hopefully coupling
levels out at a certain uh a certain size right so if you group things together if you've architected it uh organized
the code well then you'll end up with clusters of objects that are coupled to each other and then the connections
between those clusters which michael modules or packages uh have have very thin connections all right so that
straightforward right not a big deal um but we're gonna go ahead and do a commit all right so now we know we're going to
add a product um and we now have a way of observing what's the current right this zero here and uh make a but i don't
think that's uh i don't think that's where i want to maybe it'll be a field or maybe i'll use um sort of a sense of of
just holding on to what products i have and dynamically calculated on the fly i don't know yet so i can't sort of
prematurely make it make a design decision so i'm going to leave it at zero and let the tests tell me which so now we
can turn this test on right i sort of always think about is you know flipping flipping tests on and off and so now we've
got this test so we so we'll see that this is not an at service you this is part of our application layer which means
it's completely agnostic to frameworks in fact we haven't even added spring yet we're going to get there but we haven't
added it yet because we haven't needed so now we've got to figure out uh we want to add a product how do we know it was
added so we're saying that um our total will be one that's what we're saying we're saying a toothbrush is a dollar
because it's a really cheap toothbrush and um that's how we'll know so that was weird i don't know why i did that so
given a given a cart service when we add our product so this is what we're and i'm not quite sure what this is going to
look like yet um we'll be able to assert that the cart when we ask the cart service for the total the unit 69 yes
eventually when i want to tie the inside of my hexagon which is completely unaware of what framework i'm using when i
actually want to tie it to spring i will use an app being in the configuration yep exactly uh oh you're right actually
so yeah the the the state won't even stay here eventually it'll get refactored and pushed in uh because services should
not hold state so again this is this is um my the way i develop software is i tend to refactor to create new classes
rather than create them up front and start writing code in them um i don't always avoid creating classes up front but i
tend to take classes from existing code and so we'll probably pretty quickly do that so add product so what does this
need to do um you need to hand it some kind of product but remember we're getting upc's uh or if we want to be redundant
upc codes um so uh we we're gonna basically make up the fact that there's some upc code for our toothbrush i mean i
could probably go look look one up but we don't need to be realistic right now not not just yet yeah exactly um so what
we're gonna say is that uh the contract for this service is that well upc's are numbers but they sometimes have leading
zeroes uh in fact i was i was playing around with um seeing how good this third party api service was with upcs so i
punched one in from this box of this bag of pistachios i've got here and it starts with the leading zero so we can't use
even though upc's are numbers we don't treat them as numbers because we don't do math on them and this is something i
point out in my courses is like this yes it's a value yes it looks like a number but we don't treat it as a long or
float or anything like that it's still a string so we're going to want to pass this in then as a string um so we're
going to say that at product takes uh takes a string represent and that represents the upc now there's some stuff here
around hexagonal architecture and value object and domain driven design around well we don't want to just pass strings
in how do we validate and things like that but you know what you can't do everything at once so let's start here um
exactly homeless that's uh that's the test driven development process you you write the test watch it fail um but before
we can watch it fail we gotta get it to compile so we'll need to so since this method is a command it doesn't return
anything uh then we don't have to implement anything so we're good there uh hey larry kallarga are most java jobs in
finance banks i don't think so there are lots and lots of uh java applications um for enterprises that aren't
necessarily finance and banks but you will find a lot of java in in yeah a lot of insurance yeah so i worked at a
company called guidewire software which provided insurance software for large insurance companies and was all in java if
you're interested in uh in tdd yeah like space cam foundation you said you can you can search for it i've also got an
article um and there's a whole series of articles on my website about predictive test all right so we've got to compile
now we predict well uh add product does nothing total always returns zero so clearly this is going to great fails as as
expected i wish the depression i wish java was used everywhere i wish it was used more because i will probably use it
until my career is over but there's lots of lots of languages out there that lots of places that don't um so failed
fails as expected so now we have to decide what do we want to do well we can't obviously return a constant here anymore
so the next level up is um some kind of if statement or a field right so we need to have some way of of making a
decision or storing information so we could say you know what to get um maybe make it a field uh eventually that might
go away as we get additional requirements but one of the things that i've learned is um and tdd i think really helps
with is what is the smallest step you can take that gets you to working code as you understand it right now uh i'm not i
don't see a need to use a static field i'll just use a regular a regular field but what i can do is i can treat this as
a refactoring so the way i do that is i basically turn off the failing tests because kempec has a has a great saying
which is make the change easy and then make the easy change because the change we'd want is somewhere in here right
something like you know uh total plus equals one right add on one to the total we'd like that except we don't have a
variable so i could write that code create the variable update the total method and update the add product method all
while i have a failing test my preference though is to do as much as possible while preserving existing behavior right
refactoring and so for that i need to to pass so i basically turned off the test that was failing and now i've got well
one test but now what i can do is i can take the zero and i can refactor it so i can extract it use intellij's introduce
where do i initialize it i'll initialize it in the field declaration that's fine now again this is a service so this is
sort of a way station right this is the cart service services don't have state they have collaborators right they have
references to other classes but they should not have state um there are times when they do but like in general they don'
t certainly they don't have domain state and total is domain state but tdd in small steps tell us to start there and
refactor our way once we uh the energy version how a java is taught is not off topic for me because as an educator uh
right as a software developer who've seen it a lot of bad java code and it's an educator who tries to teach it right all
right so that was just a refactor to introduce the field um so nothing should have changed right so our test should
still pass and it does so now we can do a commit refactored to introduce now we can turn the test back on it'll should
still fail for the same reason and it does zero is not one and now we can basically uh jre is totally free the java
runtime is totally free unless you're like gonna license it and incorporate it into a product in which case all right so
that should get this test to pass it is totally free for enterprise usage unless you're using oracle's the one that you
have to pay for but there's lots of implementations that spacecraft foundation totals supposed to be cart quantity or
price ah good point uh the intention is for it to be price so if we think that total is confusing i think i would use
quantity if i want to know the quantity but for now it's not obvious that that that that that is the price yeah it it's
a little confusing at this point um but we define that that total is is the total's price uh but we could say cart total
price and so here we said total price as well uh jakarta is open source so it's yeah there's a common misconception that
because oracle charge and still charges for certain java jdk stuff um that it's not free but it is totally free all
right so we think this will make the test pass um if if i were to be really pedantic about tdd i would do this just
total equals one and maybe let's do that why not so this should get the test to pass now when i teach tdd people look at
me and like really look we know we're going to be incrementing by stuff why don't you just do that um and it's true we
could take a larger step right one thing that kent beck says is is you know we can use our professional judgment um but
i prefer to have tests that that force me to do things um so that when i write code i know that it's covered by a test
so sort of the inverse of of of sort of thinking about code coverage is i don't write code without a failing test means
that when that test passes i know i've written that scenario and i've got code that is so what would our next test be we
could go with the adding a second item so maybe we add uh hillary do i have any certifications i no i don't believe in
certifications i do have a a java 1 or is it a java 1.1 in the late 90s i got a certification because one of uh the
companies i was doing training for required it but i don't believe in certifications i think um i've i've helped people
study for the java certification and this you know if you really like puzzlers um then that kind of thing is uh
interesting um but honestly eighty percent of the stuff that you need to know it feels like um there's such educations
and corner cases that they ask in those certifications then i'm like honestly like i've looked at the certification i
tried i basically took a sample certification i failed and i've so uh that's exactly right daddy depression right that
it'll that allows and supports and that's why when i when i um have people learn that i say even though you could do a
bigger step try smaller steps because one of the things that's actually really hard sometimes is to to all right so
we're going to basically um i don't need this comment anymore so we're going to add this product twice and then our
expectation is that when we ask the cart service for its total the thing i like about taking smaller steps um as i've
really focused on that more um i end up with designs that that were not always what i expected like in my head i've got
a design for where this cart service is going to go all right so if we do this obviously well maybe not obviously but
the test will fail right because it's going to return one um because every time we call that product it's going to just
assign one we're expecting two so it's going to all right so it fails for the right reason we can throw in the plus
equals and now uh and now it should pass but there's a big assumption that the price of whatever product we add is a
dollar clearly that's not true yeah i actually um looked at the oca exam book um because there are some things where it'
s like oh maybe i should know that but the way i look at it is like we use such a small part of the language that when
we get the things that we don't often use we just look them up like yesterday i was exploring um some different ways to
use generics like i've used generics for for a while but i don't use them in every possible way and i was like is that
gonna work and i basically had to try it and and look it up and it's like oh okay that works um and so especially with
with the tools we have it's so easy to to to just try things um i think it's more important to sort of have a good
understanding of of what's going on underneath rather than than knowing sort of esoteric edge cases of things all right
so our test pass one of the nice thing about them running fast is i can i forget if they passed i can just do it again
so let's go ahead and do a and at this point this is general enough i don't i know i i don't need to to do three um and
so one of the things that that tdd tells us to do or guides us to do uh is think about the stories you know what
functionality we want to implement but also looking at the code to tell us um and so clearly not all items are a dollar
and so some of the things that i look for are are literals right like this one thank you yes and i i love intellij uh so
this this one where does it come from is a really interesting question right clearly it's related to this upc which is
not being used uh and so we should use it and so what we want is a is a test um for the it stuff i know kotlin uh uh
uses that as well so we want to expand on this right we want to sort of poke at this upc thing like how do we know what
the price of a product is right we know cart service probably is going to add on and accumulate the pricing but how do
we how do we know what that that upc is worth well we need then a test to drive us in that direction that is something
like add toothpaste because the toothbrush doesn't oh jetbrains oh thank you so much for the the 10 tier one subs wow we
we love you uh so toothbrush isn't very useful without a toothpaste so let's add some toothpaste then cart total price
is um how much is toothpaste two bucks was i buy it in bulk so i was like how much did i pay for it we'll call it so the
code's going to be the same we probably want to get to something like well 0 1 2 3 sort of representing toothbrush so we
want something else that represents toothpaste as it's as its upc so one thing i want to do now to make the tests easier
to read right because one of the things we want to focus on when we're doing coding and especially test driven
development is making the test readable so let's extract this to a constant and we're going to call this upc not ups
that's the name of the shipping company upc there we go uh so now this makes the test easier to read right it's still a
constant string but but it's easier to read i'm going to grab and let me take out the comments they're not needed
something like that is represents the upc all right the code for our toothpaste and so this at this point i want to make
it clear that this is associated with toothpaste so i'll immediately extract it to to paste upc now our expectation
though we said was three dollars by the way copying and pasting tests i don't mind that copying and pasting code maybe
i'd think a little bit more about but copying paste and tests um i don't mind doing that one thing you have to be
careful of though of course is when you copy paste uh you forget uh i have a license for intellij i actually don't use
all the other products intellij is all i need so i've got a license for that but i've used it for 20 years so i feel
like it's all i need um because really what else do you need your programming in java it has everything you need so i'm
going to pretend that i didn't see the one and pretend that i thought it was a three so at this point x i expect my test
to fail because it's only only adding one and so uh i'm going to expect the test to fail because one is not three
because i'm thinking it's expecting three but it passed that concerns me like that shouldn't have passed and so this is
why i like predicting failure specifically um because you make mistakes in credit writing tests uh yes once copy and
paste once the test setup code gets to a certain size then you want to really start to refactor the test setup code um
for test data oh jetbrains that would be wonderful i will definitely raffle it off because i have what i need but i'm
more than all right so this should now fail because i've corrected it uh because three is not one and perfect so now now
what do i do right so this one is no longer sufficient as a constant uh as a well constant literal uh i could change it
to three that's going to make things worse right it'll make the current test pass but it'll make other ones fail so now
clearly a constant isn't going to work here so what do we do well we know that that uh certainly all right um yeah so
once i get that from jetbrains i'll i'll uh i'll run a giveaway on a future stream so what we want to do is we want to
associate this upc with this number so right as the start of of down that that you know ratcheting up the complexity we
could do an if statement and so what's interesting is uh this cons these constants um i could convert it to an enum but
that that doesn't feel right right uh but that that would be really easy to do uh but but we could start with just the
simple if statement maybe we only have two products maybe we're a toothbrush toothpaste vending machine and all we care
about is the price of two products and then an if statement might be fine and so this is again this idea of keep things
only as complex as they need to be right immediately you could go to some kind of map or you could now extract a service
that does this right a product catalog that associates things but we'll start out simple so let's do um we could write
some code so let's make sure that we're we know where we are in terms of our tests so we change this back to one so we
still have one failing test but changing this one to basically an if statement um that might uh that might be something
we could do so and oops i commented out the wrong one i'm at the combat out this one so i'm going to basically make the
the change easy and i'm going to do it in a place where all my tests are passing so replacing this one with an if
statement um so i'm going to extract this also to a constant price or cost i mean i hardly even need to to code that and
so now i can wrap this in an if statement and would we say it was uh uh you'll next example create a cart object at some
point um at some point yeah i need a domain object right now i've got a service that i'm sort of it's dual purpose um
but uh right now i don't nothing's pushing me there just yet we're getting there but not yet so this should be
equivalent code right it's a little bit more complex it's a little bit more precise so that you could say the behavior
is slightly changing but it's close enough and the main point though is it should still pass all the tests so it does
and so now if i add or turn this test back on um it will now fail for a different reason than it failed before so that
shows that behavior has actually changed so before it failed because when i added one item it was counted as a dollar
now i'm adding an item and it's counted not at all but that's okay i can predict that and i can say that that's that's
okay all right so now i get three and not plus equals three right i could do that that would make it work or i could say
you know what look we're probably gonna have several different products let's make sure it's one of those um and so
we'll just say lsaf upc equals and i don't know why i keep typing ups i guess i think about that more i've got this
three and i could say you know what for symmetry purposes let's extract this to a constant so this is uh toothpaste rice
so this is toothbrush upc i've seen that before i could have copied it over from but i'll just continue to extract
constant on this and this is an object yes thank you intellij this is tooth that was just some basic refactorings
everything should still work but now at least we've assigned some some names to things the other thing that things that
it does is it makes this easier to see that we have a pattern right we've got if it equals something then we have when
they so let's do a commit and then we're knows price of tooth brush versus based thanks jetbrains i appreciate you
stopping by and thank you so much for what do we want to do well one thing we could do is we could look for duplication
so um the duplication that i see i see two different types of duplication i see this duplication right the comparison
for the upc against some string and i see duplication around updating the price so both are duplicates and i wanted i'd
so what i want to do is is have a method that given a upc will give me the current price for that item so let's see what
this does perfect so what i've done is i've pulled out um right because because i'm i'm basically thinking this section
of code is going to be replaced by a method by basically some kind of lookup method and so what i wanted to do is i
wanted to isolate that i could have let it have direct access to total but that's not its job so that's why i extracted
out now i want to see if i don't usually do this let's see if i do it the other way so i want to replace all occurrences
but what if i don't replace the right axis occurrences yeah so these are all right accesses yeah so the the extraction i
did would have would have made the test fail what i really want and maybe i'll just extract the method so if we extract
the method it's going to directly access the field and i don't want that so item price is total but this this fails the
test there may not be a direct way to refactor to what i want and it does so that's good so what i can do is i can say
total plus uh and then start this out at zero so that works um but i kind of do want to find like a way to could extract
total plus so yeah so the problem is this is this is a field and any any method extract like i do um is not going to
work i could extract it to method and push that as a parameter but it really needs to be a return not a parameter
because i don't want an accumulating parameter if i replace it with that yeah i may have to let's see uh the problem is
anything yeah i need to basically move this up in scope and um yeah i don't maybe there is but i'm not i'm not seeing it
usually i'm pretty good at seeing it but i'm not seeing it so let's go with the thing we had before with the manual work
uh we've got our tests let's make sure we're at passing test before we do this okay so we're good um i'm just going to
do this manually so basically uh item price equals create scope for that oops did that too early item price equals total
plus equals item price uh there's no way to turn this into a ternary because there are um separate specific equals if
this was just an else then i could turn it into a turn array uh but because there's two separate uh explicit if equals
uh i can't do that okay yeah so our goal is we want a method so now what we can do is we now that we have sort of the
item price separated from totaling up that item item why are you passing an item price though yeah it shouldn't have
needed to do that that was weird um we should just be able to return this into we'll do that as a refactoring actually
just inline this and so we get total total plus equals price for upc oh i didn't select the declaration of oh that's why
i was passing it in got it so let's do that again so price for yeah so the extra parameter should have been a signal to
me uh and now we can inline this and so now we have this method and so this method is doing the the translation between
that uh upc string um and and the price and so my goal is to push this somewhere else it does not belong in cart service
right it's it should be some other responsibility where it goes i don't know yet so i don't have a good sense of of well
i have a little bit of a sense uh probably some product lookup but right now i don't i don't have a so all of our tests
should pass and bracket method that all right so that works um we got a price that handles multiple items we could mix
it up try a mixture of toothbrush and toothpaste uh look up is look up one of the classes uh if it's sort of a
one-to-one then it might be yeah um i'd almost call it a i might be tempted to call it catalog rather than a lookup
lookup doesn't whereas i kind of want my my ports to be verbish for me but so kind of like upc finder or product finder
lookup might be the method name but it doesn't feel like it should be the class name this sort of pushed a little bit on
the product identifier but in our application where are we getting that product information from is that part of our
system or is that part um and do we want to push on on that aspect yet i think i'd want something that that starts sort
of separating the application class here from from the domain and a couple of different ways i could do that one is to
have um basically extract total because now uh total is is suffering from primitive is a is a code smell where we have
some primitive variable like like int so we could solve primitive obsession by extracting cart that's one way to go or
we could extract the price finder service or we could do both let's do both let's uh extract let's do that so what do we
want to move it to um it's going to uh product finder we haven't really defined product do we because i'm not quite sure
what the interface is i guess the interface is that accepts us a upc string and then returns returns the price kind of
feel like this int is going to cause us problems pretty soon so maybe or we could just treat this because i don't know
if i want to pull in the money class just yet well we'll leave that for now i but i think this is going to be coming uh
pretty close that we'll need um we'll need some something else for that let's pull out um so we want is um we're going
to call this a product binder product pricer because that's really all we care about right now uh what do we need from
that just this method plus this information needs to go with it i don't understand why when i when i when it extracts it
to delegate intellij seems to leave like actually i would like you to get rid of it because it inlined it here but now
this method actually is no longer needed so we can just delete it all right so we extracted product pricer take a look
at it um this is a pure factoring a little riskier than just an extract method so we want to make sure our tests pass so
let's do a commit extracted product and we could go down the road of making product pricer into a proper pork because
one of the things we said in in our design was at least that getting some of the information about that product by its
upc was an external service i hadn't originally been thinking though that it would um provide us with a price i was
actually kind of thinking there would be a catalog but just because it's stored in the database doesn't mean our port so
this is a port uh or or would become a port uh it doesn't mean it has to look like a repository the implementation of
looking up price all right so we've got add product and basically it totals up the product so i think we've we've pushed
out on the product pricing stuff what we i think what i'd like to do next is sort of push on okay i'm done uh show me
you know give me my receipt because what i wanted to do is i wanted to to not just track the cost of the items that were
added i want to track the actual items that were added so i could push on that for the receipt or maybe what's more
interesting is push on the discounts because that that's actually the main one of the main things behind this
supermarket checkout price or exercise is all these special deals and discounts so maybe let's push on that because that
will likely lead us to a cart that stores the actual products that were added and so let's do a simple one yes happy
july 4th from thank you uh this one let's do this one so this will also make us uh have to go away from in towards
something else um could do big decimal but eventually it'll be it'll be a money of some sort but we could we could do
big decimal in the meantime um so let's do this story so buy tooth to and you get one for half off what a deal uh yes i
could steward a sense i was thinking about doing that but you know i may as well just bite the bullet and go to go to
big decimal or something all right so this is this is um what we want uh so i'm going to actually create another test
class because this is here this was sort of about a general straightforward ad product now we're getting on to special
deals so let's create a new oh right i don't have a we'll just do it this way so this is uh special deals uh best so let
me import that so add two tooth brushes uh which means we're actually we actually might need to not write a new one uh
so i'm gonna go back here here we added two toothbrushes um let's change this test actually let's and then i'm gonna
change it add uh sum of product prices so instead of the toothbrush we're going and then this should be three plus one
is four so this technique is what kempec calls evident data right i'm showing that what we want is the sum of the item
uh the two individual item prices so we're just changing the test this should i can force it to fail by just changing
all right so now in here we can copy this and so uh this this thing these toothbrush upc's um so adding two toothbrushes
what we're saying well we can't say one point while we could so let's start here and then we'll refactor although we may
as well just move to um let's see what value object would we want this is uh um i don't know if i want to go to a value
object just yet i think we'll get so let's refactor and then we'll basically change this test to be the discount so we
want to change uh yeah because it's not really a type uh so let's go ahead and just change that yeah i'm going to change
the test method to basically say uh one item is half off but it's not that's not what it's doing yet right now the price
we can leave is whole dollars so what we're going to do is change this total equals total why am i having trouble
spelling total total add and that will value of i guess we could just convert product i like how it's like sure i'll go
change that but i'll make it not compile anymore um hey there uh buffy land yes i am doing tdd uh so you meant the fact
that toothbrush is a dollar or is hidden from the test um open to suggestions on solving that so this should be
equivalent um this equal to uh is uh equal i think we want is yeah is equal to here yeah if you've got suggestions so we
just throw them and chat um okay so this was a refactor to introduce and change our type from into the big decimal i
think we've got it everywhere probably a bunch of our tests are going to complain and yes they change they they uh are
broken because um we're testing uh ins versus versus big decimal so let's go fix that um by uh this one though will
actually just yeah eventually i'm yeah i am going to move price the the product pricer into a port and stub it out so we
can be clear um but you're right that right now this uh the information is hard coded here we could actually um how do
we feel about referencing this directly since it's a static referencing yeah there's something that creates the product
pricer right there's something that that puts stuff into there and right now that that that is a bit hidden i think i
think i'm gonna delay that until we extract that to a port and then stub it out and we'll get something like daddy
depression what you're talking about all right um did our test pass yes they did okay so you may be wondering how does
right i'm basically saying total which returns a big decimal is equal to a string so it turns out the implementation of
this basically takes care converting the given string to a big decimal for you so what's nice about that is you can say
8.0 and you don't have to convert it to a big decimal yourself it will do that for you and how did i know that was there
uh cause i wrote this was my big contribution back in the day to what was then called fest was all all right um are we
converted to big decimal i think we are converted to big decimal uh that's here and in our product pricer uh so we're
all good it's diamante all right awesome so cart service now is is much um is much smaller one of the things you'll
notice is this hidden dependency right so this is a collaborator the product pricer is a collaborator but it's a hidden
collaborator because it's not injected into cart service and that's causing some of these problems that that that
impressions through here have mentioned of like this product pricer is a bit opaque um so we'll want to make it more
more transparent uh and do we want to make it a stub or a fake i'm not sure might want to might want to start with the
stub but let's do a commit converted to big decimal for total price right so we did that before we extract out and fix
the product pricer let's do the special deals so we were saying that it should not be and how do we know that because we
just know so two toothbrushes uh all right um then second is or just half so this will now so now we're back i haven't
been wearing my tdd hat um because it's actually a bit warm today uh but i've got my my tdd change behavior that's where
we are we're in change behavior change behavior hat on um this test will now fail it'll fail because right now we're not
doing any discounting um so we're going to get 2 instead of 1.5 so what's the smallest step we can take all we're doing
is is totaling up uh the price as the items are added we don't keep track of the actual products so there's no memory
and so there's no way to to to know have two products um now here's where it's like well how do we know what what
products are the same well for this particular special deal i think we're going to have to hold on to but if you've got
a smaller step let me know but if that's the if that's going to be yeah i was thinking yeah so i could do it based off
of of the price um if the current total is one but i think we'd pretty quickly get to a test that that doesn't work um
and i don't feel like it's it gets us closer to what we really i think eventually want is keeping track of the history
of items of products excuse me so it's a smaller step but i'm not sure it's it's it's a smaller step that takes us in in
the right direction but it did definitely come to mind um yeah i don't know that that allows me to refactor to where i
want to where i want so disable the test that's a good idea to add a depression i could basically just say right now i
want to know what products are in the cart that'll also force me into the same situation and it would put aside looking
for did you already add this item so that's that's a that's a good idea um so we can turn this off um and what's
interesting is if we had gone down the direction of getting the receipt then we would have gotten the same the same
thing right basically we need to know what what are the contents of the cart uh so that mean so the question is if we go
the receipt route to force this um that means we have to have a way to get access to the contents of the cart and expose
it through the cart services api no matter what if we if we're gonna make it observable and know what um yeah we're
gonna have to do that anyway so let's do that so let's create another another test and this is our uh our our naming
here is a little bit feels a little bit off because we're talking about cart but then we're talking about cart receipt
and it's like do you get a receipt for a cart card sort of this temp i mean it's funny how you know we use words from
the physical world and we and we put those in in our e-commerce systems and then it feels weird like we talk about you
know adding stuff to a cart and the cart having a price though it's not until we actually turn it into an order or we
take it out of our cart and it gets put into bags and we actually pay for it so there's some language weirdness here but
let's let's not go there um so cart receipt well now we can now we can yeah i guess we could call it cart content test
um and sidestep the fact that this might be used for receipt generation uh sure i'll buy that so we're basically going
to say uh empty new cart so now um this is interesting um where we've been talking about carts but we actually don't
have cart as a class we have cart service which has been serving as this hybrid entity service thing uh we want a new
cart how do we create a new cart we can't just new up a cart we could new up the cart service but is that really a new
cart so we might need some things to to force us to just to separate these we could just separate them due to hexagon
architecture we could say look cart service is wrong it should not have any state and we could justify it that way or we
could really um i think since since i'm sort of like using this more for from a hexagonal architecture point of view
let's except we're we're still going through the api so um yeah it's it's either way we'll get there um but i feel like
actually dr even though we could divide it but because of hexagonal architecture rules i think driving it through the
test would so there was an implication that when we create a cart service that it implicitly created a new cart and
thinking outside in uh this and this is where it gets into sort of we want to purchase we want to place the order right
we want to basically conclude the transaction so we could go to sort looking at the but if we want to sort of you know
take a step back and think outside in what what we want is sort of we've we got onto special deals but we actually didn'
t finish sort of a full what is the minimal sort of you know cart system that we can that we can create that doesn't do
special deals but we can actually finish and place an order all right so we've added right we've we've started the
system we've added products and it gives us a running total if we want but at some point we'd like to actually place
that order right complete the transaction and so maybe it makes sense to to do that before we get on to the special
deals um and this is where i think uh you know this this gets back to sort of further out from uh outside in development
which is how you know in what order do you create your features and your stories and so what you want is something that
you could deliver right it might be the most useless cart system but hey if you've got you know a website for example
that only sells toothbrushes and toothpaste doesn't have special deals then you want to be able to conclude the order
and and pay for it we're not going to deal with payment because uh i think we've already got enough complexity but i
think the idea of saying okay basically now i want to buy this i think that actually needs to be our next step um before
you know it may cause some of these other things to happen but i think we need to do that uh before because that'll
that'll flesh out some so if we think about um so we've got add product to cart test our special deal stuff is on hold
so and so we've got i think we can basically say place order now we need to figure out like what are we implementing
here i said supermarket checkout pricer but maybe it's an online supermarket they have those so regardless they would
either be if it were like a kiosk there would be a button to say okay i'm done pay now or online there would be you know
basically place order so let's place order all right so you have a good have a good evening night what's the quickest
way to get to um sort of resetting the cart all right because that's really what place order does basically place order
says all right you're done here's how much to pay uh right so our goal is um carts are are transient they hang around
for a while but then they're when we place the order then they're done in the so if our scenario is uh place an order
try to place an order with an empty cart that's not valid but we can start there or we can start with a valid case which
is add an item place an order not only uh should the order total be whatever the the cart total was add one product
place order then empties cart and we'll do something like cart service um could just call it order create that method i
don't know what it's going to do yet well if this test is all about that it empties the cart uh oh we had to add a
product so let's so um so it's really part with place order um when we place the order then it empties and so when we
finalize our order oh i didn't import my so now our expectation is that total although it'd be nicer to say it's empty
um that's what i'd like except we can't do that because is empty doesn't exist so we don't know that that works as a
reliable way to observe the state of the cart so what do we do uh we basically put this test on hold and we go back to
our add product and we go back to our baseline cart total price starts at zero um i am fine with saying not only is the
price zero but it's contents but it's so now i'll create the method that's a boolean uh here i don't want to return
false i actually want to throw um an unsupported operation exception uh to really make it clear that i haven't
implemented this yet so we can run this it's going to fail and now we can basically return true oops now we need a test
that basically forces it to be not true so we're not only going to check that the total price is there but we're also
going to say assert that the cart service is empty that's false and it's really interesting um how often objects are
containers that hold things here the cart the cart service but really the the cart holds products although right now
it's not holding any products it's just holding the prices for those but it it acts like this container and so we can
often ask a lot of our objects are you empty you know whether it's a cart that's holding orders or whether it's a bank
account that holds transactions we can kind of ask if it's empty it may make less sense about an account is empty
although it is empty that means there are no transactions and that tells us that there's nothing in there but his empty
is not the same as uh has a zero amount or zero balance but it's really interesting how how a lot of these things are
similar in fact there is a whole set of object oriented patterns container is one of one of those patterns all right so
this will fail because right now we're hard coding returning true so that failed as expected um so let's uh so another
way instead of i could undo that change and get and refactor it but i know i've got one test failing and i know it's
failing right here um so i can sort of keep track of that without having to go back into the green state it's a known
red um so i'm fine with actually doing a refactoring here here i'm just going to extract this to a field it's empty and
we'll we'll declare it in so this was a refactoring so it should um now we can do is add product we can basically say is
empty it's false we don't have a remove product so that's fine so now that we have some way to detect whether a card is
empty or not let's go so now our expectation here um is that finalizing order uh basically sort of resets the cart so
not only uh should the cart be empty but actually the total should so essentially should return to its so this will fail
because finalize order right and it got tripped up first on this so when you have two assertions and again i'm not some
people are like well you can only have one assertion i'm like well what is it what can we say and observe about a cart
you know that's been finalized and basically it's gone and now there's a new one sort of an implicit new one is these
two properties one isn't enough to say that it's empty um maybe you've got a free item in there or if it's empty maybe
the total wasn't reset uh so we'll um first fix this one so we're gonna keep this we're gonna um we could have split
this into two separate tests and then we have a failing test and a passing test and a failing test and a passing test i'
ve i actually don't mind as long as you predict how the test fails in a sense that's a expected behavior which is what
we're looking for out of our test so the first thing i want to handle is the totals so now the test will fail but now
it'll uh and so now we can basically is empty is true again and that should get our test to pass uh so spacecam
foundation asks about shopping carts it's you know um one of the hardest things as an instructor uh is coming up with
examples that are at least somewhat realistic um this is the problem i have with uh tutorials that do things like with
animals and dogs and cats barking and meowing because that's not realistic unless you are actually simulating a world
where that happens so you want something that's somewhat realistic but you also want something that's non-trivial and
one of the things that most people the examples i typically use are either like a shopping cart or some kind of purchase
kind of thing or around a game but i think more people know about shopping than they know about blackjack blackjack is
the game i use in my is in my course uh which by the way i should mention uh so i'm releasing a course on hexagonal
architecture where this example um or i'm not releasing it i'm launching it uh it'll be released um over the next uh few
months but um launching it uh later this month um so i use blackjack as one of my primary examples but i wanted a
secondary example that had a bit more uh a bit different kind of thing and so shopping carts we we know what they are we
know how they work we know how to pay for stuff um we also often know about discounts and things like that so yeah well
i also see like blog post stuff but i don't i don't find that compelling because one of the things that i want from my
examples is non-trivial domain behavior because um we don't you know i can create a to-do list but there's no behavior
there um to-do list is also popular i could you know there's a bunch of kinds of things where there's sort of very much
a data focused and one of the things i try to do is really focus on behavior because it it's harder and it and it doesn'
t get enough attention um and it allows me to then uh talk about domain driven design and hexagon architecture and
things like that all right so um this is not working let's go ahead and so when we finalize an order that basically
clears out the cart um so why did we do this we did this because we wanted to try and get to the point where so this
card service might not look like much right it's what 30 lines of code may be not even um but it's it's got some some
design issues uh if nothing else um it violates what a service has but we've already got sort of multiple states here
that are very much connected right you change one you change the the other right we change total and is empty together
so these are paired and so the depression's idea of returning a pair it's actually a code smell that tells us there's
there's one thing i do is i use a wallet class to hold money as one of my tdd examples um and there you can sort of have
this idea that you know your wallet is empty if there's no money in it basically if it's zero here we can't quite say
the same thing because we might have a a free product we don't know but because these two variables that the total and
that is empty are very much two aspects of of of a single thing right there's there's sort of this cart object that's
asking to be created if nothing else due to this code smell something that encapsulates total and that is empty but
maybe it's not we're not quite there yet so now we can go to sort of add um add product to uh no the uh what we wanted
was you know we already have uh finalize order um so we kind of have could we ship what we have now um actually let's
take let's think about that right if our you know simplest feature is we can walk up to the system add a toothbrush
finalize the order um what are we missing what we're missing is sort of how much and so maybe uh maybe this is what
pushes us to well we need an invoice or receipt or something that tells us um and again i'm assuming finalize order
behind you know we're sort of assuming payment is made behind the scenes uh so i have a rule that inside of my domain
objects right those in my domain layer they have two kinds of methods queries where you can ask it for information and
commands where it does something but finalize order and here's where it's like it could return something um that violent
you know that sort of my head's tingling because it's like uh i don't like that um because i like commands and queries
uh but for now it may be okay the other thing is is okay this is sort of a single purpose machine right single user
machines so we don't have to worry about order identifiers or things like that so maybe that's okay and maybe uh that
means somewhere later we'll have something that we want to have simultaneous multi-user carts or some need for that uh
then then we can worry about it then so and sort of in a sense we want um two things we want the total plus we so let's
so let's rename place order to finalize order and so we can pretty much take this this setup and say what we want is we
want to be and so now we have to decide what are we we could return the final price or we could jump to returning so
final price doesn't tell us anything different really again what we're trying to get at is is uh right and and this is
where it gets difficult we're balancing two things we're trying to implement functionality that's useful and that we can
get feedback on but we're also trying to stretch out the flexibility of our production code and one of the things we
want from our production code is we know we need it to remember the products that have been added so one way is we can
just ask the cart what are your contents and do it that way the other is be able to finalize the order and get a receipt
and inspect so we're going to say receipt because one of those we don't know what that is we'll create um we'll just
create the class code flip that over actually we'll uh hey there trash of twitch um i uh things that you don't know are
hard that's um and for web development is is too ambiguous to to make any kind of statement about but i'm like i don't
get into language comparisons or echo system comparisons because i find those to be pointless uh you use what what you
think is best for reasons um and i i don't i don't get into sort of debates and discussions about differences between
ecosystems because that's like you know pointless yeah i'm not going to get into that that discussion because i'm a java
developer and it's trivial for me to create a quick rest api server but it depends on what you want to do with it and
what you have to connect with um there's a lot more complexities than just creating an api server from scratch all right
so let's make finalize order return a receipt and we're going to have it return null that's totally fine um in a sense
that's a refactoring so um other than this test that we're working on no tests should fail if it were true or factoring
so they don't so the first thing we can assert is simply and i see these sort of like little steps like okay i wanted to
return something that's not null um i could even say that it's exactly an which is kind of pointless because by
definition it has to be received we're not returning null i mean we are returning now so now we can return a new receipt
this will pass but this was a temporary test i'm not going to leave that assertion the way it is so now i expect but
really what i want to say is um what well one thing we want to ask it is you know what is and so this we should be able
to say uh this is equal and so let's go create this create the method and that's going to be is equal to 1 is equal this
will fail it'll be null but that's fine um now we want it to return one which is the total except we by the time we got
to this line of code we've already lost the total so that means we need to extract this into a local variable move it up
now as a refactoring so the test should still fail in the same way but nothing so that's fine and now we can say is we'
ll initialize it basically with total maybe receipt as let's do that let's let's turn it into a record um so let's uh
let's and it's a big decimal i thought i was at 18 what happened that's why intellij wasn't suggesting it okay so uh
this should not work because uh we got a receipt it holds on to the total we're passing the total here why do i have two
modules here um yeah oh oh because i branched from maine and maine is still so okay great all right let's go commit that
um spacecam foundation yes uh mentioned that before and uh that's a product pricer issue and we're gonna have to we're
gonna have to deal with that pretty quickly um because i agree that is getting confusing that's like how do we know it's
one yeah um so i think after we we do this one we'll want to to make our tests a bit more understandable and that card
service will need a reference that will force us to externalize the the yeah i mean i'm i might have one i might have
might have should have perhaps i should have fixed that earlier um but it's interesting because you know we went down
the road when we started of only being concerned with the price uh there's basically the how much the total price of
items in the cart if we had started with i don't care what the prices are i just want to know are you keeping track of
the items themselves um might have gone in a different direction and uh the pricing might have or might not have it
might not have okay so why does it think this is unused sure it's used i think intellij is a little so so now we're now
at a branching point um do we want to continue down the uh finalize order receipt having the contents of the cart which
would force us to start storing the contents of the cart as they're added right that the products as they're added uh or
do we want to take care of that product pricer um i think i want to take care of the product pricer because that's going
to cause a bunch of tests to have to be reorganized so um let's do this through refactoring this is a this is a trick i
love so what we want is we want cart service to take product pricer uh as a parameter to its constructor what's
sometimes known as dependency injection but really it's we're passing in product pricer into cart service uh so this
gives us direct access to product pricer to make it more obvious but also will help us uh so not so it'll help us with
tests but also better better architecture now you might just go ahead and say all right i'll go create a constructor and
i'll create this as a parameter but actually we can do but then you have to change um uh then you have to change a bunch
of stuff manually what i try to do is as much as possible because i love intellij um is use the refactorings to get me
there uh hey uh i'm not sure how to pronounce you're saying the receipt is because the body's not used it absolutely is
used because it has an implicit method for for total it's just confused because it doesn't there's some in index that
it's not fully updated so what we want to do is we want to say move initializer to constructor and i realize that's
slightly off screen so let's do this what we want to do is move this new to the constructor so that automatically
created our no argument constructor and did that there no no change totally totally refactoring all our tests should
continue to pass but now what we can do is use one of my favorite refactorings introduce parameter and i would love to
know why it keeps oh i know i did that okay so what this will do is it'll push out this is a parameter and everywhere
it's currently used which is in all of my tests it'll push new product pricer there right so now um by the way that just
proved you wrong because now receipt it updated it updated some index so now it knows where how it's used so it has
nothing to do with the fact these anything about curly braces or anything like that it was that some index and intellij
didn't get updated and now it but by pushing this out as an argument to cart service first of all all our tests should
continue to pass second of all that means now in all the tests it just does the same thing so now i can start creating
custom modified interacting with the product pricer and all through automated refactorings so again it's one of my
favorite techniques if i like you know started out with something that was hidden a hidden uh basically a hidden
creation a hidden dependency a hidden collaborator and by refactoring to the constructor where that's where it
instantiates it and then pushing it as a parameter is a great way to to do that without having to do a lot of manual
work um yeah okay so tests so speaking of tests yes uh intellij uh has this tendency because stuff i tend to create
through testing it puts it in the wrong in the wrong place so let's do that let's fix that up so thank you for noticing
because i often don't notice and then i'm like what why can't i access this thing um so let's move all these to the
right place yeah so car both card service and product price were all in the test directory uh so now that's right so we
got cart service product price and receipt oh and that's probably why it didn't see receipt because receipt was in um
receipt was in the right place but cart server and product price were not even though they're technically in the same
package it might have gotten confused although it stopped being confused okay so we got tests in the right place and we
got production code in the right place let's go commit uh moved project code to the correct directory um externalize the
dependency on product right here all right great um i don't think we need to keep this so what we'd like is um to now go
back and and change some of these tests uh and i can take out these comments now um we'd like this to be more obvious
and now what we'd like is we'd like to be able to initialize product pricer to a specific item but i want to drive that
through through a test through a failing test doesn't have to be a new test and we want this to be five um this will
fail because when it tries to find this product it's not there uh and right now we're assuming if it's not there it's
not worth anything so this will be zero instead of five right so i'm predicting how this is going to fail to change to
an existing test so do i like that because i let's um there's something about this that's making me uncomfortable uh
because i feel like i have to change the method the test method name um i think maybe we refactor our way there i don't
know that we need any change in behavior so let's do that so let's pull let's start with let's start with this test um
but let's pull out the toothbrush upc and the one and put that into there so what we want so in a sense um which we're
changing behavior i think that's why i'm struggling this is this is actually too big of a step i think what we want to
do is actually refactor our product pricer first because right now it's just using if thens and that's not going to be
good for something that's sort of programmable so let's let's undo that so let's focus on refactoring our product pricer
um what we want to do is is uh basically convert this we could replace it with a switch that's somewhat better but what
we really want to do is is make it have state right really right now these are static files that kind of aren't state so
um so now this is a refactor right so we're expecting all our tests to continue to pass but we're going to make some
code changes we're actually going to stuff these two things probably a map is the thing that makes the most sense so and
we're gonna map um uh string to well we'll do integer but eventually we'll probably convert those to big decimal uh
wondering how small a step do i want to take let's do this let's uh just do toothbrush so we comment that out we expect
now any test that involves that's a bunch of them how about we that's better so now we have a failing test so let's make
this test pass by doing product to price add sorry put and so um our default i don't know if i want to do this this
might be this might be too too clever um let's just do this if if product to price contains key upc return product to
price get upc and then we've got to convert that to big decimal actually in that case we may as well just convert the
big decimal right off so this is a tiny step of starting to convert it to to a map um if this if this works uh if it's
not in there then i'll fall through to this and then we'll eventually replace this so this if this works this tells me
that that i know how to use maps let's see if i know how to use maps okay apparently i do so let's do a commit so a
small step towards converting switch okay so now that we know that works now we and do product of price put then we can
delete both of these this is an odd thing but and now what i can do is i can basically and since this is just a constant
i can now inline it here and since this is just zero i can uh yes strip trailing zeros that's interesting so now this
this should still pass all my tests but now i've converted into a map so that's kind of the first step now this still is
encoded in terms of this information is encoded in here the goal of of starting to external is the goal of putting it in
a map is to take them the next step of not only making it configurable but then so what we want now is to push this out
so i can sort i could do the same technique of pushing the map outside of the product pricer or yeah i could push the
the map outside of it so let's do that move the initializer to the constructor um if i introduce that as a parameter can
i push out the so i think i'll need to create uh an overriding constructor because in production use i won't i'll be
doing something different i'm not just quite sure what um and this product pricer is actually kind of becoming uh right
now it's actually a not a real thing even though it's in production code it's not real because it's got fake pricing in
it so um so uh so the two directions i'm thinking at this point is one extract product pricer as um as an interface to
be what's basically a port in the hexagonal architecture um that's one direction the other direction is to just make it
a stub no i should do that let's let's do that okay so let's go and we'll extract interface we're going to rename the
original class because this implementation becomes a product pricer stub and it actually moves to so price 4 moves
because that's basically the the method um i yeah so i kind of figured uh some of the references to product pricer that
didn't get updated um product pricer interface with test all right cool so now uh in our test it's a product pricer stub
which is a which is appropriate and so now we can uh we can start messing it with it without feeling like we're
modifying production code so again our goal was to sort of make visible these hidden prices right so that way because my
goal when i'm writing tests whether it's test driven development or not my goal is writing tests is that you should be
able to look at this test and know everything about why we're asserting what we're asserting right now it's not evident
why this is one so what we want to do is we want to uh make it clear that the product pricer stub that we want to make
it clear that it's so let's go back to our stub i'm going to oops so i think so it allowed me to ex oh because the put
what is that going to do yeah that's not going to do what we want um so let's push out this upc and so this so how do we
want to use the stubs uh i think we want just the constructor to take pairs of upc and price so we'll do that and then
uh so our goal is to get rid of these basically these constants and i think we can basically re-inline uh re-inline
inline i'll basically turn these back into into the strings oops and so now um if we look at our test so let's go and
pull this out pricer oops i want to extract a variable product pricer we could replace the strings with with these
constants uh but i think actually i'm going to inline it and then we'll re create so now we have is let's do that fix
our formatting so now we can go through test by test right all of our tests should still pass so now we did this all
through refactorings right so none of so even though these are sort of structural changes we're able to do it um mainly
by pushing out these parameters to get the stuff into our test and now we can play around with it from there but now at
least it's evident we may have too much information right so for example cart total price is zero and is empty um we're
not adding products so it doesn't matter what the product list is so in fact we could have an empty stub but we'll need
to have a constructor that handles that so we'll have to fix that but right now since everything so pushed out
configuration of product or stub two colors now i can start cleaning up the test so here this first test i don't need
anything i just need an empty stub in fact it almost should be um so i could replace this stub with a dummy so null is
is okay as a dummy um not great but this test should still pass because it we never call add products the product but
what i'd really like is i'd like a product pricer stub that basically starts out as empty so let's do new product pricer
stub and we'll create an additional constructor we'll sort of reinitialize it back here and take this out and so now
this is a no art constructor with all right so created no arg vector product that took care of that test this test all
we care about is this so we don't need this product so we can take this out except uh we could convert to var args um
but then we'd have to sort of pair these up and that gets kind of awkward uh so although it does mean it does it is
interesting because there is a code smell of like these are some kind of parameter object right this is actually like
product a product class which is when i did tdd inside out i ended up with a product class and it looks like i might end
up but that's kind of too big of a change at this point i'm just refactoring so i'm going to just create another
constructor that takes just a single upc and its price and i know basically the test should still pass and it does so
created single so now this test is self-contained in the in terms of the information that it has right we've got one two
three here uh and one two three here and so we could extract this back out maybe red crit uh spock tests um i'm not a
spock test fan and nothing against it i'm just an old java guy and that's all i know all right so here this test
actually uses both um both items in both prices so let's go let's pull this out into the other which is tooth uh and
that's fine and then now this is redundant so let's um although if we do that that again hides so let's let's leave it
i'm actually so this one um again doesn't need the uh the other item so we can leave it like that so so now we've
achieved our goal right all through just refactorings of these tests are now self-contained right you know why this is
three because the three here matches the three here you know why this is one plus three because it matches these here um
ah that way i get the order of toothbrush toothpaste here if we know it's one so let's look at our other tests um and
right now we only need one product uh do you try bdd way to uh tests like g unit um so i haven't this in all of my tests
is sort of an implicit given when then right so like this test here given a product pricer that has these prices uh and
a cart service when i add so given that a product has been added to the cart and when i finalize the order then the
receipt total should be one right so all of my tests have those three parts whether they're bdd tests or tdd because it'
s a spectrum of just what level of abstraction what level what layer of boundary you're working at could also use you
know cucumber gerkin language for for some of that i don't i'm not crazy about it um i just don't do enough at that
level and so i tend to write all my tests using junit even if they're more bde-like all right so let's commit uh let me
finish cleaning up that test um so we've separated out product pricer we actually don't have a concrete reel
implementation uh and we might not have one for a little while um but now at least our tests are readable in isolation
uh and that's what that's what we want so um let's go back to our receipt let's now get to the point where we can
actually have multiple products in our receipt so we're keeping track of so we want to expand this tests where the
receipt is not only returning uh the total but also we want the receipt to have um items products products contents yeah
i guess i'm not too concerned about pretty formatting in tests um but again it depends on how your your team or
organization is structured uh how useful useful that is so um products doesn't actually require a separate method it is
basically just and that um so i think right now the only information we have uh is the upc we don't actually have the
name of the product um that's actually what we'll probably use uh the external service for all right so i mentioned way
back hours ago that i have this actually uh that there's a third party service where i can give it a upc and it gives me
all sorts of information about the product so i can use that to give me to for us to fetch the names uh as as we need it
so maybe a fancier receipt it can also give us categorization so i don't know about where you shop but where i shop um
often the receipts that i get at the grocery store are organized and cut into categories you know here's your dairy uh
here's your meat here's your produce um etc and so uh obviously that's not the way you scanned it but it i obviously
kept it and then categorize it according to whatever taxonomy they're using so we could use but for now uh we'll just
use that in fact let's pull this out into constant so uh clearly this will fail because products is gonna in fact it
won't even compile because over here um we don't have anything so let's do the minimum do we get due to get it to uh
collection something list that's weird don't know why i didn't expand empty list for me so now this will fail because
it's going to be empty instead of containing our product awesome fails exactly where we expected uh now we um uh we can
start down the tdd road of sort of zero one many so we had the zero case right finalize order um we could have examined
the receipt as well um and so maybe we'll we'll step back and do that so let's now that we know we're sort of in the
zero one mini case let's start out with with the zero case so um start with uh no products finalize order well actually
what do we want to happen if we finalize the order and no products were added so we can't actually do the zero case yeah
we have to do the exception case well that's part of zombies the z-o-m-b-i so boundary conditions and exception cases uh
so cart with no products so we're saying that if we um uh we'll do that we can actually have an empty stop because we
don't care about the product pricing uh we basically finalize the order um uh oh do i have not done my postfix there we
go so we're going to say what is this card is empty exception no products in and right now it's there uh i'm gonna say
extends runtime exception uh yes i did surround it with a third that thrown by you did not miss anything um so i have in
my post fit my surround templates uh so i can basically like select it use a custom template so having us surround with
a cert that's thrown by so these are live templates as opposed to dead templates but um so i have a bunch that i've
customized so if i just do att it'll expand but there are also surround ones over here that you can customize so i've
got i can surround with assert that i can surround with assert that thrown by so it takes whatever your selection is
sticks it in there fills in the rest uh and then leaves you so post fix uh live templates um are ways you can customize
uh things to make them to make intellij much uh i thought i had a post fix where i could do atdb um because i have the
latest production on three different lines plus the early access i've got four different ones and sometimes it's hard to
copy configuration across all right so we got this test this will most certainly fail because we're not so fails as
expected oops so let's go to finalize order um so we're gonna do the simplest thing we could do to make that work which
is if uh if it's empty then we'll throw a new uh no products and card exception no uh did darn it the exception got put
in the wrong place hold on this is in the wrong directory keep forgetting to check that when it creates it let's try it
again throw new no products and card exception all right so this should make the test pass yeah at some point so i base
so in my discord i do have a dedicated channel to intellij so if you need help with any of the file template stuff or
anything like that uh go ahead and ask in in that channel all right so this test passes um i wish it were a bit easier
to share some of those things with sort of like friends and neighbors as it were um but all right this tab passes um
finalizing order with no uh finalizing order for empty part uh let's see you know this place for so then that's our zero
case which is basically it's invalid so now we've got which should still fail oh i didn't refactor hold on uh let's
refactor this is uh require part not empty all right now this fails the last item added um that was basically a
refactoring of sort not really i mean i mean it didn't affect behavior so you could say it's a refactoring but it didn't
quite get us towards where we need to go but now we can basically change this so now we can uh multiple so cart with two
products so i'm going to go grab something from here and the fact that i'm copying this from here is signaling to me
that i might want to refactor the creation of this stuff um okay so we add that and we i guess i could the toothbrush
twice but that might be unclear about what my expectations are so here contains exactly that and toothpaste uh so this
will pass because it holds things up correctly uh this will fail because it's only going to store the last item so when
i predict that this will fails um i'm predicting exact exact specifically that the toothbrush will not be there anymore
and it is because the toothbrush is what again honestly these are strings i could just replace them with a name but i
want to sort of keep this idea that they're a number okay so now clearly storing just a single item is not going to work
so we can do this as a prepare refactoring right and transform this from a string to a and then this becomes
products.add and then this is just products and this we have to say is new arraylist this was just a refactoring the
fact that we're storing an item and only one item in the list it does actually slightly change behavior um so in a sense
this is not quite a refactoring because we've expanded we've genera we've actually generalized this we could if we
wanted to be precise about this instead of doing that here here that still passes but it doesn't generalize the behavior
around holding on multiple items because what i want is i want this test to still fail because that proves that the code
that i'm about to change or add actually is being tested and exercised by a test so i've seen this now fail now i can go
so there's some refactoring that i'd yucky um there's a lot of different things we could say this resets cart but if i
refactor that to that it actually isn't going to take me towards where i want to go which is basically going to be to
have a cart object in in our domain but what we have now is we've got in our application so receipt is really a domain
concept so it's currently an application but actually it doesn't belong there so let's let's take that and let's move it
um it's like it's a value object but it belongs in our domain so let's go ahead product pricer is a port it's an
outgoing thing right it's right now it's in we don't have an actual implementation but from a hexagonal architecture it'
s an external thing so we'd want it to go through so in fact we wouldn't directly talk to it we would actually talk
through through a port ah that's how i change it okay okay and then we would have do so we'd have an outbound adapter um
that can go fetch basically our price fetcher or pricer uh would go and use that service but it has no knowledge of the
specific implementation that we would eventually use so that means product price or the interface because ports are
interfaces would actually go it's part of application but i tend to segregate these outgoing ports into a directory card
services application although it's still this messy hybrid of things um no products and card exception uh so that
happens when we finalize it's unclear right now is that application level or is that domain level since i don't know
i'll leave it in application eventually we will have a cart object we will likely also have a product object of some
sort so let's go ahead and do a commit um refactored packaging according so that's all for today um tomorrow uh when am
i streaming next not tomorrow because i am busy tomorrow uh wednesday yeah so wednesday i'll probably stream part two of
doing hexagonal architecture we can probably get now to the special deals right because this required us to have sort of
knowledge and memory of and sort of the history of what items were added and now that we have that at least in a very
limited way we can now start focusing on that probably go implement the the product pricer we won't use it to get
pricing per se we'll use it to get information and sort of enrich the receipt uh with product information because right
now all we've got is upcs and we can call out to the api and get names and categories and then do some interesting stuff
with uh with that so that'll be sort of the first part of implementing something external to what's really our our sort
of core application which is in here um and then we'll uh create a sort of tester web interface um although i guess we
could do it as a console but but i'll um we'll bring in spring boot for this and we'll create a you know sort of
actually maybe we'll just use do an api uh so um that way we can actually do it from from within intellij use its uh
http um message uh requester sender kind of thing so we can do everything inside there so we'll create a rest a rest
like api um as as our adapter and then that'll uh i think that'll be a good next step all right so thank you so much for
hanging out um and thanks again uh uh to all the folks who um who subscribed and and thanks to jeff brains i'm they're
long gone uh for the the ten subs that was that was awesome um and uh who else sorry uh they changed the ui that's so
weird um uh oh and to to catalya for for bringing over the awesome set of folks who and some of which who hung out until
now so
