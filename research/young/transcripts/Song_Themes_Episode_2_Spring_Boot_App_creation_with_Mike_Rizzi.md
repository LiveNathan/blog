# ＂Song Themes＂ Episode 2： Spring Boot App creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=S100FP9piGs

---

## Transcript

all right and we are live uh welcome everyone to episode two of working on Mike rizzy's song themes app morning Mike
well this is feeling earlier than I thought it would feel I was gonna say this is the uh I think this is the earliest I'
ve ever streamed really yeah because usually it's at least a couple hours later before I stream but hey this is great
for all our European viewers because it's only 6 PM there as opposed to like 89 midnight so and I did have my capuccino
so you know that should I've got my I've got my first mug of in so uh for those of you who who didn't catch up on
yesterday's episode um do you want to might give a quick summary of of what this app is about sure um I'll just do it
verbally I'm not sure the trying to think do we have the mirror board yeah I just put the mirror board up yeah so I put
a link to the the copy of the mirror board that folks can look at um and I can show mirror board on my screen if You'
like yeah let's just do that rather than me trying to find it um so the app is very um Ted doesn't like to call it
simple so we'll call it um thin on business logic um but it turned out to be a little bit more complicated than we
thought we thought it' be one of those you know fun little experiments but the more we talked about it the more we
realized that we can there is some complexity here and we could add some complexity with future features so the idea is
um I'm I'm a volunteer radio DJ been doing it since college and I've kept lists of songs uh with themes in other words
more like it's a list of a theme so like I have one that's you know on Halloween another one that's on July 4th which is
American holiday um uh other themes you know political uh I'm trying to think about off the top of my head counting you
know days of the week you know there are all different themes you can come up with and I've done a lot of theme shows
over the decades I've been a DJ and they're either written down on pieces of physical paper they're in asky text notepad
files they're in word docks they're in spreadsheets so I've always wanted to collect them into one place and make them
available to my fellow DJs at this local community radio station that I volunteer at and I was like well why not just go
one step further might want make this this data horde uh data available to it feels like a hoorde at this point um
available to the world then if folks you know are curious because there aren't actually that many interesting shared or
public websites that say I want to find themes songs on Valentine's Day right and they tend to be if they do exist they
tend to be here are the top 10 songs on Valentine's Day and they're all huge major hits yeah yeah yeah the ones you you
really don't want to hear anymore right yeah and so whereas Community radio tends to play slightly more obscure stuff so
I thought it would be fun to make a website to share this data and going down that rabbit hole is like well rather than
just being a readon website what about there being the idea of people contributing songs besid me and well should we
just have them just contribute and without any curation or should an administrator like me you know review the
submissions and go yeah that makes sense or no that doesn't um and then we started talking about other features like
well if we had people log in as a visitor well they now they're no longer a visitor now they're a member of the website
they could get some features like um being able to save off a playlist right of what they've generated um or in various
formats or maybe even get fancy and generate a Spotify playlist or a YouTube playlist again these are a little bit Pie
in the Sky kind of stuff but yeah totally totally within the realm of possibility yeah and and I and like I said yester
like I really like the the idea of of you know bespoke apps that that we create for ourselves but that also might might
have use to others and I think um one of the things that that uh is really valuable is is is curation I think I think we
lost a bit of that um because platforms and and money and Venture Capital got got into the mix but um like you know it
used to be that that we have curation and and people have opinions and um this is not necessarily opinionated but
certainly curation and and carefully selected data as opposed to just machine learning which which tends to reinforce
the things that are already there so the dominant theme yeah yeah dominant Paradigm like that like the top 10 list is
like look if I hear another you know celebrate Christmas and so if I hear another but if I hear another Christmas song
that's like the one that they hear every year it's really annoying right whereas you heard some weird obscure ones yeah
that you know that could be fun yeah exactly which is actually literally what I'm working on right now besides this is
I'm broadcasting Christmas day but I'm pre-recording so I can my family so it's gonna have a lot of obscure stuff but
back to the uh themes the one thing I was thinking about when you're talking about curation oh I knew what I was goingon
to say is it's sort of an unofficial tagline at our at my local community radio station is that you know programmed by
humans not algorithms you know and different phrasing of that right you know like you know curated by real people that
kind of thing smans yeah we're getting Chinese food for Christmas that's that's our deal so me we can find a place
that's open um so what uh so what we're seeing on the screen we we basically walked through this yesterday this was uh
our um attempt at doing event storming and if you want the detail on that we're not going to repeat it that's why we
record the stuff so you can find it on YouTube um and uh this last one was where we we ended up with and and starting to
think about our entities and objects uh and Aggregates and and so on um and so yesterday we basically started coding um
so should we pick it up from there we left ourselves I think a good Redrum yeah I think so I know offline yesterday
afterwards we talked about um I was saying oh you know I feel uncomfortable with the fact that we have all those
different um different names for the same thing in our ubiquitous language another words we're violating the rules of
oquit language which is you know select a name and and you and I said yeah we should you know talk about it on the
stream not offline and I was like yeah it's a good point but I realized this morning you know while showering of course
that's where all the best ideas come from yes is maybe we shouldn't make that an explicit task maybe we should as we
bump up into it in the coding back to you know jit you know just in time decision making right um let's when we're
figuring out stuff it's like okay now it's time where the rubber meets the road let's make the decision yeah I I don't
think I I intended for us to to force the issue I think uh oh no it was it was me that was think actually okay yeah no
it was totally me thinking that and then I was afterwards I was like no let's yeah let's have it come organically I
think organically you know that's that's best yeah because um I mean that is the advantage of sort of coding with with
the with the customer in the room right and the customer being also a coder so we can we can basically be more
irresponsible and choose this stuff at a later time even uh last even a later responsible moment or something something
least responsible or the most irresp anyway we can choose we can choose later because we can always rename if we we bump
into it and I think that that is something that that still happens even if you you know you come up with you because you
may find as you're in a sense speaking the language more using the words more in the code because that's where it's
really going to get a lot of exercise you may find it to be really awkward um I mean I found this when I was work on
Embler I'd originally called called it a huddle which um the original first name I started with was session but that was
like really generic and that was that was not great uh and then I used huddle but then that word started having a
different meaning in our ensembles as a hey let's get together and just chat before we continue coding and so changing a
two Ensemble which is really what it what it was um happens right and and thaten happens in in the real world so so yeah
I like that cool I've got the failing test up on my screen yeah um so one thing I want to to to ask you is uh um I've
been navigating and you've been driving uh so when have you thought about switching to to navigator and when you want
want to do that so we're not being as strict as we might be in like an ensemble um so I'll leave it to you to yeah I
think let's let's continue with yeah you navigating it first um okay and then we'll when it feels like the time I'll
I'll speak up okay H you'll want to move streamyard off your screen yeah I know sorry I do that so I can look at the
camera more okay so got a failing test we've got a failing test uh so what is this test right here right so what we were
doing yesterday uh the first test we had written was sort of uh a bit inside the sort of what I would consider at at the
at the use case or or hexagon uh part the application layer as it were where there's no concept of IO or framework or
anything like that um then we decided to move all the way to the outside and start creating the uh the endpoint uh URL
for for how we're actually going to interact with with the system so we wrote this test this test passed um but then we
flipped out to our MVC test and that was test so let's go make this test pass uh uh because it did fail failed as
expected with a with a 404 um so let's go ahead and create our controller class uh I think we already have a controller
class did we create it oh we did okay oh right that was our our stand standin uh uh let's just call it homepage
controller for now we're going to get rid of it um but it's have and then we can we can close that anymore uh so let's
create our our actual thong thong themes controller so what you can do is um you can actually go from the test and hit
uh whatever the shortcut is to jump to the other thing jump to the other thing I know that was not perhaps not not
specific enough um uh it's called go to test subject so it's control shift T yeah control shift t Okay uh oh really it
didn't I expected it to offer to create a class but I guess it's outside what if it's I don't think that's G to matter
no so that's really funny so so this is where like intellig expects you to create the class first and then go to the
test and since we're doing tdd we're going the opposite way and intelligent saying I can't find a controller that
matches this and doesn't offer to create the class which is what I what was in my head so okay we'll have to do it the
we'll have to do it the hard way um yeah so let's go into the project and create a new class but it's funny that that
was like in my head because that's right I thought it would work actually I you know I'm going to suggest that that
should work I'm a I'm a good bug Filer and issue issue filer so I'm gonna remind me to do that all right um let's just
call controller sounds familiar yeah rings a bell okay that pull down below and so let's see so we're expecting this to
uh accept a post at that endpoint um so let's uh add an annotation to the controller did you say app controller no no
sorry the at sign and then controller so the word controller not nothing app yeah that one uh and then uh let's go and
uh we'll create a uh let's see what is it going to return it's going to return to redirect string upper Cas oh I see got
it yeah uh and let's open body um let's see so we had the test fail for the right reason let have it fail for a slightly
different reason so let's string that okay yep and then let's put an annotation on the method so six and a and that
takes a parameter of the URL string so that'll be a string with Slash theme- seert so to basically to match test all
right um and as always I'm going to be a little stickler for whites space so if you could put a space seven and a half
awesome uh all right let's run this test now before you run it uh we expect this test still to fail because while it
will find the endpoint hopefully uh the return value will not be a redirection so instead of the 404 we got before it's
just going to be a status code in this match all right let's run it okay so while that's running would there have been
in value in doing a test without The annotation post mapping and how Force us to do that or is that a bit too micro it's
it wouldn't have appeared to be any different in the failure because it still would have been a 404 so it wouldn't have
told us anything uh about what um it still would have been a 404 and so the test would have failed in in the in the same
way same way yeah okay anything you want me to look at in here uh so one thing you can do is uh turn off the the word
wrapping the line wrapping that's on the toolbar all the way on the right below the up and down arrows so there an up
arrow and a down arrow and then the third one there yep off the soft rra so remember that where that one is because we'
ll be turning it on and off okay it uh so let's scroll down a bit there we go so error resolving template expected
necessarily uh okay that's fair so what that's saying is we returned an empty string um so it expected us to be
returning a Time Leaf template and then it would generate the HTML and return that even though that's not a good idea
for posts um it's still what it expected so and what's weird about that though is it didn't we weren't returning a
template for the old version right the old version being homepage controller right because that was a rest controller so
what rest controller does is basically not bother with any view Technologies like time Leaf it what what you return is
what the what's what gets sent out got it and that's the main difference between rest controller and just a regular
controller um all right so let's do uh uh return a redirect colon slash as that pass what was it again sorry uh colon
and then a slash so it's basically we're saying redirect this slash you can also return it not as a string you can
return it as an actual class called a a redirect view um I like strings okay I think I just find them easier to easier
to work with easier to test all right uh if all goes well this should pass because we're just checking as to whether we
get a redirect not whether checking where it redirects to commit what what do you want for text um uh you can just say
uh added theme uh yep well that sticks around for a long time doesn't it it's almost like it's stuck on there I feel
like it's stuck because it should only last for four seconds yeah that's weird let me try clicking somewhere does that
make it what do these three dots do oh there's settings oh interesting is that new or is that I just never noticed it I
wonder if there's some additional keystroke you hit that cause it to stick around to stick around yeah play with it
later y all right um it's funny we could we could actually deploy this uh but we don't have anything that does the post
so it wouldn't wouldn't offer us anything uh um it would make the the live website look funky no it wouldn't it wouldn't
it wouldn't change anything oh we still have the home controller the homepage controller if we did do a post to this
endpoint which we could we we'd have to do it programmatically using um either the HTTP client inside of intellig or
something like curl but we could do a post and all it would do is redirect us back to the homepage and that would all
work right um I don't feel the need to do that but but it is one of those principles of sort of always Deployable which
which it is all right so what do we want to do um so I think uh so the typical sequence I follow is um uh an MVC based
test so a framework test and this basically makes sure did we set up the post mapping with the correct URL and that it
has the right annotations and that we actually do a redirect uh and now we can um go one level deeper which is a direct
nonframework test against the the controller hey weo you know what we're gonna do next uh so let's let's let's do that
okay so what we want is um actually if you go into the controller bottom y uh and then from there uh go to test oh nope
oh that was shift T control shift really you know did they break something T because control sh there we go why did that
not work before did it not work because you weren't inside the class I think I was out here let me try it again outside
the class yeah oh that's interesting so it needs to be inside the class huh I don't know that it says zero CL though
says choose well that's but that's expected right because um what it looks for is it looks for test classes with the
name song themes controller in it right right right right which we have none we have a song themes mvt test which is not
which it doesn't know how to connect yeah um but this is perfect because what we want to do is we want to create a new
test class so let's go ahead and do want yeah we don't don't want it to generate anything else top all right and so let'
s go ahead and test hey dark mode sorry welcome to the light mode stream we only do light mode here yeah we just keep it
dark in our souls um so um I'm so used oh my God you got me right after having coffee what was you um sorry you gonna
say something useful what yeah no I'm so used to using my own like at shortcut for using test but we're not going to use
that going forward the at rzy so what's the more generic way of uh so insert I'll insert got it and it keeps asking G it
five okay yeah sorry I I have to I have to reject the request since uh we're pair streaming I I need to turn off the
ability to redeem dark we come all right your um I'm just gonna try something on my method autogenerate the junit 5
thing uh no that's fine it's I think throwing exception yeah I wonder if you modified the existing template um which is
totally fine because that's that's my def my default but um we don't need the public anymore we we can fix that later
you sure you said that last time um oh did I all right if I say that twice then we need to fix it so let's go into uh I
presume in here somewhere yes um and I let's look at file and code templates it's alphabetical so F and code templates
um I think it's going to be under the code tab at the top so there and look for junit test junit 5 test yeah oh you must
have modified it so that one that's little in blue that means you've modified it ah um let's let's modify it by just
dropping the what Darth tedious what was plag Darth tedious yes that's that's my my my Darth name is tedious that's
hilarious um all right uh let's get some practice at that so let's undo the test you wrote yep awesome um so this one uh
we would like let's start by having it redirect to the right place um so um let's see results all righty uh so let's go
ahead and controller yeah uh you only need to do new first yeah I know I was brain part now you can do the dovar there
you go um and there there is a postfix to do both uh that I have at some point we'll we'll set that up for you ah so
it's a custom one yeah so you do envy and it basically does the new and thear that's so it's like I don't know why
that's not built in we do that so often right all right song themes controller or controller or something else I I like
the full name because you know we're in veros uh all right so let's uh that's our um that's our setup so let's go method
and we'll get we'll hold on to the results of that so Barrow it up and that will be uh page yep yep all right and we can
go ahead and assert uh assert that redirect page not DOT parameter thank I thought we had turned on uh automatically
import on a unambiguous Imports on the Fly we did uh look for uh unambiguous yeah it's an easier word to find um yeah
it's there it is it is turned on uh wait a second there oh that's for Java yeah huh I wonder if there were was there
more than one I don't think than one uh that one is is somewhat annoying so I I leave that off what it does is uh if you
if you did an import and then you stop using it it's still there until you uh basically do an optimize Imports manually
we have optimized Imports at commit yes and we have that on Commit on Commit it's I used to have it on but then like I'd
stop using something and then the next thing I know it had removed it and then I had to repport it and it was annoying
uh so I leave that one off um so that looks okay I wonder why it didn't automatically import it all right let's will
because I like long names and I don't like VAR that's why uh but you knew that okay so we want to say is equal to and uh
yep and we'd like the string uh redirect colon slash um what do we want our URL to be to songs results search results
song results songs um well we the name of this test is search results we have theme search as the name of the post
mapping I think search results okay we can always change it so so this this is the URL that will appear in the search
bar and that we'll um that's fine that's not let's not sh it okay because I want to know what you're thinking I'm
thinking it is not necessarily indicative of what you're looking at but it is search results and I don't want to make it
too long so you're saying that's too long we're on the site song thematic so what else is it going to be so I I think
it's fine uh it may end up being the theme theme search results once we have a different kind of thing so yeah let's
maybe let's let's tack in theme search results not terribly long we've certainly seen longer URLs in our life I mean we
could just say theme results are there any other there does yeah which okay it's for both but yeah all right uh let's
run it we expect it to fail because the strings don't match U but let's just run this this test just this one okay just
this one um pretty soon we're going to need to set up our uh different groups of tests yeah okay so that failed for the
right reason all it nope yeah it doesn't go interesting says display for four seconds that's so weird I wonder wonder if
there's something about mousing over it while it's displayed that you're unintentionally doing that maybe all right well
let's make sure we pass hey end funter zero uh so we actually already wrote our our spring MVC test to check for the
endpoint and the idea that uh the the scheme I follow is I want the fewest minimal minimalist tests that actually use
the framework because they are slow and so I want I don't I could here in this test there on the top we could check for
where it redirects to um but that would require me to run this test if I change that and I since I can check that and I
can call it directly against the controller um I want to do faster maybe that that is fairly non-standard I I feel like
I'm the only one who who does that you're gonna say something oh I'm wondering if maybe that means it's the time to to
break out fast test from slow tests should we do that now why not all right um um you know the question came up it's we'
re talking about it it's on brain stack all right so let's go ahead and do that um let's uh let's put a a tag on this
test so uh 11 and a tag and inside that we're going to put the string um I used to put integration here but I don't like
using that term anymore uh what are we using over in blackjack I think we're still using the tag integration we're just
called it IO based tests Hey swegi what' you Miss uh whole bunch of stuff no not that much we got our test to pass from
yesterday um let's uh uh so where it's gonna be annoying is when we actually have to to reference these tags it's
annoying to have special characters and spaces um but we can shorten it we can basically say this is an IO test so
lowercase yeah I'm fine with that that whoa and not the I think my brain is like going but if I have to GP IO you will
never have to GP iio I'll never have to GP it so yeah okay if you would ever GP it it would be in the context of a tag
which means it would be the only one okay yeah we could so suiga mentions um I'm going to basically put it under the
general category of IO uh all right so let's go to the other test the songs test uh that one actually that one will'll
leave untagged yeah because basically um the the io free tests are just ones that don't have io on them do tests that
one is also io3 all right so let's go um set up some run configurations oh thank you y I know you like that uh so go to
edit configurations at the top here we go and wider um so on the left side select the themes and uh let's uh do two
things so let's change the name uh this one will be our iob base slash you want the word base yeah uh but based like
that yep uh let's click on the stores project file there on the done and uh under build and run below where it says all
in package drop that drop down down uh tags and then just put IO apply and let's run that just to be sure that it works
properly all right so that run the right test just open up the for now um the check the check check mark yeah okay so
that's our MBC test perfect okay Pig we l you got it backwards we put io on the ones that are IO based and untagged um
all right so let's uh go back to the Run edit run configurations um let's go ahead and uh up in the top toolbar of that
window there's a duplicate button the third one in yeah copy config and so we'll call this one IO free I just got a
feeling that you prefer it aerc case like that is that true I think it just shows up better but it's it's fine I just
wanted hard hard and fast R all I was trying to read your mind oh okay and here we're gonna instead of IO yeah stores
stores project pile and default is fine uh and then for the tags you're going to put an exclamation point in front to
basically iio and hit apply and then let's run that and that should run the two other test classes uh oh let's go into
the the uh applications one the one the context it no you need to jump to it t yeah now click click in there it and
click on context loads yeah uh let's put tag uh the io tag at the top do you do it before or after no no it's on the it'
s on the class oh was in the class right you do it before or after I do it after because I want the yeah okay so let's
try it again to make sure that we got that oh yeah we could put none in the tag selector um I think I had a reason for
that but didn't uh all right so that is our two IO tests uh sorry those are two IO fre tests make sure it's still just
that and make sure it picked up both of those gotta run it though probably did so selecting it does not run it unless
you I know I know I thought I I pressed it all right so that ran both that's that's great commit now uh and we can say
added tag run configurations we actually did more than that right didn't we add some we um oh we also added the the
controller test yeah we probably should have done fine and some controller tests uh and uh yep awesome uh so inter
functor zero says as always the view that writing integration tests for adapters seems to make them break less often
Break um so even though the controller is in hexagonal architecture an adapter class it doesn't mean all your tests have
to be integration tests so the way I do it is if it's something that is basically around configuring the framework so
post mapping endpoints redirection um maybe default parameters so things that you would not be able to test with just
directly instantiating it those are going to require the framework workor and then those are basically iob based tests
anything I can do that does not require the framework I will do without the framework but I'm still going to be and so
most likely I end up with a bunch of test against the controller that are IO free that don't require the framework so
I'm just saying given these parameters it should do this stuff call this service on next is so we've got our song
Searcher um so I think the next step is uh connecting up to our song Searcher even though Our Song Searcher doesn't even
though a song Searcher doesn't do up um so how can so what we need to do is we need to tell we need to be able to
observe that when we do a post request to the results so my default way of doing this uh is basically give it the song
Searcher and then just expect that uh uh that there are empty results one could use nullies but I'm um and what's your
rationale for not doing Nobles um it's not my habit and so uh I'd have to go and remind myself how to how to do it um we
can talk about if we want to do that uh at some later Point sounds good um the other option is we could we could mock
song Searcher and force a return value of that and check that that's what we get uh but I don't want to do that because
I don't want to use MOX yep at least not my keto MOX um so let's go um let's create a test that uh it's going to be
somewhat similar to Our Song Searcher test uh in that we're going to do a a post and we're going to get uh basically
empty results is this where you wanted to test yes thought I heard you say it here but then okay so in the name was post
name so how do we want the search to actually work um specifically what do you mean well so we did it as a post because
that's that was my gut reaction but I correct um because we're the post is isn't doing a state change right uh it's
actually a query request and in fact that's typical to do queries as get requests because that's really what a get
request is so I may let us down the the wrong path here right should we instead of writing this test go back and change
the existing I think we need to go back and and so so the the reason you might use a post request for a search is if
there are a lot of parameters and by a lot I mean like a couple of K's worth of parameters um that's not the case here
at least I don't think it is right it's gonna be themes so that's like maybe five or six or even 10 is not going to be
that much for for get requests so all right T like a lot I I would yeah I mean that would yeah yeah um all right so let'
s let's go ahead and delete this test um and in go so let's go change post search R redirects actually we'll have to
start from the outside again let's go to uh thong themes MVC test and this is going to be instead of the post you're
going to use get uh so we'll just say uh get and it's not going to redirect it's actually going to return this one we
just want a 200 uh we can just say get to search and endpoint returns 200 okay oops get to search endpoint yeah since
that redirects okay yeah God I hate that the zero and the O next to each other does not roll off you could if you want
we could drop one I was just know doesn't off the T that way I'm fine just 200 that's yeah on that uh all right let's
change our our our get our post to get and our status to uh you'll need to import that Gap I know I hate this is this is
why I hate ham Crest and this is why I hate these is because it's all static Imports that's really annoying uh and so
here we want status dot uh is 200 uh we can just do the 2xx successful that's sufficient basically that means any 200
series 200 2011 202 is all gonna all going to be fine um let's run our iio based test and this will Now fail so we're
still doing tdd this test will fail and it'll fail because it doesn't 415 so it did fail and 405 right 405 415 is a
different one so 405 basically means you're doing a get and all we know supported uh so carore asks are you now turning
it into rest endpoints no these are not rest endpoints we are not doing rest um we are doing server side generated uh
HTML so these are all uh web tests but you expect if you go to a web page and you do a get you get a 200 so what this
tells us not necessarily that anything worked or didn't work it tells us that the endpoint is is correct right because
again this is about the configuration of of spring that we've configured it correctly um which we haven't so let's MH
send me somewhere so let's go to our mapping uh and in terms of what will return this one will be a little trickier uh
if we return an empty string we're going to get the complaint that the time Leaf template doesn't exist but let's do
that anyway so at least we'll get a different error run the test and run the tests yep I expect a Time Leaf complaint
yeah and I see time Leaf in there so let's scroll up and see what it actually template and what what's very clear is
even just with two two of these tests that they are much slower you notice how slow they run even with just two yeah
yeah there's a certain amount of of startup time that over um can cut across multiple multiple tasks but yeah it's it's
it can be pretty slow yeah and you gave me a Next Step Direction but I missed it uh I didn't um other than we need to
create a template ah so let's go uh open up the project window under um resources there um and let's call this them-
search- results actually lower casing yeah I use I use lowercase for my HTM file names yeah now what was the name again
themes HTML uh we can call the title theme search pun and just hit enter to get out of that yep here and let's just say
songs let's put that song in uppercase it's going to annoy me if it's a lowercase okay um so now we have the template um
and now uh let's go back to our bottom uh anal it's return theme- search and uh T will probably autocomplete it maybe
don't we want to say themed search results yes Dash results yeah but without the HTML so this is BAS yeah so now it now
it recognized that exists um uh and I think right um G to say do a commit but I'm feeling like I want to fix the commit
sure that's this one yes let's go to that one so let's rename the um the test right um so so it's no longer going to be
a redirect uh here we can say that it just Returns the Right View name so get search Vue and let's rename the variable
so on 13 the variable name ah uh let's leave the string there because we should expect it to fail right let's not let's
have it fail and tests all right that fails expected so commit um realized our mistake we need to have the right
committed so top of the hour should we take a break yeah actually is a good good good opportunity for a break good time
let's take a fem minute break and when we come back we'll uh start connecting our controller up to our minimal service
implementation cool all right see you in five yea all right um so what should our next step be we've got our view
appropriate and now we want to hook up our controller to our Searcher so what are your thoughts on on um a slightly meta
thought okay I was thinking about this again this morning um I'm definitely not even though we've only written one issue
in the um in the uh GitHub uhuh uh I'm thinking of I find it a little bit unsatisfying to have and go create an issue
for just some simple things so I'm I'm thinking that it might be nice to start out with going back to the simplest thing
that would work and just start with a plain text file at first and then when it gets to the point where we have issues
and people suggesting enhancements and that stuff then switching over to sure to using issues um because it might also
help lay out I was thinking this might help for viewers as well like these are the steps we're taking or have taken
right um so it might be easier for folks to visualize what we've just done versus what we're going to do um I don't know
what you think of that idea that's fine um uh one thing I realized is that um I think that first issue we created was
not was I I tend to think of my issues as being more stories right uh but we created it very much as as a as a very
small task yes pretty pretty much a single test really right um but I'm I'm fine not using it like I'm I'm not really
not wedded to it and so yeah I mean I'd like to use it eventually I think but I think as it becomes more when we start
working at at level at the higher level sure um to switch yeah so if we did a simple text do yep I would put it at the
just the root of the at the same level as the read me oh where is that or maybe even create a readme I don't think you
have a read me there's help yeah so at that level I would create the file you could just right click there and say
create new file yep um I don't want to use the word Mission because it's not really a mission but you could use Mission
because it's you could say stories tasks themes I don't know I'm gonna go with Mission I think I like it all right it's
not really a mission backlog no I don't want to be backlog either I'm deliberately trying to make it not story like um
I'll show you what I mean I think I think Miss mission is fine um can always back backlog where things go to die you
know what you could call the file name jira yes let's put it into jira and it's a text oh we should do that if you don't
do that I'm G to do that on my own thing because it's that's too funny yeah let's it's a text file okay let's see can
you rename a a file from or do you have you have to do it from the I think you have to go to the you you might be able
to do it if you're in the file but I think you have to go yeah uh there you can just hit shift F6 I was wondering if I
could do shift F6 okay perfect I don't think the haha is needed yeah now if anybody asks do use jro you can say yes it's
a text so what have we done so far let's let's you know want to get the the dopamine hit of check boxes sure um um let's
see can we can we reconjure this without having to watch the video well I think so the first thing we did Searcher um
yeah basically song functionality so actually create song Searcher uh initial by theme or I I don't know I mean it's
sort of funny to sort of backfill it to do I know I don't know what our intent our intent was to basically create our
our start creating our our use case but we're certainly not done creating the song Searcher right maybe we won't
backfill let's just do going forward can we unless you unless folks think there's value in yeah I don't I don't know uh
because I mean we could put as a as as basically a to-do create the song Searcher create song Searcher uh that can
search by theme and then we're not done with it right uh and then um and we'll probably have sub things under that uh
but then we can say uh create um get endpoint for for theme I think that's a top level thing yeah I was thinking that
too I just it auto jumped it AO on me if you put a if you put a new line it won't do that create get inpoint for what
was it you said again uh for searching by theme I hesitate to to keep saying by theme since that seems like it's implied
but it will need to be different later so that's fine uh an end fun here says wouldn't the first thing under create song
Searcher online five be uh can find a single song actually our first thing is that uh and then the next one is finds a
theme and then we can the next one would be find multiple songs that matches the theme and so that's sort of the the
query side app and so under the create the get endpoint we can since that's not really done um the first step is then
sort of somewhat mirroring the the with single song so those those those are work to do they will require us to write
some timely right there's a lot of stuff coming in chat now um so I generally so so uh the first value for the user to
find one song um we still need to be able to find no songs uh because that's simpler and so uh eventually we do want to
find one song but um generally I I I think about the zombies case because it's easier and less code and simpler uh
mainly less code to to return nothing than to return something um so that's that's the the that's my flow in general
unless it's unless there's unless it doesn't mean anything to do nothing like there is no zero case sometimes that's the
case uh but gener but especially for queries returning nothing returning one and then returning many is is a is a flow
um I think that's now I'm just going to look at the tests and the code to see if anything else GL why did I make that
plural uh that's the default test I would just close it we're not going to use it you want to get rid of the plural and
the name um you usually do tests or test singular I since that's autogenerated I would just leave it oh that was
autogenerated yeah that's the okay yeah it's interesting so so recently uh I don't know if you saw this Mike uh Kent
Beck posted an article about you know sort of tdd Cannon um and one of the things he mentions which he does in his PDD
by example book is sort of this punch list of of of tests before he starts writing a test he'll he'll he'll note down a
few tests that he's planning on writing um and it caused a bit of an interesting discussion among those of us who don't
do that uh so it's like so wait am I doing tdd if I don't create that list H um and so uh at least uh goo Hill got got
the explicit no you're still doing tdd from umbrella um but it is it is nice to to to do it um to to create sort of a
list so so you don't forget anything and as things come up you can put it on the list and then uh decide if you want to
do it once you're done with other stuff so yeah I think to add to that like I wouldn't go much farther than this yeah
right it's not like I want to create like all stories that we can think of right right it's definitely keeping it too
yeah close to the Horizon yeah um uh we so number 10 we've kind of done um although we cheated because we didn't
explicitly display there are no search results so maybe we want to add that so we are returning an empty page I think
that's fine um but I think we want to add one more which is uh results because because that's different that requires us
to to write a little bit of of time Leaf code as it were to do that uh sender fun zero says the test list is especially
useful in pairing sessions yeah um yeah example mapping uh I don't know if you saw we did we did the we did some of that
sort of as part of our event storming um although we didn't explicitly do exam um we'll probably get to that once we get
more into into the searching yeah and yeah it's always good to have a a place to external memory yeah it was actually
yeah and I guess another way of thinking about it besides the witty name of jira it's almost like um it's almost like if
I was coding solo a place where I would throw a sticky note right like on my monitor right right right or I shot it down
in my physical notebook yeah right yeah some don't want to forget this but doesn't have to be too far into the future
yeah okay so do we want to continue on the song Searcher side or on the the endpoint side um I think since our intent is
to hook up the uh the get request to our minimal service class uh we probably okay so it's not going to be an MVC test
for the most part we're done with our MVC tests um we may pretty much one of the things that that in my experience I end
up with very few MBC tests uh pretty much one or two per end per end point and since we've got our endpoint now we can
focus on the the controller test um all right so let's go to our controller for um hey it didn't ask for J five that
time that's interesting that is I wonder oh probably because it already detected that you were in a test class that had
J unit five ah right yeah so it already knows that yes 11 um file rename is that what you're saying jir 11. txt no
because it's line 11 that we're doing oh so that's the issue is is what line number in the awesome uh so for this one we
want um search returns found um trying to figure out how to say this without being sort of redundant because we what we'
re saying is that the model has an attribute that says no songs were found when no found I don't know how we want to say
that do you want to say the word attribute at the end of the name I want to say the the model has has uh the model has a
no songs found attribute model has a no songs found so like that I think has sounds weird there so how about with
returns models with yeah no songs found that welcome Joyce beast from the UK and I think we might be cheating here as
well but that's okay uh this will set us up for for the next test um so let's uh so you can I don't think we're going to
copy and paste anything so we'll just go controller look at you with the oh oh yeah you can't you can't do that you have
to let it autocomplete first but that was excellent use of of camel case I do that yes then right yeah okay perfect uh
so now we don't care about the return value what we care is that uh it's going to accept a model so let's uh let's
create a model so uh the class name that we're going to declare is model uh and the variable name will use is model as
to that one is it going to use fra spring framework UI model uh yes but that's fine okay that's still a Nonio test
because it's not doing any IO um so don't do new um but you want to import the right one oh enter which one the second
one uh in fact you know what let's do something to optimize your your your your work here uh so undo okay and now nope I
can redo oh so you want to have model there y uh what you want to do is um when you do Alt Enter um the second one so uh
go down and select the second one but don't hit enter but the second one is is the wrong one so what we want to do is we
wna we NE we like never want to instantiate this we never want to import this so if you hit the right arrow wow on this
line yep yep uh we can say exclude um and we probably want to just exclude certainly exclude logback core model so go
down one and select that hit enter so what this does is it adds to the ones that you want to exclude from Auto Import
and over time the the more you do this the more the add unambiguous Imports on the Fly will just import what you need
got it sweet yeah so now if you if you sort of back oh um and if you hit if you hit space it would have Auto imported it
but you it I see yep uh so model will be our name and that's going to be equal to a it uh so carmar asks is the name of
the first test still correct get search um we might want to drop the word get but fine um and so now when we call the
song themes controller theme search method so that uh we're going to want to pass the model in as a parameter that will
cause refactor add yep just refactor guess that's becomes a change signature um on line 15 since we just broke that um
uh let's go ahead and just create that variable so you can copy that line yeah I was wondering if you're gonna do pass a
null I was thinking about that but then that's going to cause a null poter exception and there's no reason for that so
let's just do that all right um while we're here should we take uh karmar suggestion rame uh yeah let's drop the word
get from the from the front of that test method name okay I mean technically it's a get but at at this level that's sort
of not relevant yeah thank you Kor um all right so let's go back to our the test we were working on and so what we what
we expect so this will be our our attribute can't figure out why that pop up above but I'll get that oops nope not that
one yeah there's some setting i' I've turned that off where it pops up sort of what are the possible what are the
parameter lists uh that are possible I don't remember where that is in my settings um and so what attribute name uh so I
was thinking we could put in the attributes song's not found um but it would be a Boolean and I generally don't like
naming booleans in the negative oh so what this is going to be is this is going to be a key value pair in the model
which is basically a map um that we can then uh test for uh in our time Leaf template so we'd say something like time
Leaf th if attribute name is certain value so we could said just say um so instead of just saying no songs found we
could say uh songs found is a sort of a account and then Zer and then set that to zero ah okay versus an attribute named
Zero songs found yeah which is not a negative that's that that would not be a negative uh one one could say yagy right
we don't need the song Count yet right I was just about to say that um but you have a butt you're about to say so tell
me I kind of feel we do any we're GNA need it like pretty soon like as part of when we display them I well actually this
is a customer question do you want to see how many songs were found do you care about the number um realistically I don'
t think I do it's a good question all right then let's not then let's not put it in yeah um so we either put something
like zero songs found and that's true or we put songs found is false or found songs would be false I thing with found
songs to me that's the name of a list I mean it could be viewed as a Boolean but it also could be viewed as a list yeah
yeah here's the found songs that's a good point karmar one sorry that one yeah well at some point we might have to worry
about paging if we get too many I tend not to like paging unless it's really a lot and and really slow um because I hate
paging uh but I hate infinite scrolling worse so we will not do I we will not do infinite scrolling I refuse to work on
a project that does infinite scrolling that's my that's my ethical stand um so what variable should we use here what
were the nonf founds see this is that popup that's still even though I've got no popups it's an app I'm no longer using
I should just uninstall the app but I'm just surprised it's fting me so suiga suggests uh empty search results result
yeah that works okay I like it make it SOI make it so empty gotta spell it result uh and then we're going to assert that
that is equal to um do we use the string to yeah I was wondering how that comes across well it's up to us uh because as
far as the model is concerned it's completely untyped um let's start with a Boolean and see how that works and if it's
if it turns out to be awkward in our template then we can uh so let's do Boolean dotr because that's what we're GNA want
uppercase true yep oh screaming caps yes because it's a constant right right is I always have to I uppercase as an
instruction sometimes is confusing because it could be do you mean just the first letter is uppercase or all upper case
um if you had trouble figuring it out we would have resolved that yeah yeah all right uh let's run it and this will most
certainly fail shouldn't break the other tests because the other test isn't concern with the model um but this will fail
because the model doesn't have great all right uh let's we could do we want to play the um pardon me is saying no we
don't need to play triang yeah I don't think we need to do um now we need the Searcher uh so let's um go and uh create a
a Constructor in our in our song themes were um is there a create Constructor yeah there's if you're inside the class
insert there we go yep and so that Constructor we're going Searcher and then you can go ahead and and have it generate
the field for that Enter yep yep um and even though it's not required let's go ahead and and put uh uh on 11 and a half
let's put The annotation right so so spring is complaining that it can't find a song Searcher for automatic uh wiring um
from the tests we're going to be working with we don't care about that but this is where we have the the configuration
requirement for um Bridging the Gap between our Pure domain which is song Searcher and our adapter which is the
controller so we can't so what what spring would like you to do is just make song Searcher a component that becomes a
spring component right we don't want that that because that infects that violates exogal architecture and our separation
of concerns uh but that's just a warning from intellig it's not actually a compile error so we'll we'll be fine um
although we do have a compile error because now we've got in our uh tests we Searcher uh yes this happened to me as well
when I upgraded ensembl removed all my autowire annotations and I was upset um and you can turn off the individual Auto
auto uh all the individual basically recipes that it runs um and I didn't do that and I was kind of annoyed by that even
though I know that that's quote better um I still don't like I'm I'm okay with the a level of magic that's in Spring
boot but yeah all right uh so what should we do here what do you think we should do here we have a couple of choices we
could pass a null um or we could just pass in Searcher I'm leaning towards new song Searcher because if we pass in null
it's gonna blow up really soon yeah so we're gonna dreference it pretty quickly yeah so we could create a null object
but right now song Searcher is we're eventually likely going to need to uh um yeah I don't know that I'd even bother
creating a variable local variable for it oh yeah you're right when we when we encapsulate the setup we might need to do
that but for now we don't um and we'll need to fix that in the other test method not sure I agree with it uh he's
talking about the open rewrite dropping Auto reite auto uh autowired yeah we could have done the introduced parameter
should we do that should we back up and do that let's do uh is this where it go let's see uh so let's go into the
Constructor on the bottom um let's drop the parameter just delete it and delete the assignment oops uh and so do uh uh
no no you want that um because what we want to say is on line 15 we want to say this. song see and now we can take the
new song Searcher part so just a instantiation and introduce parameter so here yeah contrl shift p nope no control alt P
Control Alt P yeah drop the number one oh hey there we go there we go thought I filed an issue for that maybe I have to
go back and look and see what the status of it is all right uh so that should have been a pure refactoring which means
all of our you okay sorry what were you saying uh let's just run our tests run the io free tests so they should still
pass because that was a pure refactoring right uh oh actually I forgot we we we technically yeah we technically should
have done that shouldn't have done that right I am personally fine and and break protocol if there's one failing test
that that we know about um so I am fine with that uh but pedantic maybe not even pedantic but proper tdd we should not
have done that um okay so now what we can do in our uh because now we want to make our test pass so let's go and um on
19 and a half let's actually use our song method uh by theme ah by theme no no no y um we can pass in an empty string
here eventually that will not work but for up found songs uh sure since we talked about it recently yeah yeah and so now
what we'd like to do is uh um if that's empty we want to add model away hello I think if you hit Escape it might go away
there we go and then we're going to do what again you add an uh so we'll add an attribute attribute uh and then whatever
we named it in our in our thing and then oh actually I guess we could just say Uh Oh you mean we could drop the if
statement and just put is empty as the of more than we need but I don't think we need to be that that precise so let's
so grab the found songs as empty uh expression so that and then go to the end of add attribute and put a comma sorry
before the pr and then paste it and then complete it uh and then if and there we go yeah oh chat's getting Lively yeah
so um this would also work then for saying that empty search results will be true when we do return stuff I don't I don'
t think that's terrible um we aren't we'll end up testing both sides and so we'll get a little bit of functionality for
free assuming that's what you're referring to uh hey there uh you Belle um is adding conditional checks in a controller
a good idea so if it's business domain logic then no it's not a good idea if it's mapping knowledge that's in the domain
into something that gets presented through the controller that's a mapping that's not domain logic so domain Logic No No
doesn't belong in controllers mapping logic where you may use if statements say if the domain has this stuff we want to
display it as this um that is mapping uh and that is totally map yeah I think we could have you know if we wanted to we
could have triangulated more precisely I didn't feel the the need to do that um all right what do we think ready to run
the test yeah that's what we were thinking about I didn't feel that that was necessary true right one of the things
about tdd judgment all right um yeah I mean definitely when learning tdd you want to triangulate a lot but then I think
even in the K Beck book he even talks about I forget which book it is I think it's the K backbook where it's like
eventually some of these triangulations are so OB screamingly obvious you don't need to triangulate right yeah so what
what I always like to say is you take bigger steps until you fall and then you back up and take smaller steps um and you
kind of learn how big a step you can take uh that's what experience is um and if it ends up we fall on a flat on our
face we know how to recover all right since we're at um passing tests um now before we commit if we we're not getting
paid for writing tests yeah it's too bad um if we try to run all the tests oh actually we didn't create an all test
thing so let's let's do that let's go into the edit configurations um we can just duplicate one of those uh we'll call
it all tests and uh you can delete the tags uh and change the tags dropdown uh yes we do want to store and just say all
in package and let's uh apply that and let's run it so I expect our uh IO tests to fail because it couldn't autowire all
right suiga have a good evening time so that so what this is complaining about again is that autowired where spring
needs to be able to inject the song Searcher an implementation of a song Searcher into the controller but it doesn't
it's not aware of song Searcher so we need to uh create a bridge and this is where we'll go into our application class
this one y yep and uh so let's create if you go to Bean that really is annoying the other the other problem I and I
think I mentioned in the issue I filed Pro is is that it it's bigger but it's also higher up yeah screen which is
annoying when you're using that part of the screen screen yeah uh so what actually I'm curious um let me just I'm trying
to something it's innocuous um I'll just do this and then now because this is here ah when you hover over you get the
three dots yes yes that's what I figured was happening so then there is size could make it small small that's still fine
and there any other settings there's no color settings is there yeah bottom center bottom right still in the way of the
code could try bottom left see how goes it's less in the way it's still in the way not as bad okay uh so we want to do
is we want to have a public method that returns a song Searcher Searcher and basically does a return of a new song
happen why are the indentations weird okay I'll figure that out in a second return new I think because the auto the
generated files get indented with two spaces so if you hit Control Alt L it'll reformat the file yeah it's weird when
they generate the code that that the template they're using is is two space indented as opposed to something else I don'
t know right all right um this should have sat ified uh spring so let's run all of this we did pass commit oh do we want
to check uh do we want to uh uh update our Jura before we best thing ever okay yeah uh I think basically we have 12 even
though we didn't quite return we return the page we didn't I think we should probably split this task because because
there's two parts there's uh the model indicates we have no we have no results but we haven't updated the time Leaf uh
the actual HTML to do that so yeah so return model saying there no results and then uh let's call it generate HTML
saying results yeah and then we would do that for the other two I think we would do that for the other for the other
ones as well we probably want to split um yeah there's really kind of two pieces to each one which is sort of the the in
a sense the the subcutaneous part right just below the HTML generation check the models there and then um those won't be
automated tests necessarily so we'll just have to those yeah we can we can leave that for now okay all right let's do
commit um do I need to no I don't text uh so I think we can just say um uh get endpoint now results okay you want to say
anything about adding the all test configure yeah that's right um so now we have a choice we could go back to our domain
logic code um or we could continue with the the UI what do you think I'm leaning towards domain okay um but that's just
timee version of jir best version of jir ever that's what jir used to be really start has a text file uh okay so then um
we would like to find a song that matches the theme so one of the things that that I can do when um I'm streaming
through OBS is I can have the banner basically pull from the current tasks that I'm doing um that's not something that
unfortunately streamyard has yeah uh so then you could put that like in the banner yeah because then I could put that as
a banner I could go write it but it's it's not worth it so right right right all right um yeah so let's find a song that
matches matches the theme um yeah so let's let's write write a theme go what do you want to call it um yeah search for
theme finds matching song finds one matching song yep uh so what theme do we want to find pick a theme um Christmas sure
why not actually we could do New Year and have it return Old Lang Z sure let's do that that'll be that'll be that'll be
our execution part of this so would you search for New Year's or website probably think about it as New too because New
Year's includes New Year's day as well that'll be interesting I wonder if there are any songs that are only about New
Year's day but not about well there a song New Year's day but yeah I don't know if that's really about that right right
right right um it would not surprise me that there's there's sort of Hangover related songs for New Year's Day uh but
yeah we're we I guess we're searching for for that this this will eventually bring up some very interesting questions
about what is the structure of that string right um but fine found songs um or do you want to go with New Year's or
something else I would say found okay yep how did that happen I G to go back and see what do uh I think all we care
about um at least initially is is that it has size of one okay right it uh let's run our IO fre tests and this should
fail because it will always basically okay oh it is top of hour yes do uh so you you had mentioned that you could go
longer I could go longer my um my appointment got cancelled so I could go up to an hour longer I don't know if there's
interest um well there's always interest uh how about we we go for as long as we feel like we're our brains are good do
we want to take a short break now though yeah if we're gonna do that let's take a short break yeah all right let's do
that so I'll take a five minute break and we'll come back and try and get this stuff implemented cool yeah so somebody
asked since since I'm doing you know since we're pairing and I'm doing a lot of the navigating um somebody asked about
are are you stent said by the way just a note you're typing your chat directly into YouTube uh what you want to do is
actually type it into streamyard I am typing in streamyard uh oh that's interesting I wonder if it's because you're not
you probably don't have do you have a twitch login um I should yeah all right we'll have to figure that out figure that
out later yeah yeah because uh it would be better because what happens is then your comment doesn't show up on on um
twitch ah because when I type in a comment it uh it basically gets broadcast to to both I'll to figure that out all
right no worries yeah cool can work on that afterwards all right so um what's our next step I think we had a failing
test right uh yes we did all right so simple thing that'll work yeah let's wrong so what do you think should we just do
uh if theme equals new year's return an empty uh yeah a list what do you do contains yeah uh no what we probably want to
do is um uh let's do case yeah just to change it up yep now would we want want to do a um return what do you think
return what we want or introduce a local variable or start out with return and then refactor to I would say whatever
whatever the yeah you can do a list of thank you list. of I can't remember how to spell it let me uh well technically
what you just wrote will work true right so let's do that because we're not checking that you actually return the
correct songs we're just saying that it that had found one of1 okay so now we'll write when to find the um yeah I just
thinking is there a really yeah so um what we can do is we could write another test but I think what I tend to do is uh
uh sort of Ratchet up the constraints on on the test we just wrote right that makes that what do you think another
assert or change the assert to I would say we can change the assert uh if we use a effect and do you want it to be this
or do you want to drive it to well I think we should actually assert what we what we want because what we want to do is
yeah all right so now it should fail yeah because empty is not all long right uh we could do a commit I feel like it we
don't have to but we could could do one where we now return a matching song disciplined were you gonna say returning
matching song yeah return single matching song okay um so so this is interesting in the sense that yes we found a song
that matches the theme um we didn't really find but we didn't find it yes yes uh so I I think what uh so we have where
we find no songs we've if it's not so the applesauce theme isn't there new year's theme is uh do we have enough to
generalize now our implementation or do we need another test probably another test what do you think because not found
will always go to line something I don't know what were you thinking I think we have enough coverage um because we
basically have uh so I think we could go to find's multiple songs and then um and then refactor after that or we could
refactor from here uh and basically in a sense do a prepare refactoring so what I tend to do is when jumping from one to
many there's likely a prepare refactoring that would be useful um but I think the more important thing and it and it's
probably related to the refactoring is it's not obvious from the test why we would expect to find a length sign right
and so we're missing basically we're missing setup ah right yep very good point so I so I think we need to satisfy the
um our our need for the setup being having all the information right so in a way it's populating s Searcher yes and what
what this does uh is actually start as down the road of how do we associate themes with songs um I think we could do it
as a refactoring right without doing a failing test yeah because it really is a refactor in um it is adding structure
yeah I guess we could and but we could still test drive it in the sense of like if we online 24 started populating song
Searcher in some way well what we have also is duplication right we've got duplication from test to code which also
indicates that we should probably refactor the test so what I mean by that is take that string on eight push it into the
Constructor take that string on nine and push it into the Constructor Constructor for song Searcher The Constructor for
song Searcher and then that gets rid of the duplication um and starts down the road of of generalizing song Searcher
doesn't prepare us for the many but it does does get us to the point where we eliminate the duplication that have I
think I know what you mean probably best for you to yeah navate toward it so so let's take um uh the string on line a at
the New Year's uh and let's uh introduce field and you don't need to select it oh right I forgot about that control you
can leave it seled y so this would be our theme theme um that's going to cause a conflict yeah I know I was about uh
let's back up and let's rename the the the parameter so back up more uh let's rename the incoming parameter to theme
query do you have a better name quested theme I think them quer is I'm not sure both then the other one was yeah I kind
of like that because I like that better because because query could mean are you writing sequel or are you giving us
some things more business oriented yeah yeah uh now let's introduce field for that to be theme whoa Control Alt F not
control yep and now this one we want to call theme right and in the initialize in Constructor all right do it and let's
do similar did do it uh it did oh I see there it is got it yeah uh let's do the same thing for the song and the default
is yeah it's already it was set to whatever you selected last so was the construct okay all right um we could run the
tests we're pretty sure that that factoring worked it was all automated yeah um and now we can take the next step of of
parameters but you want to do that from ah don't tell me control P yes but you have to be on the thing you're
introducing so theme undo oh wait a second because that's not what you parameterizing so you had it right you
Declaration what are we parameterizing what do you what do you wantan what do you want the caller to be sending in as a
parameter what would you like the the call The Constructor call to look like I want the song theme pair yeah you got to
do it one at a time right you can't you we could introduce a parameter object later but right now let's just introduce
two parameters right right right so I'm not sure what I was doing wrong um you were on the wrong side of the equal sign
that was the problem Oh you mean here yes so you introduce theme as as the parameter which is not what you want do you
want to actually introduce the string as the parameter ah now if I make this theme is it going to put it should do the
right thing if you could if you delete the one yeah yes yes okay so then the colors of this now are passing in yes New
Year's yeah all over the place we got new duplications yes yeah well we've we've we've got sort of proper initialization
but we'd have to figure out what do we right okay all right and that should and uh for completeness sake let's um force
a fa failing test so we can close the tests let's go up to the test um let's 23 uh and we can change either side of the
let's change the all L sign to something else oh you mean to get it to fail yes yeah that's fine so now we expect it to
fail because the song that's in the database as it were is not what we got and the fails for exactly that reason so that
verifies that the setup is actually impacting the it all right so let's get our test passing again and then I think we
can do a refactoring uh to externalize Our Song database or at least externalize the database cool uh so tkes asks how
long have I been coding with Java and do I like the direction of java uh I've been coding Java since pre Java 10 Java 10
beta or Alpha uh and I think the direction that Java is going is awesome would I like it to go faster of course um but
like the fact that they preview features before they they finalize them because there are useful changes that happen and
I think Java 21 with project Loom is is a very significant release because we can stop writing stupid things all right
um we've eliminated the duplication across our test and our implementation and we've made it more obvious that Searcher
so now we should take out duplication in our setups uh it might be the time to do that yes so we could extract uh we
could extract setup not sure that would did that bias anything that wouldn't bias much at this point um or is it better
to move towards a better setup I I feel like I don't know yet what our better setup might be um but if we encapsulate
our setup uh it might make that easier to change so I'd probably say let's let's encapsulate our setup um more for
making future change easier rather than anything problematic right now is it only in this one test class oh no it's
there it's pretty it's it's there as well and so what we'll probably want to do is create a method and then move it to
uh to a static uh to a factory class got it so extract to Method yeah so let's extract to Method just no it's not I have
to select how much uh you can try doing Control Alt M and see what it what it does I thought I did oh no there we go
yeah I did control shift that okay I presume it didn't find this class so how could we move this into a factory and
still have the other tests automatically reuse it can we do that or do we have to are processed duplicates can be
invoked separately we might that might work uh I'm somewhat doubtful that it will but um the other thing we could have
done is uh in song Searcher itself create the static Factory method out of the Constructor which would have um which
would have replaced all Constructor calls uh and then move that static method into a a a test or leave it thing um you
think it's worth giving that a try yeah actually I think that's a that's a better way to do this so let's let's undo
what we just did okay there's a there's a easier way to undo that than just control Z out of it right uh you can control
Z but you'd have to be in the right uh in the right place so now you're sort of in a bad State yeah so we can revert
back to okay so if you select the first two classes because we don't want to change ones um did we do a recent enough
commit let's let's look at the difference to make sure we're not throwing away code away oh so we didn't commit after we
oh we did commit okay yeah so let's roll back that's weird it didn't roll back the checked files just roll back the one
you selected so roll back that's weird that was not what I would have yeah why does this one got a green uh greens are
tests ah right right more uh that's the diff can you close that window yeah thank you and what's tests not the file you'
re in but the oh we probably need to revert all of them so let's go revert all of them I was a bit surprised that it
affected uh all of them but that's oh right because it changed the in yeah let's let's go back and we'll we'll do it
again yeah we'll see where we are so select all of them that's why so there's a different checkbox and I guess that's
that's confusing to me so if you hit the roll back it brings up a separate dialogue that is Zone check boxes that do not
mirror what you selected here which is confusing that is weird Okay yeah let's roll it back um let's run all our tests
just to be sure we're back in a good State you're doing that uh so tkes asks what front end Tech do I use most of the
time I use HTML that's my front end Tech HTML and CSS a little bit of JavaScript can you do a little bit of HTM X too or
did you already say htx um HTM X is would for me fall under JavaScript a little bit of JavaScript all right so we're
back at okay uh so um what were we doing we were yeah I don't use voden voden is great if you're doing stuff that
requires voden um but I'm very much a believer in using HTML multiple page apps like we did in those great years in the
early 2000s uh so what did we want to do next um we wanted to encapsulate our setup but we were going to go do that from
song Searcher itself so let's go to song Searcher uh let's go and I think if you Alt Enter on song Searcher it's that
name it will provide replace Constructor with Factory that whoa yeah unsurprising that you make all those great all
right so now I actually think let's leave this method here um what do um is we can create uh some additional Factory
methods um that basically hide the the sort of initial thing so we have to think about what what what do we what do we
need to use from tests versus what do we need to use from production so our our production one we don't we don't really
have production except in one place in our application class everything else is is tests so let's focus on the tests and
then we can worry about about production um so I think what we want is is variations uh of of Our Song Searcher in terms
of what it what it's pre-populated with like something along the lines of create song Searcher with one song with
multiple songs yeah something along those lines y now do we want to be able to see what those are so we know that so
that the test is self-describing without having to drill into the factory right so what we want is if we look at the
tests on top we can see that uh the first test all we want to know is that there's no song with the theme applesauce
right so there's actually too much information there on line 13 right so we might want to have create song Searcher with
songs for theme and theme and then we won't care about the songs themselves because we're not checking that whereas this
one whereas this one we theme so let's handle the first one you do extract method no we want to make know what are you
looking for I was just thinking at those cared about what's passed right those they don't those don't don't care about
the specific so they would be more the second Factory method right so I think here we're just going to have to create
new new Factory methods okay do we do it through extract method no I think we're just going to uh well um and so what we
want to do is is uh I mean we could extract method and then introduce parameter and then move the method over I'm not
sure that that's worth it so let's focus on what we want for this one which is we want to theme yeah I'm thinking that
we want to create four songs with theme now this one we just wanted to be oh oh I see create songs for theme yeah so I
kind of thinking create with songs for theme is the full name so insert the word with yeah um we might even be able to
drop create because the creation is implicit because it's a factory method that uh and then let's drop the the song
method y uh so if you click out of it you don't allow intellig to go through its yeah okay again uh no you just want to
have it create sorry yep hit enter theme enter and now you enter yep uh and Searcher and we'll pass in theme and here we
can just say uh what I would say is uh uh song for and then sort of concatenate it with with theme and attack on themes
that way when we see a test failure we would see why did we get it all right uh that should have been a refactor so let'
s uh we can just run the yeah the other IO free test the other um let's now uh go to the other test in the one above uh
sorry no I meant the second test in that same class oh yeah yeah uh I think that one we want to leave for now right
because because that we are checking yeah because we're matching uh the theme we're looking for in line 25 with the
setup and the thing we get with the setup as well right um now these could be yes so so these I think it's probably
worth doing the extract uh method and then uh make static and move so let's do that so um so not the not the controller
the song Searcher part ah right do I need to do this or need to do that okay you'll get you'll get the choice of of what
this of what when you and so this is going to be create song Searcher with one song or just say with one song since the
be yeah with one song yep and replace that one then we can take that with one song since it's already static uh we can
now yeah you can just start typing SS upper yep and then hit that one yep and then refractor um and we want to take off
that annotation not null because it's inappropriate for that method or is it just not imported actually sorry leave it
no we don't want to those annotations that's fine uh let's make the that method public since it should be public anyway
so are you saying keep the not no annotation or get rid of we'd have to choose do we want to put these annotations in we
haven't been doing so before so I feel like let's not do it now sounds good tests even the other one above it is sort of
covered by that let's just run all our tests because I think the only place where we're now using the one that we pass
in both the theme and the song name uh is in that one IO free test but also in the application itself which I think is
fine for now yeah that's fine for now um unless say I think that'll be fine for when we start using the UI and
inspecting it visually eventually it'll it'll be a method all right I think this is actually a good stopping point okay
because I know my brain is is getting Fri yeah yeah y um so let's go in and update jira oh you want to commit first or
update J first update J first yeah let's update J first anybody who's listening giving so we found a song that matches
the theme we haven't found there's there's some subtle variations of find a song that matches the theme and not finding
other songs and other stuff like that but I think we can call that one done should we write another one to clarify yeah
so let's um uh actually no we've got we sort of got it covered I think we've got it covered um we'll we'll hit some
other stuff when jira yeah should I made it all caps jera do screaming caps jer. txt uh that's up to you okay what do we
want to do for um um I think this was mostly refactor uh and so was basically uh creating nullable like adding Searcher
that look good yeah I think that's it so now it be on the left it's the way again yeah I think really the issue is small
is not small enough small is not small enough yeah and position is not fine grain enough position is also not low enough
like I want it to be at the literal bottom of there's no further bottom yeah whereas the old presentation assistant is
smaller than this small and further down than this bottom and that's really annoying I guess we could push it to the top
I do have this yeah so you can sort of see it here what's interesting is there's a transparency there is a slight
transparency yes and I think that's that's more effective yeah I think that's because see and it's like right against
but it's mainly it's smaller so it's not as tall like the fact that they're doing this um want you do a commit yeah let'
s commit let's not forget to commit yeah let's do that and then if we were doing something like bringing up the commit
window again see the fact that it's got below makes it taller it does make it taller I actually kind of I like it um but
but you're right it does make it it does make it taller but I think the problem is is that the font is still too big
yeah um one of the things I saw in the discussions where they were actually discussing this internal sort of semi-
internally uh was they decided that they didn't want you to have as fine grain size but the problem is that because we'
re zoomed small would probably be fine if we weren't zoomed but because we're zoomed that gets zoomed as well and so
therefore small is no longer small and that that size is not independent of the zooming which it really should be right
is I believe you could try zooming back out to 100 and see what it smaller but now it's too small but now but so so it's
basically being scaled with the zoom which kind of makes sense uh because that's the way zooming works it just
multiplies everything um but it's but it's small is not small enough whereas in the old plugin you used to be able to
specify the font size directly and you specify and yeah and the transparency let you see there was that slight
transparency in the color uh color I think is vital that green color I think is is key uh the like transparency is
really useful um but the fact that that the font size is too big is is the main problem and that's not low that bottom
is not low enough we might try pushing it to the top see what what that looks like okay but you might in what did we
settl in 125 or 150 uh I forget I think it was 125 okay so this is 125 is that 125 yeah let me double check yeah oh then
it was 150 okay yeah now three buttons position top Center oh good right yeah so the problem is is that it's it's still
contained within sort of the editor pane as opposed to the but that's probably better let's leave it there and see how
how that feels yeah it's probably not going to be great no matter where we put it because it's just too big so big yeah
it's too big um I think that's it anything in comments you want to reply to um no so so the the just since we mentioned
the the jira the whole idea of of us even though there are tools like uh there's various CIS and so on the idea was we
wanted to not have to switch out of um we don't want anything complex and we don't want to have to switch out of
intellig basically so that's why we we went back to a text file yeah other words the absolute simplest thing that works
for us right now yeah yeah and that and intellig intell like the structuralist is is actually a feature um because
intellig has built in task management where you can create these tasks and check them off and so on uh but then you're
now stuck with however it organizes tasks and we don't get to have random comments like the Ted file and issue for this
thing um so I'm I'm very much too uh all right anything else we want to mention before we end our day what time we on
tomorrow I could look the calendar but you believe we are at 10: am tomorrow okay so an hour later start than we started
today uh so for those of you in different time zones that would be basically minus about minus two hours from now
whatever that is in your time Zone uh so 10: a.m. Pacific time which is 6: p.m uh UTC and we'll continue from here
sounds good all right thanks everyone and we'll see you next time bye bye
