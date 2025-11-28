# Some writing, some coding with Java, Spring Boot, and HTMX

**Video URL:** https://www.youtube.com/watch?v=Ti5yGWCSxjs

---

## Transcript

all right so today uh it's a little bit of a different stream um only because uh I've been wanting to write some
articles so for good doing it while I was folks all go so the first article that I was going to work on um is basically
the HTM X websocket stuff um so what I want to do is sort of clean up my uh my little Spike demo experiment so that it's
a bit uh nicer for the article um one of the things I like to do when I'm not sure I necessarily call this a tutorial um
but one of the things that that I do when I'm writing these kinds of things is I want the project to be just enough um
one one of the things that I that I find frustrating when I'm reading uh sort of how-to articles or tutorials is that
they cram a whole bunch of things in that are might be nice might be useful um but aren't sort of directly addressing
what what the what the topic is um so what I'm going to do first is actually uh basically do a commit on this and then
I'll go and clean things that and actually unsplit okay great hey Jonas is it late for you what time zone are you in
what I why does it feel like you're you're um I think what I want to do is so right now this this demo this little demo
project has two um has has two endpoints one for sort of an echo which is maybe useful as as like a a chat um the other
one is the timer stuff that I that I've been working on um so I think what I want to do is uh oh you're in C okay not
that late but yes it is late uh so let's let's that wait help MD has a usage what have that's interesting so it's
ignored and it considers that a usage that's that uh and honestly ones okay now let's delete right uh okay so let's
let's create a uh me let me plan out the the article so let's go to my website be uh you can tell I haven't written in a
directory that's not going to be in the right place uh so 2024 to probably won't get out until next file uh actually I'm
going to clone one um grab let's grab this one I don't like that it's collapsing all my front new all right okay so let'
s see what did what did I learn from this project um let's see let me me do there uh I don't know do I want to start
with the HDMX stuff or what it was my goal yeah that's pretty much what I learned um so I think the first thing that um
was important was uh boy intellig does not like understand how markdown indentation of lists seems to work I don't
understand want so the first thing that that actually was important to learn was was sort of how do the outer band
swapping works um um uh and then um so let's see uh so we had the websocket extension so pretty much it was this these
here for data yeah I don't know if I so that's something I want to play with is like what what exactly do I need uh
because I got it working but it doesn't mean it's necessarily the most correct um so I want to figure out what what
exactly do I need uh because what I get back oops um let me close some of um since I'm doing an inner HTML my
understanding is this then applies to this div uh and then this gets replaced um so this doesn't have um the ad the adab
band swap um but I do want to play around a little more to see exactly what what Target uh but that's not what I'm doing
I'm not targeting another one I'm one wonder what the target would do um oh in HTML is a default okay uh so it puts the
content inside the target element so it looks like that is the default I don't actually need swap what I also wonder and
I I remember swap be anything useful for for my timer Focus um although it might do a much better job because really the
only thing I'm changing uh is the conic gradient and this um this Remains the Same so I wonder I wonder so that's
something I'll have to look at swaps so if you want to swap content from a response directly into the Dom by attribute
you can use the HX swap OB HTML um so I've been using this wrong and it just happened to work because I had the div IDs
ah okay so it can either be true or any any uh HX swap value um value is true the element will line yeah I have to say
this documentation really confused me and still confuses me a bit yeah suiga I mean definitely uh the it can basically
you can swap anything out of the Dom as long as it can find it um but I find this to be really as Yeah so basically uh
if a selector is given which I'm not um all elements matched by that selector will be swapped uh if not the element with
an ID swapped so all right well I figured I'd some some other stuff um uh let's go here let's create a the call it UB
swapping um and what we'll have in here is basically just another div with an ID of uh replace uh that I'll that replace
H1 because I want to play around with that so now let's put in button that will do get triggering so by default it'll
just part um let's start there but eventually I want I want all this to happen as a request through the through the
websocket can I do can I do that sockets socket send so let's what do I want to do here yeah absolutely sui and I've me
I mentioned that like a bunch of times when I was when I was first going through it's like I'd like to see a before and
after in fact what I'd love to see is like a live like self page um but let's do an outof band swap on this let's do
band default uh I me I think both both would be useful here's here's what was before and here's after what happens um so
like this when you click it I'd like to see what happens so let's let's do that so let's create HTML yeah they have some
examples but why not why not host it at well technically I just want to return strings of HTML so let's do this uh and
so here we'll do a get mapping uh but not be H1 oh come on you're not going to do uh text block there we go text block
love to be able to make that the default that um so this is replace H1 that Returns the HTML uh all right so let's uh is
that enough um let's do I need to say this what what was an what does this an H get do uh so this would be an out Advan
swap happens hey magic 79 uh front end it's sort of playing around right I'm writing an article on on what I've learned
and I realized I there's areas where I don't know what I learned so I need to figure that H1 uh and then we want a
button that's basically the same div like oh those don't look like buttons I forgot I'm using uh Tailwind so it
basically resets everything so here I should probably just put this up um yeah uh there definitely needs to be some we I
forgot yeah I mean I I gota I I actually like seems like an obvious thing to do uh so let's go into our controller H1 uh
this is our div repl do same thing here all right let's run this baby uh let's run it in debug mode so that I can stuff
so I think examples are useful um but this is already sort of too high level uh what I want is is like what what does
this do right okay great it tells HTM X this what is the result this example click happens that's that's what I want um
these examples are are useful and I'll I'll look at them uh but these are already sort of building on Concepts that
without sort of a a proper grounding yeah so it's interesting like I for anything more complex than like a couple of
Dives um like you know I don't know let's call it a dozen lines of HTML uh I'd probably go or or if I need to do a lot
of data transformation or if I'm going to reuse stuff then I'd probably go with a Time leave templates um and I know
there's a project of view template view view templates that uh makes more programmatic templates and that also has some
HTM X support um but I fully believe that you you have to start at the most Concrete in order to understand what's what'
s going on uh all right so that's running let's it oh I should probably turn that off uh so if we replace the H1 so what
that did was it replaced uh the contents of the button uh in fact we should probably also look at the page Source while
we're at it so what that did was um we clicked the button and it basically replaced the inner HTML of the so true
basically meant to change change the internals uh 44 found uh it's uh I think it's is it is it Tom schooly's article uh
um Spring htx Leaf yeah it is it is Thomas's project component and this looks really interesting and at some point I
want to try it out um but I need to understand what's going on underneath so let's go back here um so let's uh so then
this is probably going to do do the same thing so that where is swaps oh so this would have to be in the response so
it's not uh so I need to put it in the response to say out of band swap true see again here's where it's like before
response from server after that's see uh so we need to put so if we take this out and we go to our controller and we add
it here uh that see what's confusing is this looks like um the before that's in your page but rereading this now this is
what the websockets returning and it may be that's what the text says but it's really like not like it says receiving
message from webs ET um but these are the messages that are being received it doesn't tell us it doesn't connect things
from it for us um and that's really really was not clear clear to me so let's try this again let's uh uh let's let's
restart uh and I want to just compile no it restarted anyway um I should probably turn off the the timer let's refresh
this page anyway all right so which one do we one oh did I type it wrong it's HX I keep doing that is it autocomplete
here no because it's not HTML file if I do inject uh where the heck is it in language of reference HTML temporarily
injected uh so now I should have yeah okay I should do that so let's here uh So eventually we'll do an HX again fres
this up H1 uh okay so what it what it did was um it did Target and replace out of band uh to me I find even the name out
of band confusing because it's not out of band it's all in band it is out of the current scope it's really out of scope
I want to replace something that's not in the scope that that we targeted uh unfortunately what it what it seemed to
have done is also replaced the button content with get took took whatever was left guess because what I want uh so I
guess this is where you would do a Target uh and then you probably wouldn't need the swap so this replace Target uh
that's wrong this is wrong it's not specifies the event that triggers the request that's trigger I think that plugin is
wrong uh so let's go back here target uh I could set Target equal none um in I mean the question is is do I so the the
autoband swap is for art is for letting the server control where the replacement happens if the client HTML already
knows where the HTML is going then I could just say that so let's do Target uh what's the ID want this one um I want to
get complicated is it HX so HX Target none uh it's not H uh so it's not intellig that's offering the htx completions
it's a plugin and I think the plugin has a couple of boo Target targets what if I don't what if I I none where you
almost need like a table oh no worries for for uh it's basic if the only HTM X plugin that I am aware of so if you go to
plugins look for HTM X I think there's only one that's a bug because because that description paste uh the bug is it
says uh HX Target it specifies the event that triggers the request that's a copy and paste from HX trigger HX Target
specifies the returned and there may be other similar problems I know sometimes it doesn't have any docs like for Swap
and swap oob plugin uh with no target nor checks these button names are getting really long um grid um uh so let's fix
up our right I still don't know why they call this request pram it's a query pram specs oh onute value must be constant
attribute constant is does anybody know what this default oh no that's the default what is that uh a new line some tabs
a new line some tabs a new line and then some other car that's so weird um but this must be a string confused it's not
the default after it's converted to a Boolean every time I do this I think I run through the same problem uh what I
didn't notice was that this that it's a type of string this uh so if if it's true we'll return go uh otherwise uh we
return an empty string missing I can I present us string why is this complaining oh because it thinks it's it's uh uh H
attribute uh that's what happens when you inject the language now it's like what the heck is this percent s doing here
yes it is the HTML par recruits hey there me um okay so we don't care about that uh now I feel like this is getting comp
at enough so let's split this right uh and let me turn off the uh a all again right so let's go to uh we want targeting
so replace the H1 that's this thing uh no target nor HX swap with an right so the outof band response told it to to swap
whatever ID came in with um but since the target was not set uh it replaced the contents of the button with nothing here
we're going to say swap none with basically the same thing but with swap of none and that retains the uh this one what
does this one do this one says uh also replace the H1 this time using the target without the response and that's what it
does so because uh I specify the HX Target um it doesn't need the out-of band response because where I want to go is the
Target that I've specified here on on the client uh and I don't need to say swap none because it has a target for it to
to go to okay now I think I have a better on so I think what confused me about um about this part is uh the word sent
here is confusing because the way the documentation has been talking it's been talking from the point of view of the
client right the browser so when I think of send I think it's from the client browser to the um to the server this is
and it says sent by server and you think oh well of course it means the the stuff that's sent by the server but I kept
reading it as just the sent part and I didn't kind of really noticed this the by server um I think another thing that
that uh would be really useful is if the documentation used a different color or some other indication to say that this
is the response from the server and this is what's in the original HTML page um or just use them side by side uh and
have a sequence diagram kind of thing um which is how I would do it uh Mii what do I think about the next period been
programming spring boot for four years the AI that comes from behind really scares me uh I don't know about you maybe
you've had much better experience with AI than I have um I find it to be helpful about 20% of the time and only in sort
of very specific cases where I already know what it wants um I continually try to have it generate non-trivial pieces of
code and it just Falls completely flat um I think there might be some very so I don't see it as anything other than uh
occasionally making things slightly easier for for developers uh I'm not worried about 10 years I don't I I can't worry
about 10 years 10 forever I don't I don't try to predict 10 years I don't even try to predict five years um my main
concern with with you know with basically uh large language large language models and things like that is just the
incredible amount of waste yeah so I I I agree that uh because websocket is bidirectional both are sending um but the
context here um so the reason so one thing and I know that this was going to happen um when writing docs this is a
common thing I see of let me stuff three completely different examples into one little area and I understand why it's
done is because it's a lot of work to do more um which is why I'm writing this article is because am I supposed to be
like we don't read carefully that is a fact of of what we do right our brains we try to Short Circuit things we scan
things and uh my goal when I'm writing documentation as well as when I'm writing code is I want to make it scannable um
and this is not scannable this this requires me to to read this very carefully to understand what this means and that
means that's not good because what generally what we're looking for when we're the consumers of this is give me a
concrete example that does one it um there is really no good reason other than just I don't have more time to put these
three things into one code block because you scan this and and it looks like it's a single unitary unified thing it's
not it is three different things that have three results all right so that's enough of that uh okay so um um I kind of
wanted to focus on the websocket stuff but I kind of feel like you got to understand uh the diff What happens to the
result that you get so I think um we get to the basics it's the basics of HTM x uh HX get Target and OB yeah I agree ASD
that that writing from an expert point of view um makes it harder but there there are what I think are fundamental rules
of writing technical documentation of you don't put complex examples until later you start out with the simplest
possible example what do you what what do you start with what do you do and what does it end up with and if they if you
apply that to to anything you will be able to get better docs even if you don't necessarily um even if you're not able
to sort of break knowledge and this is why you know smaller methods with with names that come from the domain um and and
I think there's also the mentality of of you know and this this goes to you know many more smaller steps right I mean
small steps which means you have to break things down this thing would be broken down into steps because it would broken
down actually into steps right so uh you know there and what's interesting is there's also the scrolling problem right
I'm constantly having to scroll up wait what was this and wait what's this um and so that's that's also kind of a
problem it was hard to write so it should be hard to read dang it you should suffer as much did that's that's a very
wonderful uh empathetic um so like even this example is already too complex because it's it's there there are two pieces
to this that it's demonstrating um notifications that's a nice to have right that's extra right if we're talking about
chat we want everything we want basically this but without the notifications because then you can show and basically I'm
going to be writing writing exactly that then you can show um that you get this but then they throw in the morph them
it's like wait what do I need that is that absolutely necessary and again this is this this this I see this time and
time again is throwing in little things and it's so easy and I you know and I do this I know when I when I give
conference talks or or Meetup talks or whatever is it's so easy and and and enjoyable to go down tangents um but like in
this example why is this morom here is that required right so somebody coming new to this I'm like do I need this is
this required do I have to do that because you know what happens is people copy and paste what they see that's not a bad
thing that's how we learn um but if you put stuff extraneous stuff in right so in the book club we're talking about
cognitive load um and we'll be talking explicitly about uh intrinsic versus uh extraneous kinds of materials for
learning this is extraneous yes this is not because we need the before end but this seems extraneous or maybe it's not
extraneous I don't know but it's it's not explained idea oh I must have missed that specific uh Goot post I'll have to
go find um so I think what we want to do then is um I can close that and that and others uh if you I don't think yeah
try try yeah try saying his name three times we um we'll demo this just with an HX getap oh that's probably why I didn't
see it CU I've been sort of sking over his his stuff because I've been following it from another location as well um so
we got the change of mind mindset and so basically we will have uh I'm I'm very frustrated by intellig handling of of
markdown documents it it it especially for like indented wrong I wonder sometimes why I example uh I don't need that um
endpoint uh see this is why AI I will never replace us it's like new endpoint new endpoint this is a new endpoint um I
do want a new endpoint and I do want to get mapping so that's just Fancy Auto Complete uh so what about I want to return
um actually I don't need the new one I'll div uh this doesn't div yeah yeah yes it's listening to me it's microphone uh
that was pretty pretty interesting that that's that's the name it chose of new endpoint but it's creating a new endpoint
so what with I can have it um uh so this is interesting that um what it generated does I don't understand why it's
trying to replace all the code that I already have with this new code I didn't say replace my existing code basically I
I've done this a couple of times where I've had to generate stuff and I'm like I don't understand why you're generating
and then throwing away what I already have that's not at all what I'd want so I my my subscription for for the a for the
jet brains AI is coming up in in a in a week and I'm on the fence about it uh okay so this is replace div um I'm going
to put a hyphen in it to so here um that's not quite what I want uh although it's interesting that it would suggest that
so what I want is I is I want this um like right yeah I saw that as it's like you you hired the does I understand so so
sometimes I ask it to autocomplete I ask the AI to do the autocomplete uh and it basically does nothing because what I
was hoping it would do is is is generate the class anything and I don't know if it's just know yeah well customer
service is allow is allowed to do whatever they want so that that look like div button night so this is we want to
replace div all right let's see if we do that um we expect this to since there's no target here uh we expect when this
comes in there's no target so it's actually going to replace the contents of the happens so we want to look at basically
wanted okay so uh so we've got our button which has the HX get to this the div comes at um Network so if we click on the
button it's going to do a get request uh it's going to get some HTML and it's going to take that HTML and stuff it into
this button the headers and we can look at the response response um and so that's what that's what that does okay for
don't know why it thinks I want that um what I want is a class uh not large um tokes uh inter classes are I don't know
about used frequently but they're they're but they definitely uh do have have a lot of uses I think it's important to
understand the difference between static and non-static Inter classes uh and also understand the difference between an
inter class and a class that happens to be in the same file as another class all those are right that probably shouldn't
have been an H1 uh I mean an H2 that was a mistake uh p uh let me run Tailwind so that gets regenerated I have Tailwind
running here uh I don't am I using am I just using general I'm just using oh I have to generate the the uh yes and
Anonymous inter glasses are also really important uh especially when you want to understand uh lambdas hey Donnie Roose
uh yeah I've been long a fan of of hmx I hadn't really used it though until recently um I don't think I have a setup for
then margin all right so uh if we click this button that that this stuff uh so let's see so that's um where's the p two
not coming do I not have that in tland was this generated Folks going all right so this is the one where it doesn't work
the way we want it to um and so now what we want to do is create one that does work the way we want it to lab uh let's
see so this is the one that doesn't ID this so I'm trying to balance like putting this in one page consistent let's see
what happens I I suspect I know what's going to happen but let's happens so used to typing the the back tick for
monospace initiates so we got our class we got our HX get and uh we've got our HX Target um okay so we'll replace the
target div contents um so regardless of what we return now that we have the HX Target specifying this div this div
should go away um big so replaced here because we have the target Target uh so now demonstrate um so we got where it
replaces the wrong thing we've got it where the client the HTML directs it directs the content where to after uh that's
the dock is uh the reference of this in the first ambiguous way this one the same as uh okay so now we want another is
um contains SL right Target all it and so we'll basically do another get mapping that'll look a lot like this uh with ob
swap that's Target of that and we want HX DX HX swap o sufficient I don't know if true is sufficient um so now ah right
so here we got uh we got the content coming back and disappears uh so basically the is button contents goes away still
is there we can still click on it and we can see the time get updating here want so this one works fine because uh we
specified a Target this one is out of band swap that uh what will happen if I have an ID that's already in use up here I
guess we'll find out so here also doing uh HX Target right swap let's let's see Astra because it it'll either be uh
whatever is found by a typical document um get element by ID or it will look for the closest one um see well that's
interesting that was unexpected so it didn't either uh so it did both so we both win right because watch watch here this
one and this one I click it here and it replace lose uh so that's probably not what I demo calls both those okay fair
enough our test would have failed right uh that's for row in a grid Gap uh I probably want a bigger y Gap I currently
got it set to a gap of four which is a one ram Gap but I'd like bigger so Gap GAP Y6 yeah I mean technically you're not
supposed to have multiple IDs with the same multiple of the same IDs in fact intell is marking that uh but it is nice
enough um what is the biggest y g I can do right it's totally not a bug it's a feature um it has y12 why am I not seeing
it because I probably don't have the that uh but I don't think I have this configured correctly um I should just for
this stuff I should just use the complete the complete it works caching no oh because I didn't finish writing wanted uh
so this isn't a spike this is this is actually going to be part of the article that I'm writing so I wanted to have a
nice a decently nice Gap all right so we know we can't use the that how do I want to do that uh do I want to have a
separate endpoint that has a separate Target or do I or do I want to make it a parameter feel like making it a parameter
is is more flexible um but it gets away a bit from concreteness so for for this article I want to make it as concrete as
possible and I feel like any uh like this stuff with the parameter was was temporary I'm going to um uh in fact Let me
let me copy this class this is HTM this so since this is an article um I don't I kind of don't want to have any any code
here in a sense of any decision making so is that more more or less clear well let's try it this come part uh okay how
do I inject how do I inject assistant way thanks all right so I guess I have to inject it each bummer I do wonder how
it's storing that information though like is that in a config somewhere that I could control more easily well that's not
what I'm here to solve so uh and I need to replace this over restart oh hold on a second second just get my grocery list
I have to shop for in a okay nope that's not the view I okay I mean it's it's it's sort of as unreasonable suggestion
but it it it always uh it does seem to like it's it's trying to be helpful I I get that but um that's not what I want
all right so this replaces it but mucks up uh the button this one replaces it and keeps the button so this is the one uh
so either this one or this one are what we want so let's do uh background green let's try 100 what does that look
padding all right that looks well and to this one instead of green we'll make 100 that's good here all right so I am uh
done with these examples which is like Step Zero of what I what I actually wanted to write about which is the the
websocket stuff but um got to start somewhere all right done uh celebrate redeem I should yeah I I don't have any like
fireworks or any fancy stuff um should probably be nice to have that always always something you need all right so we
got the demo with the HX get um I think I want one more example of that uh this feels like a nice to have uh I think I
can just mention in the text that we can do that and then maybe later on I'll add that um so I think this also achieves
the change of mindset so it's it's a fundamental basic example um oh that's that's a good idea asra I time um so this
will cover the change of mindset uh and well as well as understanding the difference Target it's to um to want these
things to have slightly Target uh appears in I'm going to call client HTML whereas the HX swap out of bounds is uh HTML
it's a it's a subtle distinction because obviously the server could return HTML that has the Target in it um but it's
sort of who's controlling replaced I wonder who overrides what uh presumably the swap uh the out of band swaps would uh
in fact if I remember correctly it does override it uh I don't know that I want to get into nuance I'll mention it but
I'm not going to go deep into it yeah um yeah I'm trying not to not basically it's like just don't do yet already uh so
now I can look at this and uh let's go back to uh we can that yeah so now we can see where I was wrong which was um
putting the HX swap here um so I think now we can and I gotta end this stream in like five minutes uh so what we can now
do is we can now have a the of what'll eventually be the the timer that I that I created so what we want is the the most
Bare Bones chat um so this loads up the extension this connects to an endpoint um let's here we don't want notifications
what we want is uh just some chat messages yeah make them feel safe and then overwhelm them uh so can I on the client
side manipulate the HTM X to intrude the that I don't need that um H that's funny I don't need the CF csrf token
security can you use it for attacking I mean it's just J doing JavaScript fetch stuff so anything you could do with
JavaScript you can I mean I I don't I don't think it makes it any more powerful I mean you're still just doing get
requests and post requests which you can do in JavaScript so it's no once you're running JavaScript then you can do
whatever you could then sort of make sure you've got secure security and csrf and other kinds of stuff let's let's call
that chat um let's rename this Handler um we'll delete the send notification for now oh actually we need the method okay
uh so we want to do is we want to Target chat that um and here is where we want the swap out of bands to be before end
so it won't replace what's there uh it will um basically added to the to the inner HTML but at the at the end uh since
it's already in a div we don't this yeah I mean HDMX is just making this stuff easier it doesn't mean it's doing
anything that you couldn't already do and exactly you want to make sure your stuff is don't rely on your front end to be
secure all right I should stop drinking coffee um all right so let's go uh let's go to this page and then that'll be it
for today uh whoops I renamed the chat uh websocket Handler chat again uh that's interesting so let's take a look at
what's going on here because not ah interesting so note that uh what ends up getting put into this div is and okay now
that makes um is we're returning a div that is chat messages which means that it's going to Target this div but it
doesn't replace the div because we said HX swap out of band before end so instead what is it what it does it takes the
contents of this div and adds it to the inside of the div that already exists um if we just said swap equals true that
would replace it uh so that means we actually do want to this AST yeah so now what we see is the div has a growing set
of P tags and each one is being added at the end so after right before basically the and so now what we could do and I'm
actually now running late all right let me do this one and then and um what we'll do here so what we've been doing is
we've been grabbing the Json that we get from the button click that sends this form is actually much more than just the
contents of this input um it's actually ironically enough it's it's uh it's Json that gets sent with a bunch of uh a
bunch of headers so it' be useful to actually see what that is so let's do uh send notification um and here's where we
part uh and so okay um that's wrong but thanks thanks for playing uh that's our payload and what we want to do is we
want to send a notification uh to the session but what we want to send instead is the entire payload and Target the uh
element unchecked whatever okay so now if we run it we'll see two things come back we'll see the chat message which is
just the chat message and then we'll see the received so here's just the payload and here is the actual entire payload
um and so we see that what we're what we're getting is uh a bunch of Json we get form uh we can sort of add to that we
can basically have an input hidden uh equals username and value equals Jitter quote um map class is a class yes because
what I want is I want I just want name value pairs basically I just want a map I don't want to parse the Json much more
than that I mean I could just display the string which is what I do here but I want to actually pull out uh pull this
out all right this is it I'm out of here what we see is name of input is this text field we've got the hidden field
which is this um and then it also sends a bunch of headers uh this was an HX request the trigger was a form uh there was
no trigger name the target is also the form and the URL this oh I see yeah that's because um I'd have to use a type
reference for this lazy all right that's it I got I got to bra um so uh didn't make anywhere near the progress that I
wanted to make but I think that is always what happens um stuff just takes longer than you think basics uh of of the
swapping and uh we have for the the level one of using websockets uh and what the payload looks like and so there'll be
a couple of it'll be the the first one we did which just had the chat messages uh and then we'll add on now we can
actually Target two things um uh and then once we do that then we can move on to the more complex uh of this is actually
really more of an echo server any other anybody else who connects won't see these messages so now we'd have to say okay
now we need to keep track of sessions and and things like that so all right thanks folks thanks astd for hanging out
thanks uh deshaan Java grunt for hanging out and other folks who who were just uh lurking in the background appreciate
you um uh I will probably also stream tomorrow with just this stuff or if uh uh if my partner in crime Mike Rizzy is is
around we'll pair uh we'll do a pair to stay up to date best way to do that is on my Discord um I announce streams uh
usually with at least some some amount of notice on the Discord um I don't always announce them on social media uh but
this one this one I just announced on on on club so uh every Sunday which is basically the the next one is tomorrow um
from 10: am to 12:00 noon which is 6:00 to 800 PM UTC we discuss a book we're currently working on uh we're just
starting we just did chapter one last week chapter two coming up of the programmer's brain uh it's never too late to
join and you don't have to come to everyone and the last thing I want to mention is Tuesday uh I'm going to talk about
my tdd game uh on the agile lunch and learn so join me for that um go to bitly td- game- lunch uh to get the invite link
uh and I'll see you uh if nothing else I'll see you there on Tuesday otherwise I will see you on the next stream have a
great rest of whatever day you've got um and I will uh and stay dry or stay warm whatever whatever applies to you uh
have a good one bye yay
