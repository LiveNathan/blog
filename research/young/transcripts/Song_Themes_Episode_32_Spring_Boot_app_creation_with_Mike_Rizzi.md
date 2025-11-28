# ＂Song Themes＂ Episode 32： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=ujb_O6myknY

---

## Transcript

all right hello folks welcome to another episode of uh pairing stream with Mike Rizzy streaming uh as usual working on
the song themes app how you doing Mike doing well doing well so apparently a frog just got my FR away uh so last time we
discovered um our failure message messages weren't quite as concise as we uh thought they were or at least as I thought
they were um so uh as in very verbose and as in as in uh redundant and repetitive yeah uh so we're gonna have to just
when we thought we were done with validation we bring this back in welcome Jonas oh you caught the intro all right you
uh so um any thoughts before we dive into don't think so yeah just Dive Dive away all right let's do it so we left off
here yep and I think if I remember correctly we left ourselves a failing test bread from we did there it is I'm going to
use F4 to jump to the test that's right wait a second how come it didn't work uh because the cursor has to actually be
in in that window yeah so you gotta click in it even though it yeah yeah or you could hit alt four to get to that window
get to that window and then yeah so um yeah so one of the problems is that for what's basically one one failure missing
a header row we end up with lots of error messages because we're not checking the failure uh checking the missing row at
all and so we're getting caught in huh there's no column for artist or song title uh one for each missing column of
which there are three um so uh We've now got test for right one for each required column yes one for each required colum
column right right and since there are three required columns we got three errors yeah uh and I thought it was really
interesting that I had predicted that we'd get six because I was looking at the fact that there are two rows except that
it treats whatever the first row is as the column header um and so right the first row is in essent essentially ignored
and then the second row we try to retrieve the predefined required column of artist and song title and theme uh and it
and it fails because there uh and and uh would have been interesting if if you know if we actually had a row of data
that the song title was song title or the artist was actually artist then things would sort of work in a weird way but
yeah uh so ASD asks what is the message if you remove uh one line uh one row from from the test that's a good question
so um um let's say we remove the second or the first it doesn't really matter so what do we what are what's our
expectation well I won't let you guys see to I think it pass and it thinks those are the headers well so it treats it as
the header and then there is no data right um so I believe we do have some kind of failure for the fact that we actually
have no data um nope passes so so it passes but it passes because we were expecting one failure message so we are
getting a failure right not seeing what it is if you tack on to uh the has size say you know is empty which is weird but
we'll we just want to see what the error message is yeah because we are clearly getting a failure message and and my
expectation is that failure message is saying you've got uh yeah must have at least two rows of import data so that's
the single message we're getting and that's great um that's that's what we want uh and AST suspected that it would pass
so good for you um yes the repo is available uh I'll I'll paste a link uh into the chat for that um so let's undo our
done undo what undo the experiment we just did so is empty from from 93 take that out too okay just so there's here so
this is failing what we do want is we want to validate our basically our so what should we do well the message is saying
it's missing the required columns but it's not saying it's missing row right we would like it to to to be one message uh
in fact I think we should actually make this test a little bit more obvious about the redundancy by adding one more row
so that it's clear that we're getting right one failure message for each thing and lot because we want is regardless of
the no uh if there's no header row then there's no point in continuing right okay so here we expect six as as the number
of failure messages and that's what we get and so we can see we're getting six individual failure messages uh so not
only is it is it sort so all right so how do we want to fix this let's see here calling handle import which is calling
import songs which is is so when we're parsing a song but we didn't parse all so we're parsing the whole thing mhm so
it's almost like we want to check is the first row right is then the issue is do we want to do it within the Callum MPP
or Constructor which we talked about last week about yes you know having errors in Constructors are kind of a drag right
um I think that's where we left off I don't think we talked about how we would yeah so we decided that uh or at least we
were thinking that we don't want to do the validation in Constructor wanted to do uh a factory method that returned a
result right because we expect that um so again like this is where is this an exception or is this something that in a
sense is expected that we may get some input where we're missing the column header um and so uh I think we you know we
could certainly throw an exception but that would require us to then wrap it with a TR catch and what would we do in
that TR catch is return a result failure so may as well just return that pretty much right away and I must admit it's
been a little bit of a shift for me to think of what I used to think of as exceptions are now expected right versus
because my brain was always like it was in the on the air on the side not air on the side but if this is shouldn't
happen then that's exceptional or exception but this is a shift in thinking and it's like No it should be something that
we're really not expecting versus a scenario that yeah this could happen yeah so let's deal with it yeah so so would we
um can we refactor toward this by like uh I guess extract 22 into a factory meth or a static method yep we'll have to
change the signature but we can do that as a second step I guess well I was thinking uh we could um internally because
the results yeah internally get a and then inline it well wait a second um if we return a result the result's going to
have either an error scenario you know error information or right the column mapper correct got it so then we'll have to
do a check and if we don't have a column map or we have an error then we never 23 right because we're going have to B
fail point is that right let's see has no failures but that's different set of failures not the one we're checking for
now I was looking at the if statement on uh I wonder well let's let's do it and see what it looks like okay so if I want
to extract this to method and what do we want to call this um create column member um yeah or just create because of
eventually it'll be a method on column true and then can we just where is it to signature ah no wasn't wasn't a shortcut
there isn't one for make static oh yeah actually I I've defined a shortcut because I use it enough so I actually Define
my own shortcut uh I don't know that I mean we could make it static now that's fine I was going to do the static and
then move it but would uh I was thinking before we move it we change its return type okay nope one more keystroke
control signature so I was thinking not not using change signature to change it but to refactor and and and then use
inline to because what we want is is on 22 we don't want to we're not going to get we don't want to get back a column
mapper we want to get a result of column mapper um so what I was thinking is uh in the create method so we can do
internally is um oh I see you're like this column so then at this point we do something where we check the header or do
we well so I'm thinking as a pure refactoring to prepare for what we want right now we're always assuming success so
let's assume success here so basically we're going to return uh a result column mapper that's a success one thing I
forgot to do is turn off my cell phone uh actually you know what this might be something I need to grab all right hey F
right uh so we could directly just change it and then have things adjust but um I'm I'm sort of always playing
refactoring golf so I'm always like can we do this using automated refactorings only uh in this case there's only one
caller so it's probably pretty straightforward um but it's always uh me interesting practice to say is there a way we
could do this using uh using all automated refactorings yeah so if we change the return type then that would uh then
intell would have to figure out how to change the return type and if the method is not returning the type we want it's
not going to really be of much help um so what I want to do first is have inside the method a representation of the
correct return type and then uh introduce that uh sorry in basically inline that so we end up with that as as uh okay
now I'm unmuted yes okay um so I missed what you were saying you have a so let's um let's let's assign uh let's assign
it to a variable we'll here um and then we'll say that equals header um this one yeah and just hit Pinter now hit tab
because that's what we want okay um and then instead of a new column mapper say return result. suuccess values uh does
like the signature change that's because it's values is a list we only want to return ones to do right so that's a
completely compatible method except it's clear that we're doing work that is thrown away um but now if we make sure well
I guess it would still be failing this is a refactoring while we're red yes let's run it we should still expect the same
failure so basically uh uh we'll still get the six yeah yeah um so if we now inline like you want to keep the method or
get rid of it well you have no choice uh I mean you could keep you could keep the method but there's no point in it this
actually want to remove it got it so so this is a the way I think about what we just did is a fancy search and replace
so we extracted something and then we did some stuff and then we inlined it and it's it was all correct because they
were all automated refactorings so now we can do is um re-extract that create and that one now has the correct return
type and now we can move it over make it over the other F6 just the other F6 Max columns to parse oh it's just offering
that because it's also static ah okay so we don't need that we can escalate we're good then right so what we did was we
used extract did some stuff to get the what we want is we sort of want a want the want a different return type and so
what we do is we this is actually something that's that's fairly common uh at least that I do is is extra ex ract it and
then inside create the thing that you want as the new return type and then when you inline it you now have uh what you
want and then you can re-extract now with with the correct return type and there's some other ways to to to do that um
sometimes you want to do that with parameter so you do in introduce parameter um but in this case it's sort of I want to
change the return type and we could have just changed the return type and then corrected it um this is a way to do it
where you never are in an uncompilable State it's cool technique so if we look at column mapper yeah let's go ahead
there um we see our create method now this is now backwards compatible um but now we have done basically a prepare
refactoring to say um well we're we're now a bit closer to to what we want um so the next step would be that we need to
somehow re actually return something besides success checking write the checking the calling code first where it checks
for success or failure or write the create inside the create method test for failure or test for incorrect header um I'm
actually tempted to just return a failure message ah uh that would get the current test to pass and all and perhaps
other tests many other tests perhaps uh failing is there only one failure method yep yeah so it's overloaded so it
either takes an individual message or or so I just want to I want to uh so so asard is not convinced um and that's fine
in this specific scenario there's there's literally one usage and so it might seem like not worth it when you've got
lots of usages um this makes it easier because you you basically when you do that inline back you might be changing 5 10
30 different colors hopefully not that many callers but but any number of callers will all be absolutely correct in
terms of their new uh their new type definitions so if it's just one then then it then it doesn't seem necessarily worth
it although I still do it because it's if you're fluent in it then you just do it quickly and and and it's done um but
uh if you don't if if if you either don't know how many methods are calling it or there's there's more than one then
then I would say this is this is a better way to go and this is one of those things where if I do it in the one case
then I'm basically going to do it all the time because then I won't have to think and choose which option to go I'll
just always do this this way of doing it and the more you do it the more you get stops becoming slow or or seemingly
slower to the point where it's faster um whereas it's definitely slow for me I'm still thinking about it as we do it
right right but getting to that point will be cool yeah where it's and I like and I like things that apply in all cases
so I don't have to make decisions I just do it um and that that makes it even even more sort of automatic speaking of
automatization that we've discussing in our book club um if you if there's only one way to solve it and that always
solves it even if it might be Overkill in some situations then better uh so full novel asks explain the purpose of the
result class uh so we can't use spring internals because we're inside of our our application our application domain so
we can't use spring internals period end of story um and the purpose of result is to basically provide a somewhat
standardized way of returning something that could be a success or a failure what's what sometimes called an either or
Tri um monad various various names from from functional programming um that this encapsulates both with a single return
return value since Java can't return multiple values uh this is this is what we have to do um and the for whatever
reason there's never become a popular enough widely used enough result class in Java uh unlike net where there's a
pretty much a standard um and so you know my goal is is to try to promote more usage of it because I think yes there are
sometimes where you going to throw an exception where it's like you just asked me to change State into a certain way I
know that's not valid and I need to protect myself I'm going to throw an exception versus well maybe it's something that
uh might might be problematic or I mean or this one where it's like hey user you forgot to include the header row right
so then it's a way to get that message back without throwing an exception yeah um even if pair was in the jdk I don't
believe it is it is not fit for purpose right so result is a very specific way of looking at at results there's either
failure or success um and while we don't have the implementation there is a a library that will adopt probably at some
point um that makes it easier to sort of combine a whole series of uh results in um uh what's it called Railway oriented
programming so it's idea that you sort of uh and you can look it up and I'll provide a link to it as well somebody you
get no you get one strike in your out if if you do any kind of promotion on this channel you don't get warned you get
banned immediately um yeah so you could use pair but it doesn't Pro so mainly uh I mean right now result is sort of pair
that has a better name um but with a railway oriented programming you can basically continue to sort of stream and
process the results through multiple steps uh and out at the end you basically get either an accumulation of the
failures or you get a successful result and we're not quite there yet and so that's why we have some some if statements
in in our in our code that we could probably get rid of when we at least some of them that we could get rid of when we
move to class right so it doesn't provide the the the meaning that we want um you could use it but but it doesn't uh so
both for for both reasons we're we're pair um so um that should get our current test to pass pass callar so actually
probably not because we're not we're not checking the result because before it was just a column mapper it wasn't yeah
so do we want to make it that test pass by changing this yes let's let's get the test to pass we just do a fail and bail
uh if result is a failure then yeah oops and how are we doing let me check just do we just return the exting result well
we can't because the type is different ah so we basically have to to sort of just propagate the the failure message so
it'll be yeah where we take this result right. your message right got it okay run the test so we so we so we predict
that the current test that was failing will now pass and then possibly a whole bunch of other tests will will fail I
hope a bunch of tests fail never know huh single failure message is the one that was failing yeah so you can look at the
little Mark uh next to the test view yep check that one passed and yes we saw that other others failed so great um now
all we have to do is yeah so our our basically our hardcoded got us got us a small step so we know that that we're on
the right track um work so are we just going to say hey are you um basically well we want to check that the header has
all three required columns and if it doesn't or if it does right so we're in in sort of red uh right so we want to do
the ugly Whatever Gets the right result no pun intended um whatever gets the okay I'm not seeing a quick and easy way to
do it other than doing similar to what on line 15 parse the columns then check to see if they contain what's in set in
the required columns in the Constructor actually wait a second the par header columns already passed because it's the
Constructor ah yeah all we have is that is is the header right because it's a static method yeah so we'd have to reparse
or not I'm not seeing a quick and dirty way that you're well I mean doesn't I mean it's it's quick or dirty uh I said
ugly I I don't know if I said maybe I said quick but but you didn't it was probably just me basically like it can be
ugly it can be redundant it can be duplicative uh doesn't matter we're not worried about Elegance here worried set so is
there a way this is my lack of asking if this contains all of these and we don't care about the order uh yeah Yes except
uh what we got is a string array so we need to convert that to a a two set oh there is look at that cool well now yeah I
guess that's fine um what's collect oh just because we're ignore it yes so we do we we do want to hold on to um par
header I don't like the name but again I just want to that's fine or header set maybe I trying to you name I'm I'm
basically on in in the Mo of I'm not going to worry too much about it because this code is is going to significantly so
if required columns does not contain all of the par header is that the backwards we want to say does the pars header
contain all the required columns does contains all care about order uh I believe contains all does not care about order
if we did this and just reversed him or does the reversing not matter personal because the way I read it is like we want
to know that the parse header has the required columns not the other way around I mean it's functionally the same thing
well so what we so are is this if statement the success version or the failure version failure okay I I might flip it
and do think about what does the success look like because think about negation yeah negation is hard yeah oh it just
got removed statement doesn't have a flip on it oh really you did the all you did an Alt Enter let me try um so want to
switch it did it wrong because yeah you had the next statement wrong yeah I was commented out yep and now you can get
rid of the other one but so contains all is is insufficient um because uh if the pars header is a true right so
shouldn't we reverse this so it's par header contains all required columns yes that's what I was babbling about earlier
I just wasn't finding the right words for go so let's see does this bring us back out yes excellent cool yeah let's just
ship it right no no no refactor we could sh I was trying to trigger you there I just uh well we've got I mean we could
we could certainly do a a commit right it works right make it work that's true you know make and then uh and then and
then elegant uh so yes asid we we right now the result class is uh is impoverished and doesn't have a good way to
propagate uh other results and so that's something where if we adopt a a more sophisticated result we would get that
kind of thing that's what I was talking about before sort of being able to pass you know and results through um and then
end up with type uh hey there 5G technician if you're asking where our our result class coming from it's a it's one we
wrote um but we'll Pro probably switch to uh a more comprehensive result class at some point feedback yeah I I I still
feel like I don't commit often enough um that's something I I continue to work on uh it's it's very easy to get into the
flow and and just keep keep adding on stuff and going through the tddd cycle um but so we have a choice uh we could
refactor or we could um ratchet up our assertion about the failure message oh and then clean it up afterwards and then
clean it up after yeah I like that approach because then it might affect how the cleanup goes yeah I don't suspect that
it does but but um but it's just a suspicion so yeah y okay let's go back to the test so right now just because now we
get to think about what do we want that error message that failure message to say tell your message is returning what
well okay so actually let's stop um we're at the wrong level for testing what we're about to to test song importer
because we're at the song importer oh we're pretty high up we're we're pretty we're pretty out there yeah yeah um so I
think what we want to do is stop here with uh has size of one is sufficient um and then and then have a test that's
closer in that's looking at parser I'm just doing a crazy navigation so we were in here so do we have a um F4 to the
test no it's control yeah that one up let's see what we got for test methods um so I'm noticing something writing right
away okay speak up uh so again right how easy is it to find what we're looking for all of these tests are starting with
parcel parcel parcel parcel parcel yeah we talked about that last week so uh but let's not let's let's fix that now um I
was going to say let's not do that now because that would put us on a tangent but this will be a pretty short tangent
and we have a clear uh we have a clear thing that we want to do next even we even had this shift toward test naming to
expectation when yeah context so I think the first thing we can do is we can take all the parols um do you want to why
don't you fold all of the the methods that way we can actually work with oh um is there a fold all you're probably
looking for it at the same time you a collapse it's uh collapse all which is control shift something I don't know what
it is because in the presentation assistant it's um it's control shift and that it has an image of the keyboard and I'm
like what the heck is that wow control shift numpad oh numpad minus okay no way that is the craziest one yeah I'm we're
that's like we're gonna assume you've numpad which I guess maybe is an okay assumption on on Windows sry oh it didn't
work um try it again there we go because now what we can do is we can just worry about the uh the method names so let's
make sure all the parcels are grouped together are there any Parcels below no no okay so let's um let's take all the
parcels and just delete it yeah or parcel let's take all the parcel yeah let's take all the word parcel so you can do
the multi cursor thing and then what is it Al J alj uh oh that was the alj yeah oh oh that's a bummer okay um then let's
Let's uh um is there a find and replace that only works on what's visible when you have collapsed text um I don't think
so that what I was looking for is there's a way and I don't know what the keystrokes are uh because I don't I don't do
it very much there's a a way to do um hold out a key and do a mouse click to get uh multic cursors oh uh and I don't
it's not that there it is yeah and so it's option shift on click on on back which would probably be alt shift click so
I'm G to click on this first uh well that's already selected um but move the cursor to just before the P so not
selecting anything and now uh yeah and now do try 29 oh oh 29 yeah so you've already yeah yeah I managed it yeah so
there now do alt shift not capot alt shift click and then click here you holding down alt and shift shift you did
something before that worked oh maybe it was alt alt control now it should be alt shift that's it what did you just do I
was holding down I'm still holding down alt and shift at the same time right that's what I asked you to do is alt shift
and then click oh this is oops I on it there uh oh oh good you can get rid of one this is like this is the the L in
Sublime okay so now I can delete par now them and delete right and delete yes and do they all start with no they don't
no but you could you could un you could unselect a couple of them yeah unselect that one and that one and then go delete
and then R yeah so there there certainly are some some shortcuts that are definitely like that um yeah and this is the
case where sort of Vim like uh stuff is really handy and if I did that a lot more then um they're actually is a plug-in
that can do these kinds of things a bit more fluently but I just I personally just don't do it a lot um like I can count
on you know my my hand how often I do it in the last you know six months um but this is classic there yeah uh so that
was longer than doing it manually but um you know but we learned something but we learned something um so what we want
to do is then select 94 uh and basically cut that oh okay uh and now let's add a nested so add nested at uppercase at
the top nested yeah right where you are yep and then was and now paste the contents inside there so now we've got um
parcel return failure when fewer than two rows parcel returns multiple failure vessages it's not quite still the
expectation first but at least it got rid of some of the the redundancy uh and so now if we look at if you bring up like
uh all the all the methods mean this one yeah so now they're they're you know they're they're a bit a bit easier to read
there's still again sort of redundancy or or repetition between um you know the ones that say returns and the other one
that says uh what um what isn't separate and what something that i' I've started doing is having a different nested
class for failure conditions oh so that way it's like here's the happy scenarios and then here's all usually many more
un unhappy scenarios and then that that enables you to get rid of some of some more sort of again extract that that
duplication and and and make it even easier um but I think this is good enough for now I I I don't want to take up too
much time on this now is there a uh so so I just want to so um it's going to be expand all which is probably uh whatever
the same keystroke numpad minus is gonna be numpad plus of course yeah because minuses collapse and yeah let's go back
to the 66 and so I think I think this is why I thought we had done it is because we had a test where we were G to go and
do now um but you know uh and this is you know speaking of sort of discipline of of doing frequent commits and other
things uh the discipline of not having disabled tests uh it's it's very much um the even though I I don't I don't like
the the underlying analogy of of the broken windows Theory because it's it's actually been proven to be a little bit
whatever um but in this case it it is applicable it's like once you have one disabled test you don't really notice if
you have two three five or 20 right um and that's the same thing like to-dos like once you have one to-do and then
you've got three or five or 10 and you start searching for them it's like that you know uh and I have to admit this is I
struggle with this as well as like keeping my disabled tests to to zero um but hey you know better better late than
never I guess it um and while we're here yeah what do you think parel failure when missing requirements or do you want
to do the expectation what was the format we were looking at expectation when context yeah so yeah so failure when when
missing required header colums yeah so that one works okay good now I also do Wonder like you know the other way around
so again I like I I've I'm not saying expected you know when outcome is is the way to do it what I'm looking for is
what's the easiest to scan and find and if you have a lot of things that say failure when um then I either want to see
can I flip it around or can I move all the failure WS into a single nested class because what I'm trying to do is is
make it again sort of if I look at all the methods can I quickly scan which is the one I'm looking for and I think if we
took all of the failure WS again like I was saying before and Nest those um then you'd be left with uh you know when
fewer than two rows when header row is missing and then you could drop the when and you could just say fewer than two
rows uh had a row missing and now it's really easy to find because what we're looking for different so want that get rid
of that noise yeah yeah especially when it's it's it's I'd like it to become noise in a sense of I'd like to it's not
noise it's it's the duplication so noise would be completely irrelevant it's relevant it's just it's duplicated and
therefore hard to see the what is actually I've got five things that start with failure when what is the what is the
important thing and it's buried inside the middle of of the method right welcome back o nice to see you well should we
create the u b nested class as well uh yeah let's let's do that so astd was saying that uh she nests per per use case um
yeah and and I tend to uh I so one thing I used to do not that long ago is create separate test classes sort of per per
use case um one of the advantages of that is becomes very obvious when you've got a lot of use cases against a CL a
single class that like that class is too big it's doing too much uh but sometimes it actually got hard to name things
and and actually see that and so uh I've been trying out nested classes and it's like that's good enough but now if you
see lots of nested classes then that's now an indicator that that something's not quite right and yes of course we each
have our own definitions of huge based on on experience like yes I I think anything more than 500 lines is huge but it's
all relative all right so a new nested class under parcel um for failure I might I don't I don't I don't know I don't
can I assume we canest again let's let's see what that looks like I don't know that I like that deeply nested yeah in
fact um I'm wondering yeah let's do it and see what win and you can just cut line 21 and down that one too I guess yeah
that one would is considered a failure that is a success so we go there yeah oh it didn't Auto no it won't because it
yeah done then I gotta get the other one this yeah he let's put at the top sure so let's go back to and bring up all the
um actually what's finished okay sure missing and then this one be failure when fewer fewer than two sorry um failure
when this one's a bit unclear this one's weird uh so we probably want to rename that one also I think we decided we
liked the opening triple quotes on the same line on 43 44 yeah so control shift J up up one though nope up here yep ah
right right right right like that because now if you reformat uh it basically just takes one parel failure when you have
to testing failure is problems yeah but so that's the so parsol failure when multiple problems ah and here we could
switch it around say multiple failure messages uh but then the failure when so the failure when I'm not not thrilled
with like the failure is fine but the when is is problematic because I wonder if we should remove the wi yeah because it
forces us into when being the first word which may not be what we want yeah let's just take it out so then we might want
to switch it so it's uh failure multiple failure um we could rename the the nested class with so it's fails with uh one
failure message when missing required so the one where you write are one where you are this one yeah so the important
part is that it fails with one failure message when missing yeah and and fix the typo in on good catch um so the next
one and so this one is is it about the one failure message or is it about checking for fewer than two rows yeah I
probably think that it's that it's uh fewer than two rows is the is the is the more important one fails with multiple
failure messages for multiple problems and then that's it we go with it cool yeah I mean I'm I'm not thrilled with with
the nested the double nesting yeah yeah are we testing when we did this so there are some tests that yeah they're not
testing parcel I think they're towards the bottom yeah this one stop adding them well that one's testing parcel oh it is
oh it's just not within the um we need to move it out right oh now is that yeah problem thing yeah which which I think
it's that one we'll find out in a second this one way this one's also also parcel yep so is there anything that's I
guess we'll find out ah there's par single song well we have already have that as as a nested class right no I know
that's what I'm saying yeah is I noticed that really one test class should be for parse single song and another test for
pars all well yeah and so this is this is what I was talking about before is like do you split these right these are in
a sense two different use cases do you split these with separate test classes or do you split them with nested um and I'
ve been more doing it with nested because still provides the separation but it also keeps them in in one file which does
have some benefits uh first of all for finding things uh and second if you have um common encapsulated setup methods
right but it has a disadvantage of trying to do the second level nesting for failure it starts to make it tough yeah
that's kind of the tradeoff okay yeah should we take our break oh goodness really it's been a while yeah um Yes sounds
great all right so when we come back from our break uh we'll work on the one failure message that we want when we're
missing required hitter columns awesome so we'll see you after our coffee theme break is over n a sh oops all right and
we're back glad you're all enjoying the the coffee breaks stuff was fun to put together welcome all right so before a
break we did some uh moving around of stuff can we just make sure the tests pass I'm but it'll be nice to see muted good
cheap way to find out make sure we're all good all right and how many disabled tests do we have good see none do we have
none okay great that was the only one that was disabled the check is this guy right yeah yeah ignore yeah none all right
thought uh all right so let's write the test that we want to write um we could probably copy uh yeah think the the setup
part let's just copy the whole thing and then we don't need um we only need the the strings everything else is going to
okay oh interesting there we go because we're going to call we're going to call complete completely different method on
a completely thing adjusting par all so that yeah so this the advantage of of doing tdd um probably want to pull in
point because that would prove that we've got really not just good test coverage from a we hit this line during
execution but we actually are noticing and tests are failing when when code changes I've added it to jir one3 cool yes
because we we have seen them fail so they know they will fail they are then what I call valid Behavior change detectors
um and so we've seen them detect Behavior change because we've seen them fail for the right reason uh and then we've
seen them pass for there reason y exactly that's why it's so important to to make sure that they they fail for the right
reason because if they fail for the wrong reason or for not exactly the reason you expected then then you want look uh
so oh you know what before you do that I want you to try something since I think you have the plugin installed um all
right so can use uh uh open up the tools on the left yeah uh can you open up the tree under Tools oh here yeah are we
looking for um host yeah look oh maybe it's in a different place because I've noticed some plugins don't always put
stuff there so like let's look at installed ah it's under it actually is editor uh and it's about half to 2/3 of the way
down because it's not an alphabetical order which is really annoying so it's custom post fix oh annoying huh did you
click on it I did nothing's happening let me click now okay wait that's duplicates yeah it just was delayed okay um
let's scroll down uh to the Java ones you got all the Java ones selected so why isn't it do I actually import some
custom ones that you wrote or Sue wrote uh but but it should have a because it's got the Asser ones there uh the search
a core ones those are selected um why don't you click on the update now button there up above a little yeah oh uh not
sure what changes it apply and then update yeah are you looking for this yes um so it didn't come up because of the
learning hasn't seen me use it yet so right now it's just doing those but if I type as t h okay maybe maybe it doesn't
yeah maybe it doesn't suggest at all if we've never used it okay right um so you don't want one yeah so this's the
problem is is you've got like all it comes with all everything selected when when there's a bunch of stuff that you do
not want to use so look for yeah so yeah I'm not seeing it I don't know why all right let's do it the old and messages
yeah um of the size uh we can do has has size of one right now and that should that should pass because that's the test
basically that we have at the higher level right um and then we can sort of rethink around uh what do we want the actual
error message to say because that's the thing that we we uh we want to start test driving right okay so run it yeah so
we expect it to pass because that's the behavior we tested at the outer layer yep y um so now we can say uh instead of
has exactly and look machine learning suggested missing required header column I'm cool with that I'm fine with that too
do we want a period at the end or not I don't care do you sounds like you do we'll add it you would have brought it up
if you didn't um I also might want but we'll we can take that as as a separate step I also might want um for it to
display what it thinks the header row is right but for now this is this is a a smaller step that we can get and this
will fail this should fail because it doesn't contain that message has the empty string yep so fix so it's inside the
column mappers where we do that yep right here right yep y so then there yep so now it should pass now it should pass of
course it's yeah we'll deal with that in a minute all right and now I think I'd like a colon and then or comma and uh
header like just the name of the current column says missing required header column yeah so I was thinking something
like comma and then hetero was colon ah like this and then percent s kind of angle no we're in the test so we want to be
precise about what we want test missing required header column comma colon so the word header was 26 right right right
we probably don't want tabs here we probably want it since we're already converting it to commas commas and maybe we
want the whole thing wrapped in square brackets or quotes or something kind of like square brackets myself I think
square brackets is is yeah so well fail I think that's what we want yep yeah and it will certainly fail actually no it's
colon it's probably similar to what we have below there I know you took a peek at that this guy uh no below that the
arrays two string on line 646 ah oh this was using perc s got it but we can just we can just concatenate arrays. two
string isn't that what we're what we parsed we pars it to an array let me go see yeah so you can just do arrays. two
string this one oh right on this guy right y it'll and it'll generate the brackets for us it does well I think the two
string will generate the brackets for us I think if you ran it now we'd have too many brackets but let's try it let's
try it yeah let's find out the test will tell us brackets R of that yeah that's why I was saying that that the brackets
are easier because the two string will generate it I was thinking was not having to escape the quotes that too but I but
easier goes yeah yeah yeah yeah okay so that's passing all right um let's do this let's uh what I like to do is swap the
inputs just to yeah wait second wait second wait a second wait a second do we really want that missing requ oh header
was it's not saying what the required headers are right do we want to say that don't you think I mean from a at a UI end
sure it'd be like uh that might be useful yeah might be useful so um so expecting these guys Square bracketed out yeah
we could either put it there or I was thinking could put it in um parentheses after saying missing required header
columns and then in they're I I tend not to to be that I just basically say missing required header columns um oh okay
well so so in this specific case we're missing the entire header row right um so should we have a separate one saying
the entire header row is missing and it should be these three or at least should be that's why I don't that's why I
wasn't convinced that we actually need to say what the what the columns are because this is you're missing the entire
row and that was probably just accidental um if you then have a header row right and you're missing a column we will
actually tell you which column is this yeah yeah I feel like I probably just broke something so I trying to find out
what I did I think we changed the wording slightly yep exactly yeah that's more correct what you have yeah the neurin
yeah now it should pass yeah if it's wrong you should be reading the manual by oh there's a period at the end huh bit by
the period at the end in this case I I would say drop the period I don't I feel like that that's yeah I was gonna it's I
feel like we already have sort of a Terminator that shows that we got to the end of our failure message so yeah it's
good enough all right yep okay cool so let's commit I was just going to say that okay refactor time I think it's now
refactor time yes yay sometimes you just can't wait to get refactoring okay how are we gonna so this is actually
hopefully we won't hopefully ASD hopefully we won't regret that regretting what that causes civilization to fail because
we forgot um so what do we want here I mean we got this duplication well got more than just that too um that could
certainly be put into a method this could be a stat a a private static so it's seen by both this be a static header you
know I I don't like to make SE on I have to um it does get rid of the duplication so I'm gonna offer a different
Solution please yeah go um I'm thinking out loud when I yeah yeah we basically do uh uh um the validation that we want
to do in the Constructor and throw an exception and remove it from remove it from here and just catch the potential
exception and basically translate it to a result got it so if you do so the so the real question is is do we want the
column maper to be public right and if we do then we need to protect we do we we don't really need it to be don't we
would have encapsulate the setup that all these tests are using yeah that's that's easy enough to do I mean I'm make it
private basically extract extract method make it static move it over uh or actually just from here ask intelligate to do
it for us convert to a static Factory method um so that's another option I'm not saying it's it's the it's the best
option uh acquired columns certainly could be static I think that that's not necessarily a bad thing we are we are
defining it statically in the Constructor so that could be that could certainly become a constant right um and it's a
readon variable it's not one we'll ever yeah write at runtime we could provide another columns especially if we make
this one private right so if we make this one private we have a new Constructor that takes parsed header columns and
then just assume and that could be private as well um I mean we might even replace this Constructor with the one that
takes the the pars header columns right uh and that that then becomes private so we get rid of 16 because that is a
constant 17 becomes passed assignment yeah basically um and then we basically do all the validation in the go so let's
start by making this um is there a shortcut to shortcut of course there is don't don't tell me let me look unless I can
find it on my own um is there a way to make it oh inline field uh no no it's it's introduced constant expression cannot
be a constant initializer yeah so what you'd have to do is actually um because it's defined as a field so you can't
introduce it uh you can either uh probably the way I would go is basically tell it to do the Declaration so I think if
you do an uh decoration there we go yeah and then make it static and then make it static I mean yeah as well actually it
doesn't it could stay not static but it's essentially static because it's a final uh we might even want you can't make
it static because it's final well you could make it static um you could just stick static in front of it it's
interesting the refactory when it's gray out um because makes static uh so if you click on required columns it won't let
you make it static uh required columns on the on the variable required columns oh yeah no won't let me I'm not sure if M
static actually is a refractor ing for variables but you literally just stick if you do that I just quickly want to see
if it becomes no still not I don't think make static is is a refactoring for variables it's only for methods okay yeah
all right Jonas have a great rest eliminate this line right will it pick up yes if you do it if you if you delete that
it will then refer to the other one y don't need to explicitly do column MPP or colon required columns here right
because we're already inside the the class okay so this should all keep passing good and then let's see the next thing
we're going to do was to create a second Constructor that takes parse header we I think uh before we do that I'd want to
convert the existing column mapper to a factory method so we change all the usages Oh you mean this one yeah into a yes
uh it's not it's not a refactor it's yep I think we can just we'll have to call it create column mapper for now because
we have the other create method right let's run the test that's just want quickly see so there's no usages of that
anymore right okay well and it made it private so notice that it it made as part of the fix it makes it private got it
running the test again I keep forgetting about that technique for getting rid of all or quickly changing all the tests
basically encapsulating setup in an automated fashion yeah yeah all right so now we can be sort of Constructor you think
just manually or do you have a so I think we will have to change that specific usage back to using the Constructor
because we're about to um yeah because what we want is we want line 24 to call the Constructor because we're going to
change the Constructor to take uh uh to take an array of of the columns so I'm just going to sketch it knowing this
might not compile something along the lines of this new column mapper passing in uh pars yeah so don't do that yet that'
s what it'll eventually get to but I was sketching I wasn't refactoring I just wanted to make sure I understand where
you were going yeah where we want to get to yeah okay cool but but no no but actually you were halfway there which with
the next step which is replace that with the Constructor technically you could do an inline if you want and just uh but
not get but not remove yeah okay right because now what we're going to do is is basically what Astra is is suggesting is
is take uh line 16 and introduce that as our parameter all right p and see how it deletes the header because it doesn't
need it any right and we can now replace the parameter to 23 with the one we already parsed right so here we just take
all this out yeah so again I suggest control right and replace that with par header yep par header or part header uh
columns right all right so let's green now so this is a private Constructor it's the only Constructor this create column
mapper is anybody using this one so that's used by to keep using the factory method that we're not using in production
so in a way this is like a test Factory so in a sense it is a a a teston method uh and we we we will need to because
eventually what what we want is to uh to stop using the one that returns a column mapper and to always use one that
Returns the result a result or column mapper I guess it's like how hard would it be to change all these tests well
actually this one's taking a result oh but a different result though sorry so those tests are sort of all presumably
assuming success so what we can do is we can change line 29 to instead of using the Constructor directly use our new
create method so have 29 delegate to the create uh and then extract the result and then inline it all so it would return
create passing header right and that's it get rid of well that's not it because that returns a result of column mapper
so we need to it it's a little Annoying to have values since we're using this result class in cases where that it's not
a list um it's a little awkward to be using do we do it values but I'm not I'm not sure how else we want to I mean
because if we Implement a method that's called value and it has multiple then what do we do right so I'm I'm I'm unhappy
with that but I don't I don't have a better solution off hand um so no what we want to do is is not that so uh because
we can just do a a values. that right so that's equivalent right just want to prove it no because failure uh and I
actually think those tests are now do we do this slog and go through them one at a time well let's look at at uh so are
these all failing with no such element exception I'm assuming so yeah so what would be interesting is um what's the
actual well there's only one possibility right that the failure message is because the column header is broken and so
this is we are changing Behavior we're basically preventing us from getting to uh so so for example the first test
that's failing the one failure message when one required column is valid right because if you're missing a required
column we won't get to that we're g to we're going to basically say one failure message when one required column is
missing is basically uh you so it's slightly different it's you're not missing the header row but you are missing a
column from the header row but now we detect that earlier so before we wouldn't detect it until we actually tried to
parse that earlier so I think what we do is um revert the change and then basically but we will need to evaluate these
tests yeah here I wonder if there's a better way to to to do this should we revert first or do you want to keep yeah
let's green let's see if we need more than one revert uh whoa what much can you undo at the bottom oh the bottom so
click in the bottom here no in the bottom pane oh in the bottom pane gotcha yeah uh and undo no no don't click there
just click control Z oh got it yeah because you reverted by reverting the you didn't revert you basically roll back the
entire implementation that's not what want right right right right uh so comment out 29 and uncomment 30 because that's
what it was before right okay so what I example of me yeah where I should have paid attention to my brain that was like
in the back of my mind yeah um so what I suggest is we do a a commit and then we can basically make the the change one
by one okay so what this basically refactoring yeah I think factoring yeah y as our European friends drop off ah it's
getting late there have a good night Astro thanks for hanging out yeah um let's remind ourselves of of the the failing
tests so let's swap it back and then uh will it let you from here if you right click on the failing test if will it uh
no it won't you have to jump to Source um and then uh throw in a throw in a bookmark oh that I've not done f11 actually
I forgotten I could just do actions bookmark alt two on a looks like oh it's a toggle bookmark so it's control shift one
on the mac oh look at there's multiple oh so for me it's control because you can have up to nine or well nine that have
key key strokes next to them um but you can have up to 36 ah because it could start using letters it does count zero too
so you get 10 with numbers right yeah yeah um but we don't care how many so we just want to toggle The Bookmark so just
the the letter D that's so weird that doesn't seem right I say toggle bookmark uh oh that one doesn't have a shortcut
next to it oh that's toggle bookmark d That's not toggle bookmark oh I see um if you want to toggle bookmark I guess you
have to toggle oh it's F3 that's what I was bookmark oh it's probably different on well it's probably different on uh
it's f11 for you so was it f11 for you it's not f11 for me that's what we I have three for Mac it says in presentations
that's not confusing at all okay um so what I was thinking that we do is basically bookmark all the tests that are
failing so we don't have f11 F4 f11 so it's five test it looks like yeah oh you just un toggled it because you toggled a
parameterized test ah it's the same oh right so it's really for tests uh yes one that's parameterized correct all right
so let's go through them okay start with this one since we're here um sure go simpler would you rather go with the
simpler one like this one I don't think it's gonna yeah message one failure message when one missing I think this test
goes far song title theme right because it had to have required column in the header yeah well actually there's another
there is a scenario that I we haven't coded for yet is the required headers there but there's nothing in so sorry let me
rephrase it the header is there which includes the three required columns But a row of data is blank for one of the
three required columns we have that we have that uh in we have that in our jira to to look at to look at so that mean
basically so that's an empty cell but that's a very different test than this one than this yeah looks like the next one
is a well ah funny this is the multiple remember when we were surprised about multiple messages we couldn't have
shouldn't have been surprised because look there's three error messages yeah um so it's sort of means that that there's
a validation that we may never see outside of that we may never see um but yeah I think this I think this goes away
because we're calling par song directly but there's just no way that you can get a column mapper uh and so I mean unless
we manufacture a column mapper that's purposely broken which we can't do because it will always require that there be
those three columns right so I okay and by definition this next test well yeah so what's interesting is all our tests
against par song go away because we're testing it now except for sort of the successful ones but like the failure ones
go away because you could never get to par song If your header is broken and that was the way uh interesting so now if
we so you can jump to the next book bookmark what's the keystroke of that uh if you hit uh that one all two it'll window
it's a parameterized one failure when missing one required column yeah again this can't happen either this is going away
sorry and we have a test well so we this one I think we might want to convert because this is directly testing column
mapper um I think this one is in a sense valid but doesn't happen when we do extract column it happens when we create
the column mapper oh we're testing it the wrong the action is in the wrong I mean the executed the action has moved yeah
the behavior that we're actually wanting to test has moved from the extract column right so I think if we if we cut that
one and move it to 31 and a half so if you cut the current line oh current line okay and then move it to there yeah um
we don't care about that result we create so we're gonna get a result of column mapper if we call create instead of
create column mapper oh right okay that's I was just like wait a second this is that one we yeah for slowly getting rid
of usages of yeah we ban we should hopefully end up with no usages of this method right and if you look there's probably
only a yeah six yeah so we'll we'll get rid of those okay so this one just call create instead yeah also takes the
header yeah now the return type's going to be wrong yeah um change the variable we don't right and column MPP or we can
rename result and this should pass depending on yeah oh we and so this is new this is new Behavior oh this is new
Behavior this is the behavior we were talking about before where we were checking only for you're missing the entire
header row or it appears so now we're talking about well you got some of the right columns but you're missing the you're
still missing one or more required ones so this is this is new Behavior I see a bigger problem Oh wait again heter row
was artist release title right because song title is is missing the required it so let's see so that means so uh that
other test that's failing why is that other test failing no no not the those are just variations what's that one failing
about no exception no such element exception ah okay so I think we should fix that one first and then we can go work on
Behavior because I think that one is is going to be relatively easy to fix I was thinking when header column count does
not match count right so I think what we need to row it needs to be yeah I don't need to have four I could use three uh
well our test says four so two I was actually going to do a non-required one let me do that let me go back to right well
theme two is not required that's true I mean you could put in release title if you want but that's why I was thinking
theme two because it's all the way at the end right uh we need to change our test expectation there on 52 at the right
you could just do it run it and just copy and paste if you want we would have that expectation that that part yeah what
yeah oh it did now it's now it's failing as opposed to an except yeah no I didn't see this was collapsed so I was all
right so now that should pass and Behavior okay all right um can we check our our two so that's the one we're currently
working on what's the other one that's the one we just fixed we can remove the bookmark from that one just click I think
so just hit F 11 and I think you can unbookmark the other one because that's the only one we're looking at yeah um we
probably want to do a commit here since we're about to change Behavior even though we're not compiling we're compiling
we're just not we're did oh we did shift to the so one thing I'd want to not is why they're no longer valid because that
may or may not be obvious by looking at the diff right um and here here I'd say because we're checking the header row
upon creation of mapper or maybe are validating the uh instead of when we try to do an extract column yep BD yeah so I
think we can just change our message um five test failed uh so we don't need line 30 anymore more because we're not
passing in any anymore so uh let's see yeah we don't need the first entry anymore we basically just need here's the
here's the header and here's the failure message so we probably want to remove the first thing from our CV CSV and then
swap the parameters so um in the cbsv source yeah yeah we don't column oh column that's over here no no you have it
right it's basically this is comma separated ah right right right okay so this goes y for both of them yep and then get
rid of the uhhuh uh and I think it would make more sense to swap them to basically have the message there it manual is
there no you G have to do this manually okay because the harder part is is the CSV not the those you could swap but it
won't swap the right the test no one so wait a second comma separated which comma so break after the comma yep right
there take everything after the comma and move it to the front after the comma not including the comma quote and you can
delete that comma y total beginning total beginning oh right because we're doing comma right right yeah I'll fix that
and we probably want one more where we're missing the other required column just for completeness sake yeah will that do
it well it'll be what we want in terms of our inputs um our outputs are going to fail because not what we're getting uh
is that what we want probably close right so I think for I think the error message we probably want to have something
different when we've got some columns yeah we have if we have no required columns we're assuming you forgot the header
row right if you're missing if you have one required column then we columns so then our so we might want to add one more
input which is where we're missing two columns which changed the test slightly all right let's get rid of artist just
this uh depends on if we want the quotes or not we could change our air stop using quotes and using uh Square braces
like we use elsewhere that sense I feel like that we gonna break everything so it's not like there's it's not like
there's more want yeah do we do we want to put an S 27 or do we want to just put parenthesis s for all of them yeah I
think I'm inclined for that I'm fine with being a little now now we want to make it work this is calling the corre
correct Constructor or sorry Factory method which is actually I'm curious is the other one still being used yep
splitting so here we're doing contains so it's another right so the success the success is only if if it's all um if it'
s failure now we have to basically say how did it how did it fail right have and if it's missing all three then the
current return on 25 is right is the correct so it's really one or two well if three then we return what we're currently
returning on 25 right and a sense we don't we still don't quite know if you're missing a header row or if you're simply
missing all required columns right because there's no way to tell if if it's a header row really because you could have
theme two theme three theme four you might think that's a header row right and it is it's just wrong um but that sorry
but that would that would well the message does say missing required header row well to me that reads as you're missing
the header row that is required required versus your header row is yes which is which is more accurate and more and more
flexible are you saying reord def I think we should I think we should reword it um so I would say let's disable the
current test let's reword it back okay back to green so let's uh find a test that uses that wording and then we can
change our test and what do we say um missing required Columns of the header row uh I think we would say header is
missing require these the required columns and is it too chatty to say what the required columns are we just have those
have that somewhere no we took it out we were going to put it in but then we um yeah I might put that in parenthesis
here okay now it should fail because it's y so you want you're gonna want to bepper yeah I want to be colon so that
might break any other test that we had relying on that but I don't know we did I think I think this might be the only
one yep yep the only one so now this is in a state where we can start knocking some of these off is that way you were
thinking put that we've way past our break time haven't we uh quick all right so we'll take a break we'll come back um
let's undisable the test and so that way it's failing when pretty cool uh you can look at the test output and look for
the disable test yep that's true there we go yep so that should fail and we'll fix it when we come back there we go all
right so just uh little commercial uh message here um one of the things that you see here on the stream is we do
predictive test driven development and I have created a game a physical board game that um allows you to both have fun
and learn a bit about the process so if you go to td. cards then uh you can find out there's uh more about the game
there's a video here that uh I basically walk through what is predictive test driven development in in detail and then
walk through the game uh and show you what the game looks like how how you can play it um and then you can uh order a
copy and I've still got a few copies left in stock so if you order it ships pretty quickly so again the URL for that is
uh td. cards go to TD cards watch the video um and as always if you have any questions about it you can join the Discord
so I have a special channel for the game and other channels for other interesting topics uh so go ahead and join the
Discord if you're not already a member and I also offer uh coaching so if you want to learn about tdd and actually learn
how to do it in your code um you can either buy the coaching on its own uh or package with the game itself and speaking
of the game since a lot of us are also remote um on my solo stream uh very shortly um I.E this week uh I will be
starting work on creating an online version of the game so it's something I started a few years ago and then put on put
on hold uh and now I'm basically going to revive it uh get rid of the current front end which is in View and use HTM x
uh and regular spring MBC uh for for the UI so you can uh join for that um and that's it and now back yeah let's failing
test got a failing test so it reminds us where we where we left off so this I actually go back to the failing test look
at it more closely so this one is um supposed to be just showing the missing required title yeah so let's make sure that
our the our expected messages are correct because I don't think they're correct anymore yeah what are you thinking is
doing a variant of this yeah so I think that should still be the prefix um for headers missing the required columns um
would we also say what the header that we got is as well well so I think header is missing uh and inside the parentheses
are what columns are are missing so maybe we want to redo redo it flexible got it so this saying so let's go to our test
or you mean the test are you saying adjust the test or adjust the production well adjust the test so we can adjust
production so let's adjust the test that was testing for all missing required okay this way well it's not any of those
yeah so how are you thinking of adjusting I think that's the part I'm confused about uh so start by so we want to make
this flexible to apply to all situations so header is missing the required columns but it's not columns it's column open
s got it and then a colon and then put parenthesis yep now this will fail and succeed and we're back to the
parameterized test failing right and so now we can change our parameterized test to be more right so I would do that
programmatically uh otherwise it's going to be a so I was thinking that we would do it a little bit more
programmatically okay um so it's not the full failure message it's it's sort of the partial failure message because the
only thing that's different columns right right because header is missing the required columns text that's the same for
all of them so when we build what the failure message that we're looking for we can we can build that so what I would
say is is grab header is missing the required columns delete that from each of our parts in in the unfortunately was it
including the space after yep and then delete that cut it oh actually doesn't it's going to work um one second um oh you
could do a it so you can do an Alt J not control J the other Alt J right now now you can now you can cut it clipboard
and then we can go down to our yeah I was figuring I was going to do that yeah actually now I can take care of that
because I had it in the cboard it I think that's right uh yes what I would suggest is we rename failure message to be
names uh and then we want to append the header because that's going to be part of the the message that we're getting is
is there a better way of doing this uh two string well no no it is but the problem is our input is not going to be the
same as our manually we have to par the header no I think we just do it in in column oh just saying what we're expecting
this right just inside uh inside quotes of second you're gonna have to put escaped work so what you just typed from
quote from double quote to double quote needs to be inside 27 needs to be inside of line 27 so select that entire string
oh I see what you're saying yep and then it'll then it'll Auto escape it this comma stays there yeah comma here right
bang right there we go okay yep yep then we need to do the same thing for the other the other ones I guess we I mean we
could do it programmatically I mean it feels is that better which which way do you think is better um because I'm
realizing as we're doing it it's a little Annoying and redundant yeah we could go with programmatically that yes we're
back to where we were uh uh what about um oh noas it was AAS that puts the yeah we want to do an Aras to string but we
got to parse it first right we could steal the parsing code we got in column MPP right well it's literally parse with a
backslash oh okay where I just want to find out where it is I wanted to see H you can see it we were doing split yeah we
were doing split yeah but this case it's going to be it'll be split too right yeah it'll be split yeah so it would be
the same do we need the max columns or not uh we do need it so you can just yeah you can just literally copy that whole
okay a setup I guess maybe I think it's part of setup yeah don't oh it looks like it has that okay great great yeah the
header variable was that yep let's run it see if it's got so we expect only the missing column names to be different
same yeah yeah if you want you can click to see Yeah Yeah so basically it's always displaying all three columns are
missing and now we need to have it stop doing that yep so now back to the production is there a way to say set question
so is there um basically a no it be it would be either distinct or intersect there is a distinct but that's yeah that's
not the distinct we want is there an intersect no no um so we have to go through it one at a time and go it just seems
janky uh no what we basically need to do is um uh can you remove the complete I can see the rest of code uh yeah um so I
think we can do is we can say on on the parse header um so we've got our required columns uh what's what's the type of a
required columns is that also a set I yeah so we can do is we can um make a copy of it and then do a remove all and
columns make a copy of this remove everything in it no oh so make a so let's let's write that out in on line 24 or 25 so
erase what you have there and say required columns no no we're going to write the code oh okay required copy uh actually
we'll have to collect because if we do a copy of Let's do let's do a a set let's just do a new set okay this no no no so
what I want is another variable columns and let's define that as a set of string and we're GNA we're going to assign
that to a new set a new uh hash set with what it says y the first one of the second one no no tab basically what
suggested so we want to make a copy but that a copy that is mutable so we need to make a a mutable copy so we couldn't
use the copy of shortcuts because they create immutable sets so that we have a copy we can say now missing columns.
remove all and look at that intellig why is it want to passing in par header so we're saying here's three columns remove
the ones that are in this other set oh I see so this is how you get a sets which is annoying because these are not terms
that are used with sets there is no Union or intersect or sucky in the concept of sets you mean in yeah so this is this
is where I think somewhat of problematic way that the jdk collections are defined is that you the terms aren't
translated to to to make sense in the context of the specific subclasses so sets to say remove all is is weird because
it's really difference like give me the difference it's not removing all it's removing all the ones that are pasted in
right right so when you when you want difference between two sets you say give set yeah it's weird um and the fact that
it doesn't have uh fundamental thing is frustrating like we we'd have to bring in a library wow uh so um I believe so
does remove all return thing returns a Boolean so it returns a Boolean okay so that just says if if anything was rued or
not um so then I think we can replace what we've hardcoded in columns and because it's a set well I guess let's find out
so we go close yeah it's a set does it convert it to something oh two of them passed so clearly it does um and so now we
just have to figure out why our programmatically is that right no uh I expected is wrong headers machine the required
column theme one but it should be song title In theme one our expectation is wrong so artist from release title release
title shouldn't be in there it should be oh I see but in this case it means song title right this one should be song the
inputs the right it's our output's wrong it's not just theme one oh this one's also it's song title and theme one that
right and this one's all three and this and that one is just artist yeah yeah so yeah we had our so oh the order we not
have control are uh the expected is wrong again what happened which one was it sorry I want to look at it again oh
there's a double square here no that's not the problem yeah so can we look at the one that's yeah yes because you didn't
escape the the remember this is CSV input so turns into a new variable so you need to um for the second and third one
you need to surround those with double quotes ah here no oh around the entire thing from that's why if you look at the
the expected it doesn't even close the bracket right we have song title and then it's a comma right I was wondering
about that that was missing me because it part it stopped parsing at the comma this one so that should that should work
um and then the third one this is the problem with with CSV source and I'm very tempted uh although we'd have a problem
no matter what it was if it was tsv Source then we'd have escape the other thing so because these guys have to be
escaped yeah I mean it's it's okay um I'm not sure any other kind of text based source uh I mean the other thing you we
could do actually that would make this easier is just move to a text block actually just didn't fix is I wonder if the
CSV parser is not strings it looks like it's ignore it's not pay so it looks like CSV source does ouch um well that
stinks uh I need to look at we need to look at oh because it uses a single quote as its delimiter instead of a double
quote which is great because that makes life easier non-standard um the other thing is we could change the delimer uh
overall so we could stop doing that all together um and basically use like a pipe as our separator oh instead of tab you
mean well so instead of comma right comma yeah instead of comma we can just pipe this is just for the test this is just
for the test for this specific test what's the non using a single quote here instead like that no no using a single
quote inside the string oh so instead of where we've done an escape double quote it would be just a single quote whoa I
just curious I want to see it but you're saying it's a little bit hard to visually see I mean I think this is preferable
actually to using a a different delimiter um so I'm fine with this it's just it was unexpected because I I understand
the reasoning for using a single one because then you don't have to escape the double quotes so right um but escaping
yeah didn't work because they decided to use this instead so if we were going to change it you would say make this a
pipe yeah but then it it's I don't know how I don't know uh we'd have to make sure to um ignore leading and trailing
white space and otherwise it'll be harder to read so yeah so I think the way it is is fine okay it's good to know that
we learned something new we learned something yes yeah which we will forget the next time we use it all right so we have
the the appropriate behavior um so now let's let's commit actually let's get rid of this so we don't need this anymore
oh second well we don't need that line um we still need to figure out what we want to do with all the other callers to
call to create column mapper right so we can delete the right sorry I wasn't looking at you yes what yes do we this
comment outline yeah I didn't realize that was a question ah um and then we commit uh can we make that required columns
final so it's private final static oh yeah totally and then we probably want to change it to be shouting uh snake case
oh for this part yeah if you do a yeah screaming caps that's what I call it well that doesn't tell you what the
separator is oh what did you call it again I said screaming snake shouting snake case shouting snake case got it that's
a tongue supporting better error messages or per messages uh we're now B we're now providing which required columns are
missing the failure message now provides now which would be a very different thing yeah and very confusing in the future
all right cool what does jira say does it say we completed a task I think we have completed this entire task yes yep
that correct we haven't done that one yet we have not done done that one um which is mainly 108 is the important
scenario right so it sounds like we should uh call it for today I'm getting there yeah we're at the three-hour Point um
so let's um let's just put a marker that we want to resume from here um maybe also put uh uh that we want to take
another look at any uh we want to eliminate see if we can eliminate so before 106 we want to see if we can eliminate
usages of uh the create column maer that takes yeah I'm not sure if we can but we should be looking to see who's calling
we this one's package level and then that's private and those are private okay good yeah I I pretty much don't think it'
s a canway I think we must because uh otherwise we never get a result yeah got it but at one point I thought You' phrase
it as like you weren't sure with I wasn't sure but now looking at it um now I'm sure okay yeah cool all right cool let's
Commit This yep oh I can still push though yeah you can do yeah all right so next time we'll hopefully finish up our
updates to parsing validation yeah uh and then we can move on to other features other highle features redirect after
import currently goes to yeah that's a tiny thing yeah deployed testing yeah we're gonna have to go back to the mirror
board and figure out what Y Cool all right well thanks for hanging out with us folks um our next uh next stream will be
when will it be um well I'll be streaming solo tomorrow starting around the same time um we may pair stream later in the
week we're not sure yet uh so as always you'll want to join the Discord so you can find out uh well we do have a weekly
book club which reminds me we're coming close to the end of our current book so that means we're going to be selecting
our next book um we'll probably start our next book in the next five weeks um so you'll want to uh join us for that so
you have input into the next book um but join the Discord uh so you can be notified of streaming announcements uh
schedule updates things like that and that's it we'll see you next time
