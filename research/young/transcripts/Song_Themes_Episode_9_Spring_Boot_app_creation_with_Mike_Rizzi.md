# ＂Song Themes＂ Episode 9： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=pavYN7Yy2pQ

---

## Transcript

all right folks welcome to uh another episode of working on micro's song themes app howdy uh so where are we at what
what what what have we been up to H well I do know that we didn't check in something because we the middle of uh messing
around and I'm trying to remember what it was we were doing um well we had a failing test I think we left as a
breadcrumb right no I think it was even is it just a failing test let's find out uh there should be a failing test yes
right right right right we did we did do some a little bit of prepare refactoring when we uh when we wanted to and so
that's where we pulled out that index songs by the right we're getting ready even though we're red we figured prepare so
um so what we've been working on and uh as you can see in the jira uh is we have um we previously had working where we
could add songs and each song had a single theme and we could find songs by that theme and so what are we doing now so
now we're um if we have a song that has multiple themes which is fairly common um for example a song could be about
vampires and Halloween um or in the example we have in our test it's a song about Halloween and Christmas thank you Tim
Burton yes um and so we were going to implement adding a song with multiple themes but we realized oh how would we test
that if we can't search to see if we got it so we reversed these two Jas 33 and 34 so that now we're gonna Implement
first find a song if one of its them match so that's where we're currently at right and we had some Java stream issues
that we were struggling with right before they stopped right um and so uh this this sort of pattern of of development of
doing the the find before we do the ad um sort of the query before the the modification uh seems to be something that
that I typically do I've I I don't know if other people do it this way I it's something I need to pay a little bit more
attention to when I watch other people do um test driven development but I find it's one of those how do I know it
worked unless I can ask it for the information and see you know like it's like if I give this thing information and then
I query it that's like testing two things whereas if I just say it's in there let me see if I can get it and now I can
say if I add it I should see it uh feels like the right way to do things but um it's sort of a higher level higher level
pattern of how do you how do you slice basically how do you slice your stories right so which is actually this example
that we had yesterday yeah it was yesterday um is a classic example why you don't want to plan too many stories in
advance right we thought we would do you know story a then B and then once we started doing it it was like oh nope we
need to reverse it yeah yeah and so as they say plans are useful um but uh it doesn't mean you have to follow that plan
so you can and this is where sort of I always find myself not writing out much of a list of tests to do for exactly that
reason whereas you know Kent Beck reemphasizes in his Canon tdd article um write write a list of test first but I think
you you can only do that if you get sort of like okay we know we're going to need to to to find a song um and now we
could write the tests but I feel like we could just go write them we don't have to write the list uh and keeping track
of the other things like well we know we're going to need to add a song with multiple themes through the the uh the
object um and that that is sort of our list so anyway it's it's it's interesting how uh how you yeah you don't want to
plan I think it's I always look at as like you don't want to plan in detail much in the future you do want to have some
idea of where you're going right otherwise the whole IDE the whole metaphor of navigation doesn't work if you don't know
where you're going how do you know you get there which is one of the advantages of the old school XP version of I don't
know if it was XP but your story is whatever you can write on the index card with a sharpie so you're talking like five
maybe seven words depending how big you write um so that's not much information but like Ted says that's your you know
that's your you know what you're doing yep next you've got a few those hey there the pig cat 76 nice to see you again
best best login handle yeah hey tram star nice to see you um I was gonna say something about uh Aggregates but I'll save
that for later because tram Stars was asking a question on the Discord about Aggregates and aggregate Roots um so one
thing I'll say is uh there's a term that I that I've really started uh that I want to start using that I really like is
this idea of uh and I I don't know I have to go and find the the link to the person who who came up with the name
decider so one of the things that Aggregates do is make decisions um in general objects or any behavior is making
decisions but like the aggregate is like this main uh the aggregate root right which is right now um I guess it's our
song Searcher although there's not a lot of domain objects there yet but it's the thing that makes that makes decisions
um we don't have a lot of decisions in our application but uh I I've always dislike the reason this came up because I
always dislike the term aggregate root I find the term aggregate which refers to the set of objects that we're talking
about or the graph of objects technically a directed graph of objects um that's the aggregate right that's the scope of
of change uh but the the object you're talked to right you don't talk to all those objects you talk to a single object
um Eric Evans calls that the aggregate root uh I never lik that name because I found it was confusing because they both
had the word aggregate in there uh and so I like like the using the term decider instead of aggregate root because that'
s the thing that decides so for example if you have a shopping cart and you add items and there's a limit to how many
how much uh you can add dollar amount uh Worth to your shopping cart it's the decider that decides you can't add this
anymore so um that's kind of the use but we're just not even not even there uh at that level yet so um does it
distracted for me to take the notes like that on screen because I could do it off screen no no it's good I just figured
it's good for other folks to see you know uh so uh make sure you ask this if you didn't already in the Discord tram
stares because I'll answer it there as well um when Aggregates reference other Aggregates they cannot ref reference them
by the object because otherwise you've basically included that other object in your transaction so again the example a
shopping cart and a customer if you put it all in one big aggregate then then yes customer as one of its things would
have uh a shopping cart object but that means when you load and save the customer from the database you're also loading
and saving the entire shopping cart and all of its products and any other information that's probably not what you want
um because if I want to just change my email address why are you going to load in the shopping cart I'm not dealing with
a shopping cart I'm not I I said nothing about the shopping cart I just want to edit my email address um and so by
putting shopping cart inside the customer aggregate right if you reference it as an object it is now part of that
aggregate so the way you access one aggregate from another identifier and so um if you want to find out hey what you
know let me see the shopping cart for this customer you load the customer you get the ID of the shopping cart and then
you go fetch the shopping cart so that's an explicit load into into memory and that's loading then the shopping cart
Aggregate and now you can play with the shopping cart without having to deal with customer at all you already know ID so
you can have other entities right so the two different kinds of objects that you find in an aggregate are entities and
value objects that's like the fundamental atoms of of development um value objects are immutable uh but they can contain
logic so just because it's a value object doesn't mean it can contain logic so a good example uh is um a money instance
I want to uh take two monies and add them together so there's an add method or um I have a percentage value object that
represents some discount and so I want to say given this price what is the discount how it stores that internally maybe
it's oneir off maybe it's more complicated than that um but it's a an immutable thing then that is uh also a value
object so value objects are immutable don't have an identifier because there's no reason to differentiate 25% off here
and 25% off here it's 25% off the definition of it value um but you can have multiple entities in an aggregate uh one of
them still must be the decider right the aggregate route but you can have a bunch of other entities um generally though
you don't just you don't have more than few and so that brings us to this question which is who's the decider so in
almost in most situations you're going to find that there's going to be one object that is kind of the container so
shopping cart what does it contain it contains products so product uh in cart might be an entity um and although it's
likely going to be value object you could certainly say say say it's an entity you might have reasons for that maybe the
quantity is mutable maybe there's customization for it such as embroidering on a hat something like that um and so so
you have products in your cart that are that are entities but from the outside you don't generally sort of ask it
questions but most but mainly you don't ask it to change itself you go through the the container so you don't just
create products out of nowhere you you have to to say can you please add this product and who do you talk to you talk to
the decider who's the decider it's the cart so cart is a container and and it has a bunch of these things it also has um
things like well who's the customer but that's just an ID uh it when it gets turned into an order it there might be
payment methods and things like that um in general it's it's once you've decided sort of what is the scope of your
aggregate it's usually pretty obvious what the root is who's the decider who's making who's doing the creation who's
making sure that any constraints are are held right so you might have an invoice and line items on an invoice right a
lot of General business stuff tends to be like that you tend to have a container object that has a bunch of other things
in it uh that are like things um not always but but a lot of a lot of times when you have something like a customer well
what does it have it has um shipping addresses billing addresses payment methods contact information notification
settings but really you're talking about what do I want to work on what do I want to load from the database and that's
your decider or that's your aggregate route um lots more lots more examples we could talk about but I think hopefully
that that gives you a sense of of how do you know when the entities need to be uh which entities need to be aggregate
Roots uh the last thing I'll say is sometimes you'll guess wrong or sometimes things change and you might decide these
two things I want to be and then you split your aggregate it's a bit painful to do that um but it happens so you split
your aggregate uh and this happened in my ensembl application uh it used to be that uh Ensemble actually held the
members that clearly was not the right thing to do because members have their own life cycle uh but it started out that
way and then I split it into into two Aggregates uh and then that made a lot of things much easier to deal with so you
may guess wrong um but I think doing things like uh event storming um and maybe some kind of other kinds of modeling
will generally get you to the to the to the right Aggregates uh or at least get you most of the way there and then what
you do is you run scenarios through it it's like okay we want to do this what does that mean which objects does it is it
going to touch uh and that's this is a great use for CRC card s um and then you can basically you know run through some
some scenarios and see you know oh actually we we keep loading all this data and we never use it for these scenarios
well then let's split parts uh but you know again you're you're you might guess wrong refactoring all right uh so we
were dealing with um basically indexing songs that have right we were going somewhere with the idea of changing the
implementation of index songs by theme right and intellig was not being helpful by writing this as as some kind of for
um so there might be a way to use uh some stream operations to do what we want I am not smart enough to know what that
is so I'm going to suggest we replace um this collect grouping by with uh Dumb Dumber code uh get the test to pass and
uh so let's so in a sense we're going to do is a prepare refactor room by sort of downgrading this this lovely
collectors grouping by to a to to some kind of loop um and then uh and then we'll we'll modify it to support multiple
themes so let's make sure we're we're able to a factor by having all our tests pass which may mean disabling the one we
currently have failing this one so you can tell in the gutter that there's a little red exclamation point that means the
last time the tests were run it failed yeah one and what I wish it would do is as soon as you type disabled I wish it
removed that red mark because like disabled um but it doesn't know the status of it until you run it again so let's run
our tests again and then it should show up as as properly disabled oops that's not what I wanted no that's not what you
wanted alt shift F10 yes okay disable oh there we go it does it does show it but you have the you uh it does it won't
automatically expand it um got it is is because it treats it in a sense as as having passed as having pass right problem
or oh no thought I wasn't sure if you were oh I was waiting for you to close the run Windows sorry Oh I thought you were
looking for the shortcut to do that I was reading tram star's latest and I was thinking that's what you were doing so um
okay so what's in so what's interesting is is now it shows that test is not having uh done anything which is nice so um
so now we can continue uh and I'll trar I'll I'll address your question in a bit um so let's uh let's go into the the
implementation half uh and let's I guess let's Loop through each and then uh let's hit enter to make some space for
ourself um and so each thing so so we want a a uh no just song Arrow uh and let's see so what we're gonna want to do for
each song right now and I know that map doesn't exist yet so we'll make that come into existence in a second and what we
want to put is uh this is going to be song dot um yeah song. theme do.get first uh comma oh and here's where we have to
do that uh the so this is actually going to be a put is it gonna be a getter default um we got rid of rid of that code
when we switch to the much nicer grouping by let's let's cheat a little bit let's do nope yeah uh let's go ahead and
create whoa I don't know why it thought that that's a ridiculous suggestion uh what we want is the same as the return
type on this method the map of string to list of that straight map or hashmap uh hashmap because we want an actual
implementation right right right yeah interface yeah I don't think I've ever needed a l log back MDC adapter uh I think
for me I actually have a bunch of things in my exclusion list of of don't even bother importing it um but I don't know
if it if it affects its guess for for declaring variables but anyway um why is just unhappy oh because it shouldn't be
title it should just be song so just say list of song oh because we're indexing songs not not song titles right okay um
let's uh delete from song stream to the end of the of that because we're going to map okay now I expect this to break
some tests but let's make sure it it breaks only some tests so the ones that are asking for um out of and some past
though right can you turn on the the passing click the check mark check mark there we go yeah okay uh maybe a third uh
can you look at the implementation we had for in the so go into the gutter and just click on the on the blue in the
gutter oh two lower case okay good so we forgot the two lower case so let's add that in because I I expected fewer
failing tests in that you might have seen our parameterized test that we're testing all the cases only two only two of
them pass so that's on that's on the get yeah so here yep that's normalizing our our theme all right uh now I expect
still some tests to pass but only those that are about theme okay much better so search theme for multiples matching
song that fails uh multiple songs are found by their theme that fails uh that one's interesting so this one say results
uh that's basically the same thing um because I'm not sure we should be as precise in that test though can we just sure
yeah so here we were just saying that it has nonempty uh I think our contains I think this is actually too precise at
this level mod with non-empty search results CA um it's either going to work or not failed didn't provide us with any
additional information any thoughts on on this one no um sorry I'm looking at it and I'm like you're right it does seem
like it's asking for more information because if it's just saying non-empty search results then that's probably what we
should be asserting yeah we shouldn't do contains exactly yeah so let's just say empty interesting the trick is you can
use the you can use if you type in uppercase E so is and then NE uppercase oh right that way then it auto it'll it'll
always narrow down your search which is usually what you want when you're Auto yeah and get rid of all this and then get
rid of all that so I'd like to see this test pass the because this is not testing the behavior of the Searcher this is
testing the connection from the controller to to to the service so so now the two tests that fail are basically
specifically about multiple songs added uh for a single theme we could also question do we need level um I kind of think
that that's not needed either do we have because we've got uh added songs are saved and save songs are loaded um I think
it's doing outside in yeah I think this is fine because this is one this is basically uh testing that added songs are
found so this is fine I'm I'm okay with this I would I wasn't happy with the one at the controller but I'm I'm okay with
this for now all right so now we've got uh failing tests because we haven't fully converted the the wonderful grouping
bu to our our lowly uh for each so let's fix that uh let's um let's surround the whole map uh part of the Landa with
curly braces so we can write multiple lines of code no no no not there so from map to the end of the line ah actually
could I do it might have a uh so you don't have to select if you just do an Alt Enter I bet it will suggest uh
surrounding with braces yeah yep expand body y there we go cool um that's much nicer because it also adds the necessary
semicolon which wasn't required do default uh and basically cut the the first part lowercase so let's cut that put that
on the getter list yeah uh and then let's assign that to a songs uh and now basically get rid of 24 song yep I expect
this to now pass all tests um oh in the case where it's new we didn't add it to the map okay uh after line 24 let's do
map put so pretty much you can copy the yeah and then replace get our default with it okay there we um so now we're
we're back at at the behavior we had before but now we're we have it in a way that yes uh full full hello and yes we
want to add the basically index the same song under under all the themes that it has uh now that we've done our prepare
refactoring we should probably do a commit and then we can uncom we can reenable the test watch it fail and then we
should be able to relatively pass um see I want to write the method but I know that's not such a good name um
refactoring for multiple songs English I'm fine with that okay great I am too done okay um now let's reenable the the
the uh the we go rerun yes so this will fail again because we won't find it under uh under Halloween we're only
excellent um we could we could make it pass which would be really terrible uh because we'd break all other tests but
let's do it just for fun um so instead of get first uh let's on 22 there let's um let's actually first extract that
entire expression to a variable because twice uh and let's extract that to a local variable theme or normalized theme
and replace both replace Dar I guess it's not really the theme it's it's our convert it to lowercase right there we go
all right uh and now on on 20 let's change that get first to be get uh and then with a one in parenthesis Ah that's
definitely goingon to break it should break all but pretty much every other test uh in fact it might cause a bunch of
null pointer exceptions um so I'm not sure it's worth it but let's see what passing so but that's right this is if we if
we weren't sure the next step to go this would be triangulation because we' say well got our our our most recently
failing test to pass and we' broken everything else um all right so what's nice about this however is this provides us
with what are we going to need to iterate over so let's extract out um just the song. them.get part into another
variable theme y okay um wait a second oh right yeah that extract uh actually we don't need to extract now what we can
do is um instead of directly accessing element one we actually want to iterate over lines 21 through 24 for each uh for
each theme so we can do this a bit further uh theme and these are the uh themes yep right and so now instead of theme
doget you can basically uh replace that line themes so if you do themes. four oh and then it'll yeah and you want four
okay and now just let it go um and now take the rest of those lines push no uh Delete sorry delete the delete the theme
equals themes. Gat the whole line the whole line okay and then put the rest of it in the loop yeah that's what I was
about to do then you said okay so then I was confused uh sorry I I saw you delete something I wasn't sure where you
delet it yeah that was deleting that then was gonna copy what was oh okay but um uh should said it out loud so now
themes on the loop yeah because we pulled that out for clarification but um and so I did this piece by piece because
there was that one bit that we're basically saying instead of just one of those we want all of them everything else
remain the same uh and so now if we run it I expect everything will pass oops and it also points to theme is wrong as a
name but we can fix that in a right uh yes song. theme actually does return multiple themes that that's one of the
changes we're working on so we'll have to rename uh that component so that it better indicates that it's uh though so um
if you click on uh new array list there I think there's a way to is that what you meant redo yeah I thought I was going
to do an array list colon colon new but uh it doesn't matter that's fine okay commit um thoughts okay well it uh it's
not multiple songs by their theme it's multiple it's songs by all of their themes all right or by any of their themes
yeah right it all right uh let's rename theme to themes to better indicate that it is a this one yeah no not sorry not
that one I thought you highlighted the the other one the the record okay and let's run all our test just to anything
excellent um let's run all of our tests all I shouldn't have done the it good so far excellent y uh and so what's
interesting what I want to point out for those who um weren't aware of of the other parts of our code so we've changed
our internal structure of a song uh to have multiple um we didn't have to change anything here because we translated uh
these songs into song view view um it's just got it's just got the title so if we wanted to show multiple themes we'd
have to modify that here um but it was not a direct so I've seen a lot of folks when they write codee like this they'll
basically take their domain object and directly throw that into their either return it as part of their API or throw it
directly into their MVC model which means you would have now broken all that stuff and so what we've done here is we've
shown that that our adapter which contains our controller and the song view is decoupled uh structurally uh in terms of
what a song is um and so we can change our domain as needed without being forced to change our adapter we probably will
at some point want to change our adapter but the idea is we're not forced to right yeah it would the adapter would be
changed when there's a requirement or a story or a need for it to have additional information right and if we were
displaying all the themes for a song we might have to do that um right but we can do it a piece at a time and this goes
into the idea of we want to do everything in small steps where after each step you are at a safe Point um which is why I
usually add the word safe when I'm talking about uh uh these kinds of steps so um G Hill talks about this idea of many
more much smaller steps um and I always tack on the word safe we want those steps right you don't want to be sort of in
a precarious position as you're taking each step you want to be conf confident that you are in a good place where you
could stop um if you had to and then you can uh be in a good place step uh so code to load what I recommend is new in
Java and W boy I've got to create an FAQ for this I really need to do that because I think pretty much every single
stream now uh I'm getting to ask this question which is a great question and I'm happy to answer it but um I think I can
uh for next time I'll create an FAQ actually I should go into the video where I've answered this where I think I'd done
the best answer and go exract that and create a short um my basic answer is it's there's two parts uh one is um come up
with a project so no matter what you want to learn make have a project in mind and it could be a project you don't have
to invent a new thing uh while you might want to do something that would help you personally that's the ideal is that
it's something that you would actually use um above all you want it to be something that you're interested in um if you
can't come up with anything then you can fall back Towell I'll do a to-do app and maybe I'll do something interesting
with um you know how things are prioritized or maybe I'll do something that uh helps me schedule things or um but you
want to make it something where you're going to be motivated to to work on it and then um you for for uh for spring boot
spring boot has their spring Academy spring. Academy and it also has a bunch of guides that's how I learn spring uh
there certainly are courses out there that you can take um but the most important thing is that you write code write
code write code write code the only way you will learn is by writing code you will get informed and have and be able to
get information by watching uh tutorials and also watching streams like this where you see coding happen but unless you
actually do it you won't learn um and so you want to be able to to do it ideally if you can find someone to work with
and pair program or work in a group right in terms of like the uh priority and so on that would be the absolute best but
if you don't you still want to code on your own Rec I recommend um before moving on to Spring boot however that you are
confident in your ability to write tests because above all at least for me um and I think uh I have a pretty
well-informed opinion you will be much tests then uh pick up Spring Boot and learn how to test spring boot there's some
good resources on that um hit me up Discord uh you can find out about the Discord you can go here go to ted. Discord um
lots of folks there who will uh answer questions and and help guide you and and there's lots of good resources there for
for Learning and and and so on and there's some good resources specifically on how to how to test spring boot but you
got to know how to write tests first question thank you TR Stars yes I I wrote I took a note to to write to start
pulling an FAQ together um there was a question that I saw oh uh I'll answer this one and then we can uh dive into some
of the some of the stuff that moty's uh brought up Mei uh so we can do this for Loop because the map is not a string to
string or it's not a string to song It's a string to a list of songs right each theme which is the first string can have
zero or more well really one or more uh one or more songs right so the same theme like Christmas can have multiple songs
and so we can't just have it's not a onetoone mapping it's a one to many and it's really interesting I did a a bit of
research and it's like why doesn't the jdk collections have multimap and apparently the answer was not enough people
wanted it I I agree it's not as popular as a map but I've definitely used a multimap much more than I've used like a a
deck a double-ended que um anyway so it is what it is but but because it's a one to many uh that's why we can't just do
the the for Loop otherwise that would have been easy um while you answer that I'm gonna I'm yeah uh so um if you are
testing something directly against a database you have to ask yourself what are you testing are you T testing your
knowledge of interacting with the database so are you testing your queries your inserts or if you're using an orm are
you testing your understanding of using that orm or are you testing that your orm is writing to the tables in the way
that you expect right so you're actually testing am I using understanding the database correctly then you want to use
something like um test containers so where you can under control of your tests start up a database do your stuff when
you're done it shuts down and that way each one is is independent each test of your database stuff is independent from
the other one that's great test containers are are awesome they Bas they're used they're based on Docker but they're
under the control of the test and spring boot especially um has uh great support for writing tests using using test
containers but if you are test testing things um so if you are testing things like the criteria API if again if you're
testing your queries if you're testing database specific functionality or om specific functionality then you will have
to use your orm or your database in which case you're going to have to use test containers but there's lots of tests
you're going to write where you need a database but you're not testing the database and this is where you do want uh a
test double of some sort so a stub or a fake uh you can also use a spy like thing called an output tracker um where you'
re just testing have I saved the right thing at the right time with the right information but you're not testing the
Persistence of that you're just saying hey when I when I change the customer's email did it save a customer with that
new email you don't need the real database for that right because you're not testing the persistence you're testing when
you do this operation did it do the right thing in terms of modifying your object and asking it to be saved so that way
you've tested the the your in a sense your command your intention I want to change the email address on this customer
did it end up putting uh and calling to the persistence hey I want to save this customer with the correct email because
you've already got test that when you say save this customer it saves it correctly and so you want to that's like the
fundamental thing I talk about when I talk about testable architecture is you want to separate those those concerns so
you test your database I know if I save my customer correctly and find it by various ways using fancy criteria API
whatever that that works and I can be done with that and put it aside and now I can test the bulk of my domain logic my
domain behavior um without having to worry about persistence and it can run really fast because it's in memory and uh
even though test containers are fast it's much faster orders of magnitude faster memory I type too you uh let's see um
right and so the idea is you you want to use test containers when you are testing database specific functionality uh
when you are not don't use it and then it will be fast um but if you set up test container so there's a lot of ways to
to to configure and set up test containers in a way that is super fast where the overhead is basically running the first
test and then all the other tests use the the test container that's already running um and I found on my three and a
half year old uh iMac that it runs in well under a second so um but even so a couple maybe one or two seconds um which
is too slow for my regular cycle but it's fine for for a wider cycle uh yeah I mean any hashmap I mean if if you're
worried about concurrent access um I think that's a separate issue like you shouldn't need a concurrent hashmap in your
tests unless you've got parallel test running uh which I don't think would save you much if they're all in memory well
then aren't they are tests I mean I'd be worried about tests impacting other tests like what's going on yeah so i' I'd
be yeah so I uh I'd be curious why concurrent hashmap and why you felt the need to to have a a concurrently a hashmap
that can handle concurrency when you really don't want your test like like mik was saying it's like you want your tests
to be isolated uh from each other and not be able to interfere with each other which is really what isolation means um
so you shouldn't need need concurrent hashmap unless there's something else going on maybe um Statics static functions
that change yeah you know state I'm I'm not gonna guess yeah you're not gonna guess yeah yeah yeah and so basically what
you've done um and the danger that you have to watch out for is are you writing a database so again if you've got where
uh you're doing some fancy search that requires multiple joins and so on by your omm don't write a fake for that don't
try to emulate I've seen that happen I've seen folks who are who are just starting out it's like oh let me write a fake
for this database oh I am going to implement what the database does when it does a fine by this containing this and that
it's like no that's not the purpose of a test that uses a fake the purpose of a test that uses a fake is I'm not
concerned with that if I want to if I want to test how the queries work and how complex queries work I'm going to test
directly against the database because that's where the implementation is but you don't want to start emulating right the
idea is not to emulate a database and that's that's that's the many people have gone down that road and down um so one
last question then we'll we'll uh either take a break or or or continue um data structures and algorithms um I answer
this by saying are you interviewing for a job and have they said you were going to be interviewed by being asked about
data structions and algorithms then you will want to cram for it cram for your interviews reason I use the term cram
specifically is that means you are going to study study study that so that you remember it long enough to get past the
interview and that you never have to remember it again because that will be the fact of life once you get past your
interview you will never use that you will rarely use that information again and I always use the story of I crammed
when I was interviewing with Google if you had asked me a week later all the stuff that I crammed I would not be able to
tell you the difference between this s sorting algorithm this other one or how to do this other thing or what the Big O
notation on on this stuff is and it didn't matter once I got into my job if you think I used any of that stuff you're
sadly mistaken and I was sadly mistaken um because you end up working on on regular old stuff for the most part unless
your job is going to be to create novel search mechanisms for or novel ways of of implementing joins and databases um if
that is the job you're going for you probably already know that stuff because that's generally not stuff that an entry
level or Junior developer is gonna going to get into for the predominant set of jobs you may need to know data
structures and algorithms for the interview and then you will almost never use that information in your actual job that
is the sad State of Affairs of interviews My Hope Is that you don't have such an interview um the reality is you will
likely have such an interview uh once you get to senior level you can start saying uh as a as a response to a question
where they ask that is saying how is this used in the position I'm interviewing for because I couldn't tell you what
what the Big O on on a quick swort is I could go look it up and I understand what it but like what what how would I use
that information in my job is it would be my question but you know that's as a senior where I get this say you don't
know how to interview so let's let's move on and you know how that turns out and and I've done that I've been like that'
s a ridiculous question can we can we talk about something that's more relevant to the position that I'm interviewing
for um sometimes that's not a great reaction sometimes I you get a laugh and it's like yeah okay let's talk about this
stuff um I have one other case when I call external API it's a pooling API I need to make more calls to get the complete
response how do you test those scenarios um it depends I the there's so many ways to attack that that uh I'm not sure I
could I want to take the time here on stream to to go through that um ask ask Discord all right uh lots of questions
coming up y um what should we do next Mike I think a break would be good okay so let's take uh what break I could do
five all right we'll take five um and when we come back we'll figure out what we're going to do next um now that we've
got multiple themes index per song so we'll cool all right um so as a reminder uh I have a Discord Community where um a
lot of the questions that come up we talk about uh so things like the aggregate root stuff and things like testing
especially uh hexagonal architecture which is what we're using here um to help make uh some of the code more testable so
go ahead uh join us ted. deev Discord has the information um and you can also uh a separate channel for discussing what
we talk about here on all right should we go back to the code yeah sounds good so we got this working so is the next
step to figure out what we're going to do next um well we got stuff working or we oh we didn't refactor yeah yeah see
we're all prone to that I should put on my refactoring hat yeah yeah thought you had it on no I had my my uh change
Behavior Happ oh change Behavior it got warm enough that I don't need it so I don't know if you have any thoughts about
uh potential refactoring I'm just looking at the code right now me I mean normalized theme well one the for big so it
could be put into its own function that's method could inline theme or normalize theme but the fact that it's named is
kind of helpful normalized theme uh well we use it twice so we can't just we we actually extracted it for that reason
yeah yeah yeah right right forgot about that um did you want to go back to removing the for Loop and go back to uh see
if intellig can help us well I was gonna say if you put the uh carrot suggestions uh second collapse loop with
improvement although interestingly it us what would that what would that look like can let's let's do that yeah that's
not really much of an improvement in fact I think it's actually worse yeah hard to grock what's going on yeah all right
let's let's restore that um if we put the carrot on the four each does it suggest anything I doubt it but curious yeah
that's not really a thing um if we had the AI enabled I I would be really curious what it what it would suggest whether
it would actually come up with uh a better uh a more stream oriented solution because I'm guessing that there probably
is a way to use the the grouping by and and a flat uh and some kind of flat map in combination that might get us the
same thing but um so so what so so this is an interesting thing because we could say we could sort of you know refactor
piece by piece refactor the for Loop out out into a method and then refactor out the the the sort of the thing that
actually puts it in the map into a separate method um but if we do that we might lose the ability for us to find a
different way to refactor it yeah I agree so I wonder if we should just leave it uh and maybe I'll ask AI yeah it feels
ugly but I'm don't have I mean we could we could we could do one step and just pull the four Loop out and just say index
index index song for themes does that one come as a no no have to do the extract to there uh well just let it let four
yep oh yeah oh interesting uh that was one level out so it it wants you to extract it to a Lambda um which I'm fine with
actually I think that that's better uh because we can then just call this uh index song or index song by theme by themes
now the fact that we're passing bit um but I don't know that we can get around that at this point and consumer as the
return type yes because what uh what this thing is is it's not something that does anything it uh take it it basically
is a cons uh you're returning something that will be able to consume songs so it's a it's a song by theme IG so ises
that I mean this is actually by themes as well index songs by so this one is index songs plural plal plural and then
yeah and so I wonder I wonder if uh yeah intellig is not going to help us much more than that all right um and we could
probably collapse 19 through 21 into a single l line using the the join lines which is control shift J yep which doesn't
work when your cursor go all right um um run run the test yeah let's rerun the or or just IO free oh let's run them all
it doesn't take that much longer and cycle looks in um before you do that though oh no go ahead and do that yep right
good enough or do you want more inform so I personally don't put nearly as much information as you are I would just say
R because if I wanted to know how I refactored or what I refactored it would be obvious from the diffs got it so
refactored all right so what do we want to do next um we now support uh oh let's yeah let's close our entries so we can
now find a song yeah yeah so now we tackle ad it's I guess so yeah welcome okay where to back to service level uh so
let's see um is this level so what do you think I'm GNA bring up my want bring up your drawing my here here we wrote a
subcutaneous test that tested against the service so tested against this thing um but the service isn't doing anything
other than pretty much Searcher because we have other code that ensures that our song service is actually talking
Searcher uh why is that yellow that should be black and that should be do that so we've got we've got tests that that
test this connection um we've got it and but this test is out here and so we're basically testing through the song
service but really what we're checking what we're testing is the song Searcher Behavior so we probably want to migrate
this test down to the test or we just rewrite the test from with that new knowledge or can we refactor towards that so
we're pretty much going to um copy and paste the test remove the stuff at the other layer and then that's it so we'll
sort of peel off peel off a layer that is currently present in the test so if we look at the test we see that we create
song service and uh we call song service and we're basically just gonna for the most part replace that with the song
Searcher so let's let's copy copy the whole test move it to song Searcher test now are we checking that we're hitting
both of these in another test yeah because have a test where add uh right adds it to the reposit it's found in the
repository yeah yeah yeah so okay so I'm sorry you said let make another test a clone of this over in search by themes
yeah yeah so we can check what package is in domain how do you know oh I was doing it by yeah oh okay you were looking
at the path yeah I just look at what package is in yeah right right so so we're in domain and so that means this test is
at the correct layer um and this is where I wish you could also color test things which I guess you could but we
generally don't but anyway uh so this test is at the right layer and so um we can now uh paste the here uh and uh sui
brings up an uh an interesting way to do this um we could basically try inlining it I I don't know about that we'd have
to we'd have to see um yeah so it's it's doesn't quite I mean it has the same flavor of a of a saf squeeze but um but
yeah I always think of it as sort of peeling off a layer um so what we want is and in fact if we had uh Arc unit running
it would tell us that this test violates hexagonal architecture because we have code in a domain that is actually
accessing the application layer and that's not allowed and I know we have a should we bump it up no I don't necessary um
what we want to do is now uh so if we um so I'm curious what would happen uh let's go look at what is the song service
Constructor do so let's just bring up a preview of that contr shift I um yeah so that creates the Searcher and the
repository we don't actually need the repository so uh so we can pretty much just um instead of creating a new song
service create a uh we'll create a Searcher uh no we want to use one of the create oh um so we can use that one and then
just pass it that new song so you can pretty much delete from the where you were to to there so if you move the cursor
over one one to the left no no no no one to the right right there okay down your shift key and go down to no uh when you
say down to what does that mean uh pull down the shift key and press down arrow twice and then left arrow and until you
okay uh and now we can replace the red song service with song Searcher but we'll have to assign it to a variable so let'
s do that Y and it's just going to be by theme and that's it uh we expect this to pass because the work of the the stuff
we were modifying was actually in song Searcher so this should tests excellent sweet so we can now delete the test at
the other layer because this is right commit yes okay yep all right and so now when we go look at our Jura we can say uh
add a song with multiple themes um I think we can now say well we don't need to write it against the service layer this
is just more at the uh domain layer and so we can write our test at at right happened you're scrolled horizontally yeah
I figured out what it was yeah I'm like what where the where did the cloes go yeah exactly all right new test yeah new
test okay so now we're back be so here we're going to add multiple themes oh with multiple themes or with single back
themes I don't think there's anything we need to write because didn't we just do that up above 66 yeah yeah I'm like yep
and so um that me you find that that that um what you said earlier you were calling it um you know do you implement the
fine before the ad the query before the command so do you find that often ends up with oh we just implemented the uh
sometimes what it points to is is why did we get that for free um we got that for free because we changed what a song
was and if we look at what is the interface that song service provides it's add song give me a song so its structure
didn't change it's already on the screen hi there he is um so that didn't change and therefore there's nothing the song
service was not involved in the change basically um and even song Searcher uh and song Searcher was involved because we
changed the structure of song and then changed how we index it um and then changed how how we uh we had already been
able to find by multiple uh themes and basically the the the by theme Finder right the song Searcher by theme assumes
that the data was indexed properly so we just changed how the data was indexed we didn't touch how songs were were found
and so that's why we got that for free great my theme was where are you I mean Trivial it's basically it assumes the map
is correct and so the hard work was map sweet we got a freebie yes so yeah see now folks if you had estimated that you
probably would have given it some point value that would have been uh way overestimating how much time it would have
taken of course we didn't we don't have full top to bottom capability because we don't have the ability we don't have a
UI for this yet um right but but hey there we go all right so what do we do next well we could start moving up to the UI
though I do know that ultimately we're going to want more attributes for a song but right that's not particularly
complicated unless I'm missing something yeah so I think we uh yes I think it looks like our three choices is UI uh
flesh out the attributes for database I like the idea of holding off on persist until we really have everything Upstream
um fair we could do UI just to start having a little bit of something um and then add attributes as we need them or not
as we need them but as we decide we want them right or we could just dive into attributes now without and then we just
have well I guess if we did the UI then we didn't slice adding the attributes one at a time so it would be less of a big
bang well I would probably say unless there's something special about the other attributes um we'd probably just add
them all at once yeah let me take a look yeah because You' written them down here what the other I think there were only
two others oh um that was like an initial this year yeah theme artist song title um release title which would be like
the album title or the single title but there's what else do we got beside that um yeah type I don't know if type is the
right word for this compilation or soundtrack let me look at my spreadsheet do I have format I don't LP 7 inch no DVDs I
don't pull music off of DVDs but um is some people like the term some people call some things EPS which is you know an
extended play right um but is that you know now we're getting into how much do you care yeah like this one's physical
format right versus I don't know what you would call this other one uh conceptual I don't know what the right um yeah
yeah I don't think I care about and would you say LP or would you say vinyl right because what is right what but then
vinyl it's like which vinyl right 10 inch 12 inch or seven inch well so I'll I'll remind ourselves that that we're not
coming up with the grand schema to and all schemas we are we are focused on what do you Mike Rizzy DJ need list you just
have persist you probably yes IGI we probably assuming we retrieve from persistence um and display it then yes we would
we would definitely want to because security by obscurity at that point would not not good enough no um hold that
thought while I go um label I have it in some situations there might be situations where it version you know Verve put
out different version than clef right and so it sounds different right um I'm looking at my list here scroll through the
spreadsheet um okay and then I think then after that we get the pile of themes and then this is where it gets to yeah
we're talking now um band cam Spotify Etc right and then to lyrics which could be useful since it's about themes and
you're like oh well why does this song that of the title that seems like it's nothing to do with Christmas is about
Christmas and then you look at the lyrics and you're like oh that's why um is that valuable I don't actually keep either
of these links in my current stuff but I can see it as a future value ad again we should add it when we yeah so I I wan
to I want to restrict your thinking because you you you you've veered off into future and I I want to keep us focused on
on what do we want right now what is the minim minimum as somebody said the other day what is the minimum lovable
product for you right the reason I went here was you had asked the question um are there any unusual things that could
could make life difficult and so that's why I went through them I forget how you phrased it but something along the
lines of um the fact that we could have a song is actually themes plural right that right caught you by surprise right
when we first started working so I wanted to kind of go through these not to say let's Implement them all now definitely
oh then I you you misunderstood what I was asking I was asking for the stuff we know for the minimum lovable product
right that's our that's our Focus right now um there anything different about those attributes that uh would force us to
store it in a different way uh or um handle it in a way that's basically something other than a string so for the top
four so we got themes we've got song title for artist uh and maybe release title I don't know if you even want that in
your minimum level product um but for those are those just strings yes okay in which case I would say let's add those uh
and then we'll add them to the UI got it okay give me a second to just look at the other ones to see if there's anything
that's vital I don't think so actually I think I do need this one so the reason is if it's a if the title is you know
songs of Southeast Asia I can figure out inference okay but if the song If the album title release title is not that's
the only place to find that song which is somewhat common for certain themes you know um so knowing whether it's a comp
compilation is important okay and then the other one I think is also not minimum but DJs will appreciate it when we get
to it and that's going to be an interesting one I just forgot about is friendly and that's not going to be a Boolean I
was gonna say I please please make that not a bully no no it's GNA yeah there's no way um yeah that that one's a huge
can of worms notes um so I was just looking at the schema org to see if they have any what s of what they're using for
things that are that are like your what what you've question marked release type um they have production type so
soundtrack live album studio album uh is what they put under where did you find that you uh go to schema.org musicalbum
and I'll paste that here for see I'm guessing there was a here I'll just share it I just shared it oh okay or you can it
doesn't matter mine or yours yours uh so they have this as music album production type um so it's either compilation DJ
Mix demo live mixtape Doo interesting oh you hit it by driving in yeah so so the schema I search for compilation it's
not there yeah so so so this is the schema for music album um which has these properties so by artist release and
release type uh and and production type um but it pulls in uh information from other parts of the schema like creative
work which is all this other other whole bunch of other stuff copyrights and material and publisher and stuff but we're
really mainly I'm I'm was interested in looking at is sort of um how can it help inform form our stuff because right
whenever I'm struggling with like what the heck do I call this thing uh folks who are who whose job it was is to create
ontologies like this uh probably thought about it a bit more um so that might be useful yeah that's a very odd term
album production type yeah there's oh sorry so so basically you can look at like you know where did this come from it
came from uh this music ontology schema um how did you get there under did you back so it was basically under
acknowledgements no but how did you get to the screen you're currently showing oh where I am right now uh I clicked
through music album production type which is the TP ah okay I was clicking on album production type to its left oh
interesting my screen is not red it's clickable uh oh that's interesting yeah um so that's the name of the property that
you would find in the schema uh and this is its type so all properties have types fascinating yeah wow yeah I'm not do
some deep diving in that offline anyway back to your screen um so so I don't know if that helped with release uh not a
fan of it but that's just um I think I want to kind of STI with the release type for now and then make a note that's
fine I was gonna say let's it sounds good um so are these our our our five song yeah I would say these will be these
five all right then let's let's work on adding those okay so again we'd be at actually would we go outside in and work
at the service layer and um or start at the Domain layer and then it's all it's it's all dependent on song So this this
doesn't at least right now this this doesn't Force us to change anything outside of song so I think we just we have to
do uh who you know who's creating songs because we're probably doing that in a bunch of places we already have some uh
alternative Constructors um and and we might uh we might want to go um we could we could probably do one more backwards
compatible Constructor um so basically uh right and we were going to reverse title and themes swegi oh yeah let's uh how
about we do that run our tests commit and then um I think we can get rid of the other Constructor by inlining uh sorry
by pushing out uh but let's do one thing at a time let's change the order of of title and themes because I agree is
there way to we can do the um you can do change signature yeah that's the best way to do go safe uh so says uh you chose
Java spring boot as your career path well good luck to you I think I think it's a solid Choice um definitely spring if
nothing is is becoming more popular and uh so so well done uh full nul says what's the recommended number of Constructor
arguments fewer less um my my rule of thumb for for this is uh is the same as as it is for lots of things which is uh
several in other words three or four maybe five beyond that uh you really need to start creating objects that represent
a lot those pieces it's very likely there so I I often see two different kinds of long Constructors um one is you simply
have lots of little pieces of data uh in which case you want to start grouping those together we're probably gonna when
we do this next step of adding properties to song we're probably going to push that limit and we're going to start
wanting to think of is there just release as a value object that has title and type do those go together um and some
other combinations of attributes so you sort of have this tree of tree of attributes so at the top you've got three or
four and then each one of those is made up of smaller bits that go together you don't want to just randomly group stuff
together right so that's one type of place where I see long long Constructors uh the other type is is generally service
class service like classes where you have a lot of dependencies of because that service is going to need to access these
three repositories and these two other things and these four other things in which case your service class is too up and
then easy peasy and generally you you'll find sort of a seam where it's like okay these methods use these dependencies
and these dependencies use these dependencies and they just split the class apart just it it it it it generally will be
you you if you can find the seam then it will be a relatively straightforward refactoring if there's lots of mixture
then you have to really rethink does all of these things really require all these dependencies in which case the
dependencies themselves might be too granular uh and so that's another problem is like you've got eight different
interfaces and they all are because everybody's thinking about the uh interface segregation principle and small
interfaces that doesn't mean that they're all one methods it just means they need you also have to consider cohesion and
so if you're always using dependencies a b and c and ab and c and ab and C well again maybe that should be one right so
since we are going to start hitting that limit should we will there be a point where we're like a record no the record's
going to always provide value even if it's four or five yeah I would say let's let's add what we need right now we can
refactor I don't have a problem with with with five per se at some point we'll we'll start seeing how how those will get
broken down yeah and it does make sense that these two will go together yeah uh yeah please what were you gonna say I
was gonna say what do you think we should do next so I think and I don't know if we can do this if this will work with
the record but we can try it so let's try um uh oh let's do a commit because we reversed theme and themes and title and
then step okay all right so let's see if we take list. of theme on there on line seven that no well uh that yeah I want
to introduce parameter yes awesome um let's call that themes not theme one but themes themes plural yeah but not themes
not themes one yeah just themes and then hit enter now totally fine we've got duplicate Constructors we can now delete
this Constructor ah one more uh you have an extra closing brace oh yes uh let's run our tests want to do all or just IO
free uh if it compiles we're good yeah that was really all I cared about all right um yeah because because uh what we
did was basically say hey everybody stop calling the Constructor that takes a single theme uh just do list. of uh and
then became a duplicate and then we got rid of it yeah it' be nice if intellig was aware of that it's like oh we've just
created a Constructor that looks exactly like the one that's already there do you want me to delete it uh but no that
requires a little more smarts on our part so that push list. of out to the callers yeah so now if we look at all the
references to this record we will see a bunch that have list. of in it most likely in the tests not elsewhere yeah yep
tons of them y um so if we did the same thing with chain adding it will put a default blank string well so what do we
what so so I think that becomes a teston issue and so I think we now need to basically encapsulate our setups so uh
eventually this might lead to a song test Builder or test song Builder or a song test data Builder anyway um it might
eventually get into some kind of Builder pattern where we care about some attributes and don't care about others but I
think we can James uh so want this I just want to address this question very quickly Raja asks what's my opinion on
clean architecture um I prefer um hexagonal architecture but the ideas of clean hexagonal or ports and adapters if you
want to call it that uh or um they're all about separation of concerns around IO and domain if you don't have a strong
non-trivial domain don't bother with any of these they're Overkill uh so make sure it matches the kind of application
you're you're developing but if it does match if you have a a complex a non-trivial domain and by domain I mean lots of
business process rules and such uh then any of those architectures are fine I happen to prefer hexagonal because I like
the way it splits um the external adapters uh but I'm fine with all of them and I talk very specifically about the
differences between the different kinds of testable architectures in in my course uh which at some point I will reopen
for sale all right so let's um let's go to our tests and start encapsulating the places where we're creating songs uh so
that we can make it easier so that we don't have to change a whole bunch of places where we're creating songs and where
we don't care about these other attributes you want to start with themes controller test or service test uh I think we
should start with the service test I don't know why I have no reason coin is valid some well other than the other than
the one that I think that had the most yeah um so uh I knew this was gonna come up so so no most CR apps actually have
quite a bit of domain Behavior they're just scattered all over the place um but if there is no Behavior right if you are
literally or almost literally just editing stuff that ends up in a database table um which is a completely valid way of
creating applications so if you just want an application that for example made it easy for uh a hundred of your closest
friends to to give you their top 10 list of songs for the year and you wanted to create a special application yeah I
might do it as a pure crud app it's almost directly putting stuff in in a database table um and I might do some minimal
validation like make sure stuff isn't empty but other than that there were no rules uh then you would not use an
architecture like like clean or hexagonal if however you start having restrictions like um you can't have more than 10
songs in your list uh and your songs must be have been released in 2023 and they can't have and they must all be radio
friendly and right and all those are now starting to be domain rules and domain logic where you're going to have to
interact with external services to get information um and then scan lyrics and if you start doing that now you've got a
complex uh non-trivial domain and then you're going to want to separate your domain from uh from persistence and from
external services so for me it's all about testing um if I don't if there's not much logic there's not much testing
there's no point in testing code that that does for example an assignment it either works or it doesn't you either
mistyped in which case it wouldn't compile or or it doesn't work but the minute you've got an if statement you want to
test that and if you have a lot of them you probably want to consolidate those I sure hope it does make sense so thanks
you makes sense to factoring are you waiting for me because I was gonna let you do this oh um so I mean I can tell you
what to do but I think it yeah so what we're talking about is having um creating uh Within song Some Factory methods is
that what so uh thinking set up at a higher level yeah so um the the way I think about this is uh and I'm gonna I'm GNA
draw this so the way I think about um situations like this where I've got objects I want to create uh from tests where
there's they commonalities so the first thing I start out with at at the uh Factory method inside of the test class for
example inside of right of course it wouldn't be in song that was silly that's fine there are cases where where we do
want to put stuff into into the class but in this case uh so it might be inside of song Searcher test and there's going
to be a method called create song and what do we care about sometimes we only care about the title and then sometimes we
care theme then sometimes we care themes and for convenience from the test point of view we might might want to make
that our ARS even though the record itself takes a list we're writing these for convenience for our tests right now once
you if you if you project this out you start getting well sometimes I care about the song with not snog uh sometimes I
care about it uh I don't care what the title is um but I do care about the artist and I do care uh that it has one theme
but sometimes I I I actually care artist and a single theme and so you can see this um this you keep going this way and
you end up with uh dozens and dozens of methods and each time you add add an attribute you end up with more methods and
so exactly the solution to this is don't do this um the solution is is is once you pretty much in my mind kind of hit
this point and go once you go beyond this maybe this uh you're probably gonna want to go to a test data Builder um but
before that so this is Factory method inside the test class uh the next level up is Factory methods to a separate class
that's uh for sh sharing across multiple tests right so up um but then pretty much beyond that you're pretty much going
to want uh a Builder and so this is my hierarchy for how I think about refactoring tests I I start out here um make it
available to configuration and the important thing here is with lots of uh with attributes I don't care about right
right so in other words good basically false if you're not going to specify it so um I mean that's generally true down
here but here it's where you're really mixing and matching a lot a lot of different things uh and yes absolutely as uh
Luigi correctly observes once you exceed several um and this number of like three to five you know doesn't just come out
of nowhere it actually comes out of how our uh our our brains are structured What's called the cognitive architecture
and this comes from cognitive load Theory um which is we can generally juggle in our heads three to three to five things
those things might be very complex things uh what are technically called chunks um and experts can handle more complex
chunks than novices uh but you can only juggle three to five of them anything more than that you start mistakes all
right so uh we're we're we want to get to here first basically create some Factory methods and then we'll probably
extract it and move it to to to a separate class for use by the other test classes so back to you okay so here we're
adding two new songs to the service here we're adding one so I wouldn't bother searching I would just start refactoring
okay because it'll be it the intellig will do the searching for us got it so the question I have is would at this level
yes or at the so it's the song creation part we're worried about right we not worried but attacking that we are
concerned with it is a concern yes method I'm not digging it um I would say create song even though it's obvious the
return value from the call site it's not obvious what it if you just left off song so I generally do create song and it
whoa now here's where HJ is is going to offer you know if you parameterize this uh I'll be able to replace a bunch more
duplicates um the reason why I generally don't let it do it is because the suggestions it uses for the variable names
are terrible terrible like and actually this is worse than I've seen it I don't know what the heck it thinks it's doing
with those variable names um it could be there's some configuration in your intellig that's different from mine but I've
never seen it offer this will be our year with uh underscores with underscores and uppercase yeah case so we will keep
the original manually uh and we will replace all the occurrences where we don't have the need for um because we have
literal duplicates so uh go ahead and replace all song and push out the the title and then the actually don't need to
select the do I I just need to be yeah just need to be in the string yep let trying to do it again well that's that's
what select this is what I would have expected it to do I don't know why it was suggesting that other monstrosity um but
we can be title and now it finds duplicates where it can say oh that now that the title's parameterized I can replace
those we want to do all um and now we can push out uh The Single theme uh oh yeah oh could this be directly yep
parameterized okay then yep again all so now basically as we introduce parameters the the method becomes more General
and it can go and replace more of the callers which is why we which is why I stopped you from searching because intellig
is doing the work for us right right right no appreciate it okay fired all all right and now um we probably have a place
where uh we so now we can look for in in this song Oh besides there are we ever calling new song um I would just
honestly I would just actually do a a search search yeah oh nope uh turn off your regular expression which is that dots
dot yeah yeah yeah so we got that one place and that's it that's itet so we've captured them all as they say in in
Pokemon them uh so that's it so we can basically take that static method I um we could move it to the bottom although
it's probably goingon to move elsewhere soon anyway but let's go ahead and and move it to the bottom yeah I don't think
it's the AI assistance I think it's it it just I mean maybe it is but it's not using the AI assistant because we don't
we're not paying for it um so yeah I think it's just a weird Choice thank you and it's it's odd because you'd think that
if nothing else the humoristic for what it suggests I don't know if you noticed when we first extracted it down in the
list near the bottom was title and so if it's going to suggest basically what's a generalizing of the method why would
it not suggest the general name which is the the the name used uh inside of song right why would it use the most
specific thing instead of the most General uh it to me theistic is is is obvious but they're using not the right istic
all right uh let's run our tests I um do you want to tackle the ones in the other test class yeah I just realized that
we could have saved ourselves a little bit of time if we had moved uh oh outside of the class if we class it would have
searched the other ones U actually I don't think there's a way we might be able to to to force it with a process
duplicates uh let's commit and then we'll we'll try that out um no well I'm wondering why we have so many changes did we
not do a commit before for something can you look at the difference for the song themes controller test oh we when we
swapped the order we didn't commit we didn't commit for that yeah all right so let's make sure we note that song uh and
I'd be more clear that uh uh song Factory method for tests good point commit uh so uh tiny tangent um I personally have
a setting uh in intellig where when it shows a diff it opens up a full window instead of trying to stick it in an editor
pane because annoy because I find that to be again sort of the worst possible default like you're gonna stuff it in a
what's potentially a small window instead of just popping it up um so that's I don't think it's here I think diff um it
might be under different merge they're under that do something like it's so funny it's like I understand int you don't
want to change defaults on folks so you end up with a default that's what it used to be and then you introduce the new
feature and you don't change the default uh I don't understand that part like you clearly introduced this option and
it's still what I think is the wrong default but what do I know I'm I'm not jet brains they hopefully they collect data
and and see how how many people uncheck that thank you I will be less annoyed by those diffs for sure all right uh yeah
because I I don't use them often but when I do I want to see the whole freaking thing right I want to see it to be the
big screen all right um so yeah so let so let's now uh um I'd like to see yeah let's go to to the song themes controller
test but I'd like to see if we do refactor or is it code I forget which menu um where did they hide it um maybe it's
under refractor what's what are you looking for looking for um duplicates where did I see yeah there it is find and
replace code duplicates in the second block ah there we go let's do that okay is that enough well no to go check well
it's right now it's specified to just look at the current file which is song controller test and that's what we want um
let's try that one more but let's expand the scope in which way I mean go to the pick oh that uh so that scope so click
a whole project what because it's clear where your cursor is is a duplicate um I wonder if uh if we go to S maybe it's
because it's it's not available from here it's not public can we go back to song uh oh right right service test is that
where it was yes oh it's private that's why so let's make that public okay um and in fact let's go ahead and move it to
to a separate class in that where it's going anyway um so what I generally do here because I don't want to type the
entire package name is I type the name of something that's already in the right package Factory get rid of the word test
and get yeah and then yes the rest oh wait actually that's fine it's already yep that's good y the class uh and that's
in the right place yeah for once well because it's in test it's always right it's in test it's the other one that's the
problem it's like no yep go ahead um so let's try the the the duplicate codefinder again and it's yeah Vector not really
that's a real bummer what the heck's the point of that thing anyway include test sources yeah there's nothing extra we
could select that's a bummer all right um so uh have to manually swing sling them well so what we could do is we could
do the same refactoring we did before um and then the final step will basically be uh uh move it and then delete it I
don't know if there's a better way H uh we're trying to find just duplicates uh we're trying to I was hoping that um it
would realize that where we are now with the new song list of theme that that code is a duplicate uh of the code that's
in the static method that we pulled out to the factory oh but wait a second so far we've got the factories for a single
theme was this one now these are single themes too well so it may not realize it's a duplicate because of the list right
um so let's do this let let's let's pull this out uh so let's let's do an extract method on the the new new song
creation okay extract to what uh method method yeah and we'll just call create song that's interesting oh because theme
is a variable that's why okay that's okay keep original yeah keep original doing uh and then let's go to the create
parameter yeah title right yeah yes and what's that yellow oh that's been there that's this just a cast check that we
don't care about um so let's uh let's go back to the method um was it title theme in our song Factory the other one let'
s see title then theme yeah okay let's swap it in in here and uh don't we need something to drive well I'm wondering if
we can do the process D if we can try the process duplicates yeah interesting the name of the um yeah they must have
changed that because it used to be called process duplicates uh project yeah now be made public uh interesting is that
it's going the wrong way because start it from the other one uh would that do it actually we would start from here so
let's go start from here so hit cancel yeah cancel that's what I meant start from yeah let's start from here and and
process duplicates and I'm just going to keep calling it process duplicates because says yeah so now um I guess I was I
was confused by what direction it was looking to process duplicates for uh now I guess I know better so IGI was was
right yeah um so yeah so let's go ahead and and uh and yeah do Let's do let's replace one by one yeah let's see what
this one too and yes uh let's do that one and we'll just inline it well it's now jumping to now it's jumping to uh which
is because we said whole project instead of right restricting it so let's skip this one and we'll skip that one and that
one good thing we didn't yeah uh so now let's um let's go inline inline that method yes all right so let's go and look
at the colors there what other changes are there there is it oh there it is yeah so you can always tell by the gutter
being blue tells you where the where the changes are that looks good yeah only two places in this file and so uh if we
go to the song search by theme test we should have replaced those as well yep yep that's it all right uh let's run all
our tests and then we can commit totally yeah that's that's um unfortunate that it would suggest making a change that
could not compile or should not compile or mean having production code used code yeah well because that's what it end up
being right would a compile but it would be really bad yes yeah you do not want do not want commit let's try it our diff
just to make sure oh yeah the window pops any particular file do you care uh let's one yeah there we go and I just
there's an also a right click show diff and new window yeah but that shows it in a new window uh is this a new window oh
maybe on window on Windows no pun intended uh maybe it does that on the Mac it does something different let me see what
this one does so they're synonymous I guess that would have overridden our previous setting if you wanted to do that on
occasion this's a shortcut key right control D you could just hit control D D um cons I guess finished um consolidating
the factory methods we didn't just finish we did we do both in this one commit we did uh you could look at the song
service test to see what we did there not yeah wrong one yes so we created the factory for both yeah so now we've we've
uh created Factory class or refactored uh refactored all class okay uh do we call the Constructor I'm sure we have a
place where we call the Constructor with multiple themes right you would think is there a way to search it other this uh
if you see the gear where on the upper right where it says usages um usages would help but it won't tell us new I forget
what the way to do that is uh cancel out of that okay uh let's do search again I'm clearly getting tired um uh control b
control B yeah yeah yeah okay find usages uh so that so you actually committed that selection oh interesting I hit
Escape no it's still what changed oh I don't know what changed because I did not so control B does what now now it's
showing seven what uh well something changed yeah but what changed that's what's interesting because these are the same
project files could it be we were looking at song else well does it get does it give us what we want uh it which is
where where do we instantiate a new song and uh it's yep um oh that's the startup sorry I thought that was a test my bad
so let's go back here control B uh I don't I feel like we're not seeing everything yeah because didn't we test multiple
themes yeah let's let's do a literal let's do little literal search for for uh across files for um so we went on across
file search I forgot the shortcut for that it uh it's finding files control files yeah control shift F so let's do new
print um this is this whole word that doesn't that doesn't matter matter what we're looking for is that last test the
last entry that one right okay right so that's that's where it's calling the Constructor with a with an themes um so the
only one we haven't encapsulated the setup on right and so let's let's encapsulate that set up want to call it create
song or do we want to yeah create song it'll just be yeah and then we want to do the list first or the uh we want title
title theme so let's extract title first and okay yeah you got the title right that time well in that dialogue it gets
it right in in the uh suggestions for introduced wrong yep so now would we push it will we make it public and then push
it to well if we push it it'll escalate it to public right uh if we yeah yes it will so let's Factory all right um make
it a little bit easier to that's totally cool um let's run all our tests y oh oh it is all that's what you had yeah all
right have let's have line 11 basically call 15 no nope I want 11 to call line oh sorry sorry no we're in the same class
oh you don't need do anything yeah yeah yeah got it that's it oh so static you don't have to do it if you're in the same
class the only the same class yeah yeah because you're in the same class there's no there's no ambiguity right right um
the reason why is is this means now there's only one Constructor call to new song in our entire test uh set of test
classes right so fully encapsulated so we've fully encapsulated the setups now whenever we expand the song record
there's only going to be one place to change it in our uh in our tests and we can prove that by looking for new song in
our tests um but I'm all what I guess that is but why is only right commit let's commit actually let's read uh let's
just run the io free tests too late I'll get back to that yes yep so I think let's let's uh write down the the specific
next step and sounds like we probably want to stop here yeah I'm starting to get toast um would that be I guess it would
be a sort of T new category which is fine we foret what the caty oh I guess you could say add yeah I can put in with so
we've already got so we want to add artist m uh release time uh oh sorry you want did you want to delete 39 and 40 there
since we don't need that anymore oh because we were just yeah there's a lot of stuff in here that I gota go clean up but
yeah all right so we have um we've done a lot of preparation work but one of the nice things about all that prep work uh
it's always I always think about like making a fancy dinner it's like once you've cut and sliced and and done all the
spicing of everything it's like then it's easy you just throw it in the oven you wait yeah um and so now that done the
the the harder work of of encapsulating our setups now that when we add our attributes the only thing we'll have to
change is that one method um and then we can start worrying about places where we actually want to specify other of
those attributes um and we will create additional Factory methods and maybe or maybe not next time but probably at some
future date we will probably want a a data a test data builder for for song right but but we'll see we'll we'll create
it when we need it agag me and probably do UI after these yeah and so I think yeah I think creating the UI will be will
be the next step for for that yeah cool Al righty how long do he go went for two and a half hours okay so That's all
folks thanks a lot again for for hanging out and asking great questions and again as always uh you can find out more
about me at ted. slab um and I invite you to join our Discord uh and participate if you haven't already done so if you
have questions about the stuff we did on stream discord's the place to do it there's a dedicated channel for that uh if
you have questions about some of the topics that came up such as like architecture uh or domain driven design or testing
there's channels specific for those topics as well uh so that's all uh and of course the Discord is where uh the best
place to find out when um we will be scheduling future streams always announce it there and it's the best way to find
out basically instead of being notified when we actually go live so you get a bit of advanced notice uh if you join the
Discord and make sure if you want to know that and you want to get notified there is a special roles Channel um that you
can click on a on on an icon and you'll be notified uh with a special notification when I announce uh the next stream
that's it any any last words Mike no good thanks that was fun all right so we'll see you next time uh otherwise have a
great rest of whatever day left for you take care everyone
