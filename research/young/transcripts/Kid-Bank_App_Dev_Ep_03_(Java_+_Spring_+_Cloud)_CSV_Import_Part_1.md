# Kid-Bank App Dev Ep 03 (Java + Spring + Cloud)： CSV Import Part 1

**Video URL:** https://www.youtube.com/watch?v=T6nAg55Kc88

---

## Transcript

hi there this is Ted I'm young also known as judo Ted welcome to the series of recordings from my live coding series
where I'm developing kid bank for money tracker for kids this is episode 3 where I implement importing transactions from
a CSV file that was exported from an Excel spreadsheet that spreadsheet is what I've been using to keep track of my son'
s savings and spending and is basically what I want to replace with this application enjoy what I have up on the screen
here is it's basically the CSV that I exported from the Excel spreadsheet I'm gonna just trim out some of this extra
stuff ok so you know what I'm gonna leave that in there because that would be good edge case so we have is comma
separated now something I just realized is that I have some transactions where I've added the interest but that's
something that I'm gonna want to calculate automatically I have a story for that for calculate interest credit so for
now I actually what I import I want to ignore those but we'll we'll worry about that later so here I have I'm going to
import the CSV as is and I'll have another story for import CSV ignoring interest credit transactions and this is going
to be dependent on calculating interest credit so pins count interests okay in general you don't want stories to have
dependencies but sometimes that happens that's okay so let's look at the structure of this we basically have fortunately
for better for worse and excel didn't put any quotes around it not sure if that was an option when I exported it but so
I have a couple of choices I could do sir just a dirt cheap simple comma separated splitting and that might be okay I
could also use some libraries but I think this is really straightforward enough that I don't want to bother bringing in
I don't want to bother bringing in a full library just to to parse what's based you know it was a pretty basic comma
separated file well it'd be interesting is actually implemented and then maybe later I can look at what it would look
like to to do that so so this is interesting so when we think about where this functionality of importing the the text
into the domain the comma separated conversion so basically from a list of comma separated transactions to the core
domain that's it that's another adapter and so what we're gonna do is we're gonna basically start test-driving an
adapter so the other question is is is where is that something that's actually loaded at startup time so am I gonna so
one option is I can when the application starts up I can load in this less list of transactions I'm the other option is
basically I paste it into the web UI now if I think about sort of if I were just doing this locally having a local file
might be fine but since I'm eventually gonna deploy this to cloud probably be nice to have some button somewhere that
says import transactions so I think that's going to be my assumption which means it's basically gonna fall under the web
adapter which is where that functionality is gonna go so that's where we'll put that code now that we figured out where
where that's going to go we want to be able to do is figure out how that's going to get loaded into account so let's
take a look at account and sometimes it's useful to just look at the structure of the class like what methods it has
because sometimes you can get to involve with how things are organized so basically we have as a methods for for balance
deposits bend and add new transaction actually add new transactions shouldn't be public this should be private and let's
just make sure that I haven't broken anything by doing that so while that's running we can look at this so we're able to
get the transactions I'm actually got turned off so it's nice and now we're looking at this we're not looking at
anything were basically look at the public API for account and all our test pass are we committed anything so that was
just me private alright so I want you to do a commit on that okay so let's turn off our structure and so so far we have
no way of sort of bulk loading transactions and so the question is is do we have a CSV importer that takes a list of
strings and returns a list of transaction so that's one way to go so I think that's that's probably I think because the
other way is it directly puts them into the account I think we want to have some way of loading in a bunch of a bunch of
and let's go and create a new test and now we're gonna have an account test that I don't think we've had before because
of the test it's unit test so what we want is what if we just want to load a single a single line so sort of a de
janeiro a degenerate collection so load single row CSV should and transaction to account so what we're eventually gonna
assert so let me go create an account object where we enter you're going to assert is that our transactions start off
simply with just saying it's gonna have a size of 1 we know we're gonna load one transaction and the string for our CSV
is I think I have this yes smart paste from IntelliJ it escaped our double quotes no but that right we didn't have any
double quotes in our in the CSV file that was exported so we've got a row of CSV what we expect so a new CSV importer
and then import and we're always going to have some collection of strings so basically be so we have a single string
we'll put that in a collection of strings okay so we've got our string single row in a list of strings and let's go
ahead and create this class so this is not a domain this is actually an adapter and initially it's only going to be used
by the web adapter so we'll put it there and it's going to have lips come on oh can I not use import here because it's a
keyword darn it I'm an import from there we go okay like why can't why isn't letting me create an import method darn it
because it's a Java keyword by the way side note in case you don't keep up with Java language new stuff that's coming up
Brian gets who's at Oracle working on the Java language our architects has a proposal about creating new keywords that
basically are hyphenated which i think is an awesome proposal okay so we're creating this method eventually import so
import is weird maybe it's translate transform CSV transform I'll leave the afternoon so the question is what's this
going to so it's going to import from the list and it's basically and for now we will return empty empty list okay and
so we'll hold on to this as transactions so I guess I was taking too big of a jump because we have this separate CSV
importer so maybe this isn't an account test because what we're trying to do so yeah because if we have a count somehow
rely on the CSV importer then that pulls it into the domain and actually I don't want that to happen so somewhere in the
adapter we're gonna have so really this test doesn't make any sense because we're not going to load a CSV right into an
account we're gonna go go through an adapter so do I want to stay in a count test which means what I'm really testing is
can I load a bunch of transactions and at once can I basically do bulk import and I think that's actually what I want to
do but account know about those transactions so basically this is going to be account dot load and then it's basically
going to be a list of transactions yes it could be a set because that's what we store internally because certainly
they're going to be no duplicates so but we'll see that later and for now this is going to so I will basically do a
count new great one of those hold on to a variable and then we're going to sort that account transactions is basically
equal yeah I'm not sure what we're gonna quite do here but let's transactions to load something like that and it's going
to be a set of transaction I'll just put this in Sam's you set for now so this will fail actually this might succeed
yeah actually curious will this fail or succeed because it starts out being empty but it's not gonna be equal to yeah I
guess it is okay I don't want that so how about I just do that because I don't want to unintentionally passing tests
okay that's cool so we'll leave it at that and so then basically this test does not belong here so let's copy this over
to CSV CSV importer test but that's going to go into the web adapter as we said where it was going to go let's delete
this test because we just copied it like to here okay so we're not actually dealing with a count here so this is going
to be import single row CSP should result in single transaction so we're still going to have a CSV string we're still
going to have transactions the CSP paper is going to do that but really what we want start off with having size of one
will do let's see no we actually know that what this is going to be so in case you haven't been noticing I've been using
mainly because I've been using a search a as for awhile but also it's it's what spring boot has pretty much standardized
on so one of the nice things about search a is that we can do these really nice assertions so I can basically say that
this list of transactions contains exactly and then I can go ahead and build up a new transaction with exactly what I
want to be so the local date time is going to be of and the year is 2018 a month is one and this is five and there's no
time involved and let's put this in a new line and what else we need the action so we're gonna basically turn cash
deposit into a deposit transaction you know what since we know it's going to do that let's not use this new let's use
transaction create oh great deposit and so the next thing is amounts so remember that this int amount is scaled integer
so it's going to be five thousand and then the source is going to be basically as is birthday gift and then we're good
so now if we this it will clearly fail we just hope it fails and of course it does because it was empty because our
import does nothing all right let's clean up our ports there okay so let's add some space here okay so what we pretty
much want to do is say lists of what lists as list I don't wish they would get consistent with that and we could just
you know a hard code the transaction but I'm not going to do that so let's see what what should we do well this looks
ideal for our good friends stream in lambda so we want is we basically want to do something like CSV list right the
incoming thing we want to stream stream that and then for each one we want to do some kind of mapping function so map is
basically a transformation so we want to take a string transform it to a transaction so something like C it's the
importer transaction from CSV something like that and then we just collected and then to list list oh my god I've
forgotten the syntax let's create this so create method transaction CSV so the so that's a static method that's fine so
we are basically taking a and we don't need that because we're not doing any further typing so collect collectors to
list right so what we're doing here is we're taking the list of incoming CSV rows even if there's one and then for each
one we're going to call this conversion transaction from CSV right so that basically will convert from a line of the CSV
and give us a transaction and right now that's going to return null which it's fine so if we go back to our our test
this will still fail because it will basically have a list of a null yes all right so we now have a list but the only
thing in that list doesn't know so that's good and so now we want to create a transaction from from this row so what we
want to do is if we look at what the thing looks like it looks like this so if we split across commas that should work
fine there is the danger that there's a comma in this description but I know that from the data I have it's there there
is none stuff not that's not a worry here there could be a string that's sorry there could be a comma I don't think I
have any if I was worried about that I'd probably just jump straight to implementing it to using a library not
implementing it myself but basically there's four pieces the date be B type the transaction the amount that's gonna be
fun converting that backwards and then the source so the typical way we would do that is we'd use string split there are
some other ways let's take a quick look good use of reg X but we don't need to worry about backs we don't have double
quotes so we could just do that so we can so one of things I like to do when I'm searching is sometimes you'll find
stuff that is old so if we look for anything since 2017 we'll get more recent stuff so we could use pretty much split
see what build owner has to say yeah I don't want to bring in a whole library to do that so we could just do sprint
string split we do have guava already so you know what let's because that's what more readable because the other thing
is if in case you didn't notice there's actually spaces here around the dollar amount I'm not sure why Xcel did that but
it is what it is so I'd have to trim those out so either I'd have to use a red X during the the split promise this gives
me a raisin I don't money I raise I guess don't have any any this seems kind of ridiculous like I'm gonna basically
stream the split stuff and then trim each one and then convert it back to an array that seems horrible from a garbage
collection object point of view yes I know it might be optimized away but I don't know if I was going to do this I don't
know why I would convert it back to a string array I would just collect it to a list since we're already have guava
imported let's just do that so we're basically gonna do I don't want to omit empty strings because I need a fixed set of
things so this is structured even if one of these is empty of course this one's empty we don't know what kind of
transaction is that would be a problem but if this is empty that that's okay so what we want is a list of string that is
CSV cells equals our CSV row I guess I should be consistent about what am i calling these rows or lines let's call them
let's call them line sorry let's call them rows okay so parse CSV row I see a row and we're gonna do something with it
here basically create transaction from sells so the reason I'm doing it this way is from a testability standpoint
because I want to basically test for me doing this kind of thing and getting the components correct getting this stuff
translated properly can be a bit of a pain to get right so so let's see well splitter it will split on a comma we'll
trim the results and we can split the list we're just going to be the thing we're operating on oh why is that marked as
unstable satin dude I'm using 20 sound its beta yeah I'll leave it yeah that's fine okay so actually just return this
directly all right and that's cool so I could have written the test first and I probably should have done that so let's
go ahead and do that it's not really last year but it's more sort of testing our our expectations this is sort of a
throwaway test so given that string will assert that that list of cells it contains so list string cells equals the CSP
and Porter actually the static method so CSP importer that and what we want to use is this as our sample and so we
expect is that it's contains exactly and so this is exactly in the order I give it to you and or sorry in order to give
it to you all right that I give it to the method versus in any order so I actually it should be in this predefined order
it must be so I'm going to expect that and then cash deposit and then so this is going to be still what's there so
that's going to be the amount and then birthday gift okay what's going on here now I forgot to close the double okay so
parsing this row should give us exactly this list of strings so let's run this method and that worked which is good
again I should have written the test first but that's okay so that's the basically validating that I understood how the
API worked I don't actually need to keep this test because what I'm really interested in is that I got the the
transaction so now we can move up to actually let's make this private since its internal I should I need to test this
method directly I'm testing a report from so now we can go back to that so what's going to happen is we're going to need
to the the hard parts are converting this to a proper date and parsing it correctly and then converting this to an int
scale decimal dollar amount so so let's see we have methods in our date formatting to basically go from a string to a
local date/time and I think that is almost what we want the problem is this one uses the dash separators and the year
first so we're gonna need another one so I think we're gonna rename this method because this one was used specifically
for from the browser so if you were in my last episode we were pulling in information that was sent in from the browser
and the way the browser formats the dates when it uses the specific date input is it's basically four digits for the
year two digits month two digits day with a dash as a separator so I'm gonna rename this to be from browser date okay
just cuz I'm a little paranoid it's run all the tests okay that one failed as expected and that one failed okay so we're
cool so now I'm gonna have another one that's basically that returns a local date time and this is from a CSV date and
so we'll have the raw date and so we're gonna have another one of these DeeDee and then why why why why right yes and so
that's just swapping this stuff around that and so local deep goes look update the parse and will parse the raw date
using this this formatter and then we return the local date and startup date because we're only using good night so one
thing we see here is as some common stuff kind of okay I mean I've got two methods are pretty straightforward I'm going
to just leave it with a little bit of duplication and this is the format that CSV file is why exported in Excel
separated by slashes okay and so back to our tests our test is still failing right so we haven't done anything yet okay
so we've got our cells we've converted them converted this into basically four components so what we want to do is we
want to get a local deep time and that's going to be the CSV cells the first one actually we could do but now we've
already got a list let's do get zero so this one is going to be our date and so we're going to convert that by using the
date formatting from CSV date and then the next component is going to be the action type so here the possibilities are
cash deposit interest credit what I've been calling payment so let's go back to our test import single row CSV deposit
as a result in single deposit transaction so right now we're just testing deposit we're not going to go yet overkill on
all the different types because if I do one at a time so we now have string we'll just know that that's get zero so
basically string action or transaction type in a CSV cells one and then the next one is we need to convert CSV cells the
second the third index which is this part we need to convert that into into a scaled in so we have this scale decimals
thing that we've used before and let's take a look at that so it has a way of decimal two pennies given an amount we
also have somewhere in transaction view so this is a format as money so this basically takes an int amount and converts
it to format as money so doesn't feel like the code belongs there and it's really straightforward so I'm not gonna that
doesn't seem as reusable as the other so dollar string to scaled int and that's that one okay this is probably pretty
strict for it's already going to be a trimmed string and so what we can actually do is we can cheat since we know our
data is always going to have two decimals yeah yeah we can cheat on that somebody ever decides that they want to import
a spreadsheet that's different than this then then that will be a bug filed and we will add that feature but for now
right now I'm guaranteed so we can actually cheat we can basically eliminate the dot and we know where that is and then
eliminate the dollar and then just complete it as an integer the only problem is if there were commas so we can do is we
can strip Oh wonder if we can just strip commas dollar signs and dots I'm sure there's something we yeah so we can
basically use as I figured reg X to the rescue so we can so say int string equals dollar string replace all and so what
is it basically anything that is a dollar which I think we have to escape a comma which I think we have to escape and a
dot which I think we have to escape and I always forget whether it's a double escape or not so I think we have to double
escape it because otherwise we can't put that in there and basically replace it with nothing oh I'm not sure if this is
going to work so I'm gonna want to test this so let's say you've done an escape maybe I don't need that that's right an
escape how do I not need to escape these because you're inside of the brackets maybe I guess we'll find out so let's a
formatted dollar to in to string you know you know remove formatting and it's going to return a string let's refactor
that okay and so then basically it's just going to be in string I know the names are kind of ugly and then this is parse
int parse it's your horse int and this thing and I'm just gonna inline it oops okay this is the thing I want to test
because boy I have no idea I don't use regular expressions often enough to be sure that this is the right thing again
this is this is a test that I'm gonna write is to make sure I understand the the API so even though it looks like I'm
testing replace all I thought I could just do that I could just put this in a test so let me do that so what like do I
understand that I'm using this correctly let's go back to a test that's create and isn't basically a temporary test temp
test reg X so I'm gonna assert that this thing and let's this string dollar or string equals 50 a lot in fact let's do
the the pathological or sort of worst case yeah hey he's a millionaire let's actually give him 1 million bucks he's just
got five million dollars as a deposit mm-hmm I'm scared to think what would actually cause that that it's a to be
something real okay so here I want to assert that this is equal to so this replace all so I expect it to actually result
in basically 5 and then 1 2 3 1 2 3 1 2 like that let's run this test ok so it does what I expect because I had this
wrong we'll see that yeah okay well okay that worked nicely so now I don't need this test because this was sort of a
temporary test to make sure I understood the Reg acts work does expected ok so this is going to convert it to cents
because we basically cheated by dropping out the dollar and the comma all we're left with is a bunch of zeros so this
dollar 50.00 will be conferred to 5,000 parse it as an int to return this back to being private and so now we jump back
up to here so we've got the local date/time we've got the transaction type as a string we've converted the amount to an
int and then the last thing is is basically the description technically we've been calling the source but only for
deposits otherwise we use description so now this is basically just CSV cells get and that's the last cell okay so we
basically converted these into their components and now we can just return a new transaction so that now right now we're
only doing a deposit so I'm actually gonna sort of take a smaller step and just say transaction will create a deposit so
local daytime amount and description okay so I think we're ready to now run our CSV import test so now this probably
passes and it passed cool okay so this is a single deposit we can now test import so multiple rows multiple the CSV
deposit up like a spell deposit rows should result in multiple positive transactions why my spelling is going downhill
here which probably means I need to take a break we're coming up on the next hour I'm going to keep pushing on this but
I'm gonna take a break in about five minutes or less so let's go and grab some more of our sample data I'm gonna take so
interest credit I'm gonna have that's going to be a separate test but let's do let's do these two these are interesting
because they don't have dot zero zero they have dot seven five and we'll take those two transactions so I will say list
CSV lists those lists lists and will say that one and that so I've got to those and we'll convert a transaction so new
CSV import or import flips import from our list and then we sign that to a variable which is going to be our
transactions and now we can assert that transactions contains exactly and so we have a transaction create deposit local
daytime of so that first one is 20 18 5 3 and then 0 0 and then we got 675 is the amount whole return is where it came
from so that's one transaction and then the second transaction is also deposit local daytime of 2018 5 24 0 hours 0
minutes and that one is 775 that one's also returned this one what might just work because I operate it because I have
read the whole thing it's run o tests it all works all unit tests that one doesn't work because we have not hooked it up
yet to the account that's ok we're not there yet let's do a commit here so basically implement so we can now import
deposit import cash deposit transactions from the CSV so we haven't handled the to the two other cases we need to handle
one is the one that's listed as an interest credit which is right now basically deposit and the other one is is the
spend which is basically a spend and I wish I do you would stop doing that okay all right I'm gonna take a break and I'm
actually gonna continue on because I want to get this story done so where we are is we're still doing the CSV file to
pre-populate we've got deposit working so when we come back we're going to handle the spend the interest credit and then
handle being able sort of copy and paste that CSV into a web form it's a big text area that will then load up all the
