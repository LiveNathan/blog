# ＂Song Themes＂ Episode 8： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=5jt0gQD-S6g

---

## Transcript

all right happy New Year folks welcome to another episode uh where Mike Rizzy and I are working on Mike's song things
Year so um we haven't worked on this since last year I know I had to I had to say funny so so uh last time uh we had
created this repository like thing uh and we got it to work where it um at least in memory stored all of the information
we were able to restore it from that end memory repository uh and we proved with our last test that it actually saved
additions to that inmemory thing uh and where we left off is there's still some feature Envy code smells that we'll
probably start taking care of um and then we can look at our list but I think we could possibly look at actually
persisting um or we can check out jir and see see what else we have or look at our stories I think actually persisting
good happy New Year to you happy New Year yeah good that vertical slice a little bit more vertical or a down so yeah so
what you've got on the screen that was um the last test we got uh one thing we could do is we could um sometimes it's
it's great to have a uh a break where we've got a failing test where we know exactly what to do next but we didn't do
that last time that's fine uh but we can also um so the way I kind of work is like when I'm trying to remind myself I'm
either looking at what's the last failing test I have or um if it's not really clear what the the next step is it's like
well what have we what have we done so far uh so why don't you bring up the the git history you can do that with alt
nine alt nine alt nine not alt F9 right I think it's alt n yeah there it is and you can rearrange it so that wider nope
hoping to make it full it doesn't have a takeover completely uh if you double click in the in that gray area that you're
in that will maximize that'll do it okay yeah and if you double click again it will back it yeah yeah yeah so um song
service load song startup we did the prepare refactoring it now persists uh and then we start to fix some feature envy
and so that's where we left off do some more of that good cool so an excellent question um oh how to detect codes smell
feature envy and and to fix it uh well to detect it we'll we'll take a look at it um and see what what about it tells us
that we've got feature Envy uh and then you'll see how we fix it um generally you fix it by putting it where it seems to
belong um but uh we'll we'll look at those steps and I guess when we find it we could explain what feature is yeah uh
Happy New Year CL or clich I'm not sure how you want to pronounce that uh so why don't we go to um the song service at
the bottom because that's actually where the feature Envy shows up so if we look at uh line 29 that's our feature Envy
there so what tells us that this is feature Envy the uh well the the immediate hint is you start seeing the dot dot
something dot something when you're not streams so in this case we're adding a song to The repository the repository
isn't adding it the song to itself yeah and I think what's confusing or what might not be completely obvious is what is
what does the get song repository do um so if you click on just the get song repository and then you hit um did you have
uh you can do um oh right the control uh is it control P I don't know hand I think it's control shift ey is what you're
saying um no control P it's contrl p contrl p yep Uh Oh no you're right I actually went to the other thing which right
yeah yeah that and so we can see this returns a list so the name is kind of awkward um but for those of you who watched
us create this this came from the fact that we we did what was called an extract delegate so originally we had the list
inside of the service and then we extracted it to its own class but in a sense all we did was put it in another class
but we didn't change any sort of encapsulation we didn't we didn't really we didn't really encapsulate it we didn't we
we certainly did not encapsulate it even though it's in its own class and um and is represented there uh actually why
don't we why don't we jump over to the song repository itself yeah and uh let's scroll all the way to the top yeah so
what we can see is we can see that the the song repository has a private field song repository uh which is our
collection class but because we've got both Getters and Setters it's it's not encapsulated so just because the field is
private doesn't mean that it's encapsulated which a great example is you can at call add on the return from line 16 and
change the object exactly without the object actually knowing it kept changed right that's feature Envy yeah and so uh
there is this thing called uh uh as don't tell or some some variation of that that always confuses me because I always
think of command methods as telling an object and asking as a query so to me that that phrase never made any sense to me
and I know it's a common phrase and some people understand it but it never it just never fits my brain um and so I
always I um basically don't modify Fields you don't own I just remembered a a um a phrase that's different than as don't
tell that maybe is more clear but is lightly um what is the word double on Tandra okay okay and that's like don't don't
let anyone touch your privates uhuh um so yes like don't let the outside world change whatever you have that's private
in your class right and and to me there's there's a whole um a whole area around how to how to do that and we're
actually gonna gonna gonna see that so one of the things that we'll want to do is um basically fix fix this we we'll
encapsulate it we'll we'll look at how uh and this is very much related to um primitive Obsession so primitive Obsession
I have a whole talk on that goes into this stuff deeply uh and I think it's one of my favorite talks because it it pulls
together this idea of encapsulation and uh meaningful domain terms and things like that so um I'll post I'll post a link
to that uh but here we took the step of pulling it out a separate class because we wanted this new class to be in charge
of the list and what we want to do is we want to now protect it and so one way we can look for feature Envy is say is is
pretty much look for is anybody calling this get method and then doing something other than just looking at the list are
they doing anything any kind of logic or any kind of modification with the result of that get song Repository and if you
hit control B we will see that yes indeed right there somebody is asking for it and then modifying it directly and that
completely violates encapsulation uh and the feature Envy aspect is that we do want to add a song to it but whose
responsibility is it to take that song and put it in the list that's in the wrong place and so what we'll do is we'll
we'll move it to the right that by that I mean that yeah yeah uh and so this is one of the most common refactorings that
I do is um extract I extract a method uh isolate as necessary and then use the move method ref factoring so let's do
that let's extract that line method we want the whole line so you can select the third expression no you were fine oh no
no oh I want you to do it the other way yeah yeah yeah from here yes so now you can just down arrow twice to select the
third expression because we want the whole thing oh okay that's why I say it's it's it's you almost never have to do any
kind of selections when you're doing refactorings as long as your cursor is in the right place as long as you're as long
as you're somewhere on the thing you want to refractor yes you don't have to be in you don't have to have it selected
sweet so now you can go ahead and henter um and now we have to think about what do we want this method to be called uh
probably just add we interesting it's doing a Boolean uh yes because the ad method on a collection returns a Boolean and
so we'll have to fix uh fix the return value because it shouldn't return anything okay add it is what have so if you if
you uh you want to either hit Escape or you or you want to hit uh I don't think tab will do it I think you want to hit
Escape because right now it's autocompleting the options and if you hit enter it selects the first one right let me try
both I'm gonna try tab first nope tab I I didn't so tab is yeah add Escape yeah and now you got now enter right yeah so
the Expressions list shows up if you don't if you don't select anything and you're in some kind of thing that could be
extracted um then intellig will say which part of this do you want to extract because maybe you just wanted to extract
the variable or maybe you wanted to extract the variable and get some repository or maybe want to extract the whole
thing like we did um you can sort of like uh you could select everything you want and just do extract method and then it
will do the do whatever you selected right um but I find it it's fewer steps um to just say extract method and then
select uh rather than select and then extract method um and this is for sort of single line Expressions when you have
multiple lines then you obviously have to select what you're gonna extract because it's not gonna no or it's not gonna
consider multiple lines right it it won't consider multiple lines yeah exactly that makes sense um and it's pretty
common uh it used to be sort of a habit to select first and then run whatever refactoring but over the years I've been
training myself to to not select it all and just let intellig offer that because it's not just extract method that it
applies to it applies to a whole bunch of other refactorings um let's fix the Boolean we don't want Boolean we just want
a void just do a manual yeah um although actually it offered I wonder uh since it's offering on the ad what's that make
meth void that's what we want because then it'll drop the return value yep perfect cool all right so that was step one
is you extract the be the behavior that you basically want to encapsulate which is adding the song to The repository um
what I do next uh even though it's not absolutely it's not necessary uh but I find it makes the following step easier is
to take song repository here in this method and push parameter so not that just the song repository oh sorry yeah go
back to um repository as the name for the parameter yeah I mean it's not going to matter but sure yeah all right and so
now uh we can do this and we're going to move it to song repository the first one and so here's why uh this dialogue can
be confusing is there are a bunch of different options and this is basically saying where do you want this Behavior to
go well we don't want it to go to song because that makes no sense um or makes little sense for a song to add itself to
a repository that's not where the behavior belongs and one of the nice things about notice that we sort of followed the
trail from the get method we said who's calling this get method and doing something that they shouldn't do so we
basically followed it from there so that's where we want to push that behavior so so we came from song repository that's
where we're going to push the behavior um and then it's a question of well which song repository because there are two
choices here uh and we want the one um that is the parameter and uh that's why I push out the parameter to make this
step uh more clear so let's go ahead and refactor that and so now we can see on line 29 we no longer have uh any kind of
feature Envy Bally saying Hey song repository add the song I don't even know how you're tracking stuff do whatever do do
did we eliminate um oh to hold on yep go ahead so we're still in the repository we still have this yes we'll we'll come
back to that um so our overall goal uh a a high level goal in song repository is for us to eliminate uh as many of the
usages of get certainly any usages that are doing modifications to get to the getter uh let's go back to song repository
so our goal is to to get rid of as many usages of the get song repository um and definitely 100% eliminate usages of the
setter of the set s repository but we're focused on the getter so we'll we'll just sort of continue around that um that
that cycle and so if we look at the uh the the ad song that got moved there at the bottom uh we can see it's still
calling the getter but eventually the idea is to we'll we'll get rid of that that getter um we may not be able to get
rid of 100% uh we'll have to we'll have to see about that so let's look at the other usages of of get song repository uh
so besides the test uh which will be an interesting thing what else is using that so let's um this isn't a feature Envy
problem this is a bit of still not quite encapsulated but that's not to me the the the real code smell here the real
code smell is is a bit around um kind of feels a bit La Dem meter like but the idea of why are we this may be totally
valid that we want to create the song Searcher and just give it a list of song um but I think the idea is for for the
service not to be the intermediary here and basically to uh uh have the stong Searcher well actually now I'm not sure so
um so what I was thinking is we we would just pass in song repository but actually song Searchers in our domain which
means song Searchers should not have references to uh any kind of repository so this is actually fine is it the problem
that we've name that name of that method is get song repository yeah so that was that was something that was confusing
earlier so why don't we why don't we fix that since it's confusing us now it was really returning that um let's call it
all songs because is question on that should we really be turning the list or should we return a copy of the list yes so
for now we'll return the list um but there's a once we finish up a couple of steps we will want to return something else
uh that is not list so uh F asks don't see the value of fixing the feature Envy so if we go to the um the song service
class uh and we go down to where we did the ad so now line 29 means we don't know what the implementation of the song
repository is we don't need to before we did we asked the repository give me a list of songs and I'm going to add it so
there are two problems with that one is you have too much detail about the song repository and how it worked the other
is very much related to that which is is uh the song repository itself can't change because it doesn't know who's using
it in this in this way that's sort of bypassing any any knowledge that the song repository has right so when you would
talk about encapsulation it means that it is protecting its data and so if anybody can just stuff something in without
the object itself knowing it is it is not encapsulated and I think of of all of object-oriented program I mean the most
important thing by far is encapsulation inheritance who cares about reusability I don't care encapsulation is is the
main thing that I think about because that's what protects you from be changing an implementation somewhere and having
stuff break because some other object was doing something sort of through the back door a lot of I've seen a lot of bugs
over the years caused by somebody else outside the object you know playing around with private variables right and it's
like how did that change there's no method here changing it it's because it wasn't truly uh encapsulated which was sort
of where we were before we stop we were talking about this does break encapsulation at the moment because it's returning
a reference to this yes and people could muck with it and we're gonna fix that appropriate time but hopefully that helps
an yeah and so again the two factors of encapsulation is provide the behaviors that you want to allow callers to perform
so what are the intentions that we have we want hey song repository you're keeping what is your job your job is not hold
on to a list of songs your job is hold on to songs I don't know how you hold on to it I don't care how you keep track of
it I don't care if you write it out to files I don't care if you you you store it in a database I don't care if you keep
it in in memory in a in a sense all those are are are implementation details so encapsulation helps us hide those
implementation details so we can focus on what is the abstraction what is it supposed to do um and by providing these
very precise ways of how you change the repository right this is where command methods come in command methods say this
is the only way you change the state of this object and ideally there methods that make sense from a a a domain or or or
technical standpoint of what do we want this thing to do and again separating what we want to do the implementation uh
yes we're we're about yeah um so let's go ahead and uh go into song service and let's yeah let's rename our internal
list one second sorry I was just my streamyard just got in the way of something there we go okay so you were saying uh
so let's go to the top of song repository and let's rename that list actually to be songs uh we're not going to name
anything yeah because we're gonna yeah we're gonna get rid of of the setter and we're gonna fix the getter yeah although
it's not a getter anymore well actually still is a getter at the moment yeah yeah uh so let's let's go fix the getter
and make it not a getter um so when I when I think of encapsulation and I think of on uh objects like this they're
there're two types of methods there commands saying change something and there are query methods that say give me
information if we're going to give information there are a couple of uh her istics that I have for doing so one is um
almost never there in fact I can't think of when there's any good case to return a reference to a variable directly uh
though if it's a primitive then there's no harm because Primitives are are in a sense uh unmodifiable from the outside
so we always want to return what's basically an unmodifiable view variable I'm just summarizing some of your St uh and
so what we want to do is so here we have a a couple of choices for our all songs method because we certainly do not want
to return songs if songs were just a string it would be fine because it's a string and and the caller can't modify it
right so what we're protecting against is somebody from the outside changing our songs without going through the proper
protocol right so I always think about objects have protocols how do you interact with them how do you talk to them um
and if you change stuff behind the scenes you're not you're not following protocol and that always ends up bad so um we
could just return a copy of and so of I'm going to go back to my old um yep so that's one way to do it um that's an sort
of a necessary addition so now this object is protected against sort of out of band sideband through the back door
whatever you want to call call it basically changing the data without going through the command methods if you want to
change the songs you're supposed to go through the front door follow protocol you don't modify things directly there's a
problem though with with this method which is the return value and the return type um which a caller may see as as so
yes defensive coding is what I would consider a a a a part of what we're talking about um it's not but there's more than
just being defensive about it um defensive is is in a sense saying I'm G to write this code to make sure nobody can make
a mistake but I see it as as a bigger issue I'm not just trying to prevent people from making a mistake that's just
inappropriate and I want to make sure people follow the rules and so to me that that's a bigger issue um because there
are multiple different ways we could we could deal with this making a copy uh what sometimes called the defensive copy
uh is one way we can solve the problem but the other way we can solve the problem um is we can decide we're going to
return a different object so right now somebody calling all songs looks at the return value says oh this must be all the
songs in the repository I can go get this and change it and if they try to do that that's going to be bad because it's
actually not going to repository yes so there are there are I always think of sort of this um ladder of sort of ladder
of abstraction and I'm stealing that term from something completely different but but we can say all right let's return
a list of song that's bad because it's was a direct reference so let's return a copy but it's still a list of song
there's not much of an abstraction there that might be fine that might be as the best we can do um but I'm very
uncomfortable with that because of the way it misleads the caller so we can then move to well how about we return
something that makes information so Java offers a couple of stream and what's nice about a stream is it makes it clear
to the caller at least folks who understand what streams are all about um that you're getting a read only unmodifiable
in a sense view of what repository but that doesn't raise the level of abstraction very much so it makes it a bit more
clear what what you can expect um but it doesn't raise the level of abstraction on the other hand you might want an
object that represents all the songs in the repository and so you might create a songs class except that would pretty
much be a duplication of what song repository already does and so this is where does would a new class provide uh
anything that anything besides sort of another nice name um than than sort of a stream of song and then we'd be looking
at well okay so songs would have still inside of it a list of songs what else might it do well no that's you you would
add to it it's like well wait we already have such a thing um so you have to be careful of of uh if you already have a
good abstraction and song repository I think is already in a sense the abstraction of keeping track of songs then um
then we then we don't need anything else uh the other thing is we may not want to return songs maybe callers don't care
about every single detail that the song object has and so then we could return we could perhaps return uh a uh a song
You Know song you know songs view or just songs that is just their you know song titles or some subset of information um
that might be useful as well and that depends on sort of what callers are going to do with it uh but I think the
approach that we probably want to take here is not return a list because that's misleading um but stream so we'd want to
look at who the callers are and say what what's that going to do for us if we if we do that internal so let's go to the
internal um because let's fix that so here we're we're now inside this thing right we pulled this code in from elsewhere
but now we're inside so let's go ahead and and inline method uh and yeah so already because we did that um we've got a
problem so let's uh let's fix let's fix it so this method is allowed to directly access songs right should I just
manually fix it or pulled the comments down too but I can yeah delete the comments and just you could even undo and just
replace it songs you mean literally just yeah because usually I do the the the in in um the inlining before I do the the
protection stuff and that's why I was a little taken aback but what happened I was like what happened it took me a
second um so but this is this is what we want right so ad internally can access the collection because it's inside the
the class um but does its job and one way to think about this is oh this is great so if I ever want to change how my
songs are stored internally um no caller will have to change that's the way you want to think about it right again sort
of separating implementation and that's what proper encapsulation does is allow you to refactor your internals at will
without worrying about breaking breaking other stuff all right let's look at the other colors to uh that all songs
method okay actually can we move up the Constructor since it's here sure yeah doing down there so all songs um test yeah
so let's look at the test actually sorry I jumped ahead song Service uh but let's look at the test first that's first
okay so uh if we if we changed all songs to return a stream instead of a list a sech a will handle that fine so we won't
have to worry about that um speaking of tests we haven't run our test halfway I did it once at the beginning yeah but we
haven't done it since we were factored so let's run them again yeah and you want to do all um yeah let's do all just Alt
okay we all passed all right great um so let's now look at that other use the the last usage that we have to worry
service so now we'd have to look at um create song Searcher what uh what does parameter you want the um internal jump to
it no um now it happens to convert it to an array anyway uh so that would be a relatively straightforward refactoring to
to convert uh a stream to an array um so I think we're we're at the point where we could uh just just return a stream
and then we'll manually fix up uh okay do we do it by modifying the return and have it drive the or is it all manual um
we can actually start it by in on 21 instead of returning a list copy of do uh return songs. stream and then that'll
Force us to change the return do so third option one two three ah there it is it cool so I'm just copying a link for
something okay um so now we should have error and I expect it to be that method that we just saw in song Searcher
where's the uh I so I would I basically to to force a compile I basically just run uh tests yeah I did control shift
again I really got to get the alt on that one there okay so here this is where we expected it to have problems right so
now what we can do is um we can go into method uh the one that takes a list um and we can change its type from a list of
song to a stream of song would you do it through um just do it manually We're not gonna say Not Gonna Save anything by
doing a chain signature gotcha we could have done a a quick fix from the from the caller but we're here anyway so okay
I'm sorry some bu he trying to get what was that again I'm changing uh we're changing it to a okay yep and amazingly
enough stream has a two array method on it which I I wasn't sure I wasn't sure if it had it I wasn't sure if we were
gonna have to sort of switch it around and call arrays. two stream but apparently stream has to array as well which is
great um and so anything that was the io free test should we run all no I think that's that's sufficient so um and by
the way uh I talk a lot about this process of of what we just did in in a talk and I posted a link um to to a talk I did
on on uh primitive Obsession because to me that encapsulates a lot of this stuff about know pun pun intended I guess
encapsulation um and talks about sort of what are primitive Obsession and feature Envy how they relate to each other so
it's a one of my favorite talks um so go one uh does it have to take an array that's where we started uh we start with
VAR orgs um so VAR orgs are arrays uh and so that's just been convenient um if at some point we decide we don't want
that the primary way of creating the song Searcher we'll we'll change it um but right now I don't see I don't see a need
for that uh because I'm still unclear about what um sort of how do we want to initialize stream a strong Searcher in the
future I I I can't predict that yeah yet well we could but it' probably be wildly wrong yeah I was I I I was kind of
saying like I can't predict in the way that that that makes sense I just don't yeah yeah definitely it's it's one of
those things where um it I I I would love it if if either arrays were were hidden completely and so we just never
interact with them anymore uh that would be nice or at least if the VAR ARG somehow was made to support lists and
collections since we now have sequential collections it would be nice if if they could just use that but um arrays are
very very deep deeply implemented in the Java a virtual machine so I don't expect too much from stuff the the main
benefit for for varar is it makes is it makes it easier on the caller um but there are ways to sort of simulate that
which are just annoying so uh for example all the list. of so all the static collection creation methods um um basically
use variants of of of vogs and it's just it's just the way it is all right um let's do a commit we haven't done a commit
in a while we refactor ah so I think we've done a couple of things sure do we It's all under the rubric of continuing to
feature Envy or no um but I'd like to be a little bit more specific yeah yeah so let's just take it out entirely okay um
so we we fixed feature um fixed uh basically encapsulation yeah uh we fixed encapsulation of getting the songs from the
song from good all right uh so we can continue looking for feature eny so if we go to song repository and we've taken
care of all songs so that no longer suffer uh either suffers from or contributes to um uh feature Envy um now we can
look at the set song repository method because that's certainly so of all the the methods that I think are evil Setters
are the most evil um because you're basically at least the way they're generally implemented is you're basically saying
here's your your field I want you to set your field to this information and it allows you basically do whatever and it
treats it it very much leads to anemic data models that have just data and no Behavior because if you're just going to
else and so uh do to use the magic word uh inject you never want Setter injection you never want field injection you
never want to basically in a sense force your in a sense force your way on on this object you don't want to force
information into an object an object it's not encapsulated if you can push information in and the object can't reject it
if the object can't say no that's not valid uh then why have an object at all variables and that's fine if you're
programming in in something other than object-oriented programing but if you're doing object-oriented programming uh the
whole point is encapsulation is to protect the Integrity to allow the object to protect its own Integrity yeah even for
testing purposes that's sometimes you have to provide a Setter uh but to me that's really a Resort often doing that on
my way to repairing what's probably an underlying larger design problem um because again like being able to arbitrarily
set something uh it's one thing to put in a Constructor where you can't create the thing without it and you can't change
it once it's created uh but once it's created the object needs to protect itself and if it can't protect itself even
from tests um because who's going to say that it's only going to be called from tests uh then then you're just in a in a
in a world of trouble yeah the chances of somebody going oh look there's a set method here I can use it yeah not knowing
that it was only for tests yeah and again that to me that's very separate from from creation right so we have a bunch of
create methods maybe those create methods some of them are are meant for tests but then at least you've created
something you haven't modified something that was created through sort of a normal process a typical process so I think
that's much safer all right uh so who's calling this Center just us oh just us great then we can can uh we can fix that
in line well you can't inline it because uh if we if we look at at line 16 and 17 um what we really see is in fact what
was talking about it's like we have a Setter here only because we didn't have list so that mean to make a Constructor to
take so we need to make uh a list do we have any other Constructors or is that just the one the default this default one
okay um I don't know manually do it or I don't know that I don't know that there's any uh refactoring that will will get
us there any faster than just just um so what I would do is uh still do some manual work but I wouldn't I generally so
one one thing I've noticed about myself is I almost rarely write a method by hand I don't write methods or Constructors
by hand I always tell and tell J here's what I want you go write it so here's where I would go to line 16 and stick in
song list as a parameter and the reason why is that way again it's this idea of what does it look like from from the
caller what's convenient for the caller what does the caller want because I don't care about what the implementation is
I care about who's calling it and what do they want and now that we've got red now we can go ahead and tell intell J
please create that Constructor um and in fact we could then think about do we want a default Constructor actually is
anybody calling the def maybe we're only calling it here so if we're only calling it here I might say let's let's just
uh let's just add parameter yeah so add first parameter yeah let's do that um now we'll have to go man ually uh fix line
11 but if you do an Alt Enter on the the gray song list it should offer assign to uh ah because the parameter was
different so uh we'll have to do it we'll actually have to write code uh the other options we could change the variable
name to songs and us let's see what happens uh assign parameter yeah that worked so the third one there we go now we
don't need this and now we don't need that correct now I I I uh what were you thinking uh no go ahead delete line 18
let's run our tests what happened oh they passed oh okay sorry Miss sorry uh I was looking at at comments uh yeah now we
can go and probably what are you thinking I was thinking we could inline 16 but no let's leave it I'm not I'm not too
upset about that um the other thing we can do though is now on line nine we can actually make songs final so you can do
an Alt Enter on commit uh we have setter Setter so uh so OA says for some reason people resist moving Getters and
Setters and making the field public yeah like uh and and and and I I personally go back and forth about this there are
times when that's appropriate um such as such as dto that uh that the to attitude mentioned um and there they literally
are just data structures um where even a record is kind of annoying because records are are immutable uh and so if you
want something that's like a read and write thing but it's just data and it's just used for request response to the
outside world why not just make the the the fields public and be done with it and like not have boilerplate code that
you have to update or use a terrible tool like Lumbo and and things like that um the only downside is that it's often
unexpected and so there's there this is why I struggle with it because as as an educator and coach and so on um I want
to provide sort of good examples but also how far do you drift from what's fairly commonplace is is sort of the the
issue because you know whenever you're you're explaining something or teaching something you have to connect with what
people already know and if if people react badly to it um it may interfere with their learning if they say no that's not
the way we do it or just that looks weird um that might interfere with their learning uh and so I generally still create
objects with Getters and Setters even when it's not really required um the other issues is if you're working with a
framework or a library that expect Setters and Getters um that's where you absolutely need them because they're using
the underlying good old Java Bean specification from 1997 where Setters and Getters Define what the properties are uh
and so that's another reason why I tend to still default back to using Getters and Setters for those objects um and I
think it's I have opinions about C I feel like a lot of times they do things that learn the wrong lesson um and so one
of the things that c does is make it very it makes it trivial to Critters and Setters which is great for your dto but
terrible for your domain objects um yeah I don't know do you make it easy to do things when it or only maybe like one
half or one quarter or one tenth of sure so uh so this is an interesting statement um I don't think dto are overused I
think they're used incorrectly and I know it's a subtle difference um but if you need a dto use a dto but if you really
need Behavior then you shouldn't be using a dto um so there's a subtle Nuance here where it's like you can have a lot of
dto and that's totally fine if they are explicitly used as data transfer objects um if you just say every object is a
data transfer object then you have behavior it's in a god class somewhere yeah or it's in some big God class or it's or
it's or you've taken the approach of I am going to write my code in a much more functional style where I'm G to have
just data uh objects and all my behavior is going to be in uh functional state-free uh methods and you can totally do
that you can totally write that code in a language like Java you're going to it's going to be really awkward um but you
can totally do it um but I'd question like why are you doing Java in that case uh C seems to have make that easier um
and I know folks very talented folks who do that I just that's not me I'm a big encapsulated object-oriented kind of guy
because you're basically saying I'm not going to encapsulate my data I'm not going to combine my data with my behavior
and it's a different style so um so I would actually phrase this as there are too many anemic objects uh too many anemic
domain models so where I never want to see a dto is in my domain model because if it's truly just data then I Then I
then it should be a value object and not not a dto um which sometimes looks the same but it's it's a it is very a very
different role that if there is behavior it's inside the value object otherwise there is no Behavior so if you've got
behavior in one place and data in another then you're not oh and I and I feel like I've I've been ranting about this a
little bit here but I it's to me it's just so important not not to like if you're going to program an object oriented
language then encapsulation is your number one uh is goal hey tkes Happy New Year so um this is an interesting point uh
can you bring up in song method so we could so in fact list. of or list. copy of actually both end up returning what's
basically an unmodifiable list that creates special lists under the covers that don't use array list that they're
unmodifiable you try to operate on them and those are if you try add to them or modify them they will those methods will
fail which is actually an additional problem because if you get a list and you didn't know was unmodifiable and you try
to modify it and it blows up well I hope you were test driving that so you found that out early but if you didn't find
that out until much later then you you you you've got a problem um and so by returning a stream we're explicitly telling
the caller that they should have no expectations of being able to modify the stuff they get streams are are by
definition read only in fact they're read once once you've finished the stream you it's gone you've you've you've read
it and I hope you got what you needed from it because you can't reset the stream now you could immediately take that
stream and convert it to a list but hey that's on you you know what you're doing um hopefully you that uh what's it
runtime creation of uh well you could use collections unmodifiable but there's no reason to do that because you just use
list. copy of um you either way I think what they're saying is that in both situations you're not GNA find out till
runtime correct yes yeah because they all Implement list and this is this is actually a very deep problem in the Java
Collections classes is that there's no there's this unmodifiable thing but it is not elevated to the abstraction of
readon list or immutable list there is no such thing in Java uh standard collections there is stuff in the immutables
library in guava library in the eclipse collections Library where there's not just implementations that are uh immutable
but they are present at the the interface and so you know what to expect um and if we wanted to say hey we're going to
be using a lot of different collections where it'd be useful to have immutable collections then I'd say okay then great
let's bring in Eclipse Collections and from here instead of returning a stream we would return an immutable list again
that would that would be fine because that makes it clear to the caller that the caller should have no expectations that
um thing yeah this is this is why it's bad is because you won't know what runtime until it throws an uh unsupported
operation exception which is really just bad um and it's it shows that there is missing abstractions uh but that you
know as they say that horse is is way out out there long gone in fact the horse is the horse is dead it's so far gone um
but if from an noo perspective if an inheritor removes a parent method that's breaking that's just bad for all sorts of
reasons yes yeah that's like yeah there no longer um you're lying and and what's interesting is there is a uh a pattern
the state pattern that actually kind of requires you to do that which is why I never really like the state pattern at
least in Java because you're basically saying you're in a state where this transition that you want to do right so for
example um the good old gumball machine example right turn turn knob well you can't do that because you haven't inserted
any money so you can't do it so what do I do I throw an exception when you're in the money inserted State then you can
turn the knob and it's fine um but I don't like that because it basically so it's a surprise we won't know until run
time that that you can't yeah um so this is a good opportunity break so uh how long a break do you want five which all
right we'll do a five five minute uh break and then when we come back um time to look at at our next step which might be
persistent so stay tuned for that woohoo um so I think our uh do want to take one more look at our uh song there so we
got our songs it's final we've got a Constructor that helps us initialize it um we have a way of getting all the songs
we can add a song uh do you like static um Factory methods to be after the Constructor or before yeah I like them to be
um after the Constructor before the others an on yeah cool um I'm just thinking if we want that Constructor be private
no let's leave it let's actually it's the only usage yeah let's make it private for now we can always make it public
later I want to see well let me it's a lot of steps to just I could have just typed it yeah sometimes it's just like you
know what just modify it yeah um a slightly faster way would have been to click on the the visibility on on the public
do you're fine just uh oh no no no it's undoing too much you undid just what you final that's weird it didn't actually
redo it I know that is weird is it did I just okay one more time there we go there we go so you were saying quick here
yeah so Alt Enter for that yep oh so it's got the yeah yeah that's a little bit faster but yeah I probably could have
just typed like sort of diminish returns yeah um so why to go the other way and get rid of the stack static Factory
method I I kind of like static Factory methods um over Constructors because it's uh they are they they tend to
proliferate and and therefore I want like to me it's just an unnamed Constructor uh and we'll we'll likely be be adding
more uh varieties of these especially once we get into um uh sort of fakes and and things like that so I tend to to
prefer Constructors um so kich or kleich not sure how uh to pronounce that quite but um brings up a point which is which
is the tragic State of Affairs in most code bases that I've seen as well is uh really poor encapsulation both at the
class level and at the quote layered level in that they may look like they have layering but there's not sufficient
boundaries around that and to me it's all about boundaries right capsulation is a boundary around the class um packages
or boundaries around those that that layer or that part of the layer um and if you're not going to respect the
boundaries uh you're going to have a hard time um and it's it's it's pretty terrible because mostly it makes it really
hard to you uh how would you test stattic method um same way you test any other method not sure what what challenge you'
re or issue you're thinking of that makes that not obvious I just wanted to EMP go ahead I say I want to emphasize one
of the big advantages of having static creation methods is Ted had mentioned it but I want to emphasize it is that you
can name them right whereas you can't name a structor right um and that's very helpful um I was going to say the uh
having static methods like static methods are are generally the easiest methods to test because they require nothing
else um because by definition there is no be there's no there well you unless you have static data in which case you've
got deeper problems don't do that please um but if you got a static method uh is generally easiest to test because
there's not much else it needs other than what you hand in its parameters um static factoring methods are generally uh
relatively easy to test expect yeah so that's that's also another terrible way of of doing where where it's now you now
you've got so what i is describing is is like almost the um like a microservice approach where like nobody nobody can
have have the actual data they always have to ask to to get that information because there's no way to pass that
information along um and if you if you design it correctly like with proper boundaries for Aggregates right so I talk
about boundaries right there's there's classes of boundaries um package is is one level is actually kind of two levels
up um but really like Aggregates which is groups of objects that work together uh there you have you know clearly
defined thing that is your what you want to refer to is with identifiers because that's the thing you load uh and modify
uh from from Storage um so there it might be appropriate for IDs to be passed around but uh if you're constantly re-
retrieving the same stuff then then you there's a clear problem with with who's responsible for what um that's just
terrible and I bet your performance sucks um and perhaps made up by caching wrong uh kleich okay thank you I like I like
to try and pronounce names correctly although with with usernames you know they're all over the board and so that may
not even be a real name so uh static methods are not thread safe well I generally do just don't worry about threading I
gotta be honest I pretty much 99.99% of the time really just don't worry about threading I let the framework or other
stuff do it where uh I just make sure I don't have contention and then I don't have to we about threading um obviously
that doesn't always apply uh but I just generally especially when I'm thinking about testing I I generally assume that
threading is not going to be an issue yes caching caching makes can can make up for a lot of sins um but can cause it
cause its own problems right hard all right uh do we have another jur to work on or do we need to come up with with with
our next thing I don't know we take a look um let's see technically I think we did J 29 right I think so yeah it's in
memory yeah it may not be called that but we'll we'll fix that soon enough um so yeah so I think we have a choice of of
creating and storing it in a real database um or uh we continue adding functionality functionality so is that an
implicit question um so if we look if we scroll down we can see some of the other things we were looking at down in this
area yeah yeah so adding adding a song and adding songs by the UI so we have sort of the uh what we call the
subcutaneous right we have our service layer our application service layer where we can add songs um and so we sort of
have two directions we can we can push things uh One Direction is push uh push to the right if we're look think about
hexagonal push to the right and write to a database or uh push to the left and I don't know if you have a leaning
towards database side but I don't really have a strong argument Pro a con for either approach so the advantage of
delaying um the database is uh we if we delay the database we can not have to commit to a schema and and consider
database migration but if we're not thinking that we're going to be adding real data then that's not a concern either um
that case maybe it is better to go up to the UI it depends on how because I mean ultimately there's going to be database
are you reading a chat uh I'm just I'm just looking for a picture um go that's not quite the picture I want want I'll
find out later okay um so uh yeah since I don't think we're going to be storing real so the reason why I would be
concerned about the the database is because um right now the the properties the attributes you have for songs we just
got four of them and are we going to add to that how do we migrate that data if we do it's not terribly difficult if
we're just adding columns um but at least we we you know we've get uh more permanent more permanent storage and then the
qu and really the question is is what would that give us so sort of like you know think about what do we know the least
about and what would sort of teach us the most about what's the next step what's the next step of what's sort of unknown
well from that perspective then the UI because they'll start go through the path of what do we want to display what
happens if somebody asks for two themes or even not even asks for two themes but if somebody stores a song with two
themes well that brings up the question of uh uh have sort of a a way to add multiple themes right but if somebody added
how would they add multiple two two songs in a row the exact same song ah different theme right so there's there's some
there's some validation stuff that might might be interesting basically some con rints on on stuff that's added because
we do know that there will definitely be multiple themes per song uh I like in my spreadsheet I have up to four or five
right so in that case we're actually missing we're missing some functionality or at least missing some uh yeah we're
missing certainly missing some functionality right um so test containers are specifically for testing you would not use
test containers for running the application even if you're running it locally on dev you would for that you would use a
Docker uh Docker compose um to bring up a database but test containers are generally for as the name says containers
that are run started automatically when a test executes and then shut down automatically for you um so they're not
generally used for environment uh so I'll I'll Wally ask a an interesting question which is where do you put a piece of
code that might be used by two Services um in general th static methods are are bad because it makes testing harder uh
so if you're using common code that that calls a static method and then you want to be able to test something but that
static method is doing something that you want to substitute for with a test double you can't really do it well you can
but you really don't want to because it would require to use um a tool that we will not really want to use uh so in
general shared code should be injected just like any other dependency that way it's replaceable um so if you need code
that's shared by multiple Services pass it in to the Constructor and have it depend on it just like it does anything
else uh static method calls are the tightest form of coupling that Java has and that makes it really really really
really difficult to work with um I know one company that I've I've done some some work with it is it is at least one uh
it is the bane of their existence and they are spending lots and lots of effort to dig themselves out of static method
dependencies uh that's actually not true FNL um so test containers uh are uh is if you look at what the spring boot team
says is test containers are specifically for testing um they may run in your local environment uh but they are
explicitly for testing if you want containers to run when you run your application that's what the docker composed
support is about um and they they make they made that really clear uh that that that's the separation uh they want um if
you if you've seen something different I'd like to see it because I'd like to that's my understanding from the spring
boot uh team yes so so it's really about who's what is what is the static method being used for um if it's to create
something that's fine fine but if it's being used sort of during runtime as a library of some sort uh as shared code um
that's yeah um so do we want to write the UI or do we want to actually modify uh our current uh use case layer to accept
multiple themes per song yeah I think the multiple themes right I think will definitely well since my spreadsheet of
songs has unfortunately they're done as C well not unfortunately but they're currently done as columns which of course
we probably don't want to store it in a database that way um yeah I didn't think so that's why that's why we normalize
our tables that's why tables yes yeah um so it is a fairly common or it's going to be a fairly common occurrence so yeah
so now we're back to subcutaneous because we could build that out from that and then do the UI for it at a later point
right um I think that's where you were going right yeah that's so so basically do we have an understanding right can we
go just more subcutaneous can we go more against the application layer do we know what what that's going to look like um
is the UI just going to have so is the UI going to just support um multiple theme entry uh and we can and we talk we've
talked about that a bit um about what that might look like like you have there online 52 yeah um and so if we just
assume that that there's some way that we'll do that where uh you can just tack on multiple themes um and they'll and
basically will come in as strings uh because we talked about sort of theme management but if we're not going to worry
about sort of upfront theme management than at least right now then uh then I think we know exactly what we yeah um so
suiga brings up a good point which I think you've already stated but basically would this app be useful if themes yes
but then you would have multiple entries for the exact same song well no that's is it like so how could it prohibited if
F said ad song with theme a and then an hour later I add the same song but with a different theme it's just gonna think
of it as a new depends how it's implemented but yeah okay but my question was because that was would still require um
would let's put it this way is that the way you'd want to use it would you be happy with that no no right that's that's
what I'm getting at like you're Bas by basically saying you're going to work around the fact that it doesn't innately
support multiple themes by entering a song multiple times with different themes to me that that says you really need
multiple themes otherwise it's not very useful yeah I was more saying that how you could if we didn't support it that's
how users would behave right right right they would just start my my qu my question was more like would you really use
it would it be have would it be an MVP would it be something that you'd be happy um assuming the stored stuff in
databases in the UI was there would would you find that useful or would you be like I can't use this yet until it
supports multiple themes because it's your app yeah I mean I could use it but it would be nicer to especially with the
bulk entry to be be able to just SPO it all in be done with it okay so it sound it sounds like we we really need
multiple themes right um so I think that's that's our next Jura line 32 uh sure I was just mimicking this right yeah
minimum level product I love that awesome so this is the advantage of not committing to tables yet I don't know how we'
re going to store this in the database um likely we will have multiple tables but I don't have to think about that
because we haven't done anything with databases yet yeah it's definitely one of the advantages of kicking the database
can down the road yes is yeah yagy is is is a great tool for saying I don't do we have to worry about that yet nope so
let's not uh so what what are our steps here so add a song with multiple themes um is there anything y well you know
what yeah I guess I'll just make it it that's no not what I meant so fuel samples has a table with a single row and a
string column store Json the column solve absolutely we that um and that is certainly even reasonable considering that
we don't use the database for searching uh just for persistence and so yeah now um if we wanted to shift to the using
the database for searching like entries have we boxed ourselves into a corner no it's easy to migrate it's relatively I
mean easy it's relatively straightforward to migrate yeah and even if it's not straightforward to do it from a a pure
SQL you could always do the read write the dual read dual WR uh or dual I guess it's dual read uh sort of upgrade on the
fly or you could just run a uh some code to migrate you only have to really worry about that stuff if you've got
multiple apps talking to the same either multiple instances of an app or multiple apps talking to the same database in
which case you'd have to make sure that everybody's reading the database the way read many um yeah Al I I definitely
prefer server side generated user interfaces over separate frontend or what are called single page applications most of
the time you just don't need that complexity the way of developing is very different but in a good way because you have
all the control on all the generation of the UI in the same place as the code that uh is is storing and retrieving and
and running all of its business rules all right uh so I think that's our next step so okay what uh what do we need to do
for that write a test all right so which test are we gonna write we do this sorry go I was just gonna say so um this
doesn't require an endpoint change right so if we look at our uh controller our song themes controller it's still um
searching for one theme which that that doesn't change uh and we don't currently have an endpoint for creating so
there's nothing to change there right the advantage of of of yagy is the advantage of procrastination is is we didn't we
don't have to undo anything or modify anything we did uh so our our controllers find there's nothing to to do there and
so now we can look at our our application layer uh which is Our Song service um and it has just an ad song so uh do we
now need to split song or does song inherently as an entity as a domain are we having a yeah right now it's just a theme
and a title right in other words turn song into a class that has like a list of themes no longer make it a record right
so basically uh well song could still be a record um but instead of a theme being a string and also sort of a a related
but separate questions do we want uh uh to point we will eventually and is now is eventually now yeah I don't I don't
feel like it it it is uh I'm just sort of I'm just sort of yeah uh so D ask we're thinking adding one theme at once now
the idea is we're for a song you can add one or more themes that are for that song So UI sketch of how to do the um the
theme part yeah or you could put in multiple themes song that could be an optimization so dotus is is you know start
with a theme and then add a bunch of songs for that theme that could be a data entry optimization um but I think that's
just an optimization uh ultimately on the back end it's G it's going to be each song has one or more themes uh spinner
64 asks are we doing bdd tdd or atdd I don't I don't use the term uh atdd very very much um and whether yes I haven't
heard ATD atdd in a long time yeah so for those of you who don't don't know what what that is it's basically acceptance
test uh driven development um and what an acceptance test is versus bdd which is behavior driven sometimes people treat
that as the same I see them as as definitely different uh so you could say and and it's not usually doing multiple of
these right you're doing atdd at the at the outside in a sense that's what we're thinking about right now is we want we
already have a you can enter a song with a single theme now we want to be able to support adding a song that has more
than one theme that's Behavior that's visible from the outside and whether you call that bdd or atdd uh we don't have a
test yet for that um but to me it's it's all kind of tdd Bally you know what you want it to do then you write a test and
then make it do that and yes we definitely are doing development or SD yeah um so suige asked how many how many themes
do you have in the spreadsheet uh I think our cardinality is probably certainly under 10 I don't think you had more than
like four or five columns yeah I think the most they themes this isn't even complete remember that there's there's the
spreadsheet there's word docs there's asky docs I don't think there's any stickies or posted notes but um yeah but you
but but you know we're we're talking certainly just a 10 or under number of themes per per song yes and I definitely see
at this point just in the spreadsheet themes areas we don't need that I know asking cardinality I know yeah yeah so I
mean the yeah the number themes would be important if we had something like a million or something that we have to um so
I don't call it the Chicago style I call it the Detroit style because that's where Ron Jeff and Kent Beck and so on um I
don't like the fact that Chicago is co-opted what what was just invented in Detroit so it's the Detroit style or the the
the KCK style classical um yeah so can I mean Canon tdd uh which is a KC just basically said just to be sure everybody
knows what I'm talking about this is Canon tdd um and the only real difference between what Kent Beck wrote uh and what
we've been kind of doing is we haven't been writing much of a list of tests we're going to write they have done it
occasionally but I don't I don't tend to write much in that way um I've been assured though that that still falls under
Canon um but it's really it's it's there is no difference between that what he wrote and what he wrote in his book 20
years ago he's just basically saying for those people who likely have not read the book this is tdd there syndrome tdd
uh there are a bunch of different styles so so it has gone gotten a bit out of hand there there are several other
location based things and that starts to get into like some differences that actually are important but I don't think we
want to get get into that here um but yeah none of them tell you you need you need a translation table what do you
actually what do you exactly mean by this um and there's there's some articles about that all right um so coming back to
song when we add a song do do we care that I guess when we get a song so here's where we have to sort of think about um
what is this song record used for um when we display the song after after searching we basically display the song We
display these two pieces in fact view uh oh we aren't displaying the themes so do we want to so when you find if you
search for a theme and you find the songs do you need to show the theme for every song this will be a I'm gonna kick the
can down the road um because if you just searching by one theme then you don't need it right but we the TBD is if
somebody's searching for Christmas and Halloween right do they want both or the intersection of the two right which is
pretty much just a a Burton movie basically um no there's probably more than that but you know what I'm saying right um
and so that is unclear what would people would want would they want both lists list of all Christmas songs and Halloween
or do they want ones where they're I mean they literally is a song it's about Christmas and Halloween right so they just
want that one song right and that's the part I'm not sure what people want so feel I don't care what people want I care
what you want well I have never searched for a a double theme at this point okay I'm gonna I'm G to say that we probably
want to uh easily associate the themes with a song because that that feels useful and if we find out not and there's
something that pushes us to to a different direction then we can figure that out at that point um but I I feel like we
we want to continue having a song be uh include the theme as sort of part of that object so that means we're going to
have to migrate from song taking a single theme to a song taking one or more themes right which might take a little bit
of work um might might um refactor to it yeah we might uh do some prepare refact of that and so Durham says doing a
great job learning more about intell great thank you thanks for hanging out so um let's let's drive it in from the test
side and then that might inform us of how we might want to refactor this at what level service level yes so we want to
sort of start from uh from from the outermost layer and here's where could use a diagram you GNA pull one up I'm gonna
I'm gonna pull one up yeah me so uh what we got here is is our hexagon and so inside here are um are song as well
Searcher um but we also have at sort of uh what you might consider a different service flip it I'll flip it this way so
it's sort of this is when we're talking subcutaneous uh we're basically referring to um this thing and so we want to
figure out um how do how do things want to talk to it so what are the things that are going to talk to it are basically
our adapters and so right now we've got our uh web our so we've got got our adapter um we haven't finished this we don't
need to finish this because we basically know what this connection is going to be we know what is what is the adapter
going to need from the song service and uh from a data entry standpoint the song service has a right now has a method
where we say add a add a song um and yeah and so when we're testing they're they're basically the the two levels that
we're testing against we're testing uh at this level uh and we've got tests at basically this level and so there and use
the word level but really they're they're layers um you want to think about this as being another layer this is our
domain layer and so so these are our use case layer tests oops sometimes people call these integration tests I don't do
that because I find that a confusing term uh and then these are um tests so that's kind of our that's kind of our our
our structure uh and so so um what we want to do is when when we're developing new functionality we want to go outside
in so that's why we do this one second and so that's where it's sort of outside in because we're starting at the outer
layer and then we're we're looking at the at the inner layer and we may bounce around but idea so um and this is also
called cutaneous is just below this the the skin is kind of this what does it look like from from the truly from the
outside users will so that's our architecture code so um add what do we have what do we have at this layer we've got uh
do you want to bring up just the full yeah so we' got um save songs are loaded so we've got stuff around saving and
loading um we made sure they saved to the repository uh and when we add songs they're found by their theme let's take
one yeah so that's exactly right so um the idea is that none of these tests right there are there may be tests that we
want out here but that's a separate issue but none of these tests um even are aware of the idea of HTTP that's long gone
that's handled only uh only here this is this is the place that deals with HTTP once you get to this connection right
here this dependency right here now we're talking just code no no network no nothing which means it can be screamingly
fast yes and that's that's the the the main goal of most of our tests is that bio so uh so what are we doing here with
the song service we add a song add a song and then search so um so I think we should do we want to create another test
like multiple songs with multiple themes or yeah or do we want or do we want to modify this test where one of the songs
we add has multiple themes w yeah this is about that so if we make the second song a different theme we want it to be
the same song yeah I think that's gonna get confusing so let's let's write another test because as you said that where
where we're what we're testing is that they're found by the theme and now it has multiple themes I feel like that's a
separate test now right and just to be doing j23 at a song with so there's actually a little bit more baked into that um
yeah there's songs with multiple themes so we want to be able to find a song and then so finding and adding I think are
two separate things so we want to be able to add a song that has multiple themes and we want to be able to find a
matches right yeah it's it's likely that there's a schema out there somewhere um but we're writing a a Spoke application
so we get to decide what what's important to us yeah this does not surprise me there's lots of good schemas for stuff
yeah and I I generally look at at this kind of stuff to help inform what I might want to consider and perhaps naming of
of things uh but uh we want just what we um I don't know that we can Implement ad working in the sense that I don't know
oh if it can we we can certainly do a prepare uh but if we actually added a song with two the and pretended that it was
only theme one uh without modifying the the the search by theme to look AC crossbow themes we could never tell that
adding that song right so I think we're going to need to do find a song uh that has find a song if one of its themes
matches one of its themes match one of its theme matches match yeah verb tenses um I think we're gonna want to do first
so we're gonna have to manually manufacture some data that without using ad to make sure we have right so let's do that
let's go to our um what were you going to say yeah let's go to our song Service and I think we just write another test
where a song has multiple themes and is found by the the second theme oh right because if we change new song on 17 or
make a line like line 17 where instead of it accepting new year it accepts a list which includes New Years right right
right so we might have to do no yeah I guess we'll find out pretty quickly what we need to do parallel parallel change
or or what on this one um we'll do we'll we'll be able to do parallel change okay new test with multiple multiple themes
is found by all themes by all themes by all by by uh I want to say by any of the themes that it has that's what I'm
saying by by all that's what I mean by All Things by anything is any okay I sure any of those themes yes I don't really
know way of phrasing yeah a song with multiple themes is found by any of those that's fine yeah it's not great it's good
enough but yeah good enough I hear it's easy to change test method names okay you don't even have to refactor uh so yeah
so let's let's go ahead and um bring that into yeah view a little bit so we're gonna do something very much like that
except instead of uh two songs we're just going to add one but it's going to have multiple themes yeah I hesitate to do
this but I'm GNA anyway this would actually be set up um yes so at this point we're going to be like can we do list
stuff here we can do whatever we want here it won't compile but we can do whatever does AR work of cool so what are uh
go ahead and hit enter because you didn't finish the oh completion yeah um so what do what what would another theme be
for this song or yeah I don't want to use this song i g get into or use another song where where this is one of only one
of multiple themes yeah let me S something with multiple themes and just go from there that would be terrible OA not
that it never happens for a good reason but um that's why I kind of even for test method names I tend to to just do
rename easy oh okay because at first I'm like that has nothing to do with New Year's no I was moving away from that yeah
okay in some ways it's a canonical example um um there's nothing wrong with the syntax aren't I um well we said that
that that that was GNA happen oh right right right because we didn't change yeah well we make oh it's a record right so
we can't do it it's not an object so we can't make a second Constructor that takes the list no we could convert the
record to his class uh we can also create um a static Factory method that's allowed inside of record oh that's sweet
okay I'm not sure if intellig will support doing that let's let's find out want we have to manually do it from here we
will probably have to manually do it yes um you want to try something um I think we should probably do a prepare
refactoring to prepare us for this um since now we know what it's GNA look like there's no reason not no reason um I was
thinking of do do we want VAR args VAR ARs with records are not a good mix uh so I think we will we might make a
convenience method for a song with one theme but that would only be for testing anyway so I think it's pretty clear we
want our song record to be uh a list of string and not an individual an individual string so let's um let's actually uh
uh comment out the test because it doesn't compile so we're just gonna comment it out uh you need to comment The
annotation as well oops test test yeah a special kind of uh can we let's see who uh who's who's calling songs let's look
at all the the callers for the song record who's calling that big um no that's not what we want we want only the
constructors for that is there a way uh we don't want to see Imports turn that anything can we just look for usages of
help yeah no no no no just do find uh that's better yeah um but not any less well if we did case it would wouldn't look
for this one then does this have a case specific uh no but the problem is is there's still a bunch of places where we're
instantiating song um so I think uh let's let's see if intell will allow us to do a chain yeah says it will well let's
see what that actually turns out to be so let's um let's modify let's modify theme want to do that or what if we add the
list of and then no because what I'm hoping that we can we can do and I don't know if change signature will be the right
tool for that uh is uh change the type of theme to be list of string instead of string and have the colors all fix
automatically yeah I don't know if they will though but let's let's see what let's uh before we do this since we're we'
re sort of going to spike our refactor in are prepare factoring let's do a commit and make sure that we're in good know
I can't think of yeah enough yeah um we might want to say what prepare Factor you're doing of song with multiple themes
okay and I feel like we haven't run test in a while so yeah let's run let's run all of them they don't take that long
yeah hey X xammer um yeah so I saw suiga post a link to uh IO free and what I mean by that in in there um but the the
shorter answer is if it doesn't touch Hardware right it doesn't read files doesn't read from IO it doesn't deal with
HTTP doesn't deal with messaging um you can guarantee that those tests are going to be fast because the only thing that
slows things down is Io if it's running in memory runs super fast and one of the advantages of fast is you're not
nervous about running tests you're not like oh I can't run tests I don't have time for a coffeee break right now um
whereas if you can just keep running them all the time Y and speaking of coffee thank you for 64 um so prepare ref
factoring um I'm just curious I don't think I don't think change signature is going to help us but I'm just curious to
to try it so let's signature uh and so let's modify theme uh instead of list instead of list so Alt Enter Alt Enter can
do it from there whoa yes that's cool I don't know why it didn't Auto Import it interes but whatever whoa what are weird
oh close that window I'm not sure why that popped again why is it showing all these options Jakarta is that the one we
want the first one yeah I don't know why it's showing all those other options but yeah you want the first one uh and
let's change the name the themes I know we're kind of doing two things at once but let's see what broke I expect that uh
yeah no look at broke everything yeah yeah okay look at all the red in the gutter yeah blood in the streets so uh back
um so I think uh let's let's have intellig create this uh um basically Constructor does that mean like turn it from a
record to a class or and then turn it back to a record or um that's one way of doing it you can also I think if you do
an Alt Enter on on song itself um on there um well it doesn't offer it as an option uh do you think the um chain
signature would work if it was a class instead of a record well if it's if it's a if it's a class I mean we could do
this with a record as well um it's just not going to write the Constructor for with um it might it might just be easier
with turn it into a class s just said all insert in the body should do it oh that let's try Constructor uh we want the
canonical one because we've already got the compact one why are those windows so small that's so weird Okay um and think
how interesting it's redundant but if we change signature on this yes so if we basically change well the thing is we
don't want to change we actually want to change the component so let's go do it uh let's just change um let's change
string theme to just just be a list of string without going through the change signature at this point no not that one
on the record itself on the record itself okay so technically that is called the record component so we are changing the
record component uh you can't do arc on that because it's not an argument yeah it would be nice if we could do that but
it's not yeah uh and now um other than the problem with line seven which is going to be very easy to fix right so we
just do on the right side of that de of that assignment we say list of yep um oh what's that yeah so that's saying a
non-canonical record Constructor must delegate to the Constructor do we say do we can we not do it through the
assignment do we just do this uh so let's do is it going to offer anything to fix with Alt Enter no let me get it back
there I jumped um that's weird what did it do before because I thought I saw so I think I was over here somewhere else
me from here no uh go back to to song Enter I saw something where it was going to assign a new array list to to theme uh
oh I think that was no only we could do instant replay of the video um presentation assistant is doing yeah but it was
it was where the matters uh this is where it gets confusing to me with with records so we've got there it is oh there it
is um had the chis on the word theme on line seven oh that's but that's not going to help us that's actually not uh we
could do that I don't think it's gonna make a difference just try it out see what happens which one um there only one
yeah um yeah so that doesn't doesn't really do anything for us it does do the right thing because we no actually it
doesn't matter undo that uh so do we just can we just not I don't understand uh because it's a non-conical Constructor
it can't differentiate between the two uh or with records once you create do we need to call this is that what it was
saying by not delegating um meaning like yeah so what if we do this and pass in no not not DOT all right but this and
because why is that a I guess because we fully filled out the I don't know that's an interesting aspect of records that
that I'm confused about why there is a difference between that must be just basically a rule about records that you can'
t do the assignment to the components directly um I guess if we did it as a class and then converted it to a record yeah
it would it would be it would probably be more more clear um although we may not be able to then convert it back to a
record successfully so right right but it's interesting I didn't think that assigning the components directly was a
problem because we were using the correct types uh but clearly that records don't like that all right do you want that
blank line on six what's that do you want the blank line on six usually classes you like it but it records I gonna ask
what you do yeah records I don't I feel like for something like that it's um oh I actually don't have an opinion but if
you're going to put that space then you got to put a space on the other side as well because then it feels unbalanced
mean at eight and a half uh yes got it so does this do what we want let's tests right because theme is now a different
component type right right right right uh yeah yeah and this is actually the the the Crux of the problem um of multiple
themes is how in a sense do we index them because what this what this unnamed what this Constructor is basically doing
theme right um yeah so so sui mentions uh we could just ass if this is a true prepare refactoring then we could just do
do first uh which will return the First theme in that list um and that should be backwards compatible but it it does
mean that this is where uh we're going to have to do some non-trivial fixes so let's do that uh so right where no where
you were um just put a DOT first there oh there oh is it dot first no it's get first okay yeah yeah I think so can you
can you do a an F1 on the get first that's sequential why is it not showing help separate window uh sorry then I didn't
want F1 oh okay it must be a different keystroke on Windows uh control Q r q yeah that's a new one oh quick
documentation why did they do that I think I I think I remember reading this in the in the in the Jeep um when they
introduced sequential collections uh and I was very puzzled why they put a get in front of it instead of it just being
DOT first which is what I'd naturally think of it as oh well it is what it is yep again all right so our our prepare is
done because all we've done is basically said instead of having a single theme as a string we have a collection and we
only look at the first one uh so the behavior is completely the same the structure is now different and so I think that
is is our prepare refactoring but we're still going to have lots of songs that are passing in a single theme have to be
changed to list no no because we've created a Constructor that's backwards compatible oh right so that was the
Constructor so now we have two Constructors um one that takes just one and I think we'll keep that because for our tests
if we only need one that's fine um and then if we need need multiple then we can explicitly add multiple okay it's the
record syntax I'm still that's probably why I kept saying I want to see the class yeah well I mean you you can go ahead
and convert it to a class and take a look and then UND yeah yeah no now I get it it's but let me actually let me do it
anyways just uh was Al enter was it all enter is yeah so now you see they're basically two two um but the record was
clearly more compact Al this one's and so here yeah I mean it's basically this one delegating to that one this one's
delegating to that one yeah yeah so basically the one that's backwards compatible is delegating to to one which is as it
should be right which is as it should be yes the the full Constructor is always the one that is Constructor undo yes uh
so the pig cat 76 I love that name uh asks why use a list over over what I'm presuming you're saying VAR args and
because VAR args with records uh don't play well together um because you define the record components also become um the
accessors uh and it's just really ugly um plus we really don't want to use arrays if we can get away with it because we
actually do want to store the stuff as as lists so arrays uh you may not have seen it but we've already sort of bumped
up against the annoyance of why um how much more do we want to go today we kind of blew past our original end time let
me just see if there's any well I don't know that we had an end time today we had a start time oh we did I guess yeah I
guess mentally I was thinking two hours um let me just quickly check to see if the world is burning down or not uh
meaning if there's any text messages go let me just check email too yes um no I could I probably could go another 15
okay I was just wondering if want if we want to take a break or not so if we're only gonna go another 15 then we'll just
do that that's what I think all right uh but we've got our prepare factoring all our tests pass so commit if only the
cursor was on the right sometimes actually so I think we can just say yep so now we can go and uh uncomment test so
we've added the song I do a theme and we want to do any so we could just pick one I think we can be more specific and
and uh say that we want not the First theme mean in the title found I think we can say by Maybe by its theme yeah right
because we know that finding it by its first theme we know that already works the previous test is basically testing
that um this one we basically want to find it by its second theme and since you pinched that in assert actually me use
that cool new got in fact this one you could say a I don't know I don't I forget we create we didn't create that
shortcut view I don't think we yeah yeah so AC is is basically assert that something contains exactly that's what I use
because I do that a lot uh now and this is this is this is annoying um what I would actually say is we don't we just so
we could basically just instantiate the song the same way it did on 30 and that that should just work um I don't like
that uh because it feels it feels weird but but really what we're interested in is that the title that we get get
matches um but we could start with just instan in the same song and then and then or we could map it uh to just get out
yeah um I'm kind of with see that this is ugly doing the same thing as on 30 what would the mapping look like uh so
instead of contains exactly extracting yep and it would be song colon colon title ah and then an uh then we would say
contains exactly and then nightm nightmare ref Before welcome uh and yes I think I agree suiga um themes always felt
like it should be last anyway somehow it ended up being first uh but now certainly that it takes multiple values it it
really does feel like it needs to be last yeah luckily yes all right fail because there's still I don't know what the
code is I believe we're just looking at the first one in all situations we're just looking at the first one so it's just
going to be empty um so we're it's going to be empty so we're not going to find any song yep um so let's find the code
that's basically doing the indexing which was the song The the song was in the song Searcher right I think so this just
delegates so it's interesting um is this test might be at the wrong layer level yeah like we're too far away uh it's
fine for now but I think once it passes I think we could probably just push it closer um but the reason why we start
here is we don't necessarily know required yes exactly it's like no that's just the wrong order took forever for me to
fix that I don't know why um that's an inside joke for those of you who was like what is he talking about uh for the
longest time in a blackjack game we're working on uh the the definition of a card was was um suit first and then rank
but whenever I talk about cards I always say you don't say Hearts Ace you say ace of hearts you say three of clubs two
of spades and so being backwards is just terrible um so where do we actually do the indexing is in song Searchers
Constructor right that's where that is yeah so um in fact I I feel like we we actually might want to pull this out into
its own method called index songs by theme because right now it's not obvious what that does right completely yeah so
let's let's do that and then even though it's basically the entire thing that you're you just told me what I must be
tired that means I have to stop soon um what was the name you gave for the method again uh index songs by themes even
though right now it only does singular now um actually undo that let's extract it in in a better way okay uh let's
variable oh no so here you're gonna have to select the line and then extract it to a variable and we're going to call
that song stream one more time there you go um now extract uh uh let's see let's actually just extract from uh basically
this is stream operations so 14 on so 14 to 17 like that yeah because that actually mat returns a what a map yeah so
let's extract that even with the semicolon to the end yeah okay uh extracted to variable oh sorry uh just click yeah
actually without the the semicolon and without the final print so sorry so put your cursor on song stream and then just
just extract method and we'll figure out what it what it asks us oh extract method okay yeah uh so we want with the
collect so the second one yep uh and this is uh index s uh index theme yep yeah that's much better um so we can see that
uh on 17 basically um you give it a stream and it gives you a map um I don't know how we would do this with streams uh
because we'd have to flatten the themes but I don't I don't know how that would work with the grouping buy um so let's
ask intell to convert that to to to for Loops for us oldtimers which part the the entire uh collect uh you might have to
go to song stream itself uh um does it not know how to us it may it may not know how to convert it to to some kind of
looping thing that would be a shame um could do you think that would I don't know you could bummer um I think we should
stop here yep we hav't going for a while flatten it into oh swegi yeah there there's a way we need to to to in a sense
flatten the song into multiple songs with single themes and then index by that and group or group by that um I'm sure
there's a way to do it uh but it's going to be a bunch of trial and error that probably require uh fresher brains than
we than at least going for a while we have yeah yeah so um so this is fine we'll stop here we've got a failing test and
it's failing for the right reason um and so we'll pick it up next time with figuring out how to how to better do how to
index by multiple themes cool are there more um comments that we need to uh no I think y sounds like a tomorrow problem
yes yes that's definitely a tomorrow problem stop sharing my screen y all right uh any any other any final words before
we bit AO I think I need to commit is there anything left to commit there is so let me do that on my machine yeah you'd
be committing a a failing test but I'm fine with that as long as you don't push right even if you pushed it it wouldn't
be a problem because it's just a failing test right right um trying I mean I'd be fine if you didn't commit at all I
don't think that's really yeah okay all right that's all folks uh our next stream we haven't figured out a specific time
but it will be soon um so stay tuned for that and as always uh Discord has the most upto-date information on future
streams as well as a whole bunch of other good stuff uh so if you're not already there drop by uh join up and say Hello
uh otherwise we'll see you next time I think we can say it'll be tomorrow right we do know that much uh we're pretty
sure it's tomorrow okay it's pretty pretty sure it's tomorrow yeah all right folks have a good one see
