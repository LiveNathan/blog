# Kid-Bank App Dev Ep 02 (Java + Spring + Cloud)： The Refactorings

**Video URL:** https://www.youtube.com/watch?v=jiWU5YuP74c

---

## Transcript

hi there this is Ted I'm young also known as jitter Ted welcome to the kid Bank app development the money tracker for
kids this is episode 2 the refactoring where I refactor classes into the hexagonal architecture and then refactor the
current accounts balance tracking to use Java streams and sum over the transactions enjoy last time so last time we
completed Li spend money story the app is still up and running and oh I guess I didn't stop it so it still has the
transactions from last so on today's agenda is some minimal response of styling work I keep pushing it off because I am
barely capable of doing front-end stuff but I'm gonna push that down a bit because really what I want to get to is
importing a CSV to pre populate the account where that comes from so this is currently my layout for keeping track of
Asher's money and so I want to be able to do is basically take these transactions and load them up into get bank so I
don't have to retype it so let's hide that for now so that's what we're going to do is we're going to basically import
the CSV to pre populate the account check where we are here so all you're gonna tests so for some oh I know why so what
happens is in IntelliJ if you don't if you make some of the changes here but you don't know if you can see it but
basically these icons are grayed out if you don't save them basically it uses at least recently used and then it gets
rid of them so I had to find three kinds of tests running one is for all unit tests right those will run in less than a
second so I save that then I had one that is basically all of all the tests no matter whether they're in the unit test
directory or the integration test directory so I've got two places where I keep the integration tests one is under
integration tasks which is a fairly standard place to put integration tests those that are gonna run everything and take
a little longer and then further down here close this further down here these are the unit tests so I have a
configuration to run all unit tests but I want a configuration to run all the tests of this spacely all tests and we'll
save that and then I want to have one that's so I might just let's see so if I run I run these I think it's going to run
all of just the integration test which is what I want so this one is running the integration test these are all
integration tests and we'll save that that's saved then we want one that is so I'm just gonna so that's all unit tests
all integration tests and then I basically want to run all tests surrounding this is gonna run all unit tests so maybe
I'll just manually make a configuration duplicate this one this is gonna be all tests and this is going to be all in
package and so that will basically make it no matter where it is in you doesn't matter what directory it's in we'll just
say the whole project we don't have modules that's fine and so that way we have three different pre predefined ways to
run tests on to Gration test i'll you call all tests and then all unit tests let me just check the application this one
needs to be saved because that's what will run these unknown ones I'll just delete okay all right so now we're all set
up nothing to commit let's run all the tests just to be sure and there we go all all tests pass great okay so our story
as I mentioned is we're gonna import a CSV to pre populate an account so you know what before I do that I wanted to do
some refactoring so let's do that so right now I've got basically all of these all these classes they're just in the kid
bank package but let's start splitting them splitting them up according to the basic architecture that I'm using so for
those of you who aren't familiar with that I have my ports and adapters hexagonal architecture diagram and so the idea
if you're not familiar with this architecture is that you have a central core which is your application and holds your
domain model your business logic all the stuff that's specific to the logic of and of the application but then any
communication with the outside world whether it's sort of incoming through web app or some phone app or maybe some other
machine that's all in these adapters and there are two different kinds of adapters there would have called the primary
or driven adapters these are ones that are initiated by some incoming requests so like a web page or a phone that would
be an incoming request then there are what are called to react what I call reacting or secondary adapters and these are
things that are driven by the application so for example the application if it wants to persist something when we get to
that we're gonna use a persistent storage adapter if we wanted to do some external notification which is on the list you
know to send out an SMS or some other notification that is driven by the application so the driven ones are the primary
ones I'm not terribly happy with this naming convention I've as I've talked about it I I've been searching for good
terms but as we know naming is hard so these are the ones these blue ones are the ones that are incoming the sort of
yellow ones are the ones that the application itself pushes out so typically the direction is something in the
application causes it to talk to one of these like maybe the payment adapter okay so what I want to do is I want to move
these now to the correct part of the architecture so anything in the domain I'm going to move to the domain package so
that goes into the domain package their transaction is also in domain and account controller is in an adapter
specifically a web adapter so my naming convention that I've used is I'll have domain and everything in the domain in
there then I'll have an adapter sub package and then sub packages from there to be used for each individual adapter and
sometimes you'll have shared things across adapters like the formatting or the command stuff is things that might be
sure to cross adapters and those will will be up and sort of the generic adapter package that's not something about
their transaction view is also adapter web this is the entry point into the application that's something I don't need oh
wait yes so I'll have to come back to that transaction command is also adapter web let's see what else and date
formatting and scale decimals those are also adapter right now they're only used by web but we might share them later
and so what I also want to do is move the tests to associate with a correct package and you can tell basically here I'm
importing from domain so that means this should go to domain and I can just say domain here fix that balance that's
working on domain deposit and these are accessing the web adapter because these have to do with how the transactions are
viewed so these go into the adapter web and oh crap I think I hit a lot key here so these got moved out of the tests
yeah and must take a lot so all right so this and this are actually in here so they need to go into adapter web but they
need to actually be in test so let's do that you can always tell and all that messed up and I gotta read it reset ik
import this or I can actually just that and do you roll back there and I'm go back there and optimize my imports okay so
let's try that again so bees also go into adaptor web and it's now I'm going to check the target destination directory
for those of you who are not colorblind this is a slight green shade that tells me that that's tests account transaction
tests is not in the right place and then these balance deposit and other tests directory okay so I'm gonna go clean up
because sometimes the imports as you moving stuff around get messed up alright and I'll run all the tests again and
while it's doing that I'm going to and we import that because the imports got messed up again I should have built this
before I committed so let me run the tests again I'm actually just gonna wait till the tests run before I commit just to
be sure and I'm basically gonna amend that commit all right so commit that all tests pass great so that was a dev task
hogs and cool all right so now we if we look here we see that stuff is nicely organized into packages so our domain is
pretty small right we've got an account and accounts as a bunch of transactions our web is dealing with producing the
webpage and interacting with it so all the controller formatting for for human consumption and the transaction command
that come in from the posts those are all in our web adapter and so you should always be able to tell if you've got your
stuff in the right place as I should be able to completely delete anything in any of these adapters and not only should
the core domain still work mainly all the it's test should work but any of the other adapters that I have should if I
have them should remain working so there's no dependencies between adapters and as you can see with the era's all the
dependencies are in words so adapters can depend on the domain but the domains should not depend on the adapter so so if
you look close close up at that this is what it looks like the dependencies always go inwards so your component your
domain logic is in the center and things always depend word these are these lies are full of talk I gave at Silicon
Valley code camp this past October the slides are up on my website at Ted I'm young calm so it was all about ports and
adapters all right so we want to pull in the CSV spreadsheet for pre-loading the transactions so what that basically
means is that we want to create an account and then basically do a bunch of deposits or spends depending on what the
transaction is so that might be a little inefficient so it might be nice if there was a way to directly instantiate we
currently have transactions as an immutable set and then what happens every time we add a new transaction we basically
copy over the old set and then tack on the new one and so for you know sort of one at a time that's okay but for sort of
bulk loading it would be nice to completely replace the list of transactions this might get tricky later when we try to
hook it up with with some persistence but for now let's see where this goes one thing I'm thinking about is we currently
there was another refactoring you know what I want to get the refactorings out of the way so there's an a refactoring
that I wanted to do which is right now balances is kept separate and so there's sort of duplicate work going on we're
basically every time we do a deposit we're adding through the balance and every time we do is spend we're subtracting
from the balance but that's really redundant because we have the transactions and so we can run through them so it's
sort of like a journal right so we can run through them and get this now so what would be interesting and sort of the
direction I wanted to go anyway is to not store valence separately is to have the balance always rely on that on
basically summing up the transactions because it's not like it's gonna take all that much longer sure you know even if I
have a hundred transactions but come on the transmitting the information over the webpage is what's going to take the
time not not the running through the transactions so one thing we can do is we can basically change this so we do
transactions and we do a stream and that we do so the stream is going to give us a bunch of the stream is going to give
us basically a bunch of transaction objects and so on each transaction object we what we want to do is we want to pull
out the amount so this is interesting so we want to pull out the amount but the amount isn't enough because we need to
know what type of transaction it is in order to know whether we're gonna subtract that amount or add that amount because
the amount is always a positive amount but obviously a spend needs to lower the balance versus deposit which needs to
increase it because we could just do map to two ants so that'll basically so we can say a transaction and then amount so
what this will do is will now give us it'll extract it'll go through each transaction and extend basically pull out
extract the amount and so the amount is an int right that's an incorrect yes and so then what we can do is we can do
some and so now we have basically summed over all of the transactions basically pulling out the amount and then summing
we might not have good test coverage for this so let's undo this for a second and let's go into our deposit test so we
have a deposit test that has two transactions so that's good so that will we'll make sure that we are not just returning
like the last transaction or something like that let's look at the spend test so we want to write another test for this
where spend money twice should reduce account balance by sum of all spent okay so the same thing we can do a count and
we'll do one up and we'll put that in a variable and then we'll say account spend actually going to just copy this so
shames that date a little bit change I'll change the date a little bit more and I'll put in a different amount make this
three $100 even so now I can assert that the account balance is equal to and so this should be since we're spending
money twice it should be basically negative thirty seven ninety five and we run all unit tests this one should pass
because and of course I can't add that's why that failed usually I do that on purpose like I'll make the test fail even
though I might have the functionality and this is where I guess I kind of differ from other PDD folks that know the test
must fail but that's a discussion for another day okay now what I'd like is it is sort of one test that does a mixture
of both so here on mixing deposit and spend should result in correct balance I go back and forth with naming some of
these things like sometimes I'll use very concrete amounts like mixing deposit of ten dollars and spend of fifteen
dollars should result in twenty five dollar balance so sort of depends on how I'm feeling but I'm gonna be specific here
so we're going to say deposit seventeen and spend let's say nine she'd result in 17 minus 9 is eight and eight balance
of eight so copy over copy I can't creation so we're gonna spend we said nine which is nine hundred call that cards do a
deposit and I'll change this date again and this is bottle deposit because my son likes to drop off the bottles to get
his money because we go to the local recycler and let's say that's about it somewhere in May on May 1st of that year
okay so let me assert that account balance is equal to I know I said eight but let's make this test fail and that's
right as a scaled integer so it actually needs to be it here eight hundred so so now if they all work okay so we've got
a bunch and so now let me go to count okay so we were we now have tests that that I that I feel like cover cover it so
now we're changing the implementation so this is changing internal behavior but as external behavior it shouldn't change
so this is sort of a true refactoring we've encapsulated how we count calculating balance and nobody else outside should
care how we did that so we'll go to transactions stream and then we'll map to int and we're going to do that by doing
transaction amount and then we're gonna sum that up and I expect stuff to fail because as I mentioned before we're not
looking at whether these transactions or deposits or withdrawals so let's see which tests fail all right so this spend
command should reduce a mountain account that's right because we were ignoring the sign so that's an expected way to
fail that's also expected because instead of subtracting we added and the spend test also here so good so they failed so
now the question is this is not good enough in the sense that we don't want just sort of the magnitude of the amount we
actually want there are a couple of things we can do we could we could provide method that provides on the transaction
the sort of signed amount that might be interesting and that way we encapsulate how it figures out whether it's a
negative or positive in there so let's do that so let's let's go into transaction so transaction is one thing you'll
notice is that even though I'm using Lombok to generate the equals and hashcode and a nice to string I don't have
setters and getters for things like date action amount and source because this is this is not a Java Bean this is not
like a data transfer object this is a POJO this is a plain old Java object that has behavior in it and so what I'd like
is to have a method here that gives us a signed amount or a transaction amount not sure what name will come up with so
let's go to transaction tests and that might help us come up with the name so this is testing at the account level so
let's go and create a transaction tests create a new tests transaction tests and we're not going to set up anything yes
that goes into that directory cool so our first test that we're trying to expose is that a spend so if we create a new
transaction and technically I could probably do know for for a bunch of these since I don't really care it's like a so I
could just put in now because it really doesn't matter the action so this is the important part this is a little bit
dangerous because I'm using a string here for the action which is either deposit or spend so I'm gonna do spend here and
it's the amount I'm going to do source I think it's fine and it's do var just to hold that in a variable so now I the
transaction amount should be 1375 that's straightforward but I want to have the scaled amount or the when I say the
transaction transaction amount seems redundant signed him out try that side amount and that should be is equal to
negative one 375 so I don't really need this because I know that amount works so sign them out I think is the name of
the method I'll use I don't know why it assumed it was a boolean it's an int and we'll return zero because we're gonna
return and would help if I spelled it is equal to correctly okay so this test should fail we'll just run this test by
itself and of course it does so now the spen thing is kind of tricky there are a couple of ways to go here one is we
look at account we'll see that it's also using the string here but that's internal to account but feels like this thing
should be controlled by like who cares about whether it's deposit so one thing is it's useful we're displaying but the
other is is now it's going to be used to figure out is this a positive amount or a negative amount so it seems like that
should go into transaction so I think what we want to do is instead of explicitly calling out that this is called spend
is not leave that up to the caller but create create a spend transaction and so that means whatever the string is that's
encapsulated inside of transaction and we don't care about it and this might be a time when we when we think about
moving to an enum but let's let's hold off on that so we'll create a method that returns a transaction this is the
amount and that's the source and so we're going to do is we're going to return a new and then the rest of the stuff is
just copied this is just about the point where we want to convert this to an enum but let's actually start by moving
this into a constant and let's see how that name works out let's let's make that private because we don't care about
anybody else having access to it so let's go back to here okay so this should still fail for the same reason all we've
done is made it easier to create the transaction and that's cool okay so now we can go here and we can say well say if
action equals spend return - amount else return amount and of course we could simplify this to basically a ternary
operator and there's other things we could do so right now this could be made a bit easier to read by replacement with
is you know basically is this a spend it's so straightforward and it's only used inside here that I'm willing to leave
it my tendency is to always remove expressions into their own named thing but this is so borderline that I'm gonna I'm
gonna leave it okay so now actually our test should pass and it does so now if we run all the unit tests so they're not
passing yet that's okay because we expected that because we while we've modified and created the signed amount it's
actually not used anywhere so now let's go back to account where it calculates the balance we don't want amount anymore
we want signed amount and so now if we run the tests I think they should all pass and they do all right so now we've
basically eliminated the use of balance and you can see it's it's used but it's never actually accessed so we can go
ahead and and get rid of it and so now if we look at and just to be sure I'll run all the tests again and yes they pass
so now what's interesting is add new transaction is we're not quite at the point so we created a creation method a
factory method like thing on transaction where we could create a spend transaction because right here we shouldn't
really be doing that so what I think I want to do is another refactoring where I refactor out the creation of this
transaction and put it let's see what's the best way to do that I think the best way to do that actually is re inline
both of these so I'll do an inline all and remove the method so now we're back to here and so now I can pull out this
thing into transaction spend and now I can replace this with transaction create spend and I no longer need to pass this
in so my goal here in the refactoring that I'm doing right now is I want to get rid of these strings that that are that
define sort of the type of transaction I want to encapsulate that further even though it's nicely encapsulated inside of
account I want encapsulate it further because really it belongs to the transaction so now we've got create spend and so
that's nicely encapsulated and what I'd like to do is do something similar so for go to here I want to have another one
that's basically the same thing so first let's pull this out into a deposit and then we can do create we're not going to
need that I'll leave that in a second and so from here you can actually just say new transaction and I'm going to do it
this way so that I can do a refactoring and I can do is convert this to a constant and get rid of this because we don't
need it and so one other thing that you may not notice that I'm doing is I'm using a lot of even like just deleting a
parameter from the method signature I could have just hit glee key or you know selected it and hit delete but I'm as
much as possible leveraging IntelliJ is automatic refactoring because that means I don't have to fix up somewhere else
right because here when I delete the parameter if I just did you know let me just delete this text and treat it as text
then when I got here I'd have to go and delete it from here but because I actually did a refactoring of remove it that
way it updated all of the code everywhere it's used and just make sure everything is in good shape so now that I've
basically created these factory methods for creating types of transactions I can actually we extract us back into a
method and say add new your transaction and this is just going to be transaction so crap okay I wish i intelligent this
in the right place because that's where it really needs to go I could in line this yeah I think that's okay trying to
figure out which ones more readable no I'm gonna leave it okay and let's see so we have RiRi factored this and now
there's no mention there's no strings here if we go to transaction we see that we've and I'll just convert that to
private we have a couple of these strings could convert to enum but I think I've done enough refactoring now so let me
run all the unit tests and they all pass okay great so now I've got a count I've got everything back to where it was
transaction now has some creation methods for things and a count now you basically does a stream with a map to int to
basically sum over all of the signed amounts to give us our balance so let's run all the tests should take a few seconds
and then I can do a commit and they'll pass so this was a refactor to use stream and some for calculating balance sort
of on the fly from all transactions and removed balance variable and the balance is really you know I mean the balance
was actually sort of as a cash and so we could cash it but I mean come on that it's certainly overkill
