# ＂Song Themes＂ Episode 1： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=QvxQuh7rBb0

---

## Transcript

all right it looks like we are live hello folks and uh welcome to episode one of uh pairing with with Mike Rizzy on his
app song themes and so uh this is Mike's first time pairing on on a on a stream so uh is it can we um I think so do it
from my kitchen no my dining room once like years oh that's right that's right yes so this is the first time we've done
it remotely perhaps right definitely remotely uh but that's right I totally forgot that yes I came over to your house
and we did some streaming from there back in the days when I could stream from my laptop which uh I don't do anymore
although now I could because I've got a wonderful uh m m to Mac's laptop that could totally handle this probably better
than my current iMac but anyway um so since probably most people weren't there when when you were last here do you want
to just introduce yourself a little bit sure um my name is Mike Rizzy uh software engineer lean agile coach um
freelancer um radio DJ there's the Nick that and that last is the important one for for this for this topic right yeah
yeah I've been um a DJ in community radio stations a music DJ um since my undergraduate days uh back east and I still do
it even though I'm an old gray I mean blue-haired fart um so yeah one of the things I have kept over the years is and of
course you know um while I may be organized in some ways but some of us you know a lot of software Engineers are
organized people um I'm definitely the Shoemaker when it comes to notes as far as um so for doing radio shows I often
like come up with like oh I want to do a theme you know like if it's July 4th or uh if it's Halloween or I want to do a
show on vampires or something on um questioning patriotism whatever right and they're all in like literally handwritten
notes Word documents expr Excel spreadsheets it's just all over creation and during the pandemic I started slowly
consolidating them into a spreadsheet um to keep track of the themes but even that's not particularly well structured
and I was like you know this will be kind of fun to share with the world because there aren't many song themes websites
out there at least not ones that are full of commercials and are hard to navigate and right are trying to get money from
you um I'm thinking definitely alongs the line of simple app I don't know simple I guess that comes from magile so yeah
and I think you know I'm I'm such a big fan of thepoke apps right basically apps you know we have you know we have the
ability as software Engineers to to write these things um and like like you're alluding to is like sometimes we we don't
write stuff for ourselves that would really help um and spreadsheets you can take them a long way right for better for
worse large parts of our world run on spreadsheets uh but um the other thing is that like I don't know about you but but
less and less I'm less and less trusting of apps on the web because you never know when they're going to disappear um
unless they are especially if they're either a Google app because then you know it's going to disappear um or uh or
Venture Capital backed where how are they making their money you know are they profitable um and so you know even
putting the customization like making something really bespoken fit for exactly what you need there's also like I don't
there's a lot of apps that I might use but it's like is this going to be around for a while um I was using this app for
what's called history search and it's like and it's really great but they're shutting down uh and and this seems to
happen on like a a monthly basis so uh I'm all for you know as as much as as much work as it can be to to build it um
like my ensembl app like I could probably have cobbled stuff together with with other apps but I I just I don't know I I
like building stuff but I also like the fact that I don't have to be beholden to some some venture capital who decides
no we need to to Pivot yeah we need to Pivot or we need yeah or uh We've run out of money uh or we're g to change the UI
of something in a way that you really hate that doesn't happen often so it's funny yeah um when you were talking about
uh apps that have changed just like a couple weeks ago we were talking about the every noise at once website I think I
was showing it to you and um You probably you probably remember that so I went to load it up yesterday and there's this
big thing saying this is now an archival copy snapshot of the website because I just got laid off from Spotify few days
ago and this is um it was he was somehow pulling he was the taxon music taxonomist for Spotify oh wow he was he was
pulling this data from spotify's stuff if people know what I'm talking about maybe I should share yeah why don't you why
don't you share okay actually I'll just uh say hi to folks hey suiga and dudan welcome cool de rge o welcome hey baloda
nice to see you been a while and lexers wow look at all those people uh and X proof the short answer to your question do
I use my do do I use VAR no um that's the that's the short answer the long answer is it depends but mostly no do I need
to do anything I think I've shared okay yeah so this is every noise at once and it's every style or genre of music you
can imagine or at least as categorized by um Spotify and so you know dark might zoom in so that yeah let one there you
go yeah I was thinking about the the streamyard so like you know hard industrial techno um vegan remix free form
hardcore I mean I'm gonna scroll down look at how many styles music there are what's kind of beautiful about this site
though is that you're like oh what is Rockabilly well that one's not so um what does New England metal sound like you
can click on this and it gives you an example um of bands of that style and then there's also a way to play it which I
forget how to do at the moment that may be disabled um I have I don't think I've heard of any of those bands and I'm I'm
a metal fan so that's great yeah but it's just I'm more of an example of website that was really fun and you could get
on the rabbit hole in it um and yet it's computer hey Paige nice to see you yeah let me try this I have another one of
Mike ah suige thank you for the uh Prime gaming subscription appreciate that yeah I haven't heard I doubt many people
have heard of most of these German Jazz rap that's got to be interesting well you can tell that he just got because in
the app is now hung on my machine at least oh no yeah I'll just close it but you get the idea is here's a cool resource
that somebody built as a labor of love and well I would hope they open I mean if it's just just if it's a taxonomy I
mean maybe it can't be maintained but certainly it could open source the taxonomy itself I would hope that that's that
that's I think Spotify owns it he was tapping he was an employee of Spotify oh so is it just getting feed from oh yeah
oh that stinks well yeah interesting huh yeah but yeah he's trying to figure something out I could I was reading his
blog yesterday so yeah oh kuros thank you thank you also for your subscription appre apprciate um one of the things that
uh Mike and I have been doing uh is because Mike said hey let's work on this app and so we used it as an opportunity to
work on some things that we've been both learning from our uh a book club so I run a book club every Sunday we spend a
couple hours is a bunch of us on Zoom talking about the book uh trying to understand it better whatever that book might
be uh the current book we're reading is learning domain driven design by Vlad kov and um it's it's been an interesting
uh time because it's been uh a larger group than than we've generally had and so that's been really good and so one of
the things that um the book talks about and if you're into domain driven design you may be aware of event storming and
so we basically started by event storming uh this application um do you want do you want to walk through the the event
storming or do you want me to do that um either way I don't mind starting and then you can Okay jump in so let's share
it there we go and you'll probably want to zoom in quite a bit yeah actually why you zoom out yeah people a sense of
what's what my ability to uh navigate is a little bit slow um so yeah we've got this was from built from a template that
Ted found and that template was provided these step one two three four um approaches and so I'm going to zoom in on the
The Legend on the left here and this was sort of the different um stickies were using in the colors and what they meant
um so it gives you an idea of you know what we what colors we chose was based on this um and in the upper corner I guess
I should go through the process more than explaining the board that'll yeah do do you want to talk about the process or
do you want me to yeah why don't you talk about the process and you can yeah so idea of event storming is um you're
doing domain driven design uh at some point you need to figure out sort of do business analysis Discovery um event sour
storming isn't the only technique uh but it is a popular technique and one of the things that it does and I'll I'll
switch to my screen so I can H make sense navigate here um so one of the by the name you could probably tell one of the
things you start with is domain events so uh I don't have a link I can share shoot uh I'll I'll find that uh in a bit
because I actually do have a copy of this that I could share I can't share this one because this what is we're we're
editing um but I will share share a link that we can look at um but the idea of event storming is you basically start
with events stuff that happen that's significant important wanted to be known and be aware of by by the business and so
domain uh is the important thing in domain driven design and so domain event is something that the business recognizes
is happening so an example that you typically hear is item added to shopping cart uh order paid order shipped order
returned right all these kinds of things um that the the business cares about those are sort of high level ones but it
could be lower level ones such as item added to shopping cart item removed from shopping cart a different item added to
shopping cart another item added to shopping cart and so the idea is you know you can use this to figure out your your
business process and there's um an entire book on this Alberto brandolini is the one who who basically invented the
process uh and it is mainly done with um sort of in a large room whether virtual or real with the business people in the
room because you want to talk to them about the significant of events um oh thanks sui uh and so you pretty much start
with the main events like what are things want to happen then you can sort of backtrack from there or you can move
forward um but it's very much uh you're just sort of doing a brain dump brainstorming of of the events and then you
start backing up and one of the things that um the book talks about is this uh sort of the answer everything or the
thing that covers everything are are all of these pieces and so this a semi-standard maybe not semi there sort of a
standard color for these things based on Post-it notes that that were used by Alberto so orang is uh the domain events
commands are blue um read models or queries are green actors are yellow um and then what are called policies is sort of
this more purplish and the system is pink some of these uh change color a bit depending on the system you're using and
there's this this flow through the system is you know so something in the real world causes some actor to to issue a
command that results uh in some event right so I'm looking at a page I see oh I want that I click a button to add to the
cart that's the command so add to cart and then item added to cart is the event that would update a read model because
you've added it so now if you look at your shopping cart you should see that item in the shopping cart and there's a
whole bunch of other things but that's sort of the highlevel process um highly recommend the reading about it if you're
not familiar with it uh and so as I mentioned there's sort of three levels sort of the big picture where we're Gathering
events um and then we get to the point where we get to the design level where pretty much the business folks are
probably not in the room because you're discussing Aggregates uh and so this template that I that I got for For Better
or For Worse sort of goes a bit through those those three levels um was a bit confusing but we'll we'll talk about that
all right that was my rambling introduction no it's good I was trying to post to the chat I got one thing in but
everything else got failed to post I was sending a link to the event storming website and okay the lean Pub but alas so
I guess one of the things I don't know where you wanted to go next with this Ted but should I explain what the app is at
high yes I was I was going to suggest let's talk about the app it I'll switch over to you sure let me get my face out of
that screen um so the idea actually I'm just gonna talk and not use anything on the screen at first so the idea is like
I said earlier I have song themes right so um basically it's a single song it could be a song that's about vampires but
it also could be under the theme Halloween so for each song it could have multiple um multiple themes meanwhile you
could actually have multiple different artists doing that same song right so there's definitely a many to many going on
um so in some ways it seems like oh this is like a really silly easy app to do why would we do this with uh DDD and and
get all hardcore about it um and it's true at first I was like well let's just give it a roll and see what happens but
as with anything in software engineering I don't know about y'all but whenever I start work on something and whenever I
say the word just either out loud or to my own self it's usually an indication that it's more than just yes and so um so
some of the high level ideas we had were okay at the simplest level somebody could go to the website and they could type
in a single theme and then I would to give them a list of all the songs with that theme or they could type in multiple
themes right and we could give the list of songs with that theme um then there so that's s of the simplest scenario you
could think of um but then like well how do we get songs in do do I Mike Grizzy as administrator just dump them into a
database or do I have a way of entering them you know like either doing bulk entry or um one at a time and what if I
want to start letting other folks you know enter stuff and do I want to let him just blindly enter them or do I want to
consider him contributors such that I as the admin approve or disapprove them right like yeah that's a bit of a stretch
or no great thanks added so we started sketching out these yellow stickies which was highlevel stories and actually I
should backtrack so that's the high level of what we could do we got contributors and so forth we started with domain
events right at first and we're like ah we got stuck really fast um like what are the domain events right so I don't
know about you Ted but I feel like we got to the point where it's like I feel like we're missing a step here like
understanding our domain a little bit better even though I knew it in my head so we started sketching out like high
level stories like um oh I don't know contributor submits a song theme right admin approves a song theme update right um
or you know sub a song theme editor correction but you know the the easiest ones I don't even know if they're even in
order of easiest yeah visitor seches for songs with one theme right that's just a visitor is somebody that's not logged
in they're just at the website um yeah so so I think one of the things we we realized which may be so obvious that it
did it wasn't worth mentioning in the event storming book or resources is that you already need to have the business
process in mind like basically you have to have a good un like you can't come you clearly can't come up with an event of
song added unless you understand well how do songs get added and how do contributors contribute songs and how do we
correct songs and how do we do things like that and then so um that's why as Mike said it's like we we had to sort of
back up we were we're were having trouble coming up with the events because we didn't have a clear understanding of what
the the thing did really I mean we had a general idea but like you got to get to the point where it's like okay really
what is what does it do so that's when we we we came up and stories and so once we did that the next step was okay let's
let's figure out what the events are the little green diamonds were us going hey do we have we created all the events
for um for that story so to make sure we sort of didn't sort of like a check mark make sure we got them all covered um
and then the first step yeah so suiga asks suppose somebody's already doing some things manually or has an actual
problem to be solved and yes so clearly Mike had that in mind but when it's in your mind it's pretty ambiguous until you
get to the point like and okay really what does what does it look like what does it need to do and I think you know uh I
think Mike you'd probably agree that this app is pretty basic in term it's pretty it's pretty thin in terms of like a
business process which is where how event storming is like you know when they talk about event storming they talk about
you know hundreds of these stickies of these event stickies where it's clearly you're working on some kind of complex
thing um this not so much like actually most of the complexity or at least a fair amount of the complexity is around the
contributors and and and invites and not just if it's just you adding songs and searching it's like oh there's not not
much there and then there's there's other ideas that I came up with the last few days did like one was like a um a
suggestion um engine for lack of a better word so if somebody types in they want themes about you know summer it could
say well do you also want songs about heat or sweating or fire or you know getting a little bit exem on the fire and um
and so forth so or if you're doing it searching for the word fire themes with the fire are you doing it because of you
know there's a fire 100 miles north of where you are or is it because it's just a hot day right have something right but
it could get complicated pretty quickly I'm realizing but this initial version yes and business logic you're right is
pretty thin yeah it's most but I think we found as as we sort of got the stories and started getting into it um it it
brought up some really interesting stuff so uh so X proof asks what's a domain so domain is uh a problem to be solved so
um often we talk about business logic but not all logic is directly associated with business per se um there may be
support things or maybe things that aren't business but are other uh so generally the the word domain is used um if you
have not read learning domain driven design or any domain driven design book uh the term domain is actually quite subtle
nuanced um but at a high level it's like why are you building this thing what what's the problem you're trying to solve
and so for this one the problem we're trying to solve is want to be able to find songs with a theme um but really the
problem is is is m managing that not you know basically how do you add them and find them and update them and correct
them and allow other people to correct them and add to them um so but but all into the the I want to be able to find the
song with with with this themes but all the terms around subdomains and generic subdomains and and core subdomains and
all that stuff that that I will just defer to to the book because uh you'll you'll want to get a and and it's often
confused with bounded context but um we'll probably get into some of that do we want to skip over uh or just go over
each of these quickly the different steps yeah I think maybe just go over the first step and say so this first one was
just a blurt of events right that we could come up with they weren't necessarily in a timeline um they were just like as
we could think of them based on the stories the next one was was this one timeline yeah this one was timeline is step
two sort of timeline but also kind of affinity grouping yeah like you add a song song's modified somebody wants to
update a a song or you know to accept it or rejected so there sort of grouping and then if you want to so one of the
things we didn't talk about was we want the idea of at first I'm going to invite people to be contributors to the site
like it just won't be open to the world right first kind of like the way um Ted does invite for things like the ensembl
and so forth um so we would have the idea of me sending an invite out and the person getting that contributor role
letting them be notified so it'll be interesting because we'll be tapping into you know sending emails and because that'
s the notification system we originally settled on yeah um so so Endo funter zero asks do you include the actors in the
first step and the idea is no you don't introduce those until later the the bulk of the early work is just finding the
events um and then uh then maybe grouping them together and then we'll see the next step is is is starting to put them
in some kind of order of of occurrence right so yeah and then cont contribution submitted approved and rejected so
that's that so here is where we start getting into actors to answer endofunctor zero and normally we don't keep copies
of like step one two three four we kind of did it for y'alls to so you could see how we did it but normally Well
normally you do this in a room with stickies on a wall and so you're moving stickies around exactly and for for a mirror
board you would be doing the same thing because otherwise you get into the problem of wait did we cover that one right
because we were coping around it's like wait then that's why we put the little greenen things it's like did we copy this
one do we put it in the right place yeah yeah so we learned we know you're not supposed to reason but we learned just
actually makes it more complicated so don't copy and paste your board yeah so in this templates step three is called
track causes so now you have the events they're kind of in some kind of sequence maybe grouped together um and now
you're basically trying to find out well okay these events happened how why what caused them to happen um and generally
you're going to backtrack all the way to at some point to an actor um in our case I think almost all the actors are
actual users but that's not always true a larger system could be another system that is the actor uh that sort and so
just as you can see actors are yellow external systems pink pink is command is blue and the view read model is green and
the flow is usually or not usually it's always a command always generates an event right so you always see blue orange
as a and so when you're when you're trying to figure it out and you see an event called song added it's pretty likely
there's a command called ad song and if you see one called song modified it's pretty likely there's a command called
modify song so that works out really well do you want to mention the problem we had with with with queries and uis or do
you want me to talk about it right we did struggle with that I'm trying to remember what specifically what it was we
struggled with it so why um the way that event storming is supposed to happen is after you've got the events and you
sort of you know affinity group them and then put them into uh you know some kind of order right so invite sent is going
to lead to one of two possibilities either it's accepted or expired we didn't have a case for somebody just rejecting
the invite we figure if they don't if you don't want that invite or maybe you didn't see it it's probably going to
expire um but if it was accepted then a roll is going to be assigned and and contributor is going to be notified uh so
once you get those when you're when one of the things we we struggled with and I think we struggled with it actually at
the really just right up front where we're trying to figure out the events um is this doesn't work well when the sort of
the rights the modifications to the system are a small part of the system or like the main thing that you do with this
system is f stuff right queries um those aren't events so we actually initially put those in as events because I think I
came across somewhere as being maybe a something to do um but an event is a state change by definition and so we had
this theme query submitted here that's not really an event we kind of put it there because we're like well it's part of
what the system does but it turns out that's not really an event um because an event is a state change and theme query
submitted yes maybe at some point there is maybe a record created somewhere or some piece of information created to to
handle the the query but from a business process St from a domain process standpoint um in a sense it doesn't exist uh
so um yeah so we had like theme query submitted and theme query refined but it turns out those those don't make any
sense uh so when we finally got down to um the track causes is that's when we when we basically pulled in uh this white
sticky which is about the UI um and then that's where it came in so one thing I I certainly realized is event storming
is great for the sort of internal processes uh but it's not going to help you sort of design the UI flow it's not meant
for that um and that's what I know I was I was certainly missing me too uh so sui mentioned so we're missing read models
in a process to backtrack yeah so the read models don't come in until later right so when you're doing the track causes
how did a song get added well you had a command add song well before even that you probably had something that was a
read model if here's all the songs we've got do you want to add one maybe or maybe it's just an empty form and there's
not much there it's not really much of a read model um but we did have have uh we did introduce for example for modify
song you got to find the existing one and so that requires a read model um so that there is there is a bit of of flavor
of uh sort of cqrs command query responsibility segregation that sort of re read is separate from writes so this sort of
sort of built into uh I think this this way of thinking but um doesn't mean you have to yeah so I notic in the chat
talking about the book so so there's obviously the the blue book Eric evans's book um that's a much deeper more
conceptual harder a bit harder to read and understand uh Vlog conos I think is a more lightweight um higher level less
less depth uh but probably better introduction to uh to demain driven design and it's a bit and it's obviously more
modern because it it was written recently as opposed to 20 years ago yeah I think the um that book is a little bit more
of a gateway drug book right once you get the light it's like okay now I want to dig deeper right right yeah eventually
You're Gonna Want to read the Blue Book yeah I think I think but that's me um so do you want to uh walk through what the
the track causes causes oh that's the name of this step three I'm sorry yeah that's name I'm like what is track causes
I'm like thinking like a song is like a track right some people refer to songs that's that's funny there's there's
there's a ubiquitous language problem what do we mean by track yeah oh actually let's look at the aitous language
perfect so I'm gonna zoom out and then move back over to here nope grabby so a big part of so before you get to that oh
sure fire away lexler asked a question um did you find Value in Caro's book since we' since we actually in the book club
at least some of us read both evans's book and Vernon Von's read book demain implementing demain driven design was this
was this one was this one useful um I'm curious what what your thoughts are um I didn't read the blue book but I did
read the um I missed the book club for the blue one I don't know how I did but I did um I found this there was
definitely some aha moments from this book I think it's because he writes in a simpler or less academic way so it sort
ort of like oh yes um there's a few things that I found confusing with this book um I keep calling it this book because
I'm blanking on the author's name in front of me what do I have the book conov conov yeah um but I think to me I think
that book has helped solidify things for me as far as so yeah it' be interesting to see what lexer did lexer say well
she she didn't uh uh join us for for the current book but she was there for for the other ones so okay I I clearly I've
I've read multiple times the demain driven the Blue Book uh and the red book um but I think it's you know it almost
wouldn't have mattered what book it was to a certain extent um going over this stuff over and over again you know
especially in a group and talking about it and bringing up sort of not edge cases but sort of where our in where our
knowledge gets fuzzy um because over time my knowledge of like what is an aggregate uh every time I talk about it or we
read something about it uh it becomes much more clear and even you know now that we're doing event sourcing in in our
Ensemble um it's even becoming more much more clear and so I think uh especially for these kinds of things you almost I
don't know it feels like you almost can't talk about it and discuss it too much because uh I found that that you know I'
m I'm still learning different aspects of it um and also since it's a more current book uh kind enough brings in some
things like event storming which I had done before I taken a training that where we did it and it did you know you do it
once and if you never do it again or you do it rarely it's not going to stick and so that's kind of the other thing is
is unless you're doing this on a frequent basis you you forget stuff um and so sort of talking about it again and
discussing it again uh especially the things that that I know I was less sure about such as what's a subdomain and how
does that relate to bounded contexts um there's there was some some clarity that that was there for me but but also I
love talking about this stuff so it matter all right um so sorry so now go ahead and uh uh let's let's look at our
ubiquitous language right you might want to zoom in a bit more yeah so for the folks who don't know what an ubiquitous
languages it's part of DDD and the idea is you have common language that business and Technical people use for the exact
same thing that you don't spend energy translating from the business world to the code World in other words it's
ubiquitous and whenever you find a term that has multiple meanings like track which actually isn't the case in in our
ubiquitous language because we don't even talk about tracks right we talk about s talk about songs yeah but um if you do
if you have two different definitions that might be a hint that you need to split into this thing called the bounded
context which we won't go into but um right or if you kept talking about track and I kept talking song and we meant the
same thing that would be a place where we'd say okay we're both using different terms for the same thing which would
which one do we want and course settle on it yeah exactly so these are the ones we uh came up with we grouped them by
actors nouns and verbs so the first actor is just anyone anybody can do anything um there's or anything any of the
actors below so a user is a is known to the site in other words they have a user profile they could be a um contributor
they could be an administrator uh they could be a member in other words somebody that doesn't contribute but so one of
the other ideas we talked about was uh it's a future functionality but if you decided to become a member of the website
maybe we could do things like generate playlists for you right put them into a spreadsheet or just put it in a plain
text file or I don't even know if Spotify has apis but can we create a Spotify playlist you know through apis so that's
you know some things we could do for people that sign up if you will right um again not to make money just to like make
give people functionality right um well maybe make money yeah and then uh don't be so quick to turn down money true true
um well it's more the bad taste from all the different but hey we wouldn't have advertising and popups and stuff like
that yeah that's true and like 10 popups hiding things um but one thing I want to point out for for all of these things
is is it was you know it looks like it's just there and it's just appears um the process was was by no means right that
straightforward uh in fact even now I'm I'm rethinking like I'm not crazy about i' I'm never crazy about user because it
feels like it's the lazy term um you know and and so some of this was you know can we can we refine the terms we played
around with some different terms so stuff was changing around and so this is uh especially during the the the discovery
analysis process you know when you're doing the event storming and you're using terminology um there's a lot of back and
forth and and things shifting uh and getting it written down is so important because um otherwise you'll fall back to
whatever you you were used uh so it's it still can change over time you can come up with um so the language here so one
thing I'm not sure Mike specified about about ubiquitous language is it is for modeling and what we're modeling is not
the entire organization you never do that we used to do that that doesn't work and so the one of the main things about
domain driven design is basically drawing a box around what we're talking about and that is the bounded context so the
bounded cont context is is literally saying within the context of what we're going to be working on we're going to
Define these terms maybe another part of the organization uses this word differently they use contributor in a
completely different way but inside this box right this is why you know they say you know models are are wrong because
they can't represent the world but they're useful because they can represent a portion and view of that world that you
care about um so Within this bound to context here uh these are the the the terms we're using and just to flush that out
a little bit more yeah so for example say there's two different parts of your organization right and so the bounded
context for say the um the HR department if you're doing software for the HR department is different than the bounded
context for the Department that's doing um shipping and product fulfillment right um and they might have words that are
the same but mean different things in each bounded context right or mean the same thing in both which is fine too um to
me one of the fundamental pieces of domain der design is the ubiquitous language uh so if you're doing ubiquitous
language you're already kind of doing stuff from uh from debain driven design um but I think defining language and
defining what things mean and defining that in a concrete way you know even if you do nothing else is going to be so
important so I was actually um there was a post on on LinkedIn talking about naming one of the things I find is is you
end up with really generic not great names in your code when you don't have a ubiquitous language that clearly defines
terms from the domain because then you're like well what do I call this thing I'll call it a you know a display manager
it's like no it's a song list right and and and you don't get good names unless you can get them from somewhere where
you should be getting them is from from the from the domain pre DDD one of the things that I used to do um whenever I
joined the team I would start making my own glossery of terms like immediately and then if they didn't have a a shared
glossery I would if the if the company the team had a Wiki I would immediately publish it the wiki go hey yeah can we
all like add to this or update it or like yo Rizzy that's wrong right yeah like oh good that's good let's talk about it
right and figure out what the differences are um that's very valuable and resolve them and resolve them yeah because uh
there's nothing worse than than uh than having to constantly translate what the business people are talking about to
what's in the code and vice versa um and this is and and it sometimes work and you got to get people on the same page
and you can as a developer you can reinforce it you can say do you mean contributor because they keep saying User it's
like no do you mean contributor or do you mean administrator like and doing that after a while unless the other person
is really obstinate and and uncaring about what you think in which case you've got other issues uh people will start to
synchronize and and and converge around the language if you you start noticing that you know new people joined whether
it's business or developers and the language has shifted you can explore right because language is living uh both human
languages and and domain languages they're they're living and they change over time um I mean I just remember like
because sometimes you may have two different things that hey these are both you know these are both visitor well now
they mean two different things we need to come up with a different word to to uh lexler mentions the the user yes there'
s there's a group of folks who think that oh it's it's like calling them drug users I never thought that either um but I
do think it's it's a bit it's a and I'm guilty of this myself um but it is a bit lazy to just call them users rather
than who are they what are they doing what is their goal uh like for example here we might not call them users we might
call them Searchers they're Searchers they're searching for Stuff um so uh if you have if you can't figure it out that's
to me that's an indication you haven't quite figured out what is their why are they here what are they doing what is
what is the problem they solve so that was a a a nice a nice part um should I explain caler uh I don't think we need to
go de deep into that um another day yeah if if and when we get to that we can we can talk about it yeah so we talk
enough about actors should we move over to a nouns yeah yeah okay and again some of these are still in Flight right it's
as we're figuring it out yeah um so there's a song There's a theme and we're thinking of themes as kind of like tags
right um metaphoric well I don't even metaphorically yeah I guess you could say that um future idea of having a playlist
which holds a list of songs the results of your search if you will um song database that holds the list of songs um
propose song I think we changed that to candidate I'll have to go look at our our um event storming we have proposed
songs a a submission AKA a contributed song you can see it's easy to come up with three different names for this just
off the top of my head um and then obviously we didn't settle on correction update or change yeah we might have we'll
have to go look at this the um the events and then there's the idea of an invitation inviting someone to contribute and
then the concept of a user profile they real or a pseudonym name and an email and that one's will'll need for basically
registering someone for the site and yeah uh so I'm just going to get this question out of the way even though it's a
little bit of a quite a bit of a tangent uh so dto normally converted to yes that's all I'll say nailed it we're we're
gonna so you know uh to to slightly longer answer one of the main things you want to be doing unless you are creating a
pure crud app where you may as well just generate a front end from the database which totally could work and might
totally be sufficient for what the what the needs are but if you're building an app that has a domain where you have to
talk to business people to figure out what these terms and things are and and most importantly so we see the verbs here
and I think this is where most people got object-oriented programming wrong I was listening to a presentation uh on DDD
and they were saying yeah you know an oh oh you're supposed to start with nouns and it's like that's not the way I
learned it um but regardless really what you want to start with is the verbs because the verbs are the behavior
everybody talks about behavior-driven development well what is behavior it's verbs search fetch change find assign right
all these things are are are verbs and and the whole idea of oo is to be this this idea of active doing things with with
behavior if you just talk about the things and not the beh Behavior you end up with anemic models that have no behavior
in them because oh I've got a song it's got some data I've got a playlist that's got some data I've got a profile it's
got some data but I don't care about the data as much as I care about what do I do with it what does it do what what
what can I do what is what is the behavior um so you want to have a domain uh model right and that's what this process
is is for it's helping you to build uh and take it to the next step which we'll see when we get to to the Aggregates is
what objects do we create and that builds our our domain model and you want to be very much unconcerned with how do I
store this in a database or how do I display it on a screen because they're important but they're not as important as as
the domain itself so that was the the longer answer to it to dto but that is what we're trying to right I mean it's
really interesting because throughout my career it's it's some of the hardest stuff that you do is figuring out how do
you build an object model um and I think some of this stuff especially combined with the stuff we'll look at uh gives
you a start so back to you on verbs um if there's anything else um I don't know I mean as a sui I'm not even sure how to
pronounce sui s like with an S sui okay likei um a lot of these verbs still have multiple words right like contribute
suggest submit um modify update correct right um clearly we need to settle on one and and again this is sort of an
intive process right as we were doing this work way over here where we're tracking the causes as we went from each step
one to two to three yes we were we were already starting to refine the names yes um and in some ways we probably a task
for us is to go back and go did we settle on names and update the UL right the ubiquitous language right so that would
be a an remaining task for us y but as far as going back here um so you know you can contribute a song you can modify a
song you can propose a change to a song administrator could approve um the song could be added it could be assigned a
role could be assigned to a user and you can invite someone so these are the verbs we came up with so far yep and like
any language it is living it's meaning it's which means it's changing it's changing yeah let's see we were on step three
right yes is there anything more we wanted to say about step three or go through more detail I think we can dive into to
detail of of one of the of one of the more interesting ones one of the more interesting ones you think this one because
it's got that pick a branching brch pick a branching one yes um zoom in more on that one yeah like really really get it
in there how's that perfect okay so here the actor is looking at a song proposal sorry the actor the administrator um um
is looking at the song proposal view UI sorry O's comment was like to live is to change yes yep because if it stops
changing it's dead very true yes welcome to philosophy 101 I almost stting to break out into that Monty Python song
about philosophers but I won't um so the administrator is looking at a song proposal vui un interface a UI um and that
is presenting the proposed songs and the administrator is now going to take commands for each song and say I accept this
song proposal or I reject it if it's accept then three events get admitted first is the song proposal is accepted event
then the song is added event and then a contributor is notified like hey we approved your song thank you congrats yeah
thank you um and then the other branch is no we're not gonna accept that song and so officially it's rejected event but
then there's also a notification to the contributor saying you know it we rejected it because while it seemed like it's
about um a hot summer it's it's really about you know hot steel coming out of the Ste Mill it's not really doesn't match
the theme of hot summer um that kind of thing and I and I want to point out like a lot of things in uh I think like and
I hesitate to use the word agile so use in extreme programming um like stories and like cards so on they are tokens and
stands inss for conversations and so this process is not just about let's put some stickies up and find out the events
it's it's in fact much more important like this artifact right what you end up with is useful but it's much more
important that you got people in the room to talk about this so like what you just said is like um you know when we
first put the events together I wasn't even thinking about well if we're rejected do we want to tell them why you know
and once we started going through Now tracking causes and linking it to an actor and saying oh here's what happens that'
s when you start discovering oh maybe we want to tell them why I think we can do that it's not like know sorry we
rejected and we're not going to tell you because whatever um we'll tell you uh and then I don't know if it was here or
at the next stage where we started thinking is there a counter proposal like well you propose this but I think actually
it should be this um and so you start discovering these things now you may you know you at some point you have to have a
stopping function because otherwise you could probably go on forever um um but this is what you want you want this
discussion to happen uh and to talk about it and to agreement of course I had to write down counter proposal before I
forget yeah uh so XPR asked what's the best way to learn about domain driven design um like anything do it do it so this
process is not hard in this sense that there's nothing technically Difficult about this part of the process and this is
the important part of domain driven design which is starting to figure out names of things and terminology um what are
what are the things that happen and then the next stage we start built getting into sort of the um code design level
things but pick a project that's of personal value and do it if you can do it with someone else even better um that's
that's ideal even if neither one of you have much experience you'll be able to to support each other um so the best way
to learn is is is to do read the book so you become familiar with it and then do stuff um we're about at the hour break
did you want to take a a quick a quick break sure that works for me okay uh so we'll take a a short break and when we
come back we'll look at um the last stage last step uh where we find the Aggregates uh and we'll talk about that and
then we'll start looking at what maybe what what slices we we'll start developing who knows so stay tuned um and we'll
be back uh how much time we five for uh so I'll wait for Mike to get back oh there he is perfect timing I was trying to
figure out how to get a u icon or image for when I stop the cam oh I realized I have to do is uh so normally I use OBS
and I've got all my screen set up for that um but we're using streamyard mainly because it's way easier to bring in a
guest uh uh but it doesn't but I haven't but I realized I didn't have sort of a a break screen because maybe they assume
you don't take breaks I don't know they assume you're you're robots um and suige mentioned uh oh add add the chat and
it's like yeah why doesn't streamyard support be putting the chat onto the screen so there are some um oh oh uh yes uh I
do have that link somewhere we're both scrambling to try and find it I have it I have the link I just want to make sure
it's it's actually working because they he he moved some stuff around to his news site um uh dig deep roots and there it
is so I'll pop it here and for some reason the link that I used to have didn't have a broken uh in case people are
curious is that's that I don't always do the individual steps but it's useful to to have this as oh does JB have the the
old link I'll have to go there and see I'll mention it to image which I kind of liked actually yes if you show my screen
yeah you can see it I like it because it doesn't come across as steps like the existing one right here it's more like a
flow um whereas the other one because I don't know it's just me because it's square boxes and they're numbered one two
three yeah because they they link to um although I do like his neuron naming uh nonsense which we started using in our
Ensemble which is like applesauce and pants I like pants pants is great because it's short right all right uh so let's
look at the the what I thought was one of the most interesting stages or steps uh yes look that's where pants came from
um uh is finding the Aggregates so um I think it'd be useful to show the previous steps for a second one in particular
or just um that's fine the one thing that uh I hadn't really thought about and was never pointed out to me when I took a
training on this um I won't mention who did the training training but it was really just not great uh commands generate
events and to me that's something I I we encounter an event source and we keep encountering in all these different
contexts I think it's one of the most powerful um ideas is that commands generate events although in reality it's
commands most likely generate events they may not always generate events or they may not generate the events you want um
so like you try to say withdraw from account right that's the command it might be you don't have enough money and so
account overdrawn or withdraw rejected something like that um hey it's Java grunt AKA Sean welcome uh and so this idea
of commands generate events um and then how this fits into the the next process to me was was just such a big aha moment
so go go ahead and jump to the next one okay unless you want me to just take over and talk but why don't you take it
over and talk okay all right so uh let me switch to I think you'll verbalize the AHA better so here we've got um let's
say propose song right so propose song you the command is obviously propose song um since it's a proposal it doesn't add
a song yet but but it does create something so there is State change uh the song proposal is submitted and what that led
to so the next step is you find the commands that generate events and you stick an aggregate in between so that
generates this so propose song and propose proposal submitted and admin notified of that and so this um stick an
aggregate in between commands and events is magical to me because it it it reinforces a couple of things one is well
who's doing that work where is that implemented okay it's implemented in this aggregate uh but more so it it re re um I'
m blank on word I want to use but basically uh sort of confirms this idea that Aggregates are about change to data and I
had sort of had this idea before but it didn't become as clear until we did this and then when we did event sourcing it
was like oh exactly if you're not modifying anything you don't need Aggregates Aggregates are all about transactional
boundaries and and sometimes when you talk about that at least for me it was like okay yes that makes sense but the idea
that they're the ones that process commands and generate events they are all about the state change and that's why you
have transactions if you're not modifying anything you don't need transactions um and so there's some things uh and this
just naturally led to all sorts of things like why you have the read write split in cqrs is you've got your Aggregates
which are one view of the data oriented towards changing things Behavior because what is behavior it's changing stuff U
behavior is the way you change stuff what the stuff got changed is is the outcome right so I propose a song that changes
some data creates this song proposal thing and as an outcome we have some events that are generated and um you may have
different views of the data like I might want to change certain aspects uh and so your Aggregates might be different but
this I this this step from the previous one to cool especially when we get down to uh the role chain stuff yeah do you
want to talk about that um no we could stick are we going to finish with this one or um I wasn't gonna say much more I
think it's it's fairly straightforward so this process was once we realized that we basically okay what's what what
other song proposal related things were there where we had something that affected a proposal on the left some command
that did that and something command on the right and this led us to I think we discovered we were missing some commands
right and so again this iteration that you were talking about is like oh we're missing something we got the propose did
we have the accept I don't remember if we had that uh yeah we have the accept and so we found that and this and
associated with that was the reject we basically grab these and and move them down to here and so one of the things
that's recommended I think we didn't quite do this and that'll come up later is don't name your aggregate first even
though it's really tempting to do so uh don't do that figure out what all the commands and events are uh and maybe even
figure out what all your commands and all your events and what your other Aggregates are and stuff you then we also have
the when the song is accepted there's the what is that called an external policy right yes so once the that arrow is
coming from accepted in the second row song proposal yeah it's kind of unclear because of yeah that be pulled down oh
even better yeah yeah um so when it's accepted so remember this is a song proposal aggregate not the song so then we
have this idea of an external policy that DDD has or sorry B storming has the idea of an external policy and that policy
is now going to add the song by creating a song object and then when it's added then the aggregate will emit a song
added event right and here it's really interesting because earlier we said all commands must be initiated by an actor
here the actor is a policy in a sense it's an automated actor and it's basically saying well when this event happens I
do I execute this command when a song proposal is accepted I execute ad song however ad song works whatever it does I
don't care that's not my problem my my sole purpose in life as added yes and eventual consistency yes and that's exactly
true there are two separate Aggregates there's a song and there's a song proposal we don't know when that song will be
added likely very quickly but still not in the same transaction Y and I wish it was I I I know for me eventual when I
was first learning it it sounded like such a long period of time but it all it means is not in the same now um and
there's also external service here so um is there a policy here maybe but but basically it's like when we have these
notifications they just go out through email and so that's a uh so we can start seeing that there's this service that to
and then when I think we didn't really settle on the next section song change proposal I think we did settle it's very
similar to song proposal it's got the same symmetry yes um but it's similar but different yes it's similar in that it
has and I think this is where we noticed that there was something missing um this one has propose which is basically a
create uh accept which is basically you know process it update it uh and then reject is is a different kind of update um
and song change proposal is the same thing you have a propose accept and reject and so these are you know and we're
thinking oh maybe there's there's some kind of Base behavior of proposals that get proposed accepted and and and
rejected um because they look very similar that events are similar and the automated policy is similar they eventually
talk to modify song but event but they're all doing something with song I think when we presented this at the book club
there was a question like why not just make song proposal do both change and I don't remember what what our answer was I
think it was the behavior is slightly different because they're talking to two different external commands yeah and I
think we don't know at least I don't know maybe they will be we find out as we're implementing maybe they'll inherit
some common behavior and and or or compose some Behavior I I don't know um and I think that that's something we we will
yeah um one thing we noticed here is is we we weren't too we weren't trying to be thorough but we were thinking about um
this idea of conflicting proposals uh which I think affects the change proposals much more than than the new song
proposals um you don't want to have two different contributors proposing changes to the same song sort of inlight um and
so there might be some prerequisite of before you you create before you propose the change you look to see if there's
huh a lot of the complexi is around this at least from the domain um what did we have what did we have first we had we
had uh we had role change um and then we were looking at sort of well what does role change do so was it yeah it was
Role change yeah yeah might have been something different I don't know um but it was it there's something similar about
this idea of of you create something and then you you sort of process it and so here oh no we had invite before that was
it that's right it was called invite yes so this is the danger of creating the name too early is we started with events
invite person contributor invited invite person to become admin admin invited accept invite and all the stuff around
invite oops which seem to lead us to oh then this aggregate thing is called an not uh and this this was this was one of
those other aha moments like we named it too soon because it seemed obvious that it was an invite but and what what was
it that made us switch to role change well we're seeing what does it do what happens as a result of these events
contributor invited admin invited uh and really that's about the invites so that's sort of separate but once we start to
link it to well what happens when they accept is the roles were assigned right and we're like oh but roles are like in
this user profile thing right because we had created user profile and and user profile created as our as our events we
originally had user roles yeah in user profile and so we had user roles in here because that makes sense you had a user
profile it has roles that's the way I did it that's the way you all do it right well then we had the problem of
transactional consistency the job of this invite was to change roles and that was the aha moment and we're like wait
that means we have to have these things and and we have to connect these events to uh a change over here well that's
that's why we had the aha moment because we were like we have to change both Aggregates at the same time and the whole
idea for not the whole idea but one of the important principles of DDD is an aggregate is transactional unto itself and
should never be dependent on other Aggregates transaction right and that's where we're like but but it they need each
other yeah and so I guess we could have built it that way yeah it would have violated DDD well it wouldn't have it
wouldn't have necessarily violated we could have done it where uh and and this at least was was sort of my thought
process is okay uh contributor role assigned as the event and then we'll have some policy that runs separately that will
go ahead and then update the user profile yeah eventually but that but when we were talking more about that it was like
but why like why do we want to have a separate object with with that and have that in a separate transaction and have to
figure out how to how to update that why not just put this the thing we're changing in the aggregate that we're using to
change stuff and so that's when we realize yes technically this thing we were calling an event but really its purpose
was to do a role change and so if we move R user roles into this object then we could do it all in one transaction and
we don't have any inventional consistency so we have very here yeah that was a huge aha moment yeah that that was huge
because one of the things we we started going through is then okay well what if the you know what if the user roles were
in this uh in this in this thing what is what is that mean in terms of other stuff like you know you're trying to do
something how do we know what role you are well we could easily read it right the aggregate does not have and this again
goes back to the aggregate doesn't have to be the thing that you read we you can have multiple views multiple read
models of the same data and so user roles is just we need to stick it in a in a read model which means that the user
profile could still have access to those user roles it just means you don't change them there or we just have a
completely readon object that is not an aggregate that's basically a value object that you just read uh and find out and
associate with whoever the logged in user and that and so this kind of discovery of your aggregate boundaries is one of
the things that um you can imagine happening quite often uh and that's why again don't name your Aggregates up front
pants one pants two pants three yeah just call it applesauce so swj ask is there a possibility the whole process could
be in a generic generic subdomain um yeah I mean I I kind of think authorization kinds of stuff is generally generic uh
and how you get people to change stuff is somewhat generic uh absolutely um would it be something we'd pull in from some
third party maybe uh probably not right away but it certainly could be considered a generic subdomain because it's not a
core part of the application right so for those of you who don't know what generic subdomain is it's like it's some part
of you need it but is it something that like differentiates you from everybody else it's like no we're not going to be
differentiated by how we invite people say I am running out of things to say regarding this board okay um that's good
that means we're oh we did have that purple sticky saying insure invite not expired yeah yeah so one of the things we're
trying to figure out is is sort of prerequisite so the aggregate's job is to change data but make sure that it's okay to
change the data so things like well if we had an if we sent out an invite and an accept came in was that invite still
valid did it not expire uh and we have a separate policy that that can handle that I think we had that up here yeah we
did so yep right here invites expire oh right yeah the little clock symbol y yep um and so there are things that that
are time based or or generally time based of some sort either timeouts or regular events or some period of time uh or
whatever thing uh SOI ask is discovery of non-core subdomain something that usually occasionally happens during EV I I
would think it's very common uh you're going to come up with all sorts of things that are required you're not initially
worried about um which which subdomain it is you probably won't dive too deeply into that depending on sort of how well
known the other like a supporting subdomain you're probably going to talk in some detail about um and if it's a generic
one you're just going to say yeah we're going to use you know this third party authorization service for that or we're
going to use this other service for for that here and we don't need to to know much more about it uh one thing we didn't
do here because we were sort of already kind of within a really abounded context is when you have a lot of these events
and you start separating them you start seeing the bounded contexts you start saying this stuff is about shipping this
stuff is is about uh uh billing billing the stuff is about our customers the stuff is about you know the warehouse in
terms of loading the warehouse versus shipping right there's actually two sides to the warehouse bring stuff in and ship
stuff out um and those are two separate grounded contexts uh so when you have a lot of those events and you know that's
when we're talking about you've got dozens if not hundreds of these things then you start dividing things into into
bounded contexts and then you can show you probably will see how these things then talk to each other how does shipping
know how to do it well the order system said the payment was okay so go ahead and and ship it how do we you know know
how to display the read model for this product to know if it's in stock while the warehouse said hey we just loaded a
pallet of these things and they're ready to sh and we have email service as an external service but I realized we didn't
really put in the concept of service right and so um in fact we still we'll probably use a third party authorization
service because I don't want to write one um but in terms of the role change invites I think that's more supporting
we're going to use a generic authorization but yeah exactly I just meant we didn't have a whatever sticky that is right
we didn't have a lavender sticky for it lavender yeah is that lav I don't know I'm not good with color names Java Grand
says spring authorization service like no I don't want to run my own server pay somebody authentication I I've promised
myself I will never handle usernames and passwords again as long as I live um I will happily farm that out to somebody
else um I think that's it yeah so what's next uh we figure out what we're gonna do first what time yes uh it's three so
we got half an hour left yeah um so as so I I just want to say like this process yes it's meant for more complex systems
but even this what seemed straightforward I won't use the word simple straightforward uh it was still like you know
complex enough um that that it was I think it was definitely worth it oh God not Facebook logins no sorry and I hate
magic links so we're not using magic links well that's up that's up to Mike he's the he's the product owner as it were
but yeah magic login links actually don't know what they are I probably used them but I don't know I'm sure you've used
them um basically you you you type your email address and you hit sign in and then it sends you an email with a link
that then logs you in and no password is needed and I dislike that because when I'm on mobile I'm it's switching apps
and then I end up not where I want to be uh because I'm in a different browser um on web on on but I'm glad you're
joking o about the Facebook logs in I will never use Facebook as long as I live um but I've been banned so that's
problem uh I just want to say Java Grand yes thank you yeah love love our community uh but before we want to do that do
we want to show the repository of our code or do we want to talk about how how we're going to approach the stories um we
can show the repository okay I mean just intell do you want me to share screen or do you want to do it uh go ahead and
your screen is not shared okay so did you want to look from the intellig perspective yeah yeah okay um right one second
so le le asked what did I do to get banned on Facebook honestly I don't know I just found one day I not that I was
accessing it much but I found one day I was I was just bned wouldn't let me log in wow I wish there was a great story
behind it but unfortunately there's not that's one of those things where they don't tell you anything and I could what
do y'all think 125 or 150 that's 125 I can't see the chat I'd probably say 150 we can always drop it down if if once we
get more into into coding okay I think that's where I left off 150 awesome ah I really need to assign a shortcut for
this one there we go there we go uh why don't why don't you open up the the source tree a bit more in the project all I
know it always expands all the other things I wish it had a button for like no no just expand expand what I like under
everything under SRC I actually have a shortcut for that that I assigned where if I'm on SRC I can basically just say
expand everything under here huh you would think that right click would have an expand from here you would think okay so
um like all good ex xers we created uh the project and deployed it so we have a basically a walking skeleton so um
nothing very complex here uh just a outof the-box spring boot 3.2 app with uh with good old test containers and
postgress and and all the goodies um but we fully deployed it uh with its own URL its own domain name yep grab that I
still have that up because we very much believe in continuous deployment so it's the URL name we were schematic and we'
re deploying it using uh how do you pronounce So Co coab is how I'm pronouncing it co I don't know what what what it
means um and I heard about this one uh actually on uh one of des's java gr streams um what's nice about it is uh it has
like a free sufficient enough free tier that we could get away with deploying this and probably even uh get some
functionality in there before we perhaps run out of resources although I think for this one we it might be good enough
um and they just they just uh by the way uh the Java 21 build pack is now available so we're all good yes Thomas uh
introduced us to that so um because they didn't have Java they were having some issues and so they didn't support the
Java 21 uh build pack set and so it's set up we basically do a commit and push when GitHub gets it it will deploy Co
will pick it up and and deploy it and so now that we have that now we can be confident um and we might want to do some
additional gates in in our continuous integration where we might want to build it on GitHub and if the test passed then
we move it on to the next step uh but we're going to be good good TD deers and not even commit unless the the tests pass
sorry not P we'll commit but we won't push so from an X I forget thises walking skeleton come from the XP world um that'
s what it feels like for me I don't know if it was explicitly that um I just put I I just feel it's since XP is all
about continues delivery I feel like walking skeleton if it's not officially part of it it's unofficially a part of it
so yeah so we've got code in GitHub that kab keeps an eye on when we push it builds then publishes to the website y
doesn't do much just says coming soon that's enough we right yeah and so this was you know one of the things this does
is it we you know it wasn't it took more than a few minutes to do because we had to you know hook up the domain we had
to register accounts we had to hook up the the repositor and all these things are are you kind of want to do in advance
when you have the simplest possible thing because then like if we couldn't give it some static HTML and that didn't work
then we got to figure that out but now we know right we can return a string and here's some HTML so we know that works
yeah do you want to talk about uh Gro better that's it maven's better declared maven's better um Gradle is in for me uh
has too much capability I want I want my tools to be useful but but but simple um I really like XML call me old uh but I
like XML because it tells you when it's wrong um and there are lots of tools and and and plugins that do do what I need
um yeah okay Boomer thank you my son says that all the time uh you know if if it ain't broke don't fix it um and with
with Gradle you're basically writing writing code even though it doesn't look like you're writing code you're writing
code and I like autocomplete I like knowing exactly what what's expected and with XML because there's a schema behind it
it can tell me what's missing and what what I need with Gradle if you're using groovy then you have no you have kind of
no idea what what what's possible um with cotlin it's better because it's now typed but now you are coupled to cotlin
which has its own issues um so cradle has its place uh but but I'm I'm a maven guy it's kind of the starting from the
simplest thing that'll work approach yeah yeah right which is another I mean some might say gladle is simpler but like
depends on what you mean by simp simple um XML looks more complicated because it's very verbose uh but come on verbosity
but I I find the support especially because even though the support for Gradle inside of something like intellig is much
better than it was it feels like it's always going to be better with Maven because it's easier for tools to process um
and so therefore since I live in intellig except for email hopefully they will never add email that's the ultimate goal
of any tool it adds email you know it's dead um uh I I live in it and and so I want possible um anything else we want to
say about the the project not much else to say here I think so chest I don't think of they're pretty yeah just the
default so I think um what we'll take the last 20 minutes or so uh is to figure out what's our next step sounds good
should we go over to our yeah one thing we didn't do is we didn't when we get to the end we didn't go back and say hey
are all these stories still valid oh yeah um and we do have some stories that are that are un untagged so we didn't even
evaluate them yet but those are probably more future yeah we probably should move these over to the Future stories
freezer uh I was working with with with someone they were using pivotal tracker and I'm like wow pivotal tracker that's
awesome I didn't think that thing was still around but apparently it is uh hey Danny Roose yes uh actually we're simoc
casting to both twitch and YouTube so once it's done the YouTube video will be right there um so that's basically the
advantage of using streamyard besides making easy for guests also makes it easy to assign cast and twitch changed this
so um what should we work on first good question I know the product owner should know this but uh well well I'm thinking
what's the simp yeah I mean definitely want to channel XP and what's the simplest next step right right is it searching
or adding so this is this is frequently the question that I encounter is do you basically work on viewing the stuff or
adding creating the stuff and I always look at it from what do I do when I'm writing when I'm doing tdd is is basically
how do I verify if I worked whereas if you start with the searching how you see it how you know it works is because you
can see it um so I'm always thinking about how do I know that it's doing what I need to do um and so I generally start
with with the viewing query side rather than than side and I presume we'll start with a visitor because that where we
don't need logins or any of that that would certainly be the easier place to start yes I'll give it two diamonds just to
say hey we're starting here I am convinced I'm trying to think there's anything else that I could counter that proposal
but I think that's pretty agree so we'd have to well I imagine want to do as much Under the Skin as we can right not
worry about what the UI looks like for this um so if we think about what would our acceptance be like what do what do we
want to see what what functionality as a visitor would we want to see and not wearing about how it's formatted or
anything like that right right um well assuming we have let's just say two songs each with their own tag which is
different that when we want to see a song for one of those tags we get that song back so we could start with something
even simpler great which is and this is sort of the the zer1 many idea what if they type in a theme that doesn't exist
what what happens that's good because it's really easy to display nothing yep right we couldn't find it but hey what
what that does is even though we're not creating anything what um what I'm hearing is we got to start with typing in and
posting some request and so that sounds like work and so if we can simplify the result um that that would that would get
us that first step and then we can say okay now the theme is found theme did you want to do it at under the skin layer
or actually from so I like to start um I don't think I want to write a an HTML based test but I would want to write an
MVC level test now there was a test um that is testing what URL are we hitting uh what what do we get back from that um
but we're not going to test like the contents of the HTML or anything like that we could add that on later uh but right
now would be more basically outside in right start at what's the edge The Edge is hitting a URL what is that URL going
to be I don't know um maybe it's the homepage and maybe it just says type your theme um and then what do we expect is we
expect some HTML basically 200 status uh and then the next step is okay okay we posted the form what's the contents of
the form it's the theme what do we expect back some page right so that way we get um how does the browser interact with
it and then we can dive in deeper with with the details of what does the form look like what does search results that um
and so EGS so if we don't the stuff we're searching for yes so generally when I start with queries I start with
hardcoded data and then later on um we can we will then have the behavioral commands that will allow us to add those and
then we will be able to write test for that because we will already have seen the hardcoded data and now we'll basically
want to see that we can it's going to reflect back the data that we added as opposed to the hardcoded data it is easy to
display nothing just display a blank screen that's fine so um not sure where you want to put this did you want to create
an issue for for this where we can sort of do the kind of given when then idea yeah let me grab thought I had it in my
fingertips oh it's right here I just didn't have monitor so we'll create issues for um yeah I mean there's so many
different places and ways we could do this um right but we're doing issues because mik want us mik wanted to tried it
out yeah yeah I mean I've done you know obviously many Trello and other kinds of right different uh lean approaches
pivotal tracker pivotal tracker um yeah I just wanted to see what it was like to to use issues within GitHub for
tracking maybe tracking is not the right word because but for noting yeah like sticky notes jir yeah no hard no oops
oops sorry I about to show this one yes yes you should run away yeah definitely run away you've been warned I've proudly
gotten at least two teams to dump jir and just do stickies on the wall if you're if you're collocated that yes Co I mean
this obviously when you're coated teams uh so sui asked about HDMX uh we have talked about that and where appropriate we
will likely use it yes yeah and that's in the road map it's in the road map okay it's in our heads we it's you know it's
one of those things like we're not gonna forget about that so there's no you know it's why why write it down if we're
never goingon to forget about it it it'll be clear when we need it or or want it so even writing it down is not
necessary that's the problem with your huge backlogs it's like of course we're do yeah okay so this is going to be I
brought up the wrong event storming what this one yeah actually a little bit freaking verbose any thoughts on making it
a little bit matter perfect so any thoughts on how to do labels with this um what are our options the existing ones I
mean technically it's an enhancement I I I tend not to use labels until I have enough where I can't keep um well you
wanted to do give and when then didn't you um up to you uh you might want to zoom in the browser to make it a little bit
more readable oh yeah reminders I must be tired I'm drawing a blank here um I think we can just say given an database
and again here I'm not sure what what our ubiquitous language is but or submits a theme search perhaps is more precise
what do we call it we actually call it a query yeah again here's our here's our uous language again what we call oh you
got it on your screen yeah uh so we got uh we're sharing my screen right now I think we're sharing your screen but I'll
look at the um I can it yeah so we basically just had search but had what about visitor want get sorry I shouldn't look
at comments um hey that's why we're streaming if you're not gonna look at comments what's the point yeah true easy can
get distracted by him though okay so I'm saying good enough um cool we got our first thing to do the comment yeah you
don't have to add a comment so this is where you can start having a little bit of a conversation either with yourself or
with other people got it I will have frequent conversations with myself oh don't forget X you're publicly admitting that
huh okay it's on it's on my repo not saying people can't find as long as I don't call myself names then I'm good yeah
there you go you stupid fit what were you oops story points yeah how many story points it's always one how many story
yeah always one you guys are just triggering all these rants that I'm holding back from bugs so I think um I think our
next step is we can start okay times like this we have too many windows open I'm just going to do it the go please
navigate uh whoops didn't mean to do that um yes I guess I'm Navigator all right so uh let's create a new test class um
we'll just put it in the main I guess we could do a little uh so not directory yeah uh so let's go ahead and you can
right click and create a new Java class yep test is it a theme search or a song search I think it's a song search okay
search it's interesting because you're searching by songs so if you read that would you think it meant you were
searching for themes or searching for songs versus song search theme test song search I think it's how about song test
even better because you know now you know probably a point point where we want to search we do have features for
searching by other things yes right yeah makes sense cool created all right um so let's start writing our first uh so
what we want to do we don't necessarily have to start from the outside um I'm not sure if we want to start from all the
way to the outside which would be at the controller level uh or if we saying I would tend to go for subcutaneous but I'm
open to other out subcutaneous is there much we would test I guess we'll find out if we do it so the only potential
problem for subcutaneous test first is you might not not have your method signatures set up caller that's the only like
because we may write the tests where it's like here's a string that's a theme or here's some other thing and might
actually require some other attributes good point on the flip side we could just say we'll figure it out and refactor
our way there so um let's start here see what that feels like uh so let's write a test let's create a new this you can
keep the throws exception in there it doesn't matter okay um but now you got two ATS yeah I know the one thing you can
do is you can use the alt insert to generate the test instead of the Post Live yep oh that was control into that was
control I went out and you can just say just hit enter for test 5 and it includes exception that's weird so it also put
in the public which is odd uh I wonder if it's using a different template let's not worry about that okay um so what
does this test do what did we say uh in our story exist is that what you said uh yeah um results sure the the search for
might be redundant based on the the class name but I think we're okay we we don't need yet um so I like to sort of
sketch out what are we going to assert so we're basically saying no results um so probably it's going to return some
kind of list of something is my guess uh so we're probably gonna assert that some list doesn't exist so um we against
Asser that list doesn't exist or assert that the list is empty sorry the list is empty okay yeah that the list has no
contents um so let's um let's create a class uh what are we going to call it we'll call Searcher and then let's go ahead
and uh new that up and may as well create it at this point unless the VAR works now the V will work all right it did
yeah nice sweet no well it did what we wanted to do now we can go and create it Alt Enter no uh should be Alt Enter oh I
didn't press Alt Enter that's why uh so yeah let's go ahead and create the class not in test not in test I wish why do
they always because you're in the test directory so do we want to do that even though that's not the way we end up doing
it that should be configurable yes I that would be nice um and so let's uh yep let's skip a line because we want to say
song Searcher uh and we'll just say theme and uh let's put in quote double quotes pick a pick a theme that we won't
applesauce all right let's go create that method uh uh oh undo that because one thing we we forgot to do was actually
assign the results assign it because I know where were we here yeah yeah uh so let's assign that let's say our
expectations is going to be that it's going to return uh a list of string for now VAR isn't gonna work because the
method doesn't exist so it doesn't know do and we can say songs and not sure why list isn't importing for you that's
weird it is the only option you might not have an automatically so there's a setting automatically import unambiguous uh
Imports on the Fly which is in settings so search for unambiguous y so check that it's occasionally annoying but most of
the time it's it does what you want pardon me I want to thanks where's the there's the okay button now create now create
yes because now it'll know what to the return type will be um we could probably change applesauce as go all right uh do
we want to split our pains now since we're going back and there's no split and move left um no there's not really yeah
that is so weird okay so then I'll do this one split right okay so um RS Paul asks a good question turning a list of
strings objects um this is a case of I don't know what a song object looks like uh uh and to for me we could guess what
that is but since we're returning what's going to be an empty list it really doesn't matter um and so we're doing
basically the simplest thing that we can get away with that starts getting us towards what we want uh if we introduced a
a song object here it would actually not help us much with what this test purposes which is give given a search theme
given a theme for a search we get no results um so anything more than than than a string to me is more work than than I
need to do so that's my thought behind that um and pretty much exactly what suiga says like start with Primitives until
you know what you need because it's going to be relatively easy to create a song object once we have a better idea of
what that looks like yeah well let the tdd process will lead us down that path yeah so even it's likely when we get to
the to the to even future tests we're probably just going to start with strings um and then we'll get to stories that
talk about well what is a song what do we want to display um and we'll have to figure that out but then we will um
figure it out once we know more about what the application is so this is a case of of generally can I defer this
decision when I will know more and this is a case where I think we can and like everything trade-offs is this um screen
res or the the zoom a bit too much for folks or is it okay yes so let us know in chat if uh if the the zoom font size
the font size is good um there is another option you could go top bottom um true uh where which is what I sometimes will
do on orientation got it yeah um and so suiga mentions even the theme itself that we search for might be a value object
uh but we don't know yet y I'm I'm very anti- commitment I I I don't like to commit I like to keep my options open what
is it it's make the decision at the last responsible moment at the last responsible moment yes everybody's everybody's
definition of responsible is different right right now it feels like we're not that responsible yeah um so I just wanted
uh time note we were scheduled to stop here um I am able to uh go for another 10 minutes or so I can um so if you're
okay then then that's our do folks that tune into your stream in general you know like block out the time and they're
like oh bummer you're going extra and I can't watch I guess they could watch the stream afterwards or the um the YouTube
recording it's more about the starting time and then yeah they can always if if it goes longer then they'll miss it um
and they can watch the recording yeah okay yeah sounds good I'm okay with 10 more minutes we're we're not we're not a TV
show where we have to end our show by by a certain time yeah commercials yeah unfortunately for for some folks yeah like
IGI is like it's already really late there so another 10 minutes isn't going to matter all right um we'd like to make
this test failed but we don't have an assertion so let's empty it helps if you type the as a method first so if you do
open close pren uh and pass in and now now the auto completes GNA be much better okay or the Auto Import sorry um like
that yeah uh so you'll need to now import right because if you don't type anything as a parameter it's going to try to
import other classes and we'll fix that up in some later time but now now we've got the right import got it um so now uh
let's put that dot on a new empty all right uh we can't run this yet because it doesn't compile so let's go and on the
bottom line six and a half null and uh for tests we haven't set up anything yet so let's just run this class and we'll
we'll do other stuff around unit tests later yeah run it and we expect it to fail because null is not allowed go boom y
expect it actual to not be no right all right um let's go return an empty list at at line seven list run the test and
run the tests uh yay uh let's do a commit since we've added stuff so unlike other situations we probably want to be a
little bit more uh careful about that also we can we can go we'll do it in a separate commit we can now go back to the
pom and change it to Java 21 but for now let's okay text for the commitment you um oh right since I'm navigating I'll do
that test for theme for search for theme cool yep commit but not commit and push right right I mean you could push but
it wouldn't do anything useful uh oh let's change a couple of things uh because it's going to run code and out so
there's the gear uh in the lower right corner of so where it says commit and commit push those two buttons oh here gotta
yeah click that gear uh uncheck the analyze code because we don't care optimize Imports um that's all fine just click
out of it there's no close button oh weird yeah it is weird it's like why is there a close button or done or save but
there isn't um all right let's figure out what our so that's our our zero case did you want to do the pom or oh we'll do
that uh oh yeah let's do that so we don't won't file and let's find it it's probably at the top for the Java version
that was a bad thing to check version uh just just scroll down it's not going to be very far there it is line 17 let's
change that to 21 uh dot version and let's do a commit um oh wait let's wait until everything reloads all right cool uh
commit yeah I'm a little I'm a little less pedantic about the the code analysis stuff I like my green check marks too
but uh it always annoys me when I'm not ready for for that level of green um okay so let's uh we can close the pom file
let's go back to the test top so let's see um was that our story what was our story and now I'm forgetting what our
story was oh give me a second where was it there hey we're done with the story woohoo well so we're done with the
subcutaneous version of of the story um so so we could either extend this story to say um one song Matches the theme uh
so basically sort of EX go breadth on the class um the the song Searcher class uh the other options to sort of go sort
of vertically and move outside and say well what is this going to look like from the web point of I guess depends what
we we were talking about stopping in five minutes so which one's more likely to be able to pull off in five minutes I'm
leaning towards the the width it's probably faster uh I actually kind of want to leave a breadcrumb for next time okay
cool so um so let's let's go and create a class uh for that represents our our controller so let's go write a um a new
test and that will be our um we'll just call it song themes MVC now okay yep and uh let three so 2 and a half uh it's
going to be at web MVC test so uppercase W because we're in Java that method I forget oops alt insert that's what test
method why does it keep asking for the framework um because uh an indirect dependency has J unit 4 which I believe is
test container's fault there's a way to exclude that we can we can fiddle with um so we'll we'll sort of back ourselves
out to the um to the get request so we'll start basically with the post request uh so we'll say um post to redirects to
result no that's that's actually fine we don't care what it redirects to all right and in here uh we're going to do oh
we need to uh Pull It in our Mach half and uh so mock MBC is a class that here yep and we want a variable for that no
just no no just space St this will be our field name just Mark NBC okay uh and and put a semic in there uh and put an
annotation above that so 8 and a autowired yep and stick in a space above 10 yep thank you all right uh so 16 MVC dot
post sorry. perform I forget post is the static method so perform uh post is a method so do Post open close pen
lowercase p it's going to be a statically import imported method uh inside the post we're string um so what's our URL is
it gonna be just SL search sure why not sure um so slash search actually let's do slash theme- search I know that might
be more than we needed here but why not uh and you'll need to import that post method it's a static uh import that we're
going to have to line uh we can say dot uh and expect and what we want want there is another statically imported method
that there uh and after the Clos print on status so after that PR dot these 300 redirection that one and then put a
semicolon at the end there's our test so this is basically saying when we do a post to this URL we expect it to redirect
us because it's going to redirect us to the page that has the results um if we run this or run it and we expect it to
fail um most likely with a 404 because that endpoint doesn't exist and that would be a perfect stopping point and a good
breadcrumb point perfect yes we got a 404 so somewhere in there is 404 yep yep got a we got a client error which is a
404 um instead of the redirection that we wanted excellent so test failed is right commit um I'm fine with committing a
failing test because we're not pushing we're not commit well you tell me what you want to endpoint love it perfect
excellent right so um how'd that feel that was good yeah people were quiet while we were comments um so our next
scheduled time is tomorrow at 9:00 am Pacific Time yep uh so join us for that for episode two uh as always hit us up on
the Discord if you have any questions um would very much appreciate sharing uh our our stream sharing the links uh would
be appreciated otherwise uh great thanks for joining us and uh we will see you tomorrow for for episode two our next one
after that is planned for Thursday and then after that we'll figure out what what's after that so have a good rest of
your your day or evening and we will see you next time bye
