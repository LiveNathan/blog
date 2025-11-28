# ＂Song Themes＂ Episode 3： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=ZtWMPT_a_30

---

## Transcript

howdy all right hello folks uh welcome folks to episode three of working on Mike Riz song themes uh sorry we we had to
postpone but stuff happens um I'm glad we I'm glad mik could could resume today and um yeah uh uh where should we where
should we start should we do a quick recap of of do you want to maybe open up jira and we can see what we've done sure
I've got it open you got it open all right let switch over to it okay there we go here's our jira it's called jer. txt
it's really the only jira that I like yeah oh do we need to um get rid of this okay so the one thing we didn't do is
sort of I guess we've got the stories that are on the miror board right and we're starting to have bifurcated
information um I'm wondering if maybe I don't know if you think it's worth streaming it but I could do it after we're
done today copy over like sort of have a section at the bottom you know the stories yep you know yeah I think high level
I think we can do that off stream sounds good we could look at the mirror board password I can I have it up so I can
share it cool me so there we go and so we're working more in stuff I think we are working on this one yeah all right the
Double Diamonds was our Double Diamond right indicator of Story one yeah actually maybe I'm gonna put it right here so
visitor you can't see but I'm typing into jira visitor searches for songs with one page all right so that's our high
level that we're working on right now you think we need to go into more detail um as far as like the context in which
it's living or do folks we rely on folks doing other looking at other streams I mean other recordings I think at this
point we can we can rely on the fact that uh this is a database of songs and we're searching for themes and if you want
more you can go see the playlist and I'll I'll I'll post a link to the playlist yeah so they can watch the earlier
episodes sounds good um yeah sorry go I was gonna say so where are we at so we left off we we created a song Searcher
class that can search by theme and we did we're doing the zombies right so we got zero find no songs we got find a song
that matches a multiple we also did sorry yeah continue I was gonna say uh are our test passing I forget if we left a
breadcrumb failing let's find out R all test and I moved this up to the upper right hand corner y see if that's less
annoying yeah we're all passing great um and then we did some um endpoint testing returning outside in y yeah outside in
uh return model saying so what do you think's next bet you think we should go with back up into this area working the
model or do you think it's um um I think we I think we should flesh out uh finish out the the get endpoint um up through
returns model with with a single song matching okay youo it does feel like Christmas it's crazy yeah uh so we have
returning the model saying there were no results um let's take a look at at the test and then we'll move on to the
generate HTML so there we've got our model and that has the attribute of empty search results and that's true all right
um do we have uh so we've got search result search returns search results view so that um we so is our next test that
empty search results is false is that our is that our next test that would seem to be the case so do well here we've got
HT yeah I think we're missing a step I think so too yeah hey uh full full now full name is pronounce welcome um yeah I
think we I think we need a a middle a middle test which is yeah saying that there are results um single result or do we
I think it's just the opposite of there were no results that there are results at least based on what what our attribute
oh we're doing the attribute it okay all right let's write it the test yeah let's write it I don't think you I don't
think you need me to navigate this part hope not well you know who knows oh I've gotta do you uh search returns model
with song results or do we want to say I think we just want to say where uh search result not empty or something well we
got here with no songs found attribute oh yeah I think we didn't update the test after we renamed our attribute so let's
update that test name and then that'll this one search result returns model with no songs with empty search result s
attribute so that's an interesting design question do we want to just see if empty search results attribute is false I
guess we are trying to do a or do we want to actually have some thing in the model well I think we want to start with so
what I tend to look for is if we've got something that's testing for a Boolean true or a Boolean false we want to always
have a test for something that's the opposite of that otherwise what's the point right um I'm just I'm I'm pondering the
the word attribute in that previous test is that too precise or should we just say with empty search results because I
feel like the attribute is is almost a bit constraining it is constraining I guess the one thing about if we said with
empty search results though wouldn't that imply we were looking well no that wouldn't but the test we're about to write
it might have an interesting connotation I feel like we should draw drop the word attribute yeah I think so I was just W
to think it through yeah um all right so let's go back so this one search returns model with song results now this is
the part where it's uh with non empty search results I mean it is the opposite right and you wrote song results here and
you and it was search results before how do we feel about that I think search results yeah even though the search
results are songs did we I feel like we song search by theme song themes controller we're going to start getting into
ubiquitous language problems aren't we um well one of our verbs that we put in the list was search um the sort of the
noun that comes from that is is that song results or songs f like I don't know how I don't know that we need to really
be too particular about that just yet yeah we could wait till it's more painful but we are going to say search returns
model with non-empty search results let to see if we use search up here we did call it search revols there too I think
we've consistently called it search results um okay I think I'm okay with that but should we codify that in the uh
ubiquitous language with a yeah well it's always the case that the um let me pull that in that ous language is a living
language so we could change it so this would be a verb yeah so the verb is search which results in in nouns um so as
says so the test tests for the attribute and not for no results found uh well test for an attribute called empty search
results yeah let me go back to the code so as can see yeah and we want the this test yeah so this one's just is testing
for an empty results after and so we we particular L you did not want to use the word no um that was a particular naming
choice because it it felt very weird to test for uh a negative Boolean which is is confusing so so that's why we
explicitly called it empty search results as opposed to no results found or something hey swegi hey swegi um so we were
looking at the ubiquitous language do we need to so we have search results do we have results as a it um we could put
under nouns I feel like it would make it would almost make more sense to to sort of attach it to the verb like the
output of the verb is are these nouns what do you think search results we're current results are you saying change this
verb to so have well let me let me show you want you type it yeah yeah but you need to escape out of it otherwise I can'
t modify mirror concurrent change problem like like that got it so just like we have sort of commands generate events we
have verbs generate nouns right okay that works for me I mean we don't you know we don't have there's no standard we can
do whatever we want if we don't like it we can change it yep it is like a document that's easy to edit okay so back to
this so now are we comfortable with non-empty search results I can't think of a better way to say it though um yeah
let's just stick with it I think that's fine let's let's not let's let's not bik shed our names too much yeah agreed
because it's very easy for us to do so okay we want a song themes controller with one song You Want a Model you want to
sing things controller calling theme search with the model and then we want to assert that it is false but the setup is
wrong we want songs yeah search returns model with search results well not yet it's really not returning the results yet
yeah that's why it's it's it's not actually returning the results it's just turning are there results right we will need
to get there so this brings up an interesting qu go ahead sure and that was part of the reason originally we had this
term here attribute right so then if we had with no search result or without empty search resolve attribute or whatever
um because once you get rid of the word attribute then it sort of implies there's content there but there isn't it's
just a boo so you're gonna say something I was gonna say the you were changing it to with no songs but I think that we
want it with songs is just the one and this brings us to the fact that we don't have a search we're not actually we have
a right we have in a sense the the song themes there's a song in there we never entered the search term yeah we never
did right so this is good right this this this is this is guiding us to like oh well we have the model for getting stuff
back but we don't actually specify the search so we might want to right figure that out so you think undo this Chuck
this test and I well I thinky this better no I think well well you know what I think you're right we should do it on
this test because well I was agree with you um we could go either way I think if we if we go back to the previous one
it's unclear why we're getting empty search results right because we haven't actually we have it with one song and we
have a theme search where we're not actually searching anything I would say let's let's postpone this this test and make
the other one more clear yeah I want to check this all out maybe I'll leave the name but okay and so with one song is
actually not clear anymore um right so I think we have to we have to this is unclear and this is unclear well that's
certainly unclear because it's missing what the heck are you searching for exactly you think inline this uh I think I
think inline it because then we're gonna have to specify a uh theme search that's not that right right okay in line this
one only or just get rid of REM I think just this one only okay done right yep yeah you can actually see that the bottom
right so um let's make it so that it's we can right right right split the line that okay that works for reference okay
yeah um so really I'm curious about theme search now what does that thing even do it doesn't do anything yeah it's got
found songs well so it does hardcoded the theme right right yeah yeah that's but that's good so now what we can do is is
we can take that theme string uh and we can make it a what were we gonna say I was gonna say make it a introduce a
parameter yeah can you go straight to introduce parameter or you make it a local and then introduce parameter no you can
go straight to introduce parameter okay so like that y yeah there we go requested theme look at that even name I'm good
with that cool done um let's uh change the order of the parameters because usually um we want model sort of come at the
end so let's do a change signature on theme search Okay control shift alt T I forget which one is signature control F6
and just swap them yep done all right um probably run our test let's let's switch to to the other tests right this has
been all refactoring and there's an extra empty test it doesn't do anything but all right cool so if we want to make
this more descriptive we want to tarch I mean searching for an empty string is kind of silly want to make I think yes
and that will lead us to The Next Step which is clarifying the setup but let's let's let's put in a song theme that is
not New Year's yeah I'm almost I was getting ready to type applesauce but I'm not going to um you could or you could
type Christmas sure I'll do Christmas because it's Christmas Eve Eve yes um but that leads to now confusion right so now
we could extract this into a new method but something along the lines of um create song with New Year's theme or
something or not Christmas theme or what were you thinking I was thinking I'm not sure i' I'd go that far just yet I
might just extract the the two pieces into local variables so theme and song theme and it what is so for local is it Al
is it no C is constant V is for variable V for variable okay you want that to be theme oh it actually guessed was theme
well theme was probably the uh was probably the parameter them what I do wrong Control Alt V you and so one of the one
of the things that this will get us to later um is creating Our Song value object uh yeah or or whatever that that
becomes our our probably won't it might be an entity yeah song entity so but for now we can we can keep it keep it that
um so now I I think this test is is is more clear uh the song title we could say is is irrelevant um line it back in you
mean well I was thinking now we could extract the whole setup into crate controller with a a theme but I I'm not sure
about that yet um but I think now we can now we can test I think I'm happy with it something I'm unhappy with about it
but I'm not sure so I'm gonna let it Fester or marinate for a more positive version okay so now this new test we want to
have non-empty we need to create it I'm GNA controller new I gota let you gotta let again so for this have continue the
same model really you see a reason not to yeah that looks that looks I'm g go back to that that probably leads us to
figuring out what exactly use theme the local variable uh or or my my preference is be is to be okay so now this you
just want to chest the right what's the deal inj how come you don't know what I want to put in a string because you don'
t have the AI on luckily least fail oh you're getting it's gonna pass I think it's gonna pass oh I haven't looked at the
the theme search time what did somebody say my 46 is without empty search oh so that attribute doesn't yeah so we didn't
copy the attribute correctly so that's fine let's run it and and watch it fail for that reason oh plural versus singular
catch so it was null so null would have been would would not have been our expected so either we would expected the test
to fail because false was not true or it would have passed um but but we got an unexpected error with null and that
means that we couldn't find the attribute um and so that's again reinforcing uh the idea of predicting precisely how
your tests fail right and uh when it doesn't match your precise failure then you know your test has a problem so let's
fix that and and thank you astred for uh yeah being the human compiler um I always like it when me or my roommates do
that or me me or my teammates do that so we're gonna fix it rerun the test this time it's going to fail sorry it's gonna
pass but it shouldn't pass is that right let's see well let's see let's run it and see what happens so well yeah so past
now you know this is one of those things where it's like did we did we take too big of a step before um I mean yes we to
me it's like yes we could have hardcoded the you know line 23 to to not do anything and just return true um and then
this test would have forced us to then actually look at the found songs and and return false um I don't I don't have a
problem with that I mean it's it's it's a fairly uh obvious Next Step um but this now uh this now sort of confirms for
me that we are we have sort of hooked up our adapter to our our application um and that's really the the here uh so I
think it's it's way past time to do a commit yes open to suggestions um I'd have to look at what we actually did I think
we actually let's uh just do a quick pass in pass in a theme to our to our search that the only thing we did pretty it
um oops wrong place now passing a theme into theme search uh I would say theme search uh uh endpoint ah even better
because there's different different levels right that good uh yep that's good uh so TK tkes asks new to Java want to
become a spring boot developer what are the main advice um make sure that you have a solid solid understanding of java
uh that's critical before you get into anything about spring boot so make sure you've done enough Java development so
you know how Constructors work you know how um to test your code and write tests uh that you can write your unit test
using junit um really focus on on making sure you've got your syntax uh and understanding of classes and how they
instantiate how they get instantiated um before you move on to Spring boot once you move on to Spring boot the spring
boot Academy is really good the spring boot guides are really good follow those tutorials and then modify them and build
on them that's that's how you learn and that's in general advice to anyone who wants to learn build on tutorials follow
them but then build on them add stuff to them add more features change things see how they work um do not get into
database stuff until you're very comfortable with with other aspect it's very easy to to try and follow a tutorial that
does everything uh but you don't know what what all the different parts are and if you've watched me long enough you
know that testing is Paramount so make sure you're able to to um and as say and don't give up uh absolutely you will be
frustrated you'll be frustrated by not understanding things you'll be frustrated by the documentation not quite being as
helpful as you'd like um read primary documentation start always with the spring docs some of it is not as good as I
would like but some of it is actually quite good uh you're not going to understand half the stuff you read but you got
to read it so you know it's there um but that's why working on your own project that you're motivated to to push on when
when times get rough so don't give up um do you need to learn spring before spring boot so one thing that's very
confusing is what the universe of the spring framework is spring framework uh you're not going to want to learn sort of
directly you're not going to just say hey give let's let's start parking with a spring framework what spring boot does
is get rid of a lot of boiler plate so the whole idea of the spring boot project was because there's going to be a lot
of boilerplate code that you're going to basically copy and paste to hook things together don't do that just use spring
boot go to start dos spring.io um lots of great videos out there uh by folks like Dan Vega and and and other folks um
and so you can follow those and just use spring boot to to slowly figure out how to how to together and yeah break the
tutorials right build on them follow them but then break them change them build on them modify them all that kind of
stuff uh and yes um you one of the things you will find be very very careful about searching stack Overflow be very very
careful about using like something like chat GPT it will give you outdated and obsolete information because spring has
been around for 20 years there's a lot of stuff out there that is no longer correct or or it's somewhat obsolete uh
always make sure you get you're looking at the most recent docs um searching Google you will find stuff and it will
redirect you to versions that are out of date so make sure uh so there's a plugin um that will automatically help you
redirect to the latest version uh I have that um uh actually contributed to it uh I think a line of code um so get that
so that you're always looking at all right what uh so how do we feel about our code here in our test um well I think
it's passing but we don't think it should be passing um well I think it should be passing uh oh wait a second because
it's false search because so it's doing the right thing it's it's now confirmed that we are hooked up to to something
that's actually paying attention to the theme that we're passing in um so because we we basically tested both ways so we
know that somewhere there's logic that's being executed and good um so do we want to the test yeah rethink about I'm
just trying to figure out how to do it such that we it's still it's so that's a that's a Chrome Store plugin latest um
so basically parameterized um Factory that takes theme and song file song title I think so and I think it it should be
creating the controller in the controller is that what you said no no what I'm saying is is uh what we want to
encapsulate is the entire setup yeah yeah right but have as parameters theme and song title right so would that be that
as an extract I guess we could find out and see what is M right yeah yep what does that do mhm now we need a better name
than get sufficient okay name yeah I'm I'm unhappy with with two parameters um but I don't want to go all we no I don't
think that helps okay I think it's it is what it is yeah okay and we want to replace the other occurrences well of
course so and having the name parameters is poar yeah I kind of think we don't have a choice um move this to the bottom
yeah let's move that to the bottom and we can clean up that uh temporary variable you want to get rid of the not okay so
let's fix that line so Alt Enter oh I see in line no I was trying to see why we're inlining oh okay now I got it I was
just trying to grock it before I did it gotta cool what you don't take intell's green g uh or is there more you had
thoughts on in this area we're just dealing with the attribute at this point yeah I think that's fine so let's uh let's
go back to jir and see if we've finished what do we finish yeah we finished up model saying that there are results or
that there are no no results but yes um yes we Have No Bananas uh let's do a commit just saying 10 um now I think we
should actually get those results in our model right so because we are getting results we're just looking to see if
they're empty or not and that's good but not good enough so are we looking at this these two um or writing a new oh
that's a good question so do we want to switch to generating HTML or or change the order is that because we don't want
to do the HTML well to me the other two flowed from what we were doing all right let's do HTM feels like yeah let's
let's move the HTML at least after a single song okay and then we can worry about multiple songs sounds good so back to
controller returns model single so a new test and I'm not and I'm not and I'm not sure it's worth so we have it we had
in jro we had sort of two separate ones for one and for many I'm not sure we get much from doing one versus many because
we're already getting a list from the underlying uh application um I don't I don't feel like we need to apply 01 mini
here I think we can go directly to many it's going to be just as um so you're saying just a straightforward that yeah
yeah you hesitated so I'm going to undo uh or do you want to do it this way oh something no I I I think I was I was
thinking you know make the test a little hard but we're GNA have to write that test anyway so let's go straight to to
multiple I don't think it's gonna so I don't this to me there's nothing Unknown about returning one versus returning
many we all if we had not all if we were doing true sort of outside in one step at a time we wouldn't have a song
Searcher application code that returns a list it would have just returned one or none so what about but we've already we
already actually I'm not sure do we have a test for song Searcher that returns mult multiple songs no um I don't think
we do because we don't yeah we haven't done it so I was actually thinking this just to kind of before you yeah was these
would be one test we would build it with one knowing it's still a list and then just make that test become the multiple
so sort of baby step it but tests um all am I just throwing confusion into the Mi well I think I think what we have to
do uh is is return is is get the model with a single song because right now that's all that the underlying application
apparently supports yep then we'll want to test a new test with multiple songs which won't work and then we'll have to
test closer and then we we yeah we might just want like do what you said basically write a test get the single one um
modify the test for multiple that will be a test that won't work until we update our song Searcher uh and then then
stuff will will just work so that's let's go that way yeah okay so we're gonna do that next uh yes okay uh so full now
full says uh why not use tools like rest assur to test control instead of instantiating the controller speed um you all
my general goal in writing tests is I want to write the fastest most directly connected tests with it with the least
amount of crft in between me and the code I'm testing adding On Tools like rest assured or HTML unit and so on are great
if that's what you're testing but I want to test my code as as directly as possible and anything else is going to get in
the way in fact you'll notice that these are actually iof free tests what some people call unit tests we're not actually
using the framework which means they are super fast um my primary goal is tests that are fast as many of them as I can
get uh and only when I have to test something like framework configuration will I fall okay see we're doing model with
single test so I kind of feel like this is less a new test and more another aspect of that uh there sure so now in
addition to checking the yeah and ah go away um hit escape again what is that okay uh so there's some setting which I
couldn't find last time I'll find it uh is deter off the the hover parameter list because yeah we don't want that um so
we're going to do a get attribute now we have to decide what attribute is going to right um search results yeah so it's
it's either search um what do you think what's the name theme search I just worry about search results being meaning
different meeting having different meetings but the name of the test is search results returns model results I'm open to
arguments one way the other I'm still thinking it through but feel free to jump in my initial thought was search results
then you said songs which you go oh maybe is the symmetry of these two like this is a Boolean without using search
results yeah yeah so I I think search results is probably better because songs could be anything where did the songs
come from are they all the songs are they some songs search results is is is probably more clear so let's let's go with
that cool to uh so search results um is going to return what's basically going to be a collection uh so I think we
probably want to say uh contains exactly um it's not going to know what that is so we're gonna have to explicitly cast
it so let's do a a cast to yeah to that um in there you mean uh or do that approach no the instance of isn't going to
help us here oh right never mind never mind uh let's first extract that to a idea yeah it'll be search results um and
then instead of object we'll make it a list of something so what do we want that list to be is it a list of string it
can't be a list of string because it has multiple components to it so this is into the yeah unless we don't unless we uh
defer that and just say no it return song titles oh and not not gives us the the key that was used to get it right oh
but yeah yeah I see what you're saying that is a deferring approach and that is simpler is it too much def ferl is is is
it truly gagy um I mean eventually that's gonna that's gonna need to become I think it's okay because I don't
necessarily want okay so say it's 50 songs do I really want New Year's Eve name of song about New Year's Eve one New
Year's Eve name of New Year's Eve song two so I don't think we're yeah I don't think we're going to want the theme we're
gonna start wanting other things like artists and so forth yes it's pretty likely we're going to want other things and
so this is this is the um you know the the question of do we defer it when we have more information but if we do that it
means that we're gonna have to do more work later to refactor these tests because they won't be list of string anymore
if we right now say look we're going to return a song View and it only only has the title in it that's going to be
easier later yeah um since it's not really yagy like we know we're goingon to need it we for sure 100% absolutely know
we're going to need it um yeah we if we defer it we're actually just deferring pain and make and actually making the
pain worse so I think I think we should introduce a a a class an object here yeah yeah you had a good name for it but I
was song view yeah um so let's go create that that's record record can is it record just Key View key value pairs or I
mean pairs or it can be any number of items so record is you can think of as syntactic sugar for a class where it
creates all Getters and Setters for you okay although it doesn't have Setters because it's immutable and doesn't have
Getters they're just query methods Getters are evil yes well Setters are more evil but Getters are evil enough true yeah
Setters are more equal okay so uh I think we can add the component that we know that's we're gonna have which is the
title now for records I'm still Rusty with records I just just put the type and and just declare a variable basically of
string oh inside the yeah right there like I was doing like this yep and song title yeah I kind of think song is
redundant because we're in song view song View and song view is for a single song We're have a list of these okay yep
got it uh lower case T oh yeah it's the name y TI okay um so now uh we're going to need to cast saying uh turning l song
view into a song search result class someday will be less painful um yeah I don't know how we want to deal with with
paging might yeah since I don't so there's a case where we probably will do paging likely 70% likely I don't know what
that looks like so that I'm willing to defer um because I don't know exactly what what that looks like so uh and that
probably will also be easier to encapsulate than yeah than a list of string because that'll be a more straightforward um
Sur surround with the class but that's a good question yeah okay so you were saying cast yeah so so if you do an Alt
Enter it'll it'll offer yep got it and we will just deal with that even though it's saying hey you might not be able to
do that in this case we know that for sure we're gonna do that all right so now yeah so now we exactly contain yeah that
yeah turning a list of string into list of song view is is painful enough encapsulating the whole thing is is I think
less painful but it's also I'm not sure what that looks like whereas this I'm pretty darn sure what it looks like uh so
what do we expect it to contain so this is where we we're finding it um so what's the song we're checking for New Year's
so it would be go what's not uh you don't need list of because contain is exactly you're specifying the entries not a
list oh so I've got an extra early I mean parent um what do we think is gonna happen when we run this I think it's gonna
fail but I have to look at the code to see so it's GNA fail because that attribute of search results doesn't exist so
we're probably going to get a null um right uh we're going to get uh on the assertion on the assertion it's going to be
null and you can't assert null and so it's just going to complain that it didn't expect actual to be null gotcha so line
49 well probably 50 49 it's fine it's going to be model get attribute that's going to be return null it's fine to cast
it to whatever you want right and then and then it'll complain on the test yep expecting actual not to be null
interesting it doesn't oh maybe it's all the way at the end 51 oh after it oh when I try to dreference it here yeah
sweet uhuk says is hating writing HTML and CSS block me from becoming a good spring boot Dev um so I find that when
people say I hate writing X it means you're uncomfortable with it um and I would say don't hate doing it doesn't mean
you have to be great at it but I think it's important to understand uh what it is and learn a little bit about it um
because it's going to be a lot less fun as a single person learning something like spring boot to not be able to
generate web pages it's kind of boring uh so you're GNA want to learn just enough but if it's not the thing you enjoy
doing that's okay because spring boot is mostly about the back end I would say like 90% of what but it's all what what
most people are doing with it is is backend stuff um all right so test fails exactly as we expected Let's uh let's let's
so we could do two things we could basically make it pass sorry not pass we could make it fail differently right so
let's do that let's make it not fail with a null let's make it fail because View oh right well what happened uh I'm
waiting for the oh you went into you went into the model itself yeah I'm waiting for the presentation thing to go away
so I can close uh wow this really is you already Mouse you already moused over it so now it's it's G to not disappear
until you tell it to disappear can I tell it to disappear Escape there we go yeah okay so we would be doing that in so
what's the code that's that's model see oh right we got it hardcoded to is empty that's not hardcoded oh right because
as empty as is is is lock right right right right right right so we want to add another attribute to the model let's see
if my cool and so what do we want to put in here to get it to get it to fail differently well if we give it no I guess
we have to put something in this well that's not going to be of the right type so it's gonna get a cast failure but we
can run it and see what happens let's let's see that it does that because what I was thinking it at least get us past
the search result null Point yeah so now we're at the casting problem so you got to put something right now I can do
list up well since we we want to have the what were we going to do all this stuff I just GNA make some so we could
return empty so it got the yeah so we could do an empty list uh that will will get cast correctly um so if you just do
collection you can just do empty list and let it sorry really you got to finish typing empty list otherwise it doesn't
know where where because it's basically a static method name oh I see so open close PR now import it got it so now we
expect it to get past the cast um get past the null of course it won't have the song in it so but so it fail for that
reason right so we're sort of building up the functionality so this is why TCR would never work for me because I TCR
requires you to to to sort of it would say well the test failed we're gonna revert everything it's like no we're we're
ratcheting up we're basically using a different failures expected failures but that are that are actually making
progress um right TCR doesn't like that but I personally think like when when people talk about taking small steps it's
not just taking small steps and writing you know tests and a little bit of code it's also writing little bits of code
that because you could modify the test each time but I don't know I find that like you could say Okay assert that search
results is not empty uh assert you can start out with assert that search results is not Dull get that to pass go back to
the test modify it um and so that would sort of make TCR happy because every time you're make but then you're modifying
the test a lot um which is another way to go it's just not the way I I do it yeah exactly so I mean so you could you
could instead of making it fail in different predictable ways you could certainly ratchet it ratchet up the um ratchet
up the assertion yeah um but uh I actually find since I'm going to be predicting anyway that it's going to fail I find
it just as good to to basically say now it's going to fail for this different reason which is still a positive matching
expectation which is really what ratcheting up the assertions would do I was wondering about you colle collection would
you do that to make it more clear um or is it if I thought it was stick around for more than like a minute ah then then
yes got it right it's only there for a hot minute but it's it's there for for it's about to disappear so right yeah got
it okay so we did look at the test it failed as we expected so now it's putting the real results in right so list of
strings now we need to convert that list of strings so do we do that conversion here this is an adapter now do we
ultimately want a song view to be a domain object no view implies not domain right it's an adapter dto yeah so it's an
adapter dto so this would be the place to create it okay eventually this will be not a list of strings correct that will
likely be that'll be a domain object that'll be a domain object yes got it okay so here we've got list so here's where
we where uh a stream is what we're gonna what we're gonna want to we're gonna want to do okay so um we don't want to
declare stream what we're eventually going to end up with is is a list of song View but and so we can a variable of that
views this is where I need to coaching uh so now we're gonna do found songs. stream do stream okay and then we're going
to do a map so a map is basically a transform okay okay and you could put a line break before stream to help yeah format
things control shift L uh I think it's it's alt shift alt control L well L yes stream API one of the best best things
ever yeah I can't wait for there's a uh something coming up in preview for Java 22 which is uh stream Gathering which is
going to be really fun cool right I think I have a stream code cata that I was gonna I need to run through and get
better with streams at yeah there's there's so many different things you can do with with the stream API that that
unless you're doing some of it often you you won't you know like I'll even fall back to let me just write this as a for
Loop and get int tell J to write it as a stream uh so what we want to do is we want to do something inside the map which
which is basically a a a function so uh what we're going to get are um we're going to get a song so let's write the
variable arrow and what we want to do is convert that to a song view so we can just do new song view passin song okay
now uh okay and now we can uh collect that to to a list you can just do two list I think you miss no it's fine why is it
indenting it weird I don't know it's really re reformat yeah something something's weird now it turns out since song
view is basically a single parameter uh thing we can just have have would do that yes which is the method reference for
the Constructor right right right sweet all right and this would go where Mt W Used to Be yes or is yeah and so full now
full uh asks a really interesting question which is why do the mapping in the controller inste instead of the service
layer and here's where the architecture of of hexagonal or other architectures too but we're we're viously think I'm
certainly thinking hexagonal yeah me too um is because this mapping is particular as we can tell by the song view name
is particular for this adapter if you have different adapters you will have different needs for mapping so you don't
want your application code to be aware of how it's being presented whether it's being presented as HTML or as uh a rest
API with Json or sending stuff through some messaging cue that should that mapping of domain information to the
presentation or external layer uh layer so thank you I don't think it's I don't think it's an SRP principle um I think
it's it's it's an isolation it's a modularization principle so I I don't I don't like SRP because I don't find it useful
guidance um and so I'm always thinking about about encapsulation so this encapsulates the job of converting the domain
for this particular adapter where it needs to be and nobody else needs to use it do you think throwing up your hexagonal
um I I don't want I don't feel like doing that right now I'll I'll maybe do it later um where and the way I think about
it also is is if you put it in the service layer for this controller and then you've got a rest API so you now have more
code in your service layer uh and then you have a message cue then you have more code in your service layer now your
service layer you've got more code that's only used by some other pieces and so from a from a cohesion standpoint it's
not cohesive it's it's doing you know and you could look at so I think for me SRP is not useful I'd rather think about
cohesion um they feel similar but cohesion I think is is just the way I think about it just to add to it oh sorry yeah I
say is to also think about it is um if you're changing say the the the rest API adapter right but not the other ones
exactly think of it as like this class um if I if I'm changing something in a single class like the service class and
that service class does three different things like it's doing three significantly different things so breaking and
that's the true single responsibility principle of not hey this has a single responsibility really what it's about is it
has a single reason to change yeah um and so changing if I want to change the API then I want to change just code that's
responsible for for that um I don't want to have to go and change something and now if I'm changing something else
having to do with presentation of HTML if I'm if every time I'm changing any of those things and those are very
different things if I'm having to go to the same place that's multiple reasons for changing that code yeah exactly the
service doesn't care it's not its responsibility um it should be purely responsible for implementing the application
which is the business rules policies logic that kind of uh that kind of thing and not at all about how it it gets
presented whether it's HTML or Json or XML to the outside world yeah and and I think it's it's so such an important like
I don't care if you use hexagonal or clean or onion or whatever you talk about having those separation of concerns of
what's domain and what's basically IO right this stuff that we're dealing with here is IO right HTML it's going to sent
be sent out to somebody's browser separating that makes the testing so much easier and I always tell people if you do
nothing else better we ready to uh run the test uh yes and then I'm going to have you fix something in intell So yeah so
what do we think is gonna happen so let's see we've we've views at least we think we have um it looks like we have and
so really it's is the Searcher actually does the Searcher do does the SE work well I hope we had tests for that and and
those passed so uh yeah it looks yeah yep passed voila it wasn't that fast okay um you wanted me to fix settings you fig
out where that yeah go to um uh under or just tell me the name uh or is it signatures and it'll be under code completion
right there uh there it is uh yes so it's it's basically nearby there so hit Escape so we can see all the other options
um uncheck the show the parameter info popup because that's what's annoying us got it that's it um actually what I
didn't like that wanted yeah I over the years i' I've turned off all of the hover Auto popup stuff because if I want to
know it I want to explicitly invoke it um it annoys me to no end to to that's which is why I had to fix it to like see
other people like and it's unintentional it's like you know you're you're sitting there talking about something and and
your mouse has hovered over it and now it's popping something up that's obscuring other stuff and it's like no stop it
exactly cool um I actually realized have we been going for more than an hour really uh oh yeah I guess we have so maybe
this is a good time for a break or maybe let's to answer the text the um messages in the comments and then yeah take so
inter fun Zer asks and then answers his own question as a Searcher a mock and that's like nope we we are doing um very
much uh Detroit style um classical non-ach oriented uh using real objects in in our tests um and so uh says yes it's the
real one um and that's that I think is very much related to what what I basically just said about separation of concerns
is if your application code and so from hexagonal or or whatever separation of concerns architecture is in the center of
of you know mentally in the center and it does know IO it is just as it is cheaper it is cheaper it is faster to
instantiate your real domain objects than it is to use MOX MOX down and and it's funny it's like what but no that can't
be it's like makito will slow down your tests and there's no reason to use it it's actually faster to use real domain
objects with the additional advantage of you're not fooled into thinking your test passed when actually your real code
was broken some time ago makito is doing all sorts of stuff uh using bite buddy and and and gnarly tools to to do stuff
um uh it bypasses Reflections in some ways but it but it does some other stuff that's just nasty um and is just slow and
is unnecessary just completely unnecessary um there are places where you might want to use it but I think still
handrolled stuff uh is is much better um I don't I don't know if they use Mak I don't know that the makito existed um
probably an early form of it or maybe easy mock or some of the older jmck tools Maybe maybe existed but to me it's it's
not about from from the growing object-oriented software which is what the goose book is um it's more about when do you
implement the real code so we from from the past episodes we we did a little bit of inside out we sort of started at the
song themer The Domain object um and then now we've moved back to outside in to connect things up and so the question is
is do you sort of do depth first like let's get no songs and we go all the way down into the song theme or all the way
down to the domain object and Implement that the more Goose way of doing it is at each layer at each level you basically
mock out the rest and say okay we want to make sure that our UI works and now let's go to the next layer where we
actually talk to the real Searcher um and and do that that kind of thing um but I I very much like the the depth first
implement it all the way down um so I don't I it's been a while since I've read the books but but uh you don't have to
use a mocking tool to write your test doubles of which mocks are one type um I generally prefer to hand code mine
because they're going to be faster and they're going to give me exactly what I want uh and a lot of times you don't need
to write very much and the other thing is it's actually if you write your own should you have a need for a mock or a spy
whatever it's rolling your own yeah kind of gives you a better sense of what's actually happening versus you thing and
so the aners to that question of how do you test external APR or some services without makito is write your own makito
is shortcutting your knowledge of how you interact with other systems so you create a class that's going to be your
adapter to that EXP internal system and you create it as as a stub or as a or as a dummy or as a fake uh but you write
the code there's no reason to use makito for that all it does is make life harder when you run the test but they're
slower and it makes life much harder when you actually have to refactor uh and yes can always rely on Jaa to to have
some good stuff on that uh I'll answer this last question and then we'll we'll take a break uh we will we use contract
tests for the inmemory repo and the real repo um yes uh so generally when we write test against our basic our
application code the application code is going to need to go and fetch stuff from from some repository those application
tests should run exactly the same way I.E pass whether you're using an in-memory repository or real database um and we'
ll uh basically write tests that will'll excute both all right uh we're going to take five seven minute break uh and
then when we come back we'll write some more seven right so I'm waiting for Mike to come back um just going to mention
uh this talk so if you go to my uh YouTube channel Jitter ted. TV um I've got a bunch of talks that I've given around
the world on uh various various meetups and um uh this one in particular talks about testable architecture um using
hexagonal uh but the same principles apply whether you call it clean or hexagonal or onion again the idea is there's
your pure domain code your application code hopefully you develop that using domain driven design tactical uh basically
Discovery techniques and you apply the Tactical patterns in that module in or in that boundary uh and so uh this talk
basically goes through how it helps uh testability to way seeing that coffee is torturing me I already had one this very
early this morning but I would love a second but I think that would be truly yeah I was I was thinking about it's like
no it's after 1 and I I try not to drink coffee after 1 and I don't have decaf because I don't see the why bother yeah I
used to be a um 6:00 am and then again at like one or two midafternoon break with my colleagues but um I can't do the
two in the afternoon anymore it's called it's called get old I guess CU I remember I remember I used to be able to have
like a a you know Double Espresso after dinner and that would be fine but not anymore a friend that still can do that
but yeah so back here all right um we should do a commit if we haven't already good Lord yes wrong um uh do we want to
update jro right me you laughing at they they're calling it jir I'm laughing do we need more I guess we'll cross a we
get to it uh I don't know that I don't know do we have a test for multiple songs no we didn't do that just now did we no
we were doing no we did next yeah it hasn't yet I'm sure it will become on you know no longer warranting a chuckle but I
gotta kick out of it yeah all right so let's let's commit now that we've updated we're doing standup now yeah three
shows a day two waitress TI your waitress yeah okay um good enough yeah technically it it does more than that because
we're not we didn't just grab the first song and map it we actually M the whole list so I matching sounds good yep and
shipped speaking of yeah do we want to keep pushing I mean the next so I I think after we do the generate HTML I'd like
to to ship it to I'd like to push production now with the website be showing the HTML because I I'd rather have the
website still just be non-functional why is that if we have something that doesn't do anything for real um yeah doesn't
do anything for real right now right but it says so it soon well we're not doing continuous deployment unless we're
shipping stuff true true well but you can no no but you can ship with a feature flag you can ship with a feature flag
and it's on the server but it's not right sure but what's what's your concern um well just because it's domain somebody
someone acrosses like oh this website it doesn't do anything it just returns old z z and then otherwise it returns
nothing okay I mean it's your site I'm I'm just trying to I'm just I'm just wondering what what what your concern is
that's fine we could do feature flag yeah actually that'd be good to from a feature plag perspective that' be it's just
I'm I'm I'm uncomfortable going for too long without actually sites got it I mean with a feature flag you're still
pushing it to production what you're saying is not that you're not com pushing to production you don't really you're not
really like putting stuff behind a flag is is temporary at some point you're G to need to turn off that feature flag
right um and why not sooner rather than later right right um but again it's your site so you get to choose just saying
that that I start to be uncomfortable when when I haven't seen stuff in production especially once we get to databases
and things like that um but you know again it's it's it's your app the your site so you to decide people are saying a
lot of stuff in the I've seen worst sites you yeah but you know I don't I don't want to pressure you into do you doing
something that you're not comfortable with right right right let's um let's let it marinate um but we could still yep
right now we still we should still get it to the point where um because the other thing is also uh if if um because
right now this would not change if we pushed it to all the way to production right it still yeah right now we we have a
get mapping to a to an endpoint that nobody knows about unless they're watching this stream right um but anyway let's
let's let's get to the point where we can at least run it locally and and see the uh and see the HTML okay um so do we
want to do the just get the next one off off the list because I'm about yeah I would say let's let's do the next one one
um and then we'll generate the HTML and then we'll try it out okay um so back to controller test yep that was this one
so now we need to populate with more than one song which means this so this is GNA this is going to require us to to do
some depth uh changes in depth as it were should we move over to well no so we want to do what we want to do is if we're
we're now sort of doing full-fledged outside in which means we want a failing test at this layer which will then require
us to implement something down in the domain get that working and if that works properly this test should then pass then
pass right so let's get this test to fail we can disable it then go down a layer work um do we inline this work within
that framework to refactor towards it or do we just start that's what my I'm thinking to myself and I should be thinking
out loud so yeah it's like we want to have we want to pass in a list of themes well no wait a second controller really
it's it's create with some with with songs and these happen to be attribute pairs but for a single song right and we
have the concept of but song view is not for populating that's correct and song view is is not a pair not song view is
irrelevant from from this right so what I would say is we want to First basically create a parameter object that will be
um right now for the convenience of populating basically ending up database is there a way to automatically create a a
pop a yes so you can uh if you bring up the refractor menu or I don't know I'm not sure if Alt Enter will do it but if
we bring up the refractor menu we can introduce um uh I may have the cursor in the wrong spot yeah so if you put it on
the on the method itself yeah and it should have um uh on the refactor object H that's interesting why isn't it there
maybe you have to be inside but not parameters meaning like here menu H why is why is introduced up because sometimes
the menu has more than the so the refractor this will has more choices than uh oh more I thought it was the way around I
thought this had more than fact is introduce yeah see right here extract introduce parameter object yeah I'm just
wondering why why it wasn't coming up on the refractor this I've often found things that are available but that aren't
in refractor this I always think of refractor this is a subset of the possibilities not all of can you can you put the
cursor right after the open pren before theme try again yeah can you put it in after The Comma just wondering what
because I know yeah I know I've seen it come up in this menu oh you have yeah um all right well let's there is internet
search how do you well it's it's a I'm not gonna worry about it let's just go and refactor it so from here yes ah now
it's telling us where to singular yeah um can you try selecting both theme and song title yeah and now bring up the
refractor this okay bring up the refractor menu and see I'm I'm I'm thinking that it's not going to show see here it
shows you all the options it doesn't mean they're valid right that's why Factor this will only show you valid options in
that context um within the method declaration so sui mentions maybe it's only available in the implementation which
would be weird let's try yeah yeah there it is it is that's unfortunate um thanks IGI I feel like feel like that's
anyway it is what it is but I feel like it should should offer that at at a call site as well uh because you can do
things like so all right so what we want to do is we want to create um now this is we don't I don't quite know where
right now we're using it here uh what do we do with the values so move that out the way so we passed them right into
create song Searcher what let's jump into that yeah so this is this is something that's basically going to have to sort
of bubble all the way down and it also seems kind of weird that song Searcher Constructor gets the theme you would think
that that would be a on a search method well remember that what we're adding is we're adding the the theme and song are
basically all part of song we're basically saying create song search with one song because that's all we did when we
were doing inside out development yeah yeah but start so we need to do is is and we can do this sort of bottom up or top
down to to basically replace the theme song title pair with an object what are you thinking and then I was thinking
ultimately that object would be would contain a theme and a list of songs okay so now we're getting into now you're
getting into what is our data design and that's not how I was thinking of it at all ah okay um not that your way is
invalid it's just I was thinking here's because I was thinking how how does data entry work and where does the data come
from you get a bunch of songs for each song you get its its data and It theme and so you basically have in a sense you
you know a spreadsheet like thing um where one of those columns is is the theme right uh internally it's likely G to be
a hashmap because ultimately a single song will have multiple themes but but when you're reading and database um and so
this now gets into how we how we persist it um so so sort of taking a step fact since I'm not quite sure what the
internal structure is going to look like and it is internal what is the most convenient way for us to yeah pair add
songs so when we add a song We're likely going to be adding a song and it's gonna have the theme whether the theme is
part of the song object or not is we defer I'd probably put it on there unless there's a reason not to because um it's
always good to keep things separated that so I think uh we can sort of go top down or we can say well we know we're
going to need some song domain object and sort of move move uh sort of bottom bottom up yeah so so swegi asks a relevant
question which is kind of something of multiple themes definitely um so yes uh we know we're going to need it should
that is that something we we say we don't need it yet and defer it or do we include that now I'm inclined to a deferring
yeah I feel like we know we're going to need it I I I feel like that's a bridge too far because there's other okay so we
created we didn't create that did we um well we didn't because we we want to figure out do we want to go bottom up or or
top down right um my tendency is is to go top down because that drives what clients need and so it's a very uh client
Centric yeah uh so let's let's do that okay so where were we we were here um so full now full asks uh since both
parameters are strings what happens if we invert song and theme when calling the controller um bad things which is why
you always want to uh avoid that but when you have string parameters that are coming in uh to an endpoint um presumably
they're fed to you by a form which would then match up the names um but uh the the more you get closer to the domain the
more you're likely going to want value object for for some of these things uh but there's a trade-off and so um that
would be part of a test to make sure that when your form is submitted that the parameters are correct and that you're
evaluating the parameters correctly uh because at that level you're just dealing with with strings as you go inside you
can decide whether they're value objects or not um there but there we I think we talked about before there's there's a
cost to objects um shall we or you got a thought before we this yeah I'm just I'm just wondering uh object yeah Java can
be a stringly typed careful um so what do we want to call this is this going to be ultimately our Our Song so all right
if we wrong we can yeah Valu says when I'm joining your stream write test yes because most of the the thinking time is
you know if you're doing test driven development most of your thinking time is when you're writing tests because when
you're writing code it's almost trivial it's just okay I got to make it do this I know exactly what it needs to do and I
have a sense of exactly how it needs to work um there's generally uh from a thinking standpoint you may end you're
probably GNA end up with more test code than than code um but from a thinking standpoint it's going to vastly outweigh
the time that you're spending writing tests and thinking about your tests um than thinking about your code yeah when you
do tdd stop you don't think as much about the writing code part anymore yeah having to you're not did two things you're
there you're trying to write production code and mentally go through what a test is doing yeah in your brain like what
happens about this and what if this happened you write test for it and I will say though in terms of tests writing tests
and refactoring like what we're doing now is we're not writing tests we're refactoring um so there's certainly a large
proportion of time where you're refactoring so between thinking about what you're going to need the test to do writing
the test and then refactor it the amount of time you're actually writing production code is probably like 10 to 20% the
rest of it's your test you're so yeah I mean the test would never passed if we didn't have production code um but it's
just such a small small part of it yeah that's great that's great all right um anything else about the package let's see
at the moment it's fine we fine so um be careful about the destination directory let's make sure it's in our production
directory you might have to hit the three dots yeah oh sneaky yeah it is sneaky I hate yep all right um let's run the
test just for Giggles but that was hopefully a yeah now did it create a class or a record let's go see it created a
record well good for it um we may end up turning it into a class but but but go and let's um so now this yeah is only
dealing with the uh single song scenario right well so what we're doing is is basically um I don't know if it's quite a
prepare refactoring but before we can have multiple songs we need to group them up into objects to make that easier y
because you because you don't want to jump straight to a list of matching themes and song titles and have parallel lists
because that would be terrible um so by by bottle by sort of putting them together as as a song uh that'll it'll make it
easier for the multiple yeah if you're not rting the test first you're not doing tdd you may be doing a good job but tdd
yep that's why I do TD puts all the thinking at the safest possible point front all right so let's um uh so does this
give us enough where we can where we can add multiple songs if not we're level so we have to drop down a level yeah so
Searcher um now can we do a change signature on this and replace theme and song can we do see just delete so delete them
both and song um no I think we can't do that I think we have to do the the other way around yeah let's cancel that yeah
so let's describe what we want um uh would this work here no that's bring it up but I believe it's only for um oh no
okay so we can use existing class yes uh I don't do this very often but song uh we don't want to generate accessors we'
ve got accessors uh we shouldn't need to escalate visibility but sure leave it it's all in one package anyway let's see
here yeah so it um because it's a record because it's a record it it's it's a bit confused we could convert to a class
and have that work but I don't I don't want to do that uh so let's cancel out of this but that's something that um maybe
someday they'll fix what we want to do is uh um so we could we could change the signature and pass like what what suiga
is mentioning pass in the new object and then stop using the old old ones uh but I think what we can do instead is
inside of this create song Searcher method create a song object and then break it apart call new song Searcher and then
introduce um yep it's a freaking song it's I mean it is competing with the part par the the incoming parameter song so
let's rename the parameter because that's uh it's not song it's actually title so let's fix that okay I want to hit
enter so that get the song one is it oh yep that's right title yep is that sufficient yeah right thank you for offering
song to as um and then is it that's right okay and now let's split apart the song on 19 and on the two parameters on on
that line 19 oh I see song dot yep uh but it's a method call not a parameter variable oh what's it called I think you
called else no no you just oh I could yeah I think I think actually in uh in the record it's it's redundant it may have
made sense when it wasn't part of a parameter object but now it's now it's redundant because you're gonna say song. song
title uh but we'll fix that we'll fix that in a minute that's I yeah so now let's just run our test just to make right
and now we can do an introduced MH and so notice it's going to strike out the other ones because they're no enter and it
changed all the colors right now it changed the colors in a way that might might not have been convenient but um that's
all right we'll we'll take care of those should we go look at those right away or were you thinking so uh well let's
certainly fix the one that's in 57 you can just replace the whole thing Oh the whole thing I was working on it you still
I just doing it pass right sure all right good uh and let's let's clean we'll okay so the other usage is for this one
right yep so that one's fine uh that one I'm not sure about you can open up the you can turn on the preview in in the
upper right of that right next to where it says four usages on the upper right oh that's actually not what I wanted but
fine there's the other option to to show it below it yeah I thought it was control shift I isn't that let me undo again
uh so it's the one next to project files to the left of the word project files yeah that one the preview Source go so
that one that one's fine uh that one we can't see oh I think that one's fine too so there's a bottom scroll bars you
could that if you want that you could scroll but we can see that that one's fine because that one is using uh hardcoded
strings uh and I think the last one is that's when we changed that's when we changed good yeah Y um let's uh yeah let's
do a commit we've still got to push push this down a bit more but let's do a files I don't know um to uh yeah starting
to create song to attributes okay ship it yep well not shipping it don't be bitter yet okay hey there hey there James
welcome all right let's uh let's push it Constructor um and here we could try it the other way uh the one that sui was
suggesting yeah just see what that feels like chain sure yes so we'd add the we'd add the um parameter need to get the
type did it grab the type yes otherwise it would be red okay uh that's going to conflict so hold on let's uh well before
you do anything VAR and then uh scroll back then scroll up and we'll go and rename the other parameter at the same time
we'll see if it'll let us do that click that yeah click it again and title let's see if let's see how well it works when
you're changing two things at that um oh and this field still says song wow okay that got confused in a way that I did
not expect so on line 13 the problem isn't with title title is the correct parameter why did it stick a this in front of
it oh interesting that's that's a bug because all we did is rename the parameter to title and it got that part right but
it stuck at this in front of it which doesn't exist so if you if you remove the this from the right side of 13 uh it
should work yeah um so if we run our test it should still work despite the fact that we've got well actually I'm not
sure it depends on what it added for the callers not happy uh so let's take a look what did what did it mess up oh with
the any it it basically what oh oh because we yeah I guess any didn't didn't work um we song let's let's un let's undo
this and try it again see how far back we have to go well we just did a commit so it works we could just rever back to
the commit let that uh so uh James we're working on an app called song themes which is basically a in quick summary is
find songs that match a theme um and you can watch previous episodes if you want to catch up on our event storming of
that and some of our initial test driving uh so we're just doing some refactoring right at this moment to create an
object that we're presents a single song um and we're just trying some that uh where are we located um we're in the west
coast of of the United States so we're in Pacific time zone UTC minus 8 so you must be UTC plus4 at least so the time
zone is great for us um two o'clock in the afternoon not so good if you're if you're if you if you're on the other side
of UTC yeah uh do we want to try this again sui's way um or do we want to do it our our way uh the way we did it before
is there a way we we can pull it off yeah I think if we change the uh I think when we when we instead of using any VAR
just put in a new song um but maybe let's do it in two steps let's rename let's rename song the title title ref Factor
nothing else tricky right right letter y uh and now let's now let's try the change signature uh of adding the new
parameter looks like I have another hover problem to solve okay so here yeah and the name is song song name song don't
do don't do use anyar let I I wonder I mean we could try because I wonder if it got confused with with the other thing
we were trying to do um you just try this straight up yeah let's try this straight up we can we can quickly undo that
yeah so oh I'm G to go back um yeah because that had definitely didn't do anything uh or didn't do what we wanted so I
think we need need again let's add our parameter um for our default value let's um yeah so here's where we would we
would Define the object that we want inside and push it out and here we're we're trying to pull it in from the outside
uh and I'm not sure I'm surprised use any VAR wouldn't wouldn't work though maybe it's because we were doing two things
at once yeah that's that's why I'm wondering if if if it's a cheap experiment to do do it let's see yeah default value
oh okay so we do need a default value even if we say use any ofar so I guess I don't understand what use anyar does H uh
it says look for the variable of the appropriate type near the method column pass it to the method um so let's let's so
hit enter on that don't hit cancel uh click that let's change sign uh no let's change signature again okay let's add the
parameter song and song song uh and then open print and let's say theme comma yeah um okay that's not going to work so
strings so double quote comma double quote um and now check use any VAR and now it's ref Factor okay I have no do
original yeah I mean that part has it's always done but let's look at the usages right so that's interesting so it
worked where so line 18 there that's fine we can just delete the first two entries um line 22 not so much there we would
have to manually create the the thing but we have the place to put it um let's just do that so I don't know that there
there's a better way uh to do this but let's there's only two places it'll be good enough to just okay so let's fix up
18 first one yeah that's easy um oh actually you know what just leave it because it's fine okay we'll fix it up because
we have to do one more change signature so undo what you just did because we need the parameters there so when we delete
those first two parameters it's going to be fine okay um we want to make 22 such that if we delete the first two
parameters that it's also fine ah gotcha okay so te so what's going to remain is what's going to remain is the last
parameter the new song with the currently empty double quotes we want to move the theme and the song with theme text
over there y feel like there's a better way to do this but I need more experimenting uh be careful you pasted it wrong
so don't paste it with the double quotes delete right yeah it's in your buffer just paste it again if you're not sure
hit uh get what it is on on PC um if you do control shift V that brings up your clipboard history I write that one pen
oh I'm sitting in front of a computer with a notepad why am I getting a pen v looks like a paste buffer yes okay sweet
thank you um let's run just to make sure stuff works and then we can go ahead and change the signature to get rid of
those obsolete parameters awesome feel good let's go change signature on the on the Constructor see you can do change
signature from here why can't you do introduce parameter object from the call site it's it's the same DN thing anyway
let's go do it I'll complain to separately turn def yeah okay so now we yep just boldly go hey we've got uh oh we have
oh so we maybe should have done a safe delete so let's go back to the Constructor uh let's cancel out of here because we
didn't do the last step or did we no we didn't because we actually don't have so now what do we want to do here um uh we
do song I Think We Want To Do song dot yeah so you can just hit um undo that undo again so if you do song dot Sor go
back sorry so if you type song Dot and if you hit tab it will auto complete it and then tab yep got so now we can do you
can do the safe delete on those so delete okay yep and then again for this one yep all all right cool um now let's
commit because we propagated it all the way down and we will act in order to make the next test pass um we will probably
want to do prepare refactoring but this gets us a good good there I always miss Bell propagate every single time it's
like why isn't it prop oate no it's prop aate it's okay or remove the turtles uh okay cool um do you want to pause for
comments in the Stream uh there wasn't that much I'll I'll take one opportunity uh can you delete line 17 on the bottom
it's gonna drive me crazy oh yeah that would drive me crazy too it's so funny how like you know different people have
different sensitivities to to it's fine but like I I the one I'm fine with which I know you aren't is that that would be
fine oh no I don't I know you don't like it so totally fine to go with good uh let's see what do we want to do um want
to move towards the list next yes so I think I think now we've we've we've done a fair amount of preparation there's
probably going to be one more prepare step um do we want to do that now or do we want to write the test first is is
really the question right while you ponder that I'll answer this question so tkes asks about direction of java in Spring
boot do I like it yes do I wish it would go faster of course um unlike C where they just throw feature after feature
after feature in every release and then sometimes regret it Java takes the point of view of let's preview it for a
little while let's bake it a bit more which does mean Java moves a bit more slowly but it feels to me and I'm totally
biased so I could be totally wrong but it feels to me that when Java does something and we're talking sort of basically
the last four plus four or five years um they get it generally right uh so Java 21 was was I think people still I don't
know that people understand how significant of a release it was um the virtual threads virtually do away with uh
reactive programming you still find use for it in some places where where you can actually take advantage of what's
called back pressure if you don't need back pressure then just let iio block a thread threads are are are are extremely
cheap now um spring boot is is complex but I think they're they're doing some good things on on simplifying some things
uh but um it's one of those where I wish they had even more testable aspects to it um like they have the new HTTP client
the new jdbc client I have not played with them enough to see how well they work in a test-driven separation of concerns
context um because I know rest client and stuff like that was hard to deal with I don't know if the new ones are are
better uh but it's still better than what it was go yeah some some typos I guess we have to we have to live with um but
uh Java 22 it's not going to be as big but it's got some good stuff in it it's got some good preview stuff I'm looking
forward to that um yeah all right uh so we we've got a test that takes one song right we're moving towards multi songs
yeah so I think we I think we have to continue refactoring to push towards that otherwise we can't write this test um um
so let's do it let's is there is there a way to push it from this level or no we have I mean we have to start from the
test and the test requires us to be able to add multiple songs results no I did I was just wondering we're going to test
at this level or this level well we want to so we want to write a controller test because we want to write an outside
test that's G to fail um and then we're going to go write our inside tests get that to pass and then this this should
pass so you think write a new test versus morphing this one originally we were talking about morphing this one into oh I
still think we should morph this one okay yeah cool but we still have some more work to do because prep uh we're gonna
want to pass in not just a single new song but multiple new songs I think we can um no we can't not yet oh that's going
to be annoying what do you what do you think so I was thinking we could inline uh 40 and 41 but now song it would be
still unclear which one's the theme and which one's the title uh but can we fix song title to to title because that's
gonna me um we want to rename the actual thing on so not here I want to go into song itself and fix it oh that's the one
you made okay got it yeah actually no shift F6 yep fail yep and hopefully that did the right tests yep and now we can
rename 41 to song to to just title yeah yeah I don't think we want VAR ARS because we want to be very explicit about
what we want uh oh you're talking about the signature to the create song themes controller that takes vars of a song yes
we can absolutely do that in fact that's what we were I was going to do way to not have to have the variables uh well
let's let's just do it so let's add another let's add another song so let's do um let's put a comma after after that so
not there but here there uh let's push that to a new line new line on the same page s you're like you're like on right
there and I'm and I'm it's okay do it um let's add another song So theme and title just this oh the same theme and title
uh no sorry you you're the song guy you come up with another song oh I see um it should be it should be the same theme
okay same theme but different song yeah got it um I canot think of one do you have one in your spreadsheet uh let me see
if I have it readily available if I had a dollar for every time someone said Java was dying i' I'd be a rich man Java is
is as alive if not more so uh than it has been in quite some time and there are recent improvements and improvements
coming in Java 22 that even make it easier to learn and get started important all right um I think if we're going to do
that we can inline title above it in line oh or we could just make this another variable it's up to you oh because theme
is a variable then yeah if we have theme as the variable then it become then then it has enough documentation to yeah
you're right convinced um I'm still not liking it as much uh but unless we had a some sort of Builder it's there I don't
think there's any other way because one thing Java does not have and is unlikely to get anytime soon are name parameters
that's life um all right so um no option is what we want that's these like how it's like ad song is second parameter or
ad song is first parameter it's like thanks that's not what we want we want far ARS that's a manually uh so let's let's
do the least amount that we can get it to to compile so change um the song parameter add three dots after the the type
no sorry oh after the type so it'll be s dot dot dot now it'll complain there in line 57 we'll fix that by putting uh
square brackets zero after it because song is now an array since song is now an array let's rename it so that it's
sounds like an array uh rename though yeah but do you like that name as what I was oh was there a was there yeah songs
was there was there another choice that a plural of song yeah I mean yeah yeah I know you don't like song array that
would have not worked oh God would you have even considered that no I was trying to triangulate into what other names
were that yeah so so now this is fully backwards compatible of course we're ignoring the second song um but at least now
we're a little bit better prepared um let's run our test make sure we didn't break anything yeah I was that is there any
way I can install the old presentation assistant back on this love yeah because you can always install uh I think we
we're gonna have to push this uh vogs down so let's um let's go into yeah create song Searcher let's make that be 17
doing the zero trick again yeah yeah variable hello let's run our test just to be right I'm going to start kicking you
to use the the shortcut key to close that window oh yeah that one's shift control shift F12 right uh that's one of them
yeah you can use that one that one well there's one specific for that window but the allpurpose one uh is is better
right all right let's go into the Constructor what is it if I hover will it tell me sh shift Escape closes the current
currently open window it's hide active tool window technically um let's go into the construction one second hide active
tool window got it okay go to the Constructor trick then yeah all right uh um so now we need to change the internal
structure of uh actually before before we do that so we've propagated this down but now we want to have the test fail um
so I think we've done enough preparation up up at the controller test level uh that we can now make it fail and then
we'll have to basically have a songs this test we're going to change yes so because what we want now is we the test is
saying hey here are these two songs with the same theme we now right oh am I yep okay I was driving without instructions
No I gave you an instruction and actually what was don't tell V oh it's still in the top sweet I know where my csor is
we'll find out oh great okay so now this should fail and it's going to fail because it doesn't have two only one right
unless there's some no point or exception or something that we're not thinking of yeah no y no looks like it failed as
we expected shift Escape uh so full asks can we use list instead of VAR so we could the problem with going directly to
list is it requires a lot more code changes the args all um makes it very easy uh to change but also we don't
necessarily always want more than one um so using a list forces everyone to pass in a list regardless of whether there's
one or not we may eventually go to to a list um but it it's easier on the caller to not have that all right um so we got
a test and it's failing for the right reason uh I think um I'm just wondering you want to commit so are you thinking um
we can't that any changes we make will now cause a second failure and so want this one to be quiet for a little bit
right so we've done as much as we can at this layer um there's nothing else we can do it at the the controller can't fix
we can't fix this in the controller which means we have to go down a layer into our application into our song Searcher
um but in order to to make those changes because right now the only test that's failing is is in the adap this one right
make one of these so exactly yeah and so we don't want to get into the situation where multiple tests are failing right
where it's like for remember this one shouldn't be failing or this one's okay to fail right okay um yes um what
introduce I'm not sure they started to introduce multiple songs but it's kind okay commit I'm G to try a shift Escape
yeah works for that one too sweet yeah it's whatever the active window was active tool window if you had the run and the
commit window open it would only close one of them so you can try that if you want actually G try that I do this and ALT
four okay I was gonna do that there are there are there are even though you don't have them visible there are numeric
shortcuts associated with many of the tool windows so zero is for commit four is for run nine is for get uh seven is for
structure and I know these because they used to always show the numbers but now they don't oh they don't nope you can
turn it on but they by default I believe they don't show it so now if you do shift Escape yeah I should just do one of
them probably the most recent one I'm guessing yes and then if I do it again yeah nothing right because the active is
where the cursor is right so you'd have to go back to the commit tool window and now if you hit shift Escape it would
close right yeah so it doesn't doesn't have a tool window buffer that it's closing it jumped to where the cursor was
yeah they basically figure if if you want to close the window that that is not currently active then just do the high
all yeah yeah so uh full enough we're we're never searching by song we're always searching by theme and so the intention
is if we search by New Year's theme we should retrieve two songs so that's our that's our intention which currently does
not work because right now song Searcher only knows how to hold on to one song uh but we'll see if but that's basically
the next thing we're going to fix yeah yes I'm not going to rant about the new UI we're not using the new UI and they
will have to pry the the old UI from my cold dead hands oh in's new UI yeah yeah yeah there are a few nice aspects to it
but most of it is is in my opinion too much copying vs code and it's not just my opinion um it's three o'clock do you
want to keep going or do you want to stop I don't mind keep going um okay how much longer do you think you want to go I'
m the question the reason I'm asking that is whether we should take a break and then keep going for a bit um I don't
know that I can predict I don't have any any commitments but I don't know that I can predict do you want to take a quick
break and then yeah let's do a five minute break and then we'll just see how energy goes but I'm thinking we could do at
least a half hour okay more all right cool all right we'll take a break and when I come back we will force song Searcher
to have be able oops for that for all so we committed we got our our failing outer test and uh next time I'll also be
more prepared to sort of diagram this maybe next time we'll take a little time to to even though there's not much there
there is there is enough there where we can start sort of diagramming what goes where from an architectural standpoint
sounds um and might even refactor to those packages uh next time Jura need Zombies anymore items down here you think
yeah look you got an entry right there architecture all right let's write our um basically test now that method I'm
betting is is a bit unclear because it says songs um yeah I don't know what plural uh let's look at the implementation
of that yeah I'm not sure name so that I need to change my physical position so I'm getting back support okay oh it's
the static method I see right so let's make it make it more truthful I'm open to ideas my brain's not uh with one song
for yeah because it is only creating one song yeah um and the width is driving me crazy song Searcher width oh okay that
makes sense never mind yeah from the calling side it makes sense yeah yeah um so let's go and um I think we're goingon
to need to okay this one will be finds multiple matching all which I always thought was such an awkward thing on Windows
it's so much nicer on on a Mac yeah because there's no insert key on Mac on most Mac keyboards so we are what was the
name you said so it's basically the same name as we had for the other one search for theme and this songs oh I need to
up sorry OA strike I actually for got to update my uh uh nightbot to return the right project um what we're currently
working on that the code is actually not open source uh so sorry about that someday maybe all right um do you need
direction on on how to take it from here oh sure no I'm good um just not sure I like that though song songs right this
we can CL grab both parts you're yeah now here it's here it's just we're getting the the titles right but also I'm GNA
fix that yes on songs now will this we're expecting just the titles right whoops I didn't do the take that no no that
was not the latest thing you copied yeah that's probably why there we go uh nope try go uh you just count on the
keyboard enough you'll eventually yeah you know Tri trial and error um I'd split the a new line before the song yeah
agreed all fail um SE that it's not gonna it's only going to find one song we hope Let's see we did the the refactoring
yeah everything is based on returning just the first song and that's it so I believe that's the case well it yes we're
only going to get the first song but that's because it's only storing the first song right yeah because it's only
dealing yep um so full NL says what about search songs by themes since it can return one song or more um by definition
it can return one song or more so I I feel that we don't need to say song search uh because the name of the class that
we're calling against this is where naming is contextual naming is always contextual and so by theme uh is a method on
song Searcher because song Searcher is the context and we're saying by theme because we're going to have other ways to
search for songs but this is the one by theme all right um let's fix it okay does this have a v AR it does yes so now
we're just gonna do just enough to make it pass even though well I guess it would be generalizable to two that I I
wouldn't I wouldn't go this way I would just okay pass pass songs down without the array reference oh because uh that
just just work it should just yeah because um songs is basically an array which VAR args accepts so this should still
fail in the same way right um but now we're we're yep and now we can fix fix this one now we have to figure out how do
we want to songs any reason not to do well I guess what were you GNA say any reason not to do a list but then I was like
no we need like a hashm B of yeah hashmap is probably the most appropriate yeah so would we well we're in refactoring
well no we're failing so we're not we're writing new code right so what we should probably do is we're we're changing
internal implementation which means that's a refactor which means we should disable the current test sorry uh yeah
disable the current test really disable this test yep okay I mean you could comment it out but the problem with
commenting stuff out is if we do any refactorings they no I didn't I didn't mean disabled versus commenting I was now
well that was the only test that failed so disabling it would then get us back to green right got it I you could take
the test annotation off also but that's worse because easily forget about it you forget about it yeah of course okay uh
question about well we use a database later on yes we will eventually use a database yeah so on cassette yes we we could
call the hashmap cassette but that's probably not but Echo strike you know if you want to provide a you know create
cassette service yes uh that mails them to people when they get their song playlist somebody was was telling me is like
cassettes are coming back and I'm like why they are but why they're like like such a terrible format like I can
understand vinyl but like cassets are such a terrible we such a terrible format I don't know they were always so hissy
anyway let's let's make uh so let's so we so what we're doing now is we're basically gonna make a a backwards compatible
change we're gonna make an changing the internal structure right but everything should still work so would I just do
create the hashmap as a field yeah go from there okay you paused was that a yes yeah that was a yes sorry okay I wasn't
sure if it was a yes but yes no no but uh okay yes and final Constructor yep so so here you just would declare map on
the left side you always want to declare we well for now it's songs uh you need to establish what the keys and value
types are that's what I was gonna ask whether we did here okay uh so what are we gonna search for themes well right now
what is our type song. theme or would we do a string it's a string yeah okay right now we don't have a a any other type
for themes other than string okay um now this one we could do string and it's just theme to title uh I feel like even
though we could defer putting song there yeah I think we may as well just do song yeah yeah I mean we certainly could
get away with putting string there but we have song We may as well put song there so go ahead because we're gonna put it
in there fairly soon yeah yeah okay that's where my head was it well we didn't do much but let's run for okay so because
it's multiple well remember we just want backwards compatible so just add the first I I just just quickly do it myself I
was stupid you could have just used the um oh the theme and song yeah but it's not going to matter it's not going to
matter finish what you're doing yeah that would have been cleaner but it's not going to last long anyway it's not going
to last long that's why it's like it doesn't matter yeah uh so remember the the the value is not the title oh right we
just changed it to song or not changed it we right configured it to song all right and so now the the key part where we
actually will want to run method this one yeah so we're basically GNA in a sense completely um oh I just realized
something that's fine we'll figure it out uh we're we're no longer um just returning the song if it happens to match now
we want to basically just delete this the contents of this method and basically rewrite it the whole thing yeah because
it's all based on a structure that we're we're we're getting rid of got it do we want to keep it for scenarios sure it's
a bit you cringing I could tell mainly because our tests are the things that define our scenarios so yeah that's true
good so we the requested theme but now it's a field songs so the way we find if something is in get no no going to
return stream or uh so and and this is what we we're going to encounter in a bit that's not going to work the way it's
currently structured is it Returns the matching song object okay so that this will work fine for the for the single song
scenario but once we get to multiple songs this is not going to work which is totally fine so V uh Y what happened there
yeah that's yeah uh song Y where is needing a return of a list of strings so here the way we're doing it it turns out
song is either going to the song that was found or it's going to be null so we could actually just reuse the code that
you have commented out and right second do we have is no no no no it's old school right yeah just not will know haven't
written okay and then we return list of so right now B theme is returning a list of titles so we're gonna have to
convert that and we'll have to think about going forward do we want B theme to return a list of string or a list of song
we probably want a list of song but for now we want Backward Compatible right so title why does this not feel right um
because it's pretty darn ugly but yeah if it how do we know it's right we run the tests tests so I think there's some
stuff going on with um well it's saying it's getting empty string right so the functionality we had before which was not
uh perhaps clearly defined in uh in our test was ignoring case oh right and we deliberately did make mix different cas
yes right right right yeah did that actually let me look at the run test again so the from there we don't know because
it's not showing us what we were searching for right but if we look at if we go and look at the test that there all
right so we see the B theme has uppercase New Years the definition and it does make sense to make it um case insensitive
so so astd is is suggesting objects require non non- null or else but that's a guard Clause we don't want a guard Clause
here what we want is if we can't find your song theme that's just no results so this isn't really a guard Clause it's
just if we find no results we want to do that um and we're gonna have to do this a different way once we get to more
songs but for now how do we work we'd have to um I'm just trying to should so previously we were doing the the ignore
equals ignore case in the by theme method right it was in here should we continue to do it in here I'm trying to um so
we could make this know because it's ignoring case it's not necessarily looking for lowercase right and so we have to
think about normalizing um how we H how we basically hash our our songs and so we can basically say uh we'll normalize
it by converting it to lowercase and then but here so that would be so we're going to end up having to do it in two
places but for now just to be backwards compatible green yeah is yeah so AST this stuff is going to go away so I'm not
going to be too too worried about whether it's concise enough because this is going to pretty much go away and become a
stream oriented operation all right um but two disabled tests so before we so we've discovered missing so here we have
we've added the song with lowercase and search for it by uppercase but we haven't tested with the song with proper case
like you wouldn't enter it that way or may not be entered that way um and we want to uh and and here's where we might
want to introduce a theme value object um but that still feels like defer that we can defer that a little bit so we
would make another test casing um not sure if that's the right name yeah I'm gonna move that there for a second so we
would do this and then make this or yes but we sort of need the uh the different combinations right so we need like this
combination then another one with this is lowercase yeah so I'm thinking this might be a good you this might be a good
test sounds good should we just do that and get rid of this test parameterize the one above um oh did you duplicate it
yeah I did oh yeah uh yeah so let's get rid of the new one the new one and parameterize Pam so it is um uh we want uh at
parameterized test yeah that one which replaces the at test replaces it okay yeah um and now what we want is it so we
want oh yeah so what we want is on a new line after the app parameterized test we want the value source so at Value
source and in there we're going to have um oh but we're gonna have need pair of arguments right do we can stay the same
we don't care about right but what we're saying is we want lowercase New Year's an uppercase search by theme New Year's
oh right and then up uppercase song lowercase and then equivalent so basically there are four different combinations uh
so we can we do that um can you do more than one value Source well oh but they'll be you can't do them as pairs I'm not
sure if you can do them is string pairs uh is is the question um because we want to actually have two at a time uh and I
don't think you can do that with um with the value Source I think we Source yeah so we have to do the argument Source uh
so change that value source to argument Source okay I just oops no rzy yep uh and our argument source is going to be our
um I think it's a method name let me go up o uh oh it has to be a class okay I was thinking if there was another way to
do it but there's not okay um unless there's a better way to do this could do source can it be inline CSV or is that to
be coming yeah that's why I'm thinking I want to do the CSV since it's really straightforward uh so let's it looks one
yeah I don't want oh maybe that's actually pretty much what we want yeah um I just don't like to support that site
because oh I will hide it I find them overwhelmingly littered with ads oh my edge yeah for them you definitely need an
ad blocker um but yeah we can use we can use the uh the CSV source which will actually be compact enough so let's do
that see what what I never understand is like a lot of that that site stuff is pretty much a regurge a of the
documentation in in in a number of cases so I'd rather go to the source and just look at the junit guide guide doesn't
come up and even the first page of searching which is kind of annoying yeah because um the way the the junit docs are
structured is one big HTML file and so it's uh it doesn't rank highly in search for any of its pieces because it's too
big um yeah which is unfortunate uh so what we want to do is the CSV source is basically going to be uh a bunch of
different value string values so you need to put it surround it with uh curly braces first like that yep and then it's
going to be uh so let's case and since it's CSV it's it's basically just a comma inside the string so the first value
will be our song theme and this and the second will be what we search by so let's um actually let's replicate exactly
what we've got so change the this right side to 31 and now uh create two string method I didn't need to select it did I
control alt parameter uh you could do that sure I'm not sure what that's going to do since nobody's that's actually a
great way to do it cool yeah it sort of pushes it out into nowhere which is kind of funny H yeah introduce parameter on
that one and that will be our search theme or requested theme yeah oh yeah that works too that's the parameter that it's
taking so yeah um so this should pass yeah so at least know we get the one version yep okay um and now we comma here
yeah and you can put on a new idea and don't try to format align stuff because it's not gonna when you reformat it's
probably not going to be what you want okay so let's change that one lower case yeah okay your choice should we do a
bunch of them uh well let's do it one at a time this should still pass right because we're just doing both to lower case
yeah right all right let's add another one uh watch out what combo was in the wrong place so what I'd recommend at this
point is putting a new line after the opening curly uh before the curly Oh I thought you said after the curly got it
after the opening curly ah and now if you reformat it'll look okay I control shift L I think Control Alt L I don't know
what that performance was uh I'm not sure it wasn't Control Alt l l there there we go pair let's see if it's in my
buffer or whoops what do you want to do uppercase in this one sure and what do you want for the second one uh wait let's
run the test so this one will fail okay I believe yeah when I said I wasn't sure if you wanted this to be upper or
lowercase for the second yeah so that one fails yep um let's add uh the the last combination oh really versus making
this one pass yeah because the the next step we do is going to make whatever is failing pass so we want uppercase right
per case lower and this will also fail so it's basically failing when the the the song title that we put into the
uppercase right because it lowers it it converts to lower case the right side I'm so we're saying we're going to convert
song titles to lowercase no no okay this these are not song titles oh right these are themes right and so yes we are
going to interesting not 100% sure I'm good with that but we don't have to solve that one right now uh spring has a
linked case in sensitive map yeah I try not to use spring stuff unless I'm actively inside of spring and we're currently
in our domain and so that means we don't want to use framework stuff here and so I don't like trading spring as a
library because then it pulls in all sorts of stuff but it's nice to know it's there but it's honestly so this won't be
just a map this is actually G to be a multimap so we're gonna have to use a different collection anyway so what are you
not convinced about oh um I think I um I'm thinking I would like mixed case at the UI end right we're not changing the
UI right we're not changing the actual so that'll become clear when when we fix this let's go fix it I think that
that'll make it clear let's go to the uh Constructor no worries astred I'm amazed you you lasted this long so have a
have a happy holiday if you celebrate otherwise have a happy rest of your weekend yeah take care thanks for joining okay
um I must be getting tired too so we're gonna do um so you see there on line 17 when we put the song that's where we
convert it to lowercase because that's the key we never show the key the key never the key is just used for looking up
pass cool nice um let's uh let's commit and I think this is a good place to stop would we commit do you want to um undo
some of the disabled tests or no I we'll leave those as as breadcrumbs for next time okay uh what do you want to say for
comment um uh continue properly handled well we did stuff we properly handle case and sensitive search uh theme it all
right sounds good so so next time uh whenever that is we'll we'll finish uh converting it to multiple songs we'll find
that this hashmap is actually not quite what we need right um because it only stores one song per theme um we'll clean
up some of the song array stuff that we won't need anymore uh we'll get that to work and then we'll be able to pop back
out to the outer level and that should just work should we update our yes we need update anything in here here um except
there's nothing to update anything we want to add or is it uh I don't think there's anything we want to add at this
point where you think of something nope um I mean if you want we could put up up above in the up upper section like
seven and a half uh made search case in sensitive and then check it because you know we're not supposed to search it's
so insensitive okay did I spell it still spell it wrong uh he's it's just saying usually it's a hyphen yeah that's what
it is all right one more commit sure you could amend the commit if you want oh ah I'm already started upated jir I
comment cool and I I don't know what your schedule's like but we'll probably do something next week I think yeah right
yeah we'll figure that out okay so folks if you want to uh continue watching just uh follow on Twitch subscribe on
YouTube if you want a little bit more advanced notice um it's best if you uh join the Discord where I where you can also
ask questions about what we've been doing so you can find deev um one little question that I Miss are we're using
reactive web flux and reactive spring no there's no need to use that um especially now with virtual threads in Spring
boot 3.2 you can just use Virtual threads and again unless you need back pressure there's no reason to use there very
very little reason to use uh reactive stuff well thank you uh full nul for for your your questions and for hanging out
with us appreciate it yeah thanks everyone else for for also participating and ASD Echo strike and suiga and uh all and
tkes and some other new folks um that's it for now stay tuned for for episode four I'll see you then care bye folks bye
