# TDD & Hexagonal Architecture Exercise： Supermarket Checkout Pricer - Part 3

**Video URL:** https://www.youtube.com/watch?v=wATcmbOZsV0

---

## Transcript

on today's stream mainly continuing with uh the supermarket checkout pricer exercise that i've been doing for a couple
of streams now uh yesterday we got to the point where um we got uh almost all the test passing did some refactoring and
uh now we're gonna go and and add some more features and then look at a bit um of hooking hooking things up to um an
external service that actually provides the price for for the items so uh what we've got here uh we've got our cart
service uh let me clear the and so we've got um one failing test uh and that's the test we're gonna be working on
implementing so we had done all the refactoring to um get to the point where we can now implement this behavior so what
we've got with this project is as items are added to the cart so inside of our domain we've got a few domain objects our
cart product and receipt some tests against that at different levels and then we have our cart service which is part of
our application services layer and so if we take a step back and it seems like um what what i'm going for here is to
create a small but but sort of non-trivial application um driven using test driven development but uh structured and
organized using hexagonal architecture so if we look at the sort of hexagonal architecture diagram of what's uh what the
system is we've got um something that basically talks to the outside world that's our product scanner uh right so it
gets input from a scanner which you know sends it sends the information however it sends it in and then uh the code
within our system then sends that information by calling a method on the cart service that's part of our application
services layer it then um creates a cart deals creates products and does all that work and then the cart and the product
work together to generate a receipt we have not yet done the receipt display and we've also for our test purposes we've
stubbed out this product price fracture so that's kind of a high level view of of the project where where we are now so
we've got product it's just a record it has the upc and and it's price um receipt has the total and basically list of
string of products this we're going to change because we've introduced a new basically value object for product and cart
is the calculation code for both the total price but also taking into account discounts so all the discount work uh is
basically um this code and that's one of the things we're going to want to refactor and then we can actually uh
implement this last test which is um discounts have parodies you don't we may not want to give both half off the second
one you buy and a 10 discount so uh what we'd like is to here we've decided right and this is a business decision we've
decided that two items that have 10 discount only half off discount applies um which is actually better for the consumer
because it's half off as opposed to 10 off both uh but that's there's no sort of correct answer here it's which one so
we decided that we wanted this one uh but right now as we saw when we run the test we see it fail because um we're
actually getting the 10 off both right so 9 plus 9 is is 18 whereas what we'd like is 10 so there's some other things
that we want to look at um and that's uh right now what we're sending in are these strings we're not really looking up
they're amen uh and so um that we're gonna have to figure out so now that we have um the the pricing working sort of the
way we want it so basically uh when we add a product it just gets added um and in fact we don't need to return anything
because this this should just be a command i don't think anybody's using the return value uh and let's do a commit um
change add method to the command when i talk about commands and queries the at especially in the domain layer in the
domain object layer you generally want your methods on your classes to be of two types commands that basically request
state change so here we're adding a product and a query which asks for information that may be calculated or maybe just
returning something that is already stored so here our query is total and what it's doing is uh basically figuring out
the discounted price for each of the products and then basically does reduce by by adding them so the question is is
this test works right ten percent on this item we get nine um here uh ten percent we've got two of them so that means
it's not being considered for uh the so let's take a look at why that is um so it's basically here so the priority in
this statement is if it's the 10 off product and one of the things that we'll have to figure out as well is how do we
know which ones get which discounts right so there's the whole how do we configure this thing um but for now it's
hard-coded uh if it's the ten percent off one we calculate we figure that out first um so uh if we want only the half
off your second or later purchase discount uh so we need to see sort of is it eligible for half off and then return this
otherwise so this code is a little bit a bit um complex complicated uh and maybe we want to refactor it a bit so one of
the things that's that's causing a bit of difficulty in understanding this is there is this set for eligible products so
that's what i wanted i forgot the shortcut for highlight usages so if we look at the usages of this eligible products we
see this is when we're adding the products to the eligible list and so we did this yesterday so that we could figure out
is this product eligible for the multi-item discount but we can't just look to see how many of them are in the cart
right if you add one of them to the cart it's full price if you have the second one the first one is still full price
the second one is the one that gets half off and so we basically did some coding on this yesterday and ended up with uh
a mechanism that uses a separate set of product to see have we seen this one before so the first time around when we're
checking the product we haven't seen it then the second time we've seen it and all future times we've seen it before so
it's always eligible and we only need a set we don't need a list because once it's in there it's eligible the problem is
this variable is used in three different places and what's even more confusing is we initialize it here right we
basically reset it every time we calculate the total uh and that's that makes this code a little bit complicated and so
we can't just sum over all the things and calculate the discount we have to have this thing that that tracks eligible
products for us with our discounted group product price um if it's eligible then we we basically return the half off
price um otherwise we added here to say hey we've now seen this and the next time we we check for discounted group price
we so this field is used in several different methods uh and that means when you're trying to read this code you have to
understand what is it for and how does it get updated and is this even the right way to do it so i'd like to try and
simplify that like how do we know a product is eligible well we know we need to reset it because we want to do that
every time we calculate totals right so again we want to not discount things until we've already so when we discount
this code i want to kind of take these two methods and combine them so this one is fine this method i think is fine it's
basically is this product eligible what's confusing i think is these two methods feel like there should be a different
way to split them up and so from a refactoring standpoint what uh what i often do is sort of smush them together and
then look to see if there's a different way to split them out that makes more sense there's something else that is sort
of in the back of my head which is we've got a collection here and we've got a bunch of behavior associated with it and
this specific discount is not the primary concern of our cart class right our cart class is doing other things and so
for me those those three things together is this sort of an unconstrained type is there a behavior associated with it
and is it in the class that's doing other things which is a code smell that tells me that maybe there should be a class
that represents this idea of is this product eligible and if so calculate its its discount and so even just with that
we're starting to see that maybe there is another class that we can pull out there's a whole idea of pulling the
discounts out all together and pulling those out to be a strategy which would basically be this this code plus these two
methods so there's multiple strategies for discounts right 10 off half off the second item things like that and those
could be pulled out separately but um i'm not going to focus on the primitive obsession i want to see if i can clean up
this code first to see if there's anything obvious so i'm going to do is i'm going to take this and i'm going to
basically inline it um but it's not all that big and what's nice about this is now it's a lot more obvious that this is
the 10 discount thing in fact having to read this and and know that this is the one that's 10 discount is is hard
because like i don't know what this means other than some specific product and then i then i see the 10 discount being
applied here so let's make this easier to read by saying uh pulling this out into a method which is is eligible if i
could spell is eligible um actually let's drop the word is it's just eligible right so now the priority of applying
these discounts is clear if it's eligible for 10 will you just return the 10 off which means it is not going to be
eligible for so that's because it immediately returns um if it's eligible for half off then we calculate the half off
otherwise we add it to the list of eligible products for half off and um then return just the normal price so even this
variable is not specific enough what does eligible products mean so let's make this one more clear which products for f
and so when i'm coding i'm constantly renaming things to make them more clear if i encounter them it and it feels
confusing um and so this is uh a heuristic i call confront confusion where if you're confused and you can change a name
to relieve that confusion to clear it up then do it right away especially for fields that are private which most fields
should be or if it's a method that's private or even if it's a method that's public if it doesn't uh affect library api
kinds of things then you should rename those as well there's no so he says have empathy for your future self absolutely
and your future self might be five minutes from now so uh these kinds of things i want to rename as soon as i can uh and
siri be quiet um all right so let's run our test because that was a refactoring that was not trivial um but it was in
line and renamed so it should have been straightforward but let's run our tests just to be sure all right so the test
that we expected to be failing and still failing but now we can change the priority we can say half off to apply first
let's take that move that up now we think that'll work except not yet because we now see that this eligible thing
happens here so is that going to work so because it'll drop from here but then if it doesn't get picked up we'll still
get 10 off and so now what's interesting is i know this is going to fail are other tests going to fail i don't think
other tests but does that change how the current i don't think so i think it'll still be 18. yeah so we didn't quite fix
it so we might say oh well let's just take this and move it up we at least account for it being eligible so the next
time around when we ask to see if it's eligible for half off it will be eligible for half off i don't think this is
going to work either because i think the first time through it's going to get the 10 discount the second time through
it'll get half off so i think we're going to end up with too much of a discount we'll end up with yeah so we got 14. but
notice that i predicted right and this is part of my predictive tdd uh process i predicted how it's going to happen
because that is useful information as well that tells me i understand this method which is non-trivial um any anytime
you've got multiple ifs uh you know you're you're getting into complicated my ability to predict means that i have we
can't just so let's see how we're going to solve this uh we might have to make this eligible for so um so now we should
be back at so one thing that that moving this around tells me is that it should actually be part of uh should be part of
asking if it's eligible we only want to apply eligible for 10 discount if there's only one of that product so here's
where we can actually look at the entire cart so the eligible products needed to be separate because we only want to
discount the second one not the first one here we want to see if there's more than one of them um then we don't then
it's not eligible for so we used to have uh a thing that counted um we took out so the eligible for 10 discount is not
just it's also if the products uh and so here we'll do a stream um and we'll filter for and if that's greater than one
then we return false alright so if there's more than one of so what's interesting about this is did our business people
realize what the implications of this rule was because the implication of this rule is um it's only ten percent off one
of them not ten percent off two because you got the fifty percent off the second one now it's probably likely you would
not apply the buy one get one fifty percent off to all items right so we haven't quite associated item uh items with um
specific discounts but a lot of times the rules uh as they're defined as you implement them you find that there's really
an implication for for uh what that rule really means so if we're saying the half off takes priority what we're saying
is ten percent only applies to one item and if the rule words would was originally stated that way it would have been a
lot easier would have said oh okay of course you will only get 10 off if you only have one of them so let's see if this
this works i think it will so and something that is also sort of do we want to as we add items is a list really the
right way to to handle these right because what we've got is we've just got a list of product you add three of the same
product you end up with three product entries but a lot of times it there are line items right in in in an order you
basically say it's not that you have a product three times you have um the product with a quantity of three and so the
quantities associated with that and boy wouldn't that make some of this decision making easier if we had a map of
products to their quantity then we could just go through all right which products um have two or more apply the discount
to those and then apply whatever other discounts are so that might be a refactoring direction to go but now that our
test passed let's go ahead and do a commit right because that's really what the so we have tests to basically say well
if you got two the second one is half off if you got three the sec the second and the third are half off um here we've
got if you add have one then it is 10 off but if you've got two the second one is uh but that's quite a bit of com and
mainly it really bugs me because of it being reset each time and that that somehow seems wasteful to me but also
confusing because you don't generally expect a so one thing so and i want to i want to note this is but this state is
not observable not directly it's most certainly changing state every time you call it although in a sense it's resetting
state but processing this code changes state it changes that the content the contents of that set um but that's not
observable right because we could we could have done this in a number of different ways uh and if it was a local
variable right because we could put all all this code we could stuff it into this method um and then this would just be
a local variable and we wouldn't say that that changes state um in fact we could actually make these sort of uh a bit
more functional by passing in this set as a parameter instead of uh having a share a field and so you want to sort of
keep in mind is that this is a query method and even though it looks like it's changing state it's not changing
observable state at no time are we asking from the outside what are the eligible products for half off that's an
implementation detail and there's a number of different ways we so that's great for me to notice that because one of the
things that i constantly collect are cases where it may seem like rules that i use or heuristics that i follow don't
always apply and so sometimes clarifying and showing examples of hey it looks like this is modifying state doesn't that
violate query gives me a realistic example that i can use to explain it so i'm always on the lookout for um all right so
we've handled the priority of these two special deals um we could probably do some additional um like for example this
piece of code we we could extract to a method count so that helps a little bit that's sort of a tiny clarification um
but i think there's a structural change that that we need to make uh which is how do we associate for example this deal
um like we should probably even be checking this this first i mean it's not like this is uh it's not like this is
terribly inefficient um but we're doing a lot of uh so let's see if i can not sure that's but what that does allow us to
do is is again reiterate that what is the rule it's that if this product is this specific product and there's not more
than one of well what's the opposite of not more than one of right so we now have this this bang in front of it and that
makes this a less readable well not more than one of is um there's no unfortunately there's no way to in with with a
single refactoring just to negate this and and and change this so we'll have to rely on our tests to do that so what we
can do is we can change make this first change which we know should break stuff so we'll run our tests expecting stuff
to break and and they do which is great and now we can basically say this if we change this to equal we've now restored
uh that behavior now we can rename this method because we don't want to forget about that and now we've simplified this
method we've put this first because there's no point in looking for the discount unless it's one of these items uh
basically inverted one of these manually but note that we did it one step at a time we changed a little piece of code
expecting it to fail if nothing failed that would have been concerning because it would have meant that we don't have as
much test coverage as we thought we did so let's go do a commit um or eligible uh so let's reorganize the code a little
bit let's take um and uh put them here i'm going to take these so so code organization is is really interesting um i am
not as strict as as i think some people are uh some people like to put all private um and then all your public methods
at the top uh i tend to do that but i also don't want those private methods to be too distant from where they are in the
code from the sort of method they're being used from so it worked out that all of these methods are totally related to
this total method so that way it's the last public method but but what's interesting is when i think about sort of how
would i organize just the public methods of this and i know this is getting into really ocd like almost ocd like
behavior um i tend to think of the sort of priority or quality or importance of those methods um total to me feels more
important than something like receipt receipt feels more terminal so i feel like it's it would need to go after total
but anyway that's kind of the way i think about it i don't worry too much about that because i generally don't navigate
code by by trying to find it in scan files i do a lot of all right um let's okay so we could continue adding discounts
but i think we're at the point where um i want to take a step out and say okay well how do we know um specifically for
this product right this constant is constant literal which i guess is redundant because all literals are constants this
literal is problematic right because um this is a specific upc and how would we configure this um and as i mentioned
yesterday the tests that use this it's not obvious why this one is eligible for a 10 discount so it seems like we want
some way of querying of something being responsible for for saying what discounts are available for um for a product uh
we could immediately jump to something more complicated um but i'm gonna do this just you know sort of small steps so
there's actually two parts to this rule right there is eligible for a 10 discount and then we further apply the rule and
there's only one of them in your cart um those i feel like are two separate things because um because that's what it
feels like doesn't mean i'm correct and certainly we could say well this one we want a 10 discount only if there's one
this one we want a 10 discount if we don't care it always gets 10 and then you'll get into complicated scenarios of well
okay if this other product is 10 off and there are two of them which takes priority the 10 off with a half off and that'
s where you'd have to really split out uh the application of the discounts to uh the specific items um it i'm reminded
of uh something that somebody posted on twitter yesterday which was about um we coders tend to be attracted to
complexity and if we don't find it we off we sometimes create it um so that just came to mind because i'm thinking about
all the complexities and i think though that's that's an important thing to think about because um that i think is what
makes our code more complex than it needs to be and this is what i like about test driven development is it really
guides us to writing the simplest thing to get the thing to work to counteract our tendency to write more so let's just
say we want um to be able to now apply of ten percent off to more than just the zero nine eight seven product so that's
when it would become clear there needs to be something that can basically tell us yes or no for this specific expression
right is it can we even consider it as because i would have assumed somebody you might want to refresh your browser so
in order to basically externalize this um we have a number of streams yeah we have a bunch of streams running your
computer your browser might not be able to keep up um so i just did a test uh i'm seeing my stream on on twitch so how
do we externalize this so we can't remember we're in we're in a class that's in our domain right so going back diagram
right we're looking at code that's in here right this is inside of our domain all right this is our core domain so our
core domain um must not have references to anything outside of of the domain like um we can't we can't have this have a
reference uh in its constructor to um but we're getting a product handed in so why can't that information be in the
product that makes sense in fact that would be a good use for a product right um because they're the product is being
handed in because that's what's being uh that was what was originally added to the product in in the first place so if
we think about what is product right now it's literally just a bag of data it has a upc and its price so in addition to
its price maybe we could have its discount or some kind of discount rule and this gets into how do we discount do we
discount per item sometimes often uh sometimes we discount according to category like hey all produce today is you know
is 10 off um but right now we don't have a feature for that there's nothing uh telling us that we need to do that so we'
ll we'll leave that alone so it seems like product then should have additional information about what kind of discount
might apply right is this eligible for buy one to get one half off because we actually don't want it for all items maybe
we only want it for our toothbrushes and so product would need to have the information of some discount rule not
actually writing this code i'm just sort of sketching it so i wouldn't i'm not allowed to write code unless i have a
test that fails or unless i'm doing refactoring so this is kind of what it would what i imagine it would look like so if
we're saying that that's what we want um then uh we can do this as a refactoring right because our behavior is what we
want we're just uncomfortable with and by the way if you're watching along as i push code you can track it on the github
repository um just make sure you look at the orthogonal architecture branch because that's where we are there's actually
two branches there's one called stream which was my original there we go um so that means that product has to have along
with it uh what discounts it's eligible for well let's drive this um not drive it with a test uh drive it by changing a
test actually i think we could modify product and then have all the code basically modify this records in a sense
constructor which would modify all the code and put so let's so this is our special deal test let's actually take a look
at just our regular cart test um so what do we want in terms of the rule we could start just with an enum and just do
that for the 10 off so let's start there and see see what happens so let's go to our 10 rule which is this one um let's
pull the product out into a and what we'll do is we'll add uh we want do we we want to have constructor or we could just
have a default for that let's let's see so let's create uh and we're going to say this is uh 10 off so create an enum uh
this is in our domain and then uh we'll constant now i want to create a backwards compatible constructor let's see what
happens if we create a constructor so this is our upc this is our product price oh oh intellij so what happened was uh
when i created the enum and now i'm like hold on let's uh let's undo that let's undo creation of that let's go back here
so when i created this class this uh as an enum ah so it defaulted to tests i should have selected that here okay let's
redo this the correct way and now uh now create the enum constant that's fine and now it's not now now that's fine so
let's bind these um why did you do that that's not quite uh upc is universal product code is basically the barcode that
you find on all products that you purchase anywhere i know if it stands for universal or uniform but it's it's basically
the barcode you see on your products and that's how you know when you scan them how much they are uh no that's a really
strange thing it did i wonder uh if it's because uh so this can't be final unless i actually assign it so let's say it
was null uh no wait there's an instance field i can't have this on a record so i don't know actually so in records can
you have because really what i want okay really what i want is uh so intellij should have basically done this except i'
ve already got the parameters so i should have done that already so whatever all right so what i really want this is
annoying to do with records um product price so basically if you don't specify a uh yeah it's luca's uh all the
everything is final you just can't so this is what i want to so by default uh let me upc product price discount rule is
required um but if you only specified these two then it fills in discount rules no which i don't like um let's make sure
everything compiles because we're we're in refactor mode so let's make sure we haven't broken anything okay great uh but
i don't like null let's fill this in with a discount rule um so at least we have okay so now this test abides by the
good test heuristics right it's arranged into the three parts that we want from a test given when then and given a
product that is has this upc has this price and there's this discount rule when we add the cart to the product then when
we ask for the total we expect it to be 10 off of uh of 10 uh the product while if the discount changes we just throw so
at so right now products are not persisted where do they come from um right now we make them up but where do we want
them to come from is that information uh will be passed into cart when we do an ad but at that point we would have
looked up what the discount rule was at that point so once we've added it to the cart um by the way this is this is an
interesting uh i ran into this some years ago um so here the local safeway supermarkets they change over their their
discounts uh basically wednesday turned out i was shopping very late on tuesday uh you can probably guess what happens
next turned out to be after midnight um and so uh the discounts were not what i expected because it was already it had
switched over to the wednesday discounts um so if the product was at it's basically the discount at the time the product
was added to the cart but anyway so this is not persisted so i don't have to worry about it being final and once it's in
memory the discount doesn't change so that's fine as well right it's immutable and uh it has attributes and it describes
stuff um but as i say as i was saying with the test we now see this rule is explicit and tells us and this is what
information we didn't have before if we wanted to make this even more clear we could pull this out into a but i i think
this is fine uh although i don't need value of nine i can just say nine i think i had that because i forgot that was
equal by comparing those okay so that's that's even better great so now our upc uh sorry our product has a discount rule
um by default it's none here it's 10 off except of course in our cart we're ignoring that um but that's fine this was uh
this was a refactoring so we can say instead of product upc equals this we can say product discount rule they did not
expose that as a as a as a constant actually look they actually keep an array of them because when you do a value of and
it already has it then it pulls it out of the array but they didn't expose it as a constant at least not in my current
version of java um so this should be equivalent to what i had before um i think i need to refactor my test a bit let's
product with 10 percent off because while this is equivalent but we've got tests to make sure that um things that
shouldn't have been discounted aren't uh and this one which does have a 10 up discount should uh so now i can replace
these if it's not then i've done something wrong but it's equivalent yeah i wasn't going to even address that 3d um all
right and so i can prove to myself that this code is doing something right so i i like to do these manual mutations uh
so i'm going to say none and this should break a whole bunch of things because everything that was not supposed to be
discount will be and the stuff that is won't be so i expect to break like five or six tests if not more seven tests so
the one that we were looking at is ten percent off didn't do ten percent off the ones that did do um that should not
have had ten percent off did have ten percent off so what's nice is it failed in the way that i expected and so i often
do these manual mutations either part of trying to get the test to fail in the first place or really checking is this
being paid attention to is this code uh it's liquid this is why i'm using big decimal so i don't have to figure out
floating point error whenever you're doing monetary amounts or anything that deals with decimals and you exp and
basically you're not doing things where you don't care about fl like basically money stuff you want to use big decimal
or money is 9. um although you did point out that it did make me realize that product priced at n and ten percent of
discount there we go the nine is totally decimal just because i don't have a decimal point doesn't mean it's not decimal
i'm not quite sure what you're what you're asking it's looking so i can say 9 i can also say 9.0 i could say 9.00 um it
doesn't care because uh when it does this equal by comparing to um it ignores uh precision right nine and nine point
zero zero as far as i'm concerned are equivalent uh and the search a library handles that for me all right so we've
replaced our uh checking to see if the product is a specific product has a specific product code with now doesn't have a
specific rule so that was refactoring let's go commit moved specific check of upc to looking at products um one of these
days i have to think about whether i want to extend a search a's big decimal support to be able to pass in um um
probably longs because if you don't have a decimal then expressing it as a string is a little bit odd but what's nice
about doing it this way is i can say you know if it was 9.25 i don't have to say big decimal value of this thing so all
right so we applied our rule um now that we have a rule in place let's go uh do we um uh do i want to write a test i
don't um except i don't want to leave it as this i said except mine what are you talking about okay that's fine i think
i should have done a rebase in that case not a merge but whatever okay uh so all our test pass we're now applying the 10
off rule um this is interesting because we're saying that it has to have 10 off but isn't that part of the rule who
knows we'll leave it uh says luke you're confused because it's not a big decimal right this string is not a big decimal
but it is converted to a big decimal for us by the is equal by comparing to uh like a search a library so internally it
does if you pass it a string it does because big decimal right big decimal a big decimal uh with basically a string and
it will parse it but i decided i didn't like that because that's more noise than i need and it knows it's comparing it
to a big decimal because total is returning a big decimal so this equal by comparing to um is uh the abstract big
decimal assert and so so um all right my tests are still running okay great we're still passing great so let's see uh so
now if we look at our um when we see add product there's an implicit no discount rule is right now when we add a product
how do we know when it's discounted so here's where we start integrating uh yeah and tsuki is correct um i mean you look
up yeah so basically big decimal has a has a way to convert from from string to to to its internal big decimal and that
basically just parses it um and in fact you can have it parse all sorts of different things um so here when we're adding
the product right so the cart service is in the application layer right so it's here and that gets our price we can have
then that fetches discounts so let's do that let's come up with a port um now now you know why it takes me so long on
one of my streams probably next week i'm going to work on my diagramming software that i've been wanting to do for a
while so now we've got a port um which will be the discount butcher and doing the rotations of these things is much
easier with math than than doing it uh doing it by the eye uh service is part of the application services layer so in
hexagonal architecture um there's a layer that's part of of the hexagon that's in between the outside world and our
domain is application layer and that's where the application services live so it's you can consider it an api for your
adapters it's not um it's not an external api but it is an api and the reason why i want to be clear about it's not an
external api is most people today think of when they hear api they assume http web api but api is any application
programming interface any anything standard that you can plug into so um the service is the api for our application but
it's not meant to be connected to directly by a web request you have to if you're going to do that you have to go
through so what we're doing is we're actually writing tests um oops so we're doing is we're actually writing tests
against this layer directly uh right now we actually don't have a product scanner adapter so right now this thing
doesn't talk to the outside world um so we're testing it at this and what we're going to do is we're going to replace
this thing so generally our outbound adapters we replace especially the ones that are fetchers we that's kind of my my
heuristic um and this goes with some of the naming stuff that that i'm trying to uh pull together which reminds me how
to go back so our discount so we already have a stub for our product price fetcher even though we don't have a concrete
implementation because honestly i don't know who to talk to yet to get that information we have a representation of that
port here what we're going to want to do is introduce another port for our um so i don't think a lot about design
patterns uh the design patterns that might come into play is strategy um but the design patterns that i'm using uh
really are more associated with the hexagonal architecture right so having separate layers having uh individual
implementations having ports as interfaces um to invert dependencies um i don't i don't think a lot about design there's
a tendency to overuse design patterns you want to use what's appropriate i don't even know that we have a factory
anywhere here so there's not much in the way of design as i mentioned we probably will when we implement cart when we're
figuring out the the discount we might have a strategy right so for this rule here's how you apply the the discount that
um i don't think i have any factories though i mean unless you consider constructors factories because technically they
are ways to create objects but they're not separate from so we figured out that what we're going to want to do is cart
service so now we were doing a bunch of tests at our domain level right we were basically doing a bunch of tests
directly against and now what we want to do is um and so that's why we were hard coding the discount for a product but
ultimately um what the discounts should be so that's the job of this this discount fetcher so some service and some
external service which will also likely uh which would hopefully be hexagonally uh driven and i'm actually going to
write some small services to serve the role as external implementations of these the product price fetcher will be
trivial the discount fetcher that has to do with with applying discounts uh and it's a separate service doesn't have to
be a separate service so i might actually create a separate module um for that but anyway right now all we know is
there's some discount fetcher that is external to our system and we need to get that information the domain cannot get
that information that's by the time the domain has a product that information is already embedded so the card service
needs to coordinate that find out the price find out the discount if any and since what it's doing is it's meant it's
figuring out how to manufacture that product and that actually presents some interesting right speaking of of the the
timing issue i mentioned before about tuesday midnight tuesday 11 59 wednesday midnight the price switching we would not
want to when we persist our cart we actually don't want to persist the full product with its price and discount because
that could have changed prices go up and down especially these days they go up so um this also leads us to like does the
cart really need that information uh should we hand in some representations of that in memory um there are all sorts of
questions around that that we'll we'll get into at some point all right uh so we're coordinating the fetching of the
price but now we're saying we want this product let's actually pull this out into a variable um so we've retrieved the
product price from this external service and now we want to retrieve the discount so that means we're going to need a
test to drive this behavior so let's find out where our tests are for this oops so we've got add product via cart
service our test is going to be having that product with 10 with so i'm just noticing that um so intellij you can turn
on where it used where moving forward a word goes through the camel case it seems to jump over the 10 which to me that's
a bug i think that's a separate word but anyway uh so add product uh where uh has 10 percent uh i don't need to say add
product so okay that's good enough and so 1995. i agree naming tests is the hardest is one of the hardest things but
it's one of the nice things is once you've figured it out the rest is mechanical but yeah in general naming things is
hard but i think tesla to me is a bit harder because there's no natural abstraction um like i can you know think of you
know great names for for classes and even for methods because they're abstractions of things test names aren't
abstractions they're just nouns and that's what makes it i think a different kind of difficulty all right um so let's uh
create our product pricer stub oops um we want 10 let's use five here you know let's use eight that's our cart service
we're going to need our something else but we'll do then we expect that cart service total i don't have a live template
for that hold on i want to create a live template so if you're not familiar with postfix uh auto completion in intellij
you're about to get learned um so let's go here filing code templates oh look i already have it open uh live templates
uh this is a postfix so i don't need to surround with so i'll add basically duplicate this one uh this is going to be uh
cert by so sir uh so by comparing two uh assert that and this is uh so there's a certain it's not always obvious about
domain terms and behavior and things like that but i'm often extracting code and creating abstractions uh and so the the
domain is you know it's already a small piece of it as opposed to something a bit larger like a test so all right so one
it was equal by comparing to um or is it just a postfix uh i forget which one i want here so let's um actually that
should have worked oh there it is oops because this is the autocomplete which is this one yeah that's not the one i want
i want yeah the problem with justin is auto completion isn't enough because they both start with is equal um i'm not in
post-fix completion you're right that's why and what's interesting is um they really need to group these things together
the whole post i mean what's really frustrating is the whole post fix uh editing experience in intellij feels like it's
been incomplete for 10 years like this thing has not changed i have at least two open issues against this dialogue to
make this easier like for example you can't change this description from this ui you can actually change it in the xml
which gets stored um but you can't change it here uh and it it's so it's really annoying yeah so i have the assert the
raw assert that i have this one um but i want to duplicate this one so let's go uh duplicate i don't know why it won't
let me duplicate uh we want anything that's really non-void that's fine and apply to topmost expression and so here this
is the expression we want and then this is and use static import if possible yes why didn't it let me can you not do can
you not duplicate your own hmm yeah i don't think the duplicate button works and clearly alphabetizing doesn't i'm also
loving the fact that it changes the end location to this xml spot thing i don't know all right let's try this again the
whole that okay um yes uh please vote for for the issues i'll post them i'll post them later please vote for issues for
improving post effects postfix custom postfix creation uh hey there uh is it loden rogue or is that an i i can't tell
the difference with this font as that's an iron l but um what am i working on i'm working on what it says at the bottom
of the screen i'm working on this checkout pricer uh you can do you can always do a bang project and that'll tell you
what i'm working on uh and so what i'm working on is um what's often given as a as a an exercise to people who are
learning and since we're all learning and therefore we should all do it um and so i'm basically taking this exercise of
how would you calculate the total of items in a cart given various discounts that could apply so items have prices and
you apply discounts and so i'm doing a test driven but i'm also organizing the code according to hexagon architecture so
right now what i'm doing is i'm adding uh the ability to specify the discount rule for a specific product so right now
it fetches when it adds the product to the cart we get a upc which is the product code we go look up the price and now
we're going to go look up as a new service we're going to go look up the discount for it all right so uh we expect that
if the discount was applied um then this should be 7.2 and by the way for those of you who are not already a part of my
discord um i'm always looking for new people to join our community and discuss things and ask questions things like that
uh all right this should most certainly fail because right now by default there's no discount rule um at least not for a
single item so we expect this to fail uh it will fail because we'll get no zero that's troubling why is it zero ah okay
perfect example of why predicting failure precisely is so important who and i'm writing this down because i want to
because i'm always looking for examples of where uh of where these kinds of things happen so this test failed the
expectation is that this test should have failed because of i said the price was eight right my product price fetcher
when you ask it for price it should but why did this test result in zero nope it was integer math that does the stub
return it i'd program the stub to return eight if we look at the but now given your knowledge of what the why is this
test failing in the wrong way they both start with tooth so when i when i did the autocomplete um it picked toothbrush
and so what happens is the stub i should it's a programmable stub it's a little bit too flexible perhaps so return zero
if it's not in in the stub yeah i do need yeah but this is so important of if i didn't predict precisely and stop
because it didn't fail in precisely the way i predicted i would have assumed that everything is fine and continued to
work on the code but now and then would have wondered why something didn't work um now i have uh i've caught myself
early and that's one of the main reasons i i do the precise prediction is because if it fails for the unexpected way it
means something's wrong could be you misunderstand the code or it could be that there's a problem with the test no it
returns zero which is now that we understand now we can predict oh this should return zero because the product we added
is not the product the product that's in the stub is not the product we added right so now that's our our hypothesis and
it now matches so now if we change now we should get eight and we do yeah so that's a that's the that's a question for
um what is the proper behavior for asking the the pricing system for product it doesn't know about maybe it should throw
an exception um hey dean uh sorry i missed your chat message earlier you looked up to different code and test coverage
the difference is the code coverage is lines of code covered but covered by what that's the thing who's when are you
measuring this is a discussion we had yesterday uh when are you measuring lines of code covered covered by what when
when you're running the application normally when you're trying it out manually i mean that's so then that's test
coverage right we're always checking lines of code covered um so test coverage is features covered by tess i don't know
that that's a common common enough term so is it features versus lines of code i don't find that to be a common a common
understanding of the differences i i think they're equivalent but i call it test coverage because it's initiated by
tests and it's focused on code executed by tests i don't even think coverage is a great term either because you could
execute a lot of code that is not actually asserted uh i think i'm gonna make the stub through an exception this may
break some tests i'm going to create a domain exception because i think actually this should be part of the contract
because i could call out to an external service and may say hey i have no idea what what price this is um i don't give
products away for free just um let's create a class this port or application uh it's specific to this port i'm going to
leave it in the port but it is code so i'll do that i'm going to bail out of this does not extend throwable i wanted to
extend runtime and then i wanted to override these two actually product and let's change this to upc all right great
yeah i mean if i'm tdding i generally don't care almost at all about code coverage except when i'm doing certain
refections and this is how we got into it yesterday which i thought and swiggy mentioned this and i think it's a really
good technique is if you refactor by creating a new class you've now made public likely methods that were not public
before and so how do you know that those are that now all this code in this new class is tested properly because you
test drove it in indirectly and now you have direct access to to its api um and how do you know that that now it's it's
well covered uh so we saw yesterday actually there was some stuff missing so we used the the test code coverage to to
illuminate that for us yeah but yeah that's what i love about tdd is by definition uh if you were taking small steps so
i've seen it um and i've done this myself where if you take too large of a step of implementing behavior when a test was
failing you may not have covered that new behavior sufficiently in terms of checking all of its decision points all
right let's run our tests actually and let's make sure that it throws the exception okay so only one failed for the
right reason and by the way this is uh something that uh i was recently skimming through uh growing object-oriented
software guided by tests or the goose book um and this is something that they talk about uh improving the diagnostics
for for failing tests and so that's what we did with uh all right so now it should fail because it should be 8 and not
7.2 uh because there is no great now it fails is appropriate um no i'll do a commit well let's do a commit um okay
because it could could be it could have been a year uh step throws exception when product not found this should be part
of the reports of a price all right it's funny how numbers stick with us like if you'd asked me phone numbers from 40
years ago i would not remember them yeah because basically it was it was my username so i remember it all right um test
is failing as expected now we can let's close our stub is we want something that gives us a discount roll there we've
implemented it i don't i know i had one i don't remember it all right so i tried the simplest thing that i thought might
work which was well let me just add 10 off every time a product is added so the current test passed so i know it works
in this case but then i've broken four other tests so now i need to need a way to to fetch it um so let's go and uh what
i want is i want a method that takes a upc and returns a i might have some dependency issues but i'll figure that out oh
sid meinki thank you for subscribing with private gaming i really appreciate that thanks well the upc is just a string
so um so the architecture of this system is there's a product scanner and what it right actually that's we did a little
research yesterday on how self-checkout machines work and that's what they do right they scan they get more information
the price they get the weight they get categories they get a whole bunch of information but all that's really scanned
there's some other codes that i can recognize as well but it uses that uh so that means we um have to go out and and
fetch the discount we're currently fetching the price so that's cool uh but we need to now fetch fetch the discount
replace this constant because this with we're going to extract this to a method and then move it discount what was the
one we had the discount roll let's go our special deals so our 10 percent discounted upc was this and now let's replace
both of these with um so i've mainly just extracted this to method i'm not looking at the upc uh but now i could uh so i
should still have for the four tests failing and so now if uh upc equals 39.7 otherwise we return uh none and and it
does all right so we've hard-coded it in the cart service that's not good enough we know i mean if this was the only
product that ever got 10 off then that would be great but we know that we don't want that so now we can do is we can
extract this method to another class and extract from that an interface i could have define the port upfront right the
interface discount rule 4 that takes a upc written a stub for it plug that in um but my tendency is to take is to write
little bits of code and then then refactor them to where they need to go so in some sense it's a bit harder because on
the fly i'm doing design um but i know what what the design looks like because i do have this in mind and so i do know i
need an external fetcher but instead of in a sense doing top what some people call top down or outside in um right you i
think it's really top down like here are all the classes and all the interfaces and then i'll write the details i'm
really basically taking code that that works and and pushing it around yeah extract delegate i'm already thinking ahead
because uh intellij is notorious for doing this refactoring not quite right uh let's see let's see what it does uh so we
want this discount rule um what's nice is that we can look at this method and we can see the only dependencies it has uh
is on the parameter which is great uh or on discount rule itself which already is setting off little alarms about
dependency direction but in hexagon architecture because discount rule um but i guess discount fetcher can have that the
actual dependency uh that stick um maybe forever even forever all right so the name for this new class is going to be
our um disc uh what i call it discount fetcher discount fetcher but a specific one this is our stub discount fetcher
which ironically is going to go into the um i probably shouldn't do that just yet let's leave it in the same source root
so this is the method we're pulling out see what did you do intellij so notice that it refactored this code um but it
then still left this method here like intellij has a bad habit of not cleaning up after itself um it happens in this
refactoring and it happens in the move instance method refactoring because up here it's now doing stub discount fetcher
right there um where that gets instantiated that's up here and what's nice about this is we'll be able to push it out
through the constructor one of my favorite refactoring all right so let's get rid of this um this should not have
changed anything from a behavior standpoint so our test should still pass and they do um subtracted discount we'll look
up to uh please stop that sure okay uh so those of you who want to be following along at home just a reminder you can
always do bang project and you can always chat about the stuff on discord um by the way i publish a newsletter around
once a week where i have articles uh either about test driven development or a lot of upcoming ones about hexagonal
architecture and i do have uh my hexagonal architecture course coming up um launching it next week so i'm getting ready
for that uh it is not complete yet you'll be receiving um the first uh the first few videos and then videos over the
next few months not quite 40 times but close enough so you can get information by signing up for my newsletter there all
right now back to our show um so now that this works and i've extracted the stub discount fetcher let's go uh we want an
actual interface so right so this is an actual port interface we want this to be a port interface um we don't need that
constructor at this point but we want to extract an interface let's do that so extract interface we want to rename this
class to be stub no we want to keep this we want to extract the interface i'm usually doing the other one but this one
we want discount fetcher uh that's the package for the interface leave in same sourcefruit that's fine that's our method
um no not and that um i actually do want rename original but this all right i'll just do it this way um oh now i can
analyze usages and replace them with discount fetcher yes please do um could this dialog be any smaller so yes we want
that field to be discount fetcher do it wonderful what did you do we've got our interface oh because this is in a
different package why did you not import this uh well let's move this to the correct package because it really should be
an import um i'm not going to move it also to the test because i want to do one thing at a time okay but now i want to
move this to the test route because this is for tests right because it did not replace now i'll let the compiler tell me
where yeah so it shouldn't be this it should be discount fetcher um oh that's interesting yeah all right let's back up
all right and this is why we do commence now i knew was complaining about it i thought it was complaining about just the
declaration part which would have been valid um but it was also complaining about this uh okay so let's make sure all
our tests pass all right uh let's do this again so um delete this uh do i want to push this out yet so move the
initializer to the constructor uh do i want to have an alternate constructor no i'll push it out to everybody so now
that i have it here now i'll go ahead uh and introduce parameter thank you for that awful name intellij uh discount
fetcher um now uh this will get renamed later i'll put this dot in front of it just for future protection um so let's do
a commit uh where we pushed out my intro boost parameter parameter okay now i can go in my stub discount thing um
actually let's rename it wait that's probably what i should have done before now let's extract interface rename the
original to stub extract the interface uh oh this is in the wrong package hold on really oh that's probably why it did
that um yeah i think when i extract when i extracted delegate i should have put it directly import that's what i missed
all right so now i can introduce let's rename that so i'm hitting option e which should be but uh it appears to be
broken all right we're renaming stub discount fetcher uh even same source root this is the method refactor this looks
good and this is and we can check that we're still abiding by hexagon architecture because the imports that we should
see here are either um in either a port or domain and that's what we're seeing so that's all good uh let's run our test
it shouldn't have changed anything because in our tests uh we are instantiating the stub discount fetcher extracted port
interface for java 1994 caffeinate oh yeah you know i that reminds me i need to go buy more coffee go buy more coffee
okay um all right we extracted our port so again notice that the way i did this was i didn't create the port first and
then create a stub implementation and then inject it into cart service i actually started with working code in cart
service pulled it out into a stub one extracted the interface and now i need to move the stub into the that just still
work all right um now uh yes so now if we look at this test uh this test is is problematic because um why uh let me pull
this out to a variable there's nothing looking at this test we could look at 10 discounted upc uh but that's a bit
misleading because which is redundant like saying atm machine uh that's just the number that even though we call it that
this constant has there's no information in this constant that tells us anything about that um and in fact i'm going to
inline it because that's actually a little confusing uh let's inline on the method who else is referencing it just there
all right now it's crystal clear that if we look at this test there's no rational out there's no nothing in this test
that tells us why we would expect 7.2 and what i want for my tests is it should be clear what as part of the given or
the when makes this then obvious so this hidden information right this is actually hidden specifically this is hidden so
what we need to do is unhide that information so let's do that um we've already got upc uh so let's do this so let's um
discounted upc and we'll initialize that in the constructor and also initialize that in the constructor i can push this
out as a parameter uh let's something in intellij changed recently where it's now just really trying to make them
different by adding one and i don't know how to fix that because that's really annoying because there's no reason why i
can't call it this because i just disambiguated it with this dot and so i've pushed out what was hidden here pushed it
into the fields and then used that to then push it out into and introduce parameters uh this is a maneuver that i do
frequently we saw it a bit with the fetcher and this is the same thing um i don't have a great name so i have a name a
nice name for cohere method which is the series of automated refactorings to move behavior where it belongs i don't have
a good name for this uh for this refactoring this composite refactoring but i generally call it push out but it's not
specific enough but anyway what we end up with is now this information here it's very clear that this 10 off is
associated with this and then people can reading this test can associate these three things together and now all the
information you need to understand why we got here is up here and that that's our goal so now that we've done that uh no
i did not want to do that um so everything should still pass those were just reflecting expose hidden collaborator in
this case it's not quite a collaborator but i do like expose hidden maybe we could see that as a collaborator i tend to
think of collaborators more sophisticated but maybe that's collaborator that's that's that's that's actually not a bad
name by that i mean it's better than anything i do end up using it i'll credit you um if anybody comes up with a better
name or alternate ideas uh feel free to to suggest all right so all our tests can still still pass so um exposed hidden
information uh i pushed out basically the the association of the 987 with with the 10 off uh and i pushed it out through
the the fetcher and why are you not paying full attention am i not the most important thing in your life right now come
on man intro ram hey there tricky too so this is one of the reasons why um uh i sometimes like you know sort of
switching gears and writing new new applications even though this one is not anything useful to me it's it's fairly
realistic um and it gives me a chance to one of the things as an educator because that's what mainly i am um an educator
either serving as a technical coach or doing training uh the more different examples i have to show here's how you do
expose hidden and so this this technique of taking the literals or other constant information and basically getting it
so that i can push it out through the constructor i i do that just frequently enough that it's that it's a good skill
and now i can and now once you know it's one of those things that if you practice you can then see opportunities to do
it and then you just do it and it's much easier to do it than than other ways uh than perhaps other ways and so it's one
of those you learn the skills and then you see places where you can apply it and so my job as an educator is to find a
bunch of different scenarios that i can say hey here's the scenario we'd like to be able to do this or we don't see this
here's the steps you do it um this might be the next one that i write up it's either this one uh yeah it's this one
because i now have two examples of pushing through the constructor hey tram stores have a have a good sleep and thanks
for stopping by uh okay so all our tests pass we've pushed out the information hello sen senja sin i'm sorry that the d
followed by an h is hard to hard to pronounce hydrate thank you i was oh that was not what i expected you ever do that
you ever like you have a drink and it's like oh i thought it was gonna be something else and it tastes weird because
like that's not what i expected uh what am i creating i am basically doing an exercise of supermarket uh checkout pricer
um you can check out the repo it has a readme that describes what this is uh and i'm attacking it from a test-driven
development point of view as well as uh hexagonal architecture so this is the hexagonal architecture of uh of this
application you scan products uh it keeps track of them in a shopping cart so they're products you can get a receipt and
now i'm working on on discount rules which requires us to talk to an external service that doesn't yet exist but it will
exist but we're basically writing the code in here to do that all through test drive development so we just refactored
our way oops wrong way to having this implementation test implementation of um great so we now have the ability to
specify at least for the disk for the stub fetcher a single product represented by its upc with a single discount rule
and that gets applied um here let's externalize let's extract that um so one of the downsides of pushing things out
through the stub is we ended up with all of our stub discount fetchers uh having this this same rule and i think we can
replace most of them with just an empty uh an empty one so let's do that so here um we just need um i kind of wanted
actually a different fetcher dummy that mean it's not really a dummy because it's going to look up the product and find
none um maybe i'll just create a constructor that doesn't take any parameters so let's do that so let's delete this
create the constructor we're not going to change the signature we're going to create another one uh and so from to me
fake uh implies something different so i use um george masaros's uh terminology so fake would imply that the test code
the code that i'm testing uh is reading and writing to something when it has the word fake in front of it in this case
it's not it's not quite a dummy because it is actually used as part of the test code so it's just an it could be the uh
no discount the the no discount fetcher uh i don't know that i need to necessarily uh sorry what's private project my
github repo private no it's public what i'm not sure what um all right so we've done that here so actually now we it
does look like a dummy um but a dummy would be something that would that i'd actually like throw an exception here and
highway law uh to show that it's not used as part of the calculations or part of the execution of the code but actually
is used it is technically the node discount fetcher and that's what i was saying before i could create a separate class
um but the definition of a stub is to return a value not it doesn't always have to be related to its input methods i
could just and that's what i had before i could i always return discount 10 i was thinking static factory method for the
stub yeah um let's do that uh but in order to do that uh i'm gonna basically uh what do i want to replace um so oh that'
s interesting because this is on a different line it didn't come up all uh and yes of course wheat law suggests i could
create an abstract factory or two implementations hey and my hood um why the find that's weird uh all right let's make
sure i didn't break anything especially with re search replace that's always the possibility uh so now i can basically
take this which is used in these places um i thought there was an introduce place in here for safe i thought there was
an automated enterprise checkout for exterior yes um uh all right so let's create um let's create a factory method
factory all right i have to look that up because i thought there was a way to yeah that's not gonna work okay yes that's
that's transfers that's that's where we're danger and why you still have tram stars um all right so let's create a
method uh we'll call it um public static uh no discounts yeah if i don't stop talk and this has to return a discount
fetcher uh so return new stub discount fetcher uh we can stop making this public we cannot make this private uh and
we've just broken a whole bunch of code that's fine um with uh stub discount fetcher oops no discounts uh i'll place
that with oops uh oh that's right anyway because this now okay uh let's push this down uh and uh that's not right
because that's i had all our test paths great um so now and done just in time i don't know why i keep wanting to write
hey there hyperessy am i familiar with i'm by no means an expert i still consider myself an amateur uh i get stuff done
but not always in the best way possible all right um this is a wonderful stopping point so on a future stream our
discount fetcher and our uh product price fetcher could i help you get alignments fixed i don't think so um plus i'm
ending the stream in in a in a minute i go to other people for that help um so now that that we've got uh at least stubs
of these things um we'll create two services uh the product price fetcher um i might be able to use a third-party
service um there's one that has an api it's a little bit annoying because it because it basically returns prices for a
bunch of different stores uh which is kind of what we really want here so i'm not sure but we'll basically deploy right
and well i think i'll just run from scratch we'll write and deploy from scratch to services i'll deploy them onto
railway um because that way they're always up and and doesn't cost much and then uh um probably should also work on on
on this inbound adapter so we can actually control it from something besides tests uh maybe we'll do that first so just
something really trivial that has a single input field um of the the upc uh receipt should work i probably won't give us
enough information so there might be some more information we want to get from there um and then we'll create these two
services this shouldn't take much because they'll be even though they'll be technically separate services will in a
sense hard code what they'll return um data depression at what point do i pause td and run my app to check my code is
integrating i will write integration tests so as i uh so next time when i basically want to plug in this product scanner
into the service i will write a test at this layer and so up here this would be an integration test and then i will run
my application manually just to make sure things work right now since i don't have any real adapters there's actually
nothing to integrate with right these um these guys are all uh stubs there's nothing real there i don't even have one of
these yet and i don't have one of these so there's nothing to integrate yet but once i do have this then i write
integration tests and then i will test it manually just to make sure but the integration tests give me the confidence i
need and so i define integration tests in a very i basically say that anything that crosses this line uh yes i will just
write more tests and run them and then the things that my test does not capture which is basically what the ui looks
like because i don't write tests for that then that's why i will run it manually um and then the manual is really a
manual end-to-end test as well because i don't find end-to-end tests being all that useful to automate um well it
depends but you know manually running stuff that's a test it's just not an automated test
