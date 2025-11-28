# Kid-Bank App Dev Ep 04： CSV Import Part 2 (Java + Spring + Cloud)

**Video URL:** https://www.youtube.com/watch?v=qbiCi9_3G00

---

## Transcript

hi there this is Ted I'm young also known as jitter Ted welcome to the series of recordings from my live coding series
around developing kid bank the money tracker for kids this is episode 4 where I finished the implementation of importing
transactions from the CSV comma separated file enjoy where we left before the break was we got deposits working and now
we need to handle importing interest credit so let's do that so it's basically going to be this test so import actually
let me rename this because we're already at a series CSV import test so let's just say single row CSV deposit this one
is it going to be a single row interest credit that you're still result in a single deposit we can take out multiple
rows and this is interest credit so let me just go I'll place this we have this we don't you get a new line so ok this
one's gonna be interesting I expect it to still process the number correctly but when it converts this dollar 0.08 it'll
come out with just 8 so this should just be eight dates February first so February first and then this is that string
okay so I expect this to fell let's see what happens well that's interesting oh because we weren't we were assuming it
was a deposit we weren't checking it at all anyway yeah so that works okay where it's gonna be fun is if we do this now
as a spent single row payment should result in single spend transaction so payment is if we look at this thing payment
is one of these that's what we're calling it from here but what it's going to be called in it's gonna actually be a
spend transaction and right so this interest credit should result in a deposit so it did now let's go and grab this okay
this is interesting so the way Excel did negative numbers is it surrounded by parentheses we actually so I want so okay
so a couple of options here one is we could totally ignore what this column says and just look at the whether this is a
positive or negative amount so in accounting they usually put parentheses around negative numbers I have no idea what
the source of that is but I know from my for my work with accounting stuff that instead of putting a negative minus sign
you basically put parentheses to indicate that it's a negative number so all these are deposits or because they're all
positive numbers this one's a payment because it's a negative number and this other payment is a negative number so that
says we could ignore this column but I'm not going to do that I'm gonna assume that that that means something okay so
let's go and grab this one this is going to be a spend one and it's January fourth one for this part is this part so
take that place that and it's 30 times on earth okay I expect this four to fail for two reasons one is we're not
actually currently stripping out parentheses so I expect it's going to try to do it as a deposit and it will throw an
exception basically a parse exception on the integer so let's see if my hypothesis is correct indeed yeah so number
format exception for that so let us go and fix that so when we when we do the replace we can put in parentheses that
might be enough let's run it okay Oh duh I need both sides okay so that parsed it correctly now really the only
difference is that we were getting a deposit but we expected a spend so now we since we've been ignoring transaction
type and now we need to pay attention to it there are a couple of interesting options one that's going through my head
is using a map to which is which is interesting right because sort of what's basically a switch statement right it's a
switch on transaction type you can always convert a switch into a map that has lambdas it's kind of weird because really
that's what a switch is which is probably more readable although it depends if you're gonna have a fixed set of things
and a switch is more readable if you're gonna have variations upon some configuration that a map might be useful so let'
s but what we want to do is we want to have a method that says basically transaction transaction equals create
transaction for well let's do this way so we want is basically a switch I could spell and we're gonna switch on the
transaction type what are you saying yes I know it hasn't antique transaction declaring over here and a case of if the
transaction type is cash deposit then we will do transaction equals this thing and otherwise defaults will throw an
exception it's basically good use an illegal argument exception that's always a good one to fall back on a known
transaction that's not reachable of course it's unreachable expedient do a break here okay so we haven't changed
anything so if we go back to our CSV import test and run all of the test methods in here they'll all pass except for the
one we're working on Oh interesting okay that makes sense and this one fails too because interest credit is not one of
the deposits so we can fix that one pretty quickly by adding another case we can say case interest credit so now that
should fix that test and then the spend one should still fail okay and so what we can do is a case payment and then this
transaction is transaction crate spend local date time amount description break and boom and extract into a horse
transaction great transaction in line that so now we have I'm still a little uncomfortable with this because I've so
there's sort of two levels of abstraction here we've got one where we're doing sort of hard pulling stuff out of of a
list and then we call the CSV cells into this create transaction from mmm and I think I'm ok push me and I wanted to
push this switch down so it's out of the way so when I'm reading this it's it's more readable right so basically parsing
these and then we create the transaction based on that stuff all right slow if we're all a these look the same whenever
there's an equals issue here so we've got an expected transaction with date action action amount and source to be
exactly Oh so this is 2019 this is 2018 oh man that was kind of annoying all right that means my test is is wrong this
should have been 2019 okay so now it should work I was worried that our equals method wasn't working okay cool so now we
can let's run all unit tests I still expect now that the one at the account level to fail but all the other ones pass
cool so let's go there so now we have the CSV importer working so let's go and commit that so CSV import or you know
imports the cash deposit well actually now also imports interest credit and payment transactions I'm not gonna check in
this file no I'll check okay and do that all right so now our account test we want to load transactions so now we want
to basically load a bunch of transactions into the account so this has nothing to do actually with with the CSV we've
now converted a CSV into a list of transactions and now all we need is that and so we'll have the controller deal
integration tests I don't think anything is broken they're way those took a while for some reason okay so those are all
so let's go back to our controller and actually let's go back to our controller tests so we want to create a new load
command that takes basically a bunch of lines of string lines of CSV and we'll use the CSV importer to convert those to
transactions and then add that to the account so what that will look like is transactions into account so this is going
to be an import command will create so I'll create a class and that's in the web adapter yes and so will new it up and
will hold it in a variable so what do we need in this this is basically gonna be just a list of string the question is
how does that come in that might come in as one long string I actually don't know actually don't know let's all right so
let's jump to the UI because I actually don't know what a text area how it sends multiple lines what that looks like
let's see that's a good way of checking so parse HTML input text area lines so as use a line separator so what does they
say about number of visible text lines it's the labels bunch of properties but I'm at the text yes what is look like 1 2
3 so just have multiple rows no all right I'm gonna fall back to the debugger for a lack of a better way to do some so
let's comment this out for a second and let's go and we'll create well actually put this to a separate page but let's
create a form that accepts it's going to accept what is this this is the import objects import command and it's action
is going to go to import and that's going to be a post and we're just gonna have label and paste CSV here and then this
is going to be a field on that object which is going not gonna have any default value there although I guess we could
have the diff well the default will come in if we put something in there but the type Oh so actually this is going to be
taxed so columns form max length name placeholder rows that's just for visibility so the question is what I use text
area or search text uh I guess I actually do want to text area okay so that's not I've never used to a text area I guess
with time leaf so should I just use the let's look at time leaf so time leaf okay so it is so basically that's
interesting there was later one guess I won't basically won't use the auto closing version of that so I'll just close it
okay let's restart the app oh I didn't create a post mapping for that so it's gonna be hard to do anything with that all
right let's stop this what we want to do is we want to figure out what is multiple lines of text look like so what we're
going to do is in our account controller we'll create a post mapping for import and import CS CSV import recipe and this
and what we're going to do here is actually we're going to just set a breakpoint and run it in debug and see what this
thing looks like so let's go to import command this is basically a private string content and it will put data on this
so Lombok stuff will get generated and we need to remember that we need to put a blank one of these in the model model
and attribute contents sorry what did we call that object called it import and import new import command okay so let's
run this under the all right and let's go over here well refresh the page so okay I guess I should make that a little
bit bigger that's fine so let me actually paste let's close that let me actually paste some actual CSV and see what it
looks like so I would be basically doing something like that all right I did not put in a submit button I keep
forgetting to do that darn it that's kind of hilarious button type equals submit and it says important I seem to be
using exclamation points as my brand here all right well quote recompile that all that does is make sure that I can
reload the page properly will paste that in whoops ace that why are you not oh yes that's right and import okay so in
our import command okay it looks like we've got that's kind of funny so the content is basically it's it is using a
return a newline return line feed kind of thing so basically windows style so it's one long strength now what will be
interesting is if I change all right so let's do this let's go to import command let's say this isn't a strain but
actually a list of string will and we'll have to recompile everything so build build project so the question is will
spring Auto convert that into a list of individual strings you know let's restart the debug session I don't know
sometimes that happens well okay let's just restart okay refresh the page okay okay so import command content is that a
realist well okay that's interesting that's not at all what I would have expected it to do it decided it was gonna
parcel Ong comas instead of new lines why would you do that that I that I I don't know okay well so clearly that's not
going to work so what we want to do is we'll want to have a way of grabbing from the import command turning it into
multiple lines and that's pretty straightforward that's I'm sure guava has we can use the the raw splitter oh so
actually a question this is yeah well those will get bills like it turned out okay well that's not what we want it so
let's go Lily's name we know let's do this let's turn off the debug their breakpoint really should also make that bigger
so that's rows curious how wide this is what's the widest here that's 60 so don't put 80 okay all right so what that
means is our import command clearly list of string does not do what we want so we're gonna have basically string its
content and so now we're what we'd like is a method on on import command that will easily convert that string and parse
it along along your lines so we can say so public list of string as lines and then we basically will do a splitter on
what one is we actually want on a character match or care Matt you're not whitespace is there it's not white space so
let's do this let's let's say guava split string new so again I could use a split that gives okay so it looks like
pattern compiled this guy right so and so cool I can just do that we learned through examples in case you didn't know
that we learned through examples and so we will use this example should probably pull this out into a constant new line
separator pattern because no point in compiling it every single time so we'll do that and then we can say split two
lists oh we should probably omit any empty lines and because that'll take care if there's a sort of empty new line at
the end and then we'll basically split the list on content and basically means the account controller what will
basically be doing here do we have that I was was every day a test for this yes here it is okay let's actually rate that
test now now that we know what import command needs to have so import command set the content what we want is to go here
we'll grab these three lines because what's nice is these are the three different kinds of transactions we're going to
have and let's see so what I'm going to do is I'm gonna carry your turn line fee let's actually use the ones that we saw
from the browser oops okay so this is three transactions I don't know why you're not lighting it oh is this a plus right
so this is basically one big string these are not so basically these are the new lines that would come in from the
browser and now we want the account controller which we I guess we need to create so actually need to create an account
with an account controller or talking to that guy and now count controller we want to import a CSV with the import
command we expect that to put the transactions into the account so we expect that our accounts the transactions we
expect there to have size of three we could be more precise and describe exactly what the transactions are let's just
let's get this to see if we can get this to work first I expect this to fail because I don't think we've done anything
other than grab the import command and return a redirect so yeah so that didn't do anything so let's go ahead now and go
to our import CSV we get our import command now here's where we need to use a new CSV importer in a I'm going to make
this an injectable service because this is basically a service thing so on this we're going to import from import
command as lines and then we're gonna say that as transactions and then account oh we forgot to load the transactions in
bulk into the account I think I had was working on that in the account test right so that's the last missing piece so we
need this I know we've been saying that it's a set but really it's a list account will create a couple of transactions
so those will be the transactions to load and that will be lists as lists and so will create a transaction will create a
deposit to take time of May 20 2015 5 9 0 0 what comes next year comes next is the amounts so 78 2 3 and source or I'll
just say transaction 1 is the description so that's one of them this is really annoying let's do that so this okay so
now it's nicely formatted transaction we can still have another one transaction create a spend local tea time of of 2015
five nine zero zero and we're gonna spend play 595 on why did I mess up here great deposit returns a transaction there's
a list of transactions is it unclear oh this is guava okay that's why all right so let's do this call this new ArrayList
transaction and I will just do transactions to low add yeah that's probably another syntactically shorter way to do this
but I'm at that point where my brain is not working as well and a partner or a pair would be really good right about now
so let me port the static method that so we have the transactions to load we expect that when we do load it we exact we
get the transaction so we'll do this kind of test load transactions to load create this method and it doesn't return
anything that's cool takes a list of transactions transactions to load we will do nothing we will run this test we
expect it to fail and good this test fails because the transactions is are empty so all we need to do is so here we had
add new transaction added a single one we want to do basically something like that so it's at all the existing
transactions and then actually add all the transactions to load so this will combine the ones that we already have plus
this bulk load of transactions and then reassign it back to to the internal variable so now if we go back to our test
and we run it should pass unless R equal to is wrong yeah so we can't do any equals because this transactions returns an
immutable set whereas this transaction is to load an ArrayList so what we can actually just in any order but it's our
net it's expecting it's expecting this to be a variable number of arguments there another method we can use here let's
see compare using comparator contains let's make you bigger so we want as we want one that oh contains all right because
that's an iterable contains exactly elements of exactly in any think we want this exactly in any order of right because
it's a new account so that's what we want and then we can do transactions to load okay so let's run the test now awesome
it passed okay so now we have a way to bulk load transactions into our account and in our controller we can now use that
method we can say account load load these transactions and then redirect and so now in our account controller test we
can now run this one and so it has size of three we could do a bit more work to actually create these in turn these
individually into transactions to verify our our inputs so let's go ahead and do that so we can say contains exactly in
any order oops so we're gonna have three transactions so we've got transaction will create a deposit this deposit is a
local date time of is the first one which is March 7th 2018 at midnight and what else the amount is 5:50 so that's five
five zero and the this one's a payment so it's called a spend little take time so this one is March 25th 2018 oops I'm
18 March 5th March 25th and it's 1,200 because we convert that to a positive amount and unlike I be able to spell this
correctly because game castle is spelled funny because that's the name of a store where my son plays Magic the Gathering
and then this last one is an interest credit which is a deposit of local date time of 2018 April 1st no it is not April
Fool's except the interest amount certainly is would seem that it's April Fool's copy this and this and ok so now we
were gonna say that these are gonna convert to these and we'll run this test awesome alright so I think we're just about
done let me run all that all the tests and then we can actually try it out from from the UI and see what happens and
then we will call it a day I didn't get to do the I don't think I'd to do the persistence and nor did I although we can
do sort of fake persistence all right everything passes let me commit all tests pass with controller handling lines of
CSV to import and so we will come at that so - oops like - here let me load the page would help if we actually ran the
application we load and there's our PA the CSV yes clearly we're going to need to put this on a separate page and make
the rest of the page nicer let's go and now paste the stuff in lips grab bunch of these and boom look at that so it's in
reverse chronological order we've got a bunch of transactions the spend amount is $12 I'm assuming this adds up 69-66
yep okay so the math is good the sources are good the actions are correct and it load them all up with no errors I think
we're done if any of you are watching this and have any feedback or comments or anything I'd love to hear from you so
this was broadcast on on twitch so twitch.tv slash jitter Ted you can also visit my my web page which is Ted em
