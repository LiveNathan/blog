# TDD & Hexagonal Architecture Exercise： Supermarket Checkout Pricer - Part 4

**Video URL:** https://www.youtube.com/watch?v=iMYKE0shabc

---

## Transcript

right folks welcome to today's stream um it helps if i hit the right button that's all i can say uh so uh today's stream
is later than i usually start a stream um but this week um sort of in the last stages of getting my uh refactoring
hexagonal architecture course uh page and some of the material up so a quick preview of what what that page is going to
look like is this so this is my self-paced version of the class so this is the class that i usually teach that actually
is now two a little over two years old that i've been teaching it live to folks and i've taught it pretty close to 40
times now and over the past couple years it's been improved and lots of lots of good feedback and adjustments along the
way both as i get better explaining it as and also better at understanding it um so my goal is to get get this thing
launched this week uh but today um uh so that means um i won't be streaming earlier in the day uh because i want to
spend all that valuable uh fresh brain power on on the course uh and i'm fine with having very little brain power left
to to stream with because if i uh end up not having much brain power for that that's not as big a deal so today what i'm
gonna be working on uh is continuing with the supermarket checkout pricer that um i had started on a few weeks ago uh so
we're up to part four so last time we worked on uh getting sort of the the domain layer and the service layer all set up
so let's take a look at that code uh hey there costa daniel welcome so we've gotten our discount fetcher so our outbound
port defined and we had a stub implementation of it for testing purposes uh so this is our interface or in our in our
application port um package and we also have a product price fetcher so we now have a way to fetch uh the product price
as well as a discount and so what i sort of had sketched out last time so last time um so we've got in our domain we've
got this stuff right we've got our cart our products the receipt which i forget where we left that and we have sort of
discount rules i don't think we've quite implemented this yet but we have uh both a discount fetcher and a product price
fetcher as outbound information requests and so what we want to do with those is we want to stub those out the other
thing we need to do is create an inbound adapter so that we can get input so that we don't drive everything through
tests it'd be nice to actually see a little bit of of some kind of presentation for uh getting input about what products
were are being added to the the order for that i'm probably gonna just create a quick and dirty uh time leaf template
spring mbc page um and we know what's nice is we know uh how that adapter is gonna call into our service once we have
that then we'll start implementing some tiny serve tiny services i hesitate to call them microservices because they're
not deserving of that at this point but basically small services that will run separately out of process uh for which
we'll have to create um some stubs and then some real implementations so we've already got the stubs for um for our
product price fetcher uh and our discount fetcher so we've got uh stubs for those and so uh once we have a proper
inbound adapter then we can go ahead and create uh these little uh sort of tiny services that will run separately but
for now let's focus on want from that is basically our cart service has an ad product method and it basically takes a
upc so this is going to be pretty straightforward just going to need a very simple way to have an input field of some
kind of numeric field that will allow us to to type that in so really not much to it but it will be a proper inbound
adapter so um no i don't i didn't add that to this project yet okay so let's see everything is committed yes by the way
if you want to follow along with the project uh the source code is up on github uh and it is on a branch that that link
will take you should take you right to the branch that we're currently on uh so what we wanna do uh is introduce a
framework we don't have to introduce a framework we could a console based adapter my terminal basically have terminal
input but i think we will jump right to uh a spring boot front end mvc based uh input adapter so for that we're gonna
need to bring in some stuff into our palm file um we'll probably have to mostly blow away so so actually what i found is
the easiest way is is to go to uh the spring initializer that and our artifact is that uh supermarket check out racer
same thing with the name so let's call this um i think we're on version 17 anyway 18 uh so let's add some dependencies
um no no lombok uh and we want spring web um and we want time leaf as our template i don't think we need anything else
we don't need any database stuff just yet um yeah i think that's uh let's bring in validation because and we'll since
we're going to deploy it at some i think that's it so uh i don't want to generate the whole project i actually just need
the pom file so we can go ahead and explore and we can basically copy and paste the pom file because right now what we
have in our current pom file is basically junit 5 assert j and that's pretty much it and so we'll get all those as part
of the spring the spring stuff here so copy that and we'll pretty much um that might muck with the name of the project
here but i think we're okay so first time i'm using 271 so it's got and i don't need to call it a snapshot um so let's
run all our tests and see all right super fast tests uh added spring boot all right so now we've got that now uh what we
want to do is um the um the application file so let's copy that and we can drop the package info we don't need that
right now and then we want our basically the temp the little test that basically runs the make sure that spring starts
up so let's put that in our test directory whoops i put the application in the wrong directory let's fix that that goes
here and then this goes here all right assuming spring is set up properly and it is the long longest test about this
most time consuming but that passes so the first thing i want to do since we're now uh before we brought this in all of
our tests were unit tests in other words they were all running in memory with no access to i o but spring is a framework
that has lots of i o stuff built in so it's considered external which means i consider tests that that use spring to be
integration tests so my definition of integration is does it touch a framework or does it touch i o or hardware and then
it's integration lots of people have different definitions those are mine i like them i find them useful as a way of
thinking about the tests so what i want to do is i want to tag and that way i can set up my test configurations now
we're going to do a little bit of work here so what we want is these are going to be so i often put just in front of it
because that makes it clear that these are just the unit tests um and what we want to do is we want not all in package
but we want tags and what we want is anything that's not integration so those are our unit tests i'm going to go ahead
and store that as a project file so that'll get added to the repository a copy of this and the difference here is it's
data refreshing you get pt haskell ptsd sorry about that um and that's it let me get rid of these other ones and i'll
store this as a project file that way it's in the repo that's all good checkup pricer okay it should be 14 tests that
run really fast and it is and if i run the integration test that should run one test that's relatively slow and it does
so let's do a commit for that um what have we got that's on version uh added that's weird uh added uh spring boot
application bootstrap and fast split past configurations great so now what we want is we want to be thinking sort of
outside in right because what we're doing is is we're now working on this inbound adapter so what do we want from this
inbound adapter um well we'd like some page that when you navigate to this thing there's going to be a page it's going
to have an input field um and that and basically a button uh i'm not going to worry too much about styling it right now
because that's that's a rabbit hole um so the first thing that we want to do is uh write a test against an endpoint that
doesn't yet exist so let's go ahead now this is uh adapter inbound so we need to do is we need to start creating some
packages for that so let's go ahead and create a package in web so i'm getting distracted by this uh it's always
annoying to have like can you let me finish typing before you validate but whatever uh so we have an inbound adapter and
it's a web ui adapter um that's the the technology technically i should name it like inbound product scanner because
that's sort of the the thing that's coming in um but i'm gonna leave i'm gonna leave it as as web and let's just create
it here for convenience sake in our source code so adapter and web all right um i keep forgetting to copy my template
for tests so let's create a java class and this is going to be our product banner controller controller is an overused
word but most people get confused when i use something else so even though i would normally call this something like
just product scanner people get confused when they're looking at the code if they're coming from other spring boot
projects where it's like where's the controller so i'm going to add that on and this is a test so we'll do that uh we'll
go ahead uh do anything else i think that's it for now so let's write the test uh so the first test i want to write is
what happens when i go to the root of the application so get roots f returns what i want to return so this is going to
return a page that will have a four minute i'm not going to be testing the contents uh because that's a little bit out
of scope for for the kind of things i want to do uh so get a root path get root paths then returns um so we want a 200
that's all we really care about at this level so we'll do uh oh we'll need to auto and on that we'll do a mock nbc
perform get i i hate this style of writing tests and this is why i actually do so little testing uh with the mock mvc it
takes very much the the ham crest approach of let's do everything as statically imported uh and i always forget where
the heck it is let me go to my um oh it's web mvc test that's why it's not working um and what is the import for that
where is that there it is okay i swear if you don't use something for like a week let alone like a month and you totally
forget everything uh so this should be what it is webmvc test i don't know why it's not like letting me import that so
we'll comment that out because we're not using it i don't know why i wouldn't wouldn't bring that up hey there david
souls welcome glad you're here and shygon tv welcome um okay so so it's pretty much this test right where we basically
expect the status let me pull in the status so put that in here and so we want is and expect status so this test will
fail right so we're doing test driven development even though we are working on what i would consider an integration
test which reminds me let's tag this as integration right because this involves framework which generally implies
hardware i o infrastructure this is an adapter so is um integration you can tell my my brain is already not at full
power uh but this test is this is basically how we kick start creating our controller because the controller doesn't yet
exist so if we run this test it's going to fail and i'm going to run just this test individually we'll watch it fail it'
s going to return a 404 because there's not no controller so that's our expectations that gives us and indeed that's
what we got great so now we want to make the test pass and the way we do that is uh no we don't want product what we
want is a um product scanner controller all right and let's flip that over okay that's the test we want all right so to
get this test to pass we need an endpoint return a string because we're going to return the name of a template
eventually um and so this is uh we're going to return an empty string eventually we'll need to return the name of the
template because time leaf does not like the fact that there's no template mentioned here but what i want is i want a
different failure right so previously it failed because it was 404 now my expectation and again this is where i use my
predictive test driven development process now i expect it to fail because the temple is not found so different failure
still a failure but making small steps towards getting it to pass see and indeed it failed uh and it failed for the
right reason which was um there was no template with an empty name so let's go return one with a name and we'll call
scan this will still fail but now it's going to say can't find the template for scan so that's that's correct now we'll
go put this in the right place uh so this goes and underneath we'll go and create directory resources templates and then
in here we'll create an html file and this will be our template uh i'll have the form later right now i just want to
make sure that now the template exists um this should not work so intellij is happy because now it's changed it from a
wiggly morning to uh to a link so i can jump right to the file and it does great so now i am done with so let's go do a
commit since we've got a passing test um added endpoint and in my course uh i talk about how when you're testing inbound
adapters you can test drive them because there's actually two different things to test there's this framework
configuration that i set up my endpoints correctly and then there is my unit test which is state-based checking to see
did i hook it up to the application correctly so we did the framework configuration part right we had our controller we
had our get mapping now i want to write a unit test even though it's within an adapter right that's outside of my core
domain it's still a unit test so we'll do is we'll create um let me rename this test because this is really not a
controller test this is the um which is just a product scanner controller test flip that over to the other side and what
we want to test here is well the first thing is if i call scan product it returns the name of this page because i'm not
testing that here i could i could do view name but the way i look at it is i want these tests to be as small as possible
and often just like two lines like this is good enough that make sure i configure it correctly now here i can write a
test which is scan product returns span template so basically instantiate our product and so given our controller when
we call then we can assert that the page is equal to scan so here this test is going to pass which makes me a little
uncomfortable because i like to see my test failing but that's fine but i ran the wrong test let me run my all right so
that passes let's make sure it fails by putting nothing in here this should fail just make sure we're calling the method
and we are so we can all right let's do commit because we've got that but that's not all we're going to do because we
want to do a bit more with that right we don't just want to return empty page that's not enough we want to return a page
with a format so um we're going to need some some model stuff let's go ahead and do commit so now what we want to do is
we want to insert additionally that this page has a form in it and that form so we'll hand in model and we can use
spring mvc's concurrent model this causes a compile error so we fix that we run our tests um nothing should have failed
because this was basically a refactoring we added a parameter that's not used should not have changed behavior but our
goal is to change this test so we do get new behaviors now in addition to asserting what the page is returned we want to
assert on the model that um well what do we want to assert on the model what should the model have the model should have
uh some attribute that is basically the epc so contains attribute and we'll call it upc i guess we don't necessarily so
normally um for any non-trivial page where you're using spring mvc and like a time leaf template you create a form
object but we can start out with just like it's just a request parameter it's only one parameter we don't need an object
to store that uh if we want to do validation then we can go to an object but right now we don't need to do that so but
this is the get of the page so actually do what do we need we do need the attribute upc to be there um so all we care is
that the attribute exists we don't actually care what that attribute is so this will fail because attribute and now we
can go ahead and add attribute of upc not ups so if i typed ups and i thought i got it right right obviously the test
will fail so make sure your tests are specifying the right thing so your test fails so now this should pass because now
i've got an all right so now that i've got that what i want to do is um basically create the page uh i could just
display the ubc but i may as well go ahead and create the whole form so let's go ahead and create a form um this method
is going to be a post and the action oops is nothing because it's going to be the th action that's going to be we'll
post right back to root and inside of this we're going to have which is going to be a submit button and it's going to
say uh add product i was going to say submit but i'm like no i don't want submit let's put we'll say product uh we'll
say upc type is text and here's where we'll link it to um the field that we want so th field is going to be um epc there
we go so we can preview this page just to make sure it looks okay so let's do that yep that looks fine uh now that we
have this page and we're putting something into the upc uh we should be able to run the application and see the page so
let's do that hopefully i don't have anything else all right so we see our page now if i click the add product we expect
it to 404 because it's going to do a po well no not 404 the endpoint exists we should get a is it a 415 or 401 i always
forget what we get when it doesn't support post but it does support get it's one of the two 405. and post is not
supported so that's exactly what we what we expected so and do a commit where we've got um new behavior uh and product
page now has a form with input field for upc uh davidsol's notes time leaf that's what this th field is doing and this
th action but remember that time leaf is html that's one of the great things about time leaf is it's html if i try to
preview it the browser ignores the th stuff i actually need to add the th here i always forget to add that um do i have
i guess i don't do i not have that xml i do have it i just always forget what it is so it's xmlt okay let me do that so
xml th there we go okay so now it's got the namespace um not that um all right so we've got our namespace for the
timeleaf stuff we've got our th action so it knows where to post to um and it's got the field so now what we want to do
is we want to create a place where that field is going to come in so we're going to this is going to be new endpoint is
going to be our post endpoint so we go back to our oops let's do that so this is our uh so we need not this but we need
let me close some of these i don't need these yet uh we need our mvc test and we're gonna run another test like this
just to test the configuration so uh post to root path um now when you do web apps as opposed to apis uh you need to do
the post redirect get pattern um otherwise you get into all sorts of weirdness so post root path uh is uh redirect
that's what we want so mock mvc perform we want to form a post and when we post to that we expect uh the status is
redirect i don't care which redirection it is it's just one of them yes uh i have used htmx and it's it's quite nice i
won't be using it in this project because i don't think it's needed but hdmx is quite nice all right so this test will
fail because we have no endpoint so we'll get a 405 right because we're posting to an endpoint that doesn't support post
so let's run our integration actually and so it failed as expected with client error 405 as opposed to redirection so
great so let's go ahead and create our post mapping to slash uh and this is add product now add product is eventually
going to take string as a parameter but right now there's no test that's forcing us to do that so we're not going to do
it right because we're doing tdd we don't do we don't write code unless there's a test a test failing um and when we do
write code we write the minimum amount possible to make the current test happy so here all we want to do is we're trying
to redirect and we'll just do that as a redirect string this should be sufficient i don't know can you make it is
totally resolved view that's interesting what if i do redirect i guess that works so that's good because that's less
than slash um although i have no idea where is it where does it redirect you by default i assume slash i don't know uh
but i tested passing so let's go um host endpoint but we'd like it to redirect to slash so let's go into our other test
so this is um add product redirects to root it's going to do more than that and we'll call it product scanner controller
add product what we want to return is a redirect to slash which it won't do so it'll fail so let's go ahead and run now
back to running just unit tests right so now we're back in unit test land which means all the tests run really quickly
right so i write the minimum amount as integration tests right only a couple of very short tests and i do all the heavy
lifting in my unit tests because they're easier to work with and faster to run all right so still don't know why
intellij is complaining about that slash but whatever that now passes let's go ahead and do a commit all right so what
else do we need so we've got uh so if we run this we should be able to click a button uh click the add product button
and i'll just redirect back to the right so trust me it's redirecting back so now what well add product should actually
add the product um so uh we will want to write a test where um now we get into a bit of of trickiness so so far this
controller has been completely independent of the rest of the application we would like it now to hook up to the um to
our basically our application layer all right so we've got our adapter but nothing is yet talking to the application
layer right it's just we can handle incoming requests and it calls the right method we've got all of that and so what we
want to do is we want to hook it up to the application layer major schools of thought on the kind of test that i would
write next and how i would write it one school of thought is right the application layer which is a service you would
mock it out and then basically check for behavior interactions so you create a spy and then look to see did our
controller call the expected the other school of thought is you basically instantiate and then check the state of the
system to see did the state change right so basically behavior checking really not even behavior checking it's method
call invocation checking or state-based checking my preference because i'm very much of the classical tdd mindset i
prefer real objects is we need to write a test that is going to encourage us guide us to create that so we want more
than just add product redirects to root add valid upc um really it's post valid upc then product um sorry i was just
looking at this error message that's weird okay so and what we want is when we call that controller add product um so
let's go grab one from our which probably means i should put that into a more central location but that's fine we'll
leave it here for now let's make this compile so we're going to add a string but it's not going to be up toothpaste upc
it's just upc uh the default value we're just going to have as an empty string so what this is going to do this is
basically a refactoring it's going to add a parameter it's going to change the signature so all colors will need will be
changed to pass this in as a uh davidson's means need to boot tomcat now tomcat is not needed actually for any of my
tests i'm not the mock this test is not running uh tomcats running the mock mvc server this is not running any server at
all it's a pure unit test it doesn't all right so we've added the parameter what is our expectation um we don't care
about checking the redirect we already have a test for that the cart so we need access to the cart so who has access to
the cart now the card service takes a price fetcher and a discount fetcher right now i'm going to pass a null for those
basically these are dummies eventually it's going to get used but right now i want to get my test to pass and sorry my
test to compile so i can all right and so now i should be able to um so i can either look at the total and see what the
price of the cart is or i can look at finalize order and see if we do that that's a little bit more reliable because
we're looking at what actually was added not just necessarily the price so so we'll do is we'll assert that uh exactly
or only i think it's exactly so make sure i always forget the versus ah so contains only ignores duplicates i don't want
jupiter i don't want to allow duplicate so i want it contains exactly um what is this return a string um that doesn't
help me much what does uh right so it just returns the upc's perfect so we just want to make sure that that contains
exactly our so notice that the basically the side effect as it were right the outcome that i'm checking is that if
everything is hooked up properly there should be this so this checks really that add product not only pays attention to
the string but does the right thing with it now you could use a mock to do that but i see no reason to do that because
really i want to make sure not only does it call the method but that turns out to be the right method to call so you
could mock it up and say it should call method x and really should be calling method y to have the outcome that we want
so i am generally writing like 98 of my tests don't use any kind of uh mocking framework because i don't need to all
right so this will fail for a bunch of reasons um mainly which it does nothing with the upc uh yeah so that's that's so
this will this will fail because well it didn't do anything so let's run uh let's run our unit test because this is a
unit test it should fail because it's not there and we basically got a no products and card exception because when we
tried to finalize order it asserted that there was a product in there therefore there wasn't a product in fact we
probably could have started with an even simpler test just make sure no now uh we need to do a few things so we need two
things we need um product scanner controller needs a reference to our cart service right and that's what we said we
needed right our controller it needs a reference to our application services layer so let's wire those up but that's a
refactoring so let's disable this test temporarily get back to green and then we can do refactoring all right so our
refactoring is basically that we want to hand in cart service now this red wavy underline is spring is a spring issue
but we don't need to worry about that just yet all right so we have a reference to cart service we're still not using it
um but this should result in no changes to code um so this is why i do this when all chests are green because i can say
oh actually i could have done this a different way so let's do it a different way so what we're going to want is going
to we're going to want a reference to cart service what we really want to do is we want to create the constructor with a
parameter that is going to be valid for the other tests so let's create the constructor in a different way let's create
constructor here just a no argument one and what we want is we want a field for um let's actually uh so we can get the
rest to compile this should be no up right all the tests should pass so they do but we don't want this cart service here
we want to have that eventually auto wire but initially right now we'd like it passed in as an argument to the
constructor so this is where we use a refactoring to expose this hidden detail so we'll introduce a parameter and now
everything should still compile and work everything still should compile and work other than our disabled test but that
was a refactoring so we can go ahead and commit and say introduced cart service to all right notice the unit test passed
even though intellij is complaining because really spring is going to have a problem auto wiring this that's not a
problem from unit test point of view to trying to make spring work all right so this test we can now enable and now it
should fail because we've got the card service reference but we're not using it here so it should fail in the same way
where it throws an exception with finalize order right no products are cart perfect now what we can do is we can add the
one line of code here cart service add product upc assuming i did this correctly it should pass ah so now my dummies are
blowing up and that is actually should not have been surprising because in order to get the price for that it needed to
call um a product fetcher but for this specific test i actually don't care so let's do this let's create constants for
the product price fetcher and and let's go ahead and replace those in actually i don't know if i need to do that let's
we'll see and so for these instead of null we're going to say we're gonna basically use some lambdas to say that uh all
prices are zero what i wanted oh it wants a discount roll okay so we basically have these are um these are basically
dummies so let's all right so now uh this test will fail actually this test might pass this test is going to be
problematic because it doesn't have the the correct card service so let's give it a card service let's pull this out
into a variable and it does so now i know that my controller is properly hooked up to and calling the right method on my
application service now we can run all the tests uh actually i should create an all test so our spring tests are going
to fail because it can't wire up this thing so that's not surprising let's go edit this this is all tests store that in
the project file so now we need to do some work to to make spring happy so even though it's auto wired by default
because spring boot recognizes that's a constructor that it's going to need to inject i like to put the at auto wired
all right so this is complaining because cart service is not a class that spring is aware of and it can't be because
it's in application and so anything inside the hexagon right anything inside of this layer application layer and core
domain cannot reference anything outside of the hexagon including frameworks so i need to wire those up together but not
inside my hexagon but as part of an app bean and what we want to tell spring is hey a cart service go ahead and call
this method now for now uh which fetchers do we add here so that's a bit of a problem um we need to add something here
otherwise so uh we'll need and we could sort of convert those to in memory right so we've basically got our product yeah
so those are configured configured at startup but those are in our test directory so this this stub and uh the stub
discount fetcher are uh i should be consistent about my naming here i've got stub discount fetcher let's rename this
because i don't like all right let's run all the tests we still expect the spring test to fail um oh right now we're in
the middle of finish uh creating this um so we could actually do this just to get at least some of the tests to pass so
spring is fine except one of the tests that does the post does an ad of the upc and then tries to call something on
product price fetcher which of course fails but for now we can actually replace these with again sort of a um and that
should that should at least we'll have to figure out what we want to do about these do we always want to like we need
something there do we want um even if the services are available and up and implemented do we always want to hit them or
do we want to be able to run this application locally without having to go out and hit external services and kind of
without having to run those other services so in that case we might want in-memory versions of those but for now all
that i cared about was so implementation all right so we now have configured spring to tell it hey if you need a cart
service call this method this is um i usually put the application sort of bootstrap startup in the root package because
generally this scans files all the way down there are other ways to do it but this is how i usually start doing it and
then our controller then is now happy because it talks to a cart service and we can add a product so the next question
is do we want anything else from the front end all right so we've got a way to type in a number and have it added but
from the ui we have no way to see we could ask the cart service for the total price and inject that into the page so
let's do that we don't currently have a great way to get the products that because we sort of don't know what they are
until we actually ask for the receipt at some point we'll probably need to fix that but for now um let's do it so that
when we scan a product uh in addition to having an input field for the upc it will also show the current the current
price all right um so does that change anything from uh well because right now we weren't specific and explicit about
where does spring get this string from now it'll sort of automatically match it i think i always forget what the default
um let's actually try the application because i always forget is this good enough or i do do i need to tag it with so i
believe i need to specify but i always forget um should we should probably validate our our incoming upc so let's do
that um then that'll help us ensure that that it's working properly so if we want to modify the behavior of this we need
to go to our test let's go to our test uh post invalid upc then what do we want to do um uh so we're about to do this
again so let's extract this to a method um or sorry at least the cart service great cart service and then here we can go
ahead and find duplicates and replace that and we can just inline that okay and let's move this down to the bottom where
we like our private method great basically inline this oh no i don't want to inline that i'm and then what i want is a
product scanner controller add product so this um and we want to assert is that the page is equal to redirect error i'm
not going to bother creating that page we'll do something more sophisticated where the refreshed page here would show a
little error message but for now this is sort of easier to detect so let's run our unit test this should fail because
we're not redirecting that uh we want essentially blank so if it's blank we want to redirect had product now fails
because it was passing in uh that so let's have it pass in an actual valid uh he needs a pretty okay yeah that's why i
chose this blank um eventually we'll do more validation than this but right now i'm kind of trying to create this the
simplest possible uh input here i'm not gonna worry about anything i'm not gonna worry about anything else because i'll
have a when i set up the annotation i'll have a default all right so all our tests pass let's go ahead and that's new
behavior um so now um if i run all the tests my mvc test here um i think that'll pass because it's going to redirect
either way i'm not actually checking where it redirects to uh ah okay so here um it is null and we want to protect
against that so there are a couple things we can do we can say look let's not pass in an invalid thing um let's actually
pass in a param of upc being so normally i don't check the redirected url but here what i'm checking is is spring am i
redirecting to the right place um so apparently that's sufficient however i don't ever want null um and i could write
another test to force me to do that so let's let's do that let's temporarily comment that out so this should now fail
again with the null and it does and now let's do uh and we want name is upc that's such a weird default value so now
this should pass because by default the value is is empty and so when we do is blank yep so redirect it to error um we
could actually leave it that way and change our expectation uh but we might add more parameters so all right so now that
we're adding the uh at request ram to provide default empty string for each incoming all right so now we're sure that
this method is integrated properly with our framework so that means uh we can now go back and say what do we want our
home page to display uh we would like it to display the current at least total price the total yeah the total cost of
items products that have been added to the cart so that's going to be another attribute so let's go modify our tests so
when you're doing tdd as a reminder you don't always add new tests so someone on my discord earlier today asked such an
awesome question and by the way my discord is free totally open for you to ask questions about the stuff you see here as
well as anything related to java spring hexagonal architecture etc so the question was asked is is how do you tdd
removing features and removing is a little bit different but from the point of view of a test you basically want to
recreate either modify an existing test or write a test where you want to it's currently doing something like maybe
you're taking away an endpoint so it's currently responding to that endpoint with a 200 or maybe a redirect and you want
to change it to become a 404 right not found so you write a test for that probably undoing or modifying an existing test
and then you delete the endpoint and the test should pass and you keep doing that writing tests because it's removing a
feature as a change in behavior just as much as adding a feature is yeah join the discord um so what we want to do is we
want to change the behavior uh really it's a little bit of additional behavior where um we want scan product when uh we
do add product that scan product actually we can just say when we first call scan product it should be zero there should
be a total uh and it should be zero so it's more than scan product return scan template returns scan template with upc
with empty upc and so i think again we don't care about what's in that attribute just that it's there just that um sort
of going back and forth do i want to do a little bit more checking i think this is sufficient so uh let's run now just
back to our unit tests so that fails as expected because the attribute's not there um so here we can do model add
attribute total and basically add an entry empty attribute so clearly that's not quite enough so let's modify our test
uh be instead of contains attribute let's have get attribute and that it's equal to zero i actually don't know what i
want it to be is it 0 or 0.00 hey viable clan member let's make this fail and then we'll actually get the information
from the cart so it's a big decimal i don't know how it's gonna to stringify itself oh duh it i put it as an object um
do i want a call to string on it yeah let's let's call to string on it now is it to plain string or to regular string to
plane string hey why'd you do why'd you open that up uh two plane string so now the scale is the scale zero and so it'll
just be zero or is the scale have a default that'll be two decimals let's find out so now that we know that that's gets
displayed um not only does the add product redirect to root uh we could write a test that goes through the whole thing
at this level i don't feel it to be necessary i know total returns the right value because i've got tests against total
uh hey there moolo um i know only how to use a phone you know nothing uh so let's commit because that's a change in
behavior um added a cart total to model upon all right uh and now let's modify our template to actually show it so and
that's going to be as we add items we won't see anything because the default pricer is always zero how about we make the
default pricer always something other than zero so application and let's make every price one all right uh that
shouldn't change any of our tests because our tests don't use that code it won't matter what upc's we enter every
product costs a dollar right a true dollar store unlike dollar stores these days which not everything uh fewer and fewer
products are actually a dollar all right add product um why did that redirect to error um i wonder if i let's let's do
this um so that looks fine so we did a post what was uh holy cow hey strager welcome folks thanks for wow that's a big
party please speak of the virtues of java um java is awesome i don't know java is all i know i don't know if that's
sufficient all right yeah you go you go do what you got to do straighter thanks for bringing your family here welcome
folks um you caught me at like trying to troubleshoot a silly little problem um why yeah acid spark you you you go hide
uh so that's the preview shader what that's the request url that's the post i wonder if that wasn't the original uh and
that was the response but what was the request was the request empty hold on um time i so i knew it was a time leaf
issue because uh i had tests for everything else right so i have tests that tell me um if i pass in an empty string uh
or nothing then it redirects to error if i pass in a valid string then i know it does the right thing so i know all of
my code works i figured the template is where i've got the problem so i'm using th field that i shouldn't be using th
field because it's not a f there's no uh and this is where i'm like always like okay how do i do this in time leaf again
i have a time leaf i don't need you anymore um timeless basics uh so uh not texts value now that's attribute um i mean i
could set the name and value i so let's just do that because i know so name upc uh ph value is the incoming upc if there
that should be sufficient let's try it again by the way for those of you who are uh have have joined us and and hung
around or are hanging around um and are actually interested in java uh i have a discord uh and it's all java all the
time not all java i would say it's 90 java where we talk about java and tdd and hexagonal architecture and design and
testing and tdd and all that good stuff all right so let's try this again uh is the application running no let's run it
hey there ivan tech welcome there we go all right so i don't want uh you despise java well you don't have to hang around
i won't be offended okay um six all right so we can see that the total is increasing um so everything's working fine but
i seem cool with all thanks all right so let's uh let's stop our project so we figured out what was wrong i basically
didn't have the name because it didn't extract it because it's not a fixed form input field or single parameter
attribute in case you were curious about the code you can always take a look at the github repo it's totally open source
by the way i guess i didn't introduce what the hell i'm doing so i'm basically creating an additional set of examples so
an example project for my um for my hexagonal refactoring to hexagonal architecture course that's coming out uh very
shortly pre-sale is going to happen this week and then it'll go on uh they'll be released next week so in order to do
that one of the things that i know as an instructor educator teacher coach is that you can never have too many good
examples so i already have examples in my course from other stuff that i that i use other other applications uh but i'm
basically creating this one from scratch because it has um slightly it's slightly different it basically sort of
simulating a you know supermarket self uh checkout kind of thing so you um scan products which i'm simulating through
typing numbers in the form and then it adds it to a cart it can apply certain discounts uh so sort of the architecture
basically looks like not that uh where is my architecture diagram for this it is this it no this is it uh so basically
this is the architecture um hexagonal architecture in case you couldn't tell by the shape so um here we've got the
product scanner so this is the inbound what's called an inbound adapter and that is pretty much done so that's what i've
implemented um then i have external services so fetching discounts do you get a discount on this product um fetching the
actual product price what is the actual product price uh and then i'll have an outbound uh thing that'll be a receipt
display that'll basically just dump it uh basically the final receipt with all the discounts applied and all the product
information and so that's what this product the project is all about uh again sort of another demonstration example
project of uh uh industrial pom-pom scary yes palm files scare me um although not as much as uh gradle build files cause
i've seen my fair share of horrible confirmation yammel's worst well any ammo is worse no this is why i do not convert
my spring project yeah let's let's not go to yaml uh oh you like my design thanks so uh in case you're interested um in
more information about my course you can sign up in my newsletter in addition to stuff about my course i talk a lot
about how to make your code more testable mainly focused on java mainly from the point of view of test-driven
development and hexagon architecture and of course you can visit my site where i got a bunch of articles about test
driven development and other stuff and yes i was lucky enough to get ted.dev not as expensive as i thought it would be
it only ended up being less than 400 dollars so mine um all right so where are we we've got uh yeah i've i've paid way
more than that for not as good domain names so we've got our product scanner we can now enter it and we know it
interacts with our cart service we know everything inside of here our domain cart and product and receipt and discount
rule we know that all that stuff works because i've got tests for all that now the cart service works i know the product
scanner is now hooked up to it we've got basically dummies or stubbed out fetchers um do we have time to implement one
of yeah let's do it let's implement the separate service i am not going to call it a microservice it isn't just going to
be a tiny service so let's go ahead and create a new project a new project project and this will be a spring initializer
project uh this will be yeah nanoservice charlie does yeah what are we calling this this is our discount fetcher so this
is our discount service discount service uh where are we going to create this this will go in ted young uh guess sure
create git repository java maven dev uh discount i don't need that that's fine artifact discount service that's our
package name one of these days i love intellij um but one of these days they will figure out how to get dialogues to get
to the right size right this is this one isn't so bad where it was sort of cut off there are some dialogues where it's
like really teeny tiny and then have to expand the whole thing all right uh what do we want in here we want none of
those we'll need spring web just because we're going to create a an api a single endpoint api um don't need anything
else there don't need our timely this is not going to that's just going to be a service so there's no time leave
templates needed um do i need test containers for that no i do not i may need to add test containers to this project but
not for the service for the nano service uh i don't think i really need anything else we can delete that we don't need
it what how could help md have a usage unless you're considering the dot ignore file yes of course thank you it's in the
get there now it's not in the there now you're happy great all right uh so um and we want a server port um what port
should we have we don't want to be 8080 because that's the our main services port somebody give me a number between one
yeah 69 of course nice all right always one in the crowd uh so we'll have this at port 8069 when it runs locally when
it's deployed to um deploy to the cloud then i don't need the port but when it's run locally uh that's where it'll go
all right uh so what do we need we need an endpoint uh what endpoint do we want this is the discount service oh i
probably should have written the so i'll need another number for that for that port so new project service and that goes
in ted young which i wish uh ted that that that looks all good and again here all we'll need is just a all right let's
remove this um what version did it pull oh good 385. great okay and uh let's see so i won't need any templates so i can
delete those directories well i'll leave them there they're not going to hurt anything they're actually come on somebody
give me a number your number will be immortalized in the service okay did i really need to to specify an integer because
pi is three right that's what i was told that's what i learned in school all right so got our services um so this
service needs to take an incoming uh upc right uh product code and basically supply um so let's go write that test
because we start with our tests uh so this is going to be basically a similar test to the one we wrote here that kicked
us off on our uh uh let me close discount service because i'm going to get confused if that project is still open all
right and so we want to test so this is going to be uh price service and we'll auto wire in and so our first test is
going to be um so what's got our endpoint going to be um prices uh so prices end point uh so you get your prices
endpoint returns to so lock nbc will perform a get against prices i don't know why um intellij has gotten really bad at
this um i don't know why it's not giving me a better set of values usually it does but now it seems hung up on that so
that's a good name for an endpoint you want how much uh so let's go oh that's not where we want to be let's go back here
so get prices and what we expect is that status is okay things are okay yes i heard about the bmw charging wanting to
charge a monthly fee for the seat warmers i don't know how how tone deaf do you have to be to think that that's a good
idea like how how not thoughtful do you have yeah now i'm already paying for like so i'm already paying for the product
don't make me pay for for for little features um i actually considered that a bug i'm not it's possible that this is a
newly installed version of intellij and so it hasn't quite learned what stuff i use yeah it's like i understand
subscription pricing but you do that for things like you know they used to charge for like you know onstar and and you
know gps stuff of course now that's all included on our phones so we don't all right anyway meanwhile back at the test
so this test should fail because there there is absolutely no possible way this could work there and that's exactly what
i get great so uh we'll create uh our actual controller so this is our do i need the word service in there service is
the name of the app not the name of the controller we'll call it yeah that's an interesting way of looking at this and
just citizenship is a monthly sub um so let's rename this test because it's really about the controller all right and go
back here uh let's flip that over there so the test fails let's make the test pass a parameter but right now we're just
gonna do this we've gone through the empty empty string things let's um what am i saying this is not webm this is not
webmvc sorry this is not a template this is actually an object uh so what do i want um how about i'll just return a
string and it's not at controller it's at rest controller i'm so used to doing uh the assert true is true that'll that'
ll that'll work won't get you very far all right so now this should work it's so funny how i'm just so not used to
writing uh api endpoints these days all right so that passed um i'll push that later i gotta figure out how to do that
oh actually turn that off turn that on there we go okay all right so now we have the endpoint now we got to figure out
what do we actually want uh we probably will never want to redirect uh what do we actually probably won't want to post
either so um right everything is ten dollars right inflation not the dollar store anymore it's a ten dollar store
especially if you're in in the eurozone which is great for me because i'm in the u.s i want to buy something from from
europe uh not so good for me because i want to sell into europe my stuff is more expensive but we probably don't want to
return a string we probably want a proper json blob so let's do that let's write a test for our controller this is just
a regular controller test so let's tag this one as sorry not tag this one this one is going to be a unit test so let's
go ahead and create uh let's run that's i didn't actually want to run it but fine let it run um so we want to duplicate
this integration tests and that will be tags integration and that's going to have the tag of basically uh i'm dust wolf
right now i'm building four apis as typescript based lambdas inclusive as swagger open api uh i'm not so it's just extra
work uh viable clan members that cause you eu charge tariffs no it's because the exchange currency exchange rate right
now is almost it's been pretty close to parity one dollar what us dollar equals one euro it was not like that for quite
some time it's been usually like a dollar 20.30 per euro actually blame worldwide inflation and u.s inflation and a
bunch of other things which i will not get into all right uh so what we want is a test that when we uh so price endpoint
returns price object dto hey mvdev uh the pre-sale of my hexagonal architecture course uh is this week and then it'll
come out either later this week or next week but thank you for asking i must have closed it okay anyway yeah i've been
working on the landing page for uh for the course today so that's looking good uh okay so what we want is um new price
controller when we call price 4 what we want is an object not a string so we want a no that's not the name of the
variable let's go create that class i always forget every time i do this does jackson support records so that'll go in
there for now and what it has is basically it's going to be string upc and a price i wonder how what that looks like i
guess we'll find out i don't know what that looks like when it gets translated to um json i'm guessing it encloses it in
this uh i'm that's what i've seen trpc written your own routing call brack trying to reduce code dependencies i totally
am with anyone who's concerned about reducing dependencies so one of the things that drives me a little bit crazy um is
seeing so many dependencies pulled in for that don't really pay for themselves uh let's do that uh did it put price
response in the wrong place yes it did not in the test directory but in the source directory okay and then this uh that
then this is new um that and that oops 10. no the close of the expression is here oh you just totally messed this up
didn't you all right uh so that compiles let's go back to our tests so now that compiles and so what we'd like to assert
is that zero for this uh so we want a new price response that is uh 0.97 and um we want it to actually be 10. now i just
told it to run unit tests but because i forgot to tag it so let's tag this okay because unit tests should run fast fast
fast fast okay great so that fails the way we want um let's push this out let's but price 4 is supposed to take so let's
i'll commit that and what we want though is this is actually supposed to be a parameter so uh and then we can push that'
s just still pass and um i might want to put this as a request param so should um so should this be a param or is this
actually an identifier and it should be part of the path so should it actually it should be a path param shouldn't it so
uh let's go here um i don't want to get the content to string but i don't want to write a more complex test um we can
just do sort of a quick validation uh abc okay so this will fail because we're not returning anything we're also not
asserting would help if um so let's take this pull this into a variable and then we can now assert so let's pull and
assert that and we want to say contains oh we can do that so we want to contain not only upc but also uh 987 and what do
we call it price and let's see this is i have no idea what this is going to do uh i'm just wolf asks for the reason
behind making it a path parameter um so this has to do with am i thinking about this endpoint uh yeah i can use jsonpath
i just never remember how to use it let's find it uh so do we think about this as a resource right sort of rest like um
or do we think about it as like a search query so if we treat it as like kind of rest like we're basically just getting
whatever the resource is and the resources identified by its upc uh the other option is we can say no it's really a
query around prices um then it would be a query parameter so it for this tiny service it almost doesn't matter and so i
mean or not almost it doesn't matter and so it's more about how do i think about it and sort of think about it as this
service has a bunch of prices you don't have to query for it the only thing you're going to look up is upc and therefore
each sort of if you think about prices as a directory it has a directory full of upc's that have content and i'm just
returning it right that's really what a resource means is in a sense there's just some content there at that address
yeah um the end result is the same but it's really but you know how are you thinking about this if you are to query
across sort of two variables like hey um give me you know the where the epc that wouldn't make sense but you can look up
what are called upc categories you could say hey find me you know products that are dairy of this type then you'd use a
search query let's see what happens i don't i don't think i don't think this is gonna pass because i'm not sure the upc
is uh expected 200 right because it didn't match against anywhere because we didn't put in upc so path variable thank
you intellij for writing that for yeah so if it's sort of like a like i think about like is this a nested directory like
here is um where the hierarchy is has a specific order right so i want to find um you know i'm searching for inventory
for a certain product so the first parameter is warehouse it's always going to start at the warehouse and then it's
going to start out what aisle is it then it's going to start out what look you know what shelf is it and it's going to
look at what box is it since it's a very well-defined hierarchy you can use but that can also get a bit awkward and so
it you know would you ever search for hey i don't know which warehouse it's in but it's you know could you basically
search for it without one of those parameters no because the shelf is identified by what aisle it's in an aisle is
defined by what warehouse it's in so it makes no sense to leave out warehouse versus you're looking for a product it
makes sense to leave out all sorts of things if you're querying i want a book that has this author or maybe it has this
title right you can leave one of those out then you're not going to do it as a hierarchical thing all right well let me
know that worked so now let's run the application and that'll probably be the last thing i do because it is dinner time
for me open our http client yeah it's sort of like if so again if if there's a lot of path entries it may not be
efficient um for humans but if it it sort of in a sense requires that you have that entire sort of path right literal
path to that to that specific thing but it is hard it can't be harder to read yeah uh so what we want is um prices uh
and we're saying 0.987 uh um oh i don't know why i'm looking here it's here and there we go there's our json and so i
guess big decimal is naked that might be problematic because if there's a decimal uh that might not be parsed correctly
on the other side so we'll have to think about that but we've got our uh this is working as as we expected and as our
test said it should so that's all good um all right i think that's it this is a good place thanks to strayer for
bringing his family along uh thanks for those of you who continue to hang out uh despite java probably not being your
favorite language um i stream this kind of content a lot this around the same time so i this week because i'm working on
releasing my course i'm reserving all my most of my brain power for earlier in the day for working on the course and
then um most days i'll probably stream from like five to seven normally i stream earlier in the day uh but if you join
my discord totally free um i announce when i'm going live sometimes even more than five minutes in advance yeah amazing
because my schedule's all over the place because there are some days where i'm teaching because i also do coaching
technical coaching and instruction so there's some days i'm busy with that so join the discord you can also follow i
appreciate what do they say i don't see any of the usual suspects uh so i'm open open to raid ideas oh thanks for the
bits and i'm this wolf appreciate it yeah and the discord by the way if you have questions like that um about stuff i do
on stream or just general java and spring and tdd stuff ask away i've got a bunch of channels for that specific stuff so
i don't see anybody that i know uh that i usually follow that i would be so unless you all have an idea we can just say
have a great rest of your day for some of you it might be and so again i have a that's a chicken uh i'm on a low carb
diet so chicken nuggets are uh uh so if you want to know more about my course my hexagonal course hexagonal architecture
course which is part of my making your code more testable series um you can sign up to my newsletter but i don't just
sell that that mostly what i do is i send out emails about the stuff that i do on stream the stuff i do with with my
clients to make their code better all right uh we'll call it here so thanks so much for for hanging out i really
appreciate it uh thanks for all the followers and thanks for the bits i'm dust wolf uh and hopefully see you on a future
stream let's have a great rest of your day go get some nuggets thanks you
