# TDD & Hexagonal Architecture Exercise： Supermarket Checkout Pricer - Part 1

**Video URL:** https://www.youtube.com/watch?v=BYHlxsyD288

---

## Transcript

as some of you may know i've i'm working on a self-paced version video course of my live course for and it's been very
slow going because i realized that well am a perfectionist related to that it's very different to create a course where
i've tended to rely on conversation and discussion to teach the class and it's very different even though i do a fair
amount of lecture in the in the class anyway converting that to a self-paced course where i feel like i'm doing good
explanations and can't rely on people to say hey what did you mean by x uh as much so that's that's been taking me a
long time um and so one of the things that that i want to do is have multiple examples of hexagonal architected
basically hexagonal architecture structured code because i think uh examples are really important for for learning this
stuff i know i learned from examples in addition to actually just trying things out and doing them i learned a lot from
from examples and uh yeah so what i want to do today which is not work on my mob registration system or other stuff um
what i want to work on today is basically uh tdding and by the way this is my my new hat uh this is the red hats this is
uh the red part of this the tdd cycle i've got my uh refactor part of the cycle so maybe i'll switch hats um so weird
the weather was like really hot earlier this week and last week and now it's like uh now i'm actually chilly and it's
like not even barely barely 60 degrees fahrenheit so hey sweetie let's get to it so the uh thing i want to work on is
basically just from scratch um what does it look like to to tdd an application with hexagon architecture it's been a
while since i've done it the actually i don't know i think it was the yacht dice game which was at least a couple years
ago uh does the red hat work on kids to change their behavior um yeah i don't know uh so let's switch to can tell i'm
out of practice because i'm like where's the button there it is okay um so this is uh there's a whole bunch of variants
on this one this one was originally a kata i don't use the word kata there's a little bit of a sense of cultural
appropriation some people don't feel strongly about it and i'm like you know what i want to respect what that is and
that that culture so i try to shift things to to use the word exercise um but this actually comes from uh prague dave
one of the pragmatic programmers uh dave thomas who wrote wrote it up as part of a series on on doing these kinds of
exercises um i'm sure people have done variants of this earlier but this is the one that a lot of people reference and
so i basically these folks serenity serenity dojo so i took theirs and basically updated it and moved some things around
and uh and it's sort of like this is one of those things where it's like it doesn't really matter non-trivial in terms
of what it's doing uh and so here we've got the super merch could check out prices so the idea is to to build um you
know sort of the thing that that calculates the pricing of stuff you've got in your cart at a supermarket where it gets
tricky is is basically the special deals so we'll figure out which deals we want to uh um incorporate uh and so i set
this up sort of so you can start with with this story right given a toothbrush product that has a price of a dollar when
you add it to your cart and you ask the cart how much things cost it should return a dollar um so we'll start with um
how do we you know so the questions that that you want to think about is what is the first test that we write and so
this goes back to my um i should probably bring this up let's see uh no that's not it do i have it open no let's open it
it's always scary when it takes a long there we go uh so this the tdd cycle that i will be following uh is basically
this based on um how i teach it so this game td cards if you go there you can you can purchase the digital version of
the game so we first want to figure out what should do and how do we know it but a lot of times it's like well what's
the first test i should i should write right so if i want to get to here um what you can do is you can say well i don't
know where necessarily where i want to start beyond this and so the first test you might think of is you know if a card
has a toothbrush but that's too many new elements and so when i'm thinking about the first test i want to write i'm
thinking about what are the fewest number of elements i can get away with and so something that helps basically james
grenning's zombies which uh the zom basically zero one many so you think about okay what's the baseline test what's the
zero case uh because what what i try to do when when i'm starting out is i want to build start building some of the
these objects and so the first thing we want to probably build is a thing we'll call a cart call it a bag call it
something else but we'll use cart um and we just want to try to get this object created what's the minimal thing we
could assert about it that will basically force the object to be to come into existence as well as um what is the price
of an empty cart so we use this as a foundation that to build on when we add stuff to the cart right that that is
calculated correctly uh we're gonna have do i use the display name annotation no i don't i rely on my test method names
to to be useful um i i don't i honestly don't understand why people use display name um i know they have good reasons
but for me why not just make the method name descriptive i don't know maybe you can tell me if there's a good reason
that i'm i'm overlooking but i've looked at places where they use it i'm like okay that's slightly more readable maybe
because you've got spaces in it but you know one of the things we're good at is is you know especially in java we're
good at reading camel case words and and use the words as the delimiters so here one of the things we've got is we've we
of course want to start with a failing test right i've got my red cap on um and so this will fail because we've got the
literal fail message so we can we can take that out we can actually write a more a test that has actually some some
stuff in it um but right now it's failing because it's failing to compile right so that's the first step right is okay
we know what it should do and how do we know it did it basically we know that we should be able to create a cart and
then it should not be null um so that's that answers those questions uh and now we want to write code for the test and
it'll it'll fail to compile because things don't exist uh so now we want to write enough code to get it to compile so
that means we'll have to create the class so go ahead and create the class um it goes into our domain uh our production
code um and the layout that i like for um sort of adopted this from doing a lot of ensembles uh and i really like it is
uh having both the test and the code on the same screen where the test is on the left so you get the sense of the test
driving uh the the creation of the code so now we've got the class don't put anything in it um this test uh should now
pass um so even though there wasn't we didn't really see the test failing it was failing due to to compile but we'll
we'll change this and so this is um a technique that uh instead of writing sort of always new tests i'll sometimes write
a test that a search less than i eventually want it to as a stepping stone so i expect assuming my compiler works
assuming my test framework works this this should now pass and it does so now i can say well asserting that it's not
null that's not good enough really i want to assert something about the state uh the information from the cart i'd like
to do something like what is the current total price of the so we want to ask total price note it's not get total price
it is total price it is a query method we're asking the cart what is your current total price we are not getting so get
to me has implications of getting some internal state that's not what we're doing what we're doing is we're creating the
object how it knows the current price the total price of its stuff we don't know and we don't care and we don't want to
care there may not actually be an instance variable a field called total price in fact my implementation probably won't
go that way so what we're going to say is well as soon as this doesn't compile we want to make it compile because this
will help us use the autocomplete for our assertions so we'll create the method now we have to decide what is it going
to return for now i'm going to use whole dollars but that's going to quickly change once we get into some of the
discount stuff but we'll start with whole dollars so i'm going to use an int now i don't want to return 0 because the
test i'm about to write is gonna be assert that that it's zero and that'll pass so i don't want it to pass so there are
a couple of things you can do you can throw an unsupport operation exception that'll definitely fail the test um or you
could return some out of range number like negative one but for situations like this i kind of prefer to throw throw an
exception so now that we have the method and its return value is defined uh the return type is defined we can now say um
is zero so not you know if i say is equal to zero we can just say a zero because it search j gives us that kind of
assertion so now um right we're in the changing behavior right the red so our prediction is that this is gonna fail so
one of the important parts about both my my game and the process is the prediction right so we want to predict that uh
the test must fail and for the right reason so our expectation is this is going to fail and at this point again it's
very easy to to see how it's going to fail it's going to fail because we're going to throw an unsupported operation
exception if somehow we were calling the wrong method yeah so easy i've seen your your all right so it throws an
exception so fails as expected and so now our goal is to get this to pass with the least amount of code possible and of
course the least amount of code um so when we refactor one of the things we look for is the other thing i look for are
are constants especially in this case where i'm going to return something other than zero except at this point i don't
know that a field is the right thing to do so it'd be tempting to say oh let me go and refactor to a field that will be
called you know total price um but i have no i have nothing that really tells me that that's the next step so to do that
would be premature so let's leave it at zero and let's figure out what the next test is um so let's actually i'm going
to go on let's check out oops so our first story that we want to implement so remember that test driven development
doesn't work at the granularity of stories that tells you when you can move on to something else and it should also be a
trigger for doing more thoughtful deeper refactorings but this is uh needs to be broken down to steps which we've done
the first one of which is just establish the baseline that we when we create a cart it's total price is zero but we want
to head towards towards this which means we're gonna um want to add a product well so that means we're going to need now
it might be tempting to go ahead and create another class but i don't know what that class looks like so i'm going to
you know i can probably guess and maybe on experience i can do that but at this point i i don't know what that means
which means i'm going to need to write another test so we're back to sort of changing behavior and i won't switch my
hats all the time that's going to it would get annoying so now we're back at what is the next piece of behavior that we
want so the next piece of behavior we want is add toothbrush product then heart rights is one dollar so what do i want
to do i want it when when i add right and so this goes very much to this story right give it a toothbrush product that
the price of a dollar when toothbrush stats of the cart querying the card store price returns a dollar and now i want to
add up add a product and here's where again i might think of well let me create a product object except i don't need to
do that um i can basically say this is a toothbrush and a function zero yeah and and so i might normally you know
typically i might take a larger step because i have a sense you know we always have a sense of like oh there's probably
a product object and it has a but when we're sort of practicing tdd and taking small steps we want to really take small
steps and my preference in general is and this is my preference not not everybody does this but my preference is to
extract objects from code that already exists somehow that feels more natural for me um sometimes i'll jump and create a
class but uh i really do i don't know maybe it's it's like i really like refactoring and so creating an object a class
definition out of existing working code is somehow more fun i don't know so we need to create this this ad so we'll
create it it takes a string which we'll call uh product name and end we'll call and that's it right i don't need to do
anything else to get it to compile and so now we can do a search insertion um so what what's our expectation is that
when we ask the card for its total price it should well certainly if we run this it's going to fail how is it going to
fail well add is basically a no and so it should still be 0. and we can even see that we can inspect the code and say
it's literally so one should not be equal zero that's our expectation hey lexlers um so fails as expected and we want to
write the least amount of so that means this zero is not going to work right so the next level up in complexity from a
constant literal i guess literals are by definition constant um is some either an if statement or storing something that
is a piece of mutable data like a field um the other thing is right so if i wanted to return one all right that would
get the test to right so that's clearly not going to work but one of the things i i watch out for and and uh kent beth
beck talks about you know duplication and the uh and sort of design aspects and one of them is is you know eliminating
uh duplication um and so i kind of see this one as a duplication right because it's actually over over here and in fact
that one is then being passed into the product price so i can think okay well if i just save that i do this sort of the
simplest analysis well it's being passed in here if i can just save this product price then i can just return that that
value so now i can i can do a refactoring create so i'm going to do a refactoring even though i've got a failing test i
know but to be really sure i'm going to basically comment out this test and now i should be back at passing except i'm
not because i didn't change this back to zero so that's the danger of leaving a test failing even though it's like i
know this test fails right is that you may have unintentionally left something broken so now we should be at and so now
i can put a a name to this thing it's not total price because i want to copy this product price so i'm just going to say
so this is exactly the same code and now i can uncomment the test this should fail in the same way one is not zero but
now i can do an assignment i can say this.product price equals product price and it does and i created the branch
because i meant to do a commit earlier but i didn't so let me do a commit now so now we've got oh okay so we have um
achieved our uh not quite of course because this puts a lot of burden to pass in all of this detailed information
however that may be okay right so one of the the downsides of starting at this level right so if we think about what
kind of code this is this is pure domain code right this is all about what are the rules process calculations behavior
we want from the problem we're trying to solve which is something that can give us the price of a cart with a bunch of
items in it so let's make that clear by doing a refactor this object is a domain object so i'm going to sort of switch
gears here and think about this from a hexagonal architecture point of view not not that this right so the code we're
working on is in here completely isolated from the from the outside world and um but what gets hard is if we start here
we don't quite know well how is like the web ui gonna gonna use this or how you know we could certainly order stuff
through through text messages who knows we don't quite know what it's gonna do we also what we don't know is this orange
is the application layer it's the one that's implementing these and so where does the product information come from so
it might be represented in our core domain as an object as a domain object but where did it come from and so to me the
this is what i i really love about hexagon architecture is you know exactly where it comes from it comes from outside of
the hexagon right so this yellow line here that's the boundary of the hexagon everything inside of it is pure business
pure application meaning it has nothing to do with technical stuff for the outside world but we do retrieve stuff from
the outside world so there may be persistence maybe there's a database that has the product information or maybe it's an
external service completely that we have to communicate but it comes from outside so let's move this to where it belongs
so let's put this in a package that and since we've done that let's move our uh i always forget the keyboard shortcut to
optimize imports because i do it so infrequently um so now now we're now we're talking in the the domain which um oh i
have to update that nightbot i push back the the launch of my course to next month but i think i'm on track for that um
so one of the things that that to me um no the hexagonal architecture courses is so if you sign up at the email list
you'll get details on on the course among other things and so this is another example that i'm going to supply in the in
the course so adding domain to me does does these magical things one is it all of a sudden says no code here can
reference anything hardware io outside world related the other thing it also triggers is because we're inside the domain
so everything should be domain objects value objects right so they should all be objects so product name being just a
string is a bit suspicious of course we're not actually using it yet because we had no tests to do it and in fact maybe
you know writing this we weren't able to fully verify what we needed but we said that that was part of the given so i'm
i'm but now we sort of magically put a barrier around the code that we're looking at and it automatically triggers this
is not right and that's something that we would want to think about and so i went down this path because this api right
a lot of people think about apis as just having to do with web apis but api is just a programming interface it's
basically what methods are publicly available that you can call and so cart has an ad method it takes two pieces of
information but is that the api we want we're inside of our domain and so we should really be thinking about domain
objects we should be thinking about product something that represents the product the other thing we can do is we can
sort of see this as a little bit of a code smell right why are we passing these two things shouldn't there be some kind
of parameter object only two parameters doesn't doesn't really trigger that but it's it's and so now i'd say maybe it's
time to think about an object that represents these two pieces of information because again where does this come from
comes from the application layer and so the application layer there might be a method called add with this product price
but at this level we should be generally talking already in domain objects the application layer is the one that loads
information from external systems including from databases and then sends the sends that and coordinates that uh and
sends it into uh that's a good point squeegee having the having the product uh as the prefix for the variable name for
both of them is certainly uh indicating that that uh so josh oliver olivier uh this is um not a great place to ask that
kind of question but somebody might be able to help you with that i don't know um so the you know so now the question is
like is this yet is this a time to create uh the product object i still don't quite know enough there's also i'm really
like what's going on with this product name so i kind of feel like i need something to help me figure that out and i
don't know what that is yet do i even need the name maybe they're only toothbrushes maybe this is a toothbrush store i
don't know anytime yeah no jay has got not not even um so i don't have enough information to know where to refactor
right so even though like i know a lot about refactoring it doesn't mean that you can always refactor unless you have
sort of enough evidence and data and information about what what does that thing look like and so i think i'm gonna at
this point say i i don't know what that looks like i have a guess but i don't quite know what it what it needs right so
what's gonna be in it where does it come from what type of object is it do i even need product name i don't i don't have
that and so i can look back and say okay i basically got this first story um the next story that i could follow up with
is more about you know discounting but a slightly different direction you can go in is well one of like it's great to be
able to find out the total price but customers often want some kind of receipt or some kind of running tally of here's
how much you have and in order to create that right um there's going to be some kind of receipt printing or some kind of
uh thing that's going to show both the price of each item but also the description of each item and so when i get there
that that might but let's let's um let's implement this one and then we'll we'll move towards okay now that we have
multiple products uh what happens then so there's we can't go directly to this because this is now about um figuring out
uh the the deal right by toothbrushes two two processors and get get one half off we haven't done the many case right so
going back to the zombies we haven't done the mini case if we've done the zero case an empty cart done the one case
where we add one so really kind of need to do the many case so it'll be but we're going to add one of the downsides of
copying and pasting test code is you may forget to change all the relevant pieces so if i copied and pasted this i didn'
t change this and so here's where prediction is useful right we predict that this is going to fail because well we've
we've added two um actually went and and we may have in our head that we've changed our assertion to two because that's
what we want because remember we're trying to write a failing test for if i add multiple items it counts those multiple
items so i'm going to predict that this is going to fail because it's going to return one instead of the two that i
wanted to return but it passes because i had forgotten to change this number to reflect the change in what this test is
doing and so that's where prediction comes in handy um that oh this should actually be two because that's what i wanted
it to be and oftentimes just saying the prediction out loud makes you realize that oh i just said two and it said one
that's not right so now we expect it to fail because we actually want it to be two but it is only going to be one
because it only holds on to the last product price i can just do plus equals right and so it passes now already you know
again if i hadn't noticed and thought about why is product name not used um certainly at this point i might be thinking
about well hey what if i added two different products does that does that matter so let's come up whoops let's come up
with a different product well if you're going to buy toothbrushes you probably want to buy toothpaste as well so i'm
gonna copy and paste this is expensive it's two bucks and so we expect this to be the sum now we're just doing plus
equals and so we may think that this is fine and this will pass so one of the things i want to do is i want to say well
i don't trust this test unless i've seen it fail so i can change this back to just equals right i can sort of mutate and
modify my code to see that this fails appropriately that's one way to do it and then actually a couple of tests fail the
other way is to sort of force the assertion to be different so let's say one and so now i'll be able to predict how this
test fails right i've explicitly changed it so that it's wrong but i should still be able to say now this is going to
say we want one in incorrectly but we want one and it's going to give us three so one of the things this does is help us
understand what the code is currently doing and so we see it's returning three as we actually really do want and so
that's fine so this test didn't really add add much for us we've added two different products but it didn't really
really add much because we're not paying attention to the fact that these you know this this test here added to the same
product and this test here added two different products there's no difference the cart has we're not able to observe any
difference and so we may want to push on that right so if we think about zombies right zero one many we've done zero one
many um and so now it seems like we want some features around around the receipt printing so what would we like what we'
d like is after we add items to the cart we'd like to get some sort of receipt right what does a receipt look like it's
basically product name how much it cost and then total so who's responsible for that is the question from a tdd
standpoint we could put it in cart how that works uh is is going to be um depending on what cart actually does and so
remember strings or these these bare strings are indications that maybe there's there's a missing domain object but let'
s let's assume that look we're just going to try to make it work and then we'll refactor our way so we wanted to test we
want to start at an empty cart so so we're going to say is when we create that and so we're going to say this is going
we get to say we're going to return null cart is empty and and let's say we want that on oh am i using java 8 let me
upgrade java because i created this with java 8 um to support one of my clients who is unfortunately still stuck at java
8. we can go to 18. all right and let me yeah uh let me make sure that i am now set at 18. okay great i could do 19 but
we'll stick with 18. all right oh did you mess up intellij you did you've lost the jdk i hate when intellij does this uh
and that's because i've got this thing here okay uh there was uh do i prefer testing from the domain instead of the
application so uh if i am very clear um what the domain needs to do then i will start with a domain but i'm always
keeping in mind the um basically the application layer right so in out i'm very much thinking outside in here the
application layer there's not much that it does and so it sort of is and uh so in general i will i would start fully
outside in but because this is an exercise we're sort of uh taking that as a given of of we're going to start with cart
and see where we go things so let's say this is what we want we want card is empty total price so this will clearly fail
so now well we could just copy paste this right um eventually we'll we'll get to something that might involve spring uh
yeah so that's so i did not intend to stay at java 8 for this demonstration um and now we can move on to another uh
failing test basically so and so we'll say something like uh that text blocks are so annoying though in terms of
indentation um so what do we want to say wanted to say uh cart has and that item is and we'll put its price next to it
is so this is a lot right um uh so danny ruse says uh if i start with from within the domain i tend to write more
fragile unit tests compared to outside n yeah yeah and that that can definitely happen because you're working almost a
too low level without having a clear sense of what is outside um so we're gonna we're sort of doing a little bit of
inside out but then we're gonna sort of get our bearings and then do a bit more outside in in a sense you could say that
cart right now is the entire application so it is outside in uh other than sort of the actual interactions of like
pushing a button or clicking on something um we're starting here is like this is the boundary of our application we push
it into domain so that sort of put a boundary around it that now makes us think about certain things like strings and
then we'll use that tension to sort of push things around so let's uh let's split this into sort of multiple stages
eventually what this what this is what we want except speaking of outside in this is really a very much an outside test
and testing against the domain is not where we want it but we'll see that clarified so if we're on it now we expect it
to fail because we're literally comparing strings and they're uh we could start out with maybe showing the number the
the number of items and the item and the total price maybe that's too much so maybe we should take a step back and say
what or take take you know can we take a smaller step what are we really interested in so we started with this and maybe
this cart was is empty is was a bit overzealous right too much um and we only realized that though as as we we sort of
wrote this test so let's say you know what this is a lot to do um how about uh we forget about sort of how big the card
is and just look at sort of items in total price eventually we may want this but right now we don't we don't uh we don't
absolutely need it to drive our code so let's let's go back change this test right so we'll comment this one out and say
you know what right now we're just gonna if the card is empty it just displays total price zero dollars all right so it
failed because we've changed behavior right changing behavior is the red part and you're allowed to go back and change
tests once you write a test it's not there permanently we decided you know what that's too much to deal with so let's go
ahead and delete that now it should pass and now we can so now this is failing for for two reasons we can start with how
about before we get to this part what if we just and then so we're basically taking a small step within a test and so
some people would say you know maybe just create a separate test um and that that that would be okay but i think we're
talking about the whole receipt so i kind of want that in one assertion but i can assert part of it and i can get that
to work and then i can expand this test and then see where it goes so this will fail because it's going to return zero
instead of one right the dollar zero instead of dollar one obviously i can't replace this with um with one because then
the other test would fail and so we need to think about okay where do we have this information from in fact we already
have this information and so this is just a matter of so we can say is we can use the dot formatted to fill and so it
uses the formatter for doing that um and that's where we get all the so we want probably percent s is good enough just
general um so we want is percent s and what we want in here is total price so we predict that this works because the
components of this implementation we know the total price works and now it's really just a matter of did we use
formatted correctly so let's do a commit um we actually did a few things we moved uh so did we go this way right what
was our original goal original goal is we wanted to push on this idea of i want to show the cart contents so now that
we've got this working right so this variation is showing the total price work now we want to add back that there's a
toothbrush in here so now this will fail because there's no toothbrush being displayed right so in fact if we click to
look at the difference we see that that's the difference so how do we get that in here well we could i mean we could do
this right it's always an option that gets the test to pass but then it breaks our old test so it's clear that we need
some kind of variation well except we don't have access to that information right we could say well that's the product
price and the product price is the total price except we now have some confusion right we have this variable called
product price except we're returning that as part of and didn't really notice that before when i implemented it but one
of one of my heuristics is as soon as you you have any kind of confusion you want to clarify it right clarify the the
confusion early rather than let it sit around and people sort of then are afraid to touch it so let's refactor but in
order to refactor we need to have so i'll go ahead comment this out temporarily run all my tests and oops they don't all
pass so and now all tests are passing you want to make sure all tests are passing before you do refactoring although
here what are we doing i'm actually just going to do a rename on this variable so that was the name change a fairly
straightforward refactoring everything still passes so that's fine and so now we can uncomment this it'll fail again as
is the same way it did before but now at least in terms of the variables i all right so what do we want we want it to
say toothbrush dollar except we know that that's going to break the other test so we know that where does this come from
well now we can say we don't have this anymore we could put total price there because it's like oh well it adds up to
one and maybe that would suffice for but we'd certainly find out soon uh sooner rather than later that that that wouldn'
t work when we have multiple items but you know what right now that that might work so we'll put in a put in that s so
it works for our current test but it breaks the other one because we have total toothbrush zero and total price zero so
that's not going to be good enough well we can if the card is empty we can return a hard-coded string right we can
basically say just return this if it's zero so let's do that and uh what we're saying is if is um only if it's greater
than zero will we otherwise we'll let's try that right remember during the stage of trying to get our test to pass
copying and pasting writing ugly code that's totally fine so now we've captured the the varying expectations from when
the card is empty to when the cart so so we can refactor is well let's just pull these out into methods i don't exactly
know what what else is going to happen but you know this is uh format and then we can basically refactor this to run all
our tests they should they should still pass those were just basic it might be tempting to maybe simplify this um this
if statement and use a ternary operator to me that actually doesn't help the real key is when i was writing it i said
when the card is not empty and that's the name of the methods a total price greater than zero how do i know that that's
whether a card so i can't rename total price because that method name makes sense it's the expression that is a little
bit confusing well since i can't rename anything i can capture it and i can extract it to a method basically is i could
say is card empty but we're in the context of a cart so i can just say except now i've reversed it right because now it
reads if is empty return it receive for non-empty card so that was a naming problem so this really i like garlic knots
but not these nuts um i don't like boolean knots especially in variable names uh so we want to reverse this and so we
can basically flip the if statement so we'll invert the if condition and now we have two knots right so we have the the
bang which inverts it and we run our tests to make sure that because especially when it comes to boolean especially it
seems like the simpler the boolean the more confused i so we instead want to say is yeah is something like not empty or
or this is now return receipt for empty cart so now i actually want to flip this i want to flip it so i want to
basically say equals zero now i know the method name is wrong but then but and uh but the test should pass and now i can
adjust the name to make it make sense which is actually in this case since i flipped it now it is empty all right
because this is re return receipt for empty cart so now this name matches this name right if it's empty return receive
for run my test just to make sure i didn't mess anything up right so having these tests again gives us the confidence
that we haven't broken anything and we can always you know make sure it's like are we sure that that's capturing that we
can basically change this back to uh greater than zero and at least one or two tests should fail and they do so we know
that we've captured this correctly it does mean that we are defining is empty based on total price and at some point
we'll probably find that's not necessarily going to be correct but it works for now and so now we can do something like
great we've handled a single one we still have this constant here right this basically this literal word toothbrush um
so let's write a test that forces us so we could write another test that um adds a different item like toothpaste uh but
i think we'll capture that without having to take we could take that step and that would be a tiny step we could take a
larger step we could say all right let's just go to multiple items um i don't know that that that feels big so let's
let's do another test and so here we're going to say when we add toothpaste we'll call it two bucks we expect toothpaste
hoof toothpaste two bucks um and the total price should be we're saying that um well the total price should be correct
because that's generalized that's calculated the two dollars here that should be fine because i got that from the total
price even though technically uh that will be wrong once we have multiple items um but this this will be wrong because
we have hard coded toothbrush so we expect that that's going to be the difference and here's where you know using the
the diff in intellij to to show the comparison failure highlights that it's just that one word that is different so now
we have a single thing to change so let's take this let's extract it can we extract it as a parameter variable can we
extract this as something that's too bad uh yeah it seems to me that it'd be nice if there was a refactoring where i
could say can you just extract this to a formatted thing that would be nice but we can't so we'll do this and then we'll
need uh we don't have the product name right we can change it to toothpaste but then we know that that's not general
enough and so we actually need the product name that's a refactoring right so i could i could go ahead do what i was
going to do right put product name here create a variable create a field store it from the product name that was passed
in during add but that's doing a lot of work while a test is failing if i can split the work into two pieces refactor
which is safe and then using the refactored code right i want to make this change really easy what would make it easy is
if i already have product name all right so as kempec says make the change easy and then make the easy change so let's
make that change easy all right so we want to get back to refactoring so that means this test will comment out easier
than commenting it out all right so all our tests pass um let's create a field for product name and then we'll just hold
on to it and in fact we can actually do more we can actually replace this because we have a test that's checking it so
we can replace so refactor to and it will it fail and it does so we took a small step except we realized that it's just
a refactoring and we refactored it and now this just works so do we still need this test do we want i'll keep it around
doesn't have a high cost and does sort of demonstrate that different items will show up differently i didn't predict out
loud in my head i said it was going to fail because i put a space in and so so now that this all passes now we can look
at generalizing this further right now what happens when we have multiple items in so i'm already a bit frustrated by
the fact that i am testing this against the so i'm already thinking first of all this is really bad from a hexagonal
architecture standpoint the cart should have no knowledge of what string representation what presentation and so now i
have to decide do i want to continue down this road it's not that much further or do i want to say boy wouldn't it be
easier if i could just check does the cart have multiple items because checking this through strings you know and
they're tools that can make string checking like this easier approval tests but eventually i'm going to want to split
this so maybe maybe now's the time to to make that decision because i can already tell like what i'm going to be uh
whoops that should be toothbrush and this is gonna be annoying and it really feels like i'm gonna be doing a lot of sort
of two different things to implement this there is the thing that i that the code is currently not doing which is
keeping track of the product names it only keeps track of the last one so there's the internal structure of cart to
store but in addition to that i'm also then going to have to deal with the string formatting which means there's going
to be some kind of loop which is going to make this so i have i have two directions to go one is continue with this and
fix both those things at the same time the other is to re um refactor along hexagonal yeah it's more than a tidy it's
it's a rear it's it's almost a re-architecture or it's an architectural level refactor um let's do this um i'm gonna uh
maybe not maybe not today but it'd be interesting to to go both ways and see where we end up and see what that looks
like um i don't know that if we'll have time for that today um let's let's refactor along architectural hexagonal
architectural lines uh so let's make sure we do this so we um for multiple items so i'll commit that and what we can do
is uh at some other point um go back to the previous commit and create a branch from there and see what it would look
like or at least from from this point see what it would look like to to do it not um uh basically not refactoring to
completely because i'm not even sure i'm going to use it that way so we should be back at all all test passing and we
are um so now when we refactor to hexagon architecture the thing we want to look at is what in our code is specific to
the mode of presentation that we're looking at in other words where's the i o well we don't really have i o but we have
strings right we have strings that that we're kind of making the assumption that it's going to be displayed on a
terminal console maybe not maybe it's being displayed on a little receipt printer but whatever it is it's specific for
some kind of kind of output let's say it's a a display you know on these uh you know self-checkout machines right or the
the point of sale system so something where it makes sense for it to be displayed in this manner but that is completely
separate from how cart needs to track it right so our goal is core domain must have no knowledge of how it's presented
in the outside world because it's deep inside here only has to do with calculations and rules and things like that so
let's split that out well that's going to be relatively straightforward but that's actually a private method what we're
really because it returns a string right so when we're looking for where's the i o strings are suspicious right because
they're often something that's presentation ready or ready to send out to some somewhere else we don't want that at
least not in our domain right and we said we are now in our domain so what we want to do is who's well that would be the
that is something that is hardware it's in the outside world and so immediately that means it is pushed into what's
interesting is is this an like does it just push and this is where not starting outside in like what triggered this
whole thing where did this add method get triggered from the outside world so we're kind of missing that and so without
knowing about that right does somebody push a button is there a scanner that scans on the barcode on an item and then
that's how and so to figure that out we'd have to say okay what so let's define that so let's say and here we're sort of
you know we talked to our subject matter experts and said hey we think we have you know some sense of how this pricer
part's going to go but we're trying to build the whole system and like right just building the pricing portion doesn't
have doesn't actually give us it does say the self-service right so if we're into right you know we're the pricer team
and we're gonna have to integrate with other things so we're gonna ask the question of how did those hey somebody added
this product how does all right what is the api we expose from our service to and so you know i'll make something up but
this is where we'd be talking about what is the contract between the scanner right since we said self-service so it's
going to have a scanner between that and the pricer really the cart it's not just the pricer because actually we are
keeping track of that because we are required to present so let's put so product information comes in as right let's say
that we're actually not responsible for looking up the product in some external service we're given hey here's the name
of the product and here is its price because receipt all you care about is those two pieces of information at least
that's all we think we need we still have the question though right we're saying that receipt doesn't belong in here
basically everything around receipt doesn't belong in here basically all this code does not belong in here we're saying
it belongs in some kind of adapter except have we fully answered the question where does it go well we know the ad the
thing that triggered this right was some inbound event an inbound message saying add this item to the cart price do we
send that to some other system like the displaced part of the system or is that a response back to the caller well if
it's coming in from a scanner we're not going to send it back to the scanner right or the you know maybe you know some
controller in in the system we're not going to send it back there we're just going to maybe send it directly out that
may not be the right architecture eventually but for now that's that's what we we think we know right so right so we're
gonna you know the display says yeah just send us that stuff we'll we'll just display it on the screen we're not gonna
worry about scrolling and and things like that um so we will display the full receipt every time right because we're not
going to print it we're just putting on a display so anytime an ad comes in we want to keep track of it and then we so
even though all this software might actually be you know in a little application that's deployed right one um the the
the different parts of the system can still be treat they're external to our our cart module right so we if we have a
modular system that's still the receipt display system so that means um what we want to do is sort of push these tests
out we want to test against let's say we've got something like this all right so this is our system we've got a receipt
display here and and so what we're testing the boundary that we're going to be writing the next test against is not here
it's actually here so we're going to write a test against the application layer that when an item is added it's going to
display something on our display now what's interesting about doing this starting out with this is um it's actually the
the opposite direction that i usually start with usually i start testing this and then seeing how it responds to this
and then pushing it out to here um but i think it'd be really interesting to start here right we know that you know we
don't want to write the product scanner but we know how the product scanner is going to interact with our application
it's going to call add and give us the product name and the price and what we want is something sent out to receipt
display well this thing is hardware so we can't have direct access to it and so we're going to need to replace this with
something that we can verify in a test what you might know is mocking but we're let's change it to that so somewhere
we're gonna need to have some test double right because what so i haven't i haven't done this this kind of thing so this
is this is an interesting place we've ended up so let's let's let's keep pushing on this um so let's now take a step
back and say okay we now and but it's an outbound adapter which means um because so one of the things i'm thinking of is
yeah we could we could have a test double but that feels like a lot of work just to get to sort of where we are and we
haven't really done it's like what we really want is we just wanted to remember multiple products sort of all that that
extraneous stuff and so what i want to do is i want to say well what if we forget about the right let's let's refocus on
just the so to get our to get that way to to a refactor we could say you know what right now i'm not going to worry
about it being an outbound adapter how about we just still have a way to to ask for a receipt but we ask the application
for that receipt right so we actually have to trigger that so that makes it simpler and then we can say okay then we
want the receipt to be automatically pushed out right so now we have to do a manual query against our application hey
this will be our and so what we want is a test that's pretty much what we had before so we kind of want to move the
tests that deal with strings we want to move those because they're not domain specific we want to move those into an
adapter so i'm actually not sure where it's going to go yet so i think it'll be adapter because it's not going to be
application because we want string stuff we know that's not uh so yeah so let's move this to adapter and this is coming
in from the scanner is the sort of the first one that had strings in it which is this one so we want to say that how
this receipt is displayed that's a test so what we want is we want some kind of scanner object right and this is going
and what we in a sense we want to do is um wrap the cart with almost a decorator and so sort of from this point of view
the um this conversion to strings is really like like a decorator in a way all right we're taking we want to take some
cart contents and and wrap it all right thanks for stopping by irvite so this test obviously so now that we move let's
actually move this test we'll delete it from here um and we want to now make sure we're running all of our tests so i'm
going to run create a run configuration for all tests and and so what should a scanner have um i i sort of want to avoid
calling this a scanner because that's something that's built into the java the sdk but that's we'll leave it so scanner
this is the downside of auto imports no don't import that well we'll do this for now and it's gonna it'll it'll cause us
problems um so we want this to compile but we wanted to use our own scanner uh so and this is not in our domain but it
is oh we don't need to because it's in the same package so great all right so we can actually close that for now so we
want is we want to basically move this receipt behavior to scanner because what we want though is we want scanner to
have a cart so let's pass that in and let's go ahead and create a constructor the reason why is this is the dependency
direction between adapters and domain all right so adapters have reference into our domain right they can have a
dependency right that's basically this dependencies point inwards so our adapter can ever reference the application we
don't have an application layer yet so we can use our core domain as a stand-in for that so our application layer
doesn't yet and what we want is we want the method to be called against scanner because that's the one that should
return strings and then cart receipt should go away so we'd like then there to be a method on scanner which is receive
now again already it's like well we said scanner receipt we're trying to take a small step we're going to then move this
behavior elsewhere but right now we want an easy way to uh so we'll create the method i'm gonna return a string but what
we want now want to do is we want to say i'd like to but let's just treat this as sort of pure delegation so let's go
ahead and create a field cart and now what we'd like to do is we'd like to inline this i don't know if it'll let us do
that right because we want the code that does let's see what happens if we try to inline it so what it says is well you
can't because this is empty method the receipt and the receipt right for empty cart not empty cart is and what we can do
is we can sort of do the same thing we were doing before in terms of taking small steps right we can basically take the
tests that were in cart test and move them to scanner test and then make them only work at that level so for the empty
cart that's going to be straightforward we can basically just take this case which is receipt for empty cart we can just
in fact we can just take this entire method and then just call now by moving it out of here we're basically breaking
this code but actually we're saying we don't want that we don't care about that all our tests should still pass because
we what we did was we moved a test that was basically against this boundary and we basically said we don't want that
code in there anyway and so we moved a test to this boundary and so the code that handled that test right so we
basically want to add more well is empty is no longer used here so we can delete this which is actually good because is
empty was kind of bugging me that it was checking the price and that seems inappropriate so that was a refactoring our
test will pass so um moved uh rendering you code that there's the art from adapter now we can do okay yep so i meant to
release the course in in june that's not going to happen uh because today is june today's the last day of june so it's
not happening today um but it will will be happening in july um so we want to do is continue moving out the tests from
uh the the cart test to move them against the scanner into scanner test so let's go to cart test and so we want to
basically continue taking the code that's that's checking the rendering of the cart and moving it to an outer level so
take that put that here we want to test against scanner and so if we run our test this should pass because this test
that we just moved is not yet testing at the correct boundary right it's still testing against cart what we wanted to do
is test against scanner but let's make sure our tests pass and then we'll change it and we'll be in sort of tdd mode
okay so now we want this to be again scanner right so now it's this test is testing at this level so now we expect it to
fail because it's and so it fails as we expected it so now we want to do is want to take the receipt for non-empty cart
and basically just and the information we need from the cart hey what's the product names and the and so we can do is we
can actually so we want to do is we want to isolate this this method and this is a technique i i also show in in my
course which is um we need to isolate this so that this method can be moved well what is keeping us from moving it is a
reference to these uh at least this piece of information total prices except is accessible but it's product name that's
not well that's fine so let's but our goal is to move and split the representation rendering part from the storage part
and we may go through some steps that are ugly but this this we're trying to um all of our tests that currently pass so
we may find that that that's not the api we're going to want from our cart so what we want to do is we want to extract
product name into now whenever we extract a method we always want to ask the question is this okay are we revealing
information that's directly accessible that somebody could modify well no we're returning a string a string is immutable
right so no caller could change it does it make sense to have product name on on a cart well if it's a cart can only
hold one item sure why not which is really the state we're in it really only kind of holds one item in terms of the
product names that it remembers so now that we've done that now we can take this receipt for for we could make it static
and then move it over but i'm just going to actually cut it um sorry i'm going to make it static because because one of
the next things we need to do is we need to fix up this code and making this method static will fix up this code because
it will force us to pass in a cart here so let's do and so now this code was transformed for us now we can take it we
can move it over i don't know why it wanted me to move it uh oh product name is private let's make that public right so
we evaluated that this was okay to make public so now we can move this not sure why it's not letting me auto complete
that i'll just do that so now that we've done that but we haven't yet made our our test pass all right so remember we're
trying to make this one where it shows a single item so we've got the right uh code for that and now we need to decide
whether a cart so uh evaluate based on whether the total price is zero because we have access to that and that should
suffice for now um so let's go ahead and do that let's first make this non-static so the way we make it non-static is
there's no automated way to do it for what we want so we'll delete this because we know that we can access the but by
doing that by changing to not um so that tells us actually that there's one more test that we need to move over so we
kind of could say well to keep it stacked until we move everything over or i could just say you know what let me and
this will eventually be against scanner and that this is going to be against scanner so we've done is we've purified our
cart test cart test now no longer references anything having to do with how the receipt is printed so we can close this
now we basically pulled everything out of there cart no longer has it has receipt but no nobody's using it anymore so we
can and now our cart is domain pure well other than this product name but we'll come back to that so we can close cart
for now and focus now on getting scanner to to work properly so we've got tests against this that are that are basically
failing and we want to get them to work so the way we do that is we basically the receipt has to decide whether the card
is empty again we can wrap this with an if statement if part total price equals zero then we consider it empty otherwise
we return receipt for non-empty cart this should restore us to back where we were this this if statement look should
look familiar but now we're back at passing tests so we've moved the behavior of rendering the contents of the cart as
now i originally moved this into the scanner class because it's going to be the one that handles the input but i realize
where where we ended up is this is just uh the display portion but you know maybe the name isn't isn't great but we'll
we'll keep pushing on this we now have at least passing tests and we now have that scanner is doing the work of
formatting and cart so why did we do this again what was our what was our point our point was to separate the rendering
from the tracking of multiple products so now we can focus on that now we can put the scanner stuff to the side we can
say okay there's some stuff we need to deal with there but we wanted to focus on how can we test that the cart handles
multiple products to be used for display and so now we have a better sense of what we might need from cart in terms of
its api we have to have some way of finding out and if we weren't sure we could go back to scanner and say hey what did
you need again that's so weird that intellij is not i think there's a i think there's a bug in intellij because when it
was just called scanner which is the same name as in the java util scanner it wasn't able to find it because it tends to
look inside the project and i think it's confused so we're going to call it scanner printer because actually that's kind
of its job now and we'll see that we want so let's actually rename the test as well actually let's rename this back to
scanner and then we will rename it back to scanner printer so we can let it there we go run all our tests um one thing
we'd want to do is our scanner printer test uh we want to so receipt shows zero price to know what i'm scanned receipt
shows item and price for one item and and let's run all our tests make sure we didn't break anything uh so renamed
scanner to scanner printer uh we could take on the scanner role of the scanner printer and have it call the add method
on cart but what i want to focus on is is the card itself in terms of being able to support multiple products so now
that we have a better idea of what the scanner printer wants right when we want to display its receipt for a non-empty
cart what we're going to want to do is for each row here right which we've been sort of cheating with this cart product
name cart total price but that doesn't work when we have multiple items that's not going to work but the reason why we
want to move to cart is we don't want to write another test at this level this is too much work so we need to go back
here and say in addition to having supporting multiple ads and keeping track of the price we'd like to keep track of the
products as well but again we can't just decide at this level what is the method we want to call right so what we want
is add multiple items then part all right so we want something about the contents of the cart but that's really the
given part right given a cart with multiple items when we ask the cart for its contents and so maybe we just call it
contents and so what do we return well what does our adapter need what does the outside world need from our cart it
needs for all items it needs its product name and price because we want to display that once per product we already have
the total price that's already taken care of but we need a way well where to get that information from and so now what
we need because we can't return to two objects right you can only return a single there's only a single object to return
now we're really kind of forced to create a new type because what we'd like is we'd like contents to return a list of
something and what is that something well it can't be string because that would just be the product name it can't be the
formatted string because that's not the job of the cart so it needs to be a new type and we're going to want to return
product um because right now we'd like to be so actually once we have a sense of what this is going to be we're like
wait we're not ready for this yet let's refactor the current code to support product before we deal with multiple
products right so again how do we make this method easy it'd be great if product already existed it would be so much
easier to write this code if product already existed and there was a list of product already in cart so then let's not
write this yet and let's not write this test yet let's refactor let's introduce a parameter object so we'll create a new
class we're going to call it product it's going to be in our domain and it's going to have these two boom this was a
pure refactoring totally intellij driven it replaced note in our test it replaced handing in just a string and and the
int with new product so our test should all pass assuming intellij did its job correctly which you know it doesn't
always do sometimes it makes mistakes but that all worked so now we have product we kind of want to store that too so
instead of storing product name how about we just store so create a field for the product so again we're still refactor
mode right and that just introduced a new field that's not not really used let's now change product name to return
product product name because our goal is to actually get rid of this string so now it's unused but so we can convert to
a local variable and then basically this local variable test should still pass so now we have something that step by
step little step by little step looks like what you might have originally jumped to but every step was driven by an
actual need from a test we know we needed that thing because our test said so so we now refactored right we now have
cleaned up and tidied up card um and so now let's look at where product name is used turns out that but we don't
actually have a test to tell us that it's wrong and that's actually the next test we're going to write when we have
multiple items we'll be forced to abandon total price um but we'll be getting products and so so since we we could treat
this as a refactor and say boy wouldn't it be great if in addition to product name it returned product price and so we
can treat that as a refactoring say that should be a no op no no behavior change so let's go ahead and do that let's
drive that um right so our indirect test is basically this this kind of test testing against scanner and we could write
a test directly against this that we return a product but you don't always have it refactors don't always need to be
driven by like refactors are often not driven by tests this is a refactor the behavior isn't changing so we can say what
we'd like right so we can introduce new methods this is my point we can introduce new methods we can say what we want is
we want a the other way we could have done this is uh ah so we can't inline it hey guy royce welcome folks bringing your
party over here so uh currently i'm doing the checkout pricer exercise hey wheatlow um and so basically doing tdd and
hexagonal architecture for it so the reason why i can't inline this is uses product and so we can again refactor our way
here we can say well let's just introduce and and for this this is not really the total price we want this to be product
uh product price so do we have that does product have that well interestingly enough it does because when intellij
refactored and extracted that delegate it actually created a record which by default has method names so we should be
able to replace this with product oops product price that should be equivalent how do we know we run a test so we have
pulled out product into its own thing we've exposed it here and that means this method this product name is no longer
needed so we can go ahead and delete it so now cart has ability to add products but we can only retrieve which is fine
because then we can uh drive that implementation through this and then we'll get rid of so we're going to generalize
product but let's do a commit since we've got once we did some changes um deleted extraction uh and looks like we got a
redemption for for dark mode so let's go ahead oops i installed a different uh dark mode except oh did it also change
the font size you're not supposed to touch the font size no no no no no you don't do that you don't change fonts uh that
looks good that's a no-no if you're going to write a plug-in theme and you're going to change my font hey fat dog the
repo um that i'm working on uh i have not pushed anything there it is supermarket checkout pricer um i guess i should
expose that uh so this is uh my current repo i'll actually do i'll actually do a push i'm working on a branch um because
uh the idea is for the exercise all right um whenever i switched to dark mode i was so all our tests passed we move
product right so um our eventual goal is we want multiple items and now we can actually um do this uh let's grab this
and so now contents should report uh all the products so we want to call it contents or products actually let's call it
product right so we want to do is assert that um the cart products uh contains exactly come on oh you're not gonna be
able to do that so uh ah okay so there's another intermediate step so before we can get to this we want to and this is
actually um a common sequence of refactorings right we started out with a single thing that was returning uh a single
piece of information which was the product name now we have cart returning a single thing product except we don't want
product we want products so that means we want to do refactoring so that all the code that's currently adding in fact
what is checking this is really just the scanner printer so the fact that it's we're going to return a list we're going
to have to do that as a refactoring so uh that's why i got my refactor hat on so let's do that let's change this instead
of returning a single product let's make it return so list of product would imply that it's something that you could
manipulate but we want to sort of limit what somebody can do when they're getting this information so i think stream of
product there's a way to do this with several uh uh with basically a composite refactoring um but i feel like that that'
s overkill for actually before we do that let's see this let's pull this out into a local variable and that'll be a
little bit easier because then we can say um dot find first get and then this is just product there we go so we could
have gone gotten there through a few uh interesting refactors but i'll leave that for another time remind me i'll show
that all right so let's this was a refactoring right so our test should still be passing and no my hat's not green
because for green it would disappear because i have just like this this is invisible invisible bag um so our test still
passed that means our refactoring worked and now that uh what we've done is now cart is able to return multiple products
so let's rename i really do like contents better because products is like cart.products the contents are a stream of
products that's fine doesn't the name doesn't what branch are we on and no i don't want to pull requests all right um so
now that we've made uh all these changes we've done we're refactoring so we know everything is still working now what we
can do is we can finally oops oh um ah great i forgot we're not in refactor we are in change behavior mode the whole
point was to get to the point where we would store multiple products we are not storing multiple products but now we
have the structure for it right in terms of the api returning all products we're only storing single product so maybe we
could even change this with i think we can let's do that so we're back in refactor mode put my refactor hat on and uh
i'll get to your question next proof in a bit um so we want to do is internally we want to uh store this probably
internally as a list because storing internally as a stream makes no sense so we want this to be a list um but that's a
that's a bit too far so let's just change it i'm a bit obsessed about um trying to use automated refactorings and
sometimes it's just like that's just not worth it let's just make the the change we've got good task coverage uh so here
remember we are not changing behavior so we want to emulate the behavior that we've got um so that means product the
equivalent products and this we're basically treating the list as now i don't think this will work because it hasn't
been i i don't think you can set zero if nothing has been added to it so let's find out i don't know i think that'll
fail yeah because it's null right of course so let's make it not null let's create a new arraylist yeah because it's out
of bounds so we can do is we can um new arraylist um i don't know is it how much worth it is is it to keep backwards
compatibility let's see instead of set what if we just did add so everything still works so we haven't broken any
existing behavior which is what we want right we want to make sure we're not breaking existing behavior uh let's also
fix this and yes i know dark mode is over but my stream is almost over anyway so we'll just leave it dark okay so now
now we've refactored our code where we could wonder could we return this just as products will that pass our current
tests oops product stream is that the same or is that changing behavior that's the same so let's go ahead and commit
actually i'm going to amend that commit now i think we can finally make the change uh that's true i could do a new um
but this is sort of closer to what i eventually want and doesn't break existing behavior so i think it's i i think it's
fair um so x-proof in terms of how do you test multi-threaded code basically minimize the code that's actually doing the
multi-threading and make everything else work and do lots of immutable objects and so multi-threaded depends if it's
doing things in uh parallel and i always forget parallel versus versus concurrent but basically if it's doing things
where it's not modifying shared data so basically try to make sure your code isn't modifying shared data shared mutable
state not shared data shared mutable state and then when you actually need to do that really think about do you need to
do that and then tend towards making making it immutable so my goal um so somewhat similar maybe somewhat like what
wheat lawl said is my goal is is to turn concurrent multi-threaded shared mutable state code to just not do that and
then it's easier to test beyond that i'm not good at that i'm not uh right sweetie yeah could it could it could have
done that but also my goal is like i want to make the the i don't want to just make purely the equivalent i do want to
make the change easy so i want to get as cl sort of as close as possible to the code i need um without changing the
existing behavior so this is pretty much the code i need at least that the test is asking for so now does this work can
we make this work so here's where maybe the change i did was too much and it does right so maybe i went too far so to
sweegee's point let's we can sort of take a step back and we can say look we want to be precise we don't want to
accidentally add new behavior and it's a it's a fine line and i don't always i don't usually think about it too much um
um we can get rid of this products dot equals new we can treat it as an immutable thing right let's say um and take off
the final here so this should work and then if we turn this test on this should fail because it's only storing the last
product all right so the last product was toothpaste and uh this is what we got it stored only the last one still had
the correct pricing total but it only stored the the the last the last one um so we have made it um we've made the
change easy but we've also been careful to not change existing behavior we're basically treating this as a singleton
list that only holds one item i guess technically we didn't need to assign it this now we can make the change that
actually right now we're in red mode so we expect this test to fail so now we can change it so that this and that should
now pass and it does and now we can make this final and it still passes so how did this help us well now we know how we
want to store multiple items in the cart and we can store multiple items in the cart and we can assert that those items
were in the cart right this test is a lot easier to write and assert than what we'd ended up ending up than what we
would have ended up writing at the scanner level which is adding the items and then asserting some because this test
here and this test here and in fact this test here right all these strings if i want to say hey you know what we want
some different spacing we want the well now i'd have to change this test and this test and every single test that is
testing that right so testing at a difference at a distance right the further you are away from the code right so i'm
not scanner printer is testing code that's really in in scanner printer if it were all in cart that would be really
difficult to test and these kinds of changes would blow up and break a bunch of tests these kinds of tests tend to be
brittle a cart that is knows how to handle multiple products we can add them we extracted product as uh turns out as a
record i'm not crazy about the names now that these are in something we can actually drop the prefix so something that
squeegee pointed out before is they both have the same prefix the word product but we don't need that anymore so let's
change this to name and that should change everything else so we've um the cart now supports creating and uh products
properties no longer i understand that so let's take a look at this um let's yeah dark mode is definitely over we're now
in the conclusion phase of sorry i should have warned you put your sunglasses on bug me later please uh where was i
going i was going here and so we started out by just testing against cart we found that when we got to the receipt part
where we started that started uh making the test a bit harder to deal with we still don't have the scanner supporting
multiple products right we don't have a test for that um so maybe we'll write one more one more test to get that that
will fully then generalize this method and then we can basically be done with with the receipt portion uh so let's do
that let's go and that last test oh yeah i guess intellij highlights it in light mode too it's just i guess maybe less
obvious to me um is this there's two things so one we could write another test and we'll go ahead and do that um but
this is starting to get annoying right and it's actually not necessary so i'll talk about that in a second so uh
actually this test was just supposed to show multiple item names and prices in this and what we expect is uh toothbrush
um we expect this to fail because it's only retrieving the first product so it's not gonna have toothbrush in it the
price will be right though yeah so the price is right um but it doesn't didn't have a toothbrush in it and to more
clearly see this we can view this we can see that toothbrush is missing we should intellij formatted this as a
multi-line string maybe i should follow an issue for that because like this quote is really weird and then this quote
that yeah so i've been finally lots of issues with intellij lately with jeff brains okay so how do we fix this well um
we do the same thing as we did before we treat this as how can i make this next change easy so what would the change
have to be is i need to repeat just this line of text but that's a huge jump from where we are now uh i can't do that
with just a multi-line string right we have to have some kind of loop so instead what we can do is a refactoring and
refactor out the portion that we think is is going to then be generalized so let's turn off this test get back into
refactor mode and i'm not going to and so what we want to do is we in a sense want to i'd love to be able to extract
this this is another feature maybe i should file an issue for it would be great to extract this into a placeholder that
then had some oh costa daniel c thank you so much for your prime gaming subscription i appreciate it i know you only get
one of those a month so thank you for spending it here thank you um by the way uh discord if you want to chat about this
stuff that i'm doing um discord's the place to do it uh also this is uh this content is also gonna be be and content
like it and explaining some of the larger issues is in my refactoring taxological architecture so uh yeah so
unfortunately there's no way to do that so i think what i can do is let's see uh basically grab this replace it with
this yeah boy i'm really wishing for like a refactor here uh so we're gonna do string um product row equals and then
that's this i think that should be the same let's see there might be some extra line feeds yeah so i think i've got an
extra line feed because that and i do not like the way intellij is see i think intellij should line up the the triple
quotes even though the boundary is here because of the way that works it's very confusing to me okay so we've now done a
manual refactoring of splitting up the string um so now we can do that we've got that because this is what so let's
extract this to a method which is um product to row road display row product to receipt entry oh that's interesting uh
swedish no there's nothing to turn that into string concatenation because this is not string concat i mean this s is
string concatenation but it's a little bit more complex than that so it would not be a straightforward refactoring uh so
let's inline this so that returns that this should be the so we've now made uh once again we have made the change to
multiple easy yeah i wonder if this is actually easier to read as um but i'll leave it that way uh so i'm not quite done
because if i want do i iterate through multiple ones first and or should i just convert this to string concatenation i
could do a mapping in the join on that method let's do that um so what we're going to say is let's change the variable
and now what we want is product row equals so product map uh we want to map each one to product uh somewhere this new
line stuff so i'm not sure where that joining is gonna happen um this should also work or there might be some new line
stuff that that i'm not sure about so let's see will this pass i think it'll either pass or be close enough in terms of
new line stuff so again uh yep so it was off by the the new line here um but this the line break should be there so let'
s um we could say joining with a line break or we could change this to a line break i think if i do this it will break
some other things but i think i can then remove the space here to take up um and there we go so that gets us to um our
cart uh we can make that file that's fine and so we split along the parts that were applying to multiple right but we
did that as part of a refactor as opposed to part of behavior change and then our behavior change was was basically this
was then iterating through all the rows and converting them we could have even done that um again it's like once we left
the world of getting the first item and went and entered the world we're just streaming across all of them that's that's
a bigger behavior change so we took that that step as part of the behavior change as opposed to refactoring and now we
have a cart that we add items to it um this is still a bit annoying but but i'll talk about uh at some future point
about what um what's what's really going on here because it's not a lot of work to do it through the cart but what are
we really doing is basically testing did we format stuff and did we format stuff and did we print sort of the correct
card or not um and so let's clean this up let's move so this isn't necessarily a problem that we're using cart because
that's what this code is is doing where it can get a little bit more complicated is around the rules of well what
happens when we actually so that when we add you know a toothbrush and a toothpaste we say hey you got a bit of a
discount for multiple items except that no code here changed so what i want for my tests is to test that something
changed in the code that i'm testing if because the cart changed that i need to change my scanner printer tests that's
not great it's sometimes you can't avoid it uh but in this case we would be able to avoid it um or at least sidestep it
a bit uh but i'll leave that for for another stream so we've gotten we sort of didn't focus too much on the on the cart'
s behavior right we didn't we didn't even get to to any of the special deals because we wanted to focus on refactoring
uh project structure is now basically this right we've got our adapter an inbound scanner it basically we're sort of
treating as an in and out right it adds stuff to the cart we haven't actually explored that aspect of the adapter yet um
and then what it gets when it queries uh the receipt um it basically gets the the text right it got the contents the
core domain stuff right in our cart we've got list of products so our apis we return stream of product and we have a
command method that adds a product and that's it um we have this in total price that's a query method also uh the int
eventually we would change to money um but everything else is but this is still pure domain right we see nothing in our
imports we don't see any strings and then we've got tests against basically our cart that are also pure domain right
we've got strings in the name of our products but that's just used to create a product what we're passing into the add
method are these products and we could actually do a little refactoring on our on our test here we could say this is
this is a constant why not just create a constant uh which method names are long you're talking about the test method
names because those are not method names those so let's create this as a constant we'll and then we'll create this as a
constant so now it's a bit more clear that that we're really working at the domain level we're just adding products
adding products checking price checking so this is so um fb dude mentioned that that names are long and i'm again
presuming you're talking about the tests um and and i think it's a really important way to think about it that the
method names here on domain objects and other objects it's important to have them be concise all right in other words
not too long if they're long that's probably indicating that you haven't quite reached your abstraction but these are
not method names and this has nothing to do with naming in java being verbose i'm sorry it has nothing to do with this i
would write test method names like this in any other language because this is supposed to be right and uh yeah i've i've
tested are often longer than this right when i add two spreads and the product type prices is one dollar empty cart is
right this is supposed to be communicating as much as possible what the intent of this test is and so i actually don't
think about these as method names because nobody calls them other than the unit test runner which doesn't really count
like none of your code calls this so it serves a different purpose you could just call this you know um you know burst
test and then put a display name maybe maybe you find that useful i i don't but it is sort of the intent behind it is
that the method name is serving as the description of what is this what is this test doing right in kotlin you can just
use the backtick and you can put spaces and all this is uh this is what we what we want and let me go push this oh i did
push it great uh so wheatlel asks about the definition i don't know that there's a definition that's useful other than
uh because it gets gets a bit um fractal like so to me object-oriented programming is where uh objects are individually
responsible for the behavior around information and you communicate between now there's different so oop to me is like
not everything in the application is going to be oh to me everything inside the hexagon is oo um the stuff outside of it
can or might not be that totally depends on the framework and all the things you're doing but it but where the domain is
concerned that's where i want objects to be responsible for the behavior and manipulation around information you know so
using encapsulation that's important commands and queries are important um thinking about behavior and not just
information so i don't know if that's a great definition but that's uh i love coding uh here's where the jasmine respect
style test naming is regular strings it's getting difficult uh fpdude is a true the prototype based oops original um i
don't know i mean you'd have to go back to like simula i mean what do you call the first object-oriented language is it
similar does it go back before then were those prototype based i don't remember um small talk is sort of popularized i
don't think that's prototype based but again it's been a while since i've so for me the object oriented programming and
design is critical for the the inside of the hexagon right our application core domain our domain stuff outside it
depends i still want to keep stuff as object-oriented as possible um but some of it might just be weirdly event driven
or procedural totally depends on on the framework you data only objects so data transfer objects are important and those
don't abide by the same principle because all right well that's all for today that's all i wanted to do for today was
get um basically do test driven development hexagonal architecture for the supermarket market checkout pricer exercise
um if you want uh to see what we did this that's actually the repo with the looking at the branch that we just we're
working on we're working on the stream branch the main branch is if you want to do this on your own and so the intent of
this is not to just watch me do it um although i love you for doing it for watching me do it but the idea is to do it on
your own go through the stories how would you do it what stories would you do next um if you focused just more on on the
cart special deal behavior where would that lead you uh there was sort of a decision point in you know if we look at the
commits um all right basically when we um i think it was around here failing test for multiple items uh it's at that
point that we moved the rendering on its own to a separate class to abide by hexagonal architecture say you know what
we'll worry about that later let's focus on well you could not be here and then you wouldn't be watching um or you could
be here not actively watching and just so this is sort of a decision point and there were other sort of decision points
where we could have gone a different direction so i explicitly went from here so everything here and here and later was
was sort of with the hexagonal architecture in mind we could have gone a different direction and again focused on the
cart and its special deals and and sort of put to the side the whole thing around hexagonal so so uh my website um
ted.dev i post articles i'm currently uh finishing up my series on the predictive test driven development so if you go
to ted.dev you'll you'll see this is my new websites that i've put up in the past month and i'm basically trans
transition migrated all my articles to here you can find out about joining my discord which i encourage you to do if you
want to discuss some anything that came up during this stream and um that's it so thanks uh thanks for hanging out and
um i'll see you on the next stream where what we'll do is now that we've separated out adapter versus core domain we'll
start seeing what happens when we split the actual scanner from the printer so what is the scanner doing how does the
add products come into our system so we'll need to deal with the scanner part and then should we really have a scanner
printer maybe printer is some separate entity that we need to treat separately and so we'll split that out into a
separate adapter and i think that's where we'll take it next all right thanks folks i will see you next time
