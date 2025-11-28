# More Tutorial Writing： Spring Boot, WebSockets, and HTMX

**Video URL:** https://www.youtube.com/watch?v=cUwmZdxZUXM

---

## Transcript

a oh d oh all right hello folks and welcome to uh another solo stream apologies for the wrong go live message on Twitch
uh streamyard does not update that message uh and it's really that hello astd how's it going um so my brain's a little
fried had a a so going back and forth about streaming but I figured why not um so I think uh gonna just figure out where
I left off on my uh websocket stuff and then uh continue with that but as always interrupt or not interrupt uh qu your
questions are not interruptions that's why I stream if I wanted to just do stuff and not be interrupted then I wouldn't
stream so all right whole part of your brain back so let's see where we were uh let's buttons there we go all right so
uh for those of you who haven't been following what I've been doing is um working on examples for what started out is
just oh let me just document what I learned doing websocket stuff and HTM X and spring boot into uh a little bit more of
a formal tutorial ah yes code coverage as a goal idea well hope your presentation working on that presentation goes well
if you need any feedback I'm happy to provide I really you know I I to a certain extent I don't I don't blame management
for for wanting easily measurable things um but then they have to don't and it's kind of funny it's like if you have a
set of folks who know that code coverage as a Target is a bad idea then they'll do their best to improve it um but there
always uh there's always the danger that people are just going to say this is ridiculous I'm just going to game it we
know what we're doing and not not either situation is good but for as long as I've been in this industry that
everybody's always and this is not just software development everybody's always looking for easy metrics to measure
things because we like to measure things because we like to be able to think we're in control of things uh the fact is
we're not and we can't and um it's much harder to do the other kinds of things like actually look into what's going on
in more qualitative sub sort welcome all right um so where the heck did we l let's see um so we've done the websocket
broadcaster let's go look I think I had that's it okay um so I think we had finished sort of part one which was uh about
um basically just just sort of what HTM X offers uh HX get what the target is what the what the outof band or uh
retargeting or swap Target I really think this should be called swap Target um I might actually suggest this to to uh to
Carson gross the HDMX person um we'll see uh and so we did all the demo with HS get and the targeting uh and how the
that stuff we did the swapping um we did Changing State on the server uh we showed how that uh can change the state on
the server and then basically any refreshes or any anything like that will'll always get the curent State um we did we
did this so add script we added the web WS socket so we did all this and now uh right boy am I glad I love myself notes
so now we're going to do um uh a basic chat implementation so we did some stuff where we can handle incoming message and
basically just Echo it back but now we want to um Echo input from a single user to to everyone else yes even with Branch
coverage that doesn't help too much you can as I always say it's like code coverage tells you that code was executed it
asserts nothing about whether it executed it the yep how to instantly uh get to 100% code coverage any failing tests um
all right so uh let's see let me close this other now right so we sort of compared this versus versus this uh and
decided that actually the for Loop was was quite a bit easier to stand to to to understand um let's actually refactor
this out message that so I did the um panel text message I got the message uh out of the payload payload is map uh I got
the input name oh but I didn't have an actual class what's my chat chat websocket Handler so um so let's revisit this uh
this is the Handler no have not finished it I basically um we'll be we'll be writing part one um probably today or
tomorrow week but I did decide that it's going to um yeah let me copy the map and so let's see so what do I want to do
here um I did say my brain was was not in today uh so let's let's I don't want to cast this is a string let's actually
pull this out so this is um websocket but I think uh oh I wanted to do the change State over websocket that was what I
wanted to do here so instead of CH doing a pushing a change pushing a state change on the server through a post regular
post request do it through the the websocket variable pass that and we'll put that on hold for a um so we did that uh
and then the other thing I wanted to right uh s Ender funter zero asks about adapters from uh ports and adapters or
hexagonal architecture do I ever think about combining adapters if they are always used together you always produce a
Kafka event whenever a web request comes in um no because is if it's if it's not going through the application uh then I
don't think that's generally um I mean unless you are are are a pure pass through so like you get a web request and you
immediately produce a Kafka event um I'd honestly deploy that as just a separate little little service if it's just sort
of an echo kind of thing then then there's no Behavior so then why even bother putting it in the same application uh I
don't like this idea of of adapters that are independent of applications I don't I don't think I'm not saying you
shouldn't do that I'm just saying that's not hexagonal and so I just want you know I want to I want to say something
about hexagonal which is it is not the answer to everything right so it is very um it's it's not a good idea to try to
put all your implementations of all your services and everything that you're doing in sort of the umbrella of of hex
architecture that's that's that's saying I have a solution let me find and apply it to all the problems that I have and
I think that's uh not a good idea you need to adjust your architecture based on what you're doing so you can totally
have a service that listens for a Kafka event uh or generates a Kafka event whenever a web request comes in that's
totally fine it's just not a hexagonal wrong um same thing if it's a if a web request comes in and I I I again I don't
really know much about kunda um that's fine that's not hexagonal but that's okay right so not everything has to be
hexagonal so the point of hexagonal is you have a core part of your application and I always say to folks hexagonal is
not the answer to everything if you are integrating systems and this sounds like an integration then don't use hexagonal
there's no point to it if you have no else hey there zabeli um have I seen the socket iio implementation for Java um
socket iio is my understanding is a JavaScript side of things I have not seen a socket IO implementation for Java um so
I'm not quite sure what uh some some other socket stuff support in in Java uh with with spring boot but anymore uh so if
you haven't already forwarded them my my presentations on the topic I'd recommend starting with that um and of course uh
you can ask for more resources on on the Discord and I'll I'll I'll and there's a whole bunch in the Discord if you
search through the Discord resources Channel there's a hexagonal but again architecture architectures like hexagonal
clean onion vertical slice these all have you know just regular old layered um you have to fit the architecture to what
you're doing you don't start with an architecture you start with what problem are we trying to solve and then you fit
and choose the architecture based on the problem you're trying to solve and how it join the fried brain Club that's
welcome and so um I I have a couple of videos on hexagonal I have the one that's most popular is just because it's
oldest is actually not the the what I think is my current thinking on it um so I usually recommend uh uh that that folks
look at my more recent um Talk on hexagonal which uh that so so this one is um I'm posting in chat this one's my uh most
recent sort of iteration that I've given uh presentation in in public uh that one was from the where is that from that
was one yeah so uh there is the one that's from like four years ago but I've changed some of my thinking and approach
since then um um if you've been doing stuff for for four years and you look back and nothing's changed then then you
might want to case um so fit your architecture to your problem not the other way around is basically what one the
message I'm across much all right um right so let's uh so let's let's put this aside let's put the chat thing aside put
that uh let's put that aside so this is the want so this is this is that uh all right so let's continue with this one
then so what we want is um so this does a post based button what we want here is uh I think we want in a sense what we
did with this one so let's let's let's run the application just so we can see here by the way if you haven't seen this
would appreciate if you uh watched it and liked it and shared it around basically talk about predictive tdd and my tdd
here I'm excited because I'm going to the agile open Northwest uh in a few weeks uh so I'm gonna bring a few copies of
of my game um because I haven't actually seen people people play it live since I had the Prototype done actually at the
last time I was at the agile open Northwest conference that was oh gosh was it four years ago might have while uh all
right so let's go Local Host uh we want to go to I think just websocket socket and uh let's do this split the socket and
do that so we can see both at the same time okay so this is just the connect handling um this is if I click it what I
actually want to happen here post to I don't think do I have even have this endpoint uh oh no I do but it's in the post
controller um that's not where I want it uh so this is next state um let's go to our post controller and let's grab the
next targets um so this will be interesting controller how how do I want to do that um so this is always the interesting
balancing sort of balancing making it concise versus welcome so uh so what I'm trying to do here is do I do I take this
websocket broadcast right so all this code is is for a tutorial um but what I want want to be careful of and in general
this is my one of my complaints about tutorials is they structure things in ways that you wouldn't really want to do um
that are either just oh I wouldn't sort of combine the classes in this way or I wouldn't structure the code this way and
so I want to make it as as sort of realistic as possible but there is a balance because you some you you do things like
you have separate files for a controller versus a websocket Handler um so that or do I want to just combine this thing
kind of feel like I want a separate class even though it's a little bit noisier uh I think I want want a separate class
let's let's do that so let's actually just grab this we'll copy it um and this is controller uh and we'll grab and take
these out and so then this so it does a post interesting um I actually think I have to have it in the same class this is
where I I so so what's um I want the post request to come in and as a result not return anything to the caller right not
anything not return a response to the request but basically then send out through websockets um whatever the current
current state is uh which means they both have to share the same thing and this is where you'd use something like
hexagonal the application would would be the thing that knows the current state and then both the the post request and
the websocket would be on adapters uh but I don't want to go there just yet um okay so I've convinced myself that
actually this does need to be part of uh the same the same thing because shared hey there aard house yeah spring
projects don't have to be all all serious and busy they can be fun I do want to start my my next project that's not my
ensemble project my next sort of main project um after basically after I do this tutorial uh because this very much will
also help me on implementing uh an online version of of my tdd game so uh I've had a number of requests for that and so
I want to get started on that project but yeah um yes yay I actually have a an implementation that uses View for the
front end and after after doing this stuff here with with HTM X um there are still some benefits to to using view
because you get sort of more component things on the front end um but there's just not a lot of it's mostly it's really
mostly layout kinds of things uh and um it's going to it's going to be a long-term project but my hope is is is sometime
this year it'll be done enough that I can actually start having people people play play it on online yes oh Bel tooda
yes I know this is streamy yard's fault streamyard does not update twitch's go live message which I consider a bug and
they have not said anything about fixing it so um but tomorrow actually will be a uh a pairing stream um so my schedule
with Mike is uh tomorrow morning Pacific time will be a pairing stream Wednesday morning I think uh not sure about
Thursday yet but there'll be at least two two pairing streams with the mic so yeah I realized after I push the go live
button it's like oh shoot I forgot to update the twitch go live message but it was too I this is this is my my I I worry
about tools like streamyard doing what what um I see other tools doing which is instead of finishing your features right
so streamyards main main thing it's really two things um is uh be able to present the stuff like you see it right so so
you know code over here and and me over here um and combine the screen in different ways and and and pull the chat from
YouTube and uh twitch into one unified thing that I can see um and then multistream out to to multiple things but like
can you finish that folks before you start adding other things like webinar support like I'm not using you for webinar
support sorry um and I see this happen again and again with uh convertkit and Paia and they it's like can you finish and
flesh out right you got the 80% features can you finish the rest of the like the other 10 or 15 I don't expect you to do
100% of everything I want but like streamyard doesn't um update certain settings on YouTube uh so I like it ultra low
latency and there are actually three different latency settings on on YouTube and I like ultra low so that I can be more
more interactive uh and it doesn't update the the twitch go live and it doesn't allow certain other subtle
configurations of these stream things like and I understand you know when you just come out great um but you've been out
for a while and I'm not going to renew right so so you know yeah profit motive but like I don't understand product
management from that from that point of view yeah same here I don't I don't like this this we're going to start
including like convertkit did this where it's like you're now going to be able to sell digital products through us like
no I signed up for you to do email really well and you still kind of suck at email sorry convertkit your email creation
uh UI kind of sucks um so can you spend more effort on that because that's what I'm paying you for and not for selling
digital products I have a digital product platform for that it's called Pia but Pia why are you getting into email I've
got convert kit for that and I don't like your email and I don't like your blog posting and I'm not crazy about your
community stuff finish your product before you add other features or if you're gonna add other features great but like
also finish your product it's so like I you know I pay I happily pay for these Services because for the most part
they're really good but they're not done and and they really need to to done yeah and what's GNA happen is I I'll be
switching away from convertkit and I'll be switching away from Pia this year so that's fine then then they've lost me as
a customer and it means that that because there are other tools that are more targeted and doing a better job of of what
I want and so uh yeah that's fine they'll they'll sell to others and like you know some of these things like I can't
imagine it would take your your developers more than a few days total to implement some of these like the go live
message on Twitch that's an API call maybe two I've done it so what's what's the problem right yeah MVP but these these
tools are well past MVP these tools are are like they they've got you know they've got Market fit and so you want me so
now you got to keep me because churn is the biggest thing and like I'm I'm going to churn right out honestly I this is
exactly my thought I'm wondering it's like why can't you add these tiny little things that I've looked they are one API
call right so the YouTube thing one API call they you're probably already making it's the parameter to an API call you'
re already making why can't you do that how bad is your code so everyone says like you know ah you know we don't need to
our code to be whatever because we're you know but slow to add features I worry about the quality of your code and I
worry about the quality of streamyards code they have not done much in terms of about I can't remember the last feature
about so all these products I'm I I don't see me I don't I unless they unless they get get on the ball I'm not going to
be paying for them in in after up yeah well churn at some point is going to be a big issue I think churn is so much so
important right churn means you are gaining customers but you're also losing customers the most expensive thing for
companies is gaining customers that's the most expensive thing that that they spend money on is getting new customers
but you want to keep your old customers because they're they're otherwise the lifetime value of a customer goes down and
no investor likes to see that um I I invest in in some startups and and the the last thing I want to see is is high
churn because I know that all you're doing is is basically messing up and and not fulfilling what your current customers
expected and I'd want to know why it's it's very it's very much short short ter like looking at the wrong you metrics
yeah I mean ex it's it's it's like you know streamyard streamyard has me because the the layout stuff is just good
enough just barely good enough um I would love much more flexibility that other tools support but it's just good enough
so that I'm like all right like do I like this layout no not really would I like transparency because I have a green
screen behind me streamyard does not support transparency are you kidding me it is 2024 every single other streaming
platform supports transparency why don't you it's not this is not something you develop it's an out-of-the-box thing
from from some Library probably in the libraries you're already using it's already there but it doesn't have it and so
now have this side by side and so all this space below it's wasted um but it's like it's so it's just good enough and
there's some other stuff so bring in guests is is is the main feature besides the multi streaming that that keeps in the
streamyard but otherwise I'll I'll you know and if it doesn't get better I'm just going to go back to OBS and so I still
do a lot of solo streams um using OBS because streamyards uh basically it's streaming support and so on is is is just
not what what I want so so unless they unless they kick it into gear I'm I'm G to leave them and I'm just going to go to
a service that just does the multistreaming so there's another one called restream I wouldn't use their Studio or
anything I would just use them for restreaming uh and then you know then streamyards lost me as a customer and I'm
paying for like not the bottom not the entry level I'm paying at a higher level and it's like you know you lose a bunch
of customers like me and and you're out of business well maybe not maybe maybe I'm not their primary customer whatever
the one thing I will not do is write my own like there's there's a whole class of products where it's like I could
absolutely um write my own replacement for and and just do that and and I've done that for some things but uh video and
so on is not is not something I want to do or I might just not need it anyway if if Comcast Xfinity ever gets um better
upload speed with they which they've been promising for a a this like you it's available it's like no not really um
because once I can do that then I'll just multistream streamyard so they're gonna have to do more to keep me because I
can use I I can do I have options when I have I really think I was surprised it's like am I just missing this feature or
is it just not there it's just not it all right let's let's let's uh let me get back to to to code okay so what I want
is I so this this stuff in terms of these things um do the Multistate because I think actually that's a bit much uh so
actually let me undo uh let me just delete this grab um change the state with multiple targets uh and we'll basically
grab this thing and put into the controller and stick in a post mapping here we'll this anything so this is socket uh
because this basically connects to to this more more precisely that way so the idea here is um this is the post request
coming in websocket Broad broadcast out uh then this example will be a button bya the websocket that does a websocket
send whoops a websocket send um that doesn't that would would go through the handle text message so that's that's what
we're doing here um oh we're still here okay uh so let's this and so the side effect of this is update um but actually
we we'll just call send what's the message what the message we want is basically the current state want um our swap
Target uh because we want to do two things as as as a result of this so uh we want to update button text and then so
this is the ID that we're going to replace uh that'll be date so our swap Target ID equals that and inside of that that
uh so let's Target inside of that will be the current state which will be S we'll do formatted that guy uh and then we
want to update the button text and uh that's also going to be a swap Target so note that swap Target here this HTML
element is is irrelevant so what I've decided to sort of standardize on is when I'm sending a response from the server
and I want to Target using What's called the the of band swap which I think is as I've said many times I don't I don't
like that name uh I prefer sort of uh targeted swap so what we're doing is we're saying find the ID here and so this ID
is um this is button and so the element here doesn't matter we just need some kind of HTML element that has an ID and
what it all it does HTM X will look at this ID and say basically find it in the Dom find it in on the page it's like oh
it's here let me then take whatever is here and replace the content of of the element uh which is by default that's
that's the by default inner HTM L replacement uh thingy brain not in gear um so here what button uh actually this is the
button text here what we want here is the current want now we want to actually send that um and we can basically just
concatenate the two uh and just send both of the back those both of those back so we'll say send uh update current State
Plus text uh we'll just add exception state um updates the current generate the update current state which is this uh
and then update the button text which will basically be one of those so if this works should here we want the HX swap to
actually be none so what this means is the post request right this post mapping request even though it returns void uh
you still end up getting a message returned uh uh it basically just no content um and if you said enter HTML this might
uh be replaced with an empty string what we actually want to replaced with is uh generated over here so if this works
correctly we'll rerun that application refresh this page refresh this page uh click me whoops close so it says currently
active uh but I appear to um oh I I I forgot to to specify how I want the swap to happen on this end so here I want HX
swap out of bound out of bounds I say out of bounds it's out of default that there we go so note that as I do this both
this and this and this all change when I click this button whether um so this button is reacting uh this button
basically sends the post request and then we broadcast out though through the websocket so that's HTTP request in
websocket out what I want with this example um is uh use wsn to do the to do the post right so I want now here not to
use HTTP at all I want to use the websocket transport to send this request oh yeah I mean that it's great it's great
absolutely yeah and totally like um Mak security stuff much easier something that I'll get to probably not today uh is
some of the authentication stuff um or the authentication authorization uh websocket related stuff commit so Post in
websocket broadcast whatever all right so I I I'm just I'm just fascinated fascinated by how intellig is deciding how to
indent some of these text blocks uh this is indented 12 or it's indented four from the triple double quote um this one
that is indented I don't understand the I don't understand intelligent indentation policy on these on these text yeah
pixie report that's um that's kind uh so I think that I think that's true yeah so let's let's check the docs on that oh
astd I um I'm afraid to tell you this is normal for me all these tabs um this is not the only window that has this many
tabs I have a problem I X the HX swap we actually want uh swap so because um HX swap specified know so here it's like
the first div will be swapped into the Target in the usual manner so whatever the return and however that handles it
yeah so if it's not specified um this is what happens so if a SE selector is given right the ID which is what I use as
the selector uh all elements matched by the selector in this case only one will be completely swapped so the ele so so
by default and it would be nice if this was more clear by default it's an element swap which is what we observed so that
makes sense yes I agree as that's yeah it's it's like what it's usual if you're gonna say usual then at least link to
what that usual is so um for HX swap o uh if you don't specify it then it then it then it which uh means you haven't
specified an HX swap at oob uh then um then that's what happens yeah that makes sense so let's write let's make a note
to ourselves that that's happened uh so HX swap is inherited o so basically it's kind of like the default is outer HTML
if you don't if so if you don't specify it at all it's like you did an an outer HTML so it replaces it just throws away
the old element Pops one yeah so one of the reasons this sort of turned into more of a tutorial is is I was a bit
frustrated with the lack of quality what I call worked HDMX yeah that's where the button went so what happened was um we
did uh if we if we didn't have this this swap um it basically I assume it kept it as a I don't actually it probably
replaced it as a swap Target which is a meaningless element and it basically I think it's just treated as as a p um so
let's let's try it again uh and we can go and inspect um the the HTML let's go here inspect yeah so it did a complete
replacement um and so yeah so it just treats it as a regular text node with no anything whereas we saw with the one
where we did have the the swap o o right so on this one the target was this H2 and so the H2 remained with all of its
other stuff uh and just the content changed so this is repl this did the inner HTML and this basically did the outer
HTML so it tossed away the button completely through in the swap Target and and there we go yep I you know the the more
I do this like I I I have a presentation on sort of just learning in general and how you can use it to inform things
like documentation um but I've had a bit of of uh folks asking about hey can you sort of expand on on that specifically
as it pertains to to tutorials and documentation um so I might do a more longer specific thing on on basically the
approach I'm taking in writing this particular tutorial yeah so this technically has a node because it's called swap Das
Target is the element but that element um and this is something that was you know way back when HTML 5 came out is like
hey you can totally Define your own element and if the browser doesn't know anything about it it'll just default I do I
do it really is and that's why I'm um uh uh that's why like the current book we're reading the book club uh the
programmer's brain which by the way join um we're picking it up with chapter so it's still early we we're just about to
finish chapter 2 and get into chapter 3 uh a week from yesterday uh so in six days on Sunday we'll we'll we'll discuss
it so you're welcome to join uh just hit Discord and yeah it's really I I it you know for me it's it's um I studied it
because I wanted to to to learn more about how people learn since that's kind of my job is how is getting people to
learn uh but I also have have long been been um uh kind of a an amateur research not researcher in ter in terms of
Performing research but researcher in terms of reading research and sort of integrating it and and so on so there's a
lot of very interesting stuff that um yeah you I was I was talking with some folks this past weekend about that it's
like I hope I'm not like just you know overwhelming you with with pieces of of use of information that I find really
interesting because once you get me started on that it's really hard to stop uh so anyway so that's what's going on here
um so when doing a targeted replacement uh um if you specify HX swap o o to True so it's basically as if you had
specified OB now we know what's going on there let's go back um so there's teachers and then there's people who educate
teachers and then there's standards and it's honestly it's a political mess it's just a mess um there is evidencebased
research and a lot of folks just don't use it oh that's interesting an actual an actual degree program yeah it totally
deserves it hey there b BL yeah there's there's so some of the stuff that I'm trying to post in like I could give you
really I was trying to read I was trying to read um on the plane this weekend I was trying to read uh a book and I was
like I can't read this like there's at least two words per paragraph that I need to look up um and so I'm trying not to
provide studies that that use a lot of terms and knowledge yeah STC is is sort of I think what we call it here in in the
US yeah it's definitely um and it's also the um write the docs wri I te write the docs um that's an organization that
holds conferences a couple of times a year uh and actually one of my talks on human groups um great all right so this
this worked exactly as we want now what we want is websocket in to broadcast uh okay so want um now we need to make a
decision here so this is this method handle text message uh is what gets the the the text incoming the incoming text
over the so in this case what we want state so how do we want to change the I mean I guess just the button could do it
uh but the button gets posted so what what do we get so let's let's drop the hidden input um I think because I don't
button uh we can set the button type to be submit uh look we've got an HX swap interation ml here um so let's see what
we get uh we actually want I actually want the whole payload so let's just grab give it the whole payload and see what
we get so we're going to get a bunch of headers uh but I don't think we get anything else and I think that's why I had
the the input field um I don't know if I can put something on the button to to change that let's take a wrong um so this
is our Target oh I got I didn't get the full Target name right right so here's here's our stuff we see the um the
headers um so we find out who triggered it which was the websocket form uh what the you incoming URL is but there's no
other there's no other data so I wonder I wonder if we can send something in via the button or if we need an name do
value I have no idea if that's across oh it does oh well that's awesome all right so what we can do is we can create a
name value pair uh and that will get sent across as a piece of data in the so I I I think it's it's is that it's it's
kind of funny it's like for the most part HTM X you're not going to use Json but when it when it does basically send
stuff over the web socket um it it basically uh send it as a as a Json blob so we can now do is we can um basically
create a name value pair that will tell us that this is a command so the name is going to be um I'm going to call it a
websocket command uh and the then map um I mean to a certain extent we don't re we don't really need a name value pair
we can just have a a name uh because know yes pickle p i KL I believe any I thought it was more of an alternative to
yaml but maybe maybe alternative to both I I hate yaml um and Jason's fine for for certain things but not as like
configuration data um unlike a lot of the Apple open source projects this one actually looks interesting um hands
command um and if send uh we will actually do the same thing that we do here we'll update the current state right so
that's that's that's this thing uh and then we will update the thing uh what we want though is we want these IDs to ones
yeah it feels like it's it's more of a of a yaml killer which I'm totally fine with I don't we use so much Json for uh
inter service transport that I don't see that getting replaced um but I certainly see yaml getting replaced I don't I
don't know that there's anybody who's likes 100% yeah I actually prefer tab separated as as Mike and I are doing with
with the song not because of importing from spread but tab is a character that you don't generally or or pipe separated
but commas commas make make the parsing harder but do this so let's say uh can um good code versus like readable tuto um
we'll do this but this is uh prefix with a uh this is terrible code but this is not meant to be clean code not see all
right uh close it updated the button um me I didn't actually update the state that would help the other thing is it
didn't seem to update the Ws post it there we go look at buttons are updating the state So currently active activate
currently active currently inactive activate currently active uh and both to the server and from the server is now
happening over over websocket um so we can see them synchronized uh whereas these are happening over um a post in and
then a broadcast uh same okay so uh is the latency different it I mean this is all Local Host so I it's not going to be
noticeable where it would matter is if the server is much further away um plus it would also depend on and honestly I
don't I no longer know how the browsers internally work would it open up a new so the websocket remains open so there's
no additional uh time spent sort of setting up the the TCP level connection uh whereas for the HTTP post request there
might be a need to set up a a connection then send the HTTP message um and it depends on does does it keep that sort of
pipe that connection open or not so for the the post might have a slight bit of additional latency over the websocket um
and I generally want to lean towards using the websocket because it's already there why not put you know do everything
over over the websocket the downside is it's a little bit um more complex to handle uh but that's where you could
probably write a a class that that makes this easier because right now obviously I'm having to look oh is this incoming
thing a websocket command and so on but obviously that you you could write your own annotations and things like that
which I I might actually do yeah so we could look at the the Network Tools um that's my bet as well I don't know what
the limitations are I don't know if there's sort of a timeout uh I honestly don't know and and that stuff um I mean I
don't think you there's this if you're seeing it uh you have better eyes than I do um but if we open uh let's go to
network and we'll look yeah we'll just keep all I mean it's all Local Host so it's all fast uh second seeing oops let's
try it again oh because it's all under this here I mean heck it's the same two milliseconds it's like whatever the
minimum amount of time that that it can measure um so all this all the state changes are happening over uh this
websocket state connection uh so yeah there there's there's certainly at this um you know from my browser to my server
on the same machine there's there's no difference and I doubt there'd be much observable difference unless you're unless
you're like really far away um so maybe you know if I put this up on a server here in California you and Europe um it's
possible you'd notice it and the amount of data is so small it all fits in a packet anyway so time so we can see that um
the websocket command came in and then three milliseconds back so I don't know maybe the websockets a millisecond longer
but you know that so web that yes exactly measure profile first then fix I um I already have this some what uh what's
interesting is this one um and that's definitely related to this get we got a connection so here um I don't think we get
much like we get an ID but that ID is just for the standard websocket session uh yeah so if we want to now associate it
with the users it's really oops um this really needs to come first authenticate uh before we can associate with with
users so this is that with sockets so uh do I have that's a good question um it so apparently it re reuses um the other
stuff um and so just in our websocket security provide security so what'll happen so the way um do they provide a
diagram here no so I will say the if you're if you're writing documentation especially I I think this applies to a lot
of things but um especially this kind of documentation where there's communication between client and server diagrams
should be required I think it should be severely frowned stuff because there is back and forth uh and um mainly thinking
about this inbound connect message uh happens as part of I believe the um the websocket setup uh and I forget the
websocket setup protocol you basically have to fact you might even see it here running yeah so we see is um there's a
101 which is change protocol uh and then everything else is over websocket um so we could look up uh socket here we just
uh is this what we want the websocket this this is a subprotocol that's not what we want um right protocol so two parts
handshake and the data transfer this is the hand shake so this is the upgrade request so we're basically send a message
which is a get request saying please uh upgrade us to websocket the then we have some websocket key we've got the
switching protocols and that's it uh so the security model use the same origin model that makes sense and there are sub
protocols not going to worry about that um there's the Ws connection connect it so it looks like when it does the
connect um it's going to require a csrf token unless we turn it off uh the security context holder that's the thing that
would hold the principal um because we're not using the messaging architecture we're not using stomp we're just using
the lowest level websocket and I'm not I'm not 100% sure this a this actually applies and what TP tipped me off is um
there's uh this the quote simple um template stuff which for whatever reason they they shortened to to simp maybe it was
an acronym at some point I don't know um but uh that's if you use the broker version or so the broker based websocket
here um regardless this is authorization uh but this concerns me that this is does not apply to what we're doing I think
this is this is the really what's happening uh is is this just going to use whatever you use to to to initially set up
right your your initial get right so whatever whatever authentication information is found in the HTTP request when the
websocket connection was made which presumably means uh and we can try it out or we will try it out uh whatever get
request I did right to for example uh where is it yeah this page so this page sets up the websocket connection because
we've got that right here so whatever page served this up that seems like what we'll get it there's a a phrase that
Brian Merrick uses that I I use all the time it's like an example would be really useful right here an example would be
great right about like well let's write one uh so let's go ahead and add Spring Security yes Mar's maximum uh a diagram
would would help client I don't want to write authentication uh I could use kind um now that we know how to set that up
up it'll take all five minutes as opposed to the two hours um let's just do basic security for now client oh 323 came
out I can upgrade to not well I guess the why not is it's going to scan things wow that's really doing a lot of work uh
but in the meantime let's set up Security um let's just do username and password I I always whenever I look at this I
always feel like it should be labeled folks do not do this do not do this at home let professionals do this uh and you
are not a professional which applies to me because like I think this is just just don't do this use somebody else use
somebody else's uh use keycloak use uh um Commercial Services like you know Fusion off or kind or or other stuff don't
don't roll your own don't roll your own I mean at least don't start rolling your own off but let's just copy copy this
because that's not the purpose of this particular tutorial uh oh can I just paste this in in I love I love I love
intellig is hidden you know you can just click here and paste a bunch of text and we're going to do some magical stuff
like create a class for you which it just did I just did a paste um or past it into various areas of your uh settings
and live templates and that's how you can import easily as opposed to doing other config any request authenticated no we
don't want to do that what we'd like to do is um test matcher uh so we only want to authenticate our our websocket page
authenticated so weird not to end a line with with a semic production uh I totally get this this is not is acceptable
for demos um but yes do not do this so I'm glad I'm glad they uh so we're just going to do user password that's fine uh
it'll have a rle fine yeah I I I I would I would clarify professional as you get paid to do security uh that is your
that is your job not that you get paid and you happen to do security is part of your job you are a security professional
if that is job yeah uh I believe it will we we'll find out yes and you continue and you and you don't lose your job yeah
although that doesn't necessarily tell you you're you're actually a good professional there are people who should have
lost their jobs in certain cases and did not um let's run it and let's here considered unsafe for production it's kind
of funny you you almost I almost think like couldn't you put it in a different color to to stand out even more um so it'
s going to secure any request um oh this is too long uh let's do that secure a whatever let's yeah I almost feel like if
it's not running at Local Host you should just not even start with with this authentication uh let's go and I think we
can close that Local Host this should be fine uh no I didn't specify anything for anybody that and that would not be a
bad okay there we go the little misleading that message because I didn't use MVC matches I used request matches but
underneath it uses MVC matches all right so let's try this again right so no authentication needed here um but if we
want to go to websocket now we need to log in uh so presumably um so the question now is is when I get is question let's
look at websocket connect oh there it is get principal tada does so sui asked suppose you have a DB full of emails and
hashed uh passwords yes hopefully they're they're well hashed um depends what you want to move towards uh I mean at yeah
depends on what you want to move towards but T the typical way to do it is um basically push them through the reset
password process because yeah you you're not you don't have the original password so yeah passwords yeah typically what
you do I mean it depends on if you want to force them through that process uh um or if you want to to have them do it on
their own um what I usually see is you've got a certain amount of time to do it on your own and then we will push you
and force you to reset your reset your password you want to move towards not having their passwords uh well somebody do
you want mean to mean they don't use passwords to log in or that you don't control their password passwords like are you
moving to like a Service because yeah the magic login bya email there's usability issues with that but if you're just
moving that you don't want to handle that anymore um then you pushing through a reset password process and then uh when
you collect their email you could basically redirect them to the new you know let's say we're using kind uh you redirect
them to kind and then they log in through that and then you get your authentication um and you'd have a a column in the
user table basically saying how they transition to the to the external off if that's what you're what you're doing and
then you then at some point you scan through the table say who has transition all right we've got a principal oh look at
that they're already connected because the page reconnected uh so here our principal our principal is username user and
the password is protected well that's good all right well there's our security that was easy yeah so and this is
something that I know some vendors will help you with um uh either directly or we'll have some some documentation on how
you might do that uh but at the very minimum if if I were to just sort of off the cuff what I do is yeah what I said is
like look in the database see if they transitioned um if they have then then just redirect to that one so notice that we
have the entire easy um yeah we got the principal um and we got that with the session connected um because that's
associated with a session which means means we will get it anytime we get the session which we get on any communication
um so if I do a button click we got our text message received uh yep so we're this and text message received from
Principal um and we have their granted authorities so hey that's it we're done same good old PR principle to string so
um now we could add ooth if we wanted uh and then we'd get whatever user roles and stuff from from whomever um so this
means that we can now associate specific users uh so if we wanted to do something like sort of private chat right so the
chat example I have is basically whoever types anything in is broadcast everyone but if you want it one to one or one to
some group um or only to admins or something like that you've got all the information you need to to make those
decisions and that's just that's just code um maybe I'll write an example of that so somebody I forget who it was
somebody uh on one of my streams was asking about sort of a customer service like thing so it's a an agent to customer
so one to many uh kind of thing um and so yeah you you could this will be straightforward um here they're very dumb Dev
uh yes HDMX yeah yeah I think once you get over the hump of of realizing that you're ret turning HTML um and for me
understanding how the swap oob stuff works um it's really nice I mean all the all all the stuff I've got it's like it it
doesn't require any there's no JavaScript well at least no JavaScript written by me principal why why can't I get the
user details I probably have to oh I probably have to cast okay I won't do that okay um what here condolences I am yes
I'm I'm quite quite anti-a for the most part like architectures don't just use spa for everything don't just use
hexagonal for purpose exactly uh all right so let's let's do a commit okay um do I even need to specify with defaults
out not found how do I log out is the default logout mechanism um so I've got spring boot starter SEC right I added
spring boot starter security and I have enabled web security work oh my God JSP files oh my gosh 10 sorry I every time I
I I open up a a project that has sort of non-trivial JavaScript like basically it it has to bundle stuff together it
just like takes me so long again applets that was the my my first yeah you can't log out so I was trying to check out of
my my hotel this weekend um and the app didn't work it's like the app was so broken uh the hotel offered a digital key
and I'm like why are you doing this like it never works and then you have to check in anyway so what's the and then you
give me a key so what's the point um and then the digital key didn't work so I had to use the regular key anyway uh and
then I couldn't couldn't check out through the app but I could website software sucks is is my general days yeah I could
drop the cookies but I out because it should it should have set yeah it said it should set the log out filter unless it
logged me out out that's interesting it said confirm log out somewhere but that must have been on uh no static resource
is log out oh what no static resource logout I don't mean I mean I guess I could do this but that should be unnecessary
I don't know what that means really great oh do I have an exception that I'm that the handle request so filter chain
filter chain Anonymous authentication filter exception translation filter that's too late configuration filter filter no
static I'm actually surprised I wasn't able to Google I'm I'm kind of amazed that that that a search doesn't find this
oh my is but I'm not using JWT I don't understand right there's something I'm missing I'm not going to worry about it
now though yeah I I it requires a lot of understanding of internals and I it's the thing I yeah uh L out can be a post
request but it explicitly says right here you can if you request get log out then Spring Security displays a logout
confirmation page that uh does not appear to be the truth at least I've different because it's supposed to generate the
get log out um unless that was the customization here so that's possible uh I I don't understand though why I would need
to set this up if if it's just defaults because if it's just defaults aren't you already using the defaults so maybe
this is this is what I'm missing if so that to be documented so let's try it with that uh let's go Local Host over here
websocket we're already logged in we aha so the docs are basically saying um if if if you do this then it will set you
so my guess is this form login is out if you don't you don't get log out in fact you don't get loging either which is
what I was trying to test I was trying to test if I remove this what happens to log in um all right so now I can log out
so let me log expect whoops uh let's rerun God yeah I have I have two other pending PRS um that I need to submit to to
Spring uh with respect to the ooth security docs um but it's so painful to to submit yeah so if you don't set up the
faults it doesn't set it up at all is what it appears to be uh so let's refresh go to websocket and now you're just
forbidden um like the uh maybe maybe I I might need the support uh apparently nobody because I can't believe I can't
believe that I'm the first person who's this and to me this goes against the spring boot philosophy of working out of
the box uh I can understand not setting up HTTP basic defaults and maybe form login requires that so may so maybe it's
somewhat understandable but um but then uh this is insufficient because this is this is true misleading yeah it's only
true if you've done other things um all right uh so let me make a note of that um because I the the dispatcher type I
started writing it and I got frustrated because it was really annoying to edit the because basically to submit a PR um
you're basically editing the asky do of of this documentation and it was actually um what I did like is is there's a
direct link here to edit this page so uh so that's really nice but all that but it's not quite edit this page and then
takes you where you can actually start editing it it takes you to the source of the page from which you uh can't edit it
you actually have to go and uh and Fork it like the process itself could be improved a bit let's put it that way so all
right so I'm logged out um and if you don't have that stuff active you don't get okay yes it's it's way better than
nothing it's way better than here's here's the link to the GitHub project go figure out where the a do file is yourself
um so definitely way better than that uh but still not not not quite there um there are other um there are other
projects that make easier well you can because what you can do is you can you you could take them to to uh uh and
provide more details on okay what do I do next um so it could automatically put you through the process of forking the
page yeah Juke is is I I actually want um more I haven't played with it in in in years but uh it's always been very yeah
I really think that that I mean this is it's frustrating when a project is open source and they say we welcome uh you
know and especially you know projects I think every certainly at least every project I'm aware of wants to encourage
documentation contributions um but if you want that you you have to lower the friction to to zero right people will
submit code and go through hoops to do that but to submit doc changes you want to make it zero friction because any
little friction means I'm not GNA do this now right which is basically what's happening right now it's like H I'm not
going to do this now yeah so so yeah so take a look at the the the Juke project um if nothing else uh it's a very
different way of interacting with data in your database and I think it's it's one that should be used more um I think if
you if you sort of exceed the the the needs or I guess the if you exceed what um W Brain Brain Freeze if you see sort of
what spring data jdbc provides uh then dukee is is is basically lets you write very squel like uh statements but using
very strongly typed Java code uh so Juke has like any good open- source project has two ways of make has has a way of
making money um if you want some certain features I don't I don't forget I don't remember what or if you're using
certain databases so basically they're saying if you're using a database that you're paying a lot of money for you can
throw some money our way but if you're using it with pay yeah that's totally valid J give you some better type safety
but uh just writing SQL is totally fine um very much agree with this uh so Dan Vega one of my favorite uh spring Dev Dev
Advocates um has had a recent video on on on five things are doing wrong with with spring boot or something I haven't
watched it yet uh but it's on my list and um I was think of of doing a similar video where it's like you know the number
one thing you're doing wrong with spring boot which is using spring spring data jpa I think I get a lot of hate mail for
that though Dana when when YouTube changed their Dana and so yeah so five common mistakes spring developers make I
haven't watched it yet but um stuff you in L yeah great oh I'm sure it would be very it I mean you know that would be
definitely a polarizing um uh article yeah so Juke if if the database itself is is free um then Juke is free barring
some some extreme situations uh any database that's paid db2 Oracle in general I guess SQL Server uh you're something
yeah so the so the main problem with with so many problems um is it it gives you all sorts of stuff that you don't need
and so all sorts of so I would love for folks to tell me what projects they think jpa which is really synonymous for
most people with hibernate what projects they're using it for and why they thought it was a good choice because I don't
understand it I I have yet to see a project that actually leveraged the features at least in the last five years um I
absolutely created such projects in the early 2000s but I've less I've yet to to to see a modern you know past fiveyear
project um using jpa that actually needed its features of detached and lazy loading and all that kind of stuff uh and I
can totally understand if you're connecting to like a legacy database right that's got hundreds of tables and you want
to you know and you you you just have to read it and do stuff with it and it's not set up in a way that that you can use
any other thing that I understand um but I'm saying if if it's a generally newish application why do you want to deal
with lazy loading and detached entities I I don't I just don't understand it and i' I'd love somebody to to give me
examples so there's there's really I think there's three Alternatives um one is sure you could use jdbc directly and
write your own queries um you probably want to use something a little bit more abstract on top of jdbc so something like
jdbc template or uh uh what was it J bi was mentioned um the next level is sort of using some some tool so Juke is one
uh and spring data jdbc it's to me that's just enough om so you get the mapping you get it writes the SQL for you uh but
you can always write your own if you need to but it provides sort of just enough without it's not caching not doing
detached entities it's not dirty checking it's not doing all this stuff and wrapping every single entity in a freaking
proxy um it just but it does just enough you still have to write write your own schema generation but you can even work
around that with with some other things um and so it's just enough and that's jtbc um yeah I mean if if you've got if
the DB scheme already exists and it's not perhaps Well Suited uh then you then you might have to fall back um but I'd
first take a take a close look it's like is it is it really just not a good fit which it may not be um and you can still
use right so spring data jdbc is not you must use it for everything right you do it on a per repository basis uh and
then you can just jdbc template I mean or Juke right depends how much you want to sort of I mean Juke has its own
learning curve uh but JD like jdbc templates is fine like if you already know how to write the you know learning how to
write this the SQL queries unless they're really complex that I don't I don't see Juke as as an in between um I feel
like it's just a very path uh so you either want to go for more traditional om which is spring data JP and jdbc those
are orm right object relational mappings you you create your your objects and it figures out how to map them to uh to to
SQL um Juke is is just not really an omm uh so it's so it's just a very different different path oh swegi I just noticed
your your Prime resub thank you so much 14 months thank you another thing streamyard doesn't do is it doesn't forward uh
requests and and and subs and stuff like that to the streamyard yeah I mean you know there's a lot of boiler plate with
JD like I've written direct against jdbc and you just don't want to do that because what do you get back you get back
these result sets and then you have columns and you have to figure out what the column is and then you have to figure
out what type it is and then you have to map it to the right type and so there's a lot of there is a lot of boilerplate
right there is a lot of you're just going to be writing the same code over and over again and so for that stuff yes
let's use a decent abstraction um but with a lot of these you know like even with with spring data jdbc uh you can have
it do the the mapping of here's the results that I get to an object and then write your own query so you're doing the
sort of the tedious part that can be automated and you're letting the um the RM tool do that part but it doesn't have
the objects don't have to match tables um maybe that's a a not common knowledge um they just have to match what results
you're getting back right so if you're doing a select and you're doing a joint across tables um that's basically
referred to as a projection and you can map that to to an object and you not reading result sets and parsing parsing
those um don't use jpa unless you really need unless you need it but make sure like and this is you know if there's a
theme for today it's like make sure the thing you're using you actually need right so if you're just taking requests and
and sending out Kafka events and you're not doing any processing in between and there's no logic don't use hexagonal
architecture and if you have a database where you don't need dirty checking and jpa yeah I I think there there's a
certain I mean I'll be honest I avoided knowing a lot trying to you know learning a lot about databases for for the
longest time like I am certainly no expert in in in SQL um but I can figure stuff out and I have a sense of how stuff
works underneath um but I think having I see folks spend spend a lot of time fine-tuning their hibernate mappings when
it's just you could just write just write a query figure out the query and good um all right um Siri here let me know if
I can be quiet Siri um I I think that's all for today so I think I mean there's still um that's really the answer that
we that we found and so then associating principle um that's that's That's all folks uh the next step is now I got to
write this stuff um turn these examples actually into text uh and then I might actually turn it into to a video but I'm
going to start with the text because that that's so uh in terms of streaming schedule as tomorrow tomorrow hold on what
did what did Mike and I decide um so streaming tomorrow uh which is Tuesday 9:00 am start so 5:00 pm UTC so great for
all you uh Europe folks love you guys love you folks um on Wednesday 10:00 a.m. so an hour later so 6:00 p.m UTC um and
I'll be interspersing some some solo streams in there as well um what else what else yeah so I think uh I don't think
I'll be doing any more streams on this stuff because I think I've got everything I needed to write the Articles um so
I'll probably go back to ensembl um though I do have some other stuff that I that I might that I might throw in so as
usual uh folks thank you so much for for hanging out with me I I I really appreciate it um and as a reminder book club
the programmer's brain never too late to join we're only just into you know almost through chapter 2 so lots lots of
good stuff left lots of good stuff to catch up on hit me up on the Discord if if you're not already a member uh of the
book club and and I'll and I'll pull you in um what else um and just join the Discord if you're not already not already
there so that's it thanks folks uh and uh I will see you next time or I'll see Discord have a good uh have a good rest
of your day and if your brain is as as fried as mine get get some get some sleep that's the most important thing get
some sleep all right I'll see you next time
