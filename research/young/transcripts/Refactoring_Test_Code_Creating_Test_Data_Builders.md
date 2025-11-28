# Refactoring Test Code： Creating Test Data Builders

**Video URL:** https://www.youtube.com/watch?v=OJhHdLdDE-o

---

## Transcript

hi my name is ted m young and this video is extracted from my twitch live stream where i refactor from test code into
test data builder and the reason i do this is because sometimes the setup part of a test can be pretty verbose and often
repetitive and in this video i basically take existing code and refactor my way to create test data builders and show
both how to refactor it and how the end result makes the code and tests much more concise i think this is actually a
good candidate for for test data builder so what i want from a test data builder and you can already already see even
though this is nicely isolated in the factory um is i've got sort of different configurations so sometimes i specify a
repository sometimes i create one automatically a lot of my projects actually run jitter ted so all my classes are
taught under ted young but a lot of my the stuff i do on stream is under jitter ted so those are probably the more
interesting ones other than my kid bank which is still on ted young someday i'll um and there that gets you right to
this project so what i want to do is i want to be able to if i don't specify anything otherwise go ahead and create a
new memory repository um if i don't ask for an id i want to be able to either build a member or i just care about the
member id so sort of lots of variants both on sort of incoming parameters right sometimes i specify roles sometimes i
don't uh sometimes i specify the id i don't think i always do that maybe i want to generate it so let's take a look at
this see how it's used yeah i'm laughing because it's like oh look at that the way i do tests it's it's almost always
sort of the core domain stuff are real objects and that's why they're actually a little bit painful to set up because a
huddle in order for it to be valid it's got to have an id so for me the test data builders build real things where i'm
able to substitute one thing for one thing or another um but i'm almost always creating a real huddle uh you generally
don't at least i generally don't i don't test double all the other stuff repositories um basically any ports and any
ports are what i i test double otherwise i want all pretty much all real objects they may just be pre-populated is that
what you were asking um now i'm not sure uh so some of this i've already got the huddle factory for so that'll save some
time uh custom queries will wreak havoc on on a repository fakes yeah if you're if you're getting into custom queries i'
m not expecting my fakes to to emulate those but that shouldn't be a problem from a test-driven standpoint because you
basically pre-programmed the fake to return whatever to return so you cust you you hopefully know in the test what query
it's going to run right is it going to run the show only available huddles in which case i'm only going to code in these
are the huddles because i'm not testing the query the query especially i mean unless i'm not testing a query against
indirectly if i'm concerned that the repository that maybe i don't understand the repository implementation or either
sql or object like sql then i'll write tests against the directly against the repository and i don't have a lot of
custom queries yet at least in this app all right so what i want to do is here yeah if you've got any of that kind of
special stuff you want to test that directly against them against the repository implementation uh and then you can just
assume it works in other tests and not to worry about it um let's uh let's this way okay um so in this case the reason
why i'm passing this into the uh because it's passed in here as well so it needs to share so swap those does that still
work the reason i swapped it is what i can now do is when you have a test data builder it also has state and you can
actually query hey can you give me the the member repository because i'm going to use it to build this other thing
eventually i'll i'll assemble multiple test data builders so that i don't even have to sort of pass things around so
what i want here um what i'd like it to look like is member id member id equals new member builder i'm going to assume
it has a default repository for now i'll basically just give it all of this i don't think i care about the i'll grab the
id separately yeah with that oops um so build will return a member and then yes and and then no or builder i'm surprised
it did that this is get username and this is email do i reference this yeah i reference all of this information now i
could split out so it'd be with first name with github username with email and for the other stuff it would just be
defaults for now i'm just going to do this and then i can expand it as as needed and now build is going to return a
member why do you think i'd be uh actually this can call the member factory my assumption is it's going to put in a
repository so it should be saved so we'll do private final member repository and we'll default to an in-memory one so
we'll create a member oops that's where the pi came from option p i was wondering it's like what key typed that uh i
want um so we will do number equals and then we will return uh so member builder is going to be the more flexible
version of member factory eventually i want to get rid of member factory uh some i'm basically sort of driving it sort
of through what the test needs from uh from the builder because eventually i want to start building up builders pun
intended um that are that are more sophisticated and eventually because i want to get rid all right so this uh we will
create a create a field for and that should be um okay and number uh female email no no i don't think i need to make it
generic um i don't think there's any generification that needs to go on here it's more um a huddle with this link with
this date and time actually a lot of it'll just be default it's like create a huddle use defaults uh create a member use
this information and then i can start then i can pull the huddle and the member information out as i need it if
necessary i can pull out the i can have a create a huddle service i can have a create the member service so all kind of
the the connecting stuff gets gets done all right so this should be the equivalent other than oh right so it did not put
it in the repository in the same one um so now let's let's inline this let's take this out and we're going to actually
get the member repository from the builder so we're going to hold and then we'll get this all right and so this is one
of the things that i had a problem with is sort of this service is using this in-memory repository and then this other
service was using a completely separate in-memory repository um i mean to a certain extent like there's an aspect of
sort of building a uh a dependent not not quite an inversion of control container but kind of yeah exactly um mainly
intent but there there is a bit of an aspect of that yeah because like it's holding on to the things that i but very
much customized for for me so for example like the spy email notifier i don't want to build that separately i want to be
able to get that from so let's go now whether the member builder is the maybe maybe not i'm thinking maybe not because
this is more at least everything around member is now coming from so it's not like it's i mean this is uh so i'll be
honest i don't answer questions that you can google if you want to know the difference in java javascript you you can
find that out happy to answer higher level interesting questions but if you can google it uh uh i'm not gonna answer um
yeah so i so don't ask you so now i need basically an another builder one that deals with huddles that may then um but
let's uh let's look at some other tests um yeah that should totally be static at least yeah i don't know why that wasn't
static and tests so let's look at the registered members test here's where so there's this tool i forget if i've
actually shown it on stream i actually did a video of it uh called open rewrite and what it does is um in a sense
refactorings and als and things that are not refactorings but also uh are sort of global changes that you'd want to do
so an example would be i want to update all my tests from june at 4 to gene at 5. some of that stuff is fairly
straightforward just replace junit with you know whatever the package for junit 5 is so just swap the packages but then
some of the other things like disabled versus ignored um some of the parameterization so there's a bunch of things that
you'd have to manually repair but it's mechanical and so what open rewrite does is is it's a way of describing those
mechanical changes uh but not as a search and replace so not text based but actually understanding the structure of the
application um i don't know style cop so you can do things like i actually used it in the video i did on which is on
youtube to upgrade an old spring boot 1.5 project to uh to his current spring boot and it had to apply the j unit
changes and then the spring boot changes and a bunch of other changes and uh it had some some errors but most of it
worked and it was it saved me a lot of um and so uh it would be great to sort of do it would be nice if there was like a
hopefully they'll get there where you can sort of quickly write a plug-in like i want to replace all my member factory
stuff to use the builder but it's a you could maybe do it as a search and replace if you're fancy with a regex but you'd
really want to do it at sort of the deeper structural level so um tilted if a job advert to ask for a degree would i
apply anyway a computer science degree then yes i would apply anyway i don't think anybody should have in their job
requirements a computer science degree at all there is nothing you get from a that anybody should be putting that up as
as as a requirement um you will find that among companies that that again are mostly recruiting is run by their their hr
uh and they don't know they just by default oh this is a professional position you must have a degree yeah gamesman
doesn't have degree i have a degree but these days and and i've hired bunches of people dozens of people who would well
maybe not dozens so probably interviewed dozens if not hundreds who didn't have a degree made yeah i mean it is it is
the degree does not all roads lead to why i think computer science degrees are awful but uh on this stream but so i
won't go there but yeah you don't need to agree go ahead and apply um anyway so let's go replace this with um using our
builder so uh yep so here is a case where now i need to expand the builder uh to so be very tempting to have the builder
have another method for with member uh that took a variant of the arguments but no now i'm gonna break it down and say
okay now i want with first name with username and so on so let's split this so it's basically with first name name and
then with github username of that and then i want build so let's go create this that and then this gets converted to
with first name first name this will extract actually as a method with github username and this can be public now and
then accept it returns member builder and this and this one we can also extract to with email and that works um whoa uh
yeah nothing more for me to say okay so now we should be able to delete that get id so let's go that and that so if we
run our tests they should um so first of all a couple of things about about this this way of doing it it's technically
more verbose than it was before but i think it's um more clear right with first name with github username so in a way
it's it's it's being able to apply sort of name parameters but then any improvements or changes i make or any defaults i
don't have to i think we can do the same thing here um and in fact we don't care about the first name and the github
username so in fact and then we can get rid of this oops not we have just the essence of what in fact i might just do
that uh and so then we need we can just do that that should yeah because sometimes i actually need to specify things but
other times i um that's fine i may have to go into the member factory this is now part of setup it's part of setup right
um i haven't cleaned up the the big ones yet i'm basically just dealing with with ones that are um creating members uh
yeah let's go look at this test so here again we have the this thing because we use it to save it and then we use it to
create the member service so let's delete that i should probably have default roles if they're members they should role
user and role number and then when we create the member um oh lectures all your all your methods all your builder member
builder methods are static so how do you chain them you have to show me what you're talking about uh okay so now what we
want to do here is a and that's it so with email whoa um then i don't care about anything else i don't care about the
roles so i can delete that i want them to get saved that'll happen upon build um build member service no take this
extract this and put this in here so this returns a member service wait so let's build but i want to hold on to the
member builder and so this is member service and turn new oops return number service this will get built upon build so
create a field for that and then when we build here we will also say member service equals new member service what does
it say about this no who cares okay um oh it might be overusing lumbar yeah i don't i don't i mean lombok can build can
can create builders uh uh yeah bubble costs um what i'm doing right now is is all these tests work and so i'm just
making the tests more concise by creating some what are called test data builders oh i should actually i know it's a
little late but i may as well uh put that into done and then put this into doing so at least everybody for the next five
minutes knows what i'm doing uh so what i'm doing is i'm creating what are called test data builders to make it easier
to create the test uh so we've got our builder with email now because i've got tests for if they don't have an email
they don't yeah i'm not sure why i had that line so not sure why i had that there okay so already this is smaller and
it's um what's nice is that what's left here is um more concise right i had a lot of detail that was needed because the
constructor needs these things and uh and this thing needs this other thing and it pollutes the test with with basically
so now it's like okay i have a member builder i want one of them to have this email that's all i care about uh the spy
emailer i'll have to deal with um because that's for this but i don't need to know about how the member service got
created it will connect to the correct repository that's what's important so it will reduce the number of times i like i
mentioned before use have multiple repositories for the same thing unintentionally awesome so i think at least i would
say this is way more concise than what this was before nice improvement uh um so new member builder come on here we go
and we want do we care about the first so um we don't care about their github username we don't care about their roles
so we can get rid of those two lines of code um and oops assign it to no so much nicer and this is the so for me there's
two benefits this is the typical main benefit of a builder is uh you don't have to specify everything if you don't care
about it even though the underlying objects need the github username need identifiers um need the roles uh for this test
those aren't important and so now it's showing what's important which is i do need the first name because that gets
specified here and i need the email because that gets specified there right and the builder pattern uses the the pattern
of returning itself while you're using it so you can keep calling other methods on it and then once i build it it
returns the main thing that it's meant to build um so if i go member builder new here i'd have to explicitly say with no
email to override the default that it has an email so let's create that method and we set email equal to string yeah so
here now it's really clear i want it with no email as opposed to i created a member but i didn't set an email and so now
if we look at right there's a bunch of methods this one do i need anymore because i don't care about some stuff so let's
do that uh do we need this yes we need that do we need this no do we need this yes so here we'll say instead of with
member we don't care about that and now uh not in production i mean this is the member builders in in in tests so it i
can tell j plugin that does the dot var and charge for more usage so let's run our tests make sure we haven't broken
anything and so here's a case where we're doing relying on the tests to continue to pass to let us know that we've we've
done the right thing yeah no you know how often i i i have i've been having to have i've had to yeah no even at a penny
i don't think i could um so now that this is no longer used we uh i'll leave the github username even though it's not
currently used and hey we created um we haven't used it everywhere yet of course but we've created the beginnings of a
nice member move this up yeah it might seem a bit odd that it's creating repositories but the in general my tests a lot
of my tests are already creating them and this is responsible for sort of everything around members um unless i'm
testing the repository explicitly in which case uh i would allow you to inject the repository but so far that you know
clearly the tests i've been doing they didn't actually care about the repository they just wanted to make sure that it
was the same one that was used if it were if it if the builder were in because in prod i don't create i don't
instantiate repositories um the tattoo no it's i mean it's a builder builder is a completely this oh this i thought i
said that this member builder is not in prod this is only for tests you can tell because it has a background of green i
am creating realistic members sorry if that was confusing like i'm creating full-fledged member objects but not that are
production objects yeah okay i thought that there was a miscommunication there so yeah one thing i've learned is you can
always tell the background color of the tab if test yeah so by real i meant realistic so that was the confusion yeah um
so there's some facade-like aspects in that it makes it cleaner and an easier way to work with it but it's very much
just the builder pattern which has some essences of facade this code is not at all about the database this code could
care less about the database this is all about um if a member has an email they get they get notified if a member does
not have an email they don't get notified nothing to do with with uh databases here um i need repositories but they're
actually from this point of view they're all fakes it uses the in-memory repository but but all right uh let's run all
the tests i don't see how i could have broken anything else but hey and then i think we're done because it's dinner time
that's right it's late for you right you're four hours ahead um yeah and i'll i'm gonna next time um i don't know let's
see so next time i might work on the huddle one there's still a bunch more places that i can apply this builder next
i'll do the huddle one because i might want to create huddles with certain types of members and that kind um yeah my
pleasure i will probably this will probably go into my the writing that i'm going to do later on so all right uh all the
tests passed i'll go commit created for um simplifying and verifying tests violating what's relevant to the test and
hiding also make sure services are using are all using yes there's definitely um you could argue that why am i building
up all these realistic objects in a test couldn't i just use a mock and check stuff there uh and there are a lot of
cases you could that's but i prefer i prefer realistic objects that are executing the real object code than than mocks
yeah oh knuth books i've got lots of copy of knuth books unless you're really into the math thing i think you might have
other things that are better reads yeah i mean this is this is super reusable honestly the clarification and
simplification is less important than i keep making the pro i kept running into i was using two different repositories
and that was the most annoying thing so that for me is actually actually more important than the other stuff that i get
yeah if you really want the in in really really in-depth stuff sure but yeah i i have the canoes books i can't say if
i've ever read them since college i carry them around from place to place and they're heavy um but i don't think i've
cracked them open since 1990. all right i think that's it i think we're done uh yeah usually it was pretty obvious if i
was using two two different in-memory repositories disconnected from each other um the first time was like huh the
second time i was like wait third time's like thanks for watching i hope that was interesting and perhaps useful to you
if you are interested in seeing more live coding you can catch me on twitch at jitterted.stream you can also ask
questions and find me on twitter where i'm known as jitterted
